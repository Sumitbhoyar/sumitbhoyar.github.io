# Terminologies

### DNS
The Domain Name System is a hierarchical and decentralized naming system for computers, services, or other resources connected to the Internet or a private network. It associates various information with domain names assigned to each of the participating entities.

### Load Balancer
A load balancer is a device that distributes network or application traffic across a cluster of servers. Load balancing improves responsiveness and increases availability of applications.

A load balancer sits between the client and the server farm accepting incoming network and application traffic and distributing the traffic across multiple backend servers using various methods. By balancing application requests across multiple servers, a load balancer reduces individual server load and prevents any one application server from becoming a single point of failure, thus improving overall application availability and responsiveness.

**Most common load balancing techniques in web-based applications are**  

1.  Round robin
2.  Session affinity or sticky session
3.  IP Address affinity

#### What Is Sticky Session (session Affinity) Load Balancing? What Do You Mean By 'session Affinity'?
Sticky session or a session affinity technique another popular load balancing technique that requires a user session to be always served by an allocated machine.  

#### Why Sticky Session?
In a load balanced server application where user information is stored in the session, it will be required to keep the session data available to all machines. This can be avoided by always serving a particular user session request from one machine.  

#### How It Is Done?
The machine is associated with a session as soon as the session is created. All the requests in a particular session are always redirected to the associated machine. This ensures the user data is only at one machine and load is also shared.  
  
In the Java world, this is typically done by using a jsessionid cookie. The cookie is sent to the client for the first request and every subsequent request by a client must be containing that same cookie to identify the session.  

#### What Are The Issues With Sticky Session?
There are few issues that you may face with this approach  
-   The client browser may not support cookies, and your load balancer will not be able to identify if a request belongs to a session. This may cause strange behavior for users who use no cookie based browsers.
-   In case one of the machines fails or goes down, the user information (served by that machine) will be lost and there will be no way to recover user session.

#### What Is IP Address Affinity Technique For Load Balancing?
IP address affinity is another popular way to do load balancing. In this approach, the client IP address is associated with a server node. All requests from a client IP address are served by one server node.  
  
This approach can be really easy to implement since the IP address is always available in an HTTP request header and no additional settings need to be performed.  
  
This type of load balancing can be useful if your clients are likely to have disabled cookies.  
  
However, there is a downside to this approach. If any of your users are behind a NATed IP address then all of them will end up using the same server node. This may cause an uneven load on your server nodes.  
  
NATed IP address is really common, in fact, anytime you are browsing from an office network its likely that you and all your coworkers are using same NATed IP address.  

#### What Is Fail Over?
Failover means switching to another machine when one of the machines fails.  
  
Failover is an important technique in achieving high availability. Typically a load balancer is configured to fail over to another machine when the main machine fails.  
  
To achieve the least downtime, most load balancers support a feature of heartbeat check. This ensures that the target machine is responding. As soon as a heartbeat signal fails, load balancer stops sending the request to that machine and redirects to other machines or cluster.  

#### What Is Session Replication?
Session replication is used in application server clusters to achieve session failover.  
A user session is replicated to other machines of a cluster, every time the session data changes.  
If a machine fails, the load balancer can simply send incoming requests to another server in the cluster.  
The user can be sent to any server in the cluster since all machines in a cluster have a copy of the session.  
  
Session replication may allow your application to have session failover but it may require you to have extra cost in terms of memory and network bandwidth.

### Job Queues
In system software, a job queue, is a data structure maintained by job scheduler software containing jobs to run. Users submit their programs that they want executed, “jobs”, to the queue for batch processing. The scheduler software maintains the queue as the pool of jobs available for it to run.

### Full-text Search Service
While it’s possible to do full-text search directly from some databases (e.g., MySQL supports full-text search), it’s typical to run a separate “search service” that computes and stores the inverted index and provides a query interface. The most popular full-text search platform today is  Elasticsearch  though there are other options such as  Sphinx  or Apache Solr.

### Cloud storage
Cloud storage is a cloud computing model that stores data on the Internet through a cloud computing provider who manages and operates data storage as a service. It’s delivered on demand with just-in-time capacity and costs, and eliminates buying and managing your own data storage infrastructure. This gives you agility, global scale and durability, with “anytime, anywhere” data access.

### CDN
A content delivery network (CDN) refers to a geographically distributed group of servers which work together to provide fast delivery of Internet content. A CDN allows for the quick transfer of assets needed for loading Internet content including HTML pages, javascript files, stylesheets, images, and videos. The popularity of CDN services continues to grow, and today the majority of web traffic is served through CDNs, including traffic from major sites like Facebook, Netflix, and Amazon.

### What Is CAP Theorem?
The CAP Theorem for distributed computing was published by Eric Brewer, This states that it is not possible for a distributed computer system to simultaneously provide all three of the following guarantees:  
1.  Consistency (all nodes see the same data even at the same time with concurrent updates )
2.  Availability (a guarantee that every request receives a response about whether it was successful or failed)
3.  Partition tolerance (the system continues to operate despite arbitrary message loss or failure of part of the system)

The CAP acronym corresponds to these 3 guarantees. This theorem has created the base for modern distributed computing approaches.  
  
Worlds most high volume traffic companies (e.g. Amazon, Google, Facebook) use this as the basis for deciding their application architecture.  
  
It's important to understand that only two of these three conditions can be guaranteed to be met by a system.  
  
### What Is Sharding?
Sharding is an architectural approach that distributes a single logical database system into a cluster of machines.  
  
Sharding is Horizontal partitioning design scheme. In this database design rows of a database table are stored separately, instead of splitting into columns (like in normalization and vertical partitioning). Each partition is called a shard, which can be independently located on a separate database server or physical location.  
  
Sharding makes a database system highly scalable. The total number of rows in each table in each database is reduced since the tables are divided and distributed into multiple servers. This reduces the index size, which generally means improved search performance.  
  
The most common approach for creating shards is by the use of consistent hashing of a unique id in the application (e.g. user id).  
  
**The downsides of sharding are,**  
-   It requires the application to be aware of the data location.
-   Any addition or deletion of nodes from the system will require some rebalance to be done in the system.
-   If you require a lot of cross-node join queries then your performance will be really bad. Therefore, knowing how the data will be used for querying becomes really important.
-   A wrong sharding logic may result in worse performance. Therefore make sure you shard based on the application need.

### What Is ACID Property Of A System?
ACID is an acronym which is commonly used to define the properties of a relational database system, it stands for the following terms  
-   **Atomicity**  - This property guarantees that if one part of the transaction fails, the entire transaction will fail, and the database state will be left unchanged.
-   **Consistency**  - This property ensures that any transaction will bring the database from one valid state to another.
-   **Isolation**  - This property ensures that the concurrent execution of transactions results in a system state that would be obtained if transactions were executed serially.
-   **Durable**  - means that once a transaction has been committed, it will remain so, even in the event of power loss.

### What Is BASE Property Of A System?
BASE properties are the common properties of recently evolved NoSQL databases. According to CAP theorem, a BASE system does not guarantee consistency. This is a contrived acronym that is mapped to following property of a system in terms of the CAP theorem  
-   **Basically available**  indicates that the system is guaranteed to be available
-   Soft state indicates that the state of the system may change over time, even without input. This is mainly due to the eventually consistent model.
-   **Eventual consistency**  indicates that the system will become consistent over time, given that the system doesn't receive input during that time.
- 
### What Does Eventually Consistent Mean?
Unlike  relational database property of Strict consistency, eventual consistency property of a system ensures that any transaction will eventually (not immediately) bring the database from one valid state to another. This means there can be intermediate states that are not consistent between multiple nodes.

Eventually consistent systems are useful at scenarios where absolute consistency is not critical. For example in case of Twitter status update, if some users of the system do not see the latest status from a particular user its may not be very devastating for system.

Eventually consistent systems can not be used for use cases where absolute/strict consistency is required. For example a banking transactions system can not be using eventual consistency since it must consistently have the state of a transaction at any point of time. Your account balance should not show different amount if accessed from different ATM machines.

### What Is Shared Nothing Architecture? How Does It Scale?
A shared nothing architecture (SN) is a distributed computing approach in which each node is independent and self-sufficient, and there is no single point of contention required across the system.  
  -   This means no resources are shared between nodes (No shared memory, No shared file storage)
-   The nodes are able to work independently without depending on each other for any work.
-   Failure on one node affects only the users of that node, however other nodes continue to work without any disruption.

This approach is highly scalable since it avoids the existence of a single bottleneck in the system. Shared nothing is recently become popular for web development due to its linear scalability. Google has been using it for a long time.  
  
In theory, A shared nothing system can scale almost infinitely simply by adding nodes in the form of inexpensive machines.

### What Do You Mean By High Availability?
Having better service capacity with high availability and low latency is mission critical for almost all businesses.  
  
Availability means the ability of the application used to access the system, If a user cannot access the application, it is assumed unavailable. High Availability means the application will be available, without interruption.  
  
Achieving high availability for an application is not always an easy task. Using redundant server nodes with clustering is a common way to achieve a higher level of availability in web applications.  
  
Availability is commonly expressed as a percentage of uptime in a given year.  
  
For example, web-based maintenance management software applications are commonly mission-critical for most manufacturing businesses and availability is of much importance. This is because a skipped maintenance job can cause mechanical failure resulting in much higher repair costs for the business in addition to serious manufacturing process disruptions.

### What Is A Cluster?

A cluster is the group of computing machines that can individually run the software. Clusters are typically utilized to achieve high availability for server software.  
  
Clustering is used in many types of servers for high availability.  

-   **App Server Cluster**  
    An app server cluster is the group of machines that can run an application server that can be reliably utilized with a minimum of downtime.
-   **Database Server Cluster**  
    A database server cluster is the group of machines that can run a database server that can be reliably utilized with a minimum of downtime.
 

### Why Do You Need Clustering?
Clustering is needed for achieving high availability for server software. The main purpose of clustering is to achieve 100% availability or a zero downtime in service.  
  
Typical server software can be running on one computer machine and it can serve as long as there is no hardware failure or some other failure.  
  
By creating a cluster of more than one machine, we can reduce the chances of our service going un-available in case one of the machines fails.  
  
Doing clustering does not always guarantee that service will be 100% available since there can still be a chance that all the machine in a cluster fails at the same time. However, it is not very likely in case you have many machines and they are located at a different location or supported by their own resources.

### How Do You Update A Live Heavy Traffic Site With Minimum Or Zero Down Time?
Deploying a newer version of a live website can be a challenging task especially when a website has high traffic. Any downtime is going to affect the users. There are a few best practices that we can follow  
  
**Before deploying on Production**  
-   Thoroughly test the new changes and ensure it works in a test environment which is almost identical to a production system.
-   If possible do automation of test cases as much as possible. We use selenium for a lot of functional testing.
-   Create an automated sanity testing script (also called as the smoke test) that can be run on production (without affecting real data). These are typically the read-only type of test cases. However, depending on your application needs, you can add more cases to this. Make sure it can be run quickly by keeping it short.
-   Create scripts for all manual tasks(if possible), avoiding any hand typing mistakes during a day of deployment.
-   Test the script to make sure they work in a non-production environment.
-   Keep the build artifacts ready. e.g application deployment files, database scripts, config files, etc.
-   Create a checklist of things to do on a day of deployment.
-   Rehearse. Deploy in a non-prod environment is almost identical to production. Try this with production data volumes(if possible). Make a note of the time required for your tasks so you can plan accordingly.
 
**When doing deploying on a production environment.**  
-   Keep backup of current site/data to be able to rollback.
-   Use sanity test cases before doing a lot of in-depth testing.
