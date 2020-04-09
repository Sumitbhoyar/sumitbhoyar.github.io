# JPA

## Name some important interfaces of Hibernate framework?

Some of the important interfaces of Hibernate framework are:

1.  **SessionFactory (org.hibernate.SessionFactory)**: SessionFactory is an  immutable thread-safe cache of compiled mappings for a single database. We need to initialize SessionFactory once and then we can cache and reuse it. SessionFactory instance is used to get the Session objects for database operations.
2.  **Session (org.hibernate.Session)**: Session is a single-threaded, short-lived object representing a conversation between the application and the persistent store. It wraps JDBC  `java.sql.Connection`  and works as a factory for  `org.hibernate.Transaction`. We should open session only when it’s required and close it as soon as we are done using it. Session object is the interface between java application code and hibernate framework and provide methods for CRUD operations.
3.  **Transaction (org.hibernate.Transaction)**: Transaction is a single-threaded, short-lived object used by the application to specify atomic units of work. It abstracts the application from the underlying JDBC or JTA transaction. A org.hibernate.Session might span multiple org.hibernate.Transaction in some cases.

## Name some important annotations used for Hibernate mapping?

Hibernate supports JPA annotations and it has some other annotations in  `org.hibernate.annotations`  package. Some of the important JPA and hibernate annotations used are:

1.  **javax.persistence.Entity**: Used with model classes to specify that they are entity beans.
2.  **javax.persistence.Table**: Used with entity beans to define the corresponding table name in database.
3.  **javax.persistence.Access**: Used to define the access type, either field or property. Default value is field and if you want hibernate to use getter/setter methods then you need to set it to property.
4.  **javax.persistence.Id**: Used to define the primary key in the entity bean.
5.  **javax.persistence.EmbeddedId**: Used to define composite primary key in the entity bean.
6.  **javax.persistence.Column**: Used to define the column name in database table.
7.  **javax.persistence.GeneratedValue**: Used to define the strategy to be used for generation of primary key. Used in conjunction with  `javax.persistence.GenerationType`  enum.
8.  **javax.persistence.OneToOne**: Used to define the one-to-one mapping between two entity beans. We have other similar annotations as  `OneToMany`,  `ManyToOne`  and  `ManyToMany`
9.  **org.hibernate.annotations.Cascade**: Used to define the cascading between two entity beans, used with mappings. It works in conjunction with  `org.hibernate.annotations.CascadeType`
10.  **javax.persistence.PrimaryKeyJoinColumn**: Used to define the property for foreign key. Used with  `org.hibernate.annotations.GenericGenerator`  and  `org.hibernate.annotations.Parameter`

## What is Hibernate SessionFactory and how to configure it?
    
    SessionFactory is the factory class used to get the Session objects. SessionFactory is responsible to read the hibernate configuration parameters and connect to the database and provide Session objects. Usually an application has a single SessionFactory instance and threads servicing client requests obtain Session instances from this factory.
    
    The internal state of a SessionFactory is immutable. Once it is created this internal state is set. This internal state includes all of the metadata about Object/Relational Mapping.
    
    SessionFactory also provide methods to get the Class metadata and Statistics instance to get the stats of query executions, second level cache details etc.
    
## Hibernate SessionFactory is thread safe?
    
    Internal state of SessionFactory is immutable, so it’s thread safe. Multiple threads can access it simultaneously to get Session instances.
    

## What is Hibernate Session and how to get it?
    
    Hibernate Session is the interface between java application layer and hibernate. This is the core interface used to perform database operations. Lifecycle of a session is bound by the beginning and end of a transaction.
    
    Session provide methods to perform create, read, update and delete operations for a persistent object. We can execute HQL queries, SQL native queries and create criteria using Session object.
    

## Hibernate Session is thread safe?
    
    Hibernate Session object is not thread safe, every thread should get it’s own session instance and close it after it’s work is finished.

## How transaction management works in Hibernate?

Transaction management is very easy in hibernate because most of the operations are not permitted outside of a transaction. So after getting the session from SessionFactory, we can call session  `beginTransaction()`  to start the transaction. This method returns the Transaction reference that we can use later on to either commit or rollback the transaction.

Overall hibernate transaction management is better than JDBC transaction management because we don’t need to rely on exceptions for rollback. Any exception thrown by session methods automatically rollback the transaction.

## Which design patterns are used in Hibernate framework?
    
    Some of the design patterns used in Hibernate Framework are:
    
    -   Domain Model Pattern – An object model of the domain that incorporates both behavior and data.
    -   Data Mapper – A layer of Mappers that moves data between objects and a database while keeping them independent of each other and the mapper itself.
    -   Proxy Pattern:   for lazy loading
    -   Factory pattern:  in SessionFactory

## What are best practices to follow with Hibernate framework?
    
    Some of the best practices to follow in Hibernate are:
    
    -   Always check the primary key field access, if it’s generated at the database layer then you should not have a setter for this.
    -   By default hibernate set the field values directly, without using setters. So if you want hibernate to use setters, then make sure proper access is defined as  `@Access(value=AccessType.PROPERTY)`.
    -   If access type is property, make sure annotations are used with getter methods and not setter methods. Avoid mixing of using annotations on both filed and getter methods.
    -   Use native sql query only when it can’t be done using HQL, such as using database specific feature.
    -   If you have to sort the collection, use ordered list rather than sorting it using Collection API.
    -   Use named queries wisely, keep it at a single place for easy debugging. Use them for commonly used queries only. For entity specific query, you can keep them in the entity bean itself.
    -   For web applications, always try to use JNDI DataSource rather than configuring to create connection in hibernate.
    -   Avoid Many-to-Many relationships, it can be easily implemented using bidirectional One-to-Many and Many-to-One relationships.
    -   For collections, try to use Lists, maps and sets. Avoid array because you don’t get benefit of lazy loading.
    -   Do not treat exceptions as recoverable, roll back the Transaction and close the Session. If you do not do this, Hibernate cannot guarantee that in-memory state accurately represents the persistent state.
    -   Prefer DAO pattern for exposing the different methods that can be used with entity bean
    -   Prefer lazy fetching for associations

## What is Hibernate Validator Framework?
    Data validation is integral part of any application. You will find data validation at presentation layer with the use of Javascript, then at the server side code before processing it. Also data validation occurs before persisting it, to make sure it follows the correct format.
    
    Validation is a cross cutting task, so we should try to keep it apart from our business logic. That’s why JSR303 and JSR349 provides specification for validating a bean by using annotations. Hibernate Validator provides the reference implementation of both these bean validation specs.
    
## What types of connections (relationship) between Entity do you know (list eight types, or specify four types of connections, each of which can be further divided into two types)?

There are four types of connections

1. OneToOne (one-to-one connection, that is, one Entity object can be associated with no more than one object of another Entity),

2.  OneToMany (one-to-many connection, one Entity object can be associated with a whole collection of Entity)
3.  ManyToOne (many to one link, feedback for OneToMany),
4.  ManyToMany (many to many link) Each of which can be divided into two types:
5.  Bidirectional
6.  Unidirectional – a link to a link is set for all Entity, that is, in the case of OneToOne AB, Entity A has a link to Entity B, Entity B has a link to Entity A, Entity A is considered the owner of this link (this is important for cases of cascading data deletion , then deleting A will also delete B, but not vice versa). Undirectional- link to link is established only on one side, that is, in the case of OneToOne AB only Entity A will have link to Entity B, Entity B will not have link to A .

## What Is An Entitymanager?
Entity manager javax.persistence.EntityManager provides the operations from and to the database, e.g. find objects, persists them, remove objects from the database, etc. Entities which are managed by an EntityManager will automatically propagate these changes to the database (if this happens within a commit statement). These objects are known as persistent object. If the Entity Manager is closed (via close()) then the managed entities are in a detached state. These are known as the detached objects. If you want synchronize them again with the database, the a Entity Manager provides the merge() method. Once merged, the object(s) becomes perstent objects again.

The EntityManager is the API of the persistence context, and an EntityManager can be injected directly in to a DAO without requiring a JPA Template. The Spring Container is capable of acting as a JPA container and of injecting the EntityManager by honoring the @PersistenceContext (both as field-level and a method-level annotation).

Entity manager javax.persistence.EntityManager provides the operations from and to the database, e.g. find objects, persists them, remove objects from the database, etc. Entities which are managed by an EntityManager will automatically propagate these changes to the database (if this happens within a commit statement). These objects are known as persistent object. If the Entity Manager is closed (via close()) then the managed entities are in a detached state. These are known as the detached objects. If you want synchronize them again with the database, the a Entity Manager provides the merge() method. Once merged, the object(s) becomes perstent objects again.

The EntityManager is the API of the persistence context, and an EntityManager can be injected directly in to a DAO without requiring a JPA Template. The Spring Container is capable of acting as a JPA container and of injecting the EntityManager by honoring the @PersistenceContext (both as field-level and a method-level annotation).

## What is Mapped Superclass?

Mapped Superclass is a class from which Entity is inherited, it may contain JPA annotations, however such a class is not Entity, it does not have to fulfill all the requirements set for Entity (for example, it may not contain a primary key). Such a class cannot be used in EntityManager or Query operations. Such a class should be marked with the MappedSuperclass annotation or, respectively, described in the xml file.

## What are the three types of Inheritance Mapping Strategies described in JPA?

JPA describes three inheritance mapping strategies (Inheritance Mapping Strategies), that is, how JPA will work with the classes derived from the Entity:

1) one table for the entire inheritance hierarchy ( **a single table per class hierarchy** ) – all enity one table, to identify the type of entity is determined by a special column **“discriminator column”** . For example, if there is an entity Animals with the descendant classes Cats and Dogs, with such a strategy, all entities are recorded in the Animals table, but they have an additional column, animalType, in which the value “cat” or “dog” is written respectively. **Minus** is that in the general table, all fields unique for each of the descendant classes will be created, which will be empty for all other descendant classes. For example, in the table of animals there will be the speed of climbing a tree from cats and whether the dog can bring sneakers from dogs, which will always be null for a dog and cat, respectively.

2) unifying strategy ( **joined subclass strategy** ) – in this strategy, each enity class stores data in its own table, but only unique columns (not inherited from ancestor classes) and the primary key, and all inherited columns are written to ancestor class tables a relationship is established between these tables, for example, in the case of the Animals classes (see above), there will be three tables of animals, cats, dogs, and only the key and speed of climbing will be recorded in cats, in dogs – the key and whether the dog can bring a stick , and in animals all the rest of the data of cats and dogs are c links th to the appropriate table. **The downside** is the performance loss from joining tables (join) for any operations.

3) one table for each class ( **table per concrete class strategy** ) – everything is simple here every individual class of successor has its own table, i.e. for cats and dogs (see above), all data will be recorded simply in the tables cats and dogs as if they did not have a common superclass at all. **The downside** is poor support for polymorphism (polymorphic relationships) and the fact that selecting all the classes in the hierarchy will require a large number of separate sql queries or using a UNION query.

## What are the two types of fetch strategies in JPA do you know?

JPA describes two types of fetch strategies:

1) LAZY – these fields will be loaded only during the first access to this field,

2) EAGER – these fields will be loaded immediately.

## What is EntityManager and what are its main functions you can list?

EntityManager is an interface that describes an API for all basic operations on Enitity, data retrieval and other JPA entities. Essentially the main API for working with JPA. Basic operations:

1) For operations on Entity: persist (adding Entity under JPA control), merge (updating), remove (delete), refresh (updating data), detach (removing from management JPA), lock (blocking Enity from changes in other thread),

2) data Preparation: find (search and retrieval entity), createQuery, createNamedQuery, createNativeQuery , contains, createNamedStoredProcedureQuery, createStoredProcedureQuery

3) Preparation of other entities JPA: getTransaction, getEntityManagerFactory, getCriteriaBuilder, getMetamodel, getDelegate

4) Work with EntityGraph: createEntityGraph, getEntityGraph

4) General operations on EntityManager or all Entities: close, isOpen, getProperties, setProperty, clear.

## How does the operation persist on Entity objects of each of the four statuses?

1) If the status is Entity new, then it changes to managed and the object will be saved to the database when a transaction is committed or as a result of flush operations,

2) If the status is already managed, the operation is ignored, but dependent Entity can change the status to managed, if there are annotations of cascading changes,

3) If the status is removed, then it changes to managed,

4) If the status is detached, the exception will be thrown right away or at the commit stage of the transaction.

## How does the remove operation affect the Entity objects of each of the four statuses?

1) If the status is Entity new, the operation is ignored, however dependent Entity can change the status to removed, if they have cascading change annotations and they had the status managed,

2) If the status is managed, then the status changes to removed and the object is recorded in the database removed during commit commit (remove operations will also occur for all cascade-dependent objects),

3) If status is removed, then the operation is ignored,

4) If detached, exception is thrown right away or at the commit stage of a transaction.

##  How does the operation merge affect the Entity objects of each of the four statuses?

1) If the detached state, then either the data will be copied to the existing managed entity with the same primary key, or a new managed is created into which the data is copied,

1) If the Entity is new, then a new managed entity will be created into which the past data will be copied object,

2) If the status is managed, the operation is ignored, but the operation merge will work on the cascade-dependent Entity, if their status is not managed,

3) If the status is removed, exception will be thrown immediately or at the commit stage of the transaction.

## How does the refresh operation affect the Entity objects of each of the four statuses?

1) If the status is Entity managed, then as a result of the operation all changes from the database of this Entity will be restored, also a refresh of all cascade-dependent objects will occur,

2) If the status is new, removed or detached, exception will be thrown out.

##  How does the detach operation affect the Entity objects of each of the four statuses?

1) If the status is Entity managed or removed, then as a result of the operation, the status of Entity (and all cascade-dependent objects) will become detached.

2) If the status is new or detached, then the operation is ignored.

## What are callback methods in JPA for? To which entities do callback method annotations apply? List seven callback methods (or, equivalently, annotations of callback methods)

Callback methods are used to call on certain Entity events (that is, add processing, for example, deletion of Entity methods by JPA), can be added to the entity class, to the mapped superclass, or to the callback listener class specified by the EntityListeners annotation (see previous question). There are seven callback methods (and annotations with the same names):

1) PrePersist
2) PostPersist
3) PreRemove
4) PostRemove
5) PreUpdate
6) PostUpdate
7) PostLoad


## What are the six types of locks (lock) described in the JPA specification (or what values ​​does the enum LockModeType in JPA have)?

-   _PESSIMISTIC_READ_  – allows us to obtain a shared lock and prevent the data from being updated or deleted
-   _PESSIMISTIC_WRITE_  – allows us to obtain an exclusive lock and prevent the data from being read, updated or deleted
-   _PESSIMISTIC_FORCE_INCREMENT_  – works like  _PESSIMISTIC_WRITE_ and it additionally increments a version attribute of a versioned entity

## What are the two types of cache (cache) you know in JPA and what are they for?
JPA talks about two kinds of caches (cache):

1) first-level cache (first-level cache) —caches data from a single transaction;

2) second-level cache (second-level cache) —caches data for more than one transaction. The JPA provider can, but is not required to implement work with the second-level cache. This kind of cache can save access time and improve performance, but the downside is the ability to get outdated data.

## What are the options for setting the second-level cache (second-level cache) in JPA or what similarly describe what values ​​can the shared-cache-mode element take from persistence.xml?

JPA speaks of the five shared-cache-mode values ​​from persistence.xml, which defines how the second-level cache will be used:

1) ALL – all Entity can be cached in the second-level cache ,

2) NONE – caching is disabled for all Entity,

3) ENABLE_SELECTIVE — caching only works for those Entities that have the Cacheable (true) or their xml equivalent set, for all others, caching is disabled,

4) DISABLE_SELECTIVE — caching works for all Entity, except for those that have the Cacheable annotation (false) or its xml equivalent is

5) UNSPECIFIED – caching is not defined, each provider EPA uses its default value for caching,

## How can you change the fetch strategy settings of any Entity attributes for individual queries (query) or search methods (find), then if Enity has an attribute with fetchType = LAZY, but for a specific query you need to make it EAGER or vice versa?

For this, the EntityGraph API exists, it is used like this: using the NamedEntityGraph annotation for an Entity, it creates named EntityGraph objects that contain a list of attributes that need to change fetchType to EAGER, and then this name is specified in hits queries or the find method. As a result, the fetchType attribute of the Entity changes, but only for this request. There are two standard properties for specifying EntityGraph in hit:

1) javax.persistence.fetchgraph – all attributes listed in EntityGraph change fetchType to EAGER, all others to LAZY

2) javax.persistence.loadgraph – all attributes listed in EntityGraph change fetchType to EAGER, all others retain their fetchType (that is, if the attribute not specified in EntityGraph has fetchType was EAGER, then it will remain EAGER) With NamedSubgraph you can also change fetchType nested Entity objects.

## How is it possible in the code to work with the second-level cache (delete all or certain Entity from the cache, find out if this Entity has been cached, etc.)?

To work with the second level cache (second level cache) in JPA, the Cache interface is described which contains a large number of methods for managing the second level cache (second level cache), if supported by the JPA provider, of course. The object of this interface can be retrieved using the getCache method from EntityManagerFactory.

## What is meant by polymorphism (polymorphism) in JPQL queries (Java Persistence query language) and how to “turn it off”?

Unlike SQL, JPQL queries have automatic polymorphism, that is, each Entity request returns not only the objects of this Entity, but also objects of all its descendant classes, regardless of the inheritance strategy (for example, the select * from Animal query will return not only Animal objects, but also objects of Cat and Dog classes that are inherited from Animal). To eliminate this behavior, the TYPE function is used in the where condition (for example, select * from Animal a where TYPE (a) IN (Animal, Cat) will not return objects of the class Dog)


## How do you define a composite primary key in a JPA Entity class?

Composite primary key consists of more than one attribute, which corresponds to a set of single persistent properties or fields.

Composite primary keys must be defined in a primary key class.

Composite primary keys are annotated using the  _javax.persistence.EmbeddedId_  and  _javax.persistence.IdClass_  annotations.

### What are the different kinds of cascade operations applicable for relationships between JPA Entity classes?

Cascade operations defines the dependency of an entity object on the existence of another entity object, where there is a dependency between the two objects.

There are six different types of cascade operations.

1. DETACH - Is parent entity is detached from the persistence context, then the related entity will also be detached.

2. MERGE - If the parent entity is merged into the persistence context, then the related entity will also be merged.

3. PERSIST - If the parent entity is persisted into the persistence context, then the related entity will also be persisted.

4. REFRESH - If the parent entity is refreshed in the persistence context, then the related entity will also be refreshed.

5. REMOVE - If the parent entity is removed from the persistence context then the related entity will also be removed.

6. ALL - All the cascade operations will be applied to the parent entity's related entity.
```
@OneToMany(cascade=REMOVE)  
public  List getOrdersLines()  {  return ordersLines;  }
```

## What are JPA Embedded classes?

Embedded classes represent part of the state of an entity, but do not have a persistent identity of their own. Entity classes are annotated with the  _javax.persistence.Embeddable_  annotation.
```
@Entity  
public  class  Person  {  
  @Id  
  protected  long id  
  protected  String fname;  
  protected  String lname;  
  @Embedded  
  protected  Address address;  
  ...
```
## Explain Life Cycle Of A Jpa Entity.
Key states that an entity might be in:

1.  New / Transient: An object is instantiated but not yet associated with an Entity Manager and has no representation in the database.
2.  Managed / Persisted.
3.  Detached: Detached entity objects are objects in a special state in which they are not managed by any EntityManager but still represent objects in the database. Detached objects are often returned from a persistence tier to the web layer where they can be displayed to the end-user in some form. Changes can be made to a detached dobject, but these changes won't be persisted to the database until the entity is reassociated with a persistence context (the entity is merged back to an EntityManager to become managed again).
4.  Removed.

-   The merge method's major task is to transfer the state from an unmanaged entity (passed as the argument) to its managed counterpart within the persistence context.
-   merge deals with both new and detached entities. Merge causes either INSERT or UPDATE operation according to the sub-scenario (on the one hand it is more robust, on the other hand this robustness needn't be required.)
-   persist always causes INSERT SQL operation is executed (i.e. an exception may be thrown if the entity has already been inserted and thus the primary key violation happens.)

## What is N+1 problem in Hibernate, how will you identify and solve it?
N+1 problem is a performance issue in Object Relational Mapping that fires multiple select queries (N+1 to be exact, where N= number of records in table) in database for a single select query at application layer.
Example
First Get All User

`Select * from t_users;`

Then get roles for each user

`Select * from t_user_roles where userid = <userid>;`

#### JPA Solution:
If we are using Spring Data JPA, then we have two options to achieve this - using EntityGraph or using select query with fetch join.

```java
public interface UserRepository extends CrudRepository<User, Long> {

    List<User> findAllByRolesIn(List<Role> roles);             

    @Query("SELECT p FROM User p LEFT JOIN FETCH p.roles")  
    List<User> findWithoutNPlusOne();

    @EntityGraph(attributePaths = {"roles"})                      
    List<User> findAll();
}
```

- N+1 queries are issued at database level.
- using left join fetch, we resolve the N+1 problem
- using attributePaths, Spring Data JPA avoids N+1 problem

#### Hibernate Solution
if its pure Hibernate, then the following solution will work.

HQL Query

"from User u join fetch u.roles roles roles"

Hibernate Criteria API

```java
Criteria criteria = session.createCriteria(User.class);
criteria.setFetchMode("roles", FetchMode.EAGER);
```

under the hood, all these approaches work similar and they issue a similar database query with  `left join fetch`

## Explain Transaction Propagation
Propagation defines our business logic ‘s transaction boundary. Spring manages to start and pause a transaction according to our  _propagation_  setting.

Spring calls  _TransactionManager::getTransaction_  to get or create a transaction according to the propagation. It supports some of the propagations for all types of  _TransactionManager_, but there are a few of them that only supported by specific implementations of  _TransactionManager_.

#### REQUIRED_ Propagation
_EQUIRED_  is the default propagation. Spring checks if there is an active transaction, then it creates a new one if nothing existed. Otherwise, the business logic appends to the currently active transaction:


```java
@Transactional (propagation = Propagation.REQUIRED)

public void requiredExample(String user) {

// ...

}
```
#### SUPPORTS_ Propagation
For  _SUPPORTS_, Spring first checks if an active transaction exists. If a transaction exists, then the existing transaction will be used. If there isn't a transaction, it is executed non-transactional:
```
@Transactional (propagation = Propagation.SUPPORTS)
public void supportsExample(String user) {
	// ...
}
```
Let's see the transaction creation's pseudo-code for  _SUPPORTS_:
```java
if (isExistingTransaction()) {
	if (isValidateExistingTransaction()) {
		validateExisitingAndThrowExceptionIfNotValid();
	}
	return existing;
}
return emptyTransaction;
```

#### MANDATORY_ Propagation
When the propagation is  _MANDATORY_, if there is an active transaction, then it will be used. If there isn't an active transaction, then Spring throws an exception:

```java
@Transactional (propagation = Propagation.MANDATORY) 
public void mandatoryExample(String user) {
	// ... 
}
```
And let's again see the pseudo-code:
```java
if (isExistingTransaction()) {
	if (isValidateExistingTransaction()) {
		validateExisitingAndThrowExceptionIfNotValid();
	}
	return existing;
}
throw IllegalTransactionStateException;
```

#### NEVER_ Propagation
For transactional logic with  _NEVER_  propagation, Spring throws an exception if there's an active transaction:
```java
@Transactional(propagation = Propagation.NEVER)
public void neverExample(String user) {
	// ...
}
```
Let's see the pseudo-code of how transaction creation works for  _NEVER_  propagation:
```java
if (isExistingTransaction()) {
	throw IllegalTransactionStateException;
}
return emptyTransaction;
```
#### NOT_SUPPORTED
Spring at first suspends the current transaction if it exists, then the business logic is executed without a transaction.

```java
@Transactional(propagation = Propagation.NOT_SUPPORTED)
public void notSupportedExample(String user) {
	// ...
}
```

The  _JTATransactionManager_  supports real transaction suspension out-of-the-box. Others simulate the suspension by holding a reference to the existing one and then clearing it from the thread context

#### REQUIRES_NEW_ Propagation
When the propagation is  _REQUIRES_NEW_, Spring suspends the current transaction if it exists and then creates a new one:
```java
@Transactional(propagation = Propagation.REQUIRES_NEW)
public void requiresNewExample(String user) {
	// ...
}
```
Similar to  _NOT_SUPPORTED_, we need the  _JTATransactionManager_  for actual transaction suspension.

And the pseudo-code looks like so:
```java
if (isExistingTransaction()) {
	suspend(existing);
	try {
		return createNewTransaction();
	} catch (exception) {
		resumeAfterBeginException();
		throw` `exception;`
	}
}
return createNewTransaction();
```

#### NESTED_ Propagation
For  _NESTED_  propagation, Spring checks if a transaction exists, then if yes, it marks a savepoint. This means if our business logic execution throws an exception, then transaction rollbacks to this savepoint. If there's no active transaction, it works like _REQUIRED_.

_DataSourceTransactionManager_  supports this propagation out-of-the-box. Also, some implementations of  _JTATransactionManager_  may support this.

_JpaTransactionManager_ supports _NESTED_  only for JDBC connections. However, if we set  _nestedTransactionAllowed_  flag to  _true_, it also works for JDBC access code in JPA transactions if our JDBC driver supports savepoints.
Finally, let's set the  _propagation_  to  _NESTED_:
```java
@Transactional (propagation = Propagation.NESTED)
public void nestedExample(String user) {
	// ...
}
```

## How to fetch stream of records from a very big database table?

## How to write testcase for Hibernate/Spring Data JPA?

## Is EntityManagerFactory and EntityManager thread-safe?

## How to persist million records into database using Spring Data JPA in an efficient manner?



