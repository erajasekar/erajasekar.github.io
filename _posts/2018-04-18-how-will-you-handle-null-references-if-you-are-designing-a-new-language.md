---
layout: post
title: How will you handle null references if you are designing a new language?
date: 2018-04-18
draft: false
tags: java kotlin computer-science technology programming-languages
comments: true
description: The nullable objects introduces a fundamental problem with type system. Java 8 introduced Optionals to deal with Nullable objects. But it has some flaws. Kotlin has idiomatic solution to Null Safety.
analytics: true
---

Computer scientist Tony Hoare Said:

> I call it my billion-dollar mistake. It was the invention of the null reference in 1965

The nullable objects introduces a fundamental problem with type system. For e.g If you declare a object as String, it doesn’t guarantee that the value is real String or null.

We normally skip null checks based on our assumptions in control flow of code. But when we are wrong, the code crashes with Null Pointer Exception. Java 8 introduced Optionals to deal with Nullable objects. But it has some flaws

## Why Java Optionals is not a great way to handle nulls?

<br>
[Read on Medium](https://hackernoon.com/how-will-you-handle-null-references-if-you-are-designing-a-new-language-b1e4056456fc)
