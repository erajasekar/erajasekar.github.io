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

This post explains how default methods in Java 8 can be as a *trait* to automatically inject logger instances. 

To use logging in Java code, we need to add this boiler plate code in every Java class.

```java
private static final Logger logger = Logger.getLogger(MyClass.class.getName());
```

Like me, most of you would hate copy pasting this line and updating the class name in every Java file. Luckily Java 8 supports default methods in interfaces which can be used to solve this problem. 
<br>

### Java 8 default methods as traits

[Trait]( https://en.wikipedia.org/wiki/Trait_(computer_programming) ) is a programming concept used to define set of behaviors that classes can extend it or override implementation. *Trait* is similar to *Interface* , but it can also provide default implementation that classes can simply use it. *Interfaces* can't have default implementation prior to Java 8 and we had to use *Abstract classes*. But unlike *Interfaces*, a class can't extend multiple *Abstract classes*, so it wasn't to implement *Traits* in pre Java 8. 

Default methods was actually added to support new functionalities to be added interfaces without breaking the classes that implements that interface, but can also be used implement *Traits*. For example, we can define a `Loggable` trait with default implementation like below

```java
public interface Loggable {

    default Logger logger() {
        return Logger.getLogger(this.getClass().getName());
    }
}
```

Then, we can easily use it any class by simply implementing `Loggable` interface like

```java
public class MyClass implements Loggable {
   public void method1() {
        logger().info("on method1");
        ...
    }
}
```

