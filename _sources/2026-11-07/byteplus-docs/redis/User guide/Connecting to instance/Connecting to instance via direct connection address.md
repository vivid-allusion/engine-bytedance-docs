---
title: "Connecting to instance via direct connection address"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/connect-instance-through-direct-connection-address"
---

Cache for Redis supports connecting to instances via a direct address. This topic describes how to access Redis instances via direct connection addresses.

<span id=".5Yqf6IO95LuL57uN"></span>
## Feature introduction

After applying for a direct connection address (that is, enabling direct connection mode), Cache for Redis assigns a unified Virtual IP (VIP) address to all shards in the instance, but each shard uses a different port number. Before the client sends a request to the direct connection address for the first time, it resolves the direct connection address through a DNS server, and the resolution result is the fixed VIP address assigned by Redis. After obtaining the VIP, the client can access data in the Redis instance via the Redis Cluster protocol.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have applied for direct connection address. For specific procedures, refer to [Applying for direct connection address](https://docs.byteplus.com/en/docs/redis/apply-direct-connection-address).

* The client address has been added to the IP allowlist of the Redis instance. For specific procedures, refer to [Setting allowlist](https://docs.byteplus.com/en/docs/redis/create-allowlist).

* The ECS instance where the client resides and the target Redis instance are in the same VPC network.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Only Redis instances with sharing cluster enabled support direct connection addresses. For more details, refer to [Product architecture](https://docs.byteplus.com/en/docs/redis/product-component-architecture).

* Only clients that support the Redis Cluster protocol (such as [Jedis](https://github.com/xetorthio/jedis/wiki/Getting-started), [PhpRedis](https://github.com/phpredis/phpredis), etc.) can access Redis instances through direct connection addresses.

* Due to differences in deployment architecture, unlike instances with sharding clusters disabled, instances with sharding clusters enabled use different native Redis commands. For more information on the commands supported by Redis, refer to [Supported commands](https://docs.byteplus.com/en/docs/redis/supported-command).

* Some Redis Cluster clients do not support the SELECT command; if using such clients, only DB0 can be used.


<span id=".6L-e5o6l5pa55rOV"></span>
## Connection method

For more information on how to access Redis instances using direct addresses via a client, refer to [Connecting to instance via client application](https://docs.byteplus.com/en/docs/redis/connect-instance-via-client).

<span id="xcubfci4"></span>
## FAQs

**Q: How to troubleshoot when a Redis instance connection fails?** 

A: If you are unable to connect to a Redis instance, try the following troubleshooting steps:


   1. Use the [Connection diagnostics](https://docs.byteplus.com/en/docs/redis/Connection_diagnostics) feature to check if the client IP address has been correctly added to the Redis allowlist.

   2. If the diagnosis passes but the connection still cannot be established, further troubleshooting is required. For specific procedures, refer to [What should I do if Redis connection fails](https://docs.byteplus.com/en/docs/redis/what-should-I-do-if-Redis-connection-fails).
