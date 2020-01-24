---
layout: post
title: Learn more about Stream processing and limitaions of CAP theorem
---


### Stream Processing in Modern distributed systems
Today I was  searching for an reference implementation of distributed transactions in a microservices architecture and came across few Kafka based solutions. These solutions involved utilizing SAGA pattern using Kafka as the messaging layer.

While looking into the details, I got an excellent introductory text, a free ebook by Martin Kleppmann titled [ Making Sense of Stream Processing -Confluent ](https://www.confluent.io/wpcontent/uploads/2016/08/Making_Sense_of_Stream_Processing_Confluent_1.pdf)

I was very much impressed by the simplicity with which Martin expresses the rather complex architectures.
The ebook primarily talks about the utilising the Log(an append only immutable sequence of events) at different places in the modern web architectures. Also, that the write and read requirements are different and can not be optimally satisfied by the Same data Store(which the Enterprise dev community said before in CQRS\Event sourcing architecure), Change Data Capture, Unix Pipelines as compared to modern databases etc.

So Many good things to learn from this text.
And the book is full of references, blog links, Original papers about interesting database research from The Conference on Innovative Data Systems Research (CIDR).



### CAP Theorm : An alternating view

In one of his blog, Martin discussed at lengths about the CAP theorem and how people are using it incorrectly. He defined the three terms precisely first and showed that How the sacred CAP theorem is not the right way to think about modern distributed systems.
[Read the blog](http://martin.kleppmann.com/2015/05/11/please-stop-calling-databases-cp-or-ap.html)


### Know about Dr. Sriram Rajamani : Head of Microsoft Research
[ Interesting Interview ](https://www.microsoft.com/en-us/research/blog/innovating-in-india-with-dr-sriram-rajamani/)
