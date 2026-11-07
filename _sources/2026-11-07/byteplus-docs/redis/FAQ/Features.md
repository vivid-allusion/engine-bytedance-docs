---
title: "Features"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/feature-faq"
---

This topic summarizes the FAQs related to the features of Cache for Redis.

<span id=".57yT5a2Y5pWw5o2u5bqTLXJlZGlzLeeJiOaUr-aMgeivu-WGmeWIhuemu-WQl--8nw=="></span>
### Does Redis support read/write splitting?

Only the primary\-secondary Redis instances support read/write splitting, while the single\-node instances do not support it. For specific procedures, refer to [Setting read/write splitting](https://docs.byteplus.com/en/docs/redis/set-read-write-splitting).

<span id=".5piv5ZCm5pSv5oyB5bCG6K-75YaZ6K-35rGC6YO95LuF5Y-R6YCB6Iez5Li76IqC54K577yf"></span>
### Can I send read and write requests to the primary node only?

All read and write requests are sent to the primary node of Redis by default. The secondary node is for backup. For more details about read/write splitting, refer to [Setting read/write splitting](https://docs.byteplus.com/en/docs/redis/set-read-write-splitting).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The primary\-secondary Redis instances support read/write splitting. Single\-node instances only contain a primary node and do not support read/write splitting. All read and write requests must be sent to the primary node.</div>


<span id=".57yT5a2Y5pWw5o2u5bqTLXJlZGlzLeeJiOmHh-eUqOeahOaVsOaNruaMgeS5heWMluetlueVpeaYr-S7gOS5iO-8nw=="></span>
### What is the data persistence policy used by Redis?

Cache for Redis supports two instance types. Among them:


* AOF persistence policy is enabled for primary\-secondary instances by default.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Each Redis instance supports saving AOF files of the same size as the instance memory. For example, if the instance memory is 1 GiB, up to 1 GiB of AOF files can be saved in the instance and any portion exceeding 1 GiB will be deleted. For more details, refer to <a href="https://docs.byteplus.com/en/docs/redis/quota-and-limit#.5Yqf6IO954m55oCn6ZmQ5Yi2">Constraints and limits</a>.   </div>
   

* Single\-node instances do not have data persistence capabilities and do not support any data persistence policies. For details about the feature differences between the two instance types, refer to [Feature differences](https://docs.byteplus.com/en/docs/redis/feature-faq#.5Li75aSH5a6e5L6L5ZKM5Y2V6IqC54K557G75Z6L5a6e5L6L5pSv5oyB55qE5Yqf6IO954m55oCn5pyJ5L2V5beu5Yir77yf).


<span id=".5Li75LuO5YiH5o2i5pe25Lya5pyJ5LuA5LmI5b2x5ZON77yf"></span>
### What is the impact of failover?

The failover may have following impact:


* The node being switched has a temporary disconnection of a few seconds.

* The node being switched may be not writable briefly (less than 30 seconds), which aims to avoid potential data loss risks caused by failover and data double\-write caused by the DNS cache.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Your application should have an automatic reconnection mechanism and the ability to handle exceptions. If not, the application will prompt an exception message during the failover of an instance, such as <code>READONLY You can't write against a read only replica</code>. For more details about failover, refer to <a href="https://docs.byteplus.com/en/docs/redis/failover">Failover</a>.</div>


* <div data-tips="true" data-tips-type="tip">Only Redis instances of the primary and secondary type support failover, not single node instances.</div>



<span id=".5oWi5pel5b-X5omn6KGM5pe26ZW_55qE6ZiI5YC85piv5aSa5bCR77yf"></span>
### What is the execution time threshold for slow logs?

Cache for Redis supports viewing the slow logs of both server nodes and proxy nodes:


* **Slow log of server node**: The default threshold for execution time is 20 milliseconds. You can change the threshold for execution time through the `slowlog-log-slower-than` parameter. For specific procedures, refer to [Setting instance parameters](https://docs.byteplus.com/en/docs/redis/set-parameter).

* **Slow log of proxy node**: The constant threshold for execution time is 500 milliseconds. You do not need to set any parameters.


For more details, refer to [Querying slow logs](https://docs.byteplus.com/en/docs/redis/query-slow-log).

<span id=".57yT5a2Y5pWw5o2u5bqTLXJlZGlzLeeJiOWPr-S7peS9nOS4uuaVsOaNruW6k-adpeS9v-eUqOWQl--8nw=="></span>
### Can Cache for Redis be used as a database?

Cache for Redis supports persistence. The persistence and primary\-secondary replication of Redis are performed asynchronously, making it unsuitable for applications with high requirements for data reliability and consistency. You can put some data (for example, data with high real\-time requirements) into Redis, which is used as a cache. It is not recommended to use Redis as a database.Cache for Redis is a memory\-based database.

The business load and memory allocator can affect the amount of memory fragments. Excessive memory fragments can lower memory usage. Redis only supports basic data types such as String, List, Set, and ZSet. It does not support Integer, Data, or other commonly used data types. Redis does not support partition, schema, index, or foreign keys. The inlining and connection must be integrated to indirectly achieve multi\-condition queries. It is generally not recommended to use Redis as an independent database.

<span id=".5Li75aSH5a6e5L6L5ZKM5Y2V6IqC54K557G75Z6L5a6e5L6L5pSv5oyB55qE5Yqf6IO954m55oCn5pyJ5L2V5beu5Yir77yf"></span>
### What are the differences in the features supported by primary\-secondary instances and single\-node instances?

Refer to the table below for the differences in the features of single\-node instances and primary\-secondary instances.


|Comparison items |Primary\-secondary instance |Single\-node instance |
|---|---|---|
|Supported node specifications |Supports all node specifications currently on sale. For more details, refer to [Instance specifications](https://docs.byteplus.com/en/docs/redis/product-specification). |Does not support 256 MiB specification. The specifications of other supported nodes are consistent with those of primary\-secondary instances. For more details, refer to [Instance specifications](https://docs.byteplus.com/en/docs/redis/product-specification). |
|Whether enabling shards is supported |Supported. |Supported. |
|Number of nodes supported per shard |2 to 6. |1. |
|Supported |For more details, refer to [Billing items and prices](https://docs.byteplus.com/en/docs/redis/billing-item-price). |The node price is consistent with the node price of a primary\-secondary instance. For more details, refer to [Billing items and prices](https://docs.byteplus.com/en/docs/redis/billing-item-price). |
|Supported features |For details of supported features, refer to [Features](https://docs.byteplus.com/en/docs/redis/features). |Single\-node instances do not support the following features:<br><br><br>* [Backup and recovery](https://docs.byteplus.com/en/docs/redis/backup-and-recovery)<br><br>* [RDB analysis](https://docs.byteplus.com/en/docs/redis/rdb-analysis)<br><br>* Not support changing number of nodes when [modifying instance specifications](https://docs.byteplus.com/en/docs/redis/solutions-for-spec-modification)<br><br>* Not support selecting backup policy when d[eleting instance](https://docs.byteplus.com/en/docs/redis/delete-instance)<br><br>* [Setting read/write splitting](https://docs.byteplus.com/en/docs/redis/set-read-write-splitting)<br><br>* [Settings nearby visit](https://docs.byteplus.com/en/docs/redis/read-local-node-only)<br><br>* [Failover](https://docs.byteplus.com/en/docs/redis/hot-key-analysis)<br><br>* [Multi-availability-zone disaster recovery solution](https://docs.byteplus.com/en/docs/redis/multi-az-solution)<br><br>* Data persistence<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Except for the above features, the features supported by single\-node instances are consistent with those supported by primary\-secondary instances. For more details, refer to <a href="https://docs.byteplus.com/en/docs/redis/features">Features</a>.</div><br> |
|Is SLA applicable? |Yes<br><br>For more details, refer to [SLA for Cache for Redis](https://docs.byteplus.com/en/docs/redis/redis-sla). |No<br><br>For more details, refer to [SLA for Cache for Redis](https://docs.byteplus.com/en/docs/redis/redis-sla). |
