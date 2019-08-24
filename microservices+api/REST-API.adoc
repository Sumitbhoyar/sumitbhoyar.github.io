**REST** stands for REpresentational State Transfer. REST is a web standards based architecture and uses HTTP Protocol for data communication. It revolves around resources where every component is a resource and a resource is accessed by a common interface using HTTP standard methods. 

Web services based on REST Architecture are known as **RESTful Web Services**.  

REpresentational State Transfer indicates transfer of Resources across network.


**What does it mean to be RESTful?**

REST defined 6 constraints for services:

1. There are clients and servers, separated by API boundaries over a network. Clients take care of presentation, servers take care of logic and storage.

2. Communication is stateless, every request contains all the information required to service that request.

3. Messages are cacheable by the server, client, or any proxy in between, or when not appropriate, mark themselves as not cacheable.

4. A client cannot tell whether it is connected directly to the source of the service, there can be any number of layers in between, facilitating load balancing, caching, and more.

5. Additional code for presentation is provided to the client on demand.

6. Data and functionality are accessed through a uniform interface.


**The Richardson Maturity Model**

The Richardson Maturity Model is a way to grade your API according to the constraints of REST. The better your API adheres to these constraints, the higher its score is. The Richardson Maturity Model knows 4 levels (0-3), where level 3 designates a truly RESTful API.

Richardson used three factors to decide the maturity of a service i.e. URI, HTTP Methods and HATEOAS (Hypermedia). The more a service employs these technologies – more mature it shall be considered.

- Level Zero

Level zero of maturity do not make use of any of URI, HTTP Methods and HATEOAS capabilities.

These services have a single URI, and use a single HTTP method (typically POST).

- Level One

Level one of maturity makes use of URIs out of URI, HTTP Methods and HATEOAS.

These services employ many URIs but only a single HTTP verb – generally HTTP POST. They give each individual resource in their universe a URI. **Every resource is separately identified by a unique URI – and that make them better than level zero**.

Level 1 tackles the question of handling complexity by using divide and conquer, breaking a large service endpoint down into multiple resources.

- Level Two

Level two of maturity makes use of URIs and HTTP out of URI, HTTP Methods and HATEOAS.

Level two services host numerous URI-addressable resources. Such services support several of the HTTP verbs on each exposed resource – Create, Read, Update and Delete (CRUD) services. Here the state of resources, typically representing business entities, can be manipulated over the network.

Level 2 introduces a standard set of verbs so that we handle similar situations in the same way, removing unnecessary variation.

- Level Three

Level three of maturity makes use of all three i.e. URIs and HTTP and HATEOAS.

This is the most mature level of Richardson’s model which encourages easy discoverability and makes it easy for the responses to be self-explanatory by using HATEOAS.

Level 3 introduces discoverability, providing a way of making a protocol more self-documenting.

**Few REST APIbest practices**

URI should follow **hierarchical** structure: ```http://api.soccer.restapi.org/leagues/{leagueId}/teams/{teamId}/players/{playerId}```

**Pagination url**: ```GET /users?pageSize=25&pageStartIndex=50```

**Record filtering**: ```GET /users?role=admin```

**Sort**: ```?sort=created,modified ```

**Response codes:**

- GET: 200 + Body

- POST: 200 + Body OR 201 Created + Body OR 204 No Content

- PUT: 200 + Body OR 201 Created + Body OR 204 No Content

- DELETE: 200 + Body OR 204 No Content OR 202 Accepted(Asynchronous)

**Hypermedia** is the engine of application state.

Hypermedia are links for other API

Helps to self describe API

Hypermedia == HATEOAS -  Hypermedia As The Engine Of Application State

```javascript
{  
  "links": [{
    "href": "https://api.paypal.com/v1/payments/sale/36C38912MN9658832",
    "rel": "self",
    "method": "GET"
  }, {
    "href": "https://api.paypal.com/v1/payments/sale/36C38912MN9658832/refund",
    "rel": "refund",
    "method": "POST"
  }, {
    "href": "https://api.paypal.com/v1/payments/payment/PAY-5YK922393D847794YKER7MUI",
    "rel": "parent_payment",
    "method": "GET"
  }]
}
```

An **ETag** (entity tag) is an HTTP response header returned by an HTTP/1.1 compliant web
server used to determine change in content at a given URL.
ETags represents a version number of entity. 

ETags are used for two things – caching and conditional requests.

GET Flow: Client request a resource. Server responds entity with ETag="SomeId". Client will send another request with If-None-Match="SomeId"
If the Resource is not modified yet then server just return 302, else it returns the entity with new ETag.

PUT flow: ETag matches then it updates else it return 412- Precondition fails indicating to load the resource again for update.

**Partial Items:** It allows to load only part of te resource.

It is useful to save the bandwidth. 

api/games/123/fields=id,name,url

Partial items works also for updating resource too, called patch.

**Versioning options**

- **URI path** :  ```api/v2/user```

- **URI Parameter**: ```api/user?v=1.5```

- **Content Negotiation**: ```ContentType:application/api.1.param+json```

- **RequestHeader**: ```x-ms-version: 2011-08-10```


**HTTP Response codes**

- 1xx: Informational Communicates transfer protocol-level information.

- 2xx: Success Indicates that the client’s request was accepted successfully.

- 3xx: Redirection Indicates that the client must take some additional action in order to complete their request.

- 4xx: Client Error This category of error status codes points the finger at clients.

- 5xx: Server Error The server takes responsibility for these error status codes.


**HTTP response success code**

- 200 OK: Indicates a nonspecific success

- 201 Created: Sent primarily by collections and stores but sometimes also by controllers, to
indicate that a new resource has been created

- 202 Accepted: Sent by controllers to indicate the start of an asynchronous action

- 204 No Content: Indicates that the body has been intentionally left blank

- 301 Moved Permanently: Indicates that a new permanent URI has been assigned to the client’s requested
resource

- 303 See Other: Sent by controllers to return results that it considers optional

- 304 Not Modified: Sent to preserve bandwidth (with conditional GET)

- 307 Temporary Redirect: Indicates that a temporary URI has been assigned to the client’s requested
resource

**HTTP response error code**


- 400 Bad Request Indicates a nonspecific client error

- 401 Unauthorized Sent when the client either provided invalid credentials or forgot to send them

- 402 Forbidden Sent to deny access to a protected resource

- 404 Not Found Sent when the client tried to interact with a URI that the REST API could not
map to a resource

- 405 Method Not Allowed Sent when the client tried to interact using an unsupported HTTP method

- 406 Not Acceptable Sent when the client tried to request data in an unsupported media type format

- 409 Conflict Indicates that the client attempted to violate resource state

- 412 Precondition Failed Tells the client that one of its preconditions was not met

- 415 Unsupported Media Type Sent when the client submitted data in an unsupported media type format

- 500 Internal Server Error Tells the client that the API is having problems of its own

**The three basic principles of API First are:**

- The API comes before the user interface. Before you develop your web application, mobile, IoT, etc, you'll need to define your APIs, and then work on the channels that will use them.
- The API comes before its implementation. By using tools such as Swagger to define and describe interfaces, you are generating discussions with the customer, user story and, mocking the APIs, also a user interface.
- The API must be described or self-descriptive. API documentation is an indispensable requirement for making it usable by humans.

