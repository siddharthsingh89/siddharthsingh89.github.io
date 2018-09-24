---
layout: post
title: Design considerations for database of Web Applications
---

#### Choosing the Database
If you are designing an application which can scale, database scalability is very important in the design.  After all, most of the web apps are a way to add, edit or delete the data in the database.
For example, quora- add  questions and answers in db.

After writing down the requirements, we need to decide the db archietcture. We should ask ourselves below questions-
1. Should we use Relational Database like SQL Server, MYSQl, PostGres etc.
2. Should we use NOSQL Databases like Mongo, Cassandra etc.
3. Should we use both ?

Also, the based on the data needs, We also need to be considered below-
1. Replication
2. Recovery
3. Sharding



### When a Relationanl database can server you better?
A relational database is better when-
1. there is relationship among data and you need joins.
2. when consistancy is utmost important. All or nothing.
4. Structure data.
5. Referential integrity.

Examples- Banking system

### When is nosql database a better choice for powering your backend?
1. Data is not structued.
2. Absolute consistancy is not needed.
3. Data sets are huge.

Example- Social media post.

### How can we use both Relational and NOSQL databases ?
There are scenarios where a mix of relational and no sql can be better.


### Which one to pick among various types of nosqls?
There are many types of NOSQLs
1. Wide column
2. Keyvalue


### Calculating the Storage Requirements for your database

1. Calculate size of columns in the table.
2. Calculate the rows and estimated number of rows for a specified period of time.

### Storing large text data in the database

Consider the use case where we have to store the large text data in the database. For Examples, a Q& A website like Quora storing answers, Blog posts in wordpress etc.

Relational Database provide special fields for these type of requirements-

In SQLServer,we have nvarchar(n) and  nvarchar(max) fields which  can store up to 2 GB of unicode text data.
Similarly, in MYSQL, we have the four TEXT types as TINYTEXT, TEXT, MEDIUMTEXT, and LONGTEXT. Here, maximum bytes (4GB) can be stored in LONGTEXT.

Things to consider here-
1. Do you wish to do a full text search on the text stored? If yes, you can think of using a full text search solution like Lucene. Elastic search etc.  




### How to store images and videos in database?
Consider the scenario if we have to store the images in an application.
Example- Profile pictures, Answers having pictures in Q&A etc., Files uploaded by users etc.

If we store the images in the BLOB field of the database, it impacts the performance of queries. While replication is easy, 

We can instead use the file system to store the images or files and store the path of the file in the database. Storing large files in DB slows it down so if your files are bigger, File system is your best bet.

However, In a file system, we loose the ACID properties offered by a database. Files can be manually moved, deleted as well and we wouldn't know if the file exists.

