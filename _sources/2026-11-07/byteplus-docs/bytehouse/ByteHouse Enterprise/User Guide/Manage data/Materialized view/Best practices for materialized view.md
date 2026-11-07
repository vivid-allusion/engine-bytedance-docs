---
title: "Best practices for materialized view"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/best-practices-for-materialized-view"
---

<span id="54dd56e3"></span>
## Materialized views and distributed queries

For materialized views, it is suggested to use local tables as both source and target tables to process data locally, minimizing data exchange between nodes during processing. In this case, to query all data across nodes, a distributed table must also be created on the target table of the materialized view.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d212ee59ac5a46a78883bb8071a37207~tplv-goo7wpa0wc-image.image" width="708px" /></div>


Basic Procedure:


1. Create new source tables, including local and distributed tables.

2. Create new target tables, including local and distributed tables.

3. Create a materialized view based on local tables.

4. Insert data into the source table (distributed table).


Below is an SQL statement example:

```SQL
--1. Create source tables, including a local table and a distributed table
-- local table
CREATE TABLE default.ods_test_local ON CLUSTER bytehouse(
  `id` Int8, 
  `pDate` Date, 
  `description` String
) ENGINE = HaMergeTree(
    '/clickhouse/0/cluster_name/default.ods_test_local_17658700571/{shard}',
    '{replica}'
  )
ORDER BY id;

-- distributed table
CREATE TABLE default.ods_test ON CLUSTER bytehouse(
  `id` Int8, 
  `pDate` Date, 
  `description` String
) ENGINE = Distributed(
    'bytehouse',
    'default',
    'ods_test_local',
    rand()
  );

--2. Create target tables
-- local table
CREATE TABLE default.dm_test_local ON CLUSTER bytehouse(
  `id` Int8, 
  `pDate` Date
) ENGINE = HaMergeTree(
    '/clickhouse/0/cluster_name/default.dm_test_local_17658700571/{shard}',
    '{replica}'
  )
ORDER BY id;

-- distributed table
CREATE TABLE default.dm_test ON CLUSTER bytehouse(
  `id` Int8, 
  `pDate` Date
) ENGINE = Distributed(
    'bytehouse',
    'default',
    'dm_test_local',
    rand()
  );

--3. Create a materialized view
CREATE MATERIALIZED VIEW default.ods2dm_test_mv ON CLUSTER bytehouse
TO default.dm_test_local
AS SELECT id, pDate FROM default.ods_test_local;

--4. Insert data into the source table 
-- and query the target table to test whether the materialized view takes effect
INSERT INTO default.ods_test VALUES (1,'2024-01-01',''),(2,'2024-01-02','');

SELECT * from default.dm_test LIMIT 10;

-- Query result
1,'2024-01-01'
2,'2024-01-02'
```


<span id="2dd05c9d"></span>
## HaKafka import

Through a materialized view, HaKafka's table engine can be automatically synchronized to the local table, thereby achieving Kafka import.

The basic architecture diagram is as follows:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/91af353a515743c8887071778e46e302~tplv-goo7wpa0wc-image.image" width="609px" /></div>


In the control interface, create a new Kafka import task, which is based on this example, to be automatically generated and displayed on the interface.

Examples of SQL operations are as follows:

```SQL
-- Create a HaKafka table
CREATE TABLE TEST.CONSUMER_tce_service_resource_usage_local ON CLUSTER bytehouse (
    `current_ts` Int64,
    `psm` String,
    `cpu_limit_pod` Float64
) ENGINE = HaKafka()
SETTINGS 
kafka_broker_list = 'xxx.xxx.xxx.xxx',  -- Replace it with kafka broker
kafka_topic_list = 'xxx_topic', -- Replace it with the business topic
kafka_group_name = 'xxx_group_name', -- Replace it with the group_name related to the business
kafka_format = 'JSONEachRow', -- Normally JSON is applied
kafka_row_delimiter = '\n', -- Normally \n is applied
kafka_leader_priority = '{replica_num}', -- Fixed parameters. Do not modify it.
kafka_partition_num = '{shard_index}', -- Fixed parameters. Do not modify it.
kafka_shard_count = '{shard_count}'; -- Fixed parameters. Do not modify it.

--- Prepare a HaMergeTree table to store data.
CREATE TABLE TEST.tce_service_resource_usage_local ON CLUSTER bytehouse (
    `current_ts` Int64,
    `psm` String,
    `cpu_limit_pod` Float64
) ENGINE = HaMergeTree()
ORDER BY psm
PARTITION BY toDate(current_ts) 

CREATE TABLE TEST.tce_service_resource_usage ON CLUSTER bytehouse 
AS TEST.tce_service_resource_usage_local ENGINE = Distributed('ByteHouse'，'TEST','tce_service_resource_usage_local');

--- Create aother materialized view to select data from the HaKafka table and write it into the HaMergeTree table.
CREATE MATERIALIZED VIEW TEST.VIEW_tce_service_resource_usage_local ON CLUSTER ByteHouse
TO TEST.tce_service_resource_usage_local
AS SELECT current_ts, psm, cpu_limit_pod FROM TEST.CONSUMER_TEST_tce_service_resource_usage_local
```


Afterwards, you only need to query the distributed table of the target table to view the consumption status.

```SQL
Select * from TEST.tce_service_resource_usage limit 10;
```


<span id="b834fcdf"></span>
## Aggregate table engine

Both HaAggregatingMergeTree and HaSummingMergeTree are MergeTree engine types with aggregation functions. These two types can perform aggregation operations on the source table's data, then sync the aggregated data to the target table, thus achieving a significant acceleration in aggregate queries.

In practical applications, by leveraging their aggregate properties, the efficiency and performance of data querying can be significantly enhanced. Especially when dealing with large\-scale data sets, this aggregation function can significantly reduce the time and resource consumption required for queries.

<span id="1a17cee9"></span>
### Method 1: Automatically create the target table

```SQL
CREATE MATERIALIZED VIEW agg_test_mv ON CLUSTER bytehouse 
    ENGINE = HaAggregatingMergeTree() 
    ORDER BY (p_date, name)
    PARTITION BY p_date 
    AS SELECT p_date, name, avgState(age) as age_avg
        FROM agg_test_source_local WHERE gender = 'male' GROUP BY p_date, name

--After creating the materialized view, synchronize the database tables. You can see that a table named .inner_id.24c211a5-fec3-45a3-afed-e3d3cf46a1ea is generated as the target table. Based on the target table, you need to create a distributed table. 
CREATE TABLE agg_test_target ON CLUSTER byteHouse
    as default.`.inner_id.24c211a5-fec3-45a3-afed-e3d3cf46a1ea`
    engine = Distributed('bytehouyse','default','.inner_id.24c211a5-fec3-45a3-afed-e3d3cf46a1ea',rand());
```


<span id="19c08a7b"></span>
### Method 2: Manually build the target

```SQL
CREATE TABLE agg_test_target_local ON CLUSTER bytehouse 
    p_date Date,
    name String,
    age_avg AggregateFunction(avg, Int64) --
) engine = HaAggregatingMergeTree()
ORDER BY (p_date, name)
PARTITION BY p_date;

CREATE TABLE agg_test_target ON CLUSTER bytehouse 
    AS agg_test_target_local
    engine = Distributed('bytehouse','default','agg_test_target_local',rand());

CREATE MATERIALIZED VIEW agg_mv_test ON CLUSTER bytehouse 
    to agg_test_target_local
    AS SELECT p_date, name, avgState(age) as age_avg
        FROM test WHERE gender = 'male' GROUP BY p_date, name;
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For aggregate functions, explicit rewriting to <code>xxxState</code> is required. This function saves the intermediate state to facilitate subsequent data merging, as in this case <code>avg()</code> was rewritten to <code>avgState()</code>. Meanwhile, when querying the materialized view, it needs to be explicitly rewritten as <code>xxxMerge()</code>, such as:</div>


<div data-tips="true" data-tips-type="warning">```SQL
SELECT name, avgMerge(age_avg) from agg_mv_test GROUP BY name;
```
</div>


<span id="c9cef29a"></span>
## Modify materialized view structure

Materialized views do not support direct modification of columns. In this case, it is advised to follow these steps:


1. Delete the materialized view.

2. If a target table was manually specified, execute the Truncate command on the target table, and adjust the structure of the target table.

3. Rebuild the materialized view.


For example, if you want to add the "gender" and "profile" attributes from the source table "test" to the materialized view named "agg_mv_test" and include the aggregate metric that calculates the total age, you can follow these steps:

```SQL
DROP TABLE agg_mv_test on cluster bytehouse sync;

CREATE MATERIALIZED VIEW agg_mv_test on cluster bytehouse 
    ENGINE = HaAggregatingMergeTree() 
    ORDER BY (p_date, name)
    PARTITION BY p_date 
    AS SELECT p_date, name, gender, profile, avgState(age) as age_avg, sumState(age) as age_sum FROM test WHERE gender = 'male' GROUP BY p_date, name, gender, profile;
```


<span id="cb7af6b1"></span>
## Automatic rewrite

When a user directly queries the source table of the materialized view, automatic rewriting can be enabled by setting the parameter “`enable_view_based_query_rewrite = 1`”. With this setting, the query will automatically match the corresponding materialized view, thus achieving automatic acceleration. For instance:

```SQL
SELECT name, age from test WHERE p_date = '2019-01-01' AND gender = 'male' SETTINGS enable_view_based_query_rewrite = 1
```


If the target table is of Type HaAggregatingMergeTree, there's no need to specify "xxxMerge" during the query. Just use the standard aggregate functions, and the system will automatically rewrite it. Example as follows:

```SQL
SELECT p_date, name, avg(age) as age_avg FROM test WHERE gender = 'male' GROUP BY p_date, name SETTINGS enable_view_based_query_rewrite = 1;
```
