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

# Checksum

A checksum is the outcome of running an algorithm, called a  cryptographic hash function , on a piece of data, usually a single  file. Comparing the checksum that you generate from your version of the file, with the one provided by the source of the file, helps ensure that your copy of the file is genuine and error free.
Even a minuscule change in the file will produce a vastly different checksum, making it very clear that one is not like the other.

A checksum is also sometimes called a  _hash sum_  and less often a  _hash value_,  _hash code_, or simply a  _hash_.

Although **hashing and checksums** are similar in that they both create a value based on the contents of a file, hashing is not the same as creating a checksum. A checksum is intended to verify (check) the integrity of data and identify data-transmission errors, while a hash is designed to create a unique digital fingerprint of the data.

Checksums are useful for verifying that a file you downloaded from somewhere other than the original source is, in fact, a valid file and hasn't been altered, maliciously or otherwise, from the original. Just compare the hash you create with the one available from the file's source.

# Proxy
A forward proxy, often called a proxy, proxy server, or web proxy, is a server that sits in front of a group of client machines. When those computers make requests to sites and services on the Internet, the proxy server intercepts those requests and then communicates with web servers on behalf of those clients, like a middleman.
![Forward Proxy Flow](https://www.cloudflare.com/img/learning/cdn/glossary/reverse-proxy/forward-proxy-flow.svg)
Why would anyone add this extra middleman to their Internet activity? There are a few reasons one might want to use a forward proxy:

-   **To avoid state or institutional browsing restrictions**  - Some governments, schools, and other organizations use firewalls to give their users access to a limited version of the Internet. A forward proxy can be used to get around these restrictions, as they let the user connect to the proxy rather than directly to the sites they are visiting.
-   **To block access to certain content**  - Conversely, proxies can also be set up to block a group of users from accessing certain sites. For example, a school network might be configured to connect to the web through a proxy which enables content filtering rules, refusing to forward responses from Facebook and other social media sites.
-   **To protect their identity online**  - In some cases, regular Internet users simply desire increased anonymity online, but in other cases, Internet users live in places where the government can impose serious consequences to political dissidents. Criticizing the government in a web forum or on social media can lead to fines or imprisonment for these users. If one of these dissidents uses a forward proxy to connect to a website where they post politically sensitive comments, the IP address used to post the comments will be harder to trace back to the dissident. Only the IP address of the proxy server will be visible.

# Reverse Proxy
A reverse proxy is a server that sits in front of one or more web servers, intercepting requests from clients. This is different from a forward proxy, where the proxy sits in front of the clients. With a reverse proxy, when clients send requests to the origin server of a website, those requests are intercepted at the network edge by the reverse proxy server. The reverse proxy server will then send requests to and receive responses from the origin server.
![Reverse Proxy Flow](https://www.cloudflare.com/img/learning/cdn/glossary/reverse-proxy/reverse-proxy-flow.svg)

Below we outline some of the benefits of a reverse proxy:

-   **Load balancing**  - A popular website that gets millions of users every day may not be able to handle all of its incoming site traffic with a single origin server. Instead, the site can be distributed among a pool of different servers, all handling requests for the same site. In this case, a reverse proxy can provide a load balancing solution which will distribute the incoming traffic evenly among the different servers to prevent any single server from becoming overloaded. In the event that a server fails completely, other servers can step up to handle the traffic.
-   **Protection from attacks**  - With a reverse proxy in place, a web site or service never needs to reveal the IP address of their origin server(s). This makes it much harder for attackers to leverage a targeted attack against them, such as a  DDoS attack. Instead the attackers will only be able to target the reverse proxy, such as Cloudflare’s  [CDN], which will have tighter security and more resources to fend off a cyber attack.
-   **[Global Server Load Balancing]  (GSLB)**  - In this form of load balancing, a website can be distributed on several servers around the globe and the reverse proxy will send clients to the server that’s geographically closest to them. This decreases the distances that requests and responses need to travel, minimizing load times.
-   **Caching**  - A reverse proxy can also cache  content, resulting in faster performance. For example, if a user in Paris visits a reverse-proxied website with web servers in Los Angeles, the user might actually connect to a local reverse proxy server in Paris, which will then have to communicate with an origin server in L.A. The proxy server can then cache (or temporarily save) the response data. Subsequent Parisian users who browse the site will then get the locally cached version from the Parisian reverse proxy server, resulting in much faster performance.
-   **SSL encryption**  -  Encrypting and decrypting  SSL (or  TLS) communications for each client can be computationally expensive for an origin server. A reverse proxy can be configured to decrypt all incoming requests and encrypt all outgoing responses, freeing up valuable resources on the origin server.
- 
Source: https://www.cloudflare.com/en-in/learning/cdn/glossary/reverse-proxy/

# Caching
Caching is a mechanism to improve the performance of any type of application. Technically, caching is the process of storing and accessing data from a cache. But wait, what is a cache? A cache is a software or hardware component aimed at storing data so that future requests for the same data can be served faster.

### Challenges
##### Coherence Problem

Since whenever data is cached, a copy is created, there are now two copies of the same data. This means that they can diverge over time.
Identifying the best cache update or invalidation mechanism is one of the biggest challenges related to caching.

##### Choosing Data to Be Cached

Virtually any kind of data can be cached. This means that choosing what should reside in our cache and what to exclude is open to endless possibilities.
- If we expect data to change often, we should not want to cache it for too long. Otherwise, we may offer users inaccurate data. On the other hand, this also depends on how much time we can tolerate stale data. 
- Our cache should always be ready to store frequently required data taking a large amount of time to be generated or retrieved. Identifying this data is not an easy task, and you might risk filling our cache with useless data. 
- By caching large data, you may fill your cache very rapidly, or worse, using all available memory. If your RAM is shared between your application and your caching system, this can easily become a problem, which is why you should limit the amount of your RAM reserved for caching.

##### Dealing with Cache-misses

Cache misses represent the time-based cost of having a cache. In fact, cache misses introducing latencies that would not have been incurred in a system not using caching. So, to benefit from the speed boost deriving from having a cache, cache misses must be kept relatively lows. In particular, they should be low compared to cache hits. Reaching this result is not easy, and if not achieved, our caching system can turn into nothing more than overhead.

### Types of caching
##### In-memory Caching

In this approach, cached data is stored directly in RAM, which is assumed to be faster than the typical storing system where the original data is located. The most common implementation of this type of caching is based on key-value databases. They can be seen as sets of key-value pairs. The  _key_  is represented by a unique value, while the  _value_  by the cached data.

##### Database Caching

Each database usually comes with some level of caching. Specifically, an internal cache is generally used to avoid querying a database excessively. By caching the result of the last queries executed, the database can provide the data previously cached immediately.

##### Web Caching

This can be divided into two further subcategories:

- ##### Web Client Caching

It is usually part of browsers, it is also called  _Web Browser Caching_. The first time a browser loads a web page, it stores the page resources, such as text, images, stylesheets, scripts, and media files. The next time the same page is hit, the browser can look in the cache for resources that were previously cached and retrieve them from the user’s machine. This is generally way faster than download them from the network.

- ##### Web Server Caching

This is a mechanism aimed at storing resources server-side for reuse. Specifically, such an approach is helpful when dealing with dynamically generated content, which takes time to be created. Conversely, it is not useful in the case of static content. Web server caching avoids servers from getting overloaded, reducing the work to be done, and improves the page delivery speed.

##### CDN Caching

CDN stands for  _Content Delivery Network, and_  it is aimed at caching content, such as web pages, stylesheets, scripts, and media files, in proxy servers. It can be seen as a system of gateways between the user and the origin server, storing its resources. When the user requires a resource, a proxy server intercepts it and checks to see if it has a copy. If so, the resource is immediately delivered to the user; otherwise, the request is forwarded to the origin server. These proxy servers are placed in a vast number of locations worldwide, and user requests are dynamically routed to the nearest one.

### Cache Invalidation

It requires some maintenance to keep the cache coherent with the source of truth (e.g., database). If the data is modified in the database, it should be invalidated in the cache; if not, this can cause inconsistent application behavior.

Solving this problem is known as cache invalidation; there are three main schemes that are used:

**Write-through cache:**  Under this scheme, data is written into the cache and the corresponding database simultaneously. The cached data allows for fast retrieval and, since the same data gets written in the permanent storage, we will have complete data consistency between the cache and the storage. Also, this scheme ensures that nothing will get lost in case of a crash, power failure, or other system disruptions.

Although, write-through minimizes the risk of data loss, since every write operation must be done twice before returning success to the client, this scheme has the disadvantage of higher latency for write operations.

**Write-around cache:**  This technique is similar to write-through cache, but data is written directly to permanent storage, bypassing the cache. This can reduce the cache being flooded with write operations that will not subsequently be re-read, but has the disadvantage that a read request for recently written data will create a “cache miss” and must be read from slower back-end storage and experience higher latency.

**Write-back cache:**  Under this scheme, data is written to cache alone, and completion is immediately confirmed to the client. The write to the permanent storage is done after specified intervals or under certain conditions. This results in low-latency and high-throughput for write-intensive applications; however, this speed comes with the risk of data loss in case of a crash or other adverse event because the only copy of the written data is in the cache.

### Cache eviction policies

Following are some of the most common cache eviction policies:

1.  First In First Out (FIFO): The cache evicts the first block accessed first without any regard to how often or how many times it was accessed before.
2.  Last In First Out (LIFO): The cache evicts the block accessed most recently first without any regard to how often or how many times it was accessed before.
3.  Least Recently Used (LRU): Discards the least recently used items first.
4.  Most Recently Used (MRU): Discards, in contrast to LRU, the most recently used items first.
5.  Least Frequently Used (LFU): Counts how often an item is needed. Those that are used least often are discarded first.
6.  Random Replacement (RR): Randomly selects a candidate item and discards it to make space when necessary.

# Quorum
In a distributed environment, a quorum is the minimum number of servers on which a distributed operation needs to be performed successfully before declaring the operation’s overall success.

Minimum number of nodes in cluster that must be online and be able to communicate with each other. If any additional node failure occurs beyond this threshold, cluster will stop running.

**Deciding on number of servers in a cluster**
The cluster can function only if majority of servers are up and running. In systems doing data replication, there are two things to consider:

-   The throughput of write operations.

Every time data is written to the cluster, it needs to be copied to multiple servers. Every additional server adds some overhead to complete this write. The latency of data write is directly proportional to the number of servers forming the quorum. As we will see below, doubling the number of servers in a cluster will reduce throughput to half of the value for the original cluster.

-   The number of failures which need to be tolerated.

The number of server failures tolerated is dependent on the size of the cluster. But just adding one more server to an existing cluster doesn't always give more fault tolerance: adding one server to a three server cluster doesn't increase failure tolerance.

Considering these two factors, most practical quorum-based systems have cluster sizes of three or five. A five-server cluster tolerates two server failures and has tolerable data write throughput of few thousand requests per second.

**What value should we choose for Quorum?**

More than half of the number of nodes in cluster. (N/2 + 1)  where N is total number of nodes in cluster. Eg:  
_In a 5-node cluster, 3 voters must be online to have majority.  
In a 4-node cluster, 3 voters must be online to have majority._  
With 5-node it can afford 2 node failures whereas with 4-node it can afford only 1 node failure, because of this logic, it is recommended to always have an odd number of total nodes in the cluster.  
**_Note: Each node has 1 vote._**

**What happens when there is “Split” or “Cluster Partitioning”**

Network problems can cause communication failures among cluster nodes. One set of nodes might be able to communicate together across a functioning part of a network but not be able to communicate with a different set of nodes in another part of the network. This is known as “split” in cluster or “cluster partitioning”.

Now the partition which has quorum is allowed to continue running the application. The other partitions are removed from cluster.

**What if cluster splits into two partitions with equal number of working nodes in each?**

Its a tie situation, this can be resolve by giving the the voting members some way to perform a tiebreak, may be by giving a member a “super vote” or by disabling one members vote.
