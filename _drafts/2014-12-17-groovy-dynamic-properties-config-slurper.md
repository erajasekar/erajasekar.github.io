---
layout: post
title: Groovy - Dynamic properties in Config Slurper
date: 2014-12-17
tags: groovy programming github
comments: true
description: In this post I will provide quick tip on how to use dynamic properties in groovy config slurper.
---

Groovy provide nice utility [ConfigSlurper](http://groovy.codehaus.org/ConfigSlurper) for reading configuration files 
where settings can be different for different environment. Here is quick
[example](http://groovy.codehaus.org/ConfigSlurper#ConfigSlurper-Special"environments"Configuration) on using ConfigSlurper to read
properties for different environments.

```groovy
println evaluateCalculatedProperties(new ConfigSlurper("dev").parse(EnvironmentConfigDynamic.class)).logRetentionBytes
println evaluateCalculatedProperties(new ConfigSlurper("test").parse(EnvironmentConfigDynamic.class)).logRetentionBytes
println evaluateCalculatedProperties(new ConfigSlurper("prod").parse(EnvironmentConfigDynamic.class)).logRetentionBytes


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

another

```groovy
numberOfTopics = 4
numberOfPartitions = 4
availableDiskSpaceForData = 1024

environments {
    dev {
        availableDiskSpaceForData = 1024
        logRetentionBytes = 'availableDiskSpaceForData / (numberOfTopics * numberOfPartitions)'
    }
    
    
    test {
        availableDiskSpaceForData = 10240
        logRetentionBytes = availableDiskSpaceForData \/ (numberOfTopics * numberOfPartitions)
    }
    
    prod {
        availableDiskSpaceForData = 102400
        logRetentionBytes = availableDiskSpaceForData / (numberOfTopics * numberOfPartitions)
    }
}
```

