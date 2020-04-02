# Scalability Design Principles

## Choose a horizontal scale over a vertical
You might find that the system is limited to scale horizontally sometimes. Yet, these limits regularly extend databases in the same direction. Besides, with a horizontal scale, you can just add another server rather than upgrade the existing one. It will save you some money.

## Choosing the correct tool with scalability in mind reduces a lot of overhead
Many developers fall prey to the idea of using one technology –– if they have used PHP from start, they will refuse to look beyond the local scope or rethink the existing tech stack.
This as a Golden Hammer analogy which represents an over-reliance on a familiar tool even if the tool isn’t suited for a particular task.

## Use multiple Databases (or SQL + NoSQL) to maintain data consistency and integrity

By using multiple databases, a web app can handle a number of users simultaneously while still providing ‘good’ performance. By using and locating databases geographically across the world, it provides the shortest access time. In short, **SQL+NoSQL : Excellent Performance + scalability**

## Avoid using Local Disks and Use Object storage API of cloud to make data storage manageable
When you come to a point when your data becomes hard to maintain/ manage or it is highly unstructured, using cloud native solutions should be your go-to approach.

## Make your web applications stateless unless there is a very good reason to have state or store sessions
Web applications should be stateless, meaning each request should be treated as an independent transaction.
Avoid storing sessions on your server at all cost as it might increase the further load on your server and induce code complexities.
By going stateless, you are simplifying the client/ server communication model of your application. Since the client can request anything from the server without having the need to know the state of the server, you are helping your application to scale out the server implementation since there is no need to change the pool of sessions constantly throughout the application servers.

## Use Asynchronous Communication wherever possible to avoid wastage of application resources
With asynchronous IO, you can handle thousands and thousands of request at the same time without the need to block requests and wait for the return value from the kernel by the user application. Here’s why some applications which use asynchronous (i.e Non-Blocking), are also built using single-threaded frameworks such as NodeJS.

## Use Queues to make your tasks atomic so that they can be retrieved easily when fails
Message queues like RabbitMQ provide you with enough buffer to cope with sudden traffic spikes to your application. In the example above, you will benefit from using Message queues in the following ways:

-   If the server fails, the queue can still be able to persist the message. Even if it fails, the message will not be added to the queue. The operation is atomic.
-   If the server worked again, it receives the pending message.
-   If the server gives a response to the call and the client fails, if the client didn’t acknowledge the response the message is persisted.
-   You have contention in place. It’s you who decide how many requests are handled by the server or worker.
-   You don’t expect an immediate synchronous response, but you can implement/simulate synchronous calls.

## Always have the ability to roll back your code in case of failed deploys
When your code push is unsuccessful, a rollback becomes necessary to restore the environment to a previously stable state.

## Load or performance Test Your Application Every Single Day
While Performance testing is used to check your application’s response time to the load. On the contrary, load testing deals with scalability metrics such as requests per second and concurrent users.

## Root out any Single point of failure (SPOF), but be prepared when failure strikes your application
When it comes to scaling web application, failures are inevitable. Therefore, it becomes extremely evident for us to either isolate the failure or to identify any single point of failure.
In the majority of cases, a Single point of failure might strike your application if your application has,

-   An unsecured network
-   Failure of particular resources (e.g server, network resources, database, caching system)
-   Lacking in built-in redundancies

Following things to prevent from SPOF,

-   Use multiple zones and regions for databases
-   Use multiple cloud providers
-   Web servers can be hosted in different regions
-   Use ‘Browsing only mode’ when don’t have control over the outage

## Automate Everything to Run Continuously
When it comes to scalability, automation is considered as one of the important parameters. We need to automate everything when the infrastructure gets bigger because it is hard to manage every instance. Understanding the importance of automation can help you to scale web apps.

Don’t deploy by hand or do anything you can convince a machine to do for you.

#### References
[https://www.simform.com/tips-building-scalable-web-applications/](https://www.simform.com/tips-building-scalable-web-applications/)







