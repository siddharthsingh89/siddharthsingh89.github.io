---
layout: post
title: Design Garbage Collector
description : garbage collector, system dev, system design,
---

#### Designing a Garbage Collector
Memory is limited resource. Sure, the chips are getting smaller and cheaper but in the end, we can not ship a box with infinite memory. So, programmers have to make judicious use of memory. There are two approaches to memory management.

* Manual Memory managemnt by the programmer
* Automatic memory management using Garbage Collection

**Manual memory mangement** 
This is hard and prone to bugs. Some of the common bugs are Dangling pointers, Double Free etc, As per a statistic by Microsoft Security Response Center, the root cause of approximately 70% of security vulnerabilities that Microsoft fixes and assigns a CVE (Common Vulnerabilities and Exposures) are due to memory safety issues despite intense code reviews,static analysis etc.

**Automated memory management**
Programmers don't have to worry about freeing memory and they can forget after allocating. The runtime collects the unused objects from time to time and provides an illusion of infinite memory.

#### Design Goals of Garbage Collector
* **Correctness** 

A Garbage Collector must not collect live objects which are in use. 

* **Performance** 

A Garbage collector must be as fast as possible. 

* **Less Space Overhead**

A Garbage collector should impose minimal space overhead on the objects.


#### Components of Garbage Collector
**Mutator**

Typically, all components of a language runtime that are responsible for executing application code, allocating/de-allocating new objects, and managing execution contexts get categorized as the mutators.

**Collector**

The Garbage Collector implmented by the runtime. Runs in multiple threads and reclaims memory.

#### Garbage Collection Algorithms

##### Referene Counting
* In this approach, each allocated object contains a reference count field. 
* The memory manager is responsible for maintaining the invariant that at all times the reference count of each object is equal to the number of direct pointer references to that object.

##### Mark and Sweeep


#### References
