---
title: "SQL management of synchronous materialized view by SQL"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-materialized-view"
---

The synchronous materialized view stores frequently used queries so that they can be directly reused during querying, achieving query acceleration. This article introduces the syntax of the synchronous materialized view and the usage methods of the synchronous materialized view in different scenarios.

<span id="f5bfd12d"></span>
# Background

The essence of a synchronized materialized view is similar to a trigger; when data is written to a base table, it triggers the view to execute the defined SQL, writing to another table. The update granularity is the data block imported into the base table. The transaction can only end successfully if both the base table and the view's target table are written simultaneously. This shows that synchronized views can affect the import performance of the base table and can only support single\-table scenarios. It also cannot support scenarios where the base table merges data through merge, as changes in the base table cannot propagate to the view's target table, and does not support using a unique table as the base table.

Currently, at ByteHouse, the uses of materialized views are divided into the following scenarios:


* Aggregate materialized views to enhance the performance of specific aggregate queries

* Modify the primary key sorting in materialized views to enhance the performance of queries with non\-primary key column filters

* Realtime consumption of materialized views, used for processing real\-time data and producing outputs


<span id="c2ce9823"></span>
## Relevant syntax

```SQL
--Create a synchronous materialized view
CREATE MATERIALIZED VIEW [IF NOT EXISTS] [database.]<mv_name> [TO [database.]<target_name>]  AS <query_statement> [SETTINGS <mv_query_settings>];

--Manually refresh the view
REFRESH MATERIALIZED VIEW db_name.mv_name [PARTITION partition_name] [WHERE predicate_expr] [ASYNC | SYNC];
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5e0c2a04d0444f19833cb2e13dfd6c33~tplv-goo7wpa0wc-image.image) </span>

<span id="c6c29bb0"></span>
## Supported scenarios


* Base table types support CnchMergeTree tables, normal views, and real\-time consumption tables

* Single table aggregation, supports various aggregation operators, and allows for configured filter conditions

* Single table without aggregation, modifies sorting keys, reduces read fields, and supports configured filter conditions


<span id="ec3fd6d8"></span>
## Restricted scenarios


* **Does not support cascading updates across multiple views**

* **The primary table does not support a Unique table.** 

* **Due to the risk of data inconsistency, view query rewritings are not supported by default.** 

* **Due to the risk of data inconsistency, multi\-table query views are not supported by default.** 


**If such requirements exist, asynchronous materialized views are recommended.** 

The following example uses an event table from a behavior analysis system to illustrate how to use the aforementioned views.

<span id="b96749f0"></span>
# Limits

The ByteHouse Cloud Data Warehouse Edition version 2.2 and above supports this feature.

<span id="db4eceac"></span>
# **Source table definition**

```SQL
-- Create a database
create database mv;

-- Data source table
CREATE TABLE mv.events(
  app_id UInt32,
  server_time UInt64,
  event_name String,
  uid UInt64,
  cost UInt64,
  duration UInt64,
  event_date Date
) ENGINE = CnchMergeTree PARTITION BY toDate(event_date)
ORDER BY
  (app_id, uid, event_name);
```


<span id="0a1c39a7"></span>
# Aggregate materialized view

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d6632682d6c47bcb8347f5d98b3cbeb~tplv-goo7wpa0wc-image.image) </span>

Aggregate materialized views are one of the most common use cases for materialized views. They are based on specific aggregate queries that extract and store source data as materialized views. Since the aggregate queries have already aggregated the data into an intermediate state, querying the view reduces aggregate computations and improves query performance. Subsequent queries can hit the view, and the engine rewrites the original query to directly query the aggregate view table. Let's look at a specific scenario.

<span id="2c54ed10"></span>
## **View definition**

```SQL
--Target table of the view
CREATE TABLE mv.events_aggregation (
  app_id UInt32,
  event_name String,
  event_date Date,
  sum_cost AggregateFunction(sum, UInt64),
  max_duration AggregateFunction(max, UInt64)
) ENGINE = CnchAggregatingMergeTree() PARTITION BY toDate(event_date)
ORDER BY
  (app_id, event_name, event_date);

--Definition of view
CREATE MATERIALIZED VIEW mv.events_aggregate_view to mv.events_aggregation (app_id UInt32,  event_name String, event_date Date, sum_cost AggregateFunction(sum, UInt64), max_duration AggregateFunction(max, UInt64)) AS SELECT
     app_id,
     event_name,
     event_date,
     sumState(cost) AS sum_cost,
     maxState(duration) AS max_duration
FROM mv.events
GROUP BY app_id, event_name, event_date; 
```


<span id="e6c5224f"></span>
## Creating tables p**ractice**


* The source table typically uses the CnchMergeTree engine, temporarily not supporting tables with UNIQUE KEY due to unique keys automatically merging rows with the same unique key, which materialized views cannot detect, leading to inconsistency between the source table and the view data.

* The target table engine is CnchAggregatingMergeTree, which during the merge stage, merges rows with the same fields in the aggregate SQL's group by, thereby reducing data volume. For example, it aggregates calculations for rows with the same app_id, event_name, and event_date.

* In the target table, the data type of results obtained from aggregate functions with a State suffix is AggregateFunction type, with sumState(cost) corresponding to AggregateFunction(sum, UInt64), where UInt64 is the type for cost.

* It is advisable in view definitions to specify the target table using "to" for clarity and ease of understanding. Aggregate functions should include a State suffix, such as sumState(cost), maxState(duration). This is because the aggregated value saved in a single data file of the materialized view is a partial aggregate result, an intermediate data state, and the actual query needs to merge the intermediate results of the same group from different data nodes.

* The order of the group by fields in the view definition determines the order of the sort keys in the target, which should be decided based on business needs. Placing fields that are frequently used in query filters and have a lower dimension cardinality at the front can improve query performance. In examples, the target's order by fields are the same as the group by fields.

* The partition definitions of the target and source tables must be consistent; otherwise, the refresh command will not run.


<span id="c564a306"></span>
## **Import data**

```SQL
---Detailed table
insert into table mv.events(app_id, server_time, event_name, uid, cost, duration, event_date) values (1, 1642149961, 'show', 121245, 3454, 64, '2022-06-14');
insert into table mv.events(app_id, server_time, event_name, uid, cost, duration, event_date) values (2, 1642149961 , 'send', 2345, 476, 64, '2022-06-14');
insert into table mv.events(app_id, server_time, event_name, uid, cost, duration, event_date) values (3, 1642150683, 'show', 544545, 87, 5434, '2022-06-14');
insert into table mv.events(app_id, server_time, event_name, uid, cost, duration, event_date) values (3, 1642150683, 'show', 544545, 930, 232, '2022-06-14');
insert into table mv.events(app_id, server_time, event_name, uid, cost, duration, event_date) values (4, 1642150683, 'slide', 234545, 123, 98, '2022-06-14');
insert into table mv.events(app_id, server_time, event_name, uid, cost, duration, event_date) values (5, 1642150683, 'click', 131312, 2644, 26, '2022-06-14');
```


<span id="9230b61b"></span>
# Normal materialized views

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8db5a00500ff4b518bc39f3bc27c5bd7~tplv-goo7wpa0wc-image.image) </span>

In scenarios with frequent business iterations, it is often necessary to query using non\-primary key filters without altering the order of the primary keys in the main table. Based on this requirement, materialized views can be defined to modify the order of primary keys, selectively trim columns according to business needs, or filter data based on certain conditions, to produce the view.

<span id="7083bb64"></span>
## View definition

```SQL
--Target table of the view
CREATE TABLE mv.events_normal (
  app_id UInt32,
  event_name String,
  event_date Date,
  uid UInt64,
  cost UInt64
) ENGINE = CnchMergeTree() PARTITION BY toDate(event_date)
ORDER BY (uid, event_name);

--Definition of the view
CREATE MATERIALIZED VIEW mv.events_normal_view to mv.events_normal (app_id UInt32,
  event_name String,
  event_date Date,
  uid UInt64,
  cost UInt64) AS SELECT
     app_id,
     event_name,
     event_date,
     uid,
     cost
FROM mv.events;
```


<span id="1c32437c"></span>
## Creating table p**ractices**


* The target table and source table generally have the same engine type, usually CnchMergeTree, with consistent partition keys and primary key sequences defined based on business needs

* The view definition is directly selected based on the target table's field types and requirements, without needing to define an order by field


<span id="657682fd"></span>
# Real\-time materialized view

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b9f906861664d5d9f24c953f7c3da00~tplv-goo7wpa0wc-image.image) </span>

Real\-time consumption, taking Kafka's consumption as an example, requires the view's SQL definition to fetch data from the consumer, which can be fully acquired as a detailed table, and operations such as aggregation, filtering, and projection are possible. It can be a parallel view or a sequential view.

<span id="1d0aa77d"></span>
## View definition

```SQL
--Definition of the real-time consumption consumer table
CREATE TABLE mv.events_consumer (
  app_id UInt32,
  server_time UInt64,
  event_name String,
  uid UInt64,
  cost UInt64,
  duration UInt64,
  event_date Date
) ENGINE = CnchKafka() SETTINGS kafka_broker_list = 'XXXX:9092',
kafka_topic_list = 'ch_qa_cnch_staging_yg',
kafka_group_name = 'events_consumer_group',
kafka_format = 'JSONEachRow',
kafka_row_delimiter = '\n',
kafka_num_consumers = 5,
kafka_max_block_size = 65536;

---Definition of the detailed table view
CREATE MATERIALIZED VIEW mv.events_real_all_view to mv.events (
  app_id UInt32,
  server_time UInt64,
  event_name String,
  uid UInt64,
  cost UInt64,
  duration UInt64,
  event_date Date
) AS
SELECT * FROM mv.events_consumer;

---Definition of the aggregated table view
CREATE MATERIALIZED VIEW mv.events_real_aggregate_view to mv.events_aggregation (app_id UInt32,  event_name String, event_date Date, sum_cost AggregateFunction(sum, UInt64), max_duration AggregateFunction(max, UInt64)) AS SELECT
     app_id,
     event_name,
     event_date,
     sumState(cost) AS sum_cost,
     maxState(duration) AS max_duration
FROM mv.events_consumer
GROUP BY app_id, event_name, event_date; 

--Real-time consumption table of the normal table
CREATE MATERIALIZED VIEW mv.events_real_normal_view to mv.events_normal (app_id UInt32,  event_name String, event_date Date, sum_cost AggregateFunction(sum, UInt64), max_duration AggregateFunction(max, UInt64)) AS  SELECT
     app_id,
     event_name,
     event_date,
     uid,
     cost
FROM mv.events_consumer where uid = 5434;
```


<span id="49089824"></span>
## Creating table p**ractices**


* The source table in the view definition is a real\-time consumption table

* Currently, defining a new view requires restarting real\-time consumption; otherwise, data will not be updated

* Defining the three views will create three sets of data; defining many views or complex aggregate views will affect the performance of real\-time consumption.
