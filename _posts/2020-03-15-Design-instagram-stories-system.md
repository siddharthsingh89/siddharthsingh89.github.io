---
layout: post
title: Instagram Stories system design
description : instagram, stories, system design, snapchat, interview
---

#### What's a Instagram Story?

A story is the new cool feature these days in all the social media apps- Started by Snapchat and called snaps, these messages are short lived and disappear after a day.
Facebook family of social apps such as Whatsapp, Instagram,  Facebook App and Messenger all implemented stories on their platform.

#### Functional Requirements
1. User should be able to create a story.
2. User’s followers or friends should be able to see the story in their story feed.
3. The system should send notifications to the followers about the story.
4. Stories should disappear after 24 hours(configurable).
5. User should be able to see who has viewed the story and count of total views.

#### Non-Functional Requirements
1. The system should be highly available and can be eventually consistent.
2. The system should have low latency.
3. The system should be highly scalable.

#### Back of the Envelope Estimates

Total Daily active users = 1 M 
If every 1 out of every 10 users post a story everyDay 
Total stories posted in one day = 10^5
Stories have text, multiple images and short videos
Avg Memory required for Text story = 200 Bytes
Avg Memory required for Image story = 100 KB * 5 images = 500 KB
Avg Memory required for Video story = I MB * 2 = 2 MB

50% text + 40% image + 10% video = 

Text - 5 x 10^4 x200 bytes = 10^ 7 bytes
Images-> 4 x 10^4 x 500 x 10^3 bytes= 2 x 10^10 bytes
Videos -> 10^4 x 2 X 10^6 bytes = 2 x 10^10 bytes

Total ~50 GB per day

This data will not be accumulated and will be deleted per day.

#### High Level Design

#### API 

#### Database design

#### References
