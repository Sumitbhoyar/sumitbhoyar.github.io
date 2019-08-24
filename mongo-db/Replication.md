
# Replication

A replica set in MongoDB is a group of mongod processes that maintain the same data set. Replica sets provide redundancy and high availability

Replication provides redundancy and increases data availability. With multiple copies of data on different database servers, replication provides a level of fault tolerance against the loss of a single database server.

### Replica Set Primary
The primary is the only member in the replica set that receives write operations. MongoDB applies write operations on the primary and then records the operations on the primary’s oplog. Secondary members replicate this log and apply the operations to their data sets.

All members of the replica set can accept read operations. However, by default, an application directs its read operations to the primary member. This default  behavior could be changed.

The replica set can have at most one primary. If the current primary becomes unavailable, an election determines the new primary.

### Replica Set Secondary Members
A secondary maintains a copy of the primary’s data set. To replicate data, a secondary applies operations from the primary’s oplog to its own data set in an asynchronous process. A replica set can have one or more secondaries.

Although clients cannot write data to secondaries, clients can read data from secondary members. 
A secondary can become a primary. If the current primary becomes unavailable, the replica set holds an election to choose which of the secondaries becomes the new primary.

You can configure a secondary member for a specific purpose. You can configure a secondary to:

- Prevent it from becoming a primary in an election, which allows it to reside in a secondary data center or to serve as a cold standby. Also called as priority 0 member.
- Configure a secondary to have priority 0 to prevent it from becoming primary, which is particularly useful in multi-data center deployments.
- In many cases, you need not set standby to priority 0. However, in replica sets with varied hardware or geographic distribution, a priority 0 standby ensures that only certain members become primary.
- Prevent applications from reading from it, which allows it to run applications that require separation from normal traffic. 
- Hidden members, however, may vote in elections.
- Use hidden members for dedicated tasks such as reporting and backups.
- Keep a running “historical” snapshot for use in recovery from certain errors, such as unintentionally deleted databases.
Because delayed members are a “rolling backup” or a running “historical” snapshot of the data set, they may help you recover from various kinds of human error. For example, a delayed member can make it possible to recover from unsuccessful application upgrades and operator errors including dropped databases and collections.

### Replica Set Arbiter
An arbiter does not have a copy of data set and cannot become a primary. Replica sets may have arbiters to add a vote in elections for primary. Arbiters always have exactly 1 election vote, and thus allow replica sets to have an uneven number of voting members without the overhead of an additional member that replicates data.


## Replica Set Elections

Replica sets use elections to determine which set member will become primary. Replica sets can trigger an election in response to a variety of events, such as:

- Adding a new node to the replica set,
- initiating a replica set,
- performing replica set maintenance using methods such as rs.stepDown() or rs.reconfig(), and
- the secondary members losing connectivity to the primary for more than the configured timeout (10 seconds by default).

The replica set cannot process write operations until the election completes successfully. The replica set can continue to serve read queries if such queries are configured to run on secondaries.


