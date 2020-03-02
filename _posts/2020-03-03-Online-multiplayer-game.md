---
layout: post
title: Notes on Online Multiplayer Game system
description : game, online, multiplayer, system design, distributed system, interview,  client, server, leaderboard
---


### Designing an Online multiplayer gaming system

#### What is a Massive Multiplayer Online Game

#### Multiplayer Game types and Examples

#### Most Important Component of the System

1. Game Client App
   * User interface of the Game. Can be a Web or mobile or Console App.
   * Lots of game media, past history is cached in the client App.
   * Communicates with the Server over Websockets\raw TCP\UDP\Custom Protocol.

2. Game Server
   * Core Gaming Logic is here. Game objects, their interaction etc.
   * Cluster of servers receiving request from Load balancer.
   
3. MatchMaker System
  * Important component of Massive multiplayer games.
  * Groups user based on their characterstics, locality, latency and create an ideal group of users to play.
  * Can be implemented using Queues.
  
4. Database
  * We need to store lots of data. Examples are Player, Sessions, GameHistory etc.
  * Can be relational or noSql as well. Many highly scalabled games are successfully relational.
  * High read and write throughput is needed.
  
5. LeaderBoard System
  * A high performance Leaderboard system which can calcuate rank of user in real time.
  * Anti-Cheating system to detect fake scores.
  * Can be implemented using Redis Sorted Sets commands in logn complexity.
  * SelfBalancing BST are used to store leadership data.
  * Can be highly granular.
  
6. Media Storage System
  * Games contain lot of media eg, Images, videos, cached renditions, other compressed graphic assets, maps etc.
  * Need a storge layer to store media.
  
7. CDN
  * Great CDN deployment is must so that media is available near to the player.
  
8. Fast Distributed Caching Layer
  * Good caching layer is needed in leaderboard, gameplay etc.
  
9. Load Balancer
  * Load balancer needed to balance nodes across fleet of Game Servers.
  
10. Notification System
  * Notify players of new Game tournaments, scores, stats etc.
  
11. Instrumentation System
  * Intrument Game play data to detect scale needed.
  * Detect fake scores.
  
12. Authentication Service
  * Authenticate players before starting the game.
  
13. Chatting Service
  * Should support chatting between players during the game.
  * Optional chat translation.
  
  #### Details
  
  
  #### References
  
  
