---
title: "Application scenarios"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/application_scenarios"
---

This topic describes the common application scenarios of Cache for Redis.


* The business requires high real\-time data and read/write performance and it is sensitive to data latency.

   > A single Redis shard can provide more than 100,000 QPS. The latency of PCT99 is within 2 ms.   
   

* Certain partition fault tolerance is required, but strong data consistency is not required.

   > Final consistency can be achieved between primary and secondary nodes of Redis.   
   

* Transaction needs are low, but the need for storage and scalability of weak data structures is high.

   > Redis has weak transaction support. It is a storage based on KV models.   
   

* The flux data for a single request is not large. The data model is not complex.

   > Redis requires that a single value of String data cannot exceed 512 MiB. For non\-String data (such as Hash, Set, Zset, List, and others), the maximum element length is 8,192 and the maximum value length is 1 MiB. It is suitable for scenarios where the data volume of a single request is not large or the data model is not complex.
