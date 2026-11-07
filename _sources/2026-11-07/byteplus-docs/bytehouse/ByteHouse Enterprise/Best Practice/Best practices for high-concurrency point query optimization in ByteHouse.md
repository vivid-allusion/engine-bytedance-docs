---
title: "Best practices for high-concurrency point query optimization in ByteHouse"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/high-concurrency-point-query-optimization"
---

<span id="4ab63100"></span>
# Applicable scenarios

In many data analysis scenarios for online services, such as game log retrieval, real\-time user information queries, and so on, business teams need to provide high\-performance query interfaces for multiple analysis services based on similar SQL templates (SQL Pattern). A common characteristic of these scenarios is that they impose extremely stringent requirements on **QPS (queries per second) and query latency (latency)** , and that they expect the system to have **excellent linear scalability**, that is, query performance can increase in sync with the increase in computing resources.

<span id="805596c2"></span>
# Key features of ByteHouse for high\-concurrency point queries

From a theoretical perspective, an analytical database that excels in high\-concurrency point query scenarios must have its core capabilities built upon the following six key technical foundations:


1. **The query optimizer estimates accurately**

   Based on RBO/CBO and real\-time statistics, the system reliably generates the most efficient and concise execution plan for each query request, eliminating any redundant data scanning and computation at the source.

2. **The computing engine is sufficiently lightweight**

   SQL point queries are generally not particularly complex, so the compute engine must be able to construct and schedule execution pipelines with minimal overhead, ensuring that on\-CPU performance hotspots are focused on the actual computation logic.

3. **Metadata concurrency control is sufficiently lightweight**

   High\-concurrency point query scenarios can also place significant pressure from concurrent access on metadata systems, which are commonly Context or Catalog. Therefore, it is necessary to adopt a lock\-free or lightweight lock design when accessing metadata, in order to eliminate lock contention and waiting bottlenecks under high concurrency and to avoid some off\-CPU performance hotspots.

4. **The data read by the storage engine is small enough**

   By using techniques such as data clustering and indexing, the amount of data physically read approaches the amount required for computation, reducing the effect of read amplification.

5. **Core data and indexes are always resident in memory**

   Core data and index structures should reside in memory caches, such as PageCache or BufferPool, to minimize the impact of time\-consuming disk I/O.

6. **Predictable linear scalability**

   In high\-concurrency scenarios, query throughput (QPS) must scale linearly with the increase in the number of compute replicas.


To address these core features, the ByteHouse team has designed and implemented the following several optimization measures.


|Areas for optimization |Note |
|---|---|
|Prepared Statement |It supports pre\-registering query templates to avoid the overhead of analyzing and optimizing SQL templates. |
|Context lock |Optimizing the engine's context lock can improve CPU utilization. |
|Sync pulling pipeline |You can enable it by using `Settings use_sync_pipeline_executor = 1` in the query, which controls the engine's execution mode. After this feature is enabled, using sync mode can improve CPU utilization. |
|Table scan pipeline |You can enable it by using `Settings enable_table_scan_build_pipeline_optimization = 1` in the query. This optimizes pipeline construction overhead for tablescan and can improve CPU utilization. |
|Adjust index_granularity |You can configure `Settings index_granularity = 1024` in the query. This parameter adjusts the number of rows in a mark. In point query scenarios, less data will be accessed, which can improve QPS. |


<span id="7adb0398"></span>
# Usage restrictions

Before use, please ensure that your engine version is higher than v2.6. In the ByteHouse Enterprise Edition console, go to the **Cluster management** page, click the **Cluster name**, and view the engine version.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06b95fa90ac4490d827b1c4402c86343~tplv-goo7wpa0wc-image.image) </span>

<span id="d2d362e8"></span>
# Storage engine and index optimization

<span id="2e68282e"></span>
## Table creation best practices

When creating tables using the MergeTree family of table engines, you can significantly optimize point query performance under high concurrency by adjusting **MergeTree\-level settings**. The following recommended parameters are provided for your reference:

```SQL
CREATE TABLE t1
(
    `id`         UInt64,
    `event_time` DateTime,
    `city`       String,
    `category`   String,
    `amount`     UInt32
)
ENGINE = HaUniqueMergeTree('/clickhouse/default/t1/{shard}', '{replica}')
PARTITION BY toDate(event_time)
ORDER BY (city, category)
UNIQUE KEY id
SETTINGS
    index_granularity                   = 128,
    index_granularity_bytes             = 0,
    enable_disk_based_unique_key_index  = 0,
    load_index_granule_caches           = 1,
    merge_selector_config               = '{
        "name": "dance",
        "max_parts_to_merge_base": 25,
        "min_parts_to_merge_base": 3,
        "min_parts_to_enable_multi_selection": 10
    }';
```


<span id="48ceb4db"></span>
## Description of optimization items

<span id="8ff849fa"></span>
### Use the HaUniqueMergeTree table engine

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip"><strong>Core advantages</strong>: HaUniqueMergeTree supports real\-time data updates and deletions based on the unique key (<code>UNIQUE KEY union_id</code>), addressing pain points in the community edition and greatly simplifying the development of real\-time analytics applications.</div>


* <div data-tips="true" data-tips-type="tip"><strong>Performance overview</strong>: Query performance is nearly equivalent to the standard <code>MergeTree</code>, while single\-shard write throughput can exceed 100,000 rows per second.</div>



HaUniqueMergeTree is a self\-developed table engine by ByteHouse. It retains the high query performance of ClickHouse and also supports primary key updates. It addresses the pain point of the ClickHouse community edition not supporting efficient update operations, helping businesses develop real\-time analytics applications more easily.

The HaUniqueMergeTree engine has the following features:


* You can configure a unique key (UNIQUE KEY), which provides upsert semantics for updating and writing, and automatically returns the latest value for each unique key during queries.

* Performance: Single\-shard write throughput typically reaches over 100,000 rows per second, and query performance is nearly identical to that of the HaMergeTree table.

* The unique key can be set with multiple fields and expressions, and currently supports up to three fields.

* It supports partition\-level and table\-level unique key modes.

* It supports custom version fields; data with a lower version is automatically ignored when written.

* It supports multi\-replica deployment; data reliability is ensured through asynchronous replication between primary and standby instances;

* It supports real\-time data deletion based on UNIQUE KEY.


For more information about HaUniqueMergeTree and its usage details, please refer to [HaUniqueMergeTree](https://docs.byteplus.com/docs/bytehouse/hauniquemergetree).

<span id="6ae44a49"></span>
### **Index granularity optimization**

`index_granularity` is an important concept in the MergeTree table engine of ClickHouse. It defines the interval at which data is marked for indexing. Table data is marked into multiple small intervals based on the `index_granularity` (default is 8192), with each interval containing up to 8192 rows. After marking each interval, a Mark (MarkRange) is created, with the specific range of the MarkRange indicated by its start and end. Data files are also generated as compressed data blocks according to the `index_granularity` interval granularity.

If significant read amplification is detected, you can try lowering this parameter from its baseline value to 1024 or below. It is recommended that you set it to 128. By increasing the density of index markers, the engine is able to locate data more precisely.

Lowering `index_granularity` may result in some loss, because a finer index means:


* **Larger index size**: The index file increases in size because it contains more tags.

* **Slower data merge speed**: The background merge process needs to handle more index markers, which consumes more resources.


However, in **high\-concurrency, read\-intensive point query scenarios**, query latency is the primary optimization target. Therefore, sacrificing some write and merge performance in exchange for a substantial improvement in read performance is a completely reasonable and efficient optimization choice.

Note: Also, **the table's**`index_granularity` **parameter cannot be modified once it is set**.

At the same time, it is recommended that you set `index_granularity_bytes=0`, disable Adaptive Mark, set the Mark size to a fixed value, and reduce the computational overhead of Mark positioning.

<span id="ecf0fa72"></span>
### Maintain and build the index cache in memory


* **Maintain an in\-memory key index for the unique key of** `HaUniqueMergeTree`

   Set `enable_disk_based_unique_key_index = 0`.

   
   |Parameters |Default value |Configuration instructions |
   |---|---|---|
   |enable_disk_based_unique_key_index |Default value: 1 |0：in\-memory mode. In this mode, the system maintains an in\-memory key index for each table with a unique key, so the amount of data that can be supported is limited by memory.<br><br>1：disk\-based mode. In this mode, there is no limit on the amount of data, but performance is 10% to 30% lower than the in\-memory approach. The more frequently data is inserted, the greater the reduction in import speed.<br><br>Recommended option: When `the total data volume is less than (100 million × number of cluster shards) records`, choose in\-memory mode; in other scenarios, choose disk\-based mode. |
   

* **Create an in\-memory index cache**

   During data import and node reload, set `load_index_granule_caches = 1` to proactively build index caches for each data partition (Part) and load them into memory, ensuring that indexes do not need to be read from disk during queries.

   When executing a query, you need to add the query\-level setting: `enable_skip_index_cache` to use the constructed cache.

   
   |Parameters |Recommended value |Configuration instructions |
   |---|---|---|
   |load_index_granule_caches |true |Specifies whether to build a cache when importing or reloading the table; the default is false. |
   


<span id="faf37b8c"></span>
### Create separate indexes for commonly used query keys


* **For numeric and date columns: use the** `minmax`**index for range pruning**

   When the `WHERE` clause of a query involves this column (for example, `WHERE price > 100` or `WHERE event_date = '2023-10-26'`), the ByteHouse engine first checks the `minmax` index. If the `[min, max]` range of a granule does not overlap at all with the query condition, the engine can **safely and completely skip reading all data from this data granule**.

   ```SQL
   INDEX number_minmax_idx number TYPE minmax GRANULARITY 1
   ```
   

   Primary and sort keys include this feature by default, but you can manually add a `minmax` index to any other numeric, date, or datetime columns that are commonly used in queries to improve their performance under filtering conditions.

* **For high\-radix numeric string columns, use** `Bloom filter`**index for existence checks**

   A Bloom filter allows efficient membership testing for set members, but there is a slight risk of false positives. In index usage scenarios, false positives are not a critical issue; their only impact is that a small number of unnecessary data blocks will be read additionally.

   For query keys of string type, a bloomfilter index can be created to better support scenarios with high\-cardinality string columns.

   ```Bash
   INDEX string_bf_idx string_idx TYPE bloom_filter(0.0001) GRANULARITY 1
   ```
   

   `bloom_filter(0.0001)`: The parameter `0.0001` (that is, 0.01%) represents the expected false positive rate. The smaller the value, the more accurate the index, but it also uses more space.


For more details about the index, see [HaUniqueMergeTree](https://docs.byteplus.com/docs/bytehouse/hauniquemergetree).

<span id="437ab7a4"></span>
### **Part merge strategy optimizations**

In ClickHouse, each row write operation creates a new partition directory according to the part naming rules (called **part**). This means that even if the data belongs to the same partition, it will not be directly added to the existing partition directory.

The MergeTree table parameter **merge_selector_config** can optimize data merge strategies, control the number of partitions and the scale of merges, and reduce the number of partitions scanned during queries.


|**Sub\-parameters** |**Function** |**Recommended value** |
|---|---|---|
|name |Select a merge algorithm; dance is suitable for vector data distribution and balances write and query performance. |"dance" |
|max_parts_to_merge_base |The maximum number of partitions that can be merged in a single operation, to prevent excessive merging from causing write blocking. |25 |
|min_parts_to_merge_base |The minimum number of partitions required to trigger a merge, to prevent small partitions from persisting and increasing scan overhead. |1 |
|max_total_rows_to_merge |Maximum number of rows per merge to avoid building excessively large indexes. |20000000 |
|max_parts_to_break |When the number of partitions exceeds this threshold, the built\-in policy will attempt to proactively split large partitions in order to maintain a balance between query performance and merge efficiency. |10000 |
|enable_heuristic_to_align_parts |Disable heuristic alignment, simplify merge logic, and reduce merge time. |0 (Disabled) |


Therefore, we recommend adding the following parameters. **After data import is complete, by means of active background merging**, **it is ensured that the data can ultimately be consolidated into a single**, **optimized Part**, reducing read amplification caused by an excessive number of Parts.

```SQL
merge_selector_config = '{"name": "dance",  "max_parts_to_merge_base": 25,  "min_parts_to_merge_base": 1,  "min_parts_to_enable_multi_selection": 10}'
```


<span id="f14a89bb"></span>
# Computing engine optimization

After optimizing the table engine, we also fine\-tuned the compute engine to maximize CPU utilization and concurrent processing capability.

<span id="1bfdd1eb"></span>
## Configure the Config.xml

For high\-concurrency point queries, it is recommended to optimize the following server\-side configurations via `config.xml`. For details on how to modify configuration parameters, see [Modify configuration parameters](https://docs.byteplus.com/docs/bytehouse/modify-configuration-parameters).

```XML
<enable_use_local_lock>1</enable_use_local_lock>
<max_concurrent_queries>20000</max_concurrent_queries> 
```



|**Parameters** |**Function** |**Recommended values** |
|---|---|---|
|enable_use_local_lock |By downgrading some global locks to local locks, the system reduces the contention and waiting that occur when high\-concurrency queries access metadata, directly improving concurrent throughput. |1 (Enable it) |
|vector_index_cache_size |It is used to reduce the number of concurrent operations. |20000 |
|uncompressed_cache_size |Cache size for storing decompressed data. Ensure that hot data blocks remain in memory. |Adjust this value according to the machine's memory size |
|mark_cache_size |The cache size used by the mark index should be configured to ensure that the index for hot data resides in memory whenever possible. |Adjust this value according to the machine's memory size |


<span id="78da2f3a"></span>
## Configure User.xml

Create a Profile in User.xml for high\-concurrency point queries. For details on modifying configuration parameters, please refer to [Modify configuration parameters](https://docs.byteplus.com/docs/bytehouse/modify-configuration-parameters).

```XML
<settings>
    <log_queries_min_type>QUERY_FINISH</log_queries_min_type>
    <max_threads>1</max_threads>
    <exchange_source_pipeline_threads>1</exchange_source_pipeline_threads>
    <enable_plan_cache>true</enable_plan_cache>
    <optimize_skip_unused_shards>true</optimize_skip_unused_shards>
    <enable_table_scan_build_pipeline_optimization>true</enable_table_scan_build_pipeline_optimization>
    <use_sync_pipeline_executor>true</use_sync_pipeline_executor>
    <enable_mark_bitmap_index>false</enable_mark_bitmap_index>
    <enable_short_circuit>true</enable_short_circuit>
</settings> 
```



|Configuration item name |Function |Recommended value |
|---|---|---|
|log_queries_min_type |The minimal type of log for query_log, used to restrict which entries are included in query_log. |QUERY_FINISH |
|max_threads |In high\-concurrency point query scenarios, each query runs in a single thread to reduce the performance overhead caused by thread contention. |1 |
|exchange_source_pipeline_threads |Configure the number of threads for the exchange operator to read data. |1 |
|enable_plan_cache |Enable the plan cache to reduce the cost incurred by the execution engine when building plans. |true |
|optimize_skip_unused_shards |Enable when data is partitioned by sharding_key. When filtering by sharding_key in a SELECT query, optimize by skipping unused shards. |true |
|enable_table_scan_build_pipeline_optimization |Reduce the pipeline construction overhead of the TableScan operator to further improve CPU utilization. |true |
|use_sync_pipeline_executor |Point queries use a synchronous execution mode to reduce the overhead of asynchronous scheduling and thread switching, improving CPU utilization. |true |
|enable_mark_bitmap_index |When coverage is high, avoid using only the unique key index to read the mark, as this can result in false positives. |false |
|enable_short_circuit |TopN shortest path evaluation is used to optimize the execution of Boolean expressions. If the result is determined, the remaining expressions are not evaluated. |true |


<span id="ada56f97"></span>
## Use prepared statement (PREPARED STATEMENT)

A prepared statement (`PREPARED STATEMENT`) is used to efficiently execute the same or similar SQL statements repeatedly. It sends an SQL template (containing the placeholder `?`) to the database for one\-time precompilation (parsing and optimization), eliminating the overhead of repeated parsing and optimization on the server side. For more details about this feature, see [Preprocessing query PREPARED STATEMENT](https://docs.byteplus.com/docs/bytehouse/preprocessing-query-prepared-statement).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Currently, <code>PREPARED STATEMENT</code> only supports SQL with a fixed number of parameters.</div>


Usage examples are as follows:

```SQL
CREATE PERMANENT PREPARED STATEMENT prep1
AS
SELECT count() 
FROM (SELECT number FROM system.numbers LIMIT 10)
WHERE number < [literal_name: DataType]; 

CREATE PERMANENT PREPARED STATEMENT prep1 AS
SELECT count()
FROM (SELECT number FROM system.numbers LIMIT 10)
WHERE number < [i: UInt32];  
```
