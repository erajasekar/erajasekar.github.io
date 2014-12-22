---
layout: post
title: Groovy - Dynamic properties in Config Slurper
date: 2014-12-17
tags: groovy programming github
comments: true
description: In this post I will provide quick tip on how to use dynamic properties in groovy config slurper.
---

Groovy provides a nice utility [ConfigSlurper](http://groovy.codehaus.org/ConfigSlurper) for reading configuration files 
where settings can be different for different environment.

Let me illustrate it with a quick example, Given this `EnvironmentConfigSimple.groovy` :

```groovy
//Default values
availableDiskSpaceForData = 1024
numberOfTopics = 4
numberOfPartitions = 4

environments {
    dev {
        //will use default value
    }
    test {
        availableDiskSpaceForData = 10240
    }
    prod {
        availableDiskSpaceForData = 102400
    }
}
```

We can read value for *availableDiskSpaceForData* depending on environment using ***ConfigSlurper*** :

```groovy
println new ConfigSlurper("dev").parse(EnvironmentConfigSimple.class).availableDiskSpaceForData; //Outputs: 1024

println new ConfigSlurper("test").parse(EnvironmentConfigSimple.class).availableDiskSpaceForData; //Outputs: 10240

println new ConfigSlurper("prod").parse(EnvironmentConfigSimple.class).availableDiskSpaceForData; //Outputs: 102400

```

Let's say we want to add a property *logRetentionBytes* : maximum size of data that a topic-partition can hold alloted
from *availableDiskSpaceForData*. It can be computed dynamically based on availableDiskSpaceForData by partitioning it by
total number of topic-partitions. We can do something like this

```groovy
numberOfTopics = 4
numberOfPartitions = 4
availableDiskSpaceForData = 1024

environments {
    dev {
        availableDiskSpaceForData = 1024
        logRetentionBytes = availableDiskSpaceForData / (numberOfTopics * numberOfPartitions)
    }
    
    
    test {
        availableDiskSpaceForData = 10240
        logRetentionBytes = availableDiskSpaceForData / (numberOfTopics * numberOfPartitions)
    }
    
    prod {
        availableDiskSpaceForData = 102400
        logRetentionBytes = availableDiskSpaceForData / (numberOfTopics * numberOfPartitions)
    }
}
```

Here is output value for *logRetentionBytes* reading using ConfigSlurper

```groovy
println new ConfigSlurper("dev").parse(EnvironmentConfigSimple.class).logRetentionBytes; //Outputs: 64 

println new ConfigSlurper("test").parse(EnvironmentConfigSimple.class).logRetentionBytes; //Outputs: 640

println new ConfigSlurper("prod").parse(EnvironmentConfigSimple.class).logRetentionBytes; //Outputs: 6400

```
 
This works. But the code is duplicated and hard to maintain. If we have more of such dynamic properties, it will make it even worse.
It will be great if computation logic is written once and dynamically evaluated. Groovy's [Eval](http://www.intelligrape.com/blog/evaluating-expressions-with-groovy-util-eval/)
utility can do the trick.

Here is the revised `EnvironmentConfigDynamic.groovy` that uses *calculationParams* to define properties that will be used as input
and *calculatedProperties* to define dynamically computed properties.

```groovy
calculationParams {
    numberOfTopics = 4
    numberOfPartitions = 4
    availableDiskSpaceForData = 1024
}

calculatedProperties {
    logRetentionBytes = 'calculationParams.availableDiskSpaceForData / (calculationParams.numberOfTopics * calculationParams.numberOfPartitions)'
}
environments {
    dev {
        calculationParams.availableDiskSpaceForData = 1024
    }
    test {
        calculationParams.availableDiskSpaceForData = 10240
    }
    prod {
        calculationParams.availableDiskSpaceForData = 102400
    }
}
```

Now, we will add *evaluateCalculatedProperties* method that reads *calculatedProperties* properties from groovy *ConfigObject*
and evaluates them using *calculationParams* as input

```groovy
private ConfigObject evaluateCalculatedProperties(ConfigObject config) {
    config.calculatedProperties.flatten().each { k, v ->
           // println("Evaluating: ${k} == > ${v}");
            def value = Eval.me("calculationParams", config.calculationParams, v.toString());
           // println("Evaluated: ${k} == > ${value}");
            config.put(k, value);
        }
    return config;
}
```

Finally we can read value of *logRetentionBytes* reading using ConfigSlurper by calling *evaluateCalculatedProperties* method

```groovy

println evaluateCalculatedProperties(new ConfigSlurper("dev").parse(EnvironmentConfigDynamic.class)).logRetentionBytes; //Outputs: 64

println evaluateCalculatedProperties(new ConfigSlurper("test").parse(EnvironmentConfigDynamic.class)).logRetentionBytes; //Outputs: 640

println evaluateCalculatedProperties(new ConfigSlurper("prod").parse(EnvironmentConfigDynamic.class)).logRetentionBytes; //Outputs: 6400

```

