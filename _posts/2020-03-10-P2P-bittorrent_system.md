---
layout: post
title: Notes on P2P-Bittorrent-like system design 
description : p2p, bittorrent, system design, distributed
---

#### What is P2P system?
Let's suppose we want to share the latest Avengers movie to the whole world. The traditional way this is being done is to 
copy this file on a central server and let all the people in the world download it over the internet.
There are some problems with this approach for large files-the central server needs to have have the capacity to handle the 
load for millions of clients. If the central server goes down, the file download stops for all users.

Peer-to-Peer network based system attempt to solve these problems using a different approach. In a P2P system, each Peer(a node in the network) can send or receive files (in small parts) to others peers. Therefore, if you want to download a file, 
you can get small pieces of it from multiple computers. If a computer has only a portion of a file, it can send that portion to other computers and it is not required to have the whole file on sending peers( or seeds). Thus, a computer in the system can both receive pieces of the file from multiple other seeds, and send portions simultaneously. 

Because of this decentralized architecture, nodes get the file quickly. The bottleneck of a central server bandwidth and availability is eliminated by relying on distributed network of computers (seeds) of the P2P network.

#### What is BitTorrent?

BitTorrent is a communication protocol for peer-to-peer file transfer. Users install the the client software supporting the BitTorrent protocol such as uTorrent. The clients installed on other user’s machines  over the word form a peer-to-peer network and share files among themselves. 

The first generation peer-to-peer file sharing networks, such as Napster, relied on a central database to co-ordinate look ups on the network. 

Second generation peer-to-peer networks, such as Gnutella, used flooding to locate files, searching every node on the network. 

Third generation peer-to-peer networks use Distributed hash tables to look up files in the network. Distributed hash tables store resource locations throughout the network. A major criterion for these protocols is locating the desired nodes quickly.



#### Making a file available for Download
    Partitioning a file to chunks
    Storing file hashes in Distributed Hash Tables
    Understanding DHT

#### Downloading a file
    Search and find the Peer nodes
    Establish connection and Download
    Strategies for Download

#### Security
    Hash Verification
    Encryption
    
#### Searching a File 
    Prefix Hash Trees
    Content Similarity Searches

#### References
