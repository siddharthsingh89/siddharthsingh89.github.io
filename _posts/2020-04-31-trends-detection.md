---
layout: post
title: Design Trend detection System for social networks
description : instagram, twitter, trends, system design,
---

#### What is a Trend?
Displaying Trends is very important features of modern social networks such as Twitter\FB\Instagram and lets uesr discover what's happening in the world. The Wikipedia defination of a trend is-

> A word, phrase, or topic that is mentioned at a greater rate than others is said to be a "trending topic". Trending topics become popular either through a concerted effort by users or because of an event that prompts people to talk about a specific topic. These topics help Twitter\Instagrm and their users to understand what is happening in the world and what people's opinions are about it.

For example, if there is a cricket match between India and Australia and millions of Cricket fans start tweeting on match with hashtag #IndiaVsAustralia. Generally, #IndiaVsAustralia hashtag will be getting at most 100 tweets daily but if suddenly a hashtag gets unsual number of tweets\posts, then it is detected by the Trend detection Systems and added as a trend on twitter site.

#### What it takes to become a good trend?

##### Popularity 
The trend should be of interest to many people in our community. 

##### Novelty 
The trend should be about something new. People were not posting about it before, or at least not with the same intensity. For example, #love, #life, #travel etc are generic hastags and get millions of posts everyday and should not be counted among trends.

##### Timeliness 
The trend should surface on the social network while the real event is taking place and not after it happens. The data processing systems should process the tweets and pick the trends in near-realtime.

#### How to identify a trend from a stream of tweets?
###### Step 1 : Event Stream Generation

If a tweet or post is created by the user, an event with tweet\post data and metadata is generated and sent to a Kafka topic. This topic is consumed by the Parser component.

Lets say, a user posted below tweet.
			```India won the match, Wow #IndiaVsAustralia #Dhoni ```
An event will be generated and sent asynchronously to a Kafka topic with this tweet data and metadata. 
      
###### Step 2 :  Parsing
To detect the trends,the first step to parse tweets, collect and store data about the hashtags. We need a Parser and a data store, which processes the incoming stream of tweets and parse and filter the hashtags and stores the frequencies in the database for last seven days for every five minute intervals.
For example, 
[![Parsed Tweet Frequency Data](/images/parsed.png "Parsed Tweet Frequency Data")


###### Step 3 :  Scoring


###### Step 4 :  Ranking


###### Step 5 :  Group and Store


###### Step 6 :  Serve



#### High Level Architecture Digram



#### References
1. [Trending on Instagram](https://instagram-engineering.com/trending-on-instagram-b749450e6d93#8ddd "trending")
