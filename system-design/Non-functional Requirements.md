# Non-functional Requirements

A non-functional requirement is a specification that describes the system’s operation capabilities and constraints that enhance its functionality. These may be speed, security, reliability, etc.

## Performance 
Performance defines how fast a software system or its particular piece responds to certain users’ actions under certain workload. In most cases, this metric explains how much a user must wait before the target operation happens (the page renders, a transaction is processed, etc.) given the overall number of users at the moment. But it’s not always like that. Performance requirements may describe background processes invisible to users, e.g. backup.

## Scalability (Scale Up|Out)
Increasing or decreasing the capacity of a system by making effective use of resources is known as scalability. A scalable system can handle increasing numbers of requests without adversely affecting response time and throughput.

In software engineering, scalability is a desirable property of a system, a network, or a process, which indicates its ability to either handle growing amounts of work in a graceful manner or to be enlarged.

**Example**

A scalable  online transaction processing system  or database management system is one that can be upgraded to process more transactions by adding new hardware resources (processors, devices and storage) and which can be upgraded easily and transparently without shutting it down.

**Scaling**
Scaling is the process of increasing or decreasing the capacity of the system by changing the number of processes available to service requests.
Methods of adding more resources for a particular application fall into two broad categories:

-   Scale vertically (scale up)
    To scale vertically (or scale up) means to add:

		1. resources (addition of CPUs or memory)
    
		2. or process (addition of the same process)
	Example: You currently have a 800MHz CPU in your computer. To increase processing power, you decide to buy a new computer with an 8-core 3.4GHz CPU to replace your old computer.

-   Scale horizontally (scale out)
“Scale out” is when you increase the number of processing machines (computers, processors, servers, etc) to increase processing power.

	To scale horizontally (or scale out) means to add more nodes to a system, such as adding a new computer to a distributed software application. An example might be scaling out from one web server system to three.

	As computer prices drop and performance continues to increase, low cost “commodity” systems can be used for high performance computing applications such as seismic analysis and biotechnology workloads that could in the past only be handled by supercomputers.

	Hundreds of small computers may be configured in a  **cluster**  to obtain aggregate computing power.

#### Tradeoffs

There are tradeoffs between the two models.

Larger numbers of computers means increased management complexity, as well as a more complex programming model and issues such as  throughput and latency between nodes; also, some applications do not lend themselves to a distributed computing model.

Scale up got expensive fast. An other solution is to buy cheaper, commodity boxes to scale out instead of up, distributing the application (database,…) out over hundreds or even thousands of servers.

## Reliability
This quality attribute specifies how likely the system or its element would run without a failure for a given period of time under predefined conditions. Traditionally, it’s expressed as a probability percentage. For instance, if the system has 85 percent reliability for a month, this means that during this month, under normal usage conditions, there’s an 85 percent chance that the system won’t experience critical failure.


## Maintainability
 Maintainability defines the time required for a solution or its component to be fixed, changed to increase performance or other qualities, or adapted to a changing environment. Like reliability, it can be expressed as a probability of repair during some time. For example, if you have 75 percent maintainability for 24 hours, this means that there’s a 75 percent chance the component can be fixed in 24 hours.

## Availability
 And finally, availability describes how likely the system is accessible for a user at a given point in time. While it can be expressed as a probability percentage, you may also define it as a percentage of time the system is accessible for operation during some time period. For instance, the system may be available 98 percent of the time during a month. Availability is perhaps the most business-critical requirement, but to define it, you also must have estimations for reliability and maintainability.

## Usability

Usability is yet another classical nonfunctional requirement that addresses a simple question:  _How hard is it to use the product?_ Defining these requirements isn’t as easy as it seems. There are many types of usability criteria. One of the most popular one ones by  [Nielsen Norman Group](https://www.nngroup.com/articles/usability-101-introduction-to-usability/)  suggests evaluating usability with five dimensions:

**Learnability.** How fast is it for users to complete the main actions once they see the interface?

**Efficiency.** How quickly users can reach their goals?

**Memorability.** Can users return to the interface after some time and start efficiently working with it right away?

**Errors.** How often do users make mistakes?

**Satisfaction.** Is the design pleasant to use?

## General recommendations to documenting non-functional requirements

**Make them measurable and testable.** To understand whether your system meets quality constraints, make sure to quantify your requirements. You have to specify the units of measurement, the methods that you are going to use, as well as success and failure levels.

**Set requirements for system components rather than whole products.** Consider which critical interfaces and systems need such requirements. If your users never interact with some part of your product (e.g. an admin panel) setting up performance limitations for these components may be useless or harmful, since your team will expend much more effort with no evident gain.

**Link NFR with business objectives.** The minute-long difference in system availability may not have a drastic impact on your sales numbers, but sometimes it can mean additional weeks of engineering. Try breaking down your business objectives into system requirements.

**Consider third-party limitations.** If a third-party API that you must use returns data slower than you want, there isn’t much you or your team can do about it.

**Consider architectural limitations.** Legacy systems can put constraints on quality. While refactoring legacy code is doable, sometimes the current architecture must be completely reworked to meet some of the requirements.

**Look for existing standards and guides.** It’s likely that many system quality recommendations have been made before. So, check  guidelines to suggest some requirements for your app.

## Performance Testing
Software Performance testing is type of testing perform to determine the performance of system to major the measure, validate or verify quality attributes of the system like responsiveness, Speed, Scalability, Stability under variety of load conditions. The system is tested under a mixture of load conditions and check the time required responding by the system under varying workloads. Software performance testing involves the testing of application under test to ensure that application is working as expected under variety of load conditions. The goal of performance testing is not only find the bugs in the system but also eliminate the performance bottlenecks from the system.

### Goals of Performance Testing

The entire process of software performance testing is done to accomplish a set of four goals:

1.  To determine the throughput or the rate of transaction.
2.  To determine the server response time, which is the time taken by a given application node to give a response to a request made by another node.
3.  To determine the response time of the render, which requires the inclusion of functional test scripts in the test scenario.
4.  To determine the performance specifications and document them in the test plan.


### Types of Performance Testing
**Load Tests**
Load testing is used to study the behavior of the application under specified loads. It also shows how an application will function when the majority of its users are logged in. Load testing is mainly done to measure response times, resource utilization levels, and throughput rates.

**Stress Tests**
A stress test is performed to determine the upper limit of the application capacity and how the application performs when the current load exceeds the expected maximum. The primary focus of performing testing is to identify application bugs that occur in high load conditions. This test determines the maximum load that a given application can support.

**Soak Tests**
Soak tests are performed with the objective of determining how the application endures under a continuous expected load. For example, a soak test can be performed to monitor memory utilization and detect memory leaks and other performance problems that can occur. The objective of performing this type of test is to determine the application’s performance in sustained use.

**Spike Tests**
Spike testing is performed to determine whether a given application has the capacity to sustain the workload. The test is accomplished by increasing the number of end-users by a large amount and assessing the performance of the application overall.

**Endurance testing**:
Endurance testing is a non functional type of testing. Endurance testing involves testing a system with a expected amount of load over a long period of time to find the behavior of system. Let’s take a example where system is designed to work for 3 hrs of time but same system endure for 6 hrs of time to check the staying power of system. Most commonly test cases are executed to check the behavior of system like memory leaks or system fails or random behavior. Sometimes endurance testing is also referred as Soak testing.

**Scalability Testing**:

Scalability Testing is type of non-functional tests and it is the testing of a software application for determine its capability to scale up in terms of any of its non-functional capability like the user load supported, the number of transactions, the data volume etc. The main aim if this testing is to understand at what peak the system prevent more scaling.

**Volume testing**:

Volume testing is non-functional testing which refers to testing a software application with a large amount of data to be processed to check the efficiency of the application. The main goal of this testing is to monitor the performance of application under varying database volumes.

### Top Performance Testing Tools

 - WebLOAD
 - LoadRunner
 - Apache JMeter
 - NeoLoad
 - LoadUI
 - OpenSTA

### Performance Testing Process
![enter image description here](https://media.geeksforgeeks.org/wp-content/uploads/20190418124711/Capture4556.jpg)