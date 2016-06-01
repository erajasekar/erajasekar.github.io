---
layout: post
title: Java 8 automatically injecting logger using trait
date: 2016-05-31
draft: false
tags: java8 java functional programming trait
comments: true
description: This post explains how default interface methods in Java 8 can be as a *trait* automatically inject logger instances. 
analytics: true
---

This post explains how default methods in Java 8 can be used as a *trait* to automatically inject logger instances. 

To use logging in Java code, we need to add this boiler plate code in every Java class.

```java
private static final Logger logger = Logger.getLogger(MyClass.class.getName());
```

Like me, most of you would hate copy pasting this line and updating the class name in every Java file. Luckily Java 8 supports default methods in interfaces which can be used to solve this problem. 
<br>

### Java 8 default methods as traits

[Trait]( https://en.wikipedia.org/wiki/Trait_(computer_programming) ) is a programming concept used to define set of behaviors that classes can extend it or override implementation. *Trait* is similar to *Interface*, but it can also provide default implementation. Java 8 added *default methods* in *Interfaces* which we can use to implement *Traits*.

For example, we can define a `Loggable` trait with default implementation like below

```java
public interface Loggable {

    default Logger logger() {
        return Logger.getLogger(this.getClass().getName());
    }
}
```

Then, any class can use it by simply implementing `Loggable` interface without duplicating the code. Eg.

```java
public class MyClass implements Loggable {
   public void method1() {
        logger().info("on method1");
        ...
    }
}
```

Any class can also override the default implementation if it need to be. If a class does lot of logging, calling `logger()` method might add slight performance overhead. So to improve performance, it can cache the value in an instance variable like

```java
private final Logger logger = logger();
```





