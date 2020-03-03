---
layout: post
title: Notes on Online Multiplayer Game system
description : game, online, multiplayer, system design, distributed system, interview,  client, server, leaderboard
---


### Designing an Online multiplayer gaming system
An Online multiplayer game can be of many types. Turn based such as Chess, Poker or first Person shooters such as PUBG or world of warcraft, DOTA etc.

#### Most Important Component of the System

#### Game Client App
![Game Client](/images/gameClients.png "Game Clients")

   * User interface of the Game. Can be a Web or mobile or Console App.
   * Lots of game media, past history is cached in the client App.
   * Communicates with the Server over Websockets\raw TCP\UDP\Custom Protocol.
   

#### Game Server
   * Core Gaming Logic is here. Game objects, their interaction etc.
   * Cluster of servers receiving request from Load balancer.
   
#### MatchMaker System
  * Important component of Massive multiplayer games.
  * Matchmaker will take in a certain amount of people, pair them together and send them on their way to the game server.
   One strategy is to - get a random group of people together to play the game,this will not give balanced game play     
   experience.
   
   Main Requirement-
    * Not too easy not too hard for a gamer. 
    * No waiting for long time to get a match.
    
  * Groups user based on their characterstics, locality, latency and create an ideal group of users to play.
  * Can be implemented using Queues.
  
#### Database
  * We need to store lots of data. Examples are Player, Sessions, GameHistory etc.
  * Can be relational or noSql as well. Many highly scalabled games are successfully relational.
  * Performance is very important for games, which are extremely read and write-heavy. 
  * Game data is continuously updated and read as the player progresses through levels, defeats enemies, receives in-game  
     currency, changes inventory, unlocks upgrades, and completes achievements.
  * Each event must be written to your database layer so it isn’t lost. Durability is important.
  
#### LeaderBoard System
  * A high performance Leaderboard system which can calcuate rank of user in real time.
  * Anti-Cheating system to detect fake scores.
  * Can be implemented using Redis Sorted Sets commands in logn complexity.
  * SelfBalancing BST are used to store leadership data.
  * Can be highly granular.
  
#### Media Storage System
  * Games contain lot of media eg, Images, videos, cached renditions, other compressed graphic assets, maps etc.
  * Need a storge layer to store media.
  
#### CDN
  * Great CDN deployment is must so that media is available near to the player.
  
#### Fast Distributed Caching Layer
  * Good caching layer is needed in leaderboard, gameplay etc.
  
#### Load Balancer
  * Load balancer needed to balance nodes across fleet of Game Servers.
  
#### Notification System
  * Notify players of new Game tournaments, scores, stats etc.
  
#### Instrumentation System
  * Intrument Game play data to detect scale needed.
  * Detect fake scores.
  
#### Authentication Service
  * Authenticate players before starting the game.
  
#### Chatting Service
  * Should support chatting between players during the game.
  * Optional chat translation.
  
 
  
  
  #### References
  
  These are just notes and I will try to add more informtion to the some of the commonly asked components such as Leaderboard   in detail. Below are some important references for game and infra examples-
  
  1. [Google Cloud Gaming Infrastructure](https://cloud.google.com/solutions/gaming/cloud-game-infrastructure)
  2. [Azure Gaming](https://docs.microsoft.com/en-us/gaming/azure/)
  3. [AWS Gaming](https://aws.amazon.com/gaming/game-server/)
  4. [Leaderboard](https://cloud.google.com/solutions/using-memorystore-for-redis-as-a-leaderboard)
