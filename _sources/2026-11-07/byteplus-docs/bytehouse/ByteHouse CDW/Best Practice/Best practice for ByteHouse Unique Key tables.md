---
title: "Best practice for ByteHouse Unique Key tables"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/bytehouse-best-practice-for-unique-key-tables"
---

ByteHouse unique key tables are primarily used to implement upsert functionality. This capability is a unique feature developed by the ByteHouse team which maintains efficient query performance while also supporting unique key updates. It mainly addresses the pain point where open\-source ClickHouse does not support efficient update operations, helping businesses to more easily develop real\-time analytic applications. Users can implement Upsert update semantics by specifying the UNIQUE KEY, with the system automatically returning the latest value for each unique key during queries.

<span id="1461308a"></span>
# Feature overview

A unique key table is a CnchMergeTree table that uses a unique key index (UNIQUE KEY) and has the following characteristics:


* You configure a unique key using UNIQUE KEY, which supports upsert semantics for write operations, and queries automatically return the latest value for each unique key.

* High query performance is maintained even while ensuring real\-time update capability.

* The unique key index (UNIQUE KEY) supports multiple columns and expressions.

* Unique key tables support multiple deduplication granularities, such as partition\-level deduplication, bucket deduplication, and more.

* Supports custom version fields; automatically ignores them when writing data of a lower version.

* Supports real\-time deletion of data based on UNIQUE KEY.

* Supports partial column updates based on the UNIQUE KEY.


For more information about unique key table capabilities, functional logic, and usage restrictions, refer to [Unique Key table](https://docs.byteplus.com/docs/bytehouse/unique-key-table).

<span id="bc77e4c5"></span>
# Table creation guide

<span id="bfb513e4"></span>
## The number of UNIQUE KEYs

It is recommended that the number of UNIQUE KEY fields does not exceed five. If a unique key is formed by a combination of multiple fields, you can use their `toString(sipHash128())` hash as the unique key.

<span id="288fa681"></span>
## Deduplication granularity selection

If deduplication is required, it is recommended to prioritize using **partition\-level deduplication**. Then, based on data volume and write performance requirements (RPS, **record per second**), determine whether bucket deduplication optimization needs to be enabled.

<span id="a8c5dffd"></span>
## Bucket deduplication optimizations

When any of the following situations occurs, it is recommended to enable bucket deduplication optimization:


1. For each deduplication granularity, the data volume exceeds 20 million (20M).

2. At single deduplication granularity, write requests per second exceed 20,000 (20K)/s.


You can enable bucket deduplication optimization by setting the columns required by the **`CLUSTER BY`clause to be a subset of those required by the UNIQUE KEY** when creating a table.

<span id="10aafaa2"></span>
### Bucket quantity selection

<span id="dceb493b"></span>
#### The write side

When the deduplication granularity data volume (before splitting buckets) is m and the required peak RPS is n. Determine the number of buckets using `max{⌈m / 20M⌉, ⌈n / 20K⌉}`. If you need to reserve some margin for data volume or RPS, use `2 * max{⌈m /20M⌉, ⌈n / 20K⌉}` as the number of buckets.

<span id="170e6461"></span>
#### The query side

During a query, parts with the same number of buckets are sent to the same worker node for computation. Therefore, selecting an appropriate number of buckets has a significant impact on queries. The following principles are generally observed:


1. Ensure that the number of buckets is a multiple of the number of workers to guarantee balanced query load.

2. It is not recommended to use a number of buckets that is less than the number of workers, as this will result in load imbalance.


<span id="162a9c87"></span>
#### **Best practices**

After meeting the requirements on the write side, set `write_bucket_num` to `2 * max{⌈m / 20M⌉, ⌈n / 20K⌉}`. The number of buckets can be set based on `write_bucket_num` and the number of workers:


1. When `write_bucket_num` is less than or equal to the number of workers, you can use the number of workers directly. If you consider long\-term horizontal scaling, you can use `number of workers * 2` as the final bucket count.

2. When `write_bucket_num` is greater than the number of workers, round up to the nearest integer multiple of the number of workers to determine the final bucket count.


<span id="7c3d2c4c"></span>
### Bucket expression


1. It is recommended to use the `CLUSTER BY EXPRESSION cityHash64V2(cluster_column) % N INTO N BUCKETS` clause. For specific usage instructions, refer to [Create dynamic partitioned tables](https://docs.byteplus.com/docs/bytehouse/create-statement#b9a1a39f).

2. It is recommended to use **high\-cardinality columns** for `CLUSTER BY` columns; otherwise, **bucket data skew** can easily occur, which can affect write and query performance.


<span id="1f46a81a"></span>
### Recommended configurations for Bucket table parameters

It is recommended to use the following SETTINGS parameters:

```SQL
max_dedup_worker_number = [the pod number of cnch_vw_write], pick_dedup_worker_by_mod = 1, dedup_impl_version = 'dedup_in_txn_commit'
```


A complete example of a table creation command is as follows:

```SQL
CREATE TABLE orders
(
  `event_time` DateTime,
  `product_id` UInt64,
  `city` String,
  `category` String,
  `amount` UInt32,
  `revenue` UInt64
)
ENGINE = CnchMergeTree
PARTITION BY toDate(event_time)
ORDER BY (city, category)
CLUSTER BY EXPRESSION cityHash64V2(product_id) % 6 INTO 6 BUCKETS
UNIQUE KEY product_id
SETTINGS [..., ]max_dedup_worker_number = [cnch_vw_write 的 pod 数], pick_dedup_worker_by_mod = 1, dedup_impl_version = 'dedup_in_txn_commit';
```



|**Parameter name** |**Parameter types** |**Optional values** |**Default value** |**Parameter descriptions** |
|---|---|---|---|---|
|max_dedup_worker_number |UInt64 |Integer |1 |It is recommended that the number of Dedup workers matches the number of pods in the compute group configured by cnch_vw_write. |
|pick_dedup_worker_by_mod |Bool |true/false |false |Dedup worker distribution mode: When the configuration is set to true, the modulo operation based on the total number of nodes in the compute group ensures even distribution. By default, when set to false, distribution is based on hash values and may not be even. |
|dedup_impl_version |DedupImplVersion |dedup_in_write_suffix/<br><br>dedup_in_txn_commit |dedup_in_write_suffix |Deduplication implementation: dedup_in_write_suffix executes deduplication logic at the end of the write phase; dedup_in_txn_commit executes deduplication logic during the transaction pre\-commit phase, which is an optimized version. |


<span id="4a64b172"></span>
# Import data

<span id="2d3f0bec"></span>
## Batch aggregation

ByteHouse is designed to handle large volumes of data, so it is recommended to prioritize batch aggregation upstream whenever possible.

<span id="9f8720ab"></span>
## Non\-deduplication mode

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Non\-deduplication mode is typically used during historical data migration. In formal production environments, <strong>use with caution</strong>, as it may introduce duplicate data issues.</div>


When the data you need to import meets the following two criteria, you can enable import without deduplication at the query level:


1. The imported data itself does not contain duplicate unique keys.

2. There are no duplicate unique keys between the imported data and the historical data.


Use the following parameters to enable non\-deduplicated import at the query level:

```SQL
dedup_key_mode='append', enable_unique_partial_update = 0
```


The complete usage example is as follows:

```SQL
INSERT INTO target_table SELECT * FROM source_table SETTINGS dedup_key_mode='append', enable_unique_partial_update = 0;
```


**Parameter description**


|**Parameter name** |**Parameter types** |**Optional values** |**Default value** |**Parameter descriptions** |
|---|---|---|---|---|
|dedup_key_mode |DedupKeyMode |replace/throw/append/ignore |replace |Set the deduplication mode. Different parameters correspond to different deduplication modes:<br><br><br>* Set replace to upsert mode;<br><br>* 'throw' and 'ignore' modes can only be used outside the staging area. When a duplicate key is encountered, an exception is thrown or the duplicate is ignored.<br><br>* Append mode does not include a deduplication phase. Performance is optimal. |
|enable_unique_partial_update |Bool |true/false |true |Whether to use partial column update mode. Must be used together with a table\-level parameter of the same name; the partial column update mode is enabled **if and only if both this parameter and the table\-level parameter are enabled**. |


<span id="efb1f2be"></span>
## Concurrent writes

If concurrent writes occur during data import, you may **first consider aligning writes at the upper layer according to deduplication granularity.**  If achieving the previous method is difficult, you can enable concurrent write optimization when deduplication becomes a bottleneck. ByteHouse offers better large\-scale deduplication performance by configuring table\-level parameters to enable batch deduplication using background threads.

Table\-level parameter settings are as follows:

```SQL
cloud_enable_staging_area=1, cloud_staging_area_wait_mode='wait_txn_visible'
```


A complete example of a table creation command is as follows:

```SQL
CREATE TABLE orders
(
  `event_time` DateTime,
  `product_id` UInt64,
  `city` String,
  `category` String,
  `amount` UInt32,
  `revenue` UInt64
)
ENGINE = CnchMergeTree
PARTITION BY toDate(event_time)
ORDER BY (city, category)
CLUSTER BY EXPRESSION cityHash64V2(product_id) % 6 INTO 6 BUCKETS
UNIQUE KEY product_id
SETTINGS [..., ]cloud_enable_staging_area=1, cloud_staging_area_wait_mode='wait_txn_visible';
```


**Parameter descriptions**


|**Parameter name** |**Parameter types** |**Optional values** |**Default value** |**Parameter description** |
|---|---|---|---|---|
|cloud_enable_staging_area |Bool |true/false |false |**Whether to enable the staging area** can support optimization scenarios for asynchronous or concurrent writes. |
|cloud_staging_area_wait_mode |StagingAreaWaitMode |no_wait/wait_txn_visible |no_wait |After **enabling the staging area**, the data write mode is enabled. no_wait indicates the **asynchronous write mode**, wait_txn_visible indicates the **synchronous write mode**. |


<span id="c2a73a7b"></span>
## Major ELT tasks

When a single `INSERT SELECT/DELETE/UPDATE` operation affects more than 100 million rows, this task can be considered a large ELT task. ByteHouse supports making full use of multiple worker resources and centralized scheduling of deduplication tasks by setting table\-level and query\-level parameters. An example of parameter settings is as follows:

```SQL
# Table-level parameters
dedup_impl_version = 'dedup_in_txn_commit'

# Query-level parameters
optimize_unique_table_write = 1, max_insert_threads = 8
```


The complete usage example is as follows:


* Table\-level parameter settings

   ```SQL
   CREATE TABLE orders
   (
     `event_time` DateTime,
     `product_id` UInt64,
     `city` String,
     `category` String,
     `amount` UInt32,
     `revenue` UInt64
   )
   ENGINE = CnchMergeTree
   PARTITION BY toDate(event_time)
   ORDER BY (city, category)
   CLUSTER BY EXPRESSION cityHash64V2(product_id) % 6 INTO 6 BUCKETS
   UNIQUE KEY product_id
   SETTINGS [..., ]dedup_impl_version = 'dedup_in_txn_commit';
   ```
   

* Query\-level parameter settings

   ```SQL
   INSERT INTO target_table SELECT * FROM source_table SETTINGS optimize_unique_table_write = 1, max_insert_threads = 8;
   ```
   


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To improve performance, you can increase both <code>min_insert_block_size_bytes</code> and <code>min_insert_block_size_rows</code> at the same time; <strong>you can set them to twice their current values.</strong></div>


* <div data-tips="true" data-tips-type="warning">If you encounter OOM (Out Of Memory) resource issues, you can reduce both <code>min_insert_block_size_bytes</code> and <code>min_insert_block_size_rows</code>; <strong>they can be set to half of their current values.</strong></div>



**Parameter descriptions**


|**Parameter name** |**Parameter types** |**Optional values** |**Default value** |**Parameter descriptions** |
|---|---|---|---|---|
|dedup_impl_version |DedupImplVersion |dedup_in_write_suffix/<br><br>dedup_in_txn_commit |dedup_in_write_suffix |Deduplication implementation: dedup_in_write_suffix executes the deduplication logic at the end of the write phase, while dedup_in_txn_commit executes the deduplication logic during the transaction pre\-commit phase and is the optimized version. |
|optimize_unique_table_write |Bool |true/false |false |It is recommended to enable insert select import optimization for unique key tables only when **the staging area is not enabled** and **dedup_impl_version='dedup_in_txn_commit'** . |
|max_insert_threads |UInt64 |Positive integers |0 |Size of the worker's write thread pool for executing insert select requests |
|min_insert_block_size_bytes |UInt64 |Positive integers |1073710080 |`INSERT SELECT` Minimum size of the batch block |
|min_insert_block_size_rows |UInt64 |Positive integers |1048545 |The minimum number of rows for a `INSERT SELECT` batch block. |


<span id="8c838caa"></span>
## Coexistence of online and offline import

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This feature is currently being gradually rolled out. If you encounter any issues while using it, you can submit a support ticket or contact the ByteHouse team.</div>


When online and offline import tasks coexist, large\-volume offline tasks can severely impact the write latency of real\-time imports, resulting in significant performance fluctuations for the latter. In this scenario, you can enable optimization to resolve the issue. By configuring table\-level parameters and relying on the staging area, deduplication bandwidth can be preferentially allocated to real\-time tasks, thereby reducing the impact of large offline ELT tasks on real\-time write latency.

Example settings for table\-level parameters are as follows:

```SQL
cloud_enable_staging_area=1, cloud_staging_area_wait_mode='wait_txn_visible'，real_time_task_optimize_algo='strict_optimize'
```


The following is a complete example of a table creation command:

```SQL
CREATE TABLE orders
(
  `event_time` DateTime,
  `product_id` UInt64,
  `city` String,
  `category` String,
  `amount` UInt32,
  `revenue` UInt64
)
ENGINE = CnchMergeTree
PARTITION BY toDate(event_time)
ORDER BY (city, category)
CLUSTER BY EXPRESSION cityHash64V2(product_id) % 6 INTO 6 BUCKETS
UNIQUE KEY product_id
SETTINGS [..., ]cloud_enable_staging_area=1, cloud_staging_area_wait_mode='wait_txn_visible'，real_time_task_optimize_algo='strict_optimize';
```


**Parameter description**


|**Parameter name** |**Parameter types** |**Optional values** |**Default value** |**Parameter descriptions** |
|---|---|---|---|---|
|cloud_enable_staging_area |Bool |true/false |false |**Enabling the staging area** can support scenarios optimized for asynchronous or concurrent writes. |
|cloud_staging_area_wait_mode |StagingAreaWaitMode |no_wait/wait_txn_visible |no_wait |After **enabling the staging area**, data write mode. no_wait indicates the **asynchronous write mode**, and wait_txn_visible indicates the **synchronous write mode**. |
|real_time_task_optimize_algo |RealTimeTaskOptimizeAlgo |disabled/strict_optimize/ loose_optimize |disabled |Configure offline/online import optimization algorithms. The effects for different parameter values are as follows:<br><br><br>* 'disabled' indicates that optimization is turned off;<br><br>* The strict_optimize algorithm strictly controls the number of offline tasks and prioritizes the execution of real\-time import tasks.<br><br>* The loose_optimize algorithm executes import tasks with high priority while also improving the performance of offline tasks as much as possible. |


<span id="68fbeed1"></span>
# Examples

<span id="abf9b289"></span>
## Example 1: Partition level unique key

```SQL
-- The engine guarantees the uniqueness of the unique key within a partition by default.
CREATE TABLE t1
(
  `event_time` DateTime,
  `product_id` UInt64,
  `city` String,
  `category` String,
  `amount` UInt32,
  `revenue` UInt64
)
ENGINE = CnchMergeTree
PARTITION BY toDate(event_time)
ORDER BY (city, category)
UNIQUE KEY product_id;

INSERT INTO t1 VALUES
('2020-10-29 23:40:00', 10001, 'Beijing', 'men wear', 5, 500),
('2020-10-29 23:40:00', 10002, 'Beijing', 'men wear', 2, 200),
('2020-10-29 23:40:00', 10003, 'Beijing', 'men wear', 1, 100);

-- Writing data with the same key can achieve an update (with the upsert semantics).
INSERT INTO t1 VALUES
('2020-10-29 23:50:00', 10002, 'Beijing', 'men wear', 4, 400),
('2020-10-29 23:50:00', 10003, 'Beijing', 'men wear', 2, 200),
('2020-10-29 23:50:00', 10004, 'Beijing', 'men wear', 1, 100),
('2020-10-30 00:00:05', 10001, 'Beijing', 'men wear', 1, 100),
('2020-10-30 00:00:05', 10002, 'Beijing', 'men wear', 2, 200);

-- The query automatically returns the latest data for each key.
select * from t1 order by toDate(event_time), product_id;
┌──────────event_time─┬─product_id─┬─city────┬─category─┬─amount─┬─revenue─┐
│ 2020-10-29 23:40:00 │      10001 │ Beijing │ men wear │      5 │     500 │
│ 2020-10-29 23:50:00 │      10002 │ Beijing │ men wear │      4 │     400 │
│ 2020-10-29 23:50:00 │      10003 │ Beijing │ men wear │      2 │     200 │
│ 2020-10-29 23:50:00 │      10004 │ Beijing │ men wear │      1 │     100 │
│ 2020-10-30 00:00:05 │      10001 │ Beijing │ men wear │      1 │     100 │
│ 2020-10-30 00:00:05 │      10002 │ Beijing │ men wear │      2 │     200 │
└─────────────────────┴────────────┴─────────┴──────────┴────────┴─────────┘
```


```SQL
-- UNIQUE KEY can contain multiple fields and expressions.
-- sipHash64 is a fast hash function with a low collision rate. When using sipHash64 as the unique key, the possible hash collisions need to be taken into consideration.
-- sipHash64：https://clickhouse.com/docs/en/sql-reference/functions/hash-functions#siphash64
CREATE TABLE t1m
(
  `event_time` DateTime,
  `product_id` UInt64,
  `city` String,
  `category` String,
  `amount` UInt32,
  `revenue` UInt64
)
ENGINE = CnchMergeTree
PARTITION BY toDate(event_time)
ORDER BY (city, category)
UNIQUE KEY (product_id, sipHash64(city));

INSERT INTO t1m VALUES
('2020-10-29 23:40:00', 10001, 'Beijing', 'men wear', 5, 500),
('2020-10-29 23:40:00', 10002, 'Beijing', 'men wear', 2, 200),
('2020-10-29 23:40:00', 10003, 'Beijing', 'men wear', 1, 100),
('2020-10-29 23:50:00', 10002, 'Shanghai', 'men wear', 4, 400),
('2020-10-29 23:50:00', 10003, 'Beijing', 'men wear', 2, 200),
('2020-10-29 23:50:00', 10004, 'Beijing', 'men wear', 1, 100);

select * from t1m;
┌──────────event_time─┬─product_id─┬─city─────┬─category─┬─amount─┬─revenue─┐
│ 2020-10-29 23:40:00 │      10001 │ Beijing  │ men wear │      5 │     500 │
│ 2020-10-29 23:40:00 │      10002 │ Beijing  │ men wear │      2 │     200 │
│ 2020-10-29 23:50:00 │      10003 │ Beijing  │ men wear │      2 │     200 │
│ 2020-10-29 23:50:00 │      10004 │ Beijing  │ men wear │      1 │     100 │
│ 2020-10-29 23:50:00 │      10002 │ Shanghai │ men wear │      4 │     400 │
└─────────────────────┴────────────┴──────────┴──────────┴────────┴─────────┘
```


<span id="642f2f99"></span>
## Example 2: Custom version fields

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">There are the following restrictions when using version fields:</div>


<div data-tips="true" data-tips-type="tip">When using integers as version fields, it is recommended to use unsigned integers compatible with UInt64.</div>


<div data-tips="true" data-tips-type="tip">Supports time types such as Date and Datetime as version fields.</div>


<div data-tips="true" data-tips-type="tip">Does not support floating\-point types such as Float and Decimal as version fields.</div>


By default, data written with the same unique key will overwrite the existing data. This may lead to the following issues


* When backtracking upstream data, old data may overwrite new data, leading to retrograde results in queried data.

* In a Lambda architecture, if offline and real\-time tasks simultaneously write to a partition, the data retained ultimately depends on the sequence in which the tasks are executed.


To address the above issue, ByteHouse unique key tables support designating a field in the table as a version field. The engine ensures that when writing data with the same key, it will only be overwritten if the data version is \>= the existing version. The version field supports all UInt types and Date/DateTime and cannot be Nullable.

```SQL
-- The parameters within the parentheses of CnchMergeTree are optional version fields.
CREATE TABLE t3
(
  `event_time` DateTime,
  `product_id` UInt64,
  `city` String,
  `category` String,
  `amount` UInt32,
  `revenue` UInt64
)
ENGINE = CnchMergeTree(event_time)
PARTITION BY toDate(event_time)
ORDER BY (city, category)
UNIQUE KEY product_id;

INSERT INTO t3 VALUES
('2020-10-29 23:40:00', 10001, 'Beijing', 'men wear', 5, 500),
('2020-10-29 23:40:00', 10002, 'Beijing', 'men wear', 2, 200),
('2020-10-29 23:50:00', 10001, 'Beijing', 'men wear', 8, 800),
('2020-10-29 23:50:00', 10002, 'Beijing', 'men wear', 5, 500);

-- When tracing back the previous two pieces of data, since the version is less than the existing version, it will be automatically skipped during the writing process.
INSERT INTO t3 VALUES
('2020-10-29 23:40:00', 10001, 'Beijing', 'men wear', 5, 500),
('2020-10-29 23:40:00', 10002, 'Beijing', 'men wear', 2, 200);

-- The versions of 10001 and 10002 have not been rolled back.
select * from t3 order by toDate(event_time), product_id;
┌──────────event_time─┬─product_id─┬─city────┬─category─┬─amount─┬─revenue─┐
│ 2020-10-29 23:50:00 │      10001 │ Beijing │ men wear │      8 │     800 │
│ 2020-10-29 23:50:00 │      10002 │ Beijing │ men wear │      5 │     500 │
└─────────────────────┴────────────┴─────────┴──────────┴────────┴─────────┘

-- Continue to trace back the next two pieces of data and write two pieces of new version data.
INSERT INTO t3 VALUES
('2020-10-29 23:50:00', 10001, 'Beijing', 'men wear', 8, 800),
('2020-10-29 23:50:00', 10002, 'Beijing', 'men wear', 5, 500),
('2020-10-29 23:55:00', 10001, 'Beijing', 'men wear', 10, 1000),
('2020-10-29 23:55:00', 10002, 'Beijing', 'men wear', 7, 700);

-- The query automatically returns the data of the latest version.
select * from t3 order by toDate(event_time), product_id;
┌──────────event_time─┬─product_id─┬─city────┬─category─┬─amount─┬─revenue─┐
│ 2020-10-29 23:55:00 │      10001 │ Beijing │ men wear │     10 │    1000 │
│ 2020-10-29 23:55:00 │      10002 │ Beijing │ men wear │      7 │     700 │
└─────────────────────┴────────────┴─────────┴──────────┴────────┴─────────┘
```


<span id="2bf65463"></span>
## Example 3: Real\-time deletion of data with a specified unique key

In some application scenarios, users want to add a field during INSERT to indicate whether to delete, thereby extending the INSERT semantics.

In ByteHouse unique key tables, each table has an added **reserved field**`_delete_flag_` of type `UInt8`, where 0 indicates data written, non\-0 indicates data deletion. This field cannot be specified during CREATE TABLE nor queried, it can only be specified during INSERT, including INSERT and INSERT SELECT. Furthermore, ByteHouse unique key tables, based on **reserved field**`_delete_flag_`, support the `DELETE FROM` clause.

Usage examples are as follows:


* **INSERT**


```SQL
-- The engine guarantees the uniqueness of the unique key within a partition by default.
CREATE TABLE t5
(
  `event_time` DateTime,
  `product_id` UInt64,
  `city` String,
  `category` String,
  `amount` UInt32,
  `revenue` UInt64
)
ENGINE = CnchMergeTree
PARTITION BY toDate(event_time)
ORDER BY (city, category)
UNIQUE KEY product_id;

INSERT INTO t5 VALUES
('2020-10-29 23:40:00', 10001, 'Beijing', 'men wear', 5, 500),
('2020-10-29 23:40:00', 10002, 'Beijing', 'men wear', 2, 200),
('2020-10-29 23:40:00', 10003, 'Beijing', 'men wear', 1, 100);

-- Specify the deletion field to delete data. When the deletion field is set to a value other than 0, it indicates deletion, and when it is set to 0, it indicates a normal upsert operation.
INSERT INTO t5 (event_time, product_id, city, category, amount, revenue, _delete_flag_) VALUES
('2020-10-29 23:50:00', 10001, 'Beijing', 'men wear', 4, 400, 5),
('2020-10-29 23:50:00', 10002, 'Beijing', 'men wear', 2, 200, 1),
('2020-10-29 23:50:00', 10004, 'Beijing', 'men wear', 1, 100, 0);

-- The query results include a newly added row of data and two rows of old data have been deleted.
select * from t5 order by toDate(event_time), product_id;
┌──────────event_time─┬─product_id─┬─city────┬─category─┬─amount─┬─revenue─┐
│ 2020-10-29 23:40:00 │      10003 │ Beijing │ men wear │      1 │     100 │
│ 2020-10-29 23:50:00 │      10004 │ Beijing │ men wear │      1 │     100 │
└─────────────────────┴────────────┴─────────┴──────────┴────────┴─────────┘
```



* **INSERT WITH VERSION**


```SQL
-- The engine guarantees the uniqueness of the unique key within a partition by default.

-- Specify version
CREATE TABLE t5m
(
  `event_time` DateTime,
  `product_id` UInt64,
  `city` String,
  `category` String,
  `amount` UInt32,
  `revenue` UInt64,
  `version` UInt64
)
ENGINE = CnchMergeTree(version)
PARTITION BY toDate(event_time)
ORDER BY (city, category)
UNIQUE KEY product_id;

INSERT INTO t5m VALUES
('2020-10-29 23:40:00', 10001, 'Beijing', 'men wear', 5, 500, 10),
('2020-10-29 23:40:00', 10002, 'Beijing', 'men wear', 2, 200, 10),
('2020-10-29 23:40:00', 10003, 'Beijing', 'men wear', 1, 100, 10);

-- Specify the deletion field and the version number. If the version number is smaller than the version number of the corresponding row in the query result, the deletion operation will not take effect.
INSERT INTO t5m (event_time, product_id, city, category, amount, revenue, version, _delete_flag_) VALUES
('2020-10-29 23:40:00', 10001, 'Beijing', 'men wear', 4, 400, 5, 1),
('2020-10-29 23:40:00', 10002, 'Beijing', 'men wear', 2, 200, 5, 1),
('2020-10-29 23:40:00', 10003, 'Beijing', 'men wear', 1, 100, 5, 1);

-- The query result remains unchanged, and no data is deleted.
select * from t5m order by toDate(event_time), product_id;
┌──────────event_time─┬─product_id─┬─city────┬─category─┬─amount─┬─revenue─┬─version─┐
│ 2020-10-29 23:40:00 │      10001 │ Beijing │ men wear │      5 │     500 │      10 │
│ 2020-10-29 23:40:00 │      10002 │ Beijing │ men wear │      2 │     200 │      10 │
│ 2020-10-29 23:40:00 │      10003 │ Beijing │ men wear │      1 │     100 │      10 │
└─────────────────────┴────────────┴─────────┴──────────┴────────┴─────────┴─────────┘

-- Specify the deletion field for data deletion. If the version number is not specified or the version number is set to 0, the deletion operation will skip the version check and be executed directly.
INSERT INTO t5m (event_time, product_id, city, category, amount, revenue, _delete_flag_) VALUES
('2020-10-29 23:40:00', 10001, 'Beijing', 'men wear', 4, 400, 1);
INSERT INTO t5m (event_time, product_id, city, category, amount, revenue, version, _delete_flag_) VALUES
('2020-10-29 23:40:00', 10003, 'Beijing', 'men wear', 1, 100, 0, 1);

-- Two rows of old data are deleted from the query result.
select * from t5m order by toDate(event_time), product_id;
┌──────────event_time─┬─product_id─┬─city────┬─category─┬─amount─┬─revenue─┬─version─┐
│ 2020-10-29 23:40:00 │      10002 │ Beijing │ men wear │      2 │     200 │      10 │
└─────────────────────┴────────────┴─────────┴──────────┴────────┴─────────┴─────────┘
```



* **INSERT SELECT**


```SQL
-- The engine guarantees the uniqueness of the unique key within a partition by default.

CREATE TABLE t5x
(
  `event_time` DateTime,
  `product_id` UInt64,
  `city` String,
  `category` String,
  `amount` UInt32,
  `revenue` UInt64
)
ENGINE = CnchMergeTree
PARTITION BY toDate(event_time)
ORDER BY (city, category)
UNIQUE KEY product_id;

INSERT INTO t5x VALUES
('2020-10-29 23:40:00', 10001, 'Beijing', 'men wear', 5, 500),
('2020-10-29 23:40:00', 10002, 'Beijing', 'men wear', 2, 200),
('2020-10-29 23:40:00', 10003, 'Beijing', 'men wear', 1, 100);

-- Delete the data where revenue >= 200 through "INSERT SELECT".
INSERT INTO t5x (event_time, product_id, city, category, amount, revenue, _delete_flag_) SELECT *, 1 as _delete_flag_ from t5x where revenue >= 200;

-- The data where revenue >= 200 has been deleted in the query results.
select * from t5x order by toDate(event_time), product_id;
┌──────────event_time─┬─product_id─┬─city────┬─category─┬─amount─┬─revenue─┐
│ 2020-10-29 23:40:00 │      10003 │ Beijing │ men wear     │      1 │     100 │
└─────────────────────┴────────────┴─────────┴──────────┴────────┴─────────┘
```



* **DELETE FROM**


```SQL
-- The engine guarantees the uniqueness of the unique key within a partition by default.

CREATE TABLE t5y
(
  `event_time` DateTime,
  `product_id` UInt64,
  `city` String,
  `category` String,
  `amount` UInt32,
  `revenue` UInt64
)
ENGINE = CnchMergeTree
PARTITION BY toDate(event_time)
ORDER BY (city, category)
UNIQUE KEY product_id;

INSERT INTO t5y VALUES
('2020-10-29 23:40:00', 10001, 'Beijing', 'men wear', 5, 500),
('2020-10-29 23:40:00', 10002, 'Beijing', 'men wear', 2, 200),
('2020-10-29 23:40:00', 10003, 'Beijing', 'men wear', 1, 100);

-- Delete the data where revenue equals 500 by using the "DELETE FROM" statement.
DELETE FROM t5y WHERE revenue = 500;
-- Delete the data where revenue is greater than or equal to 200 by using the "DELETE FROM" statement.
DELETE FROM t5y WHERE revenue >= 200;

-- The data where revenue is greater than or equal to 200 has been deleted in the query results.
select * from t5y order by toDate(event_time), product_id;
┌──────────event_time─┬─product_id─┬─city────┬─category─┬─amount─┬─revenue─┐
│ 2020-10-29 23:40:00 │      10003 │ Beijing │ men wear │      1 │     100 │
└─────────────────────┴────────────┴─────────┴──────────┴────────┴─────────┘
```


<span id="862ecf5e"></span>
## Example 4: Real\-time update of data with specified unique keys

```SQL
-- The engine guarantees the uniqueness of the unique key within a partition by default.

CREATE TABLE t6
(
  `event_time` DateTime,
  `product_id` UInt64,
  `city` String,
  `category` String,
  `amount` UInt32,
  `revenue` UInt64
)
ENGINE = CnchMergeTree
PARTITION BY toDate(event_time)
ORDER BY (city, category)
UNIQUE KEY product_id;

INSERT INTO t6 VALUES
('2020-10-29 23:40:00', 10001, 'Beijing', 'men wear', 5, 500),
('2020-10-29 23:40:00', 10002, 'Beijing', 'men wear', 2, 200),
('2020-10-29 23:40:00', 10003, 'Beijing', 'men wear', 1, 100);

-- Update through the UPDATE statement.
UPDATE t6 SET amount = 10, revenue = 1000 WHERE event_time = '2020-10-29 23:40:00' and product_id=10001;

-- The data row with the value of 10001 in the query results has been updated and changed through the UPDATE operation.
select * from t6 order by toDate(event_time), product_id;
┌──────────event_time─┬─product_id─┬─city────┬─category─┬─amount─┬─revenue─┐
│ 2020-10-29 23:40:00 │      10001 │ Beijing │ men wear │     10 │    1000 │
│ 2020-10-29 23:40:00 │      10002 │ Beijing │ men wear │      2 │     200 │
│ 2020-10-29 23:40:00 │      10003 │ Beijing │ men wear │      1 │     100 │
└─────────────────────┴────────────┴─────────┴──────────┴────────┴─────────┘

-- Update through the UPDATE statement and use the limit to specify the scope.
UPDATE t6 SET category = concat('新',category) WHERE event_time = '2020-10-29 23:40:00' order by product_id limit 1;

-- Only the data row with the value of 10001 in the query results has been updated and changed through the UPDATE operation.
select * from t6 order by toDate(event_time), product_id;
┌──────────event_time─┬─product_id─┬─city────┬─category─┬─amount─┬─revenue─┐
│ 2020-10-29 23:40:00 │      10001 │ Beijing │ 新men wear   │     10 │    1000 │
│ 2020-10-29 23:40:00 │      10002 │ Beijing │ men wear     │      2 │     200 │
│ 2020-10-29 23:40:00 │      10003 │ Beijing │ men wear     │      1 │     100 │
└─────────────────────┴────────────┴─────────┴──────────┴────────┴─────────┘

-- Swap columns through the UPDATE statement.
UPDATE t6 SET amount=revenue, revenue=amount  WHERE event_time = '2020-10-29 23:40:00';

-- The columns of amount and revenue in the query results have been swapped.
select * from t6 order by toDate(event_time), product_id;
┌──────────event_time─┬─product_id─┬─city────┬─category─┬─amount─┬─revenue─┐
│ 2020-10-29 23:40:00 │      10001 │ Beijing │ 新men wear   │   1000 │      10 │
│ 2020-10-29 23:40:00 │      10002 │ Beijing │ men wear     │    200 │       2 │
│ 2020-10-29 23:40:00 │      10003 │ Beijing │ men wear     │    100 │       1 │
└─────────────────────┴────────────┴─────────┴──────────┴────────┴─────────┘
```


<span id="c3a665b0"></span>
## Example 5: Bucket table

Bucket table is a performance optimization option during table creation in ByteHouse. When using a Bucket table in ByteHouse, the system clusters table data based on one or more columns or expressions provided in the user's table creation statement, placing data with the same value under the same bucket number, thus achieving better performance during query computation.


* **Non\-bucket level unique**


When `enable_bucket_level_unique_keys` is not used to specify bucket level uniqueness. ByteHouse's unique key tables use the table engine\-specified deduplication scope, which defaults to partition\-level uniqueness; hence, there will be no duplicate data in different buckets within the same partition.

```SQL
-- The engine guarantees the uniqueness of the unique key within a partition by default.

CREATE TABLE t7
(
    `d` Date,
    `id` Int32,
    `s` String
)
ENGINE = CnchMergeTree
PARTITION BY d
CLUSTER BY s INTO 10 BUCKETS
ORDER BY s
UNIQUE KEY id;

INSERT INTO t7 VALUES 
('2023-06-26', 1, '1a'), ('2023-06-26', 2, '2a'), ('2023-06-26', 3, '3a'), ('2023-06-26', 3, '3b'), ('2023-06-26', 3, '3c');

select * from t7 order by id;
┌──────────d─┬─id─┬─s──┐
│ 2023-06-26 │  1 │ 1a │
│ 2023-06-26 │  2 │ 2a │
│ 2023-06-26 │  3 │ 3c │
└────────────┴────┴────┘
```



* **Bucket\-level unique**


**When the columns required by cluster by are all included in the unique key fields**, data with the same unique key will definitely fall into a fixed bucket, allowing for optimization through bucket deduplication; at this point, `partition_level_unique_keys` are used to specify the deduplication scope of the bucket (partition level/table level).

Bucket uniqueness can reduce the volume of data needing deduplication, thereby enhancing the write rps and P99 latency; **`enable_bucket_level_unique_keys = 1`** can skip the bucket validation of parts, further improving write efficiency.

```SQL
-- The engine guarantees the uniqueness of the unique key within a partition by default.

CREATE TABLE t7m
(
    `d` Date,
    `id` Int32,
    `s` String
)
ENGINE = CnchMergeTree
PARTITION BY d
CLUSTER BY id INTO 10 BUCKETS
ORDER BY s
UNIQUE KEY id
SETTINGS enable_bucket_level_unique_keys = 1;

INSERT INTO t7m VALUES 
('2023-06-26', 1, '1a'), ('2023-06-26', 2, '2a'), ('2023-06-26', 3, '3a'), ('2023-06-26', 3, '3b'), ('2023-06-26', 3, '3c');

select * from t7m order by id;
┌──────────d─┬─id─┬─s──┐
│ 2023-06-26 │  1 │ 1a │
│ 2023-06-26 │  2 │ 2a │
│ 2023-06-26 │  3 │ 3c │
└────────────┴────┴────┘

INSERT INTO t7m VALUES ('2023-06-26', 3, '3d');

select * from t7m order by id;
┌──────────d─┬─id─┬─s──┐
│ 2023-06-26 │  1 │ 1a │
│ 2023-06-26 │  2 │ 2a │
│ 2023-06-26 │  3 │ 3d │
└────────────┴────┴────┘
```


<span id="6166cef7"></span>
## Example 6: Partial column updates

ByteHouse Cloud Data Warehouse Edition supports partial column update mode.

In the row update mode, default values are used to fill in missing columns. In the column update mode, if the missing columns have original values, they are retained, otherwise, default values are filled in. For more information, refer to [Partial column update](https://docs.byteplus.com/docs/bytehouse/partial-column-update).

<span id="f56633d7"></span>
## Example 7: MySQL DML Benchmarking & dedup_key_mode

ByteHouse unique key tables align with and support various MySQL write modes.


|**MySQL DML semantics** |**MySQL** |**ByteHouse unique key tables** |
|---|---|---|
|**DDL examples** |```SQL```<br>```CREATE TABLE mysql_test (```<br>```  a int NOT NULL,```<br>```  b int DEFAULT NULL,```<br>```  PRIMARY KEY (a)```<br>```) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci```<br> |```SQL```<br>```CREATE TABLE mysql_test(```<br>```    `a` Int32,```<br>```    `b` Nullable(Int32)```<br>```)```<br>```ENGINE = CnchMergeTree```<br>```ORDER BY a```<br>```UNIQUE KEY a```<br> |
|insert into<br><br>Check if the unique key exists; if it does, log an error. |```SQL```<br>```MySQL [db]> insert into mysql_test values (1,1), (1,1);```<br>``````<br>```ERROR 1062 (23000): Duplicate entry '1' for key 'mysql_test.PRIMARY'```<br> |```SQL```<br>```insert into mysql_test FORMAT Values SETTINGS dedup_key_mode='throw' (1,1), (1,1) ;```<br>``````<br>```DB::Exception: Found duplication in the block when insert with setting dedup_key_mode=DedupKeyMode::THROW SQLSTATE: 22000.```<br> |
|insert ignore<br><br>Check if the unique key exists; if it does, ignore the new data being written. |```SQL```<br>```MySQL [db]> insert ignore into mysql_test values (1,1), (1,1);```<br>```Query OK, 1 row affected, 1 warning (0.07 sec)```<br>```Records: 2  Duplicates: 1  Warnings: 1```<br>``````<br>```MySQL [db]> select * from mysql_test;```<br><br><br>```SQL```<br>```┌─a─┬─b─┐```<br>```│ 1 │ 1 │```<br>```└───┴───┘```<br>```1 row in set (0.00 sec)```<br> |```SQL```<br>```insert ignore into mysql_test values (1,1), (1,1) ;```<br>``````<br>```select * from mysql_test```<br>``````<br><br><br>```SQL```<br>```┌─a─┬─b─┐```<br>```│ 1 │ 1 │```<br>```└───┴───┘```<br>```1 rows in set.```<br> |
|replace into<br><br>If a unique key exists, replace it with the written data;<br><br>If a unique key does not exist, the effect is the same as 'insert into'; |```SQL```<br>```MySQL [db]> select * from mysql_test;```<br><br><br>```SQL```<br>```┌─a─┬─b─┐```<br>```│ 1 │ 1 │```<br>```└───┴───┘```<br>```1 rows in set.```<br>```1 row in set (0.00 sec)```<br><br><br>```SQL```<br>```MySQL [db]> replace into mysql_test values (1, 2);```<br><br><br>Query OK, 2 rows affected (0.11 sec)<br><br>```SQL```<br>```MySQL [db]> select * from mysql_test;```<br><br><br>```SQL```<br>```┌─a─┬─b─┐```<br>```│ 1 │ 2 │```<br>```└───┴───┘```<br>```1 rows in set.```<br>```1 row in set (0.00 sec)```<br> |```SQL```<br>```select * from mysql_test```<br><br><br>```SQL```<br>```┌─a─┬─b─┐```<br>```│ 1 │ 1 │```<br>```└───┴───┘```<br>```1 rows in set.```<br><br><br>```SQL```<br>```insert into mysql_test values (1, 2) ;```<br>```select * from mysql_test```<br><br><br>```SQL```<br>```┌─a─┬─b─┐```<br>```│ 1 │ 2 │```<br>```└───┴───┘```<br> |
