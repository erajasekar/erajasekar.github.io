---
layout: post
title: Groovy - Dynamic properties in Config Slurper
date: 2014-12-24
tags: groovy programming github
comments: true
description: In this post I will provide quick tip on how to use dynamic properties in groovy config slurper.
---

In this post I will provide quick tip on how to use dynamic properties in Groovy Config Slurper.
Groovy provides a nice utility [ConfigSlurper](http://groovy.codehaus.org/ConfigSlurper) for reading configuration files
where settings can be overridden to different values for different environments.
<br>

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

Let's say we want to add a property *logRetentionBytes : maximum size of data that a topic/partition can hold allotted
from availableDiskSpaceForData*. It can be computed dynamically by dividing *availableDiskSpaceForData* by
total number of topic/partitions. We can do something like this

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

Here is output value of *logRetentionBytes* reading using ConfigSlurper

```groovy
println new ConfigSlurper("dev").parse(EnvironmentConfigSimple.class).logRetentionBytes; //Outputs: 64

println new ConfigSlurper("test").parse(EnvironmentConfigSimple.class).logRetentionBytes; //Outputs: 640

println new ConfigSlurper("prod").parse(EnvironmentConfigSimple.class).logRetentionBytes; //Outputs: 6400

```

This works. But the code is duplicated and it will be hard to maintain. If we have more dynamic properties, it will make it even worse.
It will be neat if computation logic is written once and dynamically evaluated. Groovy's [Eval](http://www.intelligrape.com/blog/evaluating-expressions-with-groovy-util-eval/)
utility can do the trick.

We can refactor above environment config to add  `calculationParams` property to define properties that will be used as input params and `calculatedProperties` property to define dynamically computed properties.

Here is the revised `EnvironmentConfigDynamic.groovy`

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

Now, we can write `evaluateCalculatedProperties` method that reads *calculatedProperties* properties from groovy *ConfigObject*
and evaluates them using *calculationParams* as input. Then it adds result back to *ConfigObject*.

```groovy
private ConfigObject evaluateCalculatedProperties(ConfigObject config) {
    config.calculatedProperties.flatten().each { k, v ->
            def value = Eval.me("calculationParams", config.calculationParams, v.toString());
            config.put(k, value);
        }
    return config;
}
```

Finally, we can pass result of ConfigSlurper to  *evaluateCalculatedProperties* method to get value of computed *logRetentionBytes*

```groovy

println evaluateCalculatedProperties(new ConfigSlurper("dev").parse(EnvironmentConfigDynamic.class)).logRetentionBytes; //Outputs: 64

println evaluateCalculatedProperties(new ConfigSlurper("test").parse(EnvironmentConfigDynamic.class)).logRetentionBytes; //Outputs: 640

println evaluateCalculatedProperties(new ConfigSlurper("prod").parse(EnvironmentConfigDynamic.class)).logRetentionBytes; //Outputs: 6400

```

### Source Code:

The complete source code of examples in this post is available in [github](https://github.com/erajasekar/groovy-dynamic-properties).
