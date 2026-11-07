---
title: "About Cache for Redis"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/about-redis"
---

BytePlus Cache for Redis provides entrusted cache database services. It is compatible with the Redis database engine and can help you build Redis databases on the cloud easily and quickly. Cache for Redis provides a high\-performance and secure Redis database solution. The pay\-as\-you\-go and dynamic scalability are combined to significantly help enterprises reduce costs. It also helps eliminate the complexity of database management and operation.

<span id=".5Lqn5ZOB5LyY5Yq_"></span>
## Product advantages

The code of an application currently using Redis hardly requires any modification. Simply update the original connection code (including address and port number) to the corresponding connection information of Cache for Redis to use Redis.

Cache for Redis has the following advantages to help you build your ideal application:


* High available architecture, automatic node failover, and troubleshooting.

* The data can be partitioned into up to 256 shards.

* Used with ECS, Cloud Monitor, and other BytePlus services to provide entrusted Cache for Redis with high performance and high security.

* Supports online one\-click upscaling, completely transparent to businesses and uses, and resilient and convenient resource upscaling.

* A visual web management interface for online instance restart, parameter modification, data backup and recovery, and other operations. Provides corresponding APIs to facilitate further automated management of instances.

* You can configure automatic backup policies as required or manually create backups. You can use these backups to restore instances.

* Cache for Redis has an account system for you to easily define users and permissions.


<span id=".5qC45b-D57uE5Lu2"></span>
## Core components

<span id=".5a6e5L6L"></span>
### Instance

The basic unit of Cache for Redis is an instance. An instance is an independent, virtualized database running environment. It is a set of multiple server nodes and proxy nodes. The Redis engine runs on the server nodes. When creating an instance, you need to specify the engine version and memory size for all nodes. After creating a Redis instance, you can access it through ECS.

Cache for Redis supports Redis engine versions 5.0, 6.0, and 7.0. Each engine version supports different features and commands.

Run instances on VPC if you need to use VPC services of BytePlus.

<span id=".5pWw5o2u6IqC54K5"></span>
### Server node

A server node is the smallest unit for building an instance of Cache for Redis. Each instance contains at least one server node. If each shard contains only one node, the instance cannot provide data persistence and high availability. If the number of nodes in each shard exceeds 1, the nodes must have a primary\-secondary relationship.

Each server node in the instance uses the same Redis version (the Redis version you selected when creating the instance). All server nodes in an instance have the same specifications and memory capacity. Cache for Redis supports various node specifications that provide different memory capacities. For more information on specifications, refer to [Product specifications](https://docs.byteplus.com/en/docs/redis/product-specification).

<span id=".5Luj55CG6IqC54K5"></span>
### Proxy node

Each instance has proxy nodes. A proxy node is the proxy server node for instances of Cache for Redis. It is used to achieve High Available in Redis instances. The proxy node can recognize and forward the user's read and write requests. These requests can be sent to the primary node or read\-only secondary node according to parameter settings to achieve read/write splitting. For the setting method of read/write splitting, refer to [Setting read/write splitting](https://docs.byteplus.com/en/docs/redis/set-read-write-splitting).

<span id=".5YiG54mH"></span>
### Shard

A shard is a group consisting of 1 to 6 nodes. If a shard contains one node, this node is a read/write node. If a shard contains more than one node, one of them serves as the primary node (also known as a read/write node), and the others are read\-only secondary nodes (also known as secondary nodes).

A Redis instance with sharding cluster enabled has up to 256 shards. You can perform data partitioning across shards. Increase or decrease shards according to your business needs.

A Redis instance with sharding cluster disabled has one shard. It does not support increasing or decreasing the number of shards.

<span id=".5aSN5Yi2"></span>
### Replication

Each shard of primary\-secondary instance contains at least two nodes, one of which is the primary node, and the others are the secondary nodes. There is a replication relationship between the primary and secondary nodes.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each shard of a single\-node instance contains only one node (primary node), without replication relationships between the nodes.</div>


Each secondary node synchronizes with the primary node data through an asynchronous replication mechanism. An application can read data from any node in a Redis instance, but can only write data to the primary node. A Redis instance enhances its scalability by distributing the read requests to multiple secondary nodes and ensures high availability by maintaining the data from secondary nodes. You can increase the number of secondary nodes to further improve availability.

<span id=".5a6e5L6L55uR5o6n"></span>
## Instance monitoring

You can use Cloud Monitor services to monitor the performance and health of Redis instances. View relevant charts of performances under Cloud Monitor on the console of Cache for Redis. For more information, refer to [Monitoring metrics](https://docs.byteplus.com/en/docs/redis/monitoring-metric).
