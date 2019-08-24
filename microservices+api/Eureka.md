**Eureka**
---------


**Eureka** is a REST (Representational State Transfer) based service that is primarily used in the AWS cloud for locating services for the purpose of load balancing and failover of middle-tier servers. 
It allows services to find and communicate with each other without hard coding hostname and port. The only **‘fixed point’** in such an architecture consists of a service registry with which each service has to register.
A **drawback** is that all clients must implement a certain logic to interact with this fixed point. This assumes an additional network round trip before the actual request.
In AWS cloud, because of its inherent nature, servers come and go. Unlike the traditional load balancers which work with servers with well known IP addresses and host names, in AWS, load balancing requires much more sophistication in registering and de-registering servers with load balancer **on the fly**.

**The setups involve the following**

- **Eureka Server**: A service registry is a phone book for your microservices. Each service registers itself with the service registry and tells the registry where it lives (host, port, node name) and perhaps other service-specific metadata - things that other services can use to make informed decisions about it. 

- **Eureka Client**:  A client retrieves a list of all connected peers of a service registry and makes all further requests to any other services through a load-balancing algorithm. Your architecture which is using Eureka will typically have two applications
1. **Application Client** which uses Eureka Client to make requests to the Application Service.
2. **Application Service** which receives requests from Application Client and sends a response back.
	
**Configuration**:
- **Eureka Server**:

1. Dependency - spring-cloud-starter-eureka-server

2. Add @EnableEurekaServer to @SpringBootApplication class.

3. Add following properties.

```
eureka.client.registerWithEureka=false
eureka.client.fetchRegistry=false
```
We are telling the built-in Eureka Client not to register with ‘itself’, because our application should be acting as a server.

4. start the server and check Eureka dashboard at default host:port like http://localhost:8761

**Eureka client- Application Service**:

1. Dependency - spring-cloud-starter-eureka

2. Add @EnableEurekaClient to @SpringBootApplication class.

3. Register service at Eureka server.

```
server.port=0
spring.application.name=spring-cloud-eureka-client
eureka.client.serviceUrl.defaultZone: ${EUREKA_URI:http://localhost:8761/eureka}
```
Note that all the instances/nodes of this application server should have same spring.application.name but different server.port.


4. Start Eureka server and this application service. Observe the serve getting registered with spring.application.name value.

**Eureka client- Application Client**:

1. Dependency - spring-cloud-starter-eureka

2. Add @EnableEurekaClient to @SpringBootApplication class.

3. Register service at Eureka server.

```
server.port=0
spring.application.name=spring-cloud-eureka-client
eureka.client.serviceUrl.defaultZone: ${EUREKA_URI:http://localhost:8761/eureka}
```
4. Autowire EurekaClient and get instance info 

```java
Application application = eurekaClient.getApplication("spring-cloud-eureka-client");
InstanceInfo instanceInfo = application.getInstances().get(0);
String hostname = instanceInfo.getHostName();
int port = instanceInfo.getPort();
```
5. Call the service based on this client details.

6. Other simple alternative is to use Feign Client

Steps to configure Feign client

1. Add dependency spring-cloud-starter-feign  

2. Add @EnableFeignClients along with @EnableEurekaClient to @SpringBootApplication class.

3. Create the client. It is similar to Spring data interfaces. Call the client by injecting client.
```java
@FeignClient("spring-cloud-eureka-client")
public interface GreetingClient {
	@RequestMapping("/greeting")
	String greeting();
}
```

**Eureka deployed at Netflix**:
There is one eureka cluster per region which knows only about instances in its region. There is at the least one eureka server per zone to handle zone failures.

Services register with Eureka and then send heartbeats to renew their leases every 30 seconds. If the client cannot renew the lease for a few times, it is taken out of the server registry in about 90 seconds. The registration information and the renewals are replicated to all the eureka nodes in the cluster. The clients from any zone can look up the registry information (happens every 30 seconds) to locate their services (which could be in any zone) and make remote calls.
