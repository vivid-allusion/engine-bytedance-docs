---
title: "Best practice: Avoid read-write inconsistencies"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/best-practice-avoid-read-write-inconsistencies"
---

ByteHouse is a distributed database, its default behavior does not consider read\-write consistency, **data between copies will reach eventual consistency after a period of time**. This article will introduce the factors causing read\-write inconsistencies in ByteHouse and the best practice configurations in scenarios like data processing, to help users better handle read\-write consistency issues while using ByteHouse.

<span id="6c0364b9"></span>
# Reasons for data inconsistencies

The default writing behavior of ByteHouse is asynchronous writing; data is split according to the shard key after being written to the distributed table, and is then asynchronously written to the appropriate copy (usually the Leader copy) within the shard, which will then synchronize the data to another copy in the same shard.

When reading from the distributed table, the distributed table will find the suitable copy in each shard (data delay can be up to 120s, adjustable by the user Param `max_replica_delay_for_distributed_queries`). Therefore, data written to the ByteHouse cluster cannot be read immediately for the following common reasons:


* Distributed writing latency: Data backlog in the written distributed table, due to cluster load factors, asynchronous writing to local tables is very slow.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c6dc74ddf39f4725b325e226497d4809~tplv-goo7wpa0wc-image.image) </span>

* Primary\-backup latency: Input successfully written to a node’s Local table is very slow to sync to the Local table of the other async copy within the same shard due to cluster load factors. (If there is only one copy, then this factor does not exist.)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/51a0334c015648829b0c0565d58aefd4~tplv-goo7wpa0wc-image.image) </span>

* Other reasons. For example:

   * Distributed DDL Latency: Partial distributed DDL timeout resulting in data inconsistency.

   * Write latency: Data delay caused by the default long batch time.


<span id="4fcfb085"></span>
# Best practice configuration

In scenarios such as Data Processing, if the data to be written needs to be read immediately, you can set it up according to the following guidelines. But as this is not the default behaviour of ByteHouse, pay attention to the risks of such operations.

<span id="1d0d839c"></span>
## Avoid inconsistencies caused by distributed asynchronous insertion

Change the default asynchronous behaviour to synchronous, so that the waiting insert SQL will return only after the insertion is successful at all copies.

```XML
<!-- User parameter -->
<insert_distributed_sync>true<insert_distributed_sync>
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This operation will cause the insertion to slow down, and batching execution will not be performed, which may increase the burden of Merge.</div>


<span id="361ff5c4"></span>
## Avoid inconsistencies caused by _copy synchronization

<span id="72bf90c7"></span>
### Single _copy

The simplest solution to completely avoid inconsistencies caused by _copy synchronization is to use a single _copy.

Of course, the single _copy solution will be Not available when the cluster encounters a single node failure, requiring a balance of availability, data reliability and consistency, then deciding whether to use single _copy.

<span id="6d9e8cdc"></span>
### Dual _copy

Under dual _copy, the behaviour of different engines is inconsistent, Please follow the selected engine to adjust How to use.

<span id="75ef1b89"></span>
#### HaMergeTree

HaMergeTree does not distinguish between Leader and not Leader; By setting, it allows inserting and searching to select nodes in order, achieving immediate readability of written data.

```XML
<!-- User parameter -->
<load_balancing>in_order</load_balancing>
```


But, the Cost of this operation is that another _copy cannot be sent to Search, existing only as a backup node, and both CPU and memory will be wasted. Suggestion to specify `in_order` Search only in data verification scenes; In other cases, still Search by Default value `random`.

<span id="2d100f63"></span>
#### HaUniqueMergeTree

To achieve deduplication, HaUniqueMergeTree uses table\-level leaders and non\-leaders, where only the leader writes and deduplicates data. Therefore, by adding settings when creating the table, you can ensure that reading from the distributed table always accesses only the leader table.

```SQL
Create Table ...
Engine=HaUniqueTable ...
Settings ha_unique_read_session_consistency = true;
```


<span id="ca6056f4"></span>
## Avoid inconsistencies caused by DDL

When Sent distributed DDL (on cluster) to a node to Create, Alter, Delete, or Truncate, the node will Wait for all nodes to successfully run the DDL before returning Success. However, distributed DDL has a Timeout, and will continue to Run after the timeout expires.

If there's a need to wait for previous steps like table creation and data cleanup in the data link, it's suggested to cancel the timeout Time:

```XML
<!-- User parameter -->
<distributed_ddl_task_timeout>0</distributed_ddl_task_timeout>
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Distributed DDL is a queue; it may take a long time when the Cluster is busy.</div>


<span id="621fc89d"></span>
## Avoid inconsistencies caused by insertions

<span id="261e9925"></span>
### Insert Into insertion

The INSERT INTO syntax of ByteHouse maintains atomicity. It only returns success if all data is inserted successfully. If any data fails to insert, it returns a failure, and once written successfully, the data is immediately committed to disk and becomes instantly retrievable at the current node.

Therefore, under any circumstances, insertion is guaranteed with a retry mechanism, allowing immediately readability of the written data.

<span id="dc4362c0"></span>
### Kafka

The reason why data is not immediately visible after being consumed by Kafka, besides performance reasons causing an upstream data delay, is the background batch accumulation mechanism.

If you wish to reduce data latency, consider reducing the batch accumulation time (default is 8000, or 8 seconds).

```SQL
ALTER TABLE db.kafka_table MODIFY SETTING stream_flush_interval_ms = 1000;
```


However, it is advised to maintain at least one second and pay attention to monitoring metrics such as inode to avoid system merge burden due to overly fragmented files.

<span id="bcd29283"></span>
### Flink

Similar to Kafka, to reduce data latency, you can also reduce the batch accumulation time through settings.

The suggestion is consistent with Kafka's: maintain at least one second.

```SQL
CREATE TABLE lookup_table (
  ...
) WITH (
  'connector' = 'bytehouse-ce',
  ...
  'sink.buffer-flush.interval' = '1 second'
);
```


<span id="052f9553"></span>
## Common solutions to local table conflicts

<span id="66ba523e"></span>
### Inconsistent ZooKeeper path

Rebuild the table with a DROP operation based on the nodes with more data. If the DROP table contains data, data loss will occur. Example SQL is as follows:

```SQL
DROP TABLE default.sync_cluster_node_test_local SYNC;

CREATE TABLE IF NOT EXISTS default.sync_cluster_node_test_local (`id` UInt64, `name` String) ENGINE = HaMergeTree('/clickhouse/2100775944/bytehouse_cluster_2o8k/default.sync_cluster_node_test_local_1728997209/{shard}','{replica}') ORDER BY id SETTINGS index_granularity = 8192
```


<span id="086481bd"></span>
### Inconsistent indexes

Manually create and delete indexes to maintain consistency across all nodes.

```SQL
 # Create index
 CREATE INDEX index_name ON my_table (column_name);
 
 # Delete index
 DROP INDEX index_name ON my_table;
```


<span id="ece84390"></span>
### Inconsistent settings

Manually modify the settings to keep them consistent across all nodes.

```SQL
ALTER TABLE my_table MODIFY SETTING index_granularity = 8192;
```


<span id="ed50e9e2"></span>
### Inconsistent comments

Manually change the table's comments to maintain consistency.

```SQL
# Modify table comment
ALTER TABLE my_table COMMENT 'This is the modified table comment';

# Modify table comment
ALTER TABLE my_table MODIFY COLUMN my_column COMMENT 'This is the modified column comment';
```
