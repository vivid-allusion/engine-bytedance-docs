---
title: "Glossary"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/glossary"
---

This topic summarizes the terms related to the instances of Cache for Redis.


|Term |Description |
|---|---|
|Region |The geographical location of the data. For more information on the regions where Redis services are currently available, refer to [Service endpoints](https://docs.byteplus.com/en/docs/redis/request-structure). |
|Availability zones |Abbreviated as AZ. Each region has multiple isolated areas, known as availability zones. |
|Instance |The basic unit for cloud resource management in Cache for Redis. The performances (connections, bandwidth, and others) vary depending on the specifications of the instances. For more information on the instance specifications, refer to [Product specifications](https://docs.byteplus.com/en/docs/redis/product-specification). |
|Server node |A server node is the smallest unit for building an instance of Cache for Redis. For more information on server nodes, refer to [Server node](https://docs.byteplus.com/en/docs/redis/about-redis). |
|Proxy node |The proxy server node for instances of Cache for Redis. It is used to achieve high availability in Redis instances. For more information on proxy nodes, refer to [Proxy node](https://docs.byteplus.com/en/docs/redis/about-redis). |
|Primary node |The primary server node, also known as the read/write node. One shard has one primary node. |
|Secondary node |The secondary server node, also known as the read\-only secondary node. One shard can have up to 5 secondary nodes. |
|Shard |A group consisting of 1 to 6 nodes. If each shard contains 2 or more nodes, one of them acts as the primary node and the others as the secondary nodes. A replication relationship exists between the primary and secondary nodes. |
|Sharding cluster |Cache for Redis supports enabling sharding clusters. One Redis instance can use several shards. Redis instances with sharding cluster disabled have one shard only. |
|Proxy private endpoint |The address to access Redis instances through Virtual Private Cloud (VPC) (for example, when ECS and Redis instances are in the same VPC). This address is the address of the Proxy node. To connect instances through private networks, refer to [Connecting to instance via private address](https://docs.byteplus.com/en/docs/redis/connect-instance-via-private-address). |
|Proxy public endpoint |The address to access Redis instances through the Internet. This address is the address of the Proxy node. To connect instances through public networks, refer to [Connecting to instance via public address.](https://docs.byteplus.com/en/docs/redis/connect-instance-via-public-address) |
|Direct endpoint |Redis instances with sharding cluster enabled support the direct address services. You can directly access the data shards at the instance backend through a direct address (similar to a native architecture that directly connects to the Redis server). When the client first accesses an instance through a direct address, the direct address is resolved to the virtual address of a random data shard and routed to each data shard through the Redis Cluster protocol. To request a direct address, refer to [Applying for direct connection address](https://docs.byteplus.com/en/docs/redis/apply-direct-connection-address). |
|Data flashback |The data flashback of Cache for Redis optimizes the mechanism based on AOF (Append Only File). Perform incremental archiving for AOF to achieve convenient and fast recovery in seconds, streamline operation and maintenance, and use it as a persistent storage engine. |
|Persistence |Persistence refers to writing data to persistent storage, such as solid\-state drive (SSD). For more information, refer to [Redis persistence](https://redis.io/docs/latest/operate/oss_and_stack/management/persistence/). |
|RDB (Redis DataBase) |RDB is the point\-to\-point representation of Redis data in a very compact single file. RDB files are generally used for backup. |
|AOF (Append Only File) |AOF allows appending a file that cannot be overridden. This file persistently records every write operation received by the server. These operations are executed again at server startup to reconstruct the raw dataset. The commands are recorded in the same format as the Redis protocol in an append only manner. The log can be overridden by Redis when the log size is too big. |
|SSL encryption (Secure sockets layer encryption) |SSL is a protocol that encrypts network connections between the transport layer and the application layer. The SSL encryption of Cache for Redis can improve communication data security and ensure data integrity. |
|Big Key |A typical big key contains a large amount of data or a large number of elements, such as members and the number of lists. The criteria for the big keys of Cache for Redis are as follows:<br><br><br>* For String data, it is considered a big key if memory usage exceeds 10 KiB.<br><br>* For non\-String data, it is considered a big key if the number of elements exceeds 5,000.<br><br>   For more information on big keys, refer to [Big key analysis](https://docs.byteplus.com/en/docs/redis/big-key-analysis). |
|Hot key |A hot key is usually much more frequently visited than other keys. The criteria for the hot keys of Cache for Redis are as follows:<br><br>Sample all visits in the database within the query time range (such as 1 day before now). When the sampling times are in the hundreds (such as the 100th or 200th time), if the number of visits to the corresponding key of the sample exceeds 3,000, it is considered a hot key.<br><br>For more information on hot keys, refer to [Hot key analysis](https://docs.byteplus.com/en/docs/redis/hot-key-analysis). |
|Eviction policy |When using Redis as a cache, you can set an eviction policy to evict stale data automatically. For more information, refer to [Eviction policy](https://redis.io/docs/latest/develop/reference/eviction/#eviction-policies). |
