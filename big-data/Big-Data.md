**Big data**
-------------

**Big data** is a blanket term for the non-traditional strategies and technologies needed to gather, organize, process, and gather insights from large datasets.

Characterisitcs of Big Data Technology - **3 V's**

- **Volume** – The volume of data coming from different sources is high and potentially increasing day by day.

- **Velocity** – A single processor, limited RAM and limited storage based system is not enough to process this high volume of data.

- **Variety** – Data coming from different sources varies


**Big Data Glossary**

- **Big data**: Big data is an umbrella term for datasets that cannot reasonably be handled by traditional computers or tools due to their volume, velocity, and variety. This term is also typically applied to technologies and strategies to work with this type of data.

- **Batch processing**: Batch processing is a computing strategy that involves processing data in large sets. This is typically ideal for non-time sensitive work that operates on very large sets of data. The process is started and at a later time, the results are returned by the system.

- **Cluster computing**: Clustered computing is the practice of pooling the resources of multiple machines and managing their collective capabilities to complete tasks. Computer clusters require a cluster management layer which handles communication between the individual nodes and coordinates work assignment.

- **Data lake**: Data lake is a term for a large repository of collected data in a relatively raw state. This is frequently used to refer to the data collected in a big data system which might be unstructured and frequently changing. This differs in spirit to data warehouses (defined below).

- **Data mining**: Data mining is a broad term for the practice of trying to find patterns in large sets of data. It is the process of trying to refine a mass of data into a more understandable and cohesive set of information.

- **Data warehouse**: Data warehouses are large, ordered repositories of data that can be used for analysis and reporting. In contrast to a data lake, a data warehouse is composed of data that has been cleaned, integrated with other sources, and is generally well-ordered. Data warehouses are often spoken about in relation to big data, but typically are components of more conventional systems.

- **ETL**: ETL stands for extract, transform, and load. It refers to the process of taking raw data and preparing it for the system's use. This is traditionally a process associated with data warehouses, but characteristics of this process are also found in the ingestion pipelines of big data systems.

- **Hadoop**: Hadoop is an Apache project that was the early open-source success in big data. It consists of a distributed filesystem called HDFS, with a cluster management and resource scheduler on top called YARN (Yet Another Resource Negotiator). Batch processing capabilities are provided by the MapReduce computation engine. Other computational and analysis systems can be run alongside MapReduce in modern Hadoop deployments.

- **In-memory computing**: In-memory computing is a strategy that involves moving the working datasets entirely within a cluster's collective memory. Intermediate calculations are not written to disk and are instead held in memory. This gives in-memory computing systems like Apache Spark a huge advantage in speed over I/O bound systems like Hadoop's MapReduce.

- **Machine learning**: Machine learning is the study and practice of designing systems that can learn, adjust, and improve based on the data fed to them. This typically involves implementation of predictive and statistical algorithms that can continually zero in on "correct" behavior and insights as more data flows through the system.

- **Map reduce** (big data algorithm): Map reduce (the big data algorithm, not Hadoop's MapReduce computation engine) is an algorithm for scheduling work on a computing cluster. The process involves splitting the problem set up (mapping it to different nodes) and computing over them to produce intermediate results, shuffling the results to align like sets, and then reducing the results by outputting a single value for each set.

- **NoSQL**: NoSQL is a broad term referring to databases designed outside of the traditional relational model. NoSQL databases have different trade-offs compared to relational databases, but are often well-suited for big data systems due to their flexibility and frequent distributed-first architecture.

- **Stream processing**: Stream processing is the practice of computing over individual data items as they move through a system. This allows for real-time analysis of the data being fed to the system and is useful for time-sensitive operations using high velocity metrics.

- **Data Types**
1. Structured Data: Data which is presented in a tabular format and stores in RDMS (Relational Database Management System)
2. Semi-structured Data: Data which does not have a formal data model and stores in XML, JSON etc.
3. Unstructured Data: Data which does not have a pre-defined data model like video, audio, image, text, web logs, system logs etc.


**Big Data Life Cycle**

- **Ingesting Data into the System**:

Data ingestion is the process of taking raw data and adding it to the system. The complexity of this operation depends heavily on the format and quality of the data sources and how far the data is from the desired state prior to processing.

Technologies used:

**Apache Sqoop**:- takes existing data from relational databases and add it to a big data system. 

**Apache Flume and Apache Chukwa**:- projects designed to aggregate and import application and server logs.

**Apache Kafka**:- can be used as an interface between various data generators and a big data system.

**Gobblin**:- helps to aggregate and normalize the output of these tools at the end of the ingestion pipeline.

- **Persisting the Data in Storage**:

The ingestion processes typically hand the data off to the components that manage storage, so that it can be reliably persisted to disk.
This usually means leveraging a distributed file system for raw data storage. Solutions like **Apache Hadoop's HDFS** filesystem allow large quantities of data to be written across multiple nodes in the cluster. This ensures that the data can be accessed by compute resources, can be loaded into the cluster's RAM for in-memory operations, and can gracefully handle component failures.
Data can also be imported into other distributed systems for more structured access. Distributed databases, especially **NoSQL** databases

- **Computing and Analyzing Data**:

Once the data is available, the system can begin processing the data to surface actual information.

**Batch processing**: is one method of computing over a large dataset. The process involves breaking work up into smaller pieces, scheduling each piece on an individual machine, reshuffling the data based on the intermediate results, and then calculating and assembling the final result. These steps are often referred to individually as splitting, mapping, shuffling, reducing, and assembling, or collectively as a distributed map reduce algorithm. This is the strategy used by Apache Hadoop's MapReduce.

**Real-time processing**: Real-time processing demands that information be processed and made ready immediately and requires the system to react as new information becomes available. One way of achieving this is stream processing, which operates on a continuous stream of data composed of individual items. Another common characteristic of real-time processors is in-memory computing, which works with representations of the data in the cluster's memory to avoid having to write back to disk. Apache Storm, Apache Flink, and Apache Spark provide different ways of achieving real-time or near real-time processing. 

- **Visualizing the Results**:
Due to the type of information being processed in big data systems, recognizing trends or changes in data over time is often more important than the values themselves. 

**Prometheus**: Real-time processing is frequently used to visualize application and server metrics.

**Elastic Stack**: Composed of Logstash for data collection, Elasticsearch for indexing data, and Kibana for visualization, the Elastic stack can be used with big data systems to visually interface with the results of calculations or raw metrics.

**Silk**: Apache Solr for indexing and a Kibana fork called Banana for visualization.

**How Does Hadoop Work?**

- **Stage 1**

A user/application can submit a job to the Hadoop (a hadoop job client) for required process by specifying the following items:

The location of the input and output files in the distributed file system.

The java classes in the form of jar file containing the implementation of map and reduce functions.

The job configuration by setting different parameters specific to the job.

- **Stage 2**
The Hadoop job client then submits the job (jar/executable etc) and configuration to the JobTracker which then assumes the responsibility of distributing the software/configuration to the slaves, scheduling tasks and monitoring them, providing status and diagnostic information to the job-client.

- **Stage 3**
The TaskTrackers on different nodes execute the task as per MapReduce implementation and output of the reduce function is stored into the output files on the file system.

**MapReduce Algorithm**
MapReduce is a Distributed Data Processing Algorithm, introduced by Google in it’s MapReduce Tech Paper. MapReduce algorithm is mainly useful to process huge amount of data in parallel, reliable and efficient way in cluster environments.

**MapReduce Algorithm Steps**

**Input - Queen, Joker, King, King, King, Queen, King, Queen, Joker, Joker, King, King**

- **Map Function**

1. Splitting: Dataset 1 - Queen, Joker, King, King; Dataset 2 - King, Queen, King, Queen; Dataset 3 - Joker, Joker, King, King

2. Mapping - Dataset 1 - (Queen,1), (Joker,1), (King,1), (King,1); Dataset 2 - (King,1), (Queen,1), (King,1), (Queen,1); Dataset 3 - (Joker,1), (Joker,1), (King,1), (King,1)

- **Shuffle/Merge Function**

1. Step 1: Dataset 1 - (Queen,1), (Joker,1), (King,1,1); Dataset 2 - (King,1,1), (Queen,1,1); Dataset 3 - (Joker,1,1), (King,1,1)

1. Step 1: (Queen, 1,1,1); (King,1,1,1,1,1,1); (Joker, 1,1,1)

3. Sorting: (Joker, 1,1,1); (King,1,1,1,1,1,1); (Queen, 1,1,1)

- **Reduce Function**
(Joker, 3); (King,6; (Queen, 3)

**Output - (Joker, 3); (King,6); (Queen, 3)**
