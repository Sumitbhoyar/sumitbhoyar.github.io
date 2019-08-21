# Gossip Protocol

Computer nodes are not far behind men and viruses when it comes to gossiping. The fundamentals of gossip are the same. It is the way of spreading an information to the people of the same world. When you get to know that your manager has put down her papers, you break this information to your colleague on a smoke break. Your colleague likes the information and passes it on to another colleague while you break this information to another colleague of yours. In no time, every person in the company would be aware of the “gossip” about your manager leaving her job. Actually, “in no time” is incorrect; time taken for everyone to know would be of the order of logarithmic of the number of employees in the company. That's exactly how computer nodes gossip with each other.

Consider a network of computer nodes. Let's say, node N1 receives a new information. N1 would then randomly select a peer (say, node N2) and share the information. N1 and N2 would then pick a peer each (say, node N3 and N4) randomly and share the information. The process continues in this fashion till the information is passed on to all the connected nodes. Typically, nodes store the time of information exchange also. In the example above, in the first exchange, N2 would store the details of N1, the information, and the time at which N2 got to know about the information.

### Where is Gossip Protocol Used?

Gossip protocol works beautifully in a decentralized network of nodes. It is a decentralized way of information exchange. Rules can be built on these nodes to determine the truthfulness of an information. Let's say if a network obeying gossip protocol holds a rule that when two-thirds of the nodes return the same information, that information will be considered as the truth. In this process, all the nodes are treated equally. It does not matter if a node is more powerful than its peers. The only thing that matters here is the network bandwidth.

The power of gossip lies in the robust spread of information. Even if Dave had trouble understanding Bob, he will probably run into someone else soon and can learn the news that way.

### How it works?

Gossip protocols are very simple conceptually and very simple to code.  The basic idea behind them is this: A node wants to share some information to the other nodes in the network. Then periodically it selects randomly a node from the set of nodes and exchanges the information. The node that receives the information does exactly the same thing.  The information is periodically send to N targets, N is called fanout.

![Gossip Protocol](gossip-protocol.jpg)

### Gossip Protocol in Action

It is highly unlikely that you have never used an application which uses gossip protocol. If you hold some Bitcoins, if you use any social media platform, if you use a search engine, if you have downloaded movies from torrent, you have used gossip protocol.

In Bitcoin Blockchain network, gossip protocol is used by the miners to communicate the value of nonce to fellow miners. Gossip protocol plays a critical role in the world of Blockchain. It is used by most of the major blockchain networks like Bitcoin and Hyperledger. Hashgraph, which claims itself to be a better technology than Blockchain, also uses the gossip protocol to transfer information. Hashgraph is an interesting concept and I shall cover it in my upcoming posts. To maintain the sanity, restricting this post to gossip protocol.

### Applications
- Database replication
- Information dissemination
- Cluster membership
- Failure Detectors
- Overlay Networks
- Aggregations (e.g calculate average, sum, max)

### Examples
- Riak uses a gossip protocol to share and communicate ring state and bucket properties around the cluster.
- In CASSANDRA nodes exchange information using a Gossip protocol about themselves and about the other nodes that they have gossiped about, so all nodes quickly learn about all other nodes in the cluster.
- Dynamo employs a gossip based distributed failure detection and membership protocol. It propagates membership changes and maintains an eventually consistent view of membership. Each node contacts a peer chosen at random every second and the two nodes efficiently reconcile their persisted membership change histories.
- Dynamo gossip protocol is based on a scalable and efficient failure detector introduced by Gupta and Chandra in 2001
Consul uses a Gossip protocol called SERF for two purposes:
   – discover new members and failures  
   – reliable and fast event broadcasts for events like leader election.
- The Gossip protocol used in Consul is called SERF and is based on “SWIM:  Scalable Weakly-consistent Infection-style Process Group Membership Protocol”
- Amazon s3 uses a Gossip protocol to spread server state to the system 

