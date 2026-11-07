---
title: "Data synchronization"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/data-synchronization"
---

Cache for Redis supports using the Database Transmission Service (DTS) tool to meet data synchronization requirements between different Redis databases under the same BytePlus account.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Database Transmission Service (DTS) is a data stream service that integrates data migration, synchronization, and subscription. It supports data interaction between relational databases, non\-relational databases, and other data sources, reducing the complexity of data flow between databases. DTS helps you easily migrate databases to the cloud without interrupting business operations, effortlessly build high\-availability database disaster recovery architectures through real\-time synchronization channels, and freely consume real\-time incremental data provided by cloud databases according to your own needs. For more information on DTS, refer to [About DTS](https://docs.byteplus.com/en/docs/DTS/about_database_transmission_service).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* When using DTS for data synchronization between Redis databases, specific usage limitations apply to both the source and target databases. For more details, refer to [Limits (Redis as source database)](https://docs.byteplus.com/en/docs/DTS/limits_redis_as_source_database).

* The source database requires `sync`, `psync`, and `config get` privileges; the target database requires read\-write permissions.

* DTS supports multiple data synchronization topologies, but Redis only supports certain data synchronization topologies. For the exact types of topologies supported, refer to [Supported synchronization topologies](https://docs.byteplus.com/en/docs/DTS/synchronizing_to_byteplus_cache_for_redis_redis).

* Only some commands in the source database will be synchronized to the target database. For more information on the commands supported for synchronization, refer to [Supported commands](https://docs.byteplus.com/en/docs/DTS/synchronizing_to_byteplus_cache_for_redis_redis).

* Cache for Redis supports the following two architectures: Primary\-secondary instances and single\-node instances. Single\-node instances do not have data persistence capabilities and do not support any data persistence policies. Therefore, when a single\-node instance is used as the source database for data synchronization, incremental synchronization is not supported.

   For more information on the functional characteristics of primary\-secondary and single\-node instances, refer to [Feature differences](https://docs.byteplus.com/en/docs/redis/feature-faq).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

For more information on how to use About DTS to synchronize data between Redis databases, refer to [Synchronizing BytePlus Redis to another BytePlus Redis](https://docs.byteplus.com/en/docs/DTS/synchronizing_to_byteplus_cache_for_redis_redis).
