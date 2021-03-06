Apache Zookeeper
===============


**ZooKeeper** is a distributed co-ordination service to manage large set of hosts. Co-ordinating and managing a service in a distributed environment is a complicated process. ZooKeeper allows developers to focus on core application logic without worrying about the distributed nature of the application.

A distributed application can run on multiple systems in a network at a given time (simultaneously) by coordinating among themselves to complete a particular task in a fast and efficient manner.

The time to complete the task can be further reduced by configuring the distributed application to run on more systems. A group of systems in which a distributed application is running is called a **Cluster** and each machine running in a cluster is called a **Node**.

A distributed application has two parts, **Server** and **Client** application. Server applications are actually distributed and have a common interface so that clients can connect to any server in the cluster and get the same result. Client applications are the tools to interact with a distributed application.

**Benefits of Distributed Applications**

 - Reliability − Failure of a single or a few systems does not make the whole system to fail.
 - Scalability − Performance can be increased as and when needed by adding more machines with minor change in the configuration of the application with no downtime.
 - Transparency − Hides the complexity of the system and shows itself as a single entity / application.

**Challenges of Distributed Applications**

 - Race condition − Two or more machines trying to perform a particular task, which actually needs to be done only by a single machine at any given time. For example, shared resources should only be modified by a single machine at any given time.
 - Deadlock − Two or more operations waiting for each other to complete indefinitely.
 - Inconsistency − Partial failure of data.


**The common services provided by ZooKeeper are as follows −**

- Naming service − Identifying the nodes in a cluster by name. It is similar to DNS, but for nodes.
- Configuration management − Latest and up-to-date configuration information of the system for a joining node.
- Cluster management − Joining / leaving of a node in a cluster and node status at real time.
- Leader election − Electing a node as leader for coordination purpose.
- Locking and synchronization service − Locking the data while modifying it. This mechanism helps you in automatic fail recovery while connecting other distributed applications like Apache HBase.
- Highly reliable data registry − Availability of data even when one or a few nodes are down.

**Benefits of ZooKeeper**

Here are the benefits of using ZooKeeper −

- Simple distributed coordination process
- Synchronization − Mutual exclusion and co-operation between server processes. This process helps in Apache HBase for configuration management.
- Ordered Messages
- Serialization − Encode the data according to specific rules. Ensure your application runs consistently. This approach can be used in MapReduce to coordinate queue to execute running threads.
- Reliability
- Atomicity − Data transfer either succeed or fail completely, but no transaction is partial.

**Zookeeper components**

> **Client**: One of the nodes in our distributed application cluster, access information from the server. For a particular time interval, every client sends a message to the server to let the sever know that the client is alive.Similarly, the server sends an acknowledgement when a client connects. If there is no response from the connected server, the client automatically redirects the message to another server.

> **Server**: Server, one of the nodes in our ZooKeeper ensemble, provides all the services to clients. Gives acknowledgement to client to inform that the server is alive.

> **Ensemble**: Group of ZooKeeper servers. The minimum number of nodes that is required to form an ensemble is 3.

> **Leader**: Server node which performs automatic recovery if any of the connected node failed. Leaders are elected on service startup.

> **Follower**: Server node which follows leader instruction.


**Zookeeper Setup**
```
Execute: cd /ur/path

Execute: wget http://redrockdigimark.com/apachemirror/zookeeper/zookeeper-3.4.10/zookeeper-3.4.10.tar.gz

Execute: tar -zxf zookeeper-3.4.10.tar.gz /ur/path

Edit: ~/.bashrc
export ZOOKEEPER_HOME = /ur/path/zookeeper-3.4.10
export PATH=$PATH:$ZOOKEEPER_HOME/bin

Execute: source ~/.bashrc

Edit/Create: /ur/path/zookeeper-3.4.10/conf/zoo.cfg
tickTime = 2000
dataDir = ../data
clientPort = 2181
initLimit = 5
syncLimit = 2


Execute: zkServer.sh start
```


**Hierarchical Namespace**

ZooKeeper node is referred as znode. Every znode is identified by a name and separated by a sequence of path (/).

A root znode separated by “/”. Under root, you have two logical namespaces **config** and **workers**.

The config namespace is used for centralized configuration management and the workers namespace is used for naming.

Under config namespace, each znode can store upto 1MB of data. This is similar to UNIX file system except that the parent znode can store data as well. The main purpose of this structure is to store synchronized data and describe the metadata of the znode. This structure is called as **ZooKeeper Data Model**.

**Types of Znodes**

Znodes are categorized as persistence, sequential, and ephemeral.

> **Persistence znode** − Persistence znode is alive even after the client, which created that particular znode, is disconnected. By default, all znodes are persistent unless otherwise specified.

> **Ephemeral znode** − Ephemeral znodes are active until the client is alive. When a client gets disconnected from the ZooKeeper ensemble, then the ephemeral znodes get deleted automatically. For this reason, only ephemeral znodes are not allowed to have a children further. If an ephemeral znode is deleted, then the next suitable node will fill its position. Ephemeral znodes play an important role in Leader election.

> **Sequential znode** − Sequential znodes can be either persistent or ephemeral. When a new znode is created as a sequential znode, then ZooKeeper sets the path of the znode by attaching a 10 digit sequence number to the original name. For example, if a znode with path /myapp is created as a sequential znode, ZooKeeper will change the path to /myapp0000000001 and set the next sequence number as 0000000002. If two sequential znodes are created concurrently, then ZooKeeper never uses the same number for each znode. Sequential znodes play an important role in Locking and Synchronization.

**Sessions**

Sessions are very important for the operation of ZooKeeper. Requests in a session are executed in FIFO order. Once a client connects to a server, the session will be established and a session id is assigned to the client.

The client sends heartbeats at a particular time interval to keep the session valid. If the ZooKeeper ensemble does not receive heartbeats from a client for more than the period (session timeout) specified at the starting of the service, it decides that the client died.

Session timeouts are usually represented in milliseconds. When a session ends for any reason, the ephemeral znodes created during that session also get deleted.

**Watches**

Watches are a simple mechanism for the client to get notifications about the changes in the ZooKeeper ensemble. Clients can set watches while reading a particular znode. Watches send a notification to the registered client for any of the znode (on which client registers) changes.

Znode changes are modification of data associated with the znode or changes in the znode’s children. Watches are triggered only once. If a client wants a notification again, it must be done through another read operation. When a connection session is expired, the client will be disconnected from the server and the associated watches are also removed.

**Zookeeper - Workflow**

Once a ZooKeeper ensemble starts, it will wait for the clients to connect. Clients will connect to one of the nodes in the ZooKeeper ensemble. It may be a leader or a follower node. Once a client is connected, the node assigns a session ID to the particular client and sends an acknowledgement to the client. If the client does not get an acknowledgment, it simply tries to connect another node in the ZooKeeper ensemble. Once connected to a node, the client will send heartbeats to the node in a regular interval to make sure that the connection is not lost.

- If a client wants to **read** a particular znode, it sends a read request to the node with the znode path and the node returns the requested znode by getting it from its own database. For this reason, reads are fast in ZooKeeper ensemble.

- If a client wants to **store data** in the ZooKeeper ensemble, it sends the znode path and the data to the server. The connected server will forward the request to the leader and then the leader will reissue the writing request to all the followers. If only a majority of the nodes respond successfully, then the write request will succeed and a successful return code will be sent to the client. Otherwise, the write request will fail. The strict majority of nodes is called as **Quorum**.

**Workflow components**

> **Write**: Write process is handled by the leader node. The leader forwards the write request to all the znodes and waits for answers from the znodes. If half of the znodes reply, then the write process is complete.

> **Read**: Reads are performed internally by a specific connected znode, so there is no need to interact with the cluster.

> **Replicated Database**: It is used to store data in zookeeper. Each znode has its own database and every znode has the same data at every time with the help of consistency.

> **Leader**: Leader is the Znode that is responsible for processing write requests.

> **Follower**: Followers receive write requests from the clients and forward them to the leader znode.

> **Request Processor**: Present only in leader node. It governs write requests from the follower node.

> **Atomic broadcasts**: Responsible for broadcasting the changes from the leader node to the follower nodes.


**Nodes in a ZooKeeper Ensemble**

Let us analyze the effect of having different number of nodes in the ZooKeeper ensemble.

- If we have a **single node**, then the ZooKeeper ensemble fails when that node fails. It contributes to “Single Point of Failure” and it is not recommended in a production environment.

- If we have **two nodes** and one node fails, we don’t have majority as well, since one out of two is not a majority.

- If we have **three nodes** and one node fails, we have majority and so, it is the minimum requirement. It is mandatory for a ZooKeeper ensemble to have at least three nodes in a live production environment.

- If we have **four nodes** and two nodes fail, it fails again and it is similar to having three nodes. The extra node does not serve any purpose and so, it is better to add nodes in odd numbers, e.g., 3, 5, 7.

We know that a write process is expensive than a read process in ZooKeeper ensemble, since all the nodes need to write the same data in its database. So, it is better to have less number of nodes (3, 5 or 7) than having a large number of nodes for a balanced environment.


**Zookeeper - CLI**

- **Create** znodes

> Syntax  
```
create /path /data
```

> Sample 
```
create /FirstZnode “Myfirstzookeeper-app”
```

> To create a **Sequential znode**, add -s flag as shown below.

> Syntax 
```
create -s /path /data
```

> Sample 
```
create -s /FirstZnode second-data
```

> To create an **Ephemeral Znode**, add -e flag

- **Get** data
> Syntax 
```
get /path
```

> Sample 
```
get /FirstZnode
```

> To access a **sequential znode**, you must enter the full path of the znode.

> Sample 
```
get /FirstZnode0000000023
```


- **Watch** znode for changes
Watches show a notification when the specified znode or znode’s children data changes. You can set a watch only in get command.
> Syntax ```get /path [watch] 1 ```

> Sample 
```
get /FirstZnode 1
```


- **Set data**
> Syntax 
```
set /path /data
```

> Sample 
```
set /SecondZnode Data-updated
```

- **Create children** of a znode

> Syntax 
```
create /parent/path/subnode/path /data
```

> Sample 
```
create /FirstZnode/Child1 firstchildren
```

- **List children** of a znode

> Syntax
```
ls /path
```

> Sample
```
ls /MyFirstZnode
```

- **Check Status**

> Status describes the metadata of a specified znode. It contains details such as Timestamp, Version number, ACL, Data length, and Children znode.

> Syntax 
```
stat /path
```

> Sample 
```
stat /FirstZnode
```

- **Remove / Delete** a znode
Removes a specified znode and recursively all its children. This would happen only if such a znode is available.
> Syntax 
```
rmr /path
```

> Sample 
```
rmr /FirstZnode
```


**Java (spring-boot) + ZooKeeper integration**

https://github.com/Sumitbhoyar/spring-boot-zookeeper
