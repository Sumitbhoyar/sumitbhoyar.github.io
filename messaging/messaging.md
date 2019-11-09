

# JMS

-   JMS is the acronym for Java Messaging System.
-   JMS is part of Java EE.
-   JMS API is the implementation to handle the producer-consumer problem.
-   JMS API allows us to create, send, receive, and read messages.
-   Some o the benefits of using JMS are – loosely coupled application, reliability, and asynchronous communication.

## What is Message?

The message is a piece of information. It can be a text, XML document, JSON data or an Entity (Java Object) etc. The message is very useful data to communicate between different systems.

## What is Messaging?

Messaging means exchanging information between different components in the same system or different systems. It can happen in either a synchronous manner or an asynchronous manner.

## What is JMS?

JMS stands for Java Message Service. JMS API is a Java API which contains a common set of interfaces to implement enterprise based messaging systems. JMS API is used to implement Messaging systems in Java-based applications only, it does not support other languages.

JMS API is used to create, send, receive and read messages or exchange messages between different systems. Once we develop a Java Messaging System with JMS API, then we can deploy the same application in any JMS Provider software.

#### JMS Architecture
```
Java Application
   |
JMS  API
   |
JMS  Provider (JBoss, WebLogic, Rabbit MQ)
```
## JMS Components

A typical JMS system contains the following components:

1.  **JMS Client**: Java program used to send (or produce or publish) or receive (or consume or subscribe) messages.

-   **JMS Sender**: JMS Client which is used to send messages to the destination system. JMS sender is also known as JMS Producer or JMS Publisher.
-   **JMS Receiver**: JMS Client which is used to receive messages from Source system. JMS Receiver is also known as JMS Consumer or JMS Subscriber.

2.  **JMS Provider**: JMS API is a set of common interfaces, which does not contain any implementation. JMS Provider is a third-party system who is responsible to implement the JMS API to provide messaging features to the clients.
    
    JMS Provider is also known as MOM (Message Oriented Middleware) software or Message Broker or JMS Server or Messaging Server. JMS Provider also provides some UI components to administrate and control this MOM software.
    
3.  **JMS Administered Objects**: JMS Objects which are preconfigured by an administrator for the use of JMS clients. They are ConnectionFactory and Destination Objects.

-   **ConnectionFactory**: ConnectionFactory object is used to create a connection between Java Application and JMS Provider. It is used by Application to communicate with JMS Provider.
-   **Destination**: Destinations are also JMS Objects used by a JMS Client to specify the destination of messages it is sending and the source of messages it receives. There are two types of Destinations: Queue and Topic.

4.  **JMS Message**: an object that contains the data being transferred between JMS clients.

### MessageBroker
A message broker acts as a middleman for various services (e.g. a web application, as in this example). They can be used to reduce loads and delivery times of web application servers by delegating tasks that would normally take up a lot of time or resources to a third party that has no other job.
![RabbitMQ workflow tutorial](https://www.cloudamqp.com/img/blog/workflow-rabbitmq.png)

### Messaging Domains

Most messaging products supported either the point-to-point or the publish/subscribe approach to messaging. 

#### Point-to-Point Messaging Domain

A  **point-to-point**  (PTP) product or application is built on the concept of message  **queues**, senders, and receivers. Each message is addressed to a specific queue, and receiving clients extract messages from the queues established to hold their messages. Queues retain all messages sent to them until the messages are consumed or expire.

PTP messaging has the following characteristics:

-   Each message has only one consumer.
    
-   A sender and a receiver of a message have no timing dependencies. The receiver can fetch the message whether or not it was running when the client sent the message.
    
-   The receiver acknowledges the successful processing of a message.
    


![Diagram of point-to-point messaging, showing Client 1 sending a message to a queue, and Client 2 consuming and acknowledging the message](https://docs.oracle.com/javaee/6/tutorial/doc/figures/jms-pointToPoint.gif)

Use PTP messaging when every message you send must be processed successfully by one consumer.

#### Publish/Subscribe Messaging Domain

In a  **publish/subscribe**  (pub/sub) product or application, clients address messages to a  **topic**, which functions somewhat like a bulletin board. Publishers and subscribers are generally anonymous and can dynamically publish or subscribe to the content hierarchy. The system takes care of distributing the messages arriving from a topic’s multiple publishers to its multiple subscribers. Topics retain messages only as long as it takes to distribute them to current subscribers.

Pub/sub messaging has the following characteristics.

-   Each message can have multiple consumers.
    
-   Publishers and subscribers have a timing dependency. A client that subscribes to a topic can consume only messages published after the client has created a subscription, and the subscriber must continue to be active in order for it to consume messages.
    

The JMS API relaxes this timing dependency to some extent by allowing subscribers to create  **durable subscriptions**, which receive messages sent while the subscribers are not active. Durable subscriptions provide the flexibility and reliability of queues but still allow clients to send messages to many recipients.

Use pub/sub messaging when each message can be processed by any number of consumers (or none). 
![Diagram of pub/sub messaging, showing Client 1 publishing a message to a topic, and the message being delivered to two subscribers to the topic](https://docs.oracle.com/javaee/6/tutorial/doc/figures/jms-publishSubscribe.gif)

The JMS API Programming Model

![Diagram of the JMS API programming model: connection factory, connection, session, message producer, message consumer, messages, and destinations](https://docs.oracle.com/javaee/6/tutorial/doc/figures/jms-programmingModel.gif)	

### Creating Robust JMS Applications
##### Controlling Message Acknowledgment:
You can specify various levels of control over message acknowledgment.
Until a JMS message has been acknowledged, it is not considered to be successfully consumed. The successful consumption of a message ordinarily takes place in three stages.

1.  The client receives the message.
    
2.  The client processes the message.
    
3.  The message is acknowledged. Acknowledgment is initiated either by the JMS provider or by the client, depending on the session acknowledgment mode.
##### Specifying Message Persistence
You can specify that messages are persistent, meaning they must not be lost in the event of a provider failure.
The JMS API supports two delivery modes specifying whether messages are lost if the JMS provider fails. These delivery modes are fields of the  DeliveryMode  interface.

-   The  PERSISTENT  delivery mode, the default, instructs the JMS provider to take extra care to ensure that a message is not lost in transit in case of a JMS provider failure. A message sent with this delivery mode is logged to stable storage when it is sent.
    
-   The  NON_PERSISTENT  delivery mode does not require the JMS provider to store the message or otherwise guarantee that it is not lost if the provider fails.

If you do not specify a delivery mode, the default is PERSISTENT. Using the NON_PERSISTENT delivery mode may improve performance and reduce storage overhead, but you should use it only if your application can afford to miss messages.

##### Setting Message Priority Levels
You can set various priority levels for messages, which can affect the order in which the messages are delivered. A JMS provider tries to deliver higher-priority messages before lower-priority ones but does not have to deliver messages in exact order of priority.

##### Allowing Messages to Expire
By default, a message never expires. You can specify an expiration time for messages so they will not be delivered if they are obsolete. The destruction of obsolete messages conserves storage and computing resources.

##### Creating Temporary Destinations
You can create temporary destinations that last only for the duration of the connection in which they are created.






