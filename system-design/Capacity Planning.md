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

