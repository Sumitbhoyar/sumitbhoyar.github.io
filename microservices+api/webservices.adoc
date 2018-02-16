What are microservices?

Essentially, microservice architecture is a method of developing software applications as a suite of independently deployable, small, modular services in which each service runs a unique process and communicates through a well-defined, lightweight mechanism to serve a business goal.

Microservices is a way of breaking large software projects into loosely coupled modules, which communicate with each other through simple APIs.

**Advantages**

- Software built as microservices can be broken down into multiple component services, so that each of these services can be deployed and then redeployed independently without compromising the integrity of an application. That means that microservice architecture gives developers the freedom to independently develop and deploy services.
- Better fault isolation; if one microservice fails, the others will continue to work.
- Code for different services can be written in different languages.
- Easy integration and automatic deployment; using open-source continuous integration tools such as Jenkins, etc.
- The microservice architecture enables continuous delivery.
- Easy to understand since they represent a small piece of functionality, and easy to modify for developers, thus they can help a new team member become productive quickly.
- The code is organized around business capabilities.
- Scalability and reusability, as well as efficiency. Easy to scale and integrate with third-party services.
- Components can be spread across multiple servers or even multiple data centers.
- Work very well with containers, such as Docker.
- Complement cloud activities.
- Microservices simplify security monitoring because the various parts of an app are isolated. A security problem could happen in one section without affecting other areas of the project.
- Increase the autonomy of individual development teams within an organization, as ideas can be implemented and deployed without having to coordinate with a wider IT delivery function.

**Challanges**

- Developing distributed systems can be complex. By which I mean, because everything is now an independent service, you have to carefully handle requests traveling between your modules. There can be a scenario where one of the services may not be responding, forcing you to write extra code specifically to avoid disruption. Things can get more complicated when remote calls experience latency.
- Multiple databases and transaction management can be painful.
- Testing a microservices-based application can be cumbersome. Using the monolithic approach, we would just need to launch our WAR on an application server and ensure its connectivity with the underlying database. But now, each dependent service needs to be confirmed before you can start testing.
- Deploying microservices can be complex. They may need coordination among multiple services, which may not be as straightforward as deploying a WAR in a container.


