---
layout: post
title: Log4j - Separating log lines to multiple log files.
date: 2014-08-27
draft: false
tags: log4j java tutorial
comments: true
redirect_from: "/2014/08/log4j-separating-contents-to-multiple-log-files/"
---

It's generally good practise to partition the log lines of your java application into different log files based on functionality/module etc. 

For eg. In a web application, we would want application log lines to be logged in to `server.log`,  whereas information about remote user who made the requests to be logged into `request.log`.

This can be done by defining two appenders in log4j properties and configuring them to output to two different log files. 

Here is the example log4j properties.

<iframe id="preview-iframe" src="https://doculet.net/doc/fb1114639d5a47e7b2110c006da4b720"
 align="middle"
 height="650"
 width="100%"
 frameborder="0"></iframe> 

We have defined two appenders, ***fileAppender*** to output to `server.log` and ***requestAppender*** to output to `requests.log`. 
Only ***fileAppender*** is added to ***rootLogger***, so any `Logger` instances created by passing java class will be logged to `server.log`.

Example code snippets showing how to log to `server.log`.

```java
public class RequestProcessor {

    private static final Logger logger = Logger.getLogger(RequestProcessor.class);
    
    private void handleRequest(HttpServletRequest request){
        //This message will be logged to server.log
        logger.info("Processing Request");
    }
}
```

To log to `requests.log` the `Logger` instance should be created passing `requestLogger` as logger name.

Example code snippets showing how to log to `request.log`.

```java
public class RequestInterceptor {

    private static final Logger logger = Logger.getLogger("requestLogger"); //Should match name of logger 
    
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        //This will be logged to requests.log
        logger.info("Received request from user: " + request.getRemoteUser());
        return true;
    }
}
```


 
