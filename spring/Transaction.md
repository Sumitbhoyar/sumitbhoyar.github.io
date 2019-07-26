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