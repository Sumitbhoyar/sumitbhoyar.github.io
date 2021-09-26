# Event-Driven Architecture

Event-driven architecture (EDA) is a software design pattern in which decoupled applications can asynchronously publish and subscribe to events via an event broker (modern messaging-oriented-middleware).

Event-driven architecture is a way of building enterprise IT systems that lets information flow between applications, microservices and connected devices in a real-time manner as events occur throughout your business, instead of periodically polling for updates.

The event-driven architecture pattern consists of two main topologies, the mediator and the broker.

## What is an Event?
An event is defined as a change of state of some key business system. For instance, somebody buys a product, someone else checks in for a flight or a bus is late arriving somewhere.

An example of an event might include:

-   Request to reset a password
-   A package arrived was delivered to its destination
-   A grocery warehouse updates its inventory
-   An unauthorized access attempt was denied

Each of these events is likely to trigger one or more actions or processes in response. One response might be simply to log the event for monitoring purposes. Others might be:

-   An email to reset the password is sent to the customer
-   The sales ticket is closed
-   An order for more lettuce (or whatever materials are running low) is placed
-   An account is locked and security personnel are notified

With event-driven architecture, when an event notification is sent, the system captures that something happened like a change in state has occurred and waits to send the reply to whoever requests it, whenever they request it. The application that received that message can either respond or wait to respond until the change in state has occurred that it is waiting for.

## Styles of Event Processing

Event processing is generally categorized into three nominal styles. These styles are not mutually exclusive, often appearing together in large, event-driven systems.

### Discrete event processing

The processing of discrete events; for example, the publishing of a post in a social media platform. Discrete event processing is characterized by the presence of events that are generally unrelated to one another and may be handled independently.

### Event stream processing

The processing of an unbounded stream of related events, where event records appear in some order and are processed with some knowledge of past events. A good example might be the syndication of changes to a business entity. A consumer may apply these changes in a producer-prescribed order, to save a copy of the entity in its local database. Processing these change records discretely might not cut it, as  _order matters_. Consumers also need to avoid race conditions, whereby multiple consumer instances might attempt to concurrently apply changes to the same record in a database, resulting in data inconsistencies due to out-of-order updates.

Popular event streaming platforms like Kafka rely on record keying and partitions to preserve the order of updates. Kafka also guarantees that all changes to an entity are processed by one consumer instance, avoiding concurrency races that would result if multiple consumers were to naively process events in parallel.

### Complex event processing

Complex event processing (CEP) derives or identifies complex event patterns from a series of simple events. An example of CEP might be monitoring a group of temperature and smoke sensors in a building to infer that a fire has broken out and to track its progress. Individual temperature changes might not be sufficient to raise an alert; however, the clustering of temperature spikes and the rate of change may provide more meaningful insights that could ultimately save lives.

This sort of processing is usually more involved, requiring the event processor to keep track of prior events and provide an efficient way of querying and aggregating them.

## Event model

An event driven architecture can use a pub/sub model or an event stream model.

-   **Pub/sub**: The messaging infrastructure keeps track of subscriptions. When an event is published, it sends the event to each subscriber. After an event is received, it cannot be replayed, and new subscribers do not see the event.
    
-   **Event streaming**: Events are written to a log. Events are strictly ordered (within a partition) and durable. Clients don't subscribe to the stream, instead a client can read from any part of the stream. The client is responsible for advancing its position in the stream. That means a client can join at any time, and can replay events.

## When to use this architecture

-   Multiple subsystems must process the same events.
-   Real-time processing with minimum time lag.
-   Complex event processing, such as pattern matching or aggregation over time windows.
-   High volume and high velocity of data, such as IoT.

## Benefits

-   Producers and consumers are decoupled.
-   No point-to-point integrations. It's easy to add new consumers to the system.
-   Consumers can respond to events immediately as they arrive.
-   Highly scalable and distributed.
-   Subsystems have independent views of the event stream.

Reference: https://medium.com/microservicegeeks/introduction-to-event-driven-architecture-e94ef442d824
