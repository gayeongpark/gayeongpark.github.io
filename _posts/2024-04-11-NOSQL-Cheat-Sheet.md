---
layout: post
title: NoSQL assessment preparation
subtitle: Assessment preparation for NoSQL database (particularly MongoDB)
tags: [NoSQL, database, assessment, mongoDB, data optimization, SE_06]
comments: true
author: Lantana Park
---

# The concepts, characteristics and significance of NoSQL

- It was developed from a open-source project to deal with limitation of SQL database

- It provides a free schema structure, and it offers rapid scalability to manage large and unstructured data sets.

- It is a type of distributed database, which means that information can be copied and stored on various servers, which can be remote or local. This ensures availability and reliability of data. Because, if some of the data goes offline, the rest of the distributed database can continue to run.

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

    NoSQL is designed for horizontal scalability. This means that a NoSQL database can handle large volumes of data by distributing it across multiple servers (sharding). Thus, it allows developers to utilize cheaper, standard server machines, which can be more cost-efficient.

2.  **Schema flexibility**

    NoSQL provides a flexible schema model, which allows developers to easily add or remove data fields without modifying the existing database schema records. Even though I created a schema to specify the data structure, I can dynamically add a new field so that new data and records in the same collection can have different structures.

3.  **Fast queries (fast reading)**

    Queries in NoSQL databases can be faster than those in SQL databases. Since data in SQL databases is typically normalized, querying for a single entity often requires joining data from multiple tables, which becomes costly as the tables grow. However, data in NoSQL databases is accessed and stored together due to their denormalized structure. Hence, queries typically do not require data joining, making both queries and read operations very fast. Additionally, many NoSQL databases support indexing, which can significantly speed up query processing.

## Disadvantages of NoSQL

1. **No standardized language and interface to complex queries**

   There is no standardized query languages to conduct complex queries. Developers should learn and adapt to the specific query languages and interfaces provided by each NoSQL database system.

2. **Data retrieval inconsistency**

   **NoSQL databases prioritize speed and availability due to their distributed nature, which can lead to inconsistencies in data retrieval**. **This occurs because data might not be updated simultaneously across all servers, resulting in different responses based on the server accessed**.

   **Unlike traditional SQL databases that follow ACID principles (Atomicity, Consistency, Isolation, Durability) to ensure data integrity, NoSQL databases often do not meet the consistency requirement**. This means they might not provide the same data consistency as seen in ACID-compliant databases.

   Instead of ACID, many NoSQL databases use the BASE (Basically Available, Soft state, Eventual consistency) model. Here, **consistency is achieved eventually, meaning that while immediate consistency is not guaranteed, the data will become consistent after a short delay**, which is generally acceptable in many real-world applications like social media or online shopping.

   - **Basically Available**: The system remains operational even in the presence of failures, ensuring that users can still access data and perform operations.

   - **Soft state**: The state of the system may change over time, even without input, due to eventual consistency and asynchronous updates.

   - **Eventual consistency**: The system guarantees that, given enough time and no further updates, all replicas of data will eventually converge to a consistent state.

   ### eventual consistency vs consistency

   Eventual consistency allows for temporary inconsistency between replicas with the assurance that they will eventually converge to a consistent state, while consistency ensures immediate and strong consistency across all replicas at all times.

# Two types of data processing system: OLAP (online analytical processing) and OLTP (online transaction processing)

## What is OLTP (Online Transactional Processing)?

- It is designed to **handle day-to-day operational tasks**, including simple lookups, retrieving, modifying individual records. For example, finding a customer id and retrieving their orders.

- It **handles many updates, such as updating customer information or processing payments**.

- It **handles real-time transactions like online purchases or banking transactions**. So, **strong consistency** is crucial to ensure data integrity.

## What is OLAP (Online Analytical Processing)?

- It is designed to **perform complex analytical queries and generating reports to support decision-making processes**.

- It involves operations such as aggregations, joins on large data sets. For example, calculating total revenue by stores, product, clerk, or date range. However, **it does not handle direct updates**.

- It **focuses on providing fast query response times** rather then data integrity.

# CAP theorem and its implications for selecting a NoSQL database

Distribution is important in NoSQL because of its characteristics. It relies on horizontal scaling out to handle growth/large data sets. CAP theorem provides a fundamental understanding to complexities of distributed system design. It helps in making informed decisions that align with the application's requirements and the system's architectural goals.

![mongoDB](/assets/img/mongodb/CAP_Theorem_Venn_Diagram.png)

- **Consistency** means every read receives the most recent write.
- **Availability** means every request receives a (non-error) response, without the guarantee that it contains the most recent write.
- **Partition tolerance** means the system continues to operate despite arbitrary message loss or failure of part of the system.

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
