---
title: "ByteHouse capacity planning"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/bytehouse-capacity-planning"
---

<span id="d2154cd3"></span>
# CPU usage level

<span id="bd381160"></span>
## Water level suggestion


* **Normal**: Whole cluster CPU usage is less than 80%.

* **Observation**: Whole cluster CPU usage intermittently exceeds 90%, but query write latency shows no significant change.

* **Critical**: Whole cluster CPU usage has continuously exceeded 90%, and query and write latency has increased.


<span id="df28ea92"></span>
## Troubleshooting approach

Prioritize using the SQL diagnosis feature in ByteHouse Enterprise to identify CPU\-intensive SQL statements. For details about the SQL diagnosis feature, see [SQL diagnosis](https://docs.byteplus.com/docs/bytehouse/sql-diagnostic). Then optimize those statements using the following suggestions.

This approach is also applicable to scenarios where memory or IO usage is high. When business traffic increases, prioritize vertical scaling to alleviate resource pressure. For details about vertical scaling operations, see [Vertical scaling](https://docs.byteplus.com/docs/bytehouse/reconfigure-a-cluster#f53340e8).

<span id="67dc59b0"></span>
### SELECT query optimization


* **Reduce scanned data volume**: **WHERE clause best practices**

   * **Partition key filtering**: Always include partition key filters in `WHERE`.

   * **Predicate pushdown**: Ensure that filter conditions can be pushed down to the storage layer. Avoid using non\-monotonic functions on columns in the `WHERE` clause, as this may cause index and partition pruning to fail.


**Recommended**: **Perform a calculation on the value**

```SQL
WHERE event_time >= '2025-08-01 00:00:00' AND event_time < '2025-09-01 00:00:00';
```


**Not recommended**: **Use functions on columns**

```SQL
WHERE toYYYYMM(event_time) > 202508;
```


After partition filtering, the engine can further prune unnecessary Parts by using value filter conditions and minmax information on the Part partition key.


* **Optimize JOIN operation**

   * **JOIN order**: Place the large table on the left side of the `JOIN` clause and the small table on the right side; the engine usually automatically reorders them.

   * **Pre\-filtering before JOIN**: First, use CTE or subqueries to filter and aggregate the tables to be joined, reducing the amount of data to be joined for `JOIN`.


<span id="57e01a5b"></span>
### Table structure design optimization


* **Select an appropriate partition key**

   The partition key is the most important and effective pruning tool in ByteHouse. By specifying filter conditions for partition keys in the `WHERE` clause, ByteHouse can scan only the relevant partitions and skip a large amount of unrelated data.

   **Selection principles**:

   1. **Fields commonly used for query filtering**: Select columns used to filter data in most queries; the most typical examples are date or time fields (such as `dt`, `event_date`).

   2. **Moderate cardinality**: Avoid having too many or too few partitions. Too many partitions (for example, partitioning by seconds) will increase metadata management overhead; too few partitions (for example, partitioning by year) will eliminate the benefits of partition pruning. We generally recommend partitioning by month, week, or day, and keeping the total number of partitions below 100,000.

   3. **Uniform partition granularity**: Ensure the data volume in each partition is roughly balanced to avoid data skew.

      **Example**:

   ```SQL
   -- Create an event table partitioned by day
   CREATE TABLE events (
       event_id String,
       user_id UInt64,
       event_time DateTime,
       -- ... Other columns
   ) ENGINE = CNCHMergeTree
   PARTITION BY toYYYYMMDD(event_time) -- Use date as partition key
   ORDER BY (user_id, event_time);
   ```
   

* **Order Key** **and data distribution**

   The order key determines how data is physically sorted and stored inside each partition. This ordered structure provides two main benefits:

   * **Accelerated filtering**: For range queries on sort columns, ByteHouse can leverage their ordered nature to quickly locate data blocks, similar to the effect of an index.

   * **Improved compression ratio**: When identical values are grouped together, a higher compression ratio can be achieved.

      **Selection principles**:

   1. **High\-frequency filter columns first**: Place the columns most frequently used in `WHERE` conditions at the beginning of the sort key.

   2. **Low cardinality columns first**: Placing columns with lower cardinality (such as `country` and `gender`) before columns with higher cardinality (such as `user_id`) can improve compression effectiveness.

* **Data type selection**

   Selecting the most compact and appropriate data type not only saves storage space, but also improves computational efficiency.

   * **Numeric type**: Use the `UInt` series instead of `Int` (if there are no negative numbers), and select the smallest type that can accommodate the data range, such as using `UInt8` or `UInt16` instead of `UInt64`.

   * **String type**: For strings with limited cardinality, use the `LowCardinality(String)` or `Enum` type to store them using dictionary encoding, which greatly reduces storage and accelerates filtering and aggregation.

   * **Avoid** `****NULL`: Whenever possible, define columns as `NOT NULL`, as `Nullable` columns incur additional storage and calculation overhead.


<span id="d418cd16"></span>
### Use Data Skipping Index

Data Skipping Index is a query acceleration feature supported by ByteHouse. When processing large amounts of data, query performance may decrease due to the need for a full table scan to apply the `WHERE` clause. The Data Skipping Index solves this problem by allowing the query to skip data blocks that are confirmed not to contain matching values.

<span id="d89d8926"></span>
#### Create Data Skipping Index

Four main parameters are involved when creating an index:


1. **Index name**: It serves as the identifier for creating, deleting, or materializing index files.

2. **Index expression**: A formula used to calculate and determine the range of values stored in an index, which may include columns, basic operators, and functions.

3. **Type**: It defines the calculation formula used to skip reading and evaluating each index block.

4. **Granularity**: It defines the number of granules each index block contains. For example, if the primary table index granularity is 8,192 rows and the data skipping index granularity is 4, then each index block will contain 32,768 rows (8,192 x 4).


**Syntax example**

```SQL
/*
Index name: key_i_idx
Index expression: key_i
Type: minmax
Granularity: 1
*/
INDEX key_i_idx key_i TYPE minmax GRANULARITY 1
```


<span id="6dc5a8ff"></span>
#### Supported data types


1. **Min and max values** (**minmax**)

   * **Description**: This is an efficient indexing method that retains the minimum and maximum values of the index expression for each data block. Most effective for columns with loose sorting, this is usually the most cost\-effective index type during query execution.

   * **Limitation**: Applicable only to scalar or tuple expressions, and cannot be used with expressions that generate array or mapping data types.

2. **Dataset** (**Set**)

   * **Description**: This lightweight index contains a parameter `max_size`, which is used to set the size of each block's value set. When `max_size` is 0, the value set size is not limited. It is suitable for columns where each data block contains a small set of unique values.

   * **Cost**: The cost and performance of the index depend on the cardinality within the block. If there are too many unique values, the evaluation cost will become higher; if the value set becomes empty due to exceeding `max_size`, the index will not be applied.

3. **Bloom filter types**

   A Bloom filter is a compact data structure used to determine whether a member exists in a set, which may have a very small false positive rate. In Data Skipping Index, false positives only result in reading some unnecessary blocks.

   * `tokenbf_v1`: Specifically customized for the enhanced Bloom filter feature and applicable to `String` and `FixedString` types. It splits the input expression into a sequence of substrings using non\-alphanumeric characters as delimiters. This index can be used for `LIKE`, `EQUALS`, `in`, and similar operations, and is suitable for searching a small number of specific values in unstructured logs. Its parameters include:

      * Filter size (bytes)

      * Number of hash functions

      * Hash function seed

   * `ngrambf_v1`: The function is similar to `tokenbf_v1`, but adds an extra parameter, which is the size of the `ngram` to be indexed. It is very useful for text search in languages without word boundaries, such as Chinese.

   * `bloom_filter([false_positive])`: General\-purpose Bloom filter, with the `false_positive` parameter (range 0–1, default 0.025) used to specify the false positive probability. It supports multiple data types, including `Int*`, `UInt*`, `Float*`, `String`, `Array`, and more.


<span id="f5fe18b5"></span>
# Memory level

<span id="eda5e825"></span>
## Water level suggestion


* **Normal**: Resident memory is less than 60%, and there are no queries that fail due to memory errors.

* **Observation**: Memory usage remains at 80%.

* **Critical**: Memory usage exceeds 80%, queries frequently report 'Memory limit exceeded' errors, and processes begin to be killed due to out\-of\-memory (OOM) conditions.


<span id="82f923ee"></span>
## Troubleshooting approach

<span id="34402991"></span>
### Resident memory is low, resulting in a query error: memory limit exceeded


1. Refer to the troubleshooting approach in the CPU section, prioritize using SQL Diagnosis to locate SQL statements with high memory usage, and then attempt to optimize them. For details about the SQL Diagnosis feature, see [SQL diagnosis](https://docs.byteplus.com/docs/bytehouse/sql-diagnostic).

2. Use vertical scaling to switch the cluster's computing resources to a 1:8 specification and increase the cluster memory specification. For operation details, refer to [Vertical scaling](https://docs.byteplus.com/docs/bytehouse/reconfigure-a-cluster#f53340e8).


<span id="522fad80"></span>
### Resident memory is high

After enabling the Advanced Diagnosis feature, contact the ByteHouse team for assistance. For details about the Advanced Diagnosis feature, see [Advanced diagnosis](https://docs.byteplus.com/docs/bytehouse/advanced-diagnosis).

<span id="fd211391"></span>
# Disk capacity

After cold storage is enabled for the cluster, we strongly recommend not setting a local storage cap and setting the TTL for moving data to cold storage for each table, to prevent newly written data from directly entering cold storage due to misconfiguration, which could affect the query performance of the entire table. To set the cold storage move TTL operation for a table, see [Create tables using SQL statements.](https://docs.byteplus.com/docs/bytehouse/cold-hot-storage#a49eff51)

<span id="915ffb5c"></span>
## Water level suggestion


* **Normal**: 70%~85%. When cold storage is enabled, at the same time, ensure that disk usage is below the cold storage policy threshold. The threshold value for the default cold storage policy is 100%.

* **Observation**: more than 85% or more than the cold storage policy threshold.

* **Critical**: more than 90%.


<span id="76ab2dfa"></span>
## Troubleshooting approach

Run the following command to locate tables that occupy a lot of space, and based on the query results, determine whether to adjust TTL or expand the disk. For details on TTL usage, refer to [TTL](https://docs.byteplus.com/docs/bytehouse/ttl). For details of the disk expansion operation, see [Vertical scaling](https://docs.byteplus.com/docs/bytehouse/reconfigure-a-cluster#f53340e8).

```SQL
SELECT database, table, formatReadableSize(sum(bytes_on_disk)) AS disk_bytes FROM system.parts WHERE active and disk_name='default' GROUP BY database, table ORDER BY sum(bytes_on_disk);
```


**Special cases**:

If the cluster storage space is small (less than 500G) and the number of tables is large (more than 2000), table metadata may occupy excessive disk space. At this point, it is necessary to modify the cluster parameters through XML, locate the section related to merge_tree, add the following parameters, and restart the cluster to free up excess disk space. For details about modifying cluster parameters, see [Configure cluster parameters](https://docs.byteplus.com/docs/bytehouse/modify-configuration-parameters#aba77abc).

```XML
<merge_tree>
    <manifest_store_keep_log_file_num>1</manifest_store_keep_log_file_num>
<merge_tree>
```


<span id="7acf7c86"></span>
# IO water level

<span id="7bff8022"></span>
## Water level suggestion


* **Normal**: Less than 60%.

* **Observation**: Usage intermittently exceeds 80%.

* **Critical**: Remains more than 80% for 30 Minutes & query write slows down.


<span id="7657df9c"></span>
## Troubleshooting approach


* Refer to the troubleshooting approach in the CPU section. Give priority to using the SQL Diagnosis feature to locate SQL statements with high IO usage, and perform corresponding optimizations. Caution: When using the SQL Diagnosis Feature, pay special attention to whether any SQL statements have performed unexpected data scans. For details about the SQL diagnosis feature, see [SQL diagnosis](https://docs.byteplus.com/docs/bytehouse/sql-diagnostic).

* If query usage is low, confirm whether the cluster has enabled cold storage. If cold storage is enabled and the cluster's storage water level is higher than the cold storage rule, data will frequently be moved from hot storage to cold storage, resulting in increased IO. It is suggested to adjust the TTL or expand disk capacity, and ensure that the storage water level falls below the cold storage rule. Please refer to [TTL](https://docs.byteplus.com/docs/bytehouse/ttl). For activity details for disk expansion, see [Vertical scaling](https://docs.byteplus.com/docs/bytehouse/reconfigure-a-cluster#f53340e8).

* Purchase additional bandwidth to improve overall cluster IO performance. For information on purchasing additional bandwidth, see [Add extra bandwidth](https://docs.byteplus.com/docs/bytehouse/add-extra-bandwidth).
