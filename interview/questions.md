
## What is the difference between JDK, JRE, and JVM?

- JVM
JVM is an acronym for Java Virtual Machine; it is an abstract machine which provides the runtime environment in which Java bytecode can be executed. It is a specification which specifies the working of Java Virtual Machine. Its implementation has been provided by Oracle and other companies. Its implementation is known as JRE.
JVMs are available for many hardware and software platforms (so JVM is platform dependent). It is a runtime instance which is created when we run the Java class. There are three notions of the JVM: specification, implementation, and instance.

- JRE
JRE stands for Java Runtime Environment. It is the implementation of JVM. The Java Runtime Environment is a set of software tools which are used for developing Java applications. It is used to provide the runtime environment. It is the implementation of JVM. It physically exists. It contains a set of libraries + other files that JVM uses at runtime.

- JDK
JDK is an acronym for Java Development Kit. It is a software development environment which is used to develop Java applications and applets. It physically exists. It contains JRE + development tools. JDK is an implementation of any one of the below given Java Platforms released by Oracle Corporation:

## What is classloader?

Classloader is a subsystem of JVM which is used to load class files. Whenever we run the java program, it is loaded first by the classloader. There are three built-in classloaders in Java.

1.  **Bootstrap ClassLoader**: This is the first classloader which is the superclass of Extension classloader. It loads the  _rt.jar_  file which contains all class files of Java Standard Edition like java.lang package classes, java.net package classes, java.util package classes, java.io package classes, java.sql package classes, etc.
2.  **Extension ClassLoader**: This is the child classloader of Bootstrap and parent classloader of System classloader. It loads the jar files located inside  _$JAVA_HOME/jre/lib/ext_  directory.
3.  **System/Application ClassLoader**: This is the child classloader of Extension classloader. It loads the class files from the classpath. By default, the classpath is set to the current directory. You can change the classpath using "-cp" or "-classpath" switch. It is also known as Application classloader.

## Difference between Checked and Unchecked Exceptions

1) Checked Exception
The classes which directly inherit Throwable class except RuntimeException and Error are known as checked exceptions e.g. IOException, SQLException etc. Checked exceptions are checked at compile-time.

2) Unchecked Exception
The classes which inherit RuntimeException are known as unchecked exceptions e.g. ArithmeticException, NullPointerException, ArrayIndexOutOfBoundsException etc. Unchecked exceptions are not checked at compile-time, but they are checked at runtime.

3) Error
Error is irrecoverable e.g. OutOfMemoryError, VirtualMachineError, AssertionError etc.

## What is the Atomic action in Concurrency in Java?

-   The Atomic action is the operation which can be performed in a single unit of a task without any interference of the other operations.
-   The Atomic action cannot be stopped in between the task. Once started it fill stop after the completion of the task only.
-   An increment operation such as a++ does not allow an atomic action.
-   All reads and writes operation for the primitive variable (except long and double) are the atomic operation.
-   All reads and writes operation for the volatile variable (including long and double) are the atomic operation.
-   The Atomic methods are available in java.util.Concurrent package.

## What do you understand by Callable and Future in Java?

**Java Callable interface:** In Java5 callable interface was provided by the package java.util.concurrent. It is similar to the Runnable interface but it can return a result, and it can throw an Exception. It also provides a run() method for execution of a thread. Java Callable can return any object as it uses Generic.

**Syntax:**

public interface Callable<V>

**Java Future interface:**  Java Future interface gives the result of a concurrent process. The Callable interface returns the object of java.util.concurrent.Future.

Java Future provides following methods for implementation.

-   **cancel(boolean mayInterruptIfRunning):**  It is used to cancel the execution of the assigned task.
-   **get():**  It waits for the time if execution not completed and then retrieved the result.
-   **isCancelled():**  It returns the Boolean value as it returns true if the task was canceled before the completion.
-   **isDone():**  It returns true if the job is completed successfully else returns false.


## Load Factor

The Load factor is a measure that decides when to  **increase**  the HashMap capacity to maintain the get() and put() operation complexity of  **O(1)**. The default load factor of HashMap is  **0.75f**  (75% of the map size).

**When the load factor ratio (m/n) reaches 0.75 at that time, hashmap increases its capacity.**

Where,
m is the number of entries in a hashmap.
n is the total size of hashmap.

**The initial capacity of hashmap is=16**  
**The default load factor of hashmap=0.75**  
**According to the formula as mentioned above: 16*0.75=12**

It represents that 12th  key-value pair of hashmap will keep its size to 16. As soon as 13th  element (key-value pair) will come into the Hashmap, it will increase its size from default  **24  = 16**  buckets to  **25  = 32**  buckets.

## What do you understand by fail-fast?

The Iterator in java which immediately throws ConcurrentmodificationException, if any structural modification occurs in, is called as a Fail-fast iterator. Fail-fats iterator does not require any extra space in memory.


# Hibernate/JPA

## What are the embeddable classes?

Embeddable classes represent the state of an entity but do not have a persistent identity of their own. The objects of such classes share the identity of the entity classes that owns it. An Entity may have single-valued or multivalued embeddable class attributes.

## What is an orphan removal in mappings?

If a target entity in one-to-one or one-to-many mapping is removed from the mapping, then remove operation can be cascaded to the target entity. Such target entities are known as orphans, and the orphanRemoval attribute can be used to specify that orphaned entities should be removed.

## What are the four lifecycle status of an Entity Instance’s Life Cycle you can list?

An Entity object has four lifecycle status: new, managed, detached, or removed. Their description

1) new – the object has been created but has not yet generated primary keys and has not yet been saved in the database,

2) managed – the object has been created, managed by JPA, has generated primary keys,

3) detached – the object has been created, but not managed (or no longer managed) JPA,

4) removed – the object is created, managed by JPA, but will be deleted after commit’a transaction.

## What are the different types of identifier generation?

Following are the types of id generation strategy required to specify with @GeneratedValue annotation: -

-   Automatic Id generation - In this case, the application doesn't care about the kind of id generation and hand over this task to the provider. If any value is not specified explicitly, the generation type defaults to auto.
-   Id generation using a table - The identifiers can also be generated using a database table.
-   Id generation using a database sequence - Databases support an internal mechanism for id generation called sequences. To customize the database sequence name, we can use the JPA @SequenceGenerator annotation.
-   Id generation using a database identity - In this approach, whenever a row is inserted into the table, a unique identifier is assigned to the identity column that can be used to generate the identifiers for the objects.


## What are the types of cascade supported by JPA?

Following is the list of cascade type: -

-   **PERSIST:**  In this cascade operation, if the parent entity is persisted then all its related entity will also be persisted.
-   **MERGE:**  In this cascade operation, if the parent entity is merged, then all its related entity will also be merged.
-   **DETACH:**  In this cascade operation, if the parent entity is detached, then all its related entity will also be detached.
-   **REFRESH:**  In this cascade operation, if the parent entity is refreshed, then all its related entity will also be refreshed.
-   **REMOVE:**  In this cascade operation, if the parent entity is removed, then all its related entity will also be removed.
-   **ALL**  In this case, all the above cascade operations can be applied to the entities related to the parent entity.

## Why does JPA have a @Transient annotation?  
Java's transient keyword is used to denote that a field is not to be serialized, whereas JPA's @Transient annotation is used to indicate that a field is not to be persisted in the database

## What is Mapped Superclass?

Mapped Superclass is a class from which Entity is inherited, it may contain JPA annotations, however such a class is not Entity, it does not have to fulfill all the requirements set for Entity (for example, it may not contain a primary key). Such a class cannot be used in EntityManager or Query operations. Such a class should be marked with the MappedSuperclass annotation or, respectively, described in the xml file.

## What are the three types of Inheritance Mapping Strategies described in JPA?

JPA describes three inheritance mapping strategies (Inheritance Mapping Strategies), that is, how JPA will work with the classes derived from the Entity:

1) one table for the entire inheritance hierarchy ( **a single table per class hierarchy** ) – all enity one table, to identify the type of entity is determined by a special column **“discriminator column”** . For example, if there is an entity Animals with the descendant classes Cats and Dogs, with such a strategy, all entities are recorded in the Animals table, but they have an additional column, animalType, in which the value “cat” or “dog” is written respectively. **Minus**is that in the general table, all fields unique for each of the descendant classes will be created, which will be empty for all other descendant classes. For example, in the table of animals there will be the speed of climbing a tree from cats and whether the dog can bring sneakers from dogs, which will always be null for a dog and cat, respectively.

2) unifying strategy ( **joined subclass strategy** ) – in this strategy, each enity class stores data in its own table, but only unique columns (not inherited from ancestor classes) and the primary key, and all inherited columns are written to ancestor class tables a relationship is established between these tables, for example, in the case of the Animals classes (see above), there will be three tables of animals, cats, dogs, and only the key and speed of climbing will be recorded in cats, in dogs – the key and whether the dog can bring a stick , and in animals all the rest of the data of cats and dogs are c links th to the appropriate table. **The downside** is the performance loss from joining tables (join) for any operations.

3) one table for each class ( **table per concrete class strategy** ) – everything is simple here every individual class of successor has its own table, i.e. for cats and dogs (see above), all data will be recorded simply in the tables cats and dogs as if they did not have a common superclass at all. **The downside** is poor support for polymorphism (polymorphic relationships) and the fact that selecting all the classes in the hierarchy will require a large number of separate sql queries or using a UNION query.

## What is EntityManager and what are its main functions you can list?

EntityManager is an interface that describes an API for all basic operations on Enitity, data retrieval and other JPA entities. Essentially the main API for working with JPA. Basic operations:

1) For operations on Entity: persist (adding Entity under JPA control), merge (updating), remove (delete), refresh (updating data), detach (removing from management JPA), lock (blocking Enity from changes in other thread),

2) data Preparation: find (search and retrieval entity), createQuery, createNamedQuery, createNativeQuery , contains, createNamedStoredProcedureQuery, createStoredProcedureQuery

3) Preparation of other entities JPA: getTransaction, getEntityManagerFactory, getCriteriaBuilder, getMetamodel, getDelegate

4) Work with EntityGraph: createEntityGraph, getEntityGraph

4) General operations on EntityManager or all Entities: close, isOpen, getProperties, setProperty, clear.

## What is the Access annotation for?

It defines the access type for an entity class, superclass, embeddable, or individual attributes, that is, how JPA will refer to entity attributes, like class fields (FIELD) or class properties (PROPERTY) that have getters (getter) and setters.

## What are the two types of cache (cache) you know in JPA and what are they for?

JPA talks about two kinds of caches (cache):

1) first-level cache (first-level cache) —caches data from a single transaction;

2) second-level cache (second-level cache) —caches data for more than one transaction. The JPA provider can, but is not required to implement work with the second-level cache. This kind of cache can save access time and improve performance, but the downside is the ability to get outdated data.

