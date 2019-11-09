
# RabbitMQ


### Message flow in RabbitMQ

1.  The producer publishes a message to an exchange. When creating an exchange, the type must be specified. This topic will be covered later on.
2.  The exchange receives the message and is now responsible for routing the message. The exchange takes different message attributes into account, such as the routing key, depending on the exchange type.
3.  Bindings must be created from the exchange to queues. In this case, there are two bindings to two different queues from the exchange. The exchange routes the message into the queues depending on message attributes.
4.  The messages stay in the queue until they are handled by a consumer
5.  The consumer handles the message.

![RabbitMQ Exchanges, Bindings and Routing Keys](https://www.cloudamqp.com/img/blog/exchanges-bidings-routing-keys.png)


![RabbitMQ beginners tutorial](https://www.cloudamqp.com/img/blog/rabbitmq-beginners-updated.png)

### EXCHANGES

Messages are not published directly to a queue; instead, the producer sends messages to an exchange. An exchange is responsible for routing the messages to different queues with the help of bindings and routing keys. A binding is a link between a queue and an exchange.

#### TYPES OF EXCHANGES

-   **Direct:**  The message is routed to the queues whose binding key exactly matches the routing key of the message. For example, if the queue is bound to the exchange with the binding key  _pdfprocess, a message published to_  the exchange with a routing key  _pdfprocess is routed to that queue._
-   **Fanout:**  A fanout exchange routes messages to all of the queues bound to it.
-   **Topic:**  The topic exchange does a wildcard match between the routing key and the routing pattern specified in the binding.
-   **Headers:**  Headers exchanges use the message header attributes for routing.

### RABBITMQ AND SERVER CONCEPTS

-   **Producer:**  Application that sends the messages.
-   **Consumer:**  Application that receives the messages.
-   **Queue:**  Buffer that stores messages.
-   **Message:**  Information that is sent from the producer to a consumer through RabbitMQ.
-   **Connection:**  A TCP connection between your application and the RabbitMQ broker.
-   **Channel:**  A virtual connection inside a connection. When publishing or consuming messages from a queue - it's all done over a channel.
-   **Exchange:**  Receives messages from producers and pushes them to queues depending on rules defined by the exchange type. To receive messages, a queue needs to be bound to at least one exchange.
-   **Binding:**  A binding is a link between a queue and an exchange.
-   **Routing key:**  A key that the exchange looks at to decide how to route the message to queues. Think of the routing key like an  _address for the message._
-   **AMQP:**  Advanced Message Queuing Protocol is the protocol used by RabbitMQ for messaging.
-   **Users:**  It is possible to connect to RabbitMQ with a given username and password. Every user can be assigned permissions such as rights to read, write and configure privileges within the instance. Users can also be assigned permissions for specific virtual hosts.
-   **Vhost, virtual host:**  Provides a way to segregate applications using the same RabbitMQ instance. Different users can have different permissions to different vhost and queues and exchanges can be created, so they only exist in one vhost.

### THE MANAGEMENT INTERFACE - MANAGEMENT AND MONITORING
RabbitMQ provides a web UI for the management and monitoring of your RabbitMQ server.

From the management interface, it is possible to handle, create, delete and list queues. It is also possible to monitor queue length, check message rate, or change and add users permissions and much more.

