---
title: "Glossary"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/glossary"
---

This topic summarizes the terms related to the instances of Document Database for MongoDB.


|Term |Description |
|---|---|
|Region |The geographical location of the MongoDB instance.<br><br>Specify the region when creating a MongoDB instance; it cannot be changed after the instance is created. |
|Availability zone |An availability zone refers to a physical area within the same region, isolated by its own power and network infrastructure. Availability zones feature interconnected internal networks, resulting in lower network latency within a single zone and enabling fault isolation between different availability zones.<br><br>Single availability zone means that the three nodes in the replica set of a MongoDB instance are in the same availability zone. If ECS and MongoDB are deployed in the same availability zone, the network latency will be even less. |
|Instance |An instance is the basic unit for managing MongoDB services.<br><br>MongoDB provides instances with different architectures and specifications to meet business requirements in various scenarios. |
|Replica set |Document Database for MongoDB replica set instances provide high\-availability MongoDB services.<br><br>Each replica set includes 1 primary node, 1 secondary node, and 1 hidden node. |
|Primary node |Also known as the primary database, it provides read and write functionality. Each replica set instance can only have one primary node.<br><br>When the cluster status is normal, all data from clients will be written to the primary node. |
|Secondary node |Ensure high availability by synchronizing primary node data through oplog (operation logs).<br><br>It can be elected as the new primary node if the primary node fails. |
|Hidden node |Only used to ensure high availability and is invisible to users. It synchronizes the data on the primary node through Oplog (operation log).<br><br>If a secondary node fails, the hidden node takes over as the new secondary node to ensure high availability. |
|Read\-only node |Mainly applicable to scenarios with a large amount of data read requests. It synchronizes data from the primary node or secondary node through the operation log (oplog), and the system automatically routes read requests to the read\-only node to relieve the access pressure on the primary node.<br><br>For more details on different node types, refer to [Comparison of different types of nodes](https://docs.byteplus.com/en/docs/mongodb/managing_read_only_nodes#.5LiN5ZCM57G75Z6L55qE6IqC54K55a-55q-U). |
|Sharding cluster |Sharding cluster instances provide horizontally scalable MongoDB services. Sharding clusters automatically split large collections across nodes to meet capacity and performance requirements in large\-scale, high\-performance scenarios.<br><br>The sharding process is transparent to frontend applications. A sharding cluster consists of multiple shards, sharding proxy nodes (Mongos nodes), and metadata server nodes (ConfigServer nodes). |
|Shard |Also known as a data shard, it stores database data in a sharding cluster instance. Each Shard defaults to a 3\-node replica set (meaning one Shard by default includes one primary node, one secondary node, and one hidden node).<br><br>When creating an instance, you can horizontally scale cluster data storage and read/write concurrency by adding multiple data shards. |
|Mongos |The entry point for database requests in a sharding cluster instance. All requests are coordinated through Mongos nodes. Mongos itself acts as a request distribution center, responsible for forwarding corresponding data requests to the appropriate Shard servers.<br><br>In a production environment, it is recommended to use multiple Mongos nodes as request entry points to achieve load balancing and prevent a single failure from rendering all requests inoperable. |
|ConfigServer |Store all database metadata configurations (such as routing and sharding) for a sharding cluster instance. Mongos nodes load configuration information from ConfigServer nodes when first started or restarted.<br><br>Changes in ConfigServer node information notify all Mongos nodes to update their status, ensuring ConfigServer nodes can continue to route accurately.<br><br>By default, each ConfigServer uses a 3\-node replica set (meaning each ConfigServer includes 1 primary node, 1 secondary node, and 1 hidden node). |
|Storage |Hard disk capacity of Document Database for MongoDB.<br><br>You can choose the proper storage based on your business data volume when creating an instance. |
|Backup |A backup stores all data of a MongoDB instance at a specific point in time.<br><br>Document Database for MongoDB provides both automatic and manual backup methods to effectively prevent data loss and avoid risks caused by improper operations. |
|Physical backup |Back up database\-related physical files in a MongoDB instance.<br><br>You can use physical backup to copy all physical files of a MongoDB database. Physical backup generally offers higher efficiency. |
|Logical backup |Retain the data status of the disk from a certain point of time for database recovery.<br><br>You can export database objects and save them to binary files using logical backup. Backup with logical backups is less efficient. |
|WiredTiger storage engine |An open\-source, independent storage engine characterized by high performance and easy scalability.<br><br>For more details, refer to [WiredTiger Storage Engine](https://www.mongodb.com/docs/v5.0/core/wiredtiger/). |
