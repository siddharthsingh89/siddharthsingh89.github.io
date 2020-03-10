---
layout: post
title: Notes on Task scheduler design
description : task scheduler, system design, system, interview
---

#### What is a task scheduler?
A Task scheduler System offers a service to-
1. Schedule a task which can be executed in future at configurable time.
2. At the time T, the scheduler executes the task.
3. This is useful in Many scenarios- running batch jobs, backup, notifications etc.

#### Functional Requirements
1. User should be able to submit a task to scheduler service.
2. User should be able to see the status of tasks.
3. User should be able to retry, cancel, reschedule tasks.

#### Non-Functional Requirements
1. Highly scalable - should be able to scale to support millions of events.
2. Highly available - should be always available and redundancy should be build at cost of consistency.

#### Core Algorithm
The concept of Micro Batching

#### Important Components
1. TaskAcceptor Server
2. TaskStatus Server
3. Database


#### References
1. [Bistro](https://bistro.io/)
2. [BigBen](https://github.com/walmartlabs/bigben)

