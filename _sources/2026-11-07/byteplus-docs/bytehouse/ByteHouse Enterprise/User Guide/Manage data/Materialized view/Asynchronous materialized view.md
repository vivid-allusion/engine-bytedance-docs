---
title: "Asynchronous materialized view"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/asynchronous-materialized-view"
---

<span id="d76034f1"></span>
# Basic concept


* **Base Table** \- the driving table for materialized views; asynchronous materialized views support joins and subquery multi\-table association queries.

* **Target Table** \- the table where the materialized view is actually stored, usually an AggregateMergeTree or MergeTree

* **Materialized View** \- a logical concept defining the mapping relationship from base table to target table

* **Refresh** \- After creating a materialized view, the data within it only reflects the state of the base table at the creation moment. When data in the base table changes, it is necessary to refresh by querying the base table through the view to map to the target table.

* **Query Rewrite** \- Query rewrite refers to the system automatically determining whether it can reuse the precomputed results in the materialized view when querying the base table on which the materialized view is built. If reusable, the system will directly read the precomputed results from the relevant materialized view to avoid duplicated calculations which consume system resources and time.


<span id="384675c8"></span>
## Use scenario

The current open\-source ClickHouse materialized views are synchronous views, which pose certain restrictions for use scenarios:


* It affects the performance of data import into the base table.

* It supports single tables, but cannot handle multi\-table associations.


To better support scenarios with multi\-table associations and minimize the impact on data import, a feasible solution is to use asynchronous views. The main purposes include:


* Query acceleration: Asynchronous materialized views store pre\-calculated results based on specific query statements from the base tables. When performing complex queries on the base tables, it is possible to directly reuse pre\-calculated results, avoiding repeated calculations and thereby improving query performance. The more frequently a query is run or the more complex the query statement, the more significant the performance gains.

* Data Processing: Asynchronous materialized views enable lightweight data processing through ELT on the underlying data, allowing for data conversion directly within the ClickHouse Engine, reducing the need to switch between different data processing systems, and lowering the threshold for use and maintenance costs.



|Chart type |Single\-table aggregation |Multiple Table Associations |Query Rewriting |Refresh Strategy |Data Import Impact |
|---|---|---|---|---|---|
|Asynchronous Materialized Views |Yes |Yes |Yes |Asynchronous Refresh<br><br>Manual Refresh |None |
|Sync Materialized View |Yes |No |Yes |Import Sync Refresh |Yes |


<span id="1d3b9e12"></span>
## Advantages of asynchronous materialized views


* Since they refresh asynchronously at regular intervals, they do not affect the data writing path of the base tables, enhancing the write performance of the base tables.

* If the view is aligned by partitions, it will detect changes in the base table data and refresh according to the partitions to reduce the refresh cost.

* The partitions of the base table and the target table can have expressions converted, and it is not required that they be consistent.

* Supports complex multi\-table join queries, hive external table queries, unique table, materialized view cascades, common views, and other materialized views.

* The query results are strongly consistent; the results of the original query and the rewritten materialized table query are guaranteed to be the same.

* For specific operators (sum, min, max, etc.), values are stored instead of binary intermediate state data to avoid performance overhead due to secondary merges.

* The target table of the asynchronous view is of MergeTree type rather than AggregatingMergeTree, offering higher flexibility in usage.

* Comprehensive task execution status monitoring.


<span id="0bccb136"></span>
## Basic syntax

```SQL
--Create asynchronous view
CREATE MATERIALIZED VIEW [IF NOT EXISTS] [database.]<mv_name> to [database.]<target_name> [REFRESH [ASYNC [START (start_time)] EVERY (INTERVAL refresh_interval) |  MANUAL]] AS <query_statement> properties <mv_properties>;

--System commands, start and stop view refresh, activate and deactivate the view
SYSTEM [START VIEW | STOP VIEW | ACTIVATE VIEW | DEACTIVATE VIEW] [database.]<mv_name>;

--Manually refresh the view
REFRESH MATERIALIZED VIEW [database.]<mv_name>;

--Modify view attributes
ALTER TABLE [database.]<mv_name> MODIFY PROPERTY ...;
```


<span id="9167bb39"></span>
## Cautions


* refresh_interval only accepts intervals of n days/hours/minutes/seconds.

* start_time is optional and must be in the format YYYY\-mm\-dd HH:MM:SS.

* REFRESH supports ASYNC (automatic refresh) and MANUAL (manual refresh).

* In ASYNC mode, the base table type is limited to distributed table, hive cluster table, materiaizlized view, and must include the keyword 'to' targeting the destination table.

* SYSTEM START VIEW | STOP VIEW can be executed on any node in the cluster.

* SYSTEM ACTIVATE VIEW | DEACTIVATE VIEW needs to be executed on all nodes in the cluster to disable the view and stop refresh and query rewriting.

* MODIFY PROPERTY needs to be executed on each node; active and base_tables cannot be changed, and attempts to modify them will result in an error reminder.


<span id="a7e45127"></span>
## Properties of the materialized view


* base_tables \- the list of base tables the view depends on, formatted as 'db.table_1, db.table_2,...' (automatically added when creating the table).

* active \- indicates whether the state is valid; false means not participating in rewriting, no refresh, true means participating in rewriting, refresh (automatically added when creating the table).

* async_mv_enable_trigger_all_mode \- defines the trigger mode for view refresh.

   * false (Weak dependency, triggers materialized view update when any base table is updated).

   * true (Strong dependency, triggers materialized view update only when all base tables are updated).

* async_mv_excluded_trigger_tables \- Optional dependency, configures that updates on the base tables do not trigger materialized view updates, format: 'db.table_1, db_table_2,...'.

* async_mv_refresh_execution_time: Maximum execution time for refresh tasks.

* async_mv_partition_refresh_max_limit: Limits the maximum number of partition ranges for detecting changes in original tables, with partition fields allowable as (date), ('date'), (date, hour), ('date', hour), ('date', 'hour'), e.g., for original table's date partition, async_mv_partition_refresh_max_limit = 10, will construct partition filtering conditions in partition mapping calculation: p_date \>= toDate(now()) \- 10.

* async_mv_partition_refresh_min_limit: Limits the minimum number of partition ranges for detecting changes in original tables, with partition fields allowable as (date), ('date'), (date, hour), ('date', hour), ('date', 'hour'), e.g., for original table's date partition, async_mv_partition_refresh_min_limit = 1, will construct partition filtering conditions in partition mapping calculation: p_date <= toDate(now()) \- 1; and ensure that async_mv_partition_refresh_max_limit \>= async_mv_partition_refresh_min_limit to construct detection. The scope of changes in base tables, toDate(now()) \- async_mv_partition_refresh_max_limit <= p_date \>= toDate(now()) \- async_mv_partition_refresh_min_limit, for real\-time scenarios, setting async_mv_partition_refresh_min_limit=1 means today's data changes will not be detected, reducing frequent refresh triggers.

* async_mv_enable_query_rewrite \- Whether to activate view rewriting.

* async_mv_refresh_compute_resource: Configures the cluster name for compute resources used for refresh query computations.

* async_mv_enable_refresh_execute_serial: Determines whether the refresh task execution is serial or concurrent, default value \- false.

* async_mv_max_refresh_task_num: The maximum degree of parallelism for submitting view refresh tasks at one time, default value \-16.

* async_mv_enable_split_full_refresh: Whether to split full refresh tasks into partition\-based tasks, the default is true; enabling by default helps avoid large refresh tasks.


<span id="b009db38"></span>
## Use scenario of asynchronous views

Create statements for joining two tables with asynchronous materialized views.


* Join and aggregate calculations between the dimension table business.goods and the fact table business.order_list.

* Materialized table partitions roll up from day to month partition granularity **date_trunc('month', toDate(order.order_date)) as date.** 

* Automatic data import refresh.

* Original queries are automatically rewritten to hit the views.


```SQL
---Create a database
DROP DATABASE IF EXISTS business on cluster test_shard_localhost sync;
CREATE DATABASE IF NOT EXISTS business on cluster test_shard_localhost;

---Local dimension table
DROP TABLE IF EXISTS business.goods_local on cluster test_shard_localhost sync;
CREATE TABLE business.goods_local on cluster test_shard_localhost(
    create_date       DateTime,
    series_id         UInt64,
    goods_id          Int64,
    item_name         String,
    price             Float64
) ENGINE = HaMergeTree('/clickhouse/test_shard_localhost/business.goods_local/{shard}', '{replica}') PARTITION BY toDate(create_date) ORDER BY (goods_id, item_name) SETTINGS index_granularity = 8192;

---Distributed dimension table
DROP TABLE IF EXISTS business.goods on cluster test_shard_localhost sync;
CREATE TABLE business.goods on cluster test_shard_localhost (
    create_date       DateTime,
    series_id         UInt64,
    goods_id          Int64,
    item_name         String,
    price             Float64
) ENGINE = Distributed('test_shard_localhost', 'business', 'goods_local', intHash64(goods_id));

---Local fact table
DROP TABLE IF EXISTS business.order_list_local on cluster test_shard_localhost sync;
CREATE TABLE business.order_list_local on cluster test_shard_localhost(
    order_id          Int64,
    client_id         Int64,
    goods_id          Int64,
    shop_id           UInt64,
    order_date        DateTime
) ENGINE = HaMergeTree('/clickhouse/test_shard_localhost/business.order_list_local/{shard}', '{replica}') PARTITION BY (toDate(order_date), shop_id) ORDER BY (order_id,goods_id, client_id) SETTINGS index_granularity = 8192;

---Distributed fact table
DROP TABLE IF EXISTS business.order_list on cluster test_shard_localhost sync;
CREATE TABLE business.order_list on cluster test_shard_localhost(
    order_id          Int64,
    client_id         Int64,
    goods_id          Int64,
    shop_id           UInt64,
    order_date        DateTime
) ENGINE = Distributed('test_shard_localhost', 'business', 'order_list_local', intHash64(order_id)); 

--Local destination table
DROP TABLE IF EXISTS business.order_statistics_inner_join_local on cluster test_shard_localhost sync;
CREATE TABLE business.order_statistics_inner_join_local on cluster test_shard_localhost (date Date, encoded_shop_id UInt64, encoded_goods_series_id UInt64, item_id Int64, total_price Float64, max_price Float64) ENGINE = HaMergeTree('/clickhouse/test_shard_localhost/business.order_statistics_inner_join_local/{shard}', '{replica}') PARTITION BY (date, toUInt64(encoded_shop_id + 10)) ORDER BY (date, encoded_shop_id, encoded_goods_series_id, item_id) settings index_granularity = 8192;

--Distributed destination table
DROP TABLE IF EXISTS business.order_statistics_inner_join on cluster test_shard_localhost sync;
CREATE TABLE business.order_statistics_inner_join on cluster test_shard_localhost (date Date, encoded_shop_id UInt64, encoded_goods_series_id UInt64, item_id Int64, total_price Float64, max_price Float64) ENGINE = Distributed('test_shard_localhost', 'business', 'order_statistics_inner_join_local', intHash64(item_id));


--Create an asynchronous materialized view
DROP TABLE IF EXISTS business.order_mv_inner_join on cluster test_shard_localhost sync;
CREATE MATERIALIZED VIEW business.order_mv_inner_join on cluster test_shard_localhost TO business.order_statistics_inner_join
REFRESH ASYNC START('2023-12-05 10:00:00') EVERY(INTERVAL 5 SECOND)
AS SELECT
    date_trunc('month', toDate(order.order_date)) as date,
    multiIf(order.shop_id >= 2702, toUInt64(30000), shop_id <= 2701, toUInt64(40000), toUInt64(50000)) as encoded_shop_id,
    multiIf(good.series_id = 1, toUInt64(100), good.series_id = 2, toUInt64(101), good.series_id = 3, toUInt64(103), toUInt64(10)) as encoded_goods_series_id, 
    order.order_id as item_id,
    sum(good.price) as total_price, 
    max(good.price) as max_price
FROM business.order_list as order inner JOIN business.goods as good ON good.goods_id = order.goods_id WHERE date > '2023-04-01' and date <= '2023-12-01' and order.shop_id >= 2702 GROUP BY date, encoded_shop_id, encoded_goods_series_id, item_id;

--Import data
INSERT INTO business.goods
VALUES ('2023-11-01 08:32:01', 1, 1001,'apple',2366.5), ('2023-11-02 09:13:15', 1, 1002,'pear',829.0),('2023-11-03 15:06:45', 2, 1003,'potato',2238.2), ('2023-11-03 15:23:45', 3, 1004,'waterlemon',232.2),('2023-12-03 16:13:40', 4, 1108,'keybroad',2345.2);

INSERT INTO business.order_list
VALUES
    (10001,201,1001, 2701, '2023-02-16 13:30:01'),
    (10001,301,1002, 2702, '2023-12-17 20:16:15'),
    (10002,233,1002, 2703, '2023-06-20 09:42:02'),
    (10003,453,1003, 2701, '2023-05-23 16:23:34'),
    (10004,201,2001, 2701, '2023-02-16 13:30:01'),
    (10005,201,2001, 2701, '2023-02-16 13:30:01');

--Hit the view
SELECT
    date_trunc('month', toDate(order.order_date)) AS date,
    multiIf(order.shop_id >= 2702, toUInt64(30000), shop_id <= 2701, toUInt64(40000), toUInt64(50000)) AS encoded_shop_id,
    multiIf(good.series_id = 1, toUInt64(100), good.series_id = 2, toUInt64(101), good.series_id = 3, toUInt64(103), toUInt64(10)) AS encoded_goods_series_id,
    order.order_id AS item_id,
    sum(good.price) AS total_price,
    max(good.price) AS max_price
FROM business.order_list AS order
INNER JOIN business.goods AS good ON good.goods_id = order.goods_id
WHERE (date > '2023-04-01') AND (date <= '2023-12-01') AND (order.shop_id >= 2702)
GROUP BY
    date,
    encoded_shop_id,
    encoded_goods_series_id,
    item_id ORDER BY date settings enable_optimizer=1;
```
