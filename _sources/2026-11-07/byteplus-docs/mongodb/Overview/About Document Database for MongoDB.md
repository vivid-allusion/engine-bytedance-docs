---
title: "About Document Database for MongoDB"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/about-mongodb"
---

BytePlus Document Database for MongoDB is an online cloud database service that is fully compatible with the MongoDB protocol and offers high availability and high performance.

<span id=".5Lqn5ZOB5LuL57uN"></span>
## Product introduction

Document Database for MongoDB supports multiple architectures to meet the needs of flexible business deployment. In addition to the replica set instance architecture, Document Database for MongoDB also provides a sharding cluster architecture to meet the demands of massive data business scenarios, along with a complete set of solutions including disaster recovery, backup and recovery, and monitoring. It is widely used in industries such as internet (gaming, e\-commerce, live streaming, information, social media), new retail, online education, finance, IoT, government and enterprise.

<span id=".5Lqn5ZOB5LyY5Yq_"></span>
## Product advantages


* **Excellent compatibility**

   100% compatible with the open\-source MongoDB protocol, supporting , 4.2, 4.4, 5.0, 6.0, 7.0, 8.0 and 8.3 versions. You can migrate applications to BytePlus Document Database for MongoDB without any modifications.

* **Data security**

   Ensures data redundancy with a three\-node replica architecture, supports automatic and manual backups, and guarantees data security through multiple backup layers.

* **High availability**

   A replica set architecture with a single primary node and multiple secondary nodes is provided for automatic switchover in the case of a fault, ensuring high service availability.

* **Easy\-to\-use**

   BytePlus offers unified interface management. To deploy a database, simply create instances according to your business's required data space and performance, and they will be ready for use in minutes.

* **Flexible configuration**

   BytePlus Document Database for MongoDB offers various configuration specifications that can be flexibly adjusted to meet different performance and capacity needs. It also provides both replica set and sharding cluster architectures, allowing flexible selection for different business scenarios.

* **Professional O&M**

   There's no need to worry about instance deployment, updates, or troubleshooting. The BytePlus professional O&M team eliminates your concerns, saving you from additional O&M costs.

* **Lower costs**

   Quickly deploy instances online, saving the effort of purchasing, deploying, and configuring self\-built databases. This shortens project cycles and helps businesses launch services quickly. Instantly provision resources based on business needs, eliminating the need to purchase expensive hardware during the initial business phase. This effectively reduces initial asset investment and prevents wasted idle resources.


<span id=".5Lqn5ZOB5p625p6E"></span>
## Product architecture

Document Database for MongoDB categorizes MongoDB instances into replica set instances and sharding cluster instances based on their architectures.

<span id=".5Ymv5pys6ZuG"></span>
### Replica set

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3f7a352a52d398dee008f57e708ac239.png) </span>

Replica set instances provide highly available MongoDB services. A replica set consists of one primary node, one secondary node, and one hidden node. Among them:


* **Primary node**: Provides read and write capabilities. Each replica set instance can only have one primary node. When the cluster status is normal, all data from clients will be written to the primary node.

* **Secondary node**: Ensures high availability and synchronizes data from the primary node via operation logs (oplog). It can be elected as the new primary node if the primary node fails.

* **Hidden node**: Only for ensuring high availability, it is invisible to users, synchronizes data from the primary node via oplog, and can take over a failed node to become a new secondary node, thus ensuring service high availability.


You can quickly create a three\-node replica set instance and visually manage instances through the Volcengine console. Replica set instances support advanced features such as disaster recovery failover and fault migration, and the switching and migration processes are transparent to the business.

<span id=".5YiG54mH6ZuG576k"></span>
### Sharding cluster

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Each Mongos node in a MongoDB instance has the same function. To simplify the illustration, only the connection between Mongos Node 1 and the ConfigServer and Shard nodes is shown below. All other Mongos nodes connect in the same way as Mongos Node 1.</div>


* <div data-tips="true" data-tips-type="tip">In a sharding cluster, each Shard and ConfigServer component uses a 3\-node replica set by default (that is, each Shard or ConfigServer component includes 1 primary node, 1 secondary node, and 1 hidden node). For clarity, the diagram uniformly uses "Replica Set" for illustration. For relationships between nodes in a Replica Set, refer to the <a href="https://docs.byteplus.com/en/docs/mongodb/about-mongodb#.5Ymv5pys6ZuG">Replica set architecture</a>.</div>



<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2b6f4620ce48c6201255c87cdd5f2422.png) </span>

Sharding cluster instances can provide horizontally scalable MongoDB services. Sharding clusters automatically split large collections across nodes to meet capacity and performance requirements in large\-scale, high\-performance scenarios. The sharding process is transparent to frontend applications. A sharding cluster primarily consists of ConfigServers, Mongos, and Shards, where:


* **Shard**: Responsible for storing database data within a sharding cluster instance. Each Shard uses a 3\-node replica set by default (that is, one Shard typically contains one primary node, one secondary node, and one hidden node).

   When creating an instance, you can horizontally scale cluster data storage and read/write concurrency by adding multiple data shards.

* **Mongos**: The entry point for database requests in a sharding cluster instance. All requests are coordinated through Mongos nodes. Mongos itself acts as a request distribution center, responsible for forwarding corresponding data requests to the appropriate Shard servers.

   In a production environment, it is recommended to use multiple Mongos nodes as request entry points to achieve load balancing and prevent a single failure from rendering all requests inoperable.

* **ConfigServer**: Stores the configuration for all database metadata (such as routing and sharding) within a sharding cluster instance. When a routing node is started or restarted for the first time, it loads configuration information from the configuration node. Changes in configuration node information notify all routing nodes to update their status, ensuring that routing nodes can continue to route accurately. Each ConfigServer uses a 3\-node replica set by default (that is, a ConfigServer contains a primary node, a secondary node, and a hidden node).


When creating a MongoDB instance, you can select the number and specification configuration of Mongos nodes and data shards based on your business data requirements.
