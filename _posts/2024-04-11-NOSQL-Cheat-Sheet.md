---
layout: post
title: NoSQL assessment preparation
subtitle: Assessment preparation for NoSQL database (particularly NoSQL - MongoDB)
tags: [NoSQL, database, assessment, mongoDB, data optimization]
comments: true
author: Lantana Park
---

# The concepts, characteristics and significance of NoSQL

- It was developed from open-source project to deal with limitation of SQL database

- It provides a free schema structure, so it offers rapid scalability to manage large and unstructured data sets.

- It is also type of distributed database, which means that information is copied and stored on various servers, which can be remote or local.(sharding) This ensures availability and reliability of data. Because, if some of the data goes offline, the rest of the database can continue to run.

# Different type of NoSQL database and its advantages and disadvantages

1. Document data

   Data is stored hierarchically in JSON-based documents. **MongoDB**

   ![document-based](/assets/img/mongodb/MongoDB%20document%20based.png)

2. Key Value data

   Data is represented as a collection of key-value pairs. **Redis**

   ![keyandvalue](/assets/img/mongodb/key-value.png)

   ### Difference between document based data and key value data

   Document oriented-database store data in JSON document, which allows for a complex structure compared to the simple key-value pairs. Each document can contain nested/embedded structure like arrays and sub-documents.

3. Wide-Column data

   A wide-column stores data in tables, where the names and formats of individual attributes can vary from row to row. **Apache Cassandra**

   ![column](/assets/img/mongodb/Wide-column-Database.webp)

4. Graph data

   Graph is stored in a graph structure as node, edge, and data properties. **Noe4j**

   ![neo4j](/assets/img/mongodb/Neo4j-graph.png)

# The advantages and disadvantages of NoSQL compared to relational databases

## Advantages of NoSQL

1.  **Scalability (Horizontal)**

    NoSQL, especially MongoDB, designed for **horizontal scalability**. That means NoSQL database like MongoDB can handle large volumes of data by distributing it across multiple servers (sharding). That makes it easier to scale out (horizontal scaling). Thus it allows developers to use of **cheaper** and standard machines and can be more cost-efficient at scale.

2.  **Schema flexibility**

    NoSQL, especially MongoDB, provides flexible schema model. Which allows me to easily add or remove data fields without modifying the existing database schema to affecting other data records. Even though I made a schema for specifying the data structure, I can add a new field dynamically so that a whole new data and records in the same collection can have different structures.

3.  **Fast queries(fast reading)**

    Queries in NoSQL database can be faster than SQL database. Since Data in SQL database is typically normalized, queries for a single object or entity require to join data from multiple tables. So, it takes costs when the tables are growing. However, data in NoSQL databases can be access and stored together due to denormalized structure. Hence queries typically do not require joins, and **the queries are very fast and readings are very fast.**

## Disadvantages of NoSQL

1. **No standardized language and interface to complex queries**

   There is no standardized query languages to conduct complex queries. Developers should learn and adapt to the specific query languages and interfaces provided by each NoSQL database system.

2. **Data retrieval inconsistency**

   NoSQL databases prioritize speed and availability due to their distributed nature, which can lead to inconsistencies in data retrieval. This occurs because data might not be updated simultaneously across all servers, resulting in different responses based on the server accessed.

   Unlike traditional databases that follow ACID principles (Atomicity, Consistency, Isolation, Durability) to ensure data integrity, NoSQL databases often do not meet the consistency requirement. This means they might not provide the same data consistency as seen in ACID-compliant databases.

   Instead of ACID, many NoSQL databases use the BASE (Basically Available, Soft state, Eventual consistency) model. Here, consistency is achieved eventually, meaning that while immediate consistency is not guaranteed, the data will become consistent after a short delay, which is generally acceptable in many real-world applications like social media or online shopping.

   - **Basically Available**: The system remains operational even in the presence of failures, ensuring that users can still access data and perform operations.

   - **Soft state**: The state of the system may change over time, even without input, due to eventual consistency and asynchronous updates.

   - **Eventual consistency**: The system guarantees that, given enough time and no further updates, all replicas of data will eventually converge to a consistent state.

   ### eventual consistency vs consistency

   Eventual consistency allows for temporary inconsistency between replicas with the assurance that they will eventually converge to a consistent state, while consistency ensures immediate and strong consistency across all replicas at all times.

# CAP theorem and its implications for selecting a NoSQL database

Distribution is important in NoSQL because of its characteristics. It relies on horizontal scaling out to handle growth/large data sets. CAP theorem provides a fundamental understanding to complexities of distributed system design. It helps in making informed decisions that align with the application's requirements and the system's architectural goals.

![mongoDB](/assets/img/mongodb/CAP_Theorem_Venn_Diagram.png)

- **Consistency**: all clients see the same data at the same time. For making this to fulfill, whenever data is written to one node, it should be instantly forwarded or replicated to all the other nodes in the system. That means all nodes in the system continue to cooperatively provide service, even when nodes become unavailable. Consistency supports modern workloads that are less dependent on a strong consistency, but rely heavily on availability.

- **Availability**: any client making a request for data gets a response, even if one or more nodes are down. That means all working nodes in the distributed system return a valid response for any request, without exception.

- **Partition tolerance**: it is a communications break within a distributed system — a lost or temporarily delayed connection between two nodes. Partition tolerance means that each system must continue to work together despite any number of communication breakdowns between nodes in the system.

**A distributed database system can only fully satisfy two out of the three guarantees**

- CP database: it delivers **consistency** and **partition tolerance** at the expense of availability. When a partition occurs between any two nodes, **the system has to shut down the non-consistent node until the partition is resolved**.

- AP database: it delivers **availability** and **partition tolerance** at the expense of consistency. When a partition occurs, all nodes remain available but those at the wrong end of a partition might **return an older version of data than others**.

- CA database: it delivers **consistency** and **availability** across all nodes. It can’t do this if there is a partition between any two nodes in the system, however, and therefore **can’t deliver fault tolerance**.

## MongoDB and the CAP theorem

MongoDB is classified as a **CP** data store. Because it resolves network partitions by maintaining consistency, while compromising on availability.

MongoDB uses the single master node that receives all write operations. The primary node is the source of truth for all data writes. When the primary node becomes unavailable, the secondary node, replicated from the primary node(Consistency), will be elected as the new primary node.

# Optimize the respective data structure for huge amounts of data, performance and efficiency in NoSQL (especially MongoDB)

It involves several strategies tailored to the specific type of NoSQL database.

1. **Embedding and referencing**

   Unlike SQL databases, NoSQL databases often benefit from denormalization to avoid costly join operations. Embedding generally provides better performances for read operations. Embedded data models also allow developers to update related data in a single write operation. Referencing makes much more sense when modeling many to many relationships. However, whenever referencing, an application must issue follow-up queries to resolve any references. This, in turn, requires more round-trips to the server.

2. **Indexing**

   Indexes improve the efficiency of read operations by reducing the amount of data that query operations need to process.

3. **Sharding/replication**

   Distributing data across multiple servers to horizontally scale out database improves scalability and performance.

   Creating replica sets for enabling the creation of multiple copies of data for high availability and fault tolerance. Having multiple replicas of data provides a level of data redundancy, helping protect against data loss.

4. **Caching**

   Frequent database queries can impact application performance. Implementing caching mechanisms to store frequently accessed data reduces query load.
