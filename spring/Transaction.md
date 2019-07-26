# Transaction Management

### Type of Transaction Management
In J2EE, Transaction Management can be divided in two types.

##### Global Transaction
- Use to work with multiple transaction resources like RDBMS or Message Queue (Pros)
- Managed by Application Server (WebSphere, Weblogic) using JTA (Cons)
- JNDI is required to use JTA
- Code can not be reused as JTA is available at server level(Cons)
- Example of Global Transaction : EJB CMT

##### Local Transaction
- Use to work with specific resource(transaction associated with JDBC)
- Can not work across multiple transaction resource opposite to Global transaction (cons)
- Most of web application uses only single resources hence it is best option to use in normal app.

### Different Approach for transaction management
Spring supports two different approach for transaction management.

- **Programmatic Transaction Management** : Here you will write code for transaction management.Spring API dependency. Not good for maintenance. Good for development. Flexibity.

- **Declarative Transaction Management** : Here you will use XML or annotation for transaction management. Less flexible but preferable over programmatic approach. In normal case no code is required for transaction management.

### JDBC Transaction management
```
try{
	connection.setAutoCommit(false);
	.
	.
	con.commit();
catch(Exception e){
	con.rollback();
}
```

### Spring Transaction Abstractions
The key to the Spring transaction abstraction is defined by the org.springframework.transaction.PlatformTransactionManager interface, which is as follows −
```
public interface PlatformTransactionManager {
   TransactionStatus getTransaction(TransactionDefinition definition);
   throws TransactionException;
   void commit(TransactionStatus status) throws TransactionException;
   void rollback(TransactionStatus status) throws TransactionException;
}
```

The TransactionDefinition is the core interface of the transaction support in Spring and it is defined as follows −
```
public interface TransactionDefinition {
   int getPropagationBehavior();
   int getIsolationLevel();
   String getName();
   int getTimeout();
   boolean isReadOnly();
}
```

##### Following are the possible values for propagation types −

- **PROPAGATION_MANDATORY** : Supports a current transaction; throws an exception if no current transaction exists.

- **PROPAGATION_NESTED** - Executes within a nested transaction if a current transaction exists.

- **PROPAGATION_NEVER** - Does not support a current transaction; throws an exception if a current transaction exists.

- **PROPAGATION_NOT_SUPPORTED** - Does not support a current transaction; rather always execute nontransactionally.

- **PROPAGATION_REQUIRED** : Supports a current transaction; creates a new one if none exists.

- **PROPAGATION_REQUIRES_NEW** : Creates a new transaction, suspending the current transaction if one exists.

- **PROPAGATION_SUPPORTS** : Supports a current transaction; executes non-transitionally if none exists.

- **TIMEOUT_DEFAULT**: Uses the default timeout of the underlying transaction system, or none if timeouts are not supported.

### Spring transaction
Spring supports two types of transaction management:

- **Programmatic transaction management**: This means that you have to manage the transaction with the help of programming. That gives you extreme flexibility, but it is difficult to maintain.
```
EntityManagerFactory factory = Persistence.createEntityManagerFactory("PERSISTENCE_UNIT_NAME");
EntityManager entityManager = entityManagerFactory.createEntityManager(); 
Transaction transaction = entityManager.getTransaction() 
try 
{  
   transaction.begin(); 
   someBusinessCode(); 
   transaction.commit(); 
} 
catch(Exception ex) 
{ 
   transaction.rollback();  
   throw ex; 
}
```
- **Declarative transaction management**: This means you separate transaction management from the business code. You only use annotations or XML-based configuration to manage the transactions.

Steps

Add @EnableTransactionManagement to your configuration class. 

Add the @Transactional annotation to the Class (or method in a class) or Interface (or method in an interface).

If we’re using a Spring Boot project, and have a spring-data-* or spring-tx dependencies on the classpath, then transaction management will be enabled by default.
 
@Transactional annotation can be applied over methods as well as whole class. If you want all your methods to have transaction management features, you should annotate your class with this annotation.

### Distributed transaction management

#### Two-Phase Commit Protocol
Two-phase commit protocol (or 2PC) is a mechanism for implementing a transaction across different software components (multiple databases, message queues etc.)

One of the important participants in a distributed transaction is the transaction coordinator. The distributed transaction consists of two steps:

- Prepare phase — during this phase, all participants of the transaction prepare for commit and notify the coordinator that they are ready to complete the transaction
- Commit or Rollback phase — during this phase, either a commit or a rollback command is issued by the transaction coordinator to all participants

The XA standard is a specification for conducting the 2PC distributed transactions across the supporting resources. Any JTA-compliant application server (JBoss, GlassFish etc.) supports it out-of-the-box.

However, to take advantage of this mechanism, the resources have to be deployed to a single JTA platform. This isn’t always feasible for a microservice architecture.

#### Saga pattern / Compensation based transaction management
The Saga pattern is another widely used pattern for distributed transactions. It is different from 2pc, which is synchronous. The Saga pattern is asynchronous and reactive. In a Saga pattern, the distributed transaction is fulfilled by asynchronous local transactions on all related microservices. The microservices communicate with each other through an event bus.

- Advantages of the Saga pattern: One big advantage of the Saga pattern is its support for long-lived transactions. Because each microservice focuses only on its own local atomic transaction, other microservices are not blocked if a microservice is running for a long time. This also allows transactions to continue waiting for user input. 

- Disadvantages of the Saga pattern: The Saga pattern is difficult to debug, especially when many microservices are involved. Also, the event messages could become difficult to maintain if the system gets complex. Another disadvantage of the Saga pattern is it does not have read isolation. For example, the customer could see the order being created, but in the next second, the order is removed due to a compensation transaction.

##### Example 1: 

The OrderMicroservice receives a request to place an order. It first starts a local transaction to create an order and then emits an OrderCreated event. The CustomerMicroservice listens for this event and updates a customer fund once the event is received. If a deduction is successfully made from a fund, a CustomerFundUpdated event will then be emitted, which in this example means the end of the transaction.

If any microservice fails to complete its local transaction, the other microservices will run compensation transactions to rollback the changes.

In the above example, the UpdateCustomerFund failed for some reason and it then emitted a CustomerFundUpdateFailed event. The OrderMicroservice listens for the event and start its compensation transaction to revert the order that was created.

##### Example 2: 

A travel website lets customers book itineraries. A single itinerary might comprise a series of flights and hotels. A customer traveling from Seattle to London and then on to Paris could perform the following steps when creating an itinerary:

- Book a seat on flight F1 from Seattle to London.
- Book a seat on flight F2 from London to Paris.
- Book a seat on flight F3 from Paris to Seattle.
- Reserve a room at hotel H1 in London.
- Reserve a room at hotel H2 in Paris.

These steps constitute an eventually consistent operation, although each step is a separate action. Therefore, as well as performing these steps, the system must also record the counter operations necessary to undo each step in case the customer decides to cancel the itinerary. The steps necessary to perform the counter operations can then run as a compensating transaction.

Notice that the steps in the compensating transaction might not be the exact opposite of the original steps, and the logic in each step in the compensating transaction must take into account any business-specific rules. For example, unbooking a seat on a flight might not entitle the customer to a complete refund of any money paid. 

