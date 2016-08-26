---
layout: post
title: Cool Mind reading trick to teach maths to kids
date: 2016-08-09
draft: false
tags: kids teaching education do-it-yourself maths 
comments: true
description: In this post, I will share a cool mind reading trick based on math and computer science fundamentals. It has interesting stuff to teach kids of all ages 3 or even 13.
analytics: true
---

I taught a cool mind reading trick to my kid and she loved playing it. It's based on math and computer science fundamentals and it has interesting things to teach kids of any age 3 or even 13. I'll share the trick, concepts behind it and the things we can teach kids using it.
<br>

## Let's play the game

Think of a number between 1 and 30. In below app, select all the columns you see that number  and hit submit.

<!-- <iframe src="http://embed.plnkr.co/CxbAU7/?show=preview" frameborder="0" width="100%" height="750"></iframe> -->
 

## What's the secret trick?

Play again with below app to reveal the trick

<!-- <iframe src="http://embed.plnkr.co/78COJC/?show=preview" frameborder="0" width="100%" height="750"></iframe> -->

So just add numbers in the last row for selected columns to find the number. Simple enough, Right? Are you to know curious how it works?

## How does it work?

What's special about numbers `1,2,4,8,16` ? They are powers of ***2***. Doesn't it sound related to *computer science?* Assume each column represent a binary digit ( ***0*** or ***1*** ) and 5 columns can make up a 5 bit binary. Then we'll add each number to a column only if binary representation of that number has 1 for the corresponding column. Below demo will help you to visualize it step by step. Use the slider to increment the number and watch how each number gets filled in. As a 5 bit binary can represent 1 to 31 in decimal numbers, we can use up to number 31.

<!-- <iframe src="http://embed.plnkr.co/7Wikwy/?show=preview" frameborder="0" width="100%" height="750"></iframe> -->


Yep, It's based on the binary number system. Basically, we will be converting a decimal number to a binary to fill in the table and converting binary back to decimal while finding the number.

## Adapting it based on kids age

### Younger kids.

You can just write this table in the paper to play with kids. If your kid can memorize column number `16,8,4,2,1`, you can shuffle the numbers within the column to make it more trickier.

### Elder kids.

If kids can write, we should encourage them to make this table by themselves. You can tell them the instructions like this.

> We will be writing numbers 1 to 30 using addition. We can only pick numbers `16,8,4,2,1` to add together and find a way to make resulting sum for each number between 1 to 30. we can add 2 or 3 or 4 or even 5 numbers together. 

## What can we teach kids from this?

### What younger kids can learn from this?

* Addition.
* Teaches addition of many numbers gradually from 2 and up to 5. 
* Tracking a previous result in mind and continuing calculation is an important skill they will learn.
* Constraints and rules: They have to pick from only numbers `1,2,4,8,16` . Working through a problem under given constraints is a useful skill they will learn.
* Subtraction.  To teach basics of subtraction, you can have conversation like this:

  > To place 5, you may ask, we don't have 5, but have 4. So what is needed to make 5 from 4? 
  >
  > We can add 1.   

### What we can teach to Elder kids?

Here are some ideas on what we can teach to elder kids by connecting this to real world applications.

* Introduce binary numbers.
* Talk about binary number system KB, MB, GB comparing it to decimal number system tens, hundred, thousands, millions.
* Tell them that memory capacities of phones and devices are actually listed binary number system. (Eg. 250 GB Hark disk )
* Because all the digital devices know only binary ***0*** and ***1***. It does everything using binary operations.
* Explain why the modern digital world is based on binary. It's because of all the hardware is made from wonderful material *silicon* which is a great semiconductor. It can easily change between stop conducting ( ***0*** ) and start conducting ( ***1*** ) electricity through them.
* Keep going...

## Credits

I actually learned this trick from [keithschwarz.com](http://www.keithschwarz.com/mathtricks/howboxes.php). Thanks to **Prof. Keith Schwarz**.



