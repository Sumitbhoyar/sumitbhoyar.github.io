**CAP Theorem**
---------------

The **CAP Theorem** states that, in a distributed system (a collection of interconnected nodes that share data.), you can only have two out of the following three guarantees across a write/read pair: Consistency, Availability, and Partition Tolerance - one of them must be sacrificed.

**Consistency** - A read is guaranteed to return the most recent write for a given client.
```
 _______	 _________
|Node 1	|	|Node 2	  |
| (x=5)	|------>| (x=5)	  |
|_______|	|_________|
```

**Availability** - A non-failing node will return a reasonable response within a reasonable amount of time (no error or timeout).
```
 _______		 ________
|Node 1	|		|Node 2	 |
|_______|		|________|
    ^		            ^
```
**Partition Tolerance** - The system will continue to function when network partitions occur.
```
 _______	 ________
|Node 1	|---|---|Node 2	 |
|_______|   |	|________|

```
**CP - Consistency/Partition Tolerance** - Wait for a response from the partitioned node which could result in a timeout error. The system can also choose to return an error, depending on the scenario you desire. Choose Consistency over Availability when your business requirements dictate atomic reads and writes.
MongoDB, HBase, Redis 

**AP - Availability/Partition Tolerance** - Return the most recent version of the data you have, which could be stale. This system state will also accept writes that can be processed later when the partition is resolved. Choose Availability over Consistency when your business requirements allow for some flexibility around when the data in the system synchronizes. Availability is also a compelling option when the system needs to continue to function in spite of external errors (shopping carts, etc.)

In the absence of network failure – that is, when the distributed system is running normally – both availability and consistency can be satisfied.

CAP is frequently misunderstood as if one had to choose to abandon one of the three guarantees at all times. In fact, **the choice is really between consistency and availability only** when a network partition or failure happens; at all other times, no trade-off has to be made.

Database systems designed with traditional ACID guarantees in mind such as RDBMS choose consistency over availability, whereas systems designed around the BASE philosophy, common in the NoSQL movement for example, choose availability over consistency.
