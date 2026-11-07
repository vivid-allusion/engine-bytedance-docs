---
title: "Pre-check items (Document Database for MongoDB)"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/consumption_checkpoint_items_mongodb"
---

Database Transmission Service (DTS) performs various checks on databases before creating or configuring migration or synchronization tasks for Document Database for MongoDB. This topic introduces the details of check items.


|**Item** |**Database type** |**Check scope** |**Level** |**Check content** |**Remarks** |
|---|---|---|---|---|---|
|Existence check of source synchronization objects |Source database |* All migrations<br><br>* All synchronization |Warning |Check whether the source synchronization objects exist. |None |
|Environment detection. |None |* All migrations<br><br>* All synchronization |Warning |Environment detection. |None |
|Database connection and architecture wildcard rule check |* Source database<br><br>* Target database |* All migrations<br><br>* All synchronization |Warning |Database and schema wildcard rule check. |None |
|Source and target databases connectivity check |* Source database<br><br>* Target database |* All migrations<br><br>* All synchronization |Error |Check whether the data transmission server can connect to the source database and the target database. |None |
|Source database Oplog check |Source database |* All migrations<br><br>* All synchronization |Error |Check whether the source database has enabled Oplog. |To perform incremental migration or synchronization, the source end must enable Oplog. |
|Source database account privileges check |Source database |* Incremental migration<br><br>* Incremental synchronization |Warning |Check whether the source database's account privileges meet the requirements for migration or synchronization. |Replica set: Check if the account has serverStatus privileges during incremental migration or incremental synchronization. |
|||* All migrations<br><br>* All synchronization |||Sharded cluster: Check whether the account has listShards privileges during migration or synchronization. |
|Database version check |* Source database<br><br>* Target database |* All migrations<br><br>* All synchronization |Error |Check whether the database version of the source database or target database is Document Database for MongoDB 3.6 or later. |None |
|Target database account privileges check |Target database |* All migrations<br><br>* All synchronization |Error |Check whether the account privileges of the target database meet the requirements for migration or synchronization. |The target database account has the following privileges:<br><br><br>* `find`<br><br>* `remove`<br><br>* `insert`<br><br>* `update`<br><br>* `createCollection`<br><br>* `createIndex`<br><br>* `dropCollection`<br><br>* `dropIndex`<br><br>* `dropDatabase`<br><br>* `listCollections`<br><br>* `listIndexes` |
|Primary node check |Target database |* All migrations<br><br>* All synchronization |Error |When the Document Database for MongoDB database uses a replica set architecture, check whether the source address includes the primary node address. |None |
|Architecture migration check |* Source database<br><br>* Target database |* All migrations<br><br>* All synchronization |Warning |Check whether the architecture of the source database and the target database is compatible. |None |
|Check the versions of the source and destination |* Source database<br><br>* Target database |* All migrations<br><br>* All synchronization |Warning |Check whether the Document Database for MongoDB source and target versions are compatible. |None |
|Source end mongos connection check |Source database |* All migrations<br><br>* All synchronization |Warning |Check whether the source Document Database for MongoDB sharding address is correct. |None |
|Destination mongos connection check |Target database |* All migrations<br><br>* All synchronization |Warning |Check whether the target Document Database for MongoDB sharding address is correct. |None |
|Check tables in the same instance and database on the source and target ends |* Source database<br><br>* Target database |* All migrations<br><br>* <br><br><br>Unidirectional synchronization |Warning |Check whether the source and target ends are the same instance and database & table. |None |
|Target collection existence |Target database |* All migrations<br><br>* All synchronization |Warning |Check whether the target collection exists at the destination.<br><br> |* In schema migration scenarios, if the target collection already exists, it will not be migrated. This may result in data inconsistency between the source and target collections.<br><br>* In non\-schema migration scenarios (including data synchronization), if the target collection does not exist at the destination, DTS automatically creates a target collection at the destination with only the _id primary key, which may affect normal business operations. |
|Millisecond\-level latency monitoring availability check<br><br> |Source database<br><br> |MongoDB to MongoDB synchronization |Error |Check the availability of millisecond\-level latency monitoring for the source database.<br><br> |If the pre\-check fails, you might encounter the source database account lacking root, readWriteAnyDatabase, dbAdminAnyDatabase, and cloudAdmin privileges. If you encounter the above error messages, modify the corresponding issues based on the prompts. For detailed operations, refer to [what to do if enabling millisecond-level latency monitoring pre-check fails?](https://docs.byteplus.com/en/docs/DTS/Why_is_a_heartbeat_table_required_when_enabling_millisecond-level_latency_monitoring?lang=en). |
|Shard key consistency check |* Source database<br><br>* Target database |* All migrations<br><br>* All synchronization |Warning |Check whether the shard key configuration of the source end and destination is consistent. |None |
