---
title: "Guide to addressing abnormal performance caused by excessive databases and collections"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/troubleshooting_guide_to_excessive_databases_and_collections"
---

An excessive number of databases or collections (tables) in MongoDB instances can lead to performance issues such as increased database request latency, backup anomalies, and replication lag. This topic provides a comprehensive guide from issue diagnosis to optimization solutions, helping you select the appropriate optimization strategy based on your business characteristics and ensuring stable instance operation under high\-concurrency scenarios.

<span id="8FtdKbXy"></span>
## Performance issues caused by excessive databases and collections

When there are too many databases and collections in MongoDB, both instance operation and daily maintenance will encounter severe performance bottlenecks.


|Problem category |Problem phenomenon |Impact description |
|---|---|---|
|Impaired instance stability<br><br> |Request latency spikes |Even for simple queries like `count`, extremely high `handleLock` or `schemaLock` wait times appear in `timeWaitingMicros`, generating a large number of slow logs. |
||Slow instance startup and failure recovery |WiredTiger needs to scan, verify, and load massive metadata one by one, significantly increasing service startup time and prolonging business interruption. |
||Replication lag increased |Numerous file operations consume I/O, affecting oplog replication and replay efficiency. |
|Reduced operational reliability |Severe timeout or frequent failure of backup and recovery |Too many underlying files can cause physical backups to time out or run out of memory (OOM) when creating memory snapshots, resulting in longer backup and recovery times or frequent task failures. |
||OOM risk during horizontal scaling |During the initial sync phase of a newly added node, a full set of dhandles must be established. Excessive databases and collections can easily exhaust memory and trigger OOM. |


<span id="neMCSUSp"></span>
## Root cause diagnosis

<span id="56ABzgF8"></span>
### Root cause

WiredTiger is MongoDB's default storage engine, which creates separate disk files for each collection and each independent index, and maintains a dhandle (Data handle) data structure in memory, including checkpoint information, session reference counts, B+ tree pointers, and statistics. When the number of dhandle becomes excessive, lock contention (`handleLock` or `schemaLock`) within the engine intensifies significantly, leading to increased request latency and potentially triggering instance\-level operational anomalies.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">An excessive number of databases and collections does not necessarily cause problems. Whether performance is affected depends closely on factors such as workload and access patterns. The pressure from numerous databases and collections differs greatly between systems where access is highly concentrated on a few hot tables (for example, accounting software) and systems where nearly all tables are accessed (for example, multi\-tenant SaaS platforms).</div>


<span id="5uWUIZpt"></span>
### Quick diagnosis

You can use the following commands to quickly obtain an overview of the instance's database and collection distribution (including total number of databases and collections, indexes, data volume).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The maximum number of collections allowed in a MongoDB instance varies by version and specification. If the total number of databases and collections within a single replica set reaches <strong>tens of thousands</strong>, we recommend you pay close attention and refer to this solution for timely optimization. For more details, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/product-limit">Constraints and limits</a>.</div>


* <div data-tips="true" data-tips-type="default">For more details about the commands below, refer to <a href="https://www.mongodb.com/docs/v8.0/reference/command/listdatabases/">listDatabases</a> and <a href="https://www.mongodb.com/docs/v8.0/reference/method/db.getsiblingdb/">db.getSiblingDB()</a>.</div>



```JavaScript
/* View total number of databases in the instance */
db.adminCommand("listDatabases").databases.length

/* View total number of collections in a specified database */
db.getSiblingDB("<database_name>").getCollectionNames().length

/* View global statistics of a specified database (number of collections, number of indexes, total data size and so on) */
db.getSiblingDB("<database_name>").stats()

/* View detailed statistics of a specified collection (number of documents, document size, number of indexes and so on) */
db.getSiblingDB("<database_name>").<collection_name>.stats()
```


Additionally, you can further diagnose whether performance issues caused by excessive databases and collections exist by analyzing the `timeWaitingMicros` field in slow logs.

The following is an example of a slow log query record from an instance: a `count` operation on an order status collection containing only 5 documents took over 120 seconds. The `schemaLock` wait time was as high as 120,045,600 microseconds (approximately 120 seconds), while the actual data scan time was less than 5 milliseconds. This is a typical sign of lock contention caused by an excessive number of databases and collections.

```Plain Text
2026-03-23T10:45:12.123+0800 I COMMAND [conn889900] command ec_order_db.order_status command: count {
    count: "order_status",
    query: {
        tenant_id: "T001",
        status: "PAID"
    }
}
planSummary: COLLSCAN
keysExamined: 0
docsExamined: 5
numYields: 2
locks: {
    ReplicationStateTransition: { acquireCount: { w: 2 } },
    Global: { acquireCount: { r: 2 } },
    Database: { acquireCount: { r: 2 } },
    Collection: { acquireCount: { r: 2 } }
}
storage: {
    timeWaitingMicros: {
        handleLock: 85,
        schemaLock: 120045600
    }
}
protocol: op_query 120050ms
```


<span id="tFvwGu9w"></span>
## Optimization principles

When optimizing performance issues caused by excessive databases and collections, we recommend following these principles:


* Set easonable database and collection threshold

   The maximum number of collections allowed in a MongoDB instance varies by version and specification. To ensure stable instance operation, it is recommended that **the total number of databases and collections in a single replica set not exceed 10,000**. If the number of indexes in a single collection exceeds 15, this threshold should be adjusted downward accordingly. For more details, refer to [Constraints and limits](https://docs.byteplus.com/en/docs/mongodb/product-limit).

* It is strongly recommended to **avoid directly executing ** **`dropDatabase`** ** command to delete large databases**

   After executing [dropDatabase](https://www.mongodb.com/docs/manual/reference/command/dropDatabase/) command, the WiredTiger storage engine asynchronously cleans up all files, deleting the metadata and physical files of the collections to be cleaned one by one. This operation continuously consumes I/O, causing replication lag to increase, which in turn triggers the [flowControl](https://www.mongodb.com/docs/v8.0/reference/command/serverStatus/#hedgingmetrics) mechanism, limiting the write speed on the primary node and potentially affecting all write operations with `writeConcern: majority`.

   To delete a database, you can try the following alternatives:

   1. Perform [db.collection.drop()](https://www.mongodb.com/docs/v8.0/reference/method/db.collection.drop/) on collections in batches at reasonable intervals, and then execute the `dropDatabase` operation after all collections have been cleared.

   2. Migrate data from databases and collections that need to be retained to a new instance with [Data Transmission Service (DTS)](https://docs.byteplus.com/en/docs/DTS/about_database_transmission_service), and delete old instance after thoroughly verifying data.


<span id="tXPemE4V"></span>
## Optimization solutions

The following table summarizes optimization solutions for addressing excessive databases and collections in different scenarios. Before implementing optimization, use it to evaluate your business characteristics, complexity, and required changes to select the most suitable solution.


|Optimization solutions |Applicable scenarios |Operation complexity |Business refactoring item |
|---|---|---|---|
|[Clearing stale data](https://docs.byteplus.com/en/docs/mongodb/troubleshooting_guide_to_excessive_databases_and_collections#kLIWOac7) |The instance contains historical test data, expired business data, or excessive indexes. Reduce the number of databases and collections by dropping unused collections and redundant indexes. |Low |No modification needed. |
|[Restructuring collection structure](https://docs.byteplus.com/en/docs/mongodb/troubleshooting_guide_to_excessive_databases_and_collections#qXZcwZvc) |Consolidate data from multiple collections into a single collection based on specific dimensions (such as date and region), reducing the number of collections by integrating discrete collection structures. |Medium |* Add distinguishing fields.<br><br>* Refactor read/write logic.<br><br>* Migrate existing data. |
|[Splitting instance](https://docs.byteplus.com/en/docs/mongodb/troubleshooting_guide_to_excessive_databases_and_collections#mqR8AVSL) |Multiple unrelated businesses share one instance, or business dimensions (such as priority or business lines) can be easily separated. Physically split the instance based on collection distribution, with corresponding adjustments to business logic and access methods. |Medium |* Define business data boundaries.<br><br>* Change instance access address.<br><br>* Migrate existing data. |


<span id="kLIWOac7"></span>
### Clearing stale data

If your MongoDB instance contains unused collections (such as historical test data, expired business data) or redundant indexes, you can reduce the number of disk files and corresponding dhandle structures that the WiredTiger storage engine needs to maintain by dropping unused collections or cleaning up redundant indexes, thereby alleviating performance issues caused by excessive collections.


<Tabs>
<Tab zoneid="MPXkbakcqW" title="Delete obsolete collections">
<TabTitle>Delete obsolete collections</TabTitle>

1. Refer to the suggestions in [Quick diagnosis](https://docs.byteplus.com/en/docs/mongodb/troubleshooting_guide_to_excessive_databases_and_collections#5uWUIZpt) and use [listDatabases](https://www.mongodb.com/docs/v8.0/reference/command/listdatabases/) or [db.getSiblingDB()](https://www.mongodb.com/docs/v8.0/reference/method/db.getsiblingdb/) commands to view the number of collections in the database and identify obsolete collections that can be deleted (such as historical archive collections and test collections).

2. Use [db.collection.drop()](https://www.mongodb.com/docs/v8.0/reference/method/db.collection.drop/) command to drop identified unused collections.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Before executing <code>db.collection.drop()</code>, ensure that a full backup is available. For more information on MongoDB backup, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/data_backup">Data backup</a>.   </div>
   


</Tab>
<Tab zoneid="W6Z92WrAC2" title="Remove redundant indexes">
<TabTitle>Remove redundant indexes</TabTitle>

* **Index optimization principles**

   In MongoDB, each independent index corresponds to a separate file. You can refer to the core principles in the following table to optimize indexes.

   
   |**Principle** |**Description** |**Example** |
   |---|---|---|
   |Remove unused indexes |Delete indexes on fields that are never queried by application. |For example, if no queries in the collection involve the `created_by` field, then the corresponding index `{ created_by: 1 }` can be deleted. |
   |Merge prefixes |Drop redundant short indexes covered by compound indexes. |For example, `{ user_id: 1 }` can be covered by the compound index `{ user_id: 1, action_type: 1 }`, so the redundant prefix index `{ user_id: 1 }` can be deleted. |
   |Equality query field order |Field order does not affect the efficiency of equality queries. |For example, `{ city: 1, status: 1 }` and `{ status: 1, city: 1 }` will not affect equality query efficiency, so you can delete indexes with fewer hits. |
   |Range queries adhere to ESR rules |Follow the [ESR](https://www.mongodb.com/docs/manual/tutorial/equality-sort-range-guideline/?bpass=true#the-esr-equality-sort-range-rule) rules (that is, in the order of Equality, Sort, Range) to build compound indexes. |For example, for the query `{ status: "PAID", date: { $gt: "2026-01-01" } } sort: { amount: -1 }`, the optimal index is `{ status: 1, amount: -1, date: 1 }`. |
   

* **Redundant index example**

   MongoDB supports viewing index hit statistics through [$indexStats](https://www.mongodb.com/docs/v8.0/reference/operator/aggregation/indexStats/) aggregation stage. This topic uses the user behavior analysis collection `user_activity` as an example to demonstrate how to identify redundant indexes.

   ```JavaScript
   db.getSiblingDB("ec_user_db").user_activity.aggregate({ "$indexStats": {} })
   ```
   

   Example of a partial return result is as follows.

   ```JavaScript
   [
     ...
     {
       name: 'user_id_1_action_type_1',
       key: { user_id: 1, action_type: 1 },
       host: 'mongo-testhost:27017',
       accesses: { ops: Long('15'), since: ISODate('2026-03-25T12:54:08.176Z') },
       ...
     }
   ]
   ```
   

   The descriptions of the key fields in the returned results are as follows.

   
   |**Field** |**Description** |
   |---|---|
   |`name` |Index name. |
   |`key` |Index key and sorting information. |
   |`accesses.ops` |The total number of times the index was hit.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Instance restarts or index rebuilds will reset the <code>accesses.ops</code> and <code>accesses.since</code> fields.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If <code>accesses.ops</code> remains 0 or an extremely small value for a long period, the index is most likely redundant and can be considered for removal.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If you are using MongoDB 4.4 or later version, it is recommended that you hide the index first using <a href="https://www.mongodb.com/docs/v8.0/reference/method/db.collection.hideIndex/">db.collection.hideIndex()</a> command before dropping it. After observing that there are no issues with your business for a period of time, you can then proceed to remove the index permanently using <a href="https://www.mongodb.com/docs/v8.0/reference/method/db.collection.dropIndex/">db.collection.dropIndex()</a> command. For more information about hidden indexes, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/mongodb-4-4-features?lang=zh#.6ZqQ6JeP57Si5byV77yIaGlkZGVuLWluZGV4ZXPvvIk=">Hidden indexes</a>.</div><br> |
   |`accesses.since` |Statistics start time. |
   


</Tab>
</Tabs>


<span id="qXZcwZvc"></span>
### Restructuring collection structure

You can consolidate data from multiple collections into a single collection based on business dimensions (such as date or region) to reduce the number of collections.

For example, in a multi\-tenant e\-commerce SaaS system, an initial design created separate collections for operation logs per tenant per day (such as `logs.T001_20260323` and `logs.T001_20260324`). As the number of tenants and the runtime increased, the number of collections grew linearly, and cross\-day trend queries became difficult to perform. The following example shows a comparison of collection structures before and after optimization.


<Tabs>
<Tab zoneid="Ij9Nnotguw" title="Unoptimized (Multiple collections)">
<TabTitle>Unoptimized (Multiple collections)</TabTitle>

```JavaScript
/* Collection logs.T001_20260323 */
{ "_id": 1, "ts": "2026-03-23T10:00:00Z", "event": "LOGIN", "ip": "10.1.2.3" }
{ "_id": 2, "ts": "2026-03-23T10:05:22Z", "event": "PURCHASE", "amount": 299.00 }

/* Collection logs.T001_20260324 */
{ "_id": 1, "ts": "2026-03-24T09:11:05Z", "event": "LOGIN", "ip": "10.1.5.8" }
```



</Tab>
<Tab zoneid="sBRLdh4siq" title="Optimized (Unified collection)">
<TabTitle>Optimized (Unified collection)</TabTitle>

```JavaScript
/* Unified collection logs.main, aggregating by "tenant + date" in the _id */
  "_id": { "tenant_id": "T001", "date": "2026-03-23" },
  "events": [
    { "ts": "2026-03-23T10:00:00Z", "event": "LOGIN", "ip": "10.1.2.3" },
    { "ts": "2026-03-23T10:05:22Z", "event": "PURCHASE", "amount": 299.00 }
  ]
},
{
  "_id": { "tenant_id": "T001", "date": "2026-03-24" },
  "events": [
    { "ts": "2026-03-24T09:11:05Z", "event": "LOGIN", "ip": "10.1.5.8" }
  ]
}
```



</Tab>
</Tabs>


After consolidating multiple distributed collections into a single unified collection:


* The number of collections is significantly reduced, from a set of discrete collections that grew continuously with the number of tenants and days, to a single unified collection.

* The default `_id` index can support precise queries by `tenant + date` without requiring additional indexes.

* Cross\-day queries no longer require `$lookup` for joins across collections, as they can be performed by filtering directly within the single collection.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If you are using MongoDB version 5.0 or later and your business data has strong time\-series characteristics, you may also consider using time series collections to address these issues. Time series collections improve application performance for building and running time series data while reducing disk usage for data and indexes, enabling better performance and greater scale. For more details, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/mongodb-5-features?lang=zh#.5Y6f55Sf5pSv5oyB5pe25bqP5pWw5o2u">Time series collections</a>.</div>


<span id="mqR8AVSL"></span>
### Splitting instance

When collection restructuring cannot reduce the number of databases and collections in a single instance, you can physically split the instance based on collection distribution while making corresponding adjustments at the application layer.


<Tabs>
<Tab zoneid="GnbG8x7WzG" title="Splitting solution">
<TabTitle>Splitting solution</TabTitle>

You can choose an appropriate splitting solution based on the distribution scenario of collections.


|**Collection distribution scenario** |**Splitting solution** |**Description** |
|---|---|---|
|Collections distributed across multiple databases |Database\-level migration |Evaluate the business correlation between databases. If the correlation is low (for example, multiple independent applications sharing one instance), use DTS migrate peripheral business databases to new instance for physical isolation. For specific procedures, refer to [Migrating from BytePlus MongoDB to BytePlus MongoDB](https://docs.byteplus.com/en/docs/mongodb/bp-mongodb-to-bp-mongodb).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When configuring DTS task, select <strong>databases</strong> as migration objects.</div><br><br><br>* <div data-tips="true" data-tips-type="default">After the migration is complete and data consistency is verified, execute <a href="https://www.mongodb.com/docs/manual/reference/command/dropDatabase/">dropDatabase</a> command on the source instance to delete the corresponding <strong>database</strong> and promptly release metadata memory.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If you need to migrate from a replica set instance to a sharding cluster instance, set an appropriate shard key for the sharding cluster instance based on business characteristics. For more suggestions on the use of the sharding cluster instances, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/ug-for-sharding-cluster">User guide for MongoDB sharding cluster</a>.</div><br> |
|Collections concentrated in single database |Collection\-level migration |Vertically split large databases by business dimensions (such as business modules, tenant levels, and data timeliness), and migrate high\-load collections to separate instances. For specific procedures, refer to [Migrating from BytePlus MongoDB to BytePlus MongoDB](https://docs.byteplus.com/en/docs/mongodb/bp-mongodb-to-bp-mongodb).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When configuring DTS task, select <strong>collections</strong> as migration objects.</div><br><br><br>* <div data-tips="true" data-tips-type="default">After the migration is complete and data consistency is verified, execute <a href="https://www.mongodb.com/docs/v8.0/reference/method/db.collection.drop/">db.collection.drop()</a> command on the source instance to delete corresponding <strong>collection</strong>, and promptly release metadata memory.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Before splitting, assess the consistency requirements for cross\-database transactions, and refactor related query logic at the application layer if necessary.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If you need to migrate from a replica set instance to a sharding cluster instance, set an appropriate shard key for the sharding cluster instance based on business characteristics. For more suggestions on the use of the sharding cluster instances, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/ug-for-sharding-cluster">User guide for MongoDB sharding cluster</a>.</div><br> |



</Tab>
<Tab zoneid="rK0Q4q2BLE" title="Splitting example">
<TabTitle>Splitting example</TabTitle>

A chain catering platform provides ordering, cashier, and inventory management services to tens of thousands of brands nationwide. In its initial design, the platform adopted a "one brand, one database" data model. With a significant increase in the number of onboarded brands, instance\-level `schemaLock` contention became increasingly severe. During peak lunch hours, the engine had to frequently switch between a large number of dhandles, causing API response latency for simple operations such as scanning and placing orders to rise sharply, and even leading to frequent instance restarts due to OOM.

To address these issues, the business team developed the following splitting strategy based on brand scale and business value:


* Core brand isolation: Identified the top 5% of core brands that contributed 80% of the total traffic, and migrated their corresponding databases to dedicated, high\-specification MongoDB instances using DTS.

* Geographical grouping for small and medium\-sized stores: Grouped the remaining 95% of small and medium\-sized brands by geographic location, and split their corresponding databases into MongoDB instances deployed in the corresponding regions.


Benefits achieved after the splitting:


* **Performance improvement**: Metadata lock contention on the original instance was significantly reduced, and API response latency during peak hours dropped substantially.

* **Enhanced stability**: The impact scope of a single instance failure was narrowed from all brands to a localized region, significantly improving overall system availability.

* **Cost optimization**: Differentiated node specifications were configured for instances based on their workload types, effectively reducing resource redundancy costs while addressing performance issues.


</Tab>
</Tabs>
