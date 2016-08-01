---
layout: post
title: What I learnt from uberconf - Software technical conference
date: 2016-07-31
draft: false
tags: conference java programming career
comments: true
toc: ul
description: I got to attend the wonderful technical conference uberconf and I would like share feedback about the conference and summary of my learnings in this post. 

---
I got to attend the wonderful software technical conference - [uberconf](https://uberconf.com/) and I would like share summary of what I learnt from conference in this post. 
 
## Feedback about the uberconf
       
 Before I jump on to summary of the sessions, let me share my impression about the conference. This is one the best technical conference I had attended. I tweeted 
      
 > Uninterrupted flow of food for mind and body.   
 
 The best thing I liked about the conference is that the sessions are 1.5 hours long that gave us enough time to deep-dive and learn the subject. Also, the some of the longer subjects were split into two parts so that we can learn them in depth and do some hands on work.  The speakers are not only experts on their subject, they are good mentors and presented their sessions more engaging style.
 <br>        
 The only complaint I have is that we were given only audio recordings of the session for offline listening. It would be have been great if video recordings are available after the conference. 
  
## Summary of learnings from sessions

###  Twelve ways to make code suck less by [Venkat Subramanium](https://twitter.com/venkat_s)

12. **Schedule Time to Lower Technical Debts :**  if technical debt is not paid back, we’ll end up with technical bankruptcy.
11. **Favor high cohesion:** Narrow, focused, does only one thing well
10. **Favor Loose Coupling:** Tight coupling makes code hard to extend hard to test
09. **Program with Intention:** Most of the time, we program accidentally without deliberate intention. Any code written should have a clear intention.
08. **Avoid Primitive Obsession:** Favor Functional code over imperative.
07. **Prefer Clear Code over Clever Code**
06. **Apply Zinsser's Principle on Writing:** Great timeless book On writing well by Zinsser's for writing English. But very well applies to code. Principles are Simplicity , Clarity, Brevity, Humanity
05. **Comment Why, not What:** Use comments to describe its purpose and constraints. Don't use commenting as a substitute for good code.
04. **Avoid long methods**
03. **Apply SLAP** A method should have a single level of abstraction.
02. **Do tactical code reviews:** Peer reviews catch 60% of defects.
01. **Reduce State & State Mutation :** Messing with the state is the root of many problems.

---
 
###  Evolutionary Architecture by [Venkat Subramanium](https://twitter.com/venkat_s)
                          
#### Why Evolutionary architecture?

* We won't have a good picture of the system at the beginning of project typically when architecture is created. Our knowledge of the system will improve as project mature.
* We should do **enough** up-front design not ~~big~~ up-front design.
* The ***feedback loop*** is extremely important to be able to course correct.

#### Planning for Evolutionary architecture

* When prioritizing stories, analyze both business value and architectural impact.
* Work on most **valuable** and more **impactful** stuff in the beginning.
*  **Scrum Velocity** - *It doesn't matter **how fast** you run, it's important that you run in the **right** direction.*

#### Principles for Evolutionary Architecture
 
 * **Keep it simple:**  Do minimum to meet the requirements.
 * **Reversibility:**  When making a decision, If it is easier to reverse, go for it. If it is hard to reverse, postpone the decision until you no longer can.
 * **Wait for last responsible moment:**  Compare the cost of doing it *now* vs the cost of doing it *later*. 
        
![Last Responsible Moment](https://raw.githubusercontent.com/erajasekar/erajasekar.github.io/master/assets/images/uberconf/last-responsible-moment.png){:height="400px" width="450px"}
 
* **Automated testing** - Without automated testing and feedback, it's hard to make a decision later and verify everything still work.
 * **Triangulate**
    + You don't an interface or abstract base class for everything.
    + Instead, write a class, write another similar class if it happens, then. **triangulate** - extract what is common into a base.
 * **Postle's law** - Follow [Robustness Principle](https://en.wikipedia.org/wiki/Robustness_principle)  Be conservative in what you send, be liberal in what you accept
* **Minimize libraries and frameworks:** Don't build what you can buy (or available open source) . Don't buy (or download) what you don't need. 

---

###  Measuring Quality of Design by [Venkat Subramanium](https://twitter.com/venkat_s)

* Quality of design can be measured using two key qualities ***Stability***  `(I)` and ***Abstractness***  `(A)` of all packages in the application.  Where

```java
     I = Number of classes this package depends on / (Number of classes this package depends on + Number of classes depends on this package)
     A = Number of interfaces / Number of interfaces + Number of classes in this package. 
``` 
    
* The distance from ideal design is computed as `D' = | A + I | - 1` . Where, smaller `D'` is better .
    * The ideal value of `D'` is 0. But don't go for it.
    * `D' > 0.25` is a call for refactoring.
    * `D' < 0.25` is fairly ok, don't put too much effort in lowering. Because it's hard to measure the quality of refactoring.
* All of these can be automatically computed using [jdepend](http://clarkware.com/software/JDepend.html) tool (plugins are available for build systems and IDEs) and tracked in CI tools like Jenkins.

---

###  Parallel programming with Java 8 Streams by [Venkat Subramanium](https://twitter.com/venkat_s)

* Leverage the power of Java 8 streams to easily switch sequential code to concurrent code by using parallel streams.

---

###  Frege for Java Programmers by [Venkat Subramanium](https://twitter.com/venkat_s)

* [Frege](https://github.com/Frege/frege) is a Haskell for the JVM.
* Frege compiles to Java , runs on the JVM, and reuse with existing java libraries.
* If you love **Haskell** and *purely* functional language.  ***Frege*** is a great choice.

---

###  Software Architecture Fundamentals by  [Neal Ford](https://twitter.com/@neal4d) and [Mark Richards](https://twitter.com/@markrichardssa)

* We should move from traditional *layered N-tier* architecture to ***microservices*** architecture.
    * *microservices* architecture has high score for most of the architecture characteristics like *agility, testability, scalability, evolutionary*
    * But the major complication is we can no longer manually manage applications, deployments , tests , builds etc. **DevOps** becomes very important.
* ***Service-based architecture*** can be used as a middle ground to reduce complexities of *microservices* architecture.
    * Instead of splitting into thousands of microservices and combine the into *service components*.
* ***Event driven architecture:*** Works best for applications that don't need an immediate response and everything can be asynchronously processed.
    * It's easy to build concurrent, scalable , reactive and resilient applications using event driven architecture.
    * But the problem with the event-driven approach is it becomes  **Really hard** to understand and monitor entire flow. 
* ***Microkernel Architecture:*** can be used to build *core system* to run minimal functionality and support more functionalities using *plugin-modules* .
    * Managing *transitive dependencies* and *plugin-contracts* are the biggest problems with this architecture.

---

###  Why does yesterday's best practice becomes tomorrow's Anti-pattern by [Neal Ford](https://twitter.com/@neal4d)

* Adaptability of software is more important than the predictability of software.
* Evolutionary architecture is crucial for different parts of the application to evolve on its own phase.
* *Microservices* helps to move towards Evolutionary architecture.

---

###   Java Optimizations That Matter by Douglas Hawkins

* Micro-optimizations are just that - not much *valuable*. Modern compilers are smart enough to implicitly do a bunch of optimizations.    
* `java.util.concurrent` is *awesome* , but read docs *carefully*. 

###    Concurrency Concepts in Java by Douglas Hawkins

* There is no automatic concurrency management in Java.  We need to explicitly code for synchronous handling of states during concurrent execution. 
* **Immutability is your best friend**

> Immutable objects have a very compelling list of positive qualities. When you create immutable classes, entire categories of problems simply disappear .

---

###  Distributed tracing of Microservices Architectures by [Matt Stine](https://twitter.com/@mstine)

* [Dapper](http://research.google.com/pubs/pub36356.html) is a research paper on Large-Scale Distributed Systems Tracing Infrastructure by **Google**.
* [Zipkin](http://zipkin.io/) is a distributed tracing system based on **Dapper** . It helps to track complete flow of events in distributed microservice architecture.
* [Spring Sleuth](https://cloud.spring.io/spring-cloud-sleuth/)  provides an implementation of distributed tracing solution for Spring platform based on **Dapper** and provides great with Zipkin.

---

I have summarized notes from only few important sessions. Refer to [this doc](https://goo.gl/F2gT5h)  if you like to read my complete notes on all the sessions I attended.


