---
layout: post
title: Online Game Leaderboard System
description : game, leaderboard, system design, system, interview
---


#### What is a Game Leaderboard?
1. Game leaderboards list the users and their scores for a game in an ordered manner.
2. User get to know their performance in the game against others in the game and this encourages them to play better.
3. Leaderboards encourage engagement and competition among players.

Example of a leaderboard from the PUBG game-
![LeaderBoard Example](/images/leaderboard.png "Leaderboard")

#### Important Components of the System
1. Game Client
2. Leaderboard Service
3. Database
4. Redis based Ranking Server

#### Game Client
1. Contains the API sdk to call leaderboard service REST apis.
2. sends and gets score from the service.


#### Leaderboard Service
1. Provides REST apis to add scores.
2. Provides APIs to retrieve the leaderboard, top N scores, top N scores above and below the user.

#### Database
1. MySQL database to score current user and score information.


#### Redis Server for RANK
1. Redis offer data structures Sorted Sets to maintain rank information.
2. All leaderboard get requests are served from REDIS and result is merged to mysql db and returened to the user.

#### Why use REDIS based system for Ranking?
1. There are challenges with using Relational databases for ranking queries when the user number rises and it is difficult to scale.

#### High Level System architecture

![LeaderBoard System](/images/leaderboard_system.png "Leaderboard System")

#### Details

#### References
1. AWS gaming 
2. Azure Gaming
