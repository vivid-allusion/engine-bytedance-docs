---
title: "Constraints and limits (Redis)"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/limits_redis_as_source_database"
---

This topic outlines the supported databases and limits when the target database for migration or synchronization is Cache for Redis, for example, the BytePlus Cache for Redis or self\-managed Cache for Redis.

<span id=".5pSv5oyB55qE5pWw5o2u5bqT"></span>
## Supported databases


|**Source database** |**Target database** |**Supported versions** |**Migration type** |**Synchronization type** |
|---|---|---|---|---|
|* BytePlus Cache for Redis<br><br>* Redis connected over public network<br><br>* 	<br><br><br>Redis connected over express network |* BytePlus Cache for Redis<br><br>* Redis connected over public network<br><br>* 	<br><br><br>Redis connected over express network |* Redis 4.0<br><br>* Redis 5.0<br><br>* Redis 6.0<br><br>* Redis 7.0 |* Full migration<br><br>* Incremental migration |* Full initialization<br><br>* Incremental synchronization |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When you create a synchronization task, only BytePlus Cache for Redis is currently supported for selection.</div>


* <div data-tips="true" data-tips-type="tip">If you need to migrate the data of Alibaba Cloud's cloud\-native memory database Tair to the BytePlus Cache for Redis, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> for technical support.</div>



<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


|**Type** |**Description** |
|---|---|
|Source database limits |* Bandwidth requirements: Adequate egress bandwidth is required on the source database server. Failure to meet this prerequisite will lead to suboptimal migration performance.<br><br>* During full data migration or initialization, DTS consumes certain read/write resources on both the source and target databases, which may lead to an increased load on the database servers. When database workload is high or server specifications are insufficient, it can increase pressure on the database and even lead to service unavailability. It is recommended to perform data migration or synchronization during off\-peak hours. You can also increase the parameter value of the` client-output-buffer-limit` of the source database.<br><br>* When certain keys in the source database use an expiration (`expire`) policy, a situation may arise where expired keys are not deleted promptly. This can result in the target database appearing to have fewer Keys (e.g., when checked via the `info` command) than the source.<br><br>* When horizontal scaling (e.g., increasing or decreasing the number of shards) or vertical scaling (e.g., upgrading or downgrading node specifications) occurs, you need to re\-configure the task. To ensure data consistency, it is recommended to clear the data that has already been migrated or synchronized to the target Cache for Redis before reconfiguring the task.<br><br>* Because the single\-node instance of Cache for Redis does not have AOF persistence enabled, it can not be migrated or synchronized using DTS.<br><br>* If the connection address of the source database changes during a migration or synchronization task, it will result in task failure, and you must reconfigure the task. If it still fails, you can [submit a ticket](https://console.byteplus.com/workorder/create/) for technical support. If it is not processed for a long time, the source database will reset the AOF file.<br><br>* The target database account used for data migration or synchronization must have permissions to execute write commands. |
|Other limits |* Due to added conflict resolution logic in Redis bidirectional synchronization, it currently only supports bidirectional synchronization between Volcengine Redis instances.<br><br>* Two\-way synchronization does not solve the CRDT problem. You need to ensure that there are no operations on the same Key in the source and target databases.<br><br>* It is recommended that the source and target Cache for Redis databases be the same version, or migrate from a lower version to a higher one to ensure compatibility. If you migrate from a higher version to a lower version, there may be database compatibility or data loss issues.<br><br>* In the event of a transient connection failure on the source or target instance, a full data re\-migration or re\-synchronization may be triggered, potentially leading to data inconsistency.<br><br>* During incremental data migration or synchronization, DTS cannot confirm the execution success of Lua scripts called via `EVAL` or `EVALSHA`, as the target database does not explicitly return execution results for scripts.<br><br>* The storage space of the target Cache for Redis database must be greater than the storage space occupied by the source Cache for Redis database.<br><br>* When DTS calls the `psync` and `sync` commands to transmit data, it will overwrite the data in the target database. That is, if the same Key exists in the target database, a `del` operation will be performed first.<br><br>* The self\-managed Cache for Redis database needs to support the open source Psync protocol. |
|Special cases |* If the target database's data eviction policy parameter `maxmemory-policy` is configured to a value other than `noeviction`, it may cause the target database's data to be inconsistent with the source database.<br><br>* During the execution of a migration or synchronization task, restarting the database or switching to the primary may cause the migration or synchronization to fail. |
