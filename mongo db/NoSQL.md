# NoSQL

### What is NoSQL?
NoSQL is a non-relational DMS, that does not require a fixed schema, avoids joins, and is easy to scale. NoSQL database is used for distributed data stores with humongous data storage needs. 

### Features of NoSQL
##### Non-relational
- NoSQL databases never follow the relational model
- Never provide tables with flat fixed-column records
- Work with self-contained aggregates or BLOBs
- Doesn't require object-relational mapping and data normalization
- No complex features like query languages, query planners,
- referential integrity joins, ACID

##### Schema-free

- NoSQL databases are either schema-free or have relaxed schemas
- Do not require any sort of definition of the schema of the data
- Offers heterogeneous structures of data in the same domain

##### Simple API

- Offers easy to use interfaces for storage and querying data provided
- APIs allow low-level data manipulation & selection methods
- Text-based protocols mostly used with HTTP REST with JSON
- Mostly used no standard based query language
- Web-enabled databases running as internet-facing services

##### Distributed

- Multiple NoSQL databases can be executed in a distributed fashion
- Offers auto-scaling and fail-over capabilities
- Often ACID concept can be sacrificed for scalability and throughput
- Mostly no synchronous replication between distributed nodes Asynchronous Multi-Master Replication, peer-to-peer, HDFS Replication
- Only providing eventual consistency
- Shared Nothing Architecture. This enables less coordination and higher distribution.

### Types of NoSQL Databases
##### Key Value Pair Based
Data is stored in key/value pairs.
Key-value pair storage databases store data as a hash table where each key is unique, and the value can be a JSON, BLOB(Binary Large Objects), string, etc.
Use cases: Sessions of each player in multi-player game, shopping cart contents
Examples: Redis, Dynamo, Riak. They are all based on Amazon's Dynamo paper.

##### Column-based
Column-oriented databases work on columns and are based on BigTable paper by Google. Every column is treated separately. Values of single column databases are stored contiguously.

Supplier-Parts would be stored on disk or in memory something like:

S1S2S3S4S5;2010302030;LondonParisParisLondonAthens;SmithJonesBlakeClarkAdams 
This is in contrast to a traditional rowstore which would store the data more like this:

S120LondonSmith;S210ParisJones;S330ParisBlake;S420LondonClark;S530AthensAdams

From this simple concept flows all of the fundamental differences in performance, for better or worse, between a column-store and a row-store. For example, a column store will excel at doing aggregations like totals and averages, but inserting a single row can be expensive, while the inverse holds true for row-stores.

They deliver high performance on aggregation queries like SUM, COUNT, AVG, MIN etc. as the data is readily available in a column.

Use cases: data warehouses, business intelligence, CRM, Library card catalogs,

Examples: HBase, Cassandra, HBase, Hypertable.

##### Document-Oriented:
Document-Oriented NoSQL DB stores and retrieves data as a key value pair but the value part is stored as a document. The document is stored in JSON or XML formats. The value is understood by the DB and can be queried.

Use Cases: CMS systems, blogging platforms, real-time analytics & e-commerce applications. It should not use for complex transactions which require multiple operations or queries against varying aggregate structures.

Examples: Amazon SimpleDB, CouchDB, MongoDB, Riak, Lotus Notes, MongoDB, are popular Document originated DBMS systems.

##### Graph-Based: 
A graph type database stores entities as well the relations amongst those entities. The entity is stored as a node with the relationship as edges. An edge gives a relationship between nodes. Every node and edge has a unique identifier.
Traversing relationship is fast as they are already captured into the DB, and there is no need to calculate them.

Use cases: social networks, logistics, spatial data.

Examples: Neo4J, Infinite Graph, OrientDB, FlockDB.

### Advantages of NoSQL
- Can be used as Primary or Analytic Data Source
- Big Data Capability
- No Single Point of Failure
- Easy Replication
- No Need for Separate Caching Layer
- It provides fast performance and horizontal scalability.
- Can handle structured, semi-structured, and unstructured data with equal effect
- Object-oriented programming which is easy to use and flexible
- NoSQL databases don't need a dedicated high-performance server
- Support Key Developer Languages and Platforms
- Simple to implement than using RDBMS
- It can serve as the primary data source for online applications.
- Handles big data which manages data velocity, variety, volume, and complexity
- Excels at distributed database and multi-data center operations
- Eliminates the need for a specific caching layer to store data
- Offers a flexible schema design which can easily be altered without downtime or service disruption

### Disadvantages of NoSQL
- No standardization rules
- Limited query capabilities
- RDBMS databases and tools are comparatively mature
- It does not offer any traditional database capabilities, like consistency when multiple transactions are performed simultaneously.
- When the volume of data increases it is difficult to maintain unique values as keys become difficult
- Doesn't work as well with relational data
- The learning curve is stiff for new developers
- Open source options so not so popular for enterprises.

### Eventual Consistency
The term "eventual consistency" means to have copies of data on multiple machines to get high availability and scalability. Thus, changes made to any data item on one machine has to be propagated to other replicas.

Data replication may not be instantaneous as some copies will be updated immediately while others in due course of time. These copies may be mutually, but in due course of time, they become consistent. Hence, the name eventual consistency.

### ACID vs BASE
ACID: Atomicity, Consistency, Isolation, Durability
BASE: Basic Availability, Soft state, Eventual consistency

Basically, available means DB is available all the time as per CAP theorem
Soft state means even without an input; the system state may change. This could be due to changes done on other node eventually reflects. 
Eventual consistency means that the system will become consistent over time
