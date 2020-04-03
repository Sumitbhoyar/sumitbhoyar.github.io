# Capacity Planning

The process of determining what type of hardware and software configuration is required to meet application needs adequately is called capacity planning. Capacity planning is not an exact science. Every application is different and every user behavior is different.
Without a capacity plan, organizations are either grossly under-prepared or over-prepared. Capacity planning is the process of determining the production capacity needed by an organization to meet changing demands for its products. A discrepancy between the capacity of an organization and the demands of its customers results in inefficiency, either in under-utilized resources or unfulfilled customers.

The goal of capacity planning is to minimize this discrepancy. Capacity can be increased through introducing new techniques, equipment, and materials, increasing the number of workers or machines, increasing the number of shifts, or acquiring additional production facilities.

### Capacity planning can help in answering some of the following –

-   What is the maximum load level that the system can handle?
-   What would the average response time, throughput, and CPU utilization be for a particular workload?
-   How much resources (servers, CPUs, memory) would be required to meet the Service Level Agreements (SLAs)?
-   Which components of the system affect performance the most? Are they potential bottlenecks?

### Capacity term can be used in multiple contexts, but at high level, it can be understood as

-   Number of transactions/users that can be supported by available resources during peak time of the day.
-   CPU utilization, memory utilization, and transaction response time are of interest here.
-   When capacity numbers do not meet the expectations, there are two options:
    -   Optimize application architecture and code.
    -   Add more resources.
        -   Of course, infrastructure architecture needs to support this.


## Approaches to Capacity Planning

Various techniques and approaches are used by practitioners to do capacity planning. These vary in terms of efforts required/accuracy levels and also the phase in the development cycle, when the capacity planning is done.

#### Approach 1: Make an Educated Guess
Rely on intuition, expert opinions, past experience, ad hoc procedures and general rules of thumb.
-   PROS: Quick, easy and cheap.
-   CONS: Very inaccurate and risky

#### Approach 2: Generate Load and Measure Performance
-   Use load-testing tools that generate artificial workloads and measure performance.
-   PROS: Provides accurate and realistic data. Could help to identify bottlenecks and fine-tune system prior to production.
-   CONS: Extremely expensive and time-consuming. Assumes that the system is available for testing.

#### Approach 3: Build a Performance Model of the System
-   Build and analyze performance models which capture the performance and scalability characteristics of the system.
-   PROS: Often much cheaper and quicker than load-testing. Could be applied during early phases (arch/design).
-   CONS: Extremely complex. Accuracy depends on how representative models are.

## Capacity Planning Process

-   Determine service level requirements
    -   From a capacity planning perspective, a computer system processes workloads and delivers service to users.
    -   During the first step in the capacity planning process, these workloads must be defined and a definition of satisfactory service must be created.
    -   A workload is a logical classification of work performed on a computer system. If you consider all the work performed on your systems as pie, a workload can be thought of as some piece of that pie. Workloads can be classified by a wide variety of criteria.
    -   Who is doing the work (particular user or department).
    -   What type of work is being done (order entry, financial reporting).
    -   How the work is being done (online inquiries, batch database backups).
-   Determine the unit of work
    -   What "transaction" really means.
    -   Can vary from an OLTP application to a batch system.
    -   "Business Transaction" vs "Technical Transaction."
-   Establish service levels
    -   A service level agreement is an agreement between the service provider and service consumer that defines acceptable service.
    -   The service level agreement is often defined from the user’s perspective, typically in terms of response time or throughput.
    -   Using workloads often aids in the process of developing service level agreements, because workloads can be used to measure system performance in ways that make sense to clients/users.
    -   If you want to base your service level requirements on present actual service levels, then you may want to analyze your current capacity before setting your service levels.
-   Analyze current capacity. Note that these steps are generally done for an existing system during load testing phase. but similar steps can be done using APM data for a live system or using performance modeling for a system which is still in early phases of development life cycle.
    -   First, compare the measurements of any items referenced in service level agreements with their objectives. This provides the basic indication of whether the system has adequate capacity.
        
    -   Next, check the usage of the various resources of the system (CPU, memory, and I/O devices). This analysis identifies highly used resources that may prove problematic now or in the future.
        
    -   Look at the resource utilization for each workload. Ascertain which workloads are the major users of each resource. This helps narrow your attention to only the workloads that are making the greatest demands on system resources.
        
    -   Determine where each workload is spending its time by analyzing the components of response time, allowing you to determine which system resources are responsible for the greatest portion of the response time for each workload.
        
-   Plan for the future
    -   Determine future processing requirements
    -   Systems may be satisfying service levels now, but will they be able to do that while at the same time meeting future organizational needs?
    -   Future processing requirements can come from a variety of sources. Input from management may include:
        -   Expected growth in the business, Requirements for implementing new applications.
        -   Planned acquisitions, IT budget limitations.

## Capacity Planning Parameters
### Throughput and TPS

Generally throughput is deined as the number of messages processed over a given interval of time. Throughput is a measure of the number of actions per unit time, where time can be in seconds, minutes, hours, etc. TPS is the number of atomic actions, in this case ‘transactions’ per second. For a stateless server, this will be the major characteristic that affects server capacity.

Theoretically speaking, if a user performs 60 transactions in a minute, then the TPS should be 60/60 TPS = 1 TPS. Of course, since all concurrent users who are logged into a system might not necessarily be using that system at the given time, this might not be accurate. Additionally, think time of users and pace time comes into consideration as well. But eliminating the above, this can be considered an average of 1 TPS considering users uniformly accessing the system over 60 seconds; this of course means that we can also expect all users coming within a single second which means a 60 TPS max peak load.

### Work done per transaction

Each incoming 'transaction' to a server will have some level of operations it triggers. This would mean a number of CPU instructions would be triggered to process the said message. These instructions might include application processing as well as system operations like database access, external system access, etc. If the transaction is a simple ‘pass through’ that would mean relatively lesser processing requirements than a transaction that triggers a set of further operations. If a certain type of transaction triggers, for example, a series of complex XML-based transformations or processing operations, this would mean some level of processing power or memory requirements. A sequence diagram of the transaction would help determine the actual operations that are related to a transaction.

### Think time
From a web application perspective, users submit requests, which are then processed at the server side before returned to a user. The user then often waits on the response, and 'processes' it, before submitting again. This delay is the user think time that falls between requests, and can be taken into account when calculating optimum system load. For machine to machine communication, this think time parameter would be relatively lower. For capacity planning, the average think time is useful in arriving at an accurate throughput number.

### Active users and concurrency

A system would have a total number of users - this might not affect the server capacity directly, but is an important metric in database sizing for instance. Of these total set of users, a subset of them would be active users - users who use the system at a given time. Usually the active users login to a system, perform some operations and logout; or they just let the system be, which in turn will kick the user out once the session expires (often in 30 minutes or so). Active users might have a session created for each of them, but concepts like garbage collection, etc. would come into effect as well.

![users-in-capacity-planning-figure1.png](https://b.content.wso2.com/sites/all/white-paper-landing/images/users-in-capacity-planning-figure1.png)

Figure: Users in Capacity Planning

Concurrent active users are the number of distinct users concurrently accessing the system at any given time at the same time. As shown in the example in Figure 1, concurrent users are a subset of active users who are using the system at a given time. If 200 active users are logged into the system, and have a 10 second think time, then that amounts to roughly 20 actual concurrent users hitting the system. In capacity planning, this has several meanings and implications. In an application server with a stateful application that handles sessions, the number of concurrent users will play a bigger role than in an ESB, which handles stateless access, for instance. For systems designed in such a way, each concurrent user consumes some level of memory that needs to be taken into account.

Conventionally, a system’s throughput increases with the number of concurrent users until it reaches peak capacity; from then onwards the system would experience performance degradation. Thus, it is important to calculate the maximum concurrency a system can handle.

### Message size

The size of the message passed across the 'wire' is also an important factor in determining the required capacity of a system. Larger messages mean more processing power requirement, more memory requirements, or both. As a basis for capacity planning, the following message sizes can be considered.

| Message size range |  Message size category |
|--|--|
| Less than 50 KB | Small |
| Between 50 KB and 1 MB | Moderate|
| Between 1 MB and 5 MB | Large|
| Larger than 5 MB | Extra Large|

### Latency
Latency is the additional time spent due to the introduction of a system. Non-functional requirements (NFRs) of a system would usually indicate a desired response time of a transaction that a system must then strive to meet. Considering the example in Figure 1, if a single transaction performs a number of database calls, or a set of synchronous web service calls, the calling transaction must 'wait' for a response. This would then add to the overall response time of that said transaction or service call.

![Figure 4: Server Performance - Latency](https://b.content.wso2.com/sites/all/white-paper-landing/images/users-in-capacity-planning-figure3.png)

Figure : Server Performance - Latency

Latency is usually calculated via a step-by-step process – irst test response times without the newer systems in place, and then test response times with the addition of the newer systems. The latency vs functionality due to the newer systems is then a tradeoff decision. Techniques like caching can be used to improve latency times.

Latency is usually from the client and needs to account for network/bandwith overheads as well.

### Forecasting Capacity Requirements

With the above concepts  in place, the business needs to decide what the forecasting period should be as well. Are you just focusing on year 1? Will the capacity requirements double in year 2, and if so would there be a significant downtime at the end of year one to accommodate this? A table, such as the one given in Figure 6, would be useful for forecasting, and can be based on past trends and future business forecasting.

| Parameter | Year 1 | Year 2 | Year 3 | Year 4 |
|--|--|--|--|--|
| TPS | 50 | 500 | 1000  | 2500 | 
| Concurrent Users | 20| 100| 500 | 1000 |

## Capacity Calculation

The above are just a few factors that can be used for capacity planning of a system and the importance of these factors vary based on the type of environment.

Different architects use different processes to calculate capacity. A sample process is illustrated in Figure; whatever the process, it needs to be coupled with your existing solution architecture process.
 ![Capacity Planning as Part of Deployment Architecture Process](E:%5CSumit%5Cwork%5Cworkspaces%5Cnotes%5Csystem-design%5Cusers-in-capacity-planning.png)

As per the process shown in Figure 8, it is important to have an accurate business architecture that can be converted into a high-level solution architecture. Based on this, the team can start gathering capacity data that would be used to ill a capacity planning matrix or model.

With these factors in place, we also need a set of benchmark performance numbers to calculate server capacity. For instance, if we know that an enterprise service bus in certain environmental conditions on certain type of capacity performs at 3000 TPS, then we can assume that a server of similar capacity and operations would provide the same.

## Problems in the Capacity Planning Process

-   No standard technology.
-   No standard workload.
-   Forecasting future applications/technologies is difficult.
-   Each vendor has their own benchmarks.
-   Distributed environments make modeling even more complex.

## Common Mistakes in the Capacity Planning Process

-   Wrong workload.
-   Startup /shutdown time is generally ignored.
-   Monitoring overheads are ignored.
-   Too much data/too little analysis.

## Example: Tiny URL
##### Traffic

-   Read/Write ratio: 100:1
-   New URL requests: 500M/month
-   URL requests: 500M * 100 = 50 B/month
-   Create URL Queries per second (QPS): 500 million / (30 days * 24 hours * 3600 seconds) = ~200 URLs/s
-   URL request Queries per second (QPS): 100 * 200 URLs/s = 20K/s

##### Storage

-   Storage required: Approx URL size * Requests per month * Years to keep data * 12 months = 500 bytes * 500 million * 7 years * 12 months = 21 TB

##### Memory

If we want to cache some of the hot URLs that are frequently accessed, how much memory will we need to store them? If we follow the 80-20 rule, meaning 20% of URLs generate 80% of traffic, we would like to cache these 20% hot URLs.

Since we have 20K requests per second, we will be getting 1.7 billion requests per day: 20K * 3600 seconds * 24 hours = ~1.7 billion

To cache 20% of these requests, we will need 170GB of memory. 0.2 * 1.7 billion * 500 bytes = ~170GB

#### References:
[https://dzone.com/articles/capacity-planning-process-part-1](https://dzone.com/articles/capacity-planning-process-part-1)
