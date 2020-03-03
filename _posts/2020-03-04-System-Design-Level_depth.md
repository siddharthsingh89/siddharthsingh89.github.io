---
layout: post
title: System design-Depth and SDE Levels
description : sde, system design, depth, system, interview
---


### Depth in your design

For system design interviews, expectation is different from different levels of SDE. For example, in many companies, there is no system design round for new grads
or people with less than two years of experience. Google is alos one of those companies. For 2,3 year experienced, You are asked to 
choose between a System design round and another DS\Algo round.

However, starting from mid-SDE Level(61\62 at Microsoft, SDE2, L5 at Google or E4\E5 at FB), system design interviews are a must.
Your knowledge about distributed system is assessed by interviewers. Since, there is no absolutely correct one way to design a system
, these questions tend to be open ended and Candidates are expected to drive the discussion.

The interviewers look for below things-
1. A high level design of whole system. 
2. A block digram of most important system components and data flow.
3. Tradeoff discussion around the design which constitutes the major part of the interview.

1 and 2 are easy and Educative.io\System design primer help in creating the high level design. However, third part is crucial.
For a simple follow up like how do you scale your database?

Expectation from SDE 1 : Talk about seperating read and write load, Replication, More DB servers

Expectation from SDE 2 : separating read, write, sharding strategies, Replication, consistant hashing, Using Cache

Expectation from SDE 3 : Above all along with Sharing performance using different sharing keys, busines requiremets and query patterns,
                        CQRS, Event Stores (append only dbs), CAP theorem, Quoram, idea about read and write throughputs of varios
                        databases such as Cassandra. 
And the expectation goes on and on with higher levels!

Thus,it is important to have depth in your design. Ask question while you are practicing, why have I used this database?
Do I need ACID, transactions, aggregation queries in my db requests. Will nosql db will make more sense and why? 
Distributed Systems are going to stay and with all the information available, it is going to be tougher in future with more expectations
even at lower levels.


