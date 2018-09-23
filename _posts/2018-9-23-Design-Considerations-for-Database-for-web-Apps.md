---
layout: post
title: Design considerations for database of Web Applications
---

#### Choosing the Database
If you are designing an application which can scale, database scalability is very important in the design.  After all, most of the web apps are a way to add, edit or delete the data in the database.
For example, quora- add  questions and answers in db.

After writing down the requirements, we need to decide the db archietcture. We should ask ourselves below questions-
1) Should we use Relational Database like SQL Server, MYSQl, PostGres etc.
2) Should we use NOSQL Databases like Mongo, Cassandra etc.
3) Should we use both ?

Also, the based on the data needs, We also need to be considered below-
1) Replication
2) Recovery
3) Sharding



### When a Relationanl database can server you better?
A relational database is better when-
1. there is relationship among data and you need joins.
2. when consistancy is utmost important
3. All or nothing.
4. structure data.
5. Referential integrity.

Examples- Banking system

### When is nosql database a better choice for powering your backend?
1. Data is not structued.
2. Absolute consistancy is not needed.
3. Data sets are huge.

### How can we use both Relational and NOSQL databases ?
There are scenarios where a mix of relational and no sql can be better.


### Which one to pick among various types of nosqls?
There are many types of NOSQLs
1. Wide column
2. Keyvalue


### Calculating the Storage Requirements for your database

A sample for a Q& A site is given here-

size of columns
Total size of row

### How to store images and videos in database?


### File System vs the database for storing images

