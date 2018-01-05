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

We all want to get more things done efficiently and quickly. Computers does this very well. So Let's try to understand some computer scheduling algorithms to see how they can be applied to our daily lives to become more productive at our tasks. 
<br>
# Introduction

Let's define few key terms  for easier understanding.

## Choose Right Metric

> In computer science: before you can have a plan, you must first choose a metric. 

Because the metric we pick will directly affect which scheduling approaches fare best.

Here are some example metrics to pick.

* Minimize lateness
* Maximize number of completed tasks.
* Get more valuable things done.
* Avoid burn outs. 
* Increase responsiveness or reduce waiting time.

## Category

Tasks can be boardly categoried as Independent (or unblocking ) tasks and Dependend ( or blocking ) tasks. 

### Independent tasks

Independent tasks doesn't require some other task to be completed before it can be picked up and also doesn't block other tasks from being run. TODO eg.

### Dependent tasks

Dependend tasks will have a pre-requisite. For example - in laundry drying can't done until cloths are washed first. 

So it's useful to organize the tasks by categories for efficient scheduling.



## Problems and Strategies

First things first! You don't want to be late. 

### How to meet the deadlines?

​           If you're servicing customers, you would want each customer to be helped as quick as possible. Assuming servicing each customer takes almost equal amount of time, then  you can simply take them in order they arrived. The ideal commitment or due time for a customer is as soon as they walk into your door. 

Applying the same strategy to tasks, you should start with the task due soonest and work your way toward the task due last. This strategy, known as **Earliest Due Date.**

This works best for minimizing lateness. But, we have a problem if each tasks require varying amount of time to complete.

### How to reduce pending items?

​	Going back to cutomer servicing anology, if serving each customer takes varying amounts of time, then you would want to service maximum number of customers. Let's say we can divide customers by type of service and we know typical completion time for each type of service.  Then, the best approach would be to pick customer who needs type of service with quickest completion time. 

This strategy is based on **Moore’s Algorithm** which states,

We start out just like with Earliest Due Date— by scheduling tasks as they arrive, but when deciding which task to do next, choose the quickest one and repeat this process.

It’s like focusing above all on reducing the length of your to-do list. Also, each piece of unfinished task could be like a carrying a mental burden. Flying through the easiest items will bring some measure of relief.   

~~By pushing out the tasks with largest processing time, we optimize on minimizing the sum of completion times.~~

It's not suprising that this approach is compatible with the recommendation in Getting Things Done Book to immediately perform any task that takes less than two minutes.              

This is great way to get more things done, but what do you do if all work is not equally important.

### How get most valuables work done?    

​        All work can't be equally important. For eg: Putting out an actual fire in the kitchen should probably be done before “putting out a fire” with a quick email to a client, even if the former takes a bit longer. 

In scheduling, this difference of importance is captured in a variable known as `weight`. When you’re going through your to-do list, this weight might feel literal— the burden you get off your shoulders by finishing each task. A task’s completion time shows how long you carry that burden, so minimizing the sum of weighted completion times (that is, each task’s duration multiplied by its weight) means minimizing your total oppression as you work through your entire agenda.      

The optimal strategy for this goal is a simple modification of Moore's algorithm: divide the weight of each task by how long it will take to finish, and then work in order from the highest resulting importance-per-unit-time to the lowest. For eg: If you're a consultant, `weight` can be inferred from **money you get**. So simply device each project's fee by its size, and work your way from the hightes t hourly rate to the lowest.

It might be hard to assign a degree of importance to each one of your tasks, but there is a quick rule of thumb:

>  Only prioritize a task that takes twice as long if it’s twice as important.                

But this brings us new problems, if tasks are dependent on other tasks.

### How to get unstuck?

We might get stuck sometimes because an important task can't be done until another less important task is finished. (TODO : example may be tax filing). In computer science this problem is called [priority inversion.](https://en.wikipedia.org/wiki/Priority_inversion) The practical solution to this problem is Priority Inheritance. That is to get unstuck is to treat the unimportant things as being as important as whatever it's blocking. 

### How to deal with continuous incoming work?

Life could be easy, if we have finite list of tasks. In reality, it isn't. If assignments get tossed on you at unpredictable moments. The efficient approach is to swtich tasks which is known as [preemption](https://en.wikipedia.org/wiki/Preemption_(computing)) in computer science. **preemption** is the act of temporarily interrupting a task being carried out by a computer system with the intention of resuming the task at a later time. It can be generalized as 

>  Each time a new piece of work comes in, divide its importance by the amount of time it will take to complete. If the figure is higher than for the task you're currently doing, switch to the new one; otherwise stick with the current task. 

But preemption isn't free. It comes at the cost of context switch.

### Why You might get Job burnout ?

Every time you switch tasks, you pay a price, known in computer science as a context switch. When a computer processor shifts its attention away from a given program, there’s always a certain amount of necessary overhead. It needs to effectively bookmark its place and put aside all of its information related to that program. Then it needs to figure out which program to run next. Finally it must haul out all the relevant information for that program, find its place in the code, and get in gear. The rapid context swiching would cause the performace of the computer to degrade or collapse. This phenomenon called as [thrashing](https://en.wikipedia.org/wiki/Thrashing_(computer_science)). 

You can think of as being like juggling a set of balls. If the juggler takes one more ball than he can handle, he doesn't drop ***that*** ball; he drops ***everything***.

Thrashing is a very recognizable human state. If you’ve ever had a moment where you wanted to stop doing everything just to have the chance to write down everything you were supposed to be doing, but couldn’t spare the time, you’ve thrashed. You are accomplishing nothing at all and feel burned out.

~~Human clearly have context switch overhead too — time lost to metalwork, to the logistics of bookkeeping and task management. The more you take on, the more overhead there is. At its nightmarish extreme, we would be accomplishing nothing at all.~~ 

### How can we deal with such job burnout?

#### Learn art of saying NO

One way to avert thrashing before it starts is to learn the art of saying. 











Yellow highlight | Page: 118

Drop Everything: Preemption and Uncertainty                

Yellow highlight | Page: 118

The best time to plant a tree is twenty years ago. The second best time is now.                

Note:Check out this quote.

Yellow highlight | Page: 118

In both cases, the classic strategies—Earliest Due Date and Shortest Processing Time, respectively—remain the best, with a fairly straightforward modification. When a task’s starting time comes, compare that task to the one currently under way. If you’re working by Earliest Due Date and the new task is due even sooner than the current one, switch gears; otherwise stay the course. Likewise, if you’re working by Shortest Processing Time, and the new task can be finished faster than the current one, pause to take care of it first; otherwise, continue with what you were doing.                

Yellow highlight | Page: 119

offers a simple prescription for time management: each time a new piece of work comes in, divide its importance by the amount of time it will take to complete. If that figure is higher than for the task you’re currently doing, switch to the new one; otherwise stick with the current task. This algorithm is the closest thing that scheduling theory has to a skeleton key or Swiss Army                

Yellow highlight | Page: 119

Jason Fried says, “Feel like you can’t proceed until you have a bulletproof plan in place? Replace ‘plan’ with ‘guess’ and take it easy.”                

Yellow highlight | Page: 121

Computers multitask through a process called “threading,” which you can think of as being like juggling a set of balls. Just as a juggler only hurls one ball at a time into the air but keeps three aloft,                

Yellow highlight | Page: 121

“shows up as you add more jobs to the multiprogramming mix. At some point you pass a critical threshold—unpredictable exactly where it is, but you’ll know it when you get there—and all of a sudden the system seems to die.”                

Yellow highlight | Page: 122

Think again about our image of a juggler. With one ball in the air, there’s enough spare time while that ball is aloft for the juggler to toss some others upward as well. But what if the juggler takes on one more ball than he can handle? He doesn’t drop that ball; he drops everything.                

Yellow highlight | Page: 122

This is thrashing: a system running full-tilt and accomplishing nothing at all. Denning first diagnosed this phenomenon in a memory-management context, but computer scientists now use the term “thrashing” to refer to pretty much any situation where the system grinds to a halt because it’s entirely preoccupied with metawork.                

Yellow highlight | Page: 123

Thrashing is a very recognizable human state. If you’ve ever had a moment where you wanted to stop doing everything just to have the chance to write down everything you were supposed to be doing, but couldn’t spare the time, you’ve thrashed.                

Yellow highlight | Page: 123

And the cause is much the same for people as for computers: each task is a draw on our limited cognitive resources. When merely remembering everything we need to be doing occupies our full attention—or prioritizing every task consumes all the time we had to do them—or our train of thought is continually interrupted before those thoughts can translate to action—it feels like panic, like paralysis by way of hyperactivity. It’s thrashing, and computers know it well.                

Yellow highlight | Page: 123

Another way to avert thrashing before it starts is to learn the art of saying no. Denning advocated, for instance, that a system should simply refuse to add a program to its workload if it didn’t have enough free memory to hold its working set.                

Yellow highlight | Page: 124

a thrashing state, you’re making essentially no progress, so even doing tasks in the wrong order is better than doing nothing at all. Instead of answering the most important emails first—which requires an assessment of the whole picture that may take longer than the work itself—maybe you should sidestep that quadratic-time quicksand by just answering the emails in random order, or in whatever order they happen to appear on-screen.                

Yellow highlight | Page: 124

Thinking along the same lines, the Linux core team, several years ago, replaced their scheduler with one that was less “smart” about calculating process priorities but more than made up for it by taking less time to calculate them.                

Yellow highlight | Page: 124

These two principles are called responsiveness and throughput: how quickly you can respond to things, and how much you can get done overall.                

Yellow highlight | Page: 124

And the best strategy for getting things done might be, paradoxically, to slow down.                

Yellow highlight | Page: 125

The culprit is the hard responsiveness guarantee. So modern operating systems in fact set a minimum length for their slices and will refuse to subdivide the period any more finely.                

Yellow highlight | Page: 125

Establishing a minimum amount of time to spend on any one task helps to prevent a commitment to responsiveness from obliterating throughput entirely: if the minimum slice is longer than the time it takes to context-switch, then the system can never get into a state where context switching is the only thing it’s doing.                

Yellow highlight | Page: 125

Methods such as “timeboxing” or “pomodoros,” where you literally set a kitchen timer and commit to doing a single task until it runs out, are one embodiment of this idea.                

Yellow highlight | Page: 125

To find this balancing point, operating systems programmers have turned to psychology, mining papers in psychophysics for the exact number of milliseconds of delay it takes for a human brain to register lag or flicker. There is no point in attending to the user any more often than that.                

Yellow highlight | Page: 126

The moral is that you should try to stay on a single task as long as possible without decreasing your responsiveness below the minimum acceptable limit. Decide how responsive you need to be—and then, if you want to get things done, be no more responsive than that.                

Yellow highlight | Page: 126

If you find yourself doing a lot of context switching because you’re tackling a heterogeneous collection of short tasks, you can also employ another idea from computer science: “interrupt coalescing.” If you have five credit card bills, for instance, don’t pay them as they arrive; take care of them all in one go when the fifth bill comes.                

Yellow highlight | Page: 126

Likewise, if none of your email correspondents require you to respond in less than twenty-four hours, you can limit yourself to checking your messages once a day. Computers themselves do something like this: they wait until some fixed interval and check everything, instead of context-switching to handle separate, uncoordinated interrupts from their various subcomponents.                

Yellow highlight | Page: 127

At human scale, we get interrupt coalescing for free from the postal system, just as a consequence of their delivery cycle. Because mail gets delivered only once a day, something mailed only a few minutes late might take an extra twenty-four hours to reach you.                

Yellow highlight | Page: 127

In academia, holding office hours is a way of coalescing interruptions from students.                

Yellow highlight | Page: 127

regularly scheduled meetings are one of our best defenses against the spontaneous interruption and the unplanned context switch.                

Yellow highlight | Page: 127

Donald Knuth. “I do one thing at a time,” he says. “This is what computer scientists call batch processing—the alternative is swapping in and out.





