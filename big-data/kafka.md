# Kafka

### What is Kafka
Apache Kafka is a fast, scalable, fault-tolerant messaging system which enables communication between producers and consumers using message-based topics. 


### Use cases
-  **Kafka Messaging**: As we know, Kafka is a distributed publish-subscribe messaging system. So, for a more traditional message broker, Kafka works well as a replacement. For a variety of reasons, we use Message brokers. For example, to decouple processing from data producers, to buffer unprocessed messages and many more.
However, Kafka has better throughput, built-in partitioning, replication, and fault-tolerance, in comparison to most other messaging systems. That makes it a good solution for large-scale message processing applications.

 - **Website Activity Tracking**: To be able to rebuild a user activity tracking pipeline as a set of real-time publish-subscribe feeds, it is the original Use Case for Kafka. That implies site activity is published to central topics with one topic per activity type. Here, site activity refers to page views, searches, or other actions users may take.
Let’s Explore Kafka Features

 - **Kafka Metrics**: For operational monitoring data, Kafka is often used. In addition, to produce centralized feeds of operational data, it includes aggregating statistics from distributed applications.

 - **Kafka Log Aggregation**: In order to collect logs from multiple services and make them available in a standard format to multiple consumers, we can use Kafka across an organization.

 - **Stream Processing**: However, there are some popular frameworks which read data from a topic, processes it, and write processed data to a new topic, where it becomes available for users and applications, such as Storm and Spark Streaming. In the context of stream processing, Kafka’s strong durability is also very useful.

 - **Kafka Event Sourcing**: Basically, when state changes are logged as a time-ordered sequence of records, then event sourcing is a style of application design. Also, we can say Kafka is an excellent backend for an application built in this style. Because it supports for a very large stored log.
Let’s revise Apache Kafka Operations with commands

 - **Commit Log**: While it comes to a distributed system, Kafka can serve as a kind of external commit-log for it. Generally, it replicates data between nodes. Also, acts as a re-syncing mechanism for failed nodes to restore their data. The feature of log compaction in Kafka helps to support this usage. However, Kafka is the same as Apache BookKeeper project, in this usage.
 
 ### Applications using Kafka
 - **Twitter** : Twitter is one of the best Kafka Applications. A famous online social networking service or a platform Twitter uses Kafka. Basically, it provides a way to send and receive users tweets. Through this platform, registered users can read and post tweets, but unregistered users can only read tweets. However, it uses Storm-Kafka as a part of their stream processing infrastructure.
 
 - **LinkedIn** : Another Kafka Application is LinkedIn. For activity stream data and operational metrics, LinkedIn uses Apache Kafka. There are several products like LinkedIn Newsfeed, LinkedIn Today, for online message consumption and in addition to offline analytics systems like Hadoop, Kafka messaging system helps LinkedIn. Moreover, we can say the strong durability of Kafka is also one of the key factors in connection with LinkedIn.
 
 - **Netflix** : An American multinational provider of on-demand internet streaming media, Netflix, also uses Kafka. Basically, for the purpose of real-time monitoring and event processing, it uses Kafka.
 
 - **Mozilla** : In 1998, members of Netscape created a free-software community, Mozilla. In order to collect performance and usage data from the end-users browser for projects like Telemetry, Test Pilot, etc. Kafka will soon be replacing a part of Mozilla current production system.

 - **The New York Times** : This company uses it to store and distribute, in real-time, published content to the various applications and systems that make it available to the readers. Basically, it uses Apache Kafka and the Kafka Streams both.
 
 ### Types of messaging system
 - **Point to Point Messaging System**: In a point-to-point system, messages are persisted in a queue. One or more consumers can consume the messages in the queue, but a particular message can be consumed by a maximum of one consumer only. Once a consumer reads a message in the queue, it disappears from that queue. The typical example of this system is an Order Processing System, where each order will be processed by one Order Processor, but Multiple Order Processors can work as well at the same time.
 
 - **Publish-Subscribe Messaging System**: In the publish-subscribe system, messages are persisted in a topic. Unlike point-to-point system, consumers can subscribe to one or more topic and consume all the messages in that topic. In the Publish-Subscribe system, message producers are called publishers and message consumers are called subscribers. A real-life example is Dish TV, which publishes different channels like sports, movies, music, etc., and anyone can subscribe to their own set of channels and get them whenever their subscribed channels are available. 
 
 **Kafka falls under pub-sub.**
 
 ### Concepts
 - **Topics** : 
 A topic is a feed name or category to which records are published. Topics in Kafka are always multi-subscriber — that is, a topic can have zero, one, or many consumers that subscribe to the data written to it. For each topic, the Kafka cluster maintains a partition log that looks like this:
 
 - **Partitions** : A topic may have many partitions so that it can handle an arbitrary amount of data. In the above diagram, the topic is configured into three partitions (partition{0,1,2}). Partition0 has 13 offsets, Partition1 has 10 offsets, and Partition2 has 13 offsets. There are few partitions in every Kafka broker. Each partition can be either a leader or a replica of a topic. In addition, along with updating of replicas with new data, Leader is responsible for all writes and reads to a topic. The replica takes over as the new leader if somehow the leader fails.
 
 - **Partition Offset** : Each partitioned message has a unique sequence ID called an offset. For example, in Partition1, the offset is marked from 0 to 9.
 
 - **Replicas** : Replicas are nothing but backups of a partition. If the replication factor of the above topic is set to 4, then Kafka will create four identical replicas of each partition and place them in the cluster to make them available for all its operations. Replicas are never used to read or write data. They are used to prevent data loss.
 
 - **Brokers** : Brokers are simple systems responsible for maintaining published data. Kafka brokers are stateless, so they use ZooKeeper for maintaining their cluster state. Each broker may have zero or more partitions per topic. For example, if there are 10 partitions on a topic and 10 brokers, then each broker will have one partition. But if there are 10 partitions and 15 brokers, then the starting 10 brokers will have one partition each and the remaining five won’t have any partition for that particular topic. However, if partitions are 15 but brokers are 10, then brokers would be sharing one or more partitions among them, leading to unequal load distribution among the brokers. Try to avoid this scenario.
 
 - **Zookeeper** : ZooKeeper is used for managing and coordinating Kafka brokers. ZooKeeper is mainly used to notify producers and consumers about the presence of any new broker in the Kafka system or about the failure of any broker in the Kafka system. ZooKeeper notifies the producer and consumer about the presence or failure of a broker based on which producer and consumer makes a decision and starts coordinating their tasks with some other broker.
 
 - **Cluster** : When Kafka has more than one broker, it is called a Kafka cluster. A Kafka cluster can be expanded without downtime. These clusters are used to manage the persistence and replication of message data.
 
 - **Kafka Consumer Group** : Basically, a consumer abstraction offered by Kafka which generalizes both traditional messaging models of queuing and also publish-subscribe is what we call the consumer group. However, with a consumer group name, Consumers can label themselves.
 
 - **Kafka Log Anatomy** : A log is nothing different but another way to view a partition. Basically, a data source writes messages to the log. Further, one or more consumers read that data from the log at any time they want. Let’s understand it with a diagram, here consumers A and B are reading a data source which is writing to the log and from the log at different offsets.
 
 - **Node in Kafka** : In the Apache Kafka cluster, a node is a single computer.
 
 - **Kafka Cluster** : A  group of computers which are acting together in order to achieve a common purpose is what we call a cluster. In Kafka also, it has the same meaning i.e. a group of computers, each having one instance of Kafka broker.
 
 - **Kafka Replicas** : Here, the word replica refers to a backup. That means a replica of a partition is a “backup” of a partition. Basically, we use replicas in order to prevent data loss, they never read or write data.
 
 - **Kafka Message** : In one line, Message in Kafka is an information which travels from the producer to a consumer through Apache Kafka.
 
 - **Kafka Leader** : A node which is responsible for all reads and writes for the given partition is what we call a Kafka Leader. So, every partition consists of one server, which acts as a leader.
 
 - **Follower in Kafka** : Simply putting, a node that follows leader instructions is what we call a follower. The basic usage of a follower is, if any leader fails, any of these followers will automatically become the new leader. However, it plays as the normal consumer, which pulls messages and also updates its own data store.
 
 - **Kafka Data Log** : Messages are preserved through Kafka, especially for a considerable amount of time. That means consumers can read as per their convenience. Since Kafka is configured to keep messages for 24 hours but somehow consumer is down for time greater than 24 hours, in that case, the consumer will lose messages. Still, it is possible to read that message from last known offset, only if the downtime on part of the consumer is just 60 minutes.
   
  - **Kafka Connector API** : The API which permits to build as well as run reusable consumers or producers that connects existing applications or data systems to Kafka topics, we use the Connector API.
    
### Kafka API
2. APIS
Kafka includes five core apis:
- The **Producer API** allows applications to send streams of data to topics in the Kafka cluster.
- The **Consumer API** allows applications to read streams of data from topics in the Kafka cluster.
- The **Streams API** allows transforming streams of data from input topics to output topics.
- The **Connect API** allows implementing connectors that continually pull from some source system or application into Kafka or push from Kafka into some sink system or application.
- The **AdminClient API** allows managing and inspecting topics, brokers, and other Kafka objects.

Kafka exposes all its functionality over a language independent protocol which has clients available in many programming languages. However only the Java clients are maintained as part of the main Kafka project, the others are available as independent open source projects.
 
 ### Workflow
 #### 1. Pub-Sub Messaging
 
 - At regular intervals, Kafka Producers send the message to a topic.
 - Kafka Brokers stores all messages in the partitions configured for that particular topic, ensuring equal distribution of messages between partitions. For example, Kafka will store one message in the first partition and the second message in the second partition if the producer sends two messages and there are two partitions.
 - Moreover, Kafka Consumer subscribes to a specific topic.
 - Once the consumer subscribes to a topic, Kafka offers the current offset of the topic to the consumer and save the offset in the Zookeeper ensemble.
 - Also, the consumer will request the Kafka in a regular interval, for new messages (like 100 Ms).
 - Kafka will forward the messages to the consumers as soon as received from producers.
 - The consumer will receive the message and process it.
 - Then Kafka broker receives an acknowledgment of the message processed.
 - Further, the offset is changed and updated to the new value as soon as Kafka receives an acknowledgment. Even during server outrages, the consumer can read the next message correctly, because ZooKeeper maintains the offsets.
 - However, until the consumer stops the request, the flow repeats.
 - As a benefit, the consumer can rewind/skip any offset of a topic at any time and also can read all the subsequent messages, as a par desire.
 
 #### Queue Messaging/Consumer Group
A group of Kafka consumers having the same Group ID can subscribe to a topic, instead of a single consumer, in a queue messaging system. However, with the same Group ID all consumers, those are subscribing to a topic are considered as a single group and share the messages. This system’s workflow is:

 - In regular intervals, Kafka Producers send the message to a Kafka topic.
 - As similar to the earlier scenario, here also Kafka stores all messages in the partitions configured for that particular topic.
 - Moreover, a single consumer in Kafka subscribes to a specific topic.
 - In the same way as Pub-Sub Messaging, Kafka interacts with the consumer until new consumer subscribes to the same topic.
 - As the new customers arrive, share mode starts in the operations and shares the data between two Kafka consumers. Moreover, until the number of Kafka consumers equals the number of partitions configured for that particular topic, the sharing repeats.
 - Although, the new consumer in Kafka will not receive any further message, once the number of Kafka consumers exceeds the number of partitions. It happens until any one of the existing consumer unsubscribes. This scenario arises because in Kafka there is a condition that each Kafka consumer will have a minimum of one partition and if no partition remains blank, then new consumers will have to wait.
 - In addition, we also call it Kafka Consumer Group. Hence, Apache Kafka will offer the best of both the systems in a very simple and efficient manner.
 
### Traditional queuing systems vs Apache Kafka
 
 - **Messages Retaining** : 
 Traditional queuing systems– It deletes the messages just after processing completion typically from the end of the queue.
 Apache Kafka– But in Kafka, messages persist even after being processed. That implies messages in Kafka don’t get removed as consumers receive them.
 
 - **Logic-based processing** : 
 Traditional queuing systems–Traditional queuing systems don’t permit to process logic based on similar messages or events.
 Apache Kafka– Kafka permits to process logic based on similar messages or events.
 
### Questions

#### In the producer, when there comes the situation of queue fullness?
 If there are not enough number of servers added for load balancing, there comes a situation of queue fullness.

#### Explain the offset in Kafka data integration tool?
Messages are stored in partitions and assigneda unique ID to each of them for quick and easy access. That unique number is named as the offset that is responsible to identify each of the messages in the partition.

#### How to balance loads in Kafka when one server fails?
Every partition in Kafka has one main server that plays the role of a leader and one or more non-connected servers that are named as the followers. Here, the leading server sets the permission and rest of the servers just follow him accordingly. In case, leading server fails then followers take the responsibility of the main server.

#### What role ZooKeeper plays in a cluster of Kafka?
Kafka is an open source system and also a distributed system is built to use Zookeeper. The basic responsibility of Zookeeper is to build coordination between different nodes in a cluster. Since Zookeeper works as periodically commit offset so that if any node fails, it will be used to recover from previously committed to offset.

The ZooKeeper is also responsible for configuration management, leader detection, detecting if any node leaves or joins the cluster, synchronization, etc.

#### Elaborate on the terms leader and follower in Kafka environment?
The concept of leader and follower is maintained in Kafka environment so that the overall system ensures load balancing on the servers.

For every partition in Kafka environment, one server plays the role as leader and rest of the servers act as followers.
All the data read and write commands are executed at the leader level and the rest of the followers just have to replicate the process.
At the time of any server faults and the leader is not able to function appropriately then one of the followers will take the place of the leaders. Thus making the system stable and also helps in load balancing of the server.

#### What does ISR stand in Kafka environment?
ISR stands for In sync replicas.

They are classified as a set of message replicas which are synched to be leaders.

#### What is the replica? What does it do?
A replica can be defined as a list of essential nodes that are responsible to log for a particular partition, and it doesn't matter whether they actually play the role of a leader or not.

#### Why are the replications are considered critical in Kafka environment?
The main reason why replications are needed because they can be consumed again in an uncertain event of machine error or program malfunction or the system is down due to frequent software upgrades. So to make sure to overcome these, replication makes sure that the messages published are not lost.

#### If the replica stays out of the ISR for a very long time, then what does it tell us?
If the replica stays out of the ISR for a very long time, or replica is not in sync with the ISR then it means that the follower server is not able to grasp data as fast the leader is doing. So basically the follower is not able to come up with the leader activities.

#### Explain what is a partitioning key?
Within the available producer, the main function of partitioning key is to validate and direct the destination partition of the message. Normally, a hashing based partitioner is used to assess the partition Id if the key is provided.

#### What is the purpose of the retention period in the Kafka cluster?
Within the Kafka cluster, it retains all the published records. It doesn’t check whether they have been consumed or not. Using a configuration setting for the retention period, the records can be discarded. The main reason to discard the records from the Kafka cluster is that it can free up some space.
     
     
### Code Example
 https://github.com/Sumitbhoyar/kafka 
  no