---
title: "ByteHouse CDW query optimization"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/query-optimization-best-practice"
---

<span id="44ac71b7"></span>
# 1. Introduction

<span id="1fe96614"></span>
## 1.1. Purpose and intended audience

This guide aims to provide ByteHouse CDW (Cloud Data Warehouse) users, including data analysts, data engineers, and database administrators (DBA), with a systematic SQL performance optimization framework and practical methods. Whether you are new to ByteHouse or looking to further improve the performance of your existing queries, this guide will provide you with clear and actionable guidance.

The goal is:


* **To build performance awareness**: Helps you understand the key factors that affect SQL query performance and the principles behind ByteHouse.

* **To provide systematic methods**: Provides an end\-to\-end optimization methodology covering performance diagnostics, SQL writing, data model design, and monitoring management.

* **For practical enablement**: Through abundant code examples, scenario\-based analysis, and real\-world cases, you will be able to address actual performance issues encountered in your work.


<span id="7e9102df"></span>
## 1.2. Core concepts of query optimization in ByteHouse CDW


* **Reduce data scanning** (**Reduce Data Scan**): Read as little data as possible. This is the first golden rule of performance optimization. By effectively using partition keys, sort keys, and indexes, full table scans can be avoided by design.

* **Increase computation efficiency**（**Increase computation efficiency**): Optimize the degree of parallelism and efficiency of computation within a distributed computing framework. For example, selecting the optimal JOIN algorithm (such as Broadcast Join), avoiding data skew, and efficiently using aggregate functions, and more.

* **Utilize resources wisely**: Ensure critical tasks have sufficient computing resources by configuring appropriate computing group (Virtual Warehouse, VW) specifications, managing concurrent queries, and optimizing resource queues.

* **Embrace automation**: Make full use of the automation tools provided by ByteHouse, such as automatic statistics collection, to simplify optimization tasks and ensure the accuracy of query plans.


<span id="60243e88"></span>
## 1.3. How to use the guide

This guide is organized in a logical sequence, progressing from basic to advanced, and then to practice.


* [2. ByteHouse CDW Query optimization basics](https://docs.byteplus.com/docs/bytehouse/query-optimization-best-practice#a42ff55b) and [3. Core techniques for SQL optimization](https://docs.byteplus.com/docs/bytehouse/query-optimization-best-practice#db506c32): Explains the fundamental concepts and core technologies of optimization, suitable for all users and designed to establish a solid theoretical foundation.

* [4. Scenario-based optimization practices](https://docs.byteplus.com/docs/bytehouse/query-optimization-best-practice#5b84d20b): Focus on specific business scenarios, provide targeted optimization strategies and case studies, and help you address particular issues.

* [5. Performance monitoring and management](https://docs.byteplus.com/docs/bytehouse/query-optimization-best-practice#0b891107): Introduces performance monitoring and management, suitable for users who require system\-level performance management.


We recommend that you read from beginning to end to build a comprehensive understanding. Experienced users can navigate directly to the sections they are interested in.

<span id="a42ff55b"></span>
# 2. ByteHouse CDW Query optimization basics

<span id="539adf6e"></span>
## 2.1 Quick start for query optimization

<span id="f7f167e0"></span>
### Understand the query lifecycle

The journey of an SQL query in ByteHouse typically consists of the following stages:


1. **Parsing**: When the client submits SQL text, the ByteHouse parser performs lexical and syntactic analysis to generate an abstract syntax tree (AST).

2. **Optimization**: The query optimizer is the core of performance optimization. Based on statistical information, system parameters, and predefined rules, it generates multiple candidate execution plans and selects the plan with the lowest cost from among them.

3. **Execution**: The execution engine carries out specific computational tasks—such as data scanning, filtering, aggregation, and JOIN—on each computing node according to the selected execution plan.

4. **Return**: The final calculation result is returned to the client.


Performance bottlenecks may occur at any stage, but the majority of issues are concentrated in the **execution** phase, while the key to optimization lies in influencing **optimizer** decisions.

<span id="a287a3bf"></span>
### Identify performance bottlenecks: key metrics and tools

Before starting optimization, you must first identify the problem. The following are key performance metrics:


* **Query latency**: The total time from when a query is submitted to when the result is returned.

* **CPU Time**: The total CPU time consumed by all computing nodes for this query.

* **Data scanned**: The size of raw data read by the query.

* **Peak Memory Usage**: The maximum memory consumed during query execution.


**Core tools**:


* **EXPLAIN**: Viewing the logical and physical execution plans of a query is the number one tool for SQL optimization.

* **bh_system.query_log**: It records detailed logs of all executed queries, including all of the performance metrics mentioned above, and is an essential tool for retrospective analysis of performance issues. For details on enabling this feature, refer to [Detailed log (query_log)](https://docs.byteplus.com/docs/bytehouse/sql-audit#60829051).


<span id="7589fd38"></span>
### Optimization examples: a simple journey of slow query optimization

Suppose we have a sales record table `sales` containing the partition key `dt` (date).

**Before optimization:**  A common slow query is forgetting to specify the partition, which results in a full table scan.


* **Performance**: Scanned data volume: 10 TB; scan time: 5 minutes.

   * **Optimized:**  By adding partition key filter conditions, the amount of data scanned can be greatly reduced.

* **Performance**: Scanning 10 GB of data took 3 seconds. This simple example illustrates the core idea of optimization: **read only the necessary data whenever possible**.


**Pre\-optimization SQL**:

```SQL
-- Intent: Query the total sales for yesterday
-- Issue: WHERE dt = ... was not used Attempting to restrict partitions results in a full table scan.
SELECT sum(amount)
FROM sales;
```


**Optimized SQL**:

```SQL
-- Optimize: Precisely specify partitions
SELECT sum(amount)
FROM sales
WHERE dt = '2025-08-24';
```


<span id="3c6b2c6a"></span>
## 2.2 Understand the EXPLAIN execution plan

`EXPLAIN` is a window into understanding how queries are executed. Through it, we can see which execution path the optimizer has chosen for our SQL. For details about the execution plan, see [EXPLAIN statement (EXPLAIN)](https://docs.byteplus.com/docs/bytehouse/explain-statement).

<span id="41f3c5da"></span>
### 2.2.1. How to read and analyze EXPLAIN ANALYZE

In ByteHouse, you can directly obtain the execution plan by adding the EXPLAIN ANALYZE keyword before an SQL statement. You may also append the keywords "Distributed" and "Pipeline" after EXPLAIN ANALYZE.

```SQL
EXPLAIN ANALYZE SELECT ...;
```


The output is a tree structure, read from bottom to top. Each line represents an **operator**, which represents a specific computation step. Indentation represents the parent\-child relationship between operators.

The key to analyzing `EXPLAIN ANALYZE` is:


1. **Focus on low\-level operators**: In particular, `TableScan`, check the number of `partitions` and `rows` it scans to confirm whether unnecessary data is being scanned.

2. **Check the Filter operator**: Verify whether the `WHERE` condition is effectively pushed down to the storage layer, so that data is filtered during scanning.

3. **Analyze join types**: Confirm whether the most efficient `Join` algorithm is used, for example, whether the smaller table is used as the right table.

4. **Find high\-cost operations**: Pay attention to operators that typically consume significant resources, such as `Shuffle`, `Sorting`, and more.


<span id="e7de4be8"></span>
### 2.2.2. Interpretation of key operators


* **TableScan, Filter, Project**

   * `TableScan`: Represents reading data from a table. The key information is the partitions and rows it reads. If the data volume here is much higher than expected, it is usually because partition pruning or indexing was not applied.

   * `Filter`: Applies the filtering conditions in the `WHERE` clause. Ideally, `Filter` should be as close as possible to `TableScan`.

   * `Project`: Corresponds to the `SELECT` list and indicates which columns are selected for output.

* **Join type** (**Broadcast, Shuffle**)

   * `Broadcast Join`: When one table (usually the right table) is small, ByteHouse broadcasts all of its data to all nodes participating in the `Join`. This avoids the redistribution (Shuffle) of data from the left table, resulting in extremely high performance.

   * `Shuffle Join`: When both tables are large, it is necessary to rehash and redistribute the data of both tables based on the `Join Key` (Shuffle), to ensure that rows with the same `Join Key` are distributed to the same node. `Shuffle` generates a large amount of network I/O and is one of the main sources of performance overhead.

   * `Colocation Join`: When the JOIN key matches the bucket key of both the left and right tables, you can use `Colocation Join`.

* **Aggregation**

   * `Aggregation`: Performs `GROUP BY` aggregation operation. ByteHouse performs two\-stage aggregation: first, partial aggregation is carried out on each node, and then the local results are `Shuffle`d to a small number of nodes for final aggregation, in order to improve parallelism.

* **Runtime Filter**

   * Runtime Filter is a key technology used by ByteHouse in `Join` optimization. During the build phase of `Join` (build side, usually the smaller table), a filter is generated based on the `Join Key` and then pushed down to the scan phase of the fact table (probe side, usually the larger table). This allows a large amount of data that cannot possibly match the `Join` condition to be filtered out early when scanning large tables. This greatly reduces the amount of data transfer and computation during the `Join` process. Seeing `Runtime Filter` in `EXPLAIN` usually indicates that `Join` performance will be significantly improved. Depending on the statistics, you can appropriately increase the value of the `wait_runtime_filter_timeout` parameter.


<span id="8343a61e"></span>
### 2.2.3 Identify common problems through EXPLAIN


* **Full table scan**: `TableScan` read all partitions.

* **Predicate pushdown failure**: The `Filter` operator is far from the `TableScan` operator, with a `Join` or other complex operations in between.

* **Unreasonable join type**: The `join` order between large and small tables is incorrect; if statistical information is insufficient, you can adjust it using SQL hints.

* **Data skew**: An instance of the `Aggregation` or `Join` operator takes significantly longer than other instances. This requires analysis using `query_log`.


<span id="db506c32"></span>
# 3. Core techniques for SQL optimization

<span id="da2ef6ea"></span>
## 3.1 Data model and DDL optimization

The data model is the cornerstone of the data warehouse, and good design is the starting point for high performance. In ByteHouse, the design of the table structure directly determines the physical storage of data and the efficiency of data scanning during queries.

<span id="6efbf174"></span>
### Best practices for table structure design


* **Choose an appropriate partition key (Partition Key)** 

   The partition key is the most important and effective pruning tool in ByteHouse. By specifying partition key filter conditions in the `WHERE` clause, ByteHouse can scan only the relevant partitions and skip a large amount of unrelated data.

   **Selection principles**:

   1. **Fields commonly used for query filtering**: Select columns that are used to filter data in the vast majority of queries, with date or time fields being the most typical examples (such as `dt`, `event_date`).

   2. **Moderate cardinality** (**Cardinality**): The number of partitions should be neither too many nor too few. Having too many partitions, such as partitioning by second, increases metadata management overhead; having too few partitions, such as partitioning by year, makes partition pruning meaningless. It is generally recommended to partition by month, week, or day, and the total number of partitions should be less than 100,000.

   3. **Uniform partition granularity**: Ensure that the amount of data in each partition is roughly balanced to prevent data skew.

      **Example**:

   ```SQL
   -- Create an event table partitioned by day 
   CREATE TABLE events (
       event_id String,
       user_id UInt64,
       event_time DateTime,
       -- ... Other columns
   ) ENGINE = CNCHMergeTree
   PARTITION BY toYYYYMMDD(event_time) Use the date as the partition key
   ORDER BY (user_id, event_time);
   ```
   

* **The order key** (**Order Key**) **and data distribution**

   The sort key determines how data is physically ordered and stored within each partition. This orderliness offers the following benefits:

   1. **Accelerated filtering**: For range queries on sorted columns, ByteHouse can leverage their ordered nature to quickly locate data blocks, similar to the effect of an index.

   2. **Increase compression ratio**: When identical values are grouped together, a higher compression ratio can be achieved.

      **Selection principles**:

   3. **Place high\-frequency filter columns first**: Place columns most frequently used in `WHERE` conditions at the beginning of the sort key.

   4. **Low\-cardinality columns first**: Place columns with lower cardinality (such as `country` and `gender`) before columns with higher cardinality (such as `user_id`) to improve compression efficiency.

* **Data type selection**

   Selecting the most compact and appropriate data types not only saves storage space but also improves computational efficiency.

   * **Numeric types**: Use the `UInt` series instead of `Int` when negative values are not required, and select the smallest type that can accommodate the data range, such as using `UInt8` or `UInt16` instead of `UInt64`.

   * **String type**: For strings with limited cardinality, using the `LowCardinality(String)` or `Enum` type enables dictionary encoding, which significantly reduces storage and accelerates filtering and aggregation.

   * **Avoid**`****NULL`: Whenever possible, define columns with the `NOT NULL` property, as `Nullable` columns incur additional storage and computation overhead.


<span id="2f68664b"></span>
## 3.2 Skipping index

The Skip Index is a query acceleration feature supported by ByteHouse. When processing large amounts of data, query performance may decline because a full table scan is required to apply the `WHERE` clause. Skip index solves this problem by allowing queries to skip data blocks that are confirmed not to contain matching values.

<span id="46303c4e"></span>
### Create hop count indexes

When creating an index, four main parameters are involved:


1. **Index Name**: Serves as an identifier for creating, deleting, or building index files.

2. **Index Expression**: A formula used to calculate and determine the range of values stored in an index, which can include columns, basic operators, and functions.

3. **Type**: Defines the computation method used to skip reading and evaluating each index block.

4. **Granularity**: The number of granules contained in each index block. For example, if the main table index granularity is 8,192 rows and the jump index granularity is 4, then each index block will contain 32,768 rows (8,192 x 4).


**Grammar examples**

```SQL
/*
Index name: key_i_idx
Index expression: key_i
Type: minmax
Granularity: 1
*/
INDEX key_i_idx key_i TYPE minmax GRANULARITY 1 
```


<span id="548136a0"></span>
### Supported data types

**1. Minmax (minmax)** 


* **Description**: This is an efficient indexing method that retains the minimum and maximum values of the index expression for each data block. This index type is most effective for columns with loose ordering and is typically the most cost\-effective index type for query execution.

* **Limitation:**  Only applicable to scalar or tuple expressions; cannot be used with expressions that generate arrays or mapping data types.


**2. Dataset (Set)** 


* **Description**: This lightweight index includes a parameter `max_size`, which is used to set the size of the value set for each block. When `max_size` is 0, there is no limit on the size of the value set. It applies to columns where, for each group of particles, the values are clustered around the median.

* **Cost**: The cost and performance of the index depend on the cardinality within the block. If there are too many unique values, the evaluation cost will increase; if the value set is empty because it exceeds `max_size`, the index will not be applied.


**3. Bloom filter types (Bloom filter types)** 

A Bloom filter is a compact data structure used to determine whether a member exists in a set. It may have a very low false positive rate. In skip list indexes, false positives only result in reading some unnecessary blocks.


* `tokenbf_v1`: Specifically customized for enhanced Bloom filter functionality, suitable for `String` and `FixedString` types. It splits the input expression into a sequence of characters using non\-alphanumeric characters as delimiters. This index can be used for `LIKE`, `EQUALS`, `in`, and other operations, and is suitable for searching a small number of specific values in unstructured logs. Its parameters include:

   * Filter size (bytes)

   * Number of hash functions

   * Hash function seeds

* `ngrambf_v1`: The functionality is similar to `tokenbf_v1`, but includes an additional parameter specifying the size of the ngram to be indexed. It is very useful for text search in languages without word boundaries, such as Chinese.

* `bloom_filter([false_positive])` **:**  A general\-purpose Bloom filter. The `false_positive` parameter (range 0–1, default 0.025) specifies the false positive probability. It supports multiple data types, including `Int*`, `UInt*`, `Float*`, `String`, `Array`, and many others.


<span id="b31cfaf8"></span>
#### Analyze index effectiveness

```SQL
EXPLAIN ANALYZE indexes = 1 SQL
```


**Effect example as follows**:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f6c0a4e2a1bf4dbc9e9d558218972a81~tplv-goo7wpa0wc-image.image" width="2482px" /></div>


<span id="154a0f4a"></span>
## 3.3 Usage examples

<span id="711a5fff"></span>
### 1. Load datasets to ByteHouse

First, create a database and a table for loading sample data.

```SQL
DROP DATABASE IF EXISTS test_si;
CREATE DATABASE test_si;

Create a table to load the numbers_source.csv dataset
CREATE TABLE test_si.numbers
(
    `number` UInt64
)
ENGINE = CnchMergeTree
ORDER BY number;
```


Then, use the data loading feature to load the `numbers_source.csv` dataset into the `test_si.numbers` table.

<span id="2b1ac14d"></span>
### 2. Create a data table without indexes

Create a table without indexes and insert data.

```SQL
CREATE TABLE test_skipindex
(
    `id` UInt64,
    `key_i` UInt64,
    `p_date` Date
)
ENGINE = CnchMergeTree
PARTITION BY p_date
ORDER BY id;

INSERT INTO test_skipindex SELECT
    number,
    number,
    today()
FROM test_si.numbers
LIMIT 10000000;
```


Executing the following query will process all 10 million rows of data.

```SQL
SELECT * FROM test_skipindex WHERE key_i in (200, 700);
```


<span id="0ff0c1af"></span>
### 3. Add indexes

<span id="5631f204"></span>
#### **Add indexes to a new table**

Directly define indexes when creating a table.

```SQL
CREATE TABLE test_skipindex
(
    `id` UInt64,
    `key_i` UInt64,
    `p_date` Date,
    Add indexes when creating a table
    INDEX key_i_idx key_i TYPE minmax GRANULARITY 1
)
ENGINE = CnchMergeTree
PARTITION BY p_date
ORDER BY id
SETTINGS index_granularity = 8192;

INSERT INTO test_skipindex SELECT
    number,
    number,
    today()
FROM test_si.numbers
LIMIT 1000000;
```


Execute the following query again; the result shows that only 8,192 rows were processed and the execution speed improved significantly.

```SQL
SELECt * FROM test_skipindex WHERE key_i in (200, 700);
```


<span id="849171f8"></span>
#### **Add indexes to historical data**

If an index is added after data has been inserted, by default, the index only applies to data written subsequently. For existing historical data, you must perform the materialization (materialize) operation.


1. **Add index**:

   ```SQL
   ALTER TABLE test_si.test_skipindex ADD index key_i_idx key_i TYPE minmax GRANULARITY 1;
   ```
   

2. **Add a materialized index**:

   ```SQL
   -- Build indexes for all historical data
   ALTER TABLE test_si.test_skipindex MATERIALIZE INDEX key_i_idx;
   ```
   


After execution, the query will be able to use the index, significantly reducing the number of rows processed.

<span id="5947c97a"></span>
#### **Add indexes to historical data partitions**

If you only want to build an index for a specific partition, you can use the `IN PARTITION` clause. Indexes are generated only for data in specified partitions, and historical data in other partitions are not affected.

```SQL
-- Assume that the previous day's date is '20230927'
ALTER TABLE test_si.test_skipindex MATERIALIZE INDEX key_i_idx IN PARTITION '20230927';
```


<span id="c0484c4a"></span>
### 4. Delete indexes

Use the `DROP INDEX` command to delete an existing index.

```SQL
ALTER TABLE test_si.test_skipindex DROP INDEX key_i_idx;
```


<span id="bba9def2"></span>
### Usage recommendations

When the data volume is small, the cost of creating indexes is low. However, if you need to create indexes for the entire historical data set, directly using `MATERIALIZE INDEX` may cause a significant load on the cluster. In this case, it is recommended to use `IN PARTITION` to build indexes one partition at a time to reduce the load on the cluster.

When the data that meets the query conditions exhibits clear locality, a locality\-aware index can be used to accelerate queries.

<span id="a06b9437"></span>
## 3.4 Efficient SQL writing techniques

A good data model requires efficient SQL, and following best practices can help avoid many common performance pitfalls.

<span id="7952673d"></span>
### SELECT query optimization

<span id="378161d4"></span>
#### **Reduce scan data volume: WHERE clause best practices**


* **Partition key filtering**: Always include a filter condition on the partition key in the `WHERE` clause.

* **Predicate pushdown**: Ensure that filter conditions can be pushed down to the storage layer. Avoid using non\-monotonic functions on columns in the `WHERE` clause, as this may cause index and partition pruning to fail.


**Antipattern: Using functions on columns**

```SQL
WHERE toYYYYMM(event_time) > 202508;
```


**Calculate based on the value**

```SQL
WHERE event_time >= '2025-08-01 00:00:00' AND event_time < '2025-09-01 00:00:00';
```


This example uses value\-based filtering. On top of partition filtering, the engine can further prune unnecessary Parts by leveraging minmax information on the Part partition key.

<span id="58a378b4"></span>
#### **Use PREWHERE**

For filtering on non\-sort keys, `PREWHERE` is more efficient than `WHERE`. ByteHouse first reads the columns related to `PREWHERE`, filters the data, and then reads the other columns required by `SELECT`.

Normally, the engine automatically pushes down suitable conditions from the `WHERE` clause to the `PREWHERE` clause. If the business can determine that a certain condition has a high filtering rate, it can manually write the `WHERE` condition in the `PREWHERE` clause, especially for subcolumns of the MAP type (the engine does not automatically push these down).

```SQL
SELECT 
    order_id, 
    user_id, 
    total_amount, 
    payment_method,
    province,
    items  Read large fields last
FROM order_data
PREWHERE 
    order_date BETWEEN '2024-04-01' AND '2024-06-30'  --Filter the date range first
    AND status = 'paid'  Filter paid statuses
WHERE 
    payment_method = 'credit_card'  -- Further filter payment methods
    AND total_amount > 1000  Amount filtering conditions
```


<span id="0f6a9308"></span>
#### **Optimize JOIN operations**


* **JOIN order**: Place the larger table on the left side of the `JOIN` clause and the smaller table on the right side. The engine usually reorders tables automatically; if it does not, you can collect statistics first. For details, refer to [4.1 The statistical information collection](https://docs.byteplus.com/docs/bytehouse/query-optimization-best-practice#070fdfca).

* **Pre\-filtering before JOIN**: First, use a CTE or subquery to filter and aggregate the tables to be joined, reducing the amount of data for `JOIN`.


<span id="5b84d20b"></span>
# 4. Scenario\-based optimization practices

Theoretical knowledge needs to be combined with practical scenarios to realize its greatest value. This section provides specific optimization strategies and case analyses for three typical query scenarios: complex queries, batch processing, and real\-time queries.

<span id="070fdfca"></span>
## 4.1 The statistical information collection

<span id="57e1b194"></span>
### Automatic collection

For ByteHouse CDW, you must specify the virtual warehouse used to perform statistics collection.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This feature is currently in the Beta phase. To use it, you can submit a ticket or contact the ByteHouse team to enable it.</div>


```SQL
-- Specify a virtual warehouse for collecting statistical information
CREATE AUTO STATS *.* WITH statistics_virtual_warehouse='vw-stats-collector'; 
```


<span id="cd7ed2c5"></span>
### **Manually trigger a collection**

After significant changes to the data, such as importing large volumes of data, you can manually trigger a one\-time statistics collection to ensure that the optimizer immediately uses the latest information.

```SQL
-- Manually collect statistical information for a single table
CREATE STATS table_name;

Collect for the entire database
CREATE STATS DATABASE db_name; 
```


<span id="bffd1e3c"></span>
### How to determine whether statistical information is outdated or inaccurate


* **View the EXPLAIN plan**: If the estimated `rows` value shown in `EXPLAIN` differs significantly from the actual value (by more than an order of magnitude), it usually indicates that the statistics are inaccurate.

* **Query performance fluctuations**: If a previously stable query suddenly experiences degraded performance, this may be due to changes in the data that have rendered the existing statistics invalid, while new statistics have not yet been collected.


<span id="d259b68d"></span>
## 4.2 Complex query optimization

Complex queries typically involve `JOIN` operations on multiple large tables, nested subqueries, CTEs, and window functions, and are a major source of performance issues.

<span id="b32c2ebb"></span>
### Multi\-table `JOIN` query

**Core strategies**:


1. **Reduce the amount of data for JOIN**: Before `JOIN`, filter out invalid data as much as possible by using `WHERE` or CTE.

2. **Join order**: Make sure the small table is on the right.

3. **JOIN key type consistency and use of Runtime Filter**: This is ByteHouse's flagship feature. Ensure that the types of the `JOIN` keys in the fact table (large table) and the dimension table (small table) are exactly the same, so that the `Runtime Filter` can take effect and also avoid the performance overhead caused by implicit type conversion.


<span id="e74f61ed"></span>
### Queries with subqueries or CTEs

**Core strategy**:


1. **Use CTE to improve readability**: Prefer using the `WITH` clause (CTE) instead of nested subqueries for clearer code and easier analysis by the optimizer.

2. **Materialize CTE** (**MATERIALIZE**): If a CTE is referenced multiple times, consider using a materialized view to trade space for time.


<span id="e54a866f"></span>
### **Case study: Complex report query optimization**

A typical scenario is calculating the sales revenue and user count for each city and product category.


* **Performance issue**: The `sales` table and `users` table are both very large, and a direct `JOIN` results in a massive data `Shuffle`. `count(DISTINCT)` operation performs poorly on high\-cardinality columns.

* **Pre\-optimization performance**: Query duration **95 seconds**.

* **Optimization approach**: First, pre\-aggregate the largest table `sales` by week, which greatly reduces the amount of data involved in `JOIN`. By using the `uniqCombined` approximate deduplication function, the high cost of exact deduplication is avoided.

* **Optimized performance**: Query duration **8 seconds**.


**Pre\-optimization SQL**:

```SQL
-- Directly JOIN three large tables without prior filtering
SELECT
    ci.city_name,
    p.category_name,
    sum(s.sale_amount) AS total_sales,
    count(DISTINCT s.user_id) AS total_users
FROM sales s
JOIN users u ON s.user_id = u.user_id
JOIN cities ci ON u.city_id = ci.city_id
JOIN products p ON s.product_id = p.product_id
WHERE s.dt BETWEEN '2025-08-01' AND '2025-08-07'
GROUP BY 1, 2; 
```


**Optimized SQL**:

```SQL
-- Use CTE for pre-aggregation, and replace exact deduplication with approximate calculation functions
WITH weekly_sales AS ( 
    Step 1: First perform pre-aggregation and filtering on the largest fact table
    SELECT
        user_id,
        product_id,
        sum(sale_amount) AS sale_amount
    FROM sales
    WHERE dt BETWEEN '2025-08-01' AND '2025-08-07'
    GROUP BY 1, 2
)
SELECT
    ci.city_name,
    p.category_name,
    sum(s.sale_amount) AS total_sales,
    uniqCombined(s.user_id) AS approx_total_users -- Step 2: Use uniqCombined to perform high-performance approximate deduplication
FROM weekly_sales s
Step 3: Join the aggregated small result set with the dimension table
JOIN users u ON s.user_id = u.user_id
JOIN cities ci ON u.city_id = ci.city_id
JOIN products p ON s.product_id = p.product_id
GROUP BY 1, 2;
```


<span id="03303a1e"></span>
## 4.3 Batch data processing optimization

Batch processing tasks, such as ETL/ELT, are characterized by large data volumes and scheduled execution, with optimization focused on throughput and resource efficiency.

<span id="49d88b91"></span>
### Bulk data import (INSERT INTO ... SELECT)

**Core strategy**:


1. **Adjust block size**: Appropriately increasing the size of the blocks being written (`max_insert_block_size`) can generate more regular data Parts and reduce the load on background Merge.

2. **SELECT\-side optimization**:`INSERT INTO ...` The bottleneck of `SELECT` often occurs on the `SELECT` side. Apply all `SELECT` optimization techniques from the previous chapters.


<span id="f2b27788"></span>
### Periodic ETL/ELT task optimization

**Core strategies**:


1. **Task breakdown**: Break a large, complex ETL task into multiple independent subtasks that can be executed in parallel.

2. **Resource isolation**: Configure dedicated virtual warehouses (VW) for ETL tasks to prevent resource contention with online query operations.

3. **Enable BSP mode**: For details, please refer to [ELT Support](https://docs.byteplus.com/docs/bytehouse/docs-elt-support).


<span id="14f7f464"></span>
### **Case study: Performance improvement of night batch processing tasks**

This task runs daily in the early morning to clean and transform the log data for the day, then writes the results to a daily user behavior summary table.


* **Performance issues**: A single SQL statement is too complex, making it difficult for the optimizer to generate an optimal plan. All computations are assigned to a single task, making parallel execution impossible.

* **Performance before optimization**: Task duration is **2.5 hours**, with frequent delays affecting downstream reports.

* **Optimization approach**: Apply "divide and conquer" to individual tasks. Each step performs only one task, and the logic is clear. Steps can be executed in parallel if there are no dependencies, and the intermediate results of each step can be reused and inspected. This reduces the complexity of optimization and also improves overall robustness.

* **Performance after optimization**: Total task duration is **40 minutes**.


**Pre\-optimization SQL**:

```SQL
-- A large INSERT ... SELECT statement containing complex JOIN and transformation logic
INSERT INTO user_behavior_daily 
SELECT
    user_id,
    toDate(event_time) AS dt,
    -- ... Numerous complex UDFs and multi-table JOIN logic ...
FROM raw_logs
WHERE toDate(event_time) = yesterday();
```


**The optimized solution**:

```SQL
-- Step 1: Clean and preliminarily process logs, then write to temporary table 1
CREATE TABLE cleaned_logs_tmp ...; 
INSERT INTO cleaned_logs_tmp
SELECT ... FROM raw_logs WHERE toDate(event_time) = yesterday();

-- Step 2: Associate dimension information, write to temporary table 2
CREATE TABLE enriched_logs_tmp ...;
INSERT INTO enriched_logs_tmp
SELECT ... FROM cleaned_logs_tmp JOIN users ON ...;

-- Step 3: Final aggregation, write to the target table
INSERT INTO user_behavior_daily
SELECT ... FROM enriched_logs_tmp GROUP BY ...;

-- Clean up temporary tables
DROP TABLE cleaned_logs_tmp;
DROP TABLE enriched_logs_tmp;
```


<span id="330e2535"></span>
## 4.4 Real\-time query optimization

Real\-time query scenarios, such as an online dashboard, require extremely low query latency and relatively high concurrency capability.

<span id="d22b313a"></span>
### Design considerations for low\-latency queries

**Core strategies**:


1. **Data pre\-aggregation**: Do not perform complex calculations during real\-time queries. Create pre\-aggregated summary tables—Flink wide table flattening and materialized views are both excellent tools for this purpose—so that queries can directly retrieve the results.

2. **Ultimate SELECT optimization**: Apply all `SELECT` optimization techniques to ensure queries make maximum use of partitions and indexes, scanning as little data as possible.

3. **Avoid joining large tables**: Real\-time queries should avoid `JOIN` operations whenever possible, especially `Shuffle Join`. If `JOIN` is required, use the wide table approach to flatten dimension information into the fact table before performing the join.


<span id="644a167b"></span>
### Concurrent query performance optimizations

**Core strategy**:


1. **Expand virtual warehouses**: During peak periods, handle high\-concurrency requests by increasing the number of nodes in the virtual warehouse (Scale Out) or upgrading node specifications (Scale Up).

2. **Query queues and priorities**: Assign different resource queues and priorities to queries of varying importance to ensure that core business queries are not blocked by lower\-priority tasks.

3. **Use intermediate result caching**: For highly repetitive queries, ByteHouse's intermediate result cache can return results within seconds, significantly reducing backend load. Enable the `enable_intermediate_result_cache` parameter.


<span id="2edc7a45"></span>
### **Case study: High\-concurrency dashboard query response time optimization**

A monitoring dashboard must refresh the key business metrics for the most recent minute every 5 seconds.


* **Performance issue**: Tens of thousands of rows are written to the `api_calls` table every second. Even when querying just one minute of data, the overhead of aggregation calculations is unacceptable under high concurrency.

* **Performance before optimization**: An average response time of **500 ms**, with latency spiking to **2\-3 seconds** as concurrency increases.

* **Optimization approach**: Materialized views perform pre\-aggregation continuously and incrementally in the background. Frontend queries no longer need to compute raw data; instead, they query a materialized view containing very few rows—the number of rows equals the number of status types multiplied by six time windows. Functions such as `countState` and `sumState` enable aggregation results to be efficiently merged.

* **Optimized performance**: Average response time `< 50ms` and remains stable under high concurrency.


**Pre\-optimization SQL**:

```SQL
-- Aggregate directly on the original data table 
SELECT
    status,
    count(*),
    avg(response_time)
FROM api_calls
WHERE event_time >= now() - INTERVAL '1 MINUTE'
GROUP BY status;
```


**The optimized solution**:

```SQL
-- Step 1: Create a materialized view that refreshes every 10 seconds 
CREATE MATERIALIZED VIEW api_calls_10s_mv
ENGINE = CnchMergeTree
AS SELECT
    toStartOfInterval(event_time, INTERVAL 10 SECOND) AS t_10s,
    status,
    countState() AS calls,
    sumState(response_time) AS total_response_time
FROM api_calls
GROUP BY t_10s, status;

-- Step 2: Query a materialized view in Dashboard
SELECT
    status,
    sum(calls),
    sum(total_response_time) / sum(calls)
FROM api_calls_10s_mv
WHERE t_10s >= toStartOfInterval(now() - INTERVAL '1 MINUTE', INTERVAL 10 SECOND)
GROUP BY status;
```


<span id="0b891107"></span>
# 5. Performance monitoring and management

SQL optimization is not a one\-time task, but a continuous process. Establishing effective monitoring and management mechanisms is the key to ensuring the long\-term healthy and efficient operation of the data warehouse.

<span id="29a1f622"></span>
## 5.1 Query monitoring and analysis

<span id="bf249735"></span>
### Use the system table (bh_system.query_log) for performance analysis

`bh_system.query_log` is the "black box" of ByteHouse, it records detailed information about every executed query. This is the most important data source for post\-event performance diagnosis and auditing.

**Commonly used key fields**:


* `query`: Executed SQL statement.

* `type`: Query event type (such as `QueryStart` and `QueryFinish`).

* `query_duration_ms`: Total query duration (milliseconds).

* `read_rows`, `read_bytes`: Number of rows and bytes read.

* `written_rows`, `written_bytes`: Number of rows and bytes written.

* `memory_usage`: Peak memory usage.

* `exception_code`: Exception code, used to locate failed queries.


**Analysis examples**:

```SQL
-- Find the top 10 most time-consuming queries in the past 24 hours
SELECT
    query_duration_ms,
    read_rows,
    memory_usage,
    query
FROM bh_system.query_log
WHERE type = 'QueryFinish'
  AND query_start_time >= now() - INTERVAL '1 DAY'
ORDER BY query_duration_ms DESC
LIMIT 10;
```


<span id="3bfe05a1"></span>
### Identify slow queries and resource\-intensive queries

By performing aggregation analysis on `bh_system.query_log`, you can easily locate various problematic queries.


* **Find the major CPU consumers**: Sort by `ProfileEvents['UserTimeMicroseconds'] + ProfileEvents['SystemTimeMicroseconds']`.

* **Identify major memory consumers**: Sort by `memory_usage`.

* **Find queries with a high failure rate**: Count queries where `exception_code != 0`.


<span id="0f2ff39f"></span>
### Visual performance monitoring tools

You can analyze using the metrics exposed in the Bytehouse console. For details, see [Monitoring and alarm](https://docs.byteplus.com/docs/bytehouse/monitoring-and-alarm).

<span id="541fdebc"></span>
## 5.2 Resource management and concurrency control

<span id="096b79d6"></span>
### Configuration and scaling of the Virtual Warehouse

The virtual warehouse (VW) is the management unit for computing resources in ByteHouse. By properly configuring virtual warehouses, you can achieve resource isolation and elastic scaling.


* **Create different virtual warehouses for different business scenarios**: For example, create separate virtual warehouses for ETL tasks, BI reports, and Ad\-hoc queries to prevent interference between them.

* **Auto scaling**:

   * **Scale Up** (**vertical scaling**): Increase the specifications of the nodes in a virtual warehouse (for example, `L` \-\> `XL` \-\> `2XL`). This is suitable for complex queries that require more memory or greater single\-node computing power.

   * **Scale Out** (**horizontal scaling**): Increase the number of nodes in a virtual warehouse; this is suitable for handling high\-concurrency query scenarios.


<span id="d099f205"></span>
### Concurrent query optimization and queuing strategies


* **Maximum concurrency setting**: You can set `max_concurrent_queries` for each virtual warehouse to prevent too many queries from entering simultaneously, which would slow down all queries.

* **Limit CPU usage for a single query**: To limit the CPU usage of a single query, set the `max_query_cpu_seconds` parameter.

* **Query queue**: When the concurrency limit is reached, subsequent queries are placed in the queue to wait. Proper queue configuration can ensure system stability.

* **Priority**: You can set query priorities for different users or roles to ensure that core business requests are processed first.
