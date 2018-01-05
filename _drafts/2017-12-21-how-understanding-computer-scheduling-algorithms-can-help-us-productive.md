---
layout: post
title: How understanding computer scheduling algorithms can help us to be productive?
date: 2017-12-21
draft: true
tags: computer-science education productivity tips
comments: true
toc: ul
description: We all want to get more things done efficiently and quickly. Computers does this very well. So Let's try to understand some computer scheduling algorithms to see how they can be applied to our daily lives to become more productive at our tasks.
analytics: true
---

We all want to get more things done efficiently and quickly. Computers are best at it. So Let's try to understand some computer scheduling algorithms to see how they can apply to our daily lives to become more productive at our tasks. 
<br>
## Problems and Strategies

First things first! You don't want to be late. 

### How to meet the deadlines?

​           If you're servicing customers, you would want each to help each customer as quick as possible. Assuming servicing each customer takes almost equal amount of time, then  you can take them in order they arrived. The ideal commitment or due time for a customer is as soon as they walk into your door. 

Applying the same strategy to tasks:

> You should start with the task due soonest and work your way toward the task due last.

This strategy, known as **Earliest Due Date.** which works best for minimizing lateness. But, we have a problem if each tasks takes varying amount of time to complete.

### How to reduce pending task list?

​	Going back to cutomer servicing anology, if serving each customer takes varying amounts of time, then you would want to service most number of customers. Let's say we can divide customers by type of service and we know typical completion time for each type of service.  Then, the best approach would be to pick customer who needs type of service with quickest completion time. 

This strategy is based on **Moore’s Algorithm** which states,

> We start out just like with Earliest Due Date— by scheduling tasks as they arrive, but when deciding which task to do next, choose the quickest one and repeat this process.

It’s like focusing above all on reducing the length of your to-do list. Also, each piece of unfinished task could be like a carrying a mental burden. Flying through the easiest items will bring some measure of relief.   

It's not suprising that this approach is compatible with the recommendation in [Getting Things Done](http://amzn.to/2CFOsxe) Book to immediately perform any task that takes less than two minutes.              

This is great way to get more things done, But all work can't be equally important.

### How get most valuables work done?    

​        Putting out an actual fire in the kitchen should probably be done before “putting out a fire” with a quick email to a client, even if the former takes a bit longer. 

In scheduling, this difference of importance is captured in a variable known as `weight`. When you’re going through your to-do list, this weight might feel literal — the burden you get off your shoulders by finishing each task. A task’s completion time shows how long you carry that burden, so minimizing the sum of weighted completion times (that is, each task’s duration multiplied by its weight) means minimizing your total oppression as you work through your entire agenda.      

The optimal strategy for this goal is a simple modification of Moore's algorithm:

>  Divide the weight of each task by how long it will take to finish, and then work in order from the highest resulting importance-per-unit-time to the lowest. 

For eg: If you're a consultant, *weight* can be inferred from **money you get**. So simply divide each project's fee by its size, and work your way from the hightest hourly rate to the lowest.

It might be hard to assign a degree of importance to each one of your tasks, but there is a quick rule of thumb:

>  Only prioritize a task that takes twice as long if it’s twice as important.                

But this will bring us new problems, if tasks are dependent on other tasks.

### How to get unstuck?

We might get stuck sometimes because an important task can't be done until another less important task is finished. In computer science this problem is called [priority inversion.](https://en.wikipedia.org/wiki/Priority_inversion) `**Priority inversion** is a problematic scenario in scheduling in which a high priority task is indirectly preempted by a lower priority task effectively "inverting" the relative priorities of the two tasks.`

The practical solution to this problem is Priority Inheritance. That is 

> To get unstuck is to treat the unimportant things as being as important as whatever it's blocking. 

### How to work through continuous incoming tasks?

Life could be easy, if we have finite list of tasks. In reality, it isn't. If assignments get tossed on you at unpredictable moments. The efficient approach is to swtich tasks which is known as [preemption](https://en.wikipedia.org/wiki/Preemption_(computing)) in computer science. `**Preemption** is the act of temporarily interrupting a task being carried out by a computer system with the intention of resuming the task at a later time.` It can be generalized as 

>  Each time a new piece of work comes in, divide its importance by the amount of time it will take to complete. If the figure is higher than for the task you're currently doing, switch to the new one; otherwise stick with the current task. 

But preemption isn't free. It comes at the cost of context switch.

### Why Job burnout happens?

Every time you switch tasks, you pay a price, known in computer science as a context switch. When a computer processor shifts its attention away from a given program, there’s always a certain amount of necessary overhead. It needs to effectively bookmark its place and put aside all of its information related to that program. Then it needs to figure out which program to run next. Finally it must haul out all the relevant information for that program, find its place in the code, and get in gear. The rapid context swiching would cause the performace of the computer to degrade or collapse. This phenomenon called as [thrashing](https://en.wikipedia.org/wiki/Thrashing_(computer_science)). 

You can think of as being like juggling a set of balls. If the juggler takes one more ball than he can handle, he doesn't drop ***that*** ball; he drops ***everything***.

Thrashing is a very recognizable human state. If you’ve ever had a moment where you wanted to stop doing everything just to have the chance to write down everything you were supposed to be doing, but couldn’t spare the time, you’ve thrashed. You are accomplishing nothing at all. You feel exhausted and burned out.

### How to reduce burden of multitasking?

#### Don't keep your plates full.

The best strategy for getting things done might be, paradoxically, to slow down.  One way to avert thrashing before it starts is to learn the art of saying NO.

#### Sometimes random order is better than perfect schedule

One of the biggest sources of metawork in switching contexts is the very act of choosing what to do next. So even doing tasks in the wrong order is better than doing nothing at all in thrashed state. 

Thinking along the same lines, the Linux core team, several years ago, replaced their scheduler with one that was less “smart” about calculating process priorities but more than made up for it by taking less time to calculate them.                

These two principles are called responsiveness and throughput: how quickly you can respond to things, and how much you can get done overall.     

#### Commit doing single task for minimum amount of time

Computer Operating system schedulers typically define a “period” in which every program is guaranteed to run at least a little bit, with the system giving a “slice” of that period to each program.

To utilize this strategy, you should learn to balance between two principles ***responsiveness*** and ***throughput***: how quickly you can respond to things, and how much you can get done overall.

The general idea is that:

>  Stay on a single task as long as possible without decreasing your responsiveness below the minimum acceptable limit. Decide how responsive you need to be— and then, if you want to get things done, be no more responsive than that.

The method to achieve this is [Timeboxing](https://en.wikipedia.org/wiki/Timeboxing) (i.e allocates a fixed time period, called a **time box**, to each planned activity). Another very useful technique is the [Pomorado](https://en.wikipedia.org/wiki/Pomodoro_Technique) that uses a timer to break down work into intervals, traditionally 25 minutes in length, separated by short breaks. 

#### Batch process similiar tasks

If you find yourself doing a lot of context switching, you can also employ another idea from computer science:  [interrupt coalescing](https://en.wikipedia.org/wiki/Interrupt_coalescing). Computers do this by waiting until some fixed interval and check everything, instead of context-switching to handle separate, uncoordinated interrupts from their various subcomponents.       

For eg: If you have five credit card bills, for instance, don’t pay them as they arrive; take care of them all in one go when the fifth bill comes.                

In workplace, holding office hours is a way of coalescing interruptions from co-workers.  Regularly scheduled meetings are one of our best defenses against the spontaneous interruption and the unplanned context switch.                

## Summary

In addtion to kind of scheduling problem you want to solve, you also need to choose right metric to optimize. Because the metric we pick will directly affect which scheduling approaches fare best. 

> In computer science: before you can have a plan, you must first choose a metric. 

Here is the quick guide that summarizes when to choose a strategy based on metrics to optimize.

| Metric to Optimize          | When to choose?                          | Strategy                                 |
| --------------------------- | ---------------------------------------- | ---------------------------------------- |
| Minimize lateness           | You have due dates, All tasks need similar amount of time to do. | Earliest Due Date                        |
| Maximize completed tasks    | Tasks take varying amounts to time to complete. | Moore's Algorithm.                       |
| Maximize the value produced | Tasks are not equally important.         | Weighed Moore's Algorithm.               |
| Minimize stalling           | Tasks depend on other tasks.             | Priority Inheritance                     |
| Increase responsiveness.    | Continous flow of incoming tasks.        | Preemption                               |
| Increase throughput         | Exhausted with multi-tasking.            | Saying NO, Random order, Timeboxing, Pomorado, Coalescing interruptions. |


## Credits

This article is inpsired the wonderful book [Algorithms to live by](http://amzn.to/2F1ZyLy). If you enjoyed this article, consider reading the [book](http://amzn.to/2F1ZyLy) which provides similar strategies for

* Optimal stopping — When to stop looking?
* Explore new things vs exploit what worked best.
* Sorting 
* Caching 
* Bayers's Rule — Predicting the future.
* Overfitting — When to think less.
* Relaxation — Let it slide.
* Randomness — When to leave it to chance.
* Networking — How we connect.
* Game theory — The minds of others.