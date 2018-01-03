---
layout: post
title: How understanding computer scheduling algorithms can help us to be productive?
date: 2017-12-21
draft: false
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

Independent tasks doesn't require some other task to be completed before it can be picked up and also doesn't block other tasks from being completed. TODO eg.

### Dependent tasks

Dependend tasks will have a pre-requisite for example in laundry drying can't done until cloths are washed first. 

So it's useful to organize the tasks by categories for efficient scheduling.



## Problems and Strategies

### Minimize lateness

​           If you're servicing customers, you would want each customer to be helped as quick as possible. Assuming servicing each customer takes almost equal amount of time, then simply you can take them in order they arrived. The ideal due time for a customer is as soon as they walk into your door. 

Applying same strategy to tasks, is to start with the task due soonest and work your way toward the task due last. This strategy, known as **Earliest Due Date.**

This works best for minimizing lateness. But, we have a problem if each tasks require varying amount of time to complete.

### Minimize number of tasks delayed

​	Going back to cutomer servicing anology, if serving each customer takes different amount of time, then you would want to service maximum number of customers. Let's say we can divide customers by time of service and we know typical completion time for each type of service.  Then, the best approach would be to pick next customer who needs type of service with quickest completion time. 

This strategy is based on **Moore’s Algorithm** which says,

We start out just like with Earliest Due Date— by scheduling tasks as they arrive, but when deciding which task to do next, choose the quickest one and repeat this process.

By pushing out tasks with largest processing time, we optimize on minimizing the sum of completion times 



 out our produce in order of spoilage date, earliest first, one item at a time. However, as soon as it looks like we won’t get to eating the next item in time, we pause, look back over the meals we’ve already planned, and throw out the biggest item (that is, the one that would take the most days to consume). For instance, that might mean forgoing the watermelon that would take a half dozen servings to eat; not even attempting it will mean getting to everything that follows a lot sooner. We then repeat this pattern, laying out the foods by spoilage date and tossing the largest already scheduled item any time we fall behind. Once everything that remains can be eaten in order of spoilage date without anything spoiling, we’ve got our plan.



>  Do the difficult things while they are easy and do the great things while they are small. - LAO TZU



Minimizing the sum of completion times leads to a very simple optimal algorithm called Shortest Processing Time: always do the quickest task you can.

Yellow highlight | Page: 110

(Perhaps it’s no surprise that it is compatible with the recommendation in Getting Things Done to immediately perform any task that takes less than two minutes.)                

Yellow highlight | Page: 110

it’s like focusing above all on reducing the length of your to-do list. If each piece of unfinished business is like a thorn in your side, then racing through the easiest items may bring some measure of relief.                

Yellow highlight | Page: 110

A task’s completion time shows how long you carry that burden, so minimizing the sum of weighted completion times (that is, each task’s duration multiplied by its weight) means minimizing your total oppression as you work through your entire agenda.                

Yellow highlight | Page: 111

only prioritize a task that takes twice as long if it’s twice as important.                

Yellow highlight | Page: 111

you’re a consultant or freelancer, that might in effect already be done for you: simply divide each project’s fee by its size, and work your way from the highest hourly rate to the lowest.)                

Yellow highlight | Page: 114

What happens in a priority inversion is that a low-priority task takes possession of a system resource (access to a database, let’s say) to do some work, but is then interrupted partway through that work by a timer, which pauses it and invokes the system scheduler. The scheduler tees up a high-priority task, but it can’t run because the database is occupied. And so the scheduler moves down the priority list, running various unblocked medium-priority tasks instead—rather than the high-priority one (which is blocked), or the low-priority one that’s blocking it (which is stuck in line behind all the medium-priority work). In these nightmarish scenarios, the system’s highest priority can sometimes be neglected for arbitrarily long periods of time.* Once JPL engineers had identified the Pathfinder problem as a case of priority inversion, they wrote up a fix and beamed the new code across millions of miles to Pathfinder. What was the solution they sent flying across the solar system? Priority inheritance. If a low-priority task is found to be blocking a high-priority resource, well, then all of a sudden that low-priority task should momentarily become the highest-priority thing on the system, “inheriting” the priority of the thing it’s blocking.                

Yellow highlight | Page: 116

But in 1968, Lawler proved that this is no trouble as long as you build the schedule back to front: look only at the tasks that no other tasks depend on, and put the one with the latest due date at the end of the schedule. Then simply repeat this process, again considering at each step only those tasks that no other (as-yet unscheduled) tasks depend upon as a prerequisite.                

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





