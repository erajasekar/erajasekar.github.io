---
layout: post
title: How can you create flexible enums with different behaviors and associated values?
date: 2018-04-27
draft: false
tags: java kotlin computer-science technology programming-languages
comments: true
description: t’s hard to implement enums for classes that has slightly different behaviors. But it’s easy to implement it using Kotlin’s sealed classes. It makes code concise and error safe.
analytics: true
---

Enums are great to group objects with similar behavior. They are also efficient because only one instance of them will get created. However, it’s hard to implement enums for classes that has slightly different behaviors. Let me illustrate with an example.

## Example: Stats Calculator

Let’s say we want write a Stats Calculator to compute mathematical statistics for list of values for eg. SUM, COUNT, AVG, QUANTILES . Let’s first define an interface.

<br>
[Read on Medium](https://hackernoon.com/how-can-you-create-flexible-enums-with-different-behaviors-and-associated-values-ed42c69be02e)
