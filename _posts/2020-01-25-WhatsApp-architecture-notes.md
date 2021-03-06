---
layout: post
title: Notes on WhatsApp architecture design
description : whatsapp, system design, distributed system, interview,  client, server, gateway
---


### Real time messaging system architecture like whatsapp
I was asked this question in one of my interviews some time back and it was a bit difficult to think, design and explain on many features 
of the features of Whatsapp. At that time, I gave a Okayish generic answer having cliche Load balancer, web servers etc. and failed the interview.

I thought of studying the architecture and add some notes here.

#### Some important things first
1. This is just a sample design based on my experiences, Youtube videos, blogs and other sources on the web. 
2. No answer is wrong or is absolutely correct. There are many designs possible.
3. This is just to help with pointers to consider during your actual interview.
4. This covers a very small subset of feartures in the system. There are hundred of things whicha are not present. Think of 
Authentication, Logging, monitoring, Deployment,  Notification systems, CI/CD, Storage Layers, Replication, Backup, Disaster recovery, Compliance, GDPR, Privacy to name a few.


#### Scale of Whatsapp
Official Whatsapp Stats in mid-2017 are below- [Source](https://blog.whatsapp.com/10000631/Connecting-One-Billion-Users-Every-Day)
1. 1 Billion Daily Active Users
2. 1.3 Billion Monthly Active Users
3. 55 Billion Messages sent per day (what!)
4. 4.5 Billion photos shared per day (omg)
5. 1 Billion videos shared per day (what?!!)
6. 60 Languages Supporated
7. More than a million people register daily.
8. More than 2 billion minutes of voice and video calls are made on WhatsApp daily.
9. There are 3 million companies using WhatsApp Business.

This is nearly two years old stats, must have been doubled by now.
Whatsapp is lucky that they don't have to store these messages, videos and images forever like other messenger apps. Even if the storage is cheap these days, this scale is a monster.


### Important Components of the System

#### WhatsApp Client Application
![Client App](/images/whatsapp_client.png "Client App Diagram")

Hi, I am the Client Application, developed for different platforms(iOS, android, Web, kaiOS etc).  My job is to -
  1. Start a connection to the WhatsApp server
  2. Store messages on your phone using lightweight databases such as sqllite.
  3. Fetch and store the User profile information (name, status, 
  contacts, Groups, security settings)from the server and cache on the device.
  4. Send text messages.
  5. Send pictures, videos and other documents.
  6. Index the messages locally to search faster.
  7. Provide various settings to manage the application and user preferences.
  
 
 
#### Gateway Server

![Gateway Server](/images/whatsapp_gateway.png "Gateway Diagram")

Hi, I am the gateway server. I live in Whatsapp\FB data centers and handle connections. My job is-
  1. To maintain connections to the client App. When user A launches the Whatsapp Application, they open a TCP connection with me and than 
  a websocket protocaol based communication is establised between me and the client. WebSockets helps me to push messages to the clients.
  2. I maintain a lot of connections- millions of them. On a single box, it may be 10 millions connection which is huge.
  3. There are other gateway servers as well who maintain similar connection to other clients apps. Together our fleet of servers handle the billions of whatsapp users.
  
   Question: What happens to the 10 millions connections I am maintaining if I am crashed? 
   Answer : The client app will restart connection and will be assigned to other servers who are waiting on standby. Meanwhile, I will 
  be diagonised and rebooted.

#### User Service
Hello, I am your favourite user Service. I live in WhatsApp\FB data center. I store user data on the server. My job is-
  1. Register the user. I take phone numbers, use it as an ID to uniquely identify users.
  2. I store the name, status, contacts(?), account settings, group information about the users.
  3. I can use relational database but it's best for me to use Read-optimized hight available key-value store for storing user information.
  4. Let's say I use Amazon Dynamo for storing it. I also interact with a Redis Cache before hitting the database.
  5. What I store is something like-
  
  ```json
    { 
      "id" : "121212121212", 
      "name" : "Sidharth Singh",
      "status" : "sleeping :-)", 
       "settings" : { 
                      "account_setting": {},
                      "device_setting: {}
                     },
       "groups" : { 
                    "group_id": "2233232",
                    "group_name": "School Friends"
                  }
    }
```
   
#### Messaging Service
  Hello, I am the most critical component and it's important for you to draw me on the whiteboard. 
  1. Erlang has this concept of lightweight units called processes which are dynamic, can grow and shrink. They are lighter than threads
  with really small memory footprint, identified by a unique PID.
  2. Messaging Server spawns a new process and a message queue for a connected client. The process has access to the WebSocket connection
  maintained by the Gateway server.It continiously polls the queue and sends the message using the connection.
  If the user is not connected, message stay in the queue.
  3. Since Erlang Process are lightWeight, it is easy to create millions on single box unlike threads which are a bit heavy.
  4. The process also retries messages which are failed.
  5. For an A->B message, Process A can write the message to Queue of User B. User B's process can then send the message.
  6. The process have information about the users connections and proceses from a data store described below.
  7. Messaging Sub system also maintains mapping between PID and UserID in a read-optimized cache.
  8. A sample message looks like -
  
  ```json
  {
    "message_id": "121212121212",
    "msg_type": "MSG_TEXT",
    "content" : "HI there",
    "receipent" : "User B",
    "Sender" : "User A",
  }
  ```
  
 #### Media Service
  Hi I am the media service. I help in sending images, videos and other media files. My job is-
  1. Whenever user selects and sends an image in the client app, It is uploaded over a different Http connection to an Image optimized store (such as Facebooks HayStack) and an unique ID is given to this resource.
  2. A message is sent to to user with the Image resoruce ID.
  3. The receiver client Application downloads the Image file from the Image store over Http.
  
  
#### Security 
  
  1. All Whatsapp messages, group chats, images, videos , calls etc are end-2-end encrypted.
  2. WhatsApp uses the Signal Protocol designed by Open Whisper systems.
  3. In this protocaol, if encryption keys from a user’s device are ever physically compromised, they cannot be used to go    back in time to decrypt previously transmitted messages.
  
  Hope this helps. I will add some diagrams(MOST IMPORTANT).
  To be continued-
  

#### References
To be added
