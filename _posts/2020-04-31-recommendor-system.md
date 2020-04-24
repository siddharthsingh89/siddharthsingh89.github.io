---
layout: post
title: Design Recommender System
description : recommender system, ML, system design, AI
---
##### What is a Recommendar System?
Recommendar systems are algorithms which predict the user behaviour and suggest items which will probably be liked by the User. They are very important component of modern web applications and are used in variety of domains. Some of the classic use cases for Recommendation system are-
1. Netflix recommending the TV shows which you should watch based on your interests.
2. Amazon recommendaing products based on your purchase history.
3. Youtube videos suggestions.
4. Spotify music suggestions such as Discover Weekly playlists etc.
5. Medium.com sending daily emails with recommended blog posts based on articles you read on the site.

##### No magic! It's just data.
Recommendatios can be provided in real-time when the user is using the service eg. while Browsing Youtube, Netflix or amazon or over email or SMS etc, and other offline methods. And to provide accurate recommendations, the system needs to know about the user interests and preferences. 

Once the system gets data about your preferences, they use this data to recommend other similar content or product which you may like and they have become really good at it. Spotify Discover playlists are famous and have surprised many users by their recommended songs. People have been tweeting that Spotify knows their music taste better then their family members.

At first, when users' tastes and preferences are not known, recommendations are based on item attributes alone. Over time and with enough data, various machine learning algorithms and data pipelines are used  perform useful analysis and deliver meaningful recommendations. Other users’ inputs can also improve the results, enabling the system to be retrained periodically.

##### Anatomy of a Recommendation System
A typical recommendation engine consists of a pipeline with below major steps-

1. Data Collection.
2. Data Storage and processing
3. Analysis
4. Recommendation

The first high level digram which you are going to draw on that whiteboard is below-
![Recommendation System Example](/images/basic_recommendation_system.png "Recommendation system")

The various components of the system are-
###### Frontend component
The website or the mobile app which is used to collect the data about the user. For example, Amazon web app, Netflix Mobile App, Spotify Android etc. are examples of the frontend. All user activity (eg. liking an artist, playing a song, skiping a song etc) is tracked as events and sent over Http to the backend service. This data is temporarily buffered in a Kafka queue and stored in database.

###### Data Storage
The user interaction data stream is stored in permanent store and processed and filtered so that it can be analyzed by one or More Machine Learning algorithms. The storage can be noSql Store like Cassandra or a SQL store as well.  We will discuss the most important algorithms below.

###### Machine Learning Platform
This involves processing the data collected and generating recommendations out of it. Running ML algorithms on massive datasets involves Data processing systems such as Spark, Hadoop etc.

###### Recommendation Storage
Generated recommendations are stored in this generally read-optized database. Recommendations are served in realtime to the front end or offline using services such as Email processing Services.


##### References


