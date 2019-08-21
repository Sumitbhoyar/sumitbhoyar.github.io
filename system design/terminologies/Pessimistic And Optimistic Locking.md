# Pessimistic And Optimistic Locking

#### Q: What do Pessimistic Locking and Optimistic Locking mean?

**Pessimistic Locking**: It assumes the worst. It thinks conflicts are very likely to happen. So it locks as early as it can.

**Optimistic Locking**: It assumes conflicts are unlikely to happen, though it might happen. So it locks as late as it can.

Conclusions:

- Pessimistic locking provides better integer with the cost of performance. Many financial transactions would probably need to use pessimistic locking for data integrity.
- Optimistic locking is useful, if our DB has lots of read and very rare writes. Most web applications are fine with dirty reads – on the rare occasion the data doesn’t exactly tally the next reload does.

#### Q: What is CAS? Please explain the workflow of Optimistic Locking.

**CAS: check-and-set**

CAS determines if an object has been updated by another client between the time it was initially read and the time the save was attempted.

Optimistic Locking is a strategy where you read a record, take note of a version number (other methods to do this involve dates, timestamps or checksums/hashes) and check that the version hasn’t changed before you write the record back.

#### Q: Would pessimistic locking leads to dirty reads at application level?

With pessimistic locking, you may have read outdated data.

But thanks to CAS mechanism, the updates are guaranteed to be correct.

#### Q: As a developer, how I can benefit from knowing the difference?

Let’s say you need to implement a counter service.

You might choose pessimistic/optimistic locking differently, depending on the requirements.

- Optimistic Locking: This strategy is most applicable to high-volume systems and three-tier architectures where you do not necessarily maintain a connection to the database for your session. In this situation the client cannot actually maintain database locks as the connections are taken from a pool and you may not be using the same connection from one access to the next. See more.
- To use pessimistic locking you need either a direct connection to the database (as would typically be the case in a two tier client server application) or an externally available transaction ID that can be used independently of the connection.

## References:
- https://architect.dennyzhang.com/design-locks/