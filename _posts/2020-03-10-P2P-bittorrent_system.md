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


#### Functional Requirements of the System
1. Upload - Users should be able to upload a file to the network so that other users can download it.
2. Download - Other users should be able to download the file using the distributed P2P network.
3. Users should be able to search the file.


#### Non-Functional Requirements
1. Fault Tolerant - The system should be able to function properly even if multiple peer nodes are down.
2. Scalable - The systen should be able to support fast download even in case of millions of users all over the world.
3. Decentralized - The system should be decentralized such that it does not depend on any one network or region of the world.


#### The Torrent Flow
1. The content provider creates a meta file (with the .torrent suffix name) for the media file it wants to share, makes it available to users via search engines or torrent sites.

2. Then the content provider starts a BitTorrent client with a full copy of the torrent file as the original seed. For each torrent file, there is a tracker site, whose URL is encoded in the meta file, to help peers find each other to exchange the file chunks. However, newer version of protocol does not need any trackers and rely on Distributed Hash tables on Nodes for peer discovery.

3. A user starts a BitTorrent client as a downloader at the beginning to download file chunks from other peers or seeds in parallel. 

4. A peer that has downloaded the file completely also becomes a seed that could in turn provide downloading service to other peers.

5. All peers in the system, including both downloaders and seeds, self-organize into a P2P network, known as a torrent. The initial seed can leave the torrent when there are other seeds available, and content availability and system performance in the future depend on the arrival and departure of downloaders and other seeds.

#### Upload a file as a content provider
![Uploading a file](/images/partitionfile.png "Partition File")

1. When creating the torrent file from the original file, the original file is cut into smaller pieces, usually 512 KB or 256Kb in size. 

2. The SHA-1 hash codes of the pieces are included in the torrent file. The downloaded data are verified by computing the SHA-1 hash code and comparing it to the SHA-1 code of the corresponding piece in the torrent file. This way the data is checked for errors and it guarantees to the users that they are downloading the real thing. 

#### Finding the Peer nodes having the torrent and Downloading

##### Distributed Hash Table
From Wikipedia, "A distributed hash table (DHT) is a distributed system that provides a lookup service similar to a hash table: (key, value) pairs are stored in a DHT, and any participating node can efficiently retrieve the value associated with a given key. 

The main advantage of a DHT is that nodes can be added/removed with minimum work around re-distributing keys. Keys are unique identifiers which map to particular values, which in turn can be anything from addresses, to documents, to arbitrary data. 

Responsibility for maintaining the mapping from keys to values is distributed among the nodes, in such a way that a change in the set of participants causes a minimal amount of disruption. This allows a DHT to scale to extremely large numbers of nodes and to handle continual node arrivals, departures, and failures.
    
When a node wants to find peers for a torrent, it uses the distance metric to compare the infohash of the torrent with the IDs of the nodes in its own routing table.

It then contacts the nodes it knows about with IDs closest to the infohash and asks them for the contact information of peers currently downloading the torrent. If a contacted node knows about peers for the torrent, the peer contact information is returned with the response. 

Otherwise, the contacted node must respond with the contact information of the nodes in its routing table that are closest to the infohash of the torrent. The original node iteratively queries nodes that are closer to the target infohash until it cannot find any closer nodes.

After the search is exhausted, the client then inserts the peer contact information for itself onto the responding nodes with IDs closest to the infohash of the torrent.

![Searching and download](/images/dhtsearch.png "DHT Search")

##### Downloading Strategies

The BitTorrent protocol selects pieces to download by using the following four simple policies:
1. Strict Policy: Until a piece is assembled, only download sub-pieces for that piece.
2. Rarest First: Determine the pieces that are most rare among your peers and download those first.
3. Random First Piece: Select a random piece of the file and download it.
4. Endgame mode: When all the sub-pieces that a peer doesn’t have are actively being requested, these are requested from every peer.
These policies ensure that the pieces are replicated, and that every peer has the largest probability of retrieving the complete file, as quickly as possible.


#### Searching a File over the network

DHT-based systems lack the support of a user friendly content-based search and can only do exact match search by default because of the use of hash functions. Another Content-based search system needs to be developed over the Distributed hash tables to allows the lookup of files without knowing an exact keyword. Prefix Hash Trees are a good data structure for this.
Also Content Similarity Searches based systems can be used.

#### References

1. Bittorrent.org
