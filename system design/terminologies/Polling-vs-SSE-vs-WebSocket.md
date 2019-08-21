# Polling vs SSE vs WebSocket

Sometimes we need information from our servers as soon as it’s available. Technologies that enable this “proactively” have been around for quite some time and are limited to two general approaches: client pull or server push.

A few ways to implement these:
- Long/short polling (client pull)
- WebSockets (server push)
- Server-Sent Events (server push)

#### Client pull

Polling is a technique by which the client asking the server for new data regularly. We can do polling in two ways: Short Polling and Long Polling. In simple terms, Short polling is an AJAX-based timer that calls at fixed delays whereas Long polling is based on Comet (i.e server will send data to the client when the server event happens with no delay). Both have pros and cons and suited based on the use case.

#### Server push — server is proactively pushing updates to the client (reverse of client pull)

- WebSockets : A WebSocket is nothing but a persistent connection between the client and the server. This is a communications protocol providing full-duplex communication channels over a single TCP connection.
- Server-Sent Events : SSE is a mechanism that allows the server to asynchronously push the data to the client once the client-server connection is established. The server can then decide to send data whenever a new “chunk” of data is available. It can be considered as a one-way publish-subscribe model.

**Benefits of SSE**
 
- Simpler implementation and Data efficiency
- It is automatically multiplexed over HTTP/2 out of the box
- Limits the number of connections for data on the client to one

#### Long Polling: pros and cons
**Pros**

- Long polling is implemented on the back of XMLHttpRequest, which is near-universally supported by devices so there’s usually little need to support further fallback layers. In cases where exceptions must be handled though, or where a server can be queried for new data but does not support long polling (let alone other more modern technology standards), basic polling can sometimes still be of limited use, and can be implemented using XMLHttpRequest, or via JSONP through simple HTML script tags.

**Cons**

- Long polling is a lot more intensive on the server.
- Reliable message ordering can be an issue with long polling because it is possible for multiple HTTP requests from the same client to be in flight simultaneously. For example, if a client has two browser tabs open consuming the same server resource, and the client-side application is persisting data to a local store such as localStorage or IndexedDb, there is no in-built guarantee that duplicate data won’t be written more than once.
- Depending on the server implementation, confirmation of message receipt by one client instance may also cause another client instance to never receive an expected message at all, as the server could mistakenly believe that the client has already received the data it is expecting.

#### WebSockets: pros and cons
**Pros**

- WebSockets keeps a unique connection open while eliminating latency problems that arise with Long Polling.
- WebSockets generally do not use XMLHttpRequest, and as such, headers are not sent every-time we need to get more information from the server. This, in turn, reduces the expensive data loads being sent to the server.

**Cons**

- WebSockets don’t automatically recover when connections are terminated – this is something you need to implement yourself, and is part of the reason why there are many client-side libraries in existence.
- Browsers older than 2011 aren’t able to support WebSocket connections - but this is increasingly less relevant.

#### How to choose among SSE, WebSocket and Polling?
After the long and exhaustive client and server implementations, it looks like SSE is the final answer to our problem for data delivery. There are some issues with it as well but it can be solved.
A few simple examples of applications that could make use of Server-Sent Events:
- A real-time chart of streaming stock prices
- Real-time news coverage of an important event (posting links, tweets, and images)
- A live Github / Twitter dashboard wall fed by Twitter’s streaming API
- A monitor for server statistics like uptime, health, and running processes.

- However, SSE is not just a viable alternative to the other methods for delivering fast updates. Each one dominates over others in a few specific scenarios like in our case where SSE proved to be an ideal solution. Consider a scenario like MMO (Massive Multiplayer Online) Games that need a huge amount of messages from both ends of the connection. In such a case, WebSockets dominates SSE.


## References:

- https://www.ably.io/blog/websockets-vs-long-polling/
- https://codeburst.io/polling-vs-sse-vs-websocket-how-to-choose-the-right-one-1859e4e13bd9
