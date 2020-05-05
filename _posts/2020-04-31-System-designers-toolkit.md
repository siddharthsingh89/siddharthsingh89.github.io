---
layout: post
title: System designers Toolkit
description : system design, algorithms
---

#### System design problmes and commonly used solutions
A popular website like facebook is used by more than 3 billion people. It is not one grand system but composed of thousands of subsystems such as services, tools, databases,  programming languages, algorithms etc. Here I have listed some common problems of large scale system design and how various organisations solved these problems. Many comlex problems can be solved using a specialized Algorithm which or some special data structure but there is always a trade-off. 

Here, I will provide some idea about the problem, how it is solved and what is the tradeoff. 

##### Counting 
 * Hyperloglog
 * CountMin sketch
 
##### Storage
 * HDFS - (Storing images)
 * Fast Write- LSM Storage engine
 * Indexing - B+ Trees
 
##### Ranking
 * Self-Balancing BST (outputs Rank in logN)
 * Skip Lists ( Rank in logN, used in REDIS, Level DB etc)

##### Millions of small processes
 * Actor model - Akka 
 * Erlang processes

##### Search 
 * Inverted Index
 
##### Recommendation
 * Collaborative filtering
 
##### Location
 * QuadTree
 * R-Tree
 * Geohash

##### Rate Limiting
 * Leaky bucket
 * Sliding window

##### Peer-2-Peer 
 * Distributed hash table
 
 

#### Various Algorithms

##### Collaborative Document Editing -
  * Operational Transform
  
##### Recommendation System 
  * Collaborative filtering

##### Checking if something exists fast
 * Bloom filter





