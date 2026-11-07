---
title: "Optimizer"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/optimizer"
---

<span id="概念"></span>
# Concept

ByteHouse Optimizer is currently the only ClickHouse optimization solution in the industry. A brief overview of the capabilities of the ByteHouse Optimizer is as follows:


* RBO: Supports: column trimming, partition trimming, expression simplification, subquery decorrelation, predicate pushdown, elimination of redundant operators, Outer\-JOIN to INNER\-JOIN conversion, operator pushdown to storage, and distributed operator splitting, among other common heuristic optimizations.

* CBO: Based on the Cascade search framework, it has implemented an efficient Join enumeration algorithm, and cost estimation based on the Histogram, for Join Reorder issues involving up to ten tables, it can fully enumerate and seek the best solution, meanwhile for Join Reorder involving more than ten tables, it supports heuristic enumeration to seek the best solution. CBO supports rules\-based expansion of the search space, in addition to common Join Reorder issues, it also supports Outer\-Join/Join Reorder, Magic Set Placement, and other related optimization capabilities.

* Distributed Plan Optimization: Oriented towards distributed MPP databases, generates distributed query plans, and integrates them with CBO. Compared to mainstream industry implementations: Divided into two phases, first seeking the optimal single\-machine plan, then distributing it. Our approach integrates these two phases, during the entire CBO process of seeking the optimal solution, it combines the needs of the distributed plan and selects the best distributed plan from a cost perspective. Support for Partition properties has also been expanded in Join/Aggregate.

* Advanced optimization capabilities: Implemented Dynamic Filter pushdown, single\-table materialized view rewrite, and cost\-based CTE (Common Expression Share).


<span id="使用示例"></span>
# Use Example

Activate ClickHouse SQL Mode:

```sql
set enable_optimizer =1
```


<span id="统计信息"></span>
## Statistics Info

Collect histogram info of the data in the table. Currently, automatic collection is not supported, so it needs to be manually triggered.

<span id="收集统计信息"></span>
### Collect Statistics Info

```sql
-- Collect statistics for all tables in current database
create stats all;

-- Collect statistics for all tables and start sampling
create stats all settings statistics_enable_sample = 1

-- Collect statistics of a table
create stats [IF NOT EXISTS] <table_name>;

-- Collect statistics of a table and start sampling
create stats <table_name> settings statistics_enable_sample = 1
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0ee6e5baffe6a50e993877492e4eed1c.png) </span>

<span id="显示统计信息"></span>
### Display Statistics Info

```sql
-- Display all statistics
show stats all;

-- Display Statistics of a table
show stats [<db_name>.]<table_name>;

-- Display column level statistics of all tables
show column_stats all;

-- Display specified column level statistics of specified table
show column_stats [<db_name>.]<table_name> [at column <column_name>];
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_984face0589a8918b68bd539ea513b64.png) </span>

Column Intro:


* Identifier: Table name.Column name

* Type: Column type

* Count: Total number of values in the column.

* Null_count: The number of empty fields in the column.

* NDV: Number of distinct values in the column.

* Min: The minimum value in the column (if it's a String type, then ?).

* Max: The maximum value in the column.

* Has_histogram: Whether a histogram has been generated.


<span id="删除统计信息"></span>
### Delete statistics

```sql
-- Delete all statistics in current database
drop stats all;

-- Delete statistics of a table
drop stats <table_name>;
```


<span id="载入、读取统计信息"></span>
### Load, read statistics

```sql
set graphviz_path='/path/to/folder'
use <database_name>
show stats __save; # save statistics into /path/to/folder/<database_name>.bin
show stats __load; # load statistics from /path/to/folder/<database_name>.bin
```


The file is in PB format, please refer to `dbms/src/Protos/cbo_statistics.proto`.

<span id="执行计划"></span>
## Execution plan

Supports `EXPLAIN` (Returns the execution plan without executing).

```sql
EXPALIN SELECT sum(l_extendedprice * l_discount) AS revenue
FROM lineitem
WHERE l_shipdate >= toDate('1994-01-01')
  AND l_shipdate < toDate('1994-01-01') + INTERVAL '1' YEAR
  AND l_discount BETWEEN toFloat64('0.06') - toFloat64('0.01') AND toFloat64('0.06') + toFloat64('0.01')
  AND l_quantity < 24
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_82239ac8de09306827d9b210d93ff491.jpg) </span>

<span id="plan-可视化"></span>
##### Plan visualization


* Activate query plan visualization:


```sql
set print_graphviz=1
set graphviz_path='/.../...'  （A path you can access on the server）
```



* Install VScode and graphviz to view the execution plan visualization


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cb70ae8c874625f488f4f4273871ce85.png) </span>

<span id="处理性能回退"></span>
## Handle performance regression

If there is a performance regression, you can manually specify `SETTINGS enable_optimizer=0` at the query level

```sql
--Add "SETTINGS enable_optimizer=0" after your query to turn off optimizer
select distinct d_year from date_dim SETTINGS enable_optimizer=0;
```
