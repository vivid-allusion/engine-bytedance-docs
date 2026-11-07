---
title: "Product architecture"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/product-component-architecture"
---

Cache for Redis currently supports two architectures: enabling and not enabling sharded clusters. Each architecture supports two types of instances: master\-slave and single\-node. This topic introduces detailed information about the product architecture of Cache for Redis.

## Sharding cluster enabled

Redis instances with sharding cluster enabled can use sharded partitions to increase cache capacity and concurrent connections. The architecture deployment and supported capabilities vary depending on the type of Redis instance.

### Primary\-secondary instance

Each shard of a primary\-secondary instance contains one primary node and one to five secondary nodes. The shard itself is invisible externally by default. If the primary node fails in the shard, a secondary node in the same shard will be upgraded to the primary node to continue providing the services. With read/write splitting service, you can send write requests to the primary node for processing while all read requests are processed by the secondary nodes, improving the overall read/write performance of the Redis instance.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3dafa5c51a1b32a3545a656bf0a1ebb3.png)

### Single\-node instance

Each shard of a single\-node instance contains one node. It does not have High Availability (HA) capability, health check, and failover capability. The nodes do not have replication relationships.

When a node fails, the system can activate a new node, but the node data will be lost. The [Service Level Agreement of Cache for Redis](https://docs.byteplus.com/en/docs/redis/redis-sla) is not applicable to single\-node instances.

> **danger**

> Single\-node instances do not support persistence or backup, and cannot guarantee data availability or service continuity. We recommend that you use them only in testing, learning, and other scenarios, and not in production environments.

## Sharding cluster disabled

Redis instances with sharding cluster disabled contain one shard. The architecture deployment and supported capabilities vary depending on the type of Redis instance.

### Primary\-secondary instance

The data of primary and secondary nodes in a shard is always consistent through a real\-time replication mechanism. If the primary node fails, the secondary node automatically upgrades to the primary node. Redis instances with sharding cluster disabled support setting the read/write splitting service. After setting it, you can send write requests to the primary node for processing while all read requests are processed by the secondary nodes, improving the overall read/write performance of the Redis instance.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fddb3f4d3186a4cfa3a37011188ecf9b.png)

### Single\-node instance

Single\-node instances have one node. It does not have High available (HA) capability. It does not support health check and failover capability. The nodes do not have replication relationships.

When a node fails, the system can activate a new node, but the node data will be lost. The [Service Level Agreement of Cache for Redis](https://docs.byteplus.com/en/docs/redis/redis-sla) is not applicable to single\-node instances.

> **danger**

> Single\-node instances do not support persistence or backup, and cannot guarantee data availability or service continuity. We recommend that you use them only in testing, learning, and other scenarios, and not in production environments.
