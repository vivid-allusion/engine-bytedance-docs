---
title: "Instance type selection guide"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/instance-type-selection-guide"
---

Before using instances of Cache for Redis, you need to consider factors such as use case, service load, product performance, and price to choose the Redis instance that best suits your services with optimal cost\-effectiveness.

<span id=".6YCJ5Z6L5rWB56iL"></span>
## Selection process

In the specific business, you can refer to the following steps to complete the Redis instance selection:

<span id=".XzEt6aKE5Lyw5omA6ZyA5pWw5o2u5bqT6LWE5rqQ"></span>
### 1. Estimate database resources required

Preliminary estimates of the required database resources are based on the following service metrics.


|Service metrics |Description |
|---|---|
|Data volume |Peak amount of data that the Serviceneeds to store in Redis. |
|Queries per second (QPS) |Peak number of Redis service queries per second. |
|Bandwidth per second (BPS) |Peak Redis service data volume per second. |
|Connections |Peak number of connections between a client and a single Redis instance. |


<span id=".XzIt6YCJ5oup5a6e5L6L5p625p6E"></span>
### 2. Select instance architecture

Based on the estimated resource requirements, choose the appropriate instance architecture first. Cache for Redis currently supports the following two architectures.


|Instance architecture |Introduction |Applicable scenario |
|---|---|---|
|[Sharding cluster enabled](https://docs.byteplus.com/en/docs/redis/product-component-architecture#.5ZCv55So5YiG54mH6ZuG576k) |Redis instances with sharding cluster enabled can use sharded partitions to increase cache capacity and concurrent connections. Each shard contains one primary node and one to five secondary nodes. The shard itself is invisible externally by default. If the primary node fails in the shard, a secondary node in the same shard will be upgraded to the primary node to continue providing the services. |* Large data volume/rapid data growth scenario.<br><br>* Scenarios with high overall read and write request pressure.<br><br>* Scenarios with high data throughput, traffic, and high performance requirements.<br><br>* Services with persistent requirements. |
|[Sharding cluster disabled](https://docs.byteplus.com/en/docs/redis/product-component-architecture#.5pyq5ZCv55So5YiG54mH6ZuG576k) |Redis instances with sharding cluster disabled only contain one shard, and the data of the primary and secondary nodes in the shard is maintained consistently through real\-time replication mechanism. If the primary node fails, the secondary node automatically upgrades to the primary node. |* Businesses with high requirements for Redis command compatibility.<br><br>* Service with a small amount of data and manageable pressure.<br><br>* Service uses relatively simple Redis data elements.<br><br>* Servicees with persistent requirements. |


<span id=".XzMt56Gu5a6a5a6e5L6L6KeE5qC8"></span>
### 3. Determine instance specification

On the basis of the selected instance architecture, determine the appropriate instance specifications, including node specifications, number of shards, and number of nodes per shard.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the total memory required for an instance is the same, we recommend that you opt for smaller\-size nodes and more shards. For example, if the total memory required for the service is 8 GiB, compared with 4 GiB/per shard \* two shards, we recommend that you use a combination of 2 GiB/per shard \* four shards or 1 GiB/per shard \* 8 shards. The two options using more shards increase the total number of connections available and bandwidth of the instance, and reduce the time required for Redis snapshots, primary\-secondary replication, and modification of instance specification at the same time.</div>



|Option |Description |
|---|---|
|Node specification |Cache for Redis supports various node specifications, and the maximum connection count and QPS values supported by the specifications are fixed (5,000 and 80,000, respectively). However, memory and bandwidth vary between different node specifications. For more information on node performance, refer to [Instance specifications](https://docs.byteplus.com/en/docs/redis/product-specification).<br><br>Therefore, when selecting node specifications, the main considerations are the amount of data and bandwidth your service requires. |
|Number of shards |* Redis instances with sharding cluster disabled only contain one shard by default. If an instance with sharding cluster disabled can meet your application scenario, you do not need to consider the number of shards used.<br><br>* For Redis instances with sharding cluster enabled, each shard under the instance uses the same node specifications.  Therefore, the overall performance of the instance = number of shards x performance corresponding to respective shard specifications (including memory, bandwidth, connection count, and QPS value). For more information on specifications, refer to [Instance specifications](https://docs.byteplus.com/en/docs/redis/product-specification). |
|Number of nodes per shard |Each shard in Cache for Redis supports the use of two to six nodes, with one being the primary node and the rest being secondary nodes. You can determine the required number of nodes based on the following two factors:<br><br><br>* Availability requirements: The greater the number of nodes, the more guaranteed the availability of the instance.<br><br>* The amount of service read and write requests: If the load of service read requests is high, you can choose a larger number of nodes and enable read/write splitting for instance to distribute read requests across multiple secondary nodes to expand read capacity.<br><br>   * Both types of Redis instances (sharding cluster enabled and disabled) support the setting of read/write splitting. With read/write splitting, you can send write requests to the primary node for processing while all read requests are processed by the secondary nodes, improving the overall read/write performance of the Redis instance.<br><br>   * When data is synchronized from the primary node to the secondary node, there will be a time lag of a certain length. Therefore, the read/write splitting function is not suitable for services with high data consistency requirements. For more details, refer to [Setting read/write splitting](https://docs.byteplus.com/en/docs/redis/set-read-write-splitting). |
