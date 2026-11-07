---
title: "SQL management of asynchronous materialized view by SQL"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/Asynchronous_Materialized_View"
---

The asynchronous materialized view can better support scenarios involving the association of multiple tables, reducing the impact on data import. It can be applied to scenarios such as complex query acceleration, data processing, and query matching. This article introduces the syntax of the asynchronous materialized view, how to create and configure the asynchronous materialized view, and also provides the best practices for the asynchronous materialized view.

<span id="7d6dbf7d"></span>
# Prerequisite

Before using the asynchronous materialized view, ensure the view definition aligns with recommended usage scenarios:


1. The base tables used in the view definition SQL should preferably be **offline tables updated daily**. **Real\-time tables are not recommended**, as they may cause frequent refresh task triggers, increasing refresh costs and system load.

2. The view definition SQL **must ensure partition alignment**. The target table's partitions should be computed from the partition data of one base table. Otherwise, changes to any base table will trigger a costly **full refresh**.

3. The optimal scenario for joins is: **fact tables updated daily offline** and **dimension tables that are rarely updated**. If fact tables lack partition alignment or dimension tables change frequently, it will cause frequent full refreshes, significantly increasing system load.

4. Views **lack a retry mechanism** upon refresh failure. Failed refreshes will only be retried at the next scheduled interval. Therefore, it is **recommended to set the scheduling interval to minutes** to increase retry opportunities.

5. The actual execution timing **is not guaranteed to strictly adhere to the set interval** and depends on task execution duration. If a task's execution exceeds the interval, it will be deferred to the next cycle. **Do not strictly rely on the scheduling interval for precise timing**.

6. Configuring parameters for asynchronous views in ByteHouse CDW is complex, involving various **Virtual Warehouse (VW) settings**. Failure to configure correctly will route tasks to the default VW, potentially overloading servers. **Carefully configure settings by referring to the** [VW resource isolation](https://docs.byteplus.com/docs/bytehouse/Asynchronous_Materialized_View#71ec34d4) **section.** 


<span id="9b8043a8"></span>
# Background

<span id="a5bf1511"></span>
## Asynchronous materialized view

In order to better support multi\-table association scenarios and reduce the impact on data import, asynchronous views are a better solution.

The purpose of an asynchronous view is twofold:


* Complex Query Acceleration: Asynchronous materialized views store pre\-computed results based on specific query statements of the base table. When performing complex queries on the base table, the pre\-computed results can be directly reused to avoid repeated calculations, thereby improving query performance. The higher the frequency of the query or the more complex the query statement, the more obvious the performance gain will be.

* Data processing: Through asynchronous materialized views, lightweight data processing can be performed on the underlying data by ELT, and data conversion can be realized directly in the bytehouse engine content, reducing switching between different data processing systems, reducing the threshold for use and maintenance costs.

* Query matching: The asynchronous view will determine whether the detailed table or the materialized table is read through the refreshed version of the base table data to ensure the consistency of the data query.


<span id="d8db3dd2"></span>
## Asynchronous materialized view advantage


* **Balance between performance and real\-time performance**: Minimize the impact on write performance while maintaining data freshness through an asynchronous update mechanism.

* **Complex Query Optimization**Precompute and store complex query results, significantly improving analysis performance.

* **Resource Utilization Efficiency**Optimize system resource usage by intelligently scheduling update operations.

* **data consistency**: Finding a balance between near real\-time updates and eventual consistency, supporting view rewriting query consistency

* **Support for complex materialized queries**: Support multi\-table complex view definition, support nested views, nested materialized views


<span id="3d6d3b87"></span>
## Partition incremental refresh strategy

The single\-table scenario is relatively simple. How to reduce the cost of refresh as much as possible in the scenario of multi\-table association? The solution is to limit the scenario, find relatively unchanged data and frequently changing data, and find incremental data refresh to reduce the refresh cost.

Data modeling often involves associating data according to business semantics. Different data association methods lead to different modeling methods, such as star schema and snowflake schema, which both use fact tables and dimension tables. Some business scenarios require multiple large fact tables, while other scenarios involve complex dimension tables and complex relationships between them. The fact table changes frequently, and the dimension table basically does not change. Based on this scenario, the view target table can be aligned with a base table that changes frequently, and the refresh strategy is based on partition granularity.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9626605fb47d485f8d1271b895aab9a6~tplv-goo7wpa0wc-image.image) </span>

<span id="057baced"></span>
# Limits

The ByteHouse Cloud Data Warehouse Edition version 2.2 and above supports this feature.

<span id="d14dad19"></span>
# Asynchronous View Syntax and Configuration

<span id="1a23e363"></span>
## Related syntax

```SQL
--Create asynchronous views
CREATE MATERIALIZED VIEW [IF NOT EXISTS] [database.]<mv_name> [TO [database.]<target_name>] [REFRESH [ASYNC [START (start_time)] EVERY (INTERVAL refresh_interval) | MANUAL]] AS <query_statement> [SETTINGS <mv_query_settings>] [PROPERTIES <mv_properties>];

--System command, start, stop view refresh, activate, disable view
SYSTEM [START VIEW | STOP VIEW | ACTIVATE VIEW | DEACTIVATE VIEW] [database.]<mv_name>;

--Manually refresh the view
REFRESH MATERIALIZED VIEW [database.]<mv_name> [ASYNC | SYNC];

--Modify view properties
ALTER TABLE [database.]<mv_name> MODIFY PROPERTY ...;

--Modify the SQL settings of the view
ALTER TABLE [database.]<mv_name> MODIFY VIEW QUERY SETTING ...;

--Modify the view refresh mode
ALTER TABLE [database.]<mv_name> MODIFY REFRESH ...;
```


**Note**


* The refresh interval supports integer units of days/hours/minutes/seconds, for example: INTERVAL 5 SECOND, INTERVAL 10 MINUTE

* The refresh start time is optional and must be defined in YYYY\-mm\-dd HH: MM: SS format, for example 2023\-12\-05 10:00:00

* Refresh mode supports scheduled automatic trigger refresh (ASYNC), manual trigger refresh (MANUAL)

* Since the destination table is generated by the original table, it only needs to limit the partition range of the original table to automatically generate the destination table. Therefore, the destination table does not allow setting TTL for data deletion, otherwise it will cause data inconsistencies. When building the table, it will also check whether the destination table has TTL definition


<span id="fea774ab"></span>
## Supported scenarios


* Base table types support CnchMergeTree tables (including unqiue tables), HIVE surfaces, nested materialized views, normal views

* Single table aggregation, supports various aggregation operators, filter conditions

* Single table without aggregation, modify sorting key, reduce read field, filter condition

* Multi\-table join aggregate query, support inner join, left join, semi jon, anti join, non\-equivalent join, equivalent join type

* Materialized View Multi\-layer Cascade

* Support union all, full join refresh, scalar quantum query, but do not support view rewriting, for ETL scenarios


<span id="eddc6541"></span>
## Asynchronous view properties

The asynchronous view\-specific related property configuration instructions are defined in the PROPERTIES keyword of the table\-building statement, and can also be modified by the MODIFY PROPERTY command.


|<span id="abc3c067"></span><br>#### **configuration name** |<span id="fcdeba0e"></span><br>#### **meaning** |<span id="18f26286"></span><br>#### **Configuration options and instructions** |<span id="72abece4"></span><br>#### **default value** |
|---|---|---|---|
|async_mv_enable_trigger_all_mode |Trigger mode for view refresh |* False \- weak dependency, a base table update will trigger a materialized view update<br><br>* True \- strong dependency, materialized view update is triggered only when all base tables are updated |False |
|async_mv_excluded_trigger_tables |Specify which base table updates do not trigger materialized view updates. |Format: 'db. table_1, db_table_2,...' |' |
|async_mv_refresh_execution_time |Refresh task maximum execution time |In seconds, 0 means there is no limit to the refresh time |0 |
|async_mv_partition_refresh_max_limit |Limit the maximum number of partition ranges for detecting changes in the original table, and the partition field definition requires a partition key field of Date type |Parameters define the range of changes in the base table to be detected, and filter conditions are added: toDate (now ()) \- async_mv_partition_refresh_max_limit < = p_date \> = toDate (now ()) \- async_mv_partition_refresh_min_limit<br><br>The purpose is to calculate the view results using only the most recent data for business scenarios, limit the update range of the base table, and reduce the frequent triggering of refresh operations |0 |
|async_mv_partition_refresh_min_limit |Limit the minimum number of partition ranges to detect changes in the original table, and the partition field definition requires a partition key field of Date type |Parameters define the range of changes in the base table to be detected, and filter conditions are added: toDate (now ()) \- async_mv_partition_refresh_max_limit < = p_date \> = toDate (now ()) \- async_mv_partition_refresh_min_limit<br><br>The purpose is to calculate the view results using only the most recent data for business scenarios, limit the update range of the base table, and reduce the frequent triggering of refresh operations |0 |
|async_mv_enbale_query_rewrite |Whether to enable view overwriting |* True \- open view automatically rewrites<br><br>* False\-close view automatically rewrites |True |
|async_mv_enable_refresh |Whether to enable view refresh |* True \- enable view refresh<br><br>* False \- close view refresh |True |
|async_mv_refresh_task_bsp_mode |Whether to use bsp mode (stage operation mode, which can effectively reduce resource usage) |* True \- Enable view bsp mode<br><br>* False \- close view bsp mode |True |
|enable_drop_inner_table_cascade |Whether to automatically delete implicit tables |* True \- enable automatic deletion of implicit tables<br><br>* False\-off automatic deletion of implicit tables |True |
|async_mv_enable_refresh_execute_serial |Execute refresh task execution mode |* True \- perform refresh tasks in serial mode<br><br>* False \- execute refresh task in concurrent mode |True |
|async_mv_max_refresh_task_num |Execute refresh task maximum parallelism |Execute concurrently when async_mv_enable_refresh_execute_serial = false, limiting the maximum concurrency of refresh task execution |16 |
|async_mv_enable_split_full_refresh |Whether to split the full refresh task into refresh tasks according to partition granularity |The full refresh task is to refresh all the data. When the amount of data is large, the query time is long. The full refresh task can be split into tasks refreshed according to the partition granularity |True |
|async_mv_refresh_work_period |Define the time period for view refresh execution |Format: "Schedule1; Schedule2;... |timezone" schedule: "HH: MM\-HH: MM/1,2,3,4,5", for example: 12:00\-13:00/1,3,5; 14:00\-18:00/6,7; 00:00\-23:59/1,2,3,4,5 |
|Active (automatically added when creating a table) |Is the view valid? |* True \- run the refresh task, the view does not participate in overwriting<br><br>* False \- stop refresh task, view does not participate in query overwriting |True |
|base_tables (automatically added when creating a table) |View dependent base table list |Format: 'db. table_1, db_table_2,...' |' |


<span id="c163fb50"></span>
## Global system configuration


|<span id="35f6eaea"></span><br>#### **configuration name** |<span id="16b8c988"></span><br>#### **meaning** |<span id="e5894894"></span><br>#### **Configuration options and instructions** |<span id="2e8a37c4"></span><br>#### **default value** |
|---|---|---|---|
|async_mv_refresh_task_submit_to_bg_thread |Whether the manual refresh command is submitted to the central node for execution |Does the manual refresh perform the refresh task on the current node, or is it submitted to the central node for execution |True |
|enable_async_mv_debug |Show detailed debugging information |Manual refresh whether to enable detailed debugging information configuration |False |
|enable_sync_mv_with_multiple_base_tables |Whether to allow multiple table synchronization views |* True, you can create a multi\-table synchronous view<br><br>* False, disable the creation of multi\-table synchronous views |True |


<span id="4e6a3d0f"></span>
## System configuration file

Start CNCH_REFRESH_MATERIALIZED_VIEW refresh thread in deamon\-manager.xml

```SQL
...
</daemon_manager>
<daemon_jobs>
  ...
  <job>
    <name>CNCH_REFRESH_MATERIALIZED_VIEW</name>
    <interval>5000</interval>
    <disable>false</disable>
  </job>
  ...
 </daemon_jobs>
</daemon_manager>
...
```


<span id="2e211685"></span>
## Table instance

```SQL
DROP DATABASE IF EXISTS async_mv_left_join_test;
CREATE DATABASE async_mv_left_join_test;

-- Create base tables
CREATE TABLE async_mv_left_join_test.orders
(
    order_id UInt32,
    user_id UInt32,
    product_id UInt32,
    order_date Date,
    order_amount Decimal(10,2)
) ENGINE = CnchMergeTree
PARTITION BY order_date
ORDER BY (order_id, user_id);

CREATE TABLE async_mv_left_join_test.users
(
    user_id UInt32,
    username String,
    registration_date Date
) ENGINE = CnchMergeTree
PARTITION BY toYYYYMM(registration_date)
ORDER BY user_id;

CREATE TABLE async_mv_left_join_test.products
(
    product_id UInt32,
    product_name String,
    category String,
    price Decimal(10,2),
    last_updated DateTime
) ENGINE = CnchMergeTree
PARTITION BY toYYYYMM(last_updated)
ORDER BY product_id
UNIQUE KEY product_id;

-- Create materialized view with WITH clause and implicit table
CREATE MATERIALIZED VIEW async_mv_left_join_test.order_summary_mv
ENGINE = CnchMergeTree
PARTITION BY order_date
ORDER BY (category, username, product_name)
REFRESH ASYNC START('2024-09-12 15:43:48') EVERY(INTERVAL 5 SECOND) AS
WITH 
    price_categories AS (
        SELECT
            product_id,
            multiIf(
                price <= 50, 'Low',
                price <= 100, 'Medium',
                'High'
            ) as price_category
        FROM async_mv_left_join_test.products
    )
SELECT
    toYYYYMM(addYears(addDays(o.order_date, 2), 1))as order_date,
    assumeNotNull(u.username) as username,
    p.product_name as product_name,
    assumeNotNull(p.category) as category,
    o.order_amount as order_amount,
    assumeNotNull(pc.price_category) as price_category,
    p.price as product_price
FROM async_mv_left_join_test.orders o
LEFT JOIN async_mv_left_join_test.users u ON o.user_id = u.user_id
LEFT JOIN async_mv_left_join_test.products p ON o.product_id = p.product_id
LEFT JOIN price_categories pc ON o.product_id = pc.product_id
WHERE o.order_amount > 0 AND p.price > 0 SETTINGS max_memory_usage = 68719476736,
  max_threads = 8,
  virtual_warehouse = 'hdfs-staging-default',
  max_memory_usage_for_user = 242292621312,
  exchange_queue_bytes = 1073741824,
  max_execution_time = 3600 PROPERTIES 
  async_mv_refresh_execution_time = 3600,
  async_mv_enable_refresh_execute_serial = 1,
  async_mv_max_refresh_task_num = 8,
  async_mv_enbale_query_rewrite = 1,
  async_mv_enable_refresh = 1,
  async_mv_refresh_work_period = '00:00-23:59/1,2,3,4,5,6,7|Asia/Shanghai',
  async_mv_refresh_task_bsp_mode = 1;

-- Insert initial test data
INSERT INTO async_mv_left_join_test.orders VALUES (1, 101, 1001, '2023-05-01', 55.00), (2, 102, 1002, '2023-05-02', 85.00), (3, 103, 1003, '2023-05-03', 110.00), (4, 104, 1004, '2023-06-01', 130.00), (5, 105, 1005, '2023-06-02', 95.00); 

INSERT INTO async_mv_left_join_test.users VALUES (101, 'user1', '2023-01-01'), (102, 'user2', '2023-01-02'), (103, 'user3', '2023-01-03'), (104, 'user4', '2023-02-01'), (105, 'user5', '2023-02-02'); 

INSERT INTO async_mv_left_join_test.products VALUES (1001, 'Product A', 'Category1', 50.00, '2023-05-01 10:00:00'), (1002, 'Product B', 'Category2', 80.00, '2023-05-01 11:00:00'), (1003, 'Product C', 'Category1', 120.00, '2023-05-01 12:00:00'), (1004, 'Product D', 'Category2', 150.00, '2023-06-01 10:00:00'), (1005, 'Product E', 'Category1', 95.00, '2023-06-01 11:00:00');

-- enable_materialized_view_rewrite = 1 test whether match views
WITH 
    price_categories AS (
        SELECT
            product_id,
            multiIf(
                price <= 50, 'Low',
                price <= 100, 'Medium',
                'High'
            ) as price_category
        FROM async_mv_left_join_test.products
    )
SELECT
    toYYYYMM(addYears(addDays(o.order_date, 2), 1))as order_date,
    assumeNotNull(u.username) as username,
    p.product_name as product_name,
    assumeNotNull(p.category) as category,
    o.order_amount as order_amount,
    assumeNotNull(pc.price_category) as price_category,
    p.price as product_price
FROM async_mv_left_join_test.orders o
LEFT JOIN async_mv_left_join_test.users u ON o.user_id = u.user_id
LEFT JOIN async_mv_left_join_test.products p ON o.product_id = p.product_id
LEFT JOIN price_categories pc ON o.product_id = pc.product_id
WHERE o.order_amount > 10 AND p.price > 30 order by order_date, username  settings enable_optimizer = 1, enable_materialized_view_rewrite = 1;
   

-- enable_materialized_view_rewrite = 0 check not match view result
WITH 
    price_categories AS (
        SELECT
            product_id,
            multiIf(
                price <= 50, 'Low',
                price <= 100, 'Medium',
                'High'
            ) as price_category
        FROM async_mv_left_join_test.products
    )
SELECT
    toYYYYMM(addYears(addDays(o.order_date, 2), 1))as order_date,
    assumeNotNull(u.username) as username,
    p.product_name as product_name,
    assumeNotNull(p.category) as category,
    o.order_amount as order_amount,
    assumeNotNull(pc.price_category) as price_category,
    p.price as product_price
FROM async_mv_left_join_test.orders o
LEFT JOIN async_mv_left_join_test.users u ON o.user_id = u.user_id
LEFT JOIN async_mv_left_join_test.products p ON o.product_id = p.product_id
LEFT JOIN price_categories pc ON o.product_id = pc.product_id
WHERE o.order_amount > 10 AND p.price > 30  order by order_date,username settings enable_optimizer = 1, enable_materialized_view_rewrite = 0;

-- modify property
ALTER TBALE async_mv_left_join_test.order_summary_mv MODIFY PROPERTY async_mv_max_refresh_task_num = 10;

-- modify view query setting
ALTER TBALE async_mv_left_join_test.order_summary_mv MODIFY VIEW QUERY SETTING max_execution_time = 3000;

-- modify refresh 
ALTER TBALE async_mv_left_join_test.order_summary_mv MODIFY REFRESH ASYNC START('2024-09-12 15:43:48') EVERY(INTERVAL 10 SECOND);

-- check table definition
SHOW CREATE TABLE async_mv_left_join_test.order_summary_mv;

DROP DATABASE IF EXISTS async_mv_left_join_test;
```


<span id="ab7e54a7"></span>
# Overall execution flow

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/753f4aaebd1f4603b384b7a305af1233~tplv-goo7wpa0wc-image.image) </span>

The asynchronous view execution flow is as follows:

<span id="f2a1bfda"></span>
## Create asynchronous view

```Plain Text
 Users create asynchronous materialized views through SQL statements. The system records view definitions, dependencies, and other information in metadata.
```


<span id="3dcbf493"></span>
## Background management process

DaemonManager acts as the background process manager of the bytehouse and is responsible for monitoring and managing various system tasks. When DaemonManager detects the existence of an asynchronous view, it initializes and starts RefreshMaterializedViewThread background thread on the server side dedicated to refreshing asynchronous materialized views. After the thread is started, the refresh task is performed periodically according to the configured refresh policy.

<span id="b84f4ca8"></span>
## Refresh task execution


* Get base table partition changes: Check the base table partition changes since the last refresh to identify new, modified, or deleted partitions.

* Calculate the scope of influence: Analyze and determine the affected target table partition according to the change of the base table partition, consider the filter conditions, aggregation operations, etc. in the view definition, and precisely locate the data range that needs to be updated.

* Construct refresh tasks: Split large refresh tasks into multiple small tasks for parallel processing and resource management. Each small task is responsible for refreshing a specific partition.

* Task submission and scheduling: Submit the refresh task to the task queue of the bytehouse, and the system scheduler schedules the task execution according to the current load and priority.

* Task execution: Perform refresh operations, which may include steps such as data recalculation, aggregation, and updating. For incremental updates, only the changed data part is processed to improve efficiency.

* Meta information update: Update the meta information of the materialized view, including the latest partition information, timestamp, etc.

* Resource management and optimization: Implement a mechanism to dynamically adjust the refresh rate, adaptively according to system load and data change rate. Introduce priority queues to ensure that key views can be refreshed in time.

* Monitoring and reporting: Provide detailed refresh logs and statistics for easy monitoring and optimization by administrators.


<span id="1250d330"></span>
# Partition mapping calculation

The purpose of the verification is to parse the SQL of the view to determine whether the partition of the destination table is calculated by one of the base tables, and can be calculated from the partition value, so that it belongs to the view that can be refreshed asynchronously at the partition level.

<span id="d36240ef"></span>
## Align partition**validation**


* Condition 1: The partitioned computed fields of the destination table must come from the same base table

* Condition 2: The evaluation expression of the destination table partition can be calculated from the partition field of the base table


**Example:** 

Destination table partition:

```SQL
(date, toUInt64(encoded_shop_id + 10))
```


View SQL mapping:

```SQL
date_trunc('month', toDate(order.order_date)) as date

multiIf(order.shop_id >= 2702, toUInt64(30000), shop_id <= 2701, toUInt64(40000), toUInt64(50000)) as encoded_shop_id
```


Base table partition:

```SQL
(toDate(order_date), shop_id)
```


Validation condition 1: date is converted from order_date, encoded_shop_id is converted from shop_id, order_date, shop_id all come from the same base table order_list

Validation condition 2: Destination table partition requires (toDate (order_date), shop_id) two fields, both order_list table partition field

```SQL
(date_trunc('month', `toDate(order_date)`), toUInt64(multiIf(shop_id >= 2702, CAST(30000, 'UInt64'), shop_id <= 2701, CAST(40000, 'UInt64'), CAST(50000, 'UInt64')) + 10)
```


<span id="0f937f26"></span>
## Partition conversion**expression**

Input: partition data for source table eg. '2023\-11\-10' or ('2023\-11\-10', 1)

Convert expression: Constructs a partition expression action that extracts the filter condition for the partition

Output: partition data of destination table eg. '2023\-11\-10'

**Example:** 

Enter block header: ('toDate (order_date) ', 'shop_id')

Input value: ('2023\-11\-10', 1)

Transform expression list with filter

```SQL
(date_trunc('month', `toDate(order_date)`), toUInt64(multiIf(shop_id >= 2702, CAST(30000, 'UInt64'), shop_id <= 2701, CAST(40000, 'UInt64'), CAST(50000, 'UInt64')) + 10), (date_trunc('month', `toDate(order_date)`) > '2023-04-01') AND (date_trunc('month', `toDate(order_date)`) <= '2023-12-01'))
```


Output block header: ('date', 'toUInt64 (encoded_shop_id + 10) ')

Output value: ('2023\-11\-01', 3000)

<span id="01b178d8"></span>
## Partition mapping calculation

In addition to the 1:1 mapping relationship between the original table and the destination table, there are actually 1: n, n: 1 and n: n mapping relationships. It is necessary to deduce the overwritten partition list of the destination table from the partition of the base table.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a5830607bc4141ccb93f95d56d12656a~tplv-goo7wpa0wc-image.image) </span>

Partition mapping expression, is order_list date partition, rollup to month partition, equivalent to N: 1 mapping relationship, in the construction of the refresh task insert overwrite statement is needed to determine which partition from the base table to do query to update the target table partition, the following example:

```SQL
(date_trunc('month', `toDate(order_date)`), toUInt64(multiIf(shop_id >= 2702, CAST(30000, 'UInt64'), shop_id <= 2701, CAST(40000, 'UInt64'), CAST(50000, 'UInt64')) + 10)
```



* A change was detected in the partition ('2023\-12\-06', 2703) version of the alignment base table business.order_list

* The first partition mapping calculation: to get the partition of business.order_statistics ('2023\-12\-01', 30010), you need to do insert overwrite


Since the partition is N: 1, the order_statistics partition is calculated by business order_list all 2023\-12 months of partitions together

To, so you need to determine which other partitions in business. order_list need to participate in the calculation together as data sources


* Second partition calculation: Get the list of all partitions in the current business.order_list, get the target partition list by mapping calculation, and compare it with ('2023\-12\-01', 30010). If the value is the same, it is determined to participate in the calculation of the base table partition

* Final mapping: target < ('2023\-12\-01', 30010 )\> \-\-\-\-\> source < (('2023\-12\-06', 2703), ('2023\-12\-17', 2703)) \>


NOTE:

Directly doing partition mapping calculations according to partitions will have certain restrictions on the SQL of the view and lack certain flexibility. This prompts the user to modify the SQL in the design of the tool. At the same time, the mapping calculation of partitions may cause some partitions to be overwritten. After all, all filter conditions are not considered, but the changed partitions can be overwritten.

<span id="f20f10b5"></span>
# Refresh task execution

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c42673275204ae890b92f0274655a09~tplv-goo7wpa0wc-image.image) </span>

<span id="71fc3516"></span>
## Detailed execution logic


* Get a list of current partition version information for all base tables

* Gets a list of partition version information for the last refresh saved base table

* Calculate the different sets of partition version information for the same base table, including new and deleted partitions

* If the partition of the base table that is not aligned is updated, all materialized views need to be refreshed

* If the aligned base table partition is updated, do the partition mapping and calculate the mapping relationship between the target partition and the base table partition

* Construct a refresh query according to the mapping relationship, and construct a refresh task for each update destination partition, which is added to the execution queue waiting to be executed

* The view refresh scheduler thread periodically starts to execute the refresh task according to the set time

* Refresh task execution completed, commit transaction and data, update base table update partition meta information


<span id="9ff77492"></span>
## View state table (system cnch_view_tables)

In order to better diagnose the state of the view, the view\-related information, partition current state record in the table system. cnch_view_tables.

<span id="5a34bc4a"></span>
### Definition

```SQL
CREATE TABLE system.cnch_view_tables
(
    `database` String,
    `table` String,
    `uuid` UUID,
    `vw_name` String,
    `definition` String,
    `base_tables` Array(String),
    `dependent_tables` Array(String),
    `non_dependent_tables` Array(String),
    `target_table` String,
    `partition_diffs` Array(String),
    `latest_visible_partitions` Array(String),
    `previous_partitions` Array(String),
    `refresh_type` String,
    `refresh_start_time` String,
    `refresh_interval` String,
    `active` UInt8,
    `enable_refresh` UInt8,
    `enable_query_rewrite` UInt8,
    `refresh_status` String
)
ENGINE = SystemCnchViewTables 
```


<span id="066bcc3c"></span>
### Field


|<span id="5855eacd"></span><br>#### **field name** |<span id="e1f16dd6"></span><br>#### **meaning** |
|---|---|
|Database, table, uuid, definition |View database, table name, view creation statement |
|base_tables |View dependent base table |
|dependent_tables |View refresh partition aligned base table list |
|non_dependent_tables |View refresh partition unaligned base table list |
|target_table |Destination table database & table name |
|partition_diffs |The comparison list of the partition version that has been refreshed and the current partition version, add_parittions represents the current newly added partition, drop_partitions represents the deleted partition, and the refresh will construct the corresponding refresh task according to the comparison result |
|latest_visible_partitions |Current base table latest partition version information |
|previous_partitions |Base table partition version information that has been refreshed |
|refresh_type, refresh_start_time, refresh_interval |Refresh type, startup time, refresh interval |
|Active |Is it currently valid? If you encounter modification of the base table involving the view chart, it will be set to the view invalid state, cannot be overwritten, refresh |
|enable_refresh |Whether to enable view refresh |
|enable_query_rewrite |Whether to enable view overwriting |
|refresh_status |Current view refresh task status |


<span id="dda7ce71"></span>
### Example

Query

```SQL
select * from system.cnch_view_tables where database = 'async_mv_left_join_test' and table = 'order_summary_mv';
```


Result

```SQL
database:                  async_mv_left_join_test
table:                     order_summary_mv
uuid:                      e13047fd-01b2-4a1d-86b4-dda47324b828
vw_name:                   
definition:                CREATE MATERIALIZED VIEW async_mv_left_join_test.order_summary_mv UUID 'e13047fd-01b2-4a1d-86b4-dda47324b828' TO INNER UUID '123eac1f-f19b-4363-8262-9e3063a7992c'
(
    `order_date` UInt32,
    `username` String,
    `product_name` String,
    `category` String,
    `order_amount` Decimal(10, 2),
    `price_category` String,
    `product_price` Decimal(10, 2)
)
ENGINE = CnchMergeTree
PARTITION BY order_date
ORDER BY (category, username, product_name)
REFRESH ASYNC START('2024-09-12 15:43:48') EVERY(INTERVAL 5 SECOND) AS
WITH price_categories AS
    (
        SELECT
            product_id,
            multiIf(price <= 50, 'Low', price <= 100, 'Medium', 'High') AS price_category
        FROM async_mv_left_join_test.products
    )
SELECT
    toYYYYMM(addYears(addDays(o.order_date, 2), 1)) AS order_date,
    assumeNotNull(u.username) AS username,
    p.product_name AS product_name,
    assumeNotNull(p.category) AS category,
    o.order_amount AS order_amount,
    assumeNotNull(pc.price_category) AS price_category,
    p.price AS product_price
FROM async_mv_left_join_test.orders AS o
LEFT JOIN async_mv_left_join_test.users AS u ON o.user_id = u.user_id
LEFT JOIN async_mv_left_join_test.products AS p ON o.product_id = p.product_id
LEFT JOIN
price_categories AS pc ON o.product_id = pc.product_id
WHERE (o.order_amount > 0) AND (p.price > 0)
SETTINGS max_memory_usage = 68719476736, max_threads = 8, max_memory_usage_for_user = 242292621312, exchange_queue_bytes = 1073741824, max_execution_time = 3600 PROPERTIES active = 1, base_tables = 'async_mv_left_join_test.orders,async_mv_left_join_test.products,async_mv_left_join_test.users', async_mv_refresh_execution_time = 3600, async_mv_enable_refresh_execute_serial = 1, async_mv_max_refresh_task_num = 8, async_mv_enbale_query_rewrite = 1, async_mv_enable_refresh = 1, async_mv_refresh_work_period = '00:00-23:59/1,2,3,4,5,6,7|Asia/Shanghai', async_mv_refresh_task_bsp_mode = 1

base_tables:               ['async_mv_left_join_test.users','async_mv_left_join_test.products','async_mv_left_join_test.orders']
dependent_tables:          ['async_mv_left_join_test.orders']
non_dependent_tables:      ['async_mv_left_join_test.products','async_mv_left_join_test.users']
target_table:              async_mv_left_join_test..inner_id.e13047fd-01b2-4a1d-86b4-dda47324b828
partition_diffs:           ['{"add_partitions": {},"drop_partitions": {}}']
latest_visible_partitions: ['{"version_partitions": {"async_mv_left_join_test.orders": ["partition-\'2023-05-01\', versoin-453920447620186137", "partition-\'2023-05-02\', versoin-453920447620186137", "partition-\'2023-05-03\', versoin-453920447620186137", "partition-\'2023-06-01\', versoin-453920447620186137", "partition-\'2023-06-02\', versoin-453920447620186137"],"async_mv_left_join_test.products": ["partition-202305, versoin-453920448119046158", "partition-202306, versoin-453920448119046158"],"async_mv_left_join_test.users": ["partition-202301, versoin-453920447830163476", "partition-202302, versoin-453920447830163476"]}}']
previous_partitions:       ['{"version_partitions": {"async_mv_left_join_test.users": ["partition-202301, versoin-453920447830163476", "partition-202302, versoin-453920447830163476"],"async_mv_left_join_test.products": ["partition-202305, versoin-453920448119046158", "partition-202306, versoin-453920448119046158"],"async_mv_left_join_test.orders": ["partition-\'2023-05-01\', versoin-453920447620186137", "partition-\'2023-05-02\', versoin-453920447620186137", "partition-\'2023-05-03\', versoin-453920447620186137", "partition-\'2023-06-01\', versoin-453920447620186137", "partition-\'2023-06-02\', versoin-453920447620186137"]}}']
refresh_type:              ASYNC
refresh_start_time:        2024-09-12 15:43:48
refresh_interval:          5 Second
active:                    1
enable_refresh:            1
enable_query_rewrite:      1
refresh_status:            Running
```


<span id="01ceb738"></span>
## System status view command

<span id="878952e0"></span>
### Rewrite performance query

Query

```SQL
SELECT
    materialized_views,
    query_duration_ms,
    (ProfileEvents['MvRewriteElapsedMicroseconds']) / 1000 AS rewrite_duration_ms,
    concat(formatReadableQuantity(round((((ProfileEvents['MvRewriteElapsedMicroseconds']) / 1000) / query_duration_ms) * 100, 2)), '%') AS rewrite_ratio,
    concat(formatReadableQuantity(round(((ProfileEvents['MvPartitionConsistencyCheckElapsedMicroseconds']) / (ProfileEvents['MvRewriteElapsedMicroseconds'])) * 100, 2)), '%') AS part_check_ratio,
    concat(formatReadableQuantity(round(((ProfileEvents['GetPreviousPartMetaElapsedMicroseconds']) / (ProfileEvents['MvRewriteElapsedMicroseconds'])) * 100, 2)), '%') AS get_previous_version_ratio,
    concat(formatReadableQuantity(round(((ProfileEvents['GetCurrentPartMetaElapsedMicroseconds']) / (ProfileEvents['MvRewriteElapsedMicroseconds'])) * 100, 2)), '%') AS get_current_version_ratio,
    concat(formatReadableQuantity(round(((ProfileEvents['SyncBaseTablePartitionsElapsedMicroseconds']) / (ProfileEvents['MvRewriteElapsedMicroseconds'])) * 100, 2)), '%') AS sync_partition_diff_ratio,
    concat(formatReadableQuantity(round(((ProfileEvents['TransformForAsyncElapsedMicroseconds']) / (ProfileEvents['MvRewriteElapsedMicroseconds'])) * 100, 2)), '%') AS transform_part_ratio
FROM system.query_log
WHERE (query_id = 'e1caee81-b346-4d70-84ba-057622a62dff') AND (type = 2)
```


Result

```SQL
Materialized_views: ['async_cv_1eft_join_test. order_stummary_mv ']
query_duration_ms:           1155 -- Query Time
rewrite_duration_ms:         1124.7 -- View rewriting time
rewrite_ratio:               97.38%  -- proportion of view rewriting time to total time spent
part_check_ratio:            0.92%  -- Partition check as a percentage of rewrite time
get_previous_version_ratio:  0.58%  -- Proportion of time to obtain original information of materialized partitions
get_current_version_ratio:   0.33%  -- Proportion of time to obtain current partition metadata information
sync_partition_diff_ratio:   0.92%  -- proportion of synchronous partition calculation time
transform_part_ratio:        0.00%  -- Partition conversion time ratio
```


<span id="60e8d1ed"></span>
# Refresh task load control policy

In order to avoid view refresh taking up too much resources and affecting the overall load of the cluster, some measures are needed to control the refresh load. The use of resources can be effectively balanced in the following ways.

<span id="71ec34d4"></span>
## VW resource isolation

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1da5cdb6db244a598c024cc471254d0e~tplv-goo7wpa0wc-image.image) </span>

**VW resource isolation**: Configure VW separately for refresh operation, and the table under construction can be specified.**virtual_warehouse**, the refreshed load will be calculated at the specified vw.

```SQL
CREATE MATERIALIZED VIEW async_mv_left_join_test.order_summary_mv
ENGINE = CnchMergeTree
PARTITION BY order_date
ORDER BY (category, username, product_name)
REFRESH ASYNC START('2024-09-12 15:43:48') EVERY(INTERVAL 5 SECOND) AS
WITH 
    price_categories AS (
        SELECT
            product_id,
            multiIf(
                price <= 50, 'Low',
                price <= 100, 'Medium',
                'High'
            ) as price_category
        FROM async_mv_left_join_test.products
    )
SELECT
    toYYYYMM(addYears(addDays(o.order_date, 2), 1))as order_date,
    assumeNotNull(u.username) as username,
    p.product_name as product_name,
    assumeNotNull(p.category) as category,
    o.order_amount as order_amount,
    assumeNotNull(pc.price_category) as price_category,
    p.price as product_price
FROM async_mv_left_join_test.orders o
LEFT JOIN async_mv_left_join_test.users u ON o.user_id = u.user_id
LEFT JOIN async_mv_left_join_test.products p ON o.product_id = p.product_id
LEFT JOIN price_categories pc ON o.product_id = pc.product_id
WHERE o.order_amount > 0 AND p.price > 0 
SETTINGS 
  max_memory_usage = 68719476736,
  max_threads = 8,
  virtual_warehouse = 'hdfs-staging-default', --Configure refresh vw in View Query Settings
  max_memory_usage_for_user = 242292621312,
  exchange_queue_bytes = 1073741824,
  max_execution_time = 3600 
PROPERTIES 
  async_mv_refresh_execution_time = 3600,
  async_mv_enable_refresh_execute_serial = 1,
  async_mv_max_refresh_task_num = 8,
  async_mv_enbale_query_rewrite = 1,
  async_mv_enable_refresh = 1,
  async_mv_refresh_work_period = '00:00-23:59/1,2,3,4,5,6,7|Asia/Shanghai',
  async_mv_refresh_task_bsp_mode = 1;
```


<span id="bc623105"></span>
## BSP (Bulk Synchronous Parallel) Execution Mode

ByteHouse is based on the high\-performance computing framework.**Added support for the BSP pattern: task\-level fault tolerance; more fine grained scheduling; support for resource\-aware scheduling (BORN: ByteHouse On\-premises Resource Negotiator).** The benefits are:


* When an error is encountered during query execution, the current task can be automatically retried instead of retrying from scratch. Significantly reduce retry costs.

* When the memory required by the query is huge, even larger than the memory of a single machine, the memory occupation per unit time can be reduced by increasing the degree of parallelism. Just adjust the parallelism parameter, which can theoretically be expanded indefinitely.


The bsp execution mode can be configured on the properties of the view async_mv_refresh_task_bsp_mode = 1, which is also the default execution mode.

```SQL
CREATE MATERIALIZED VIEW async_mv_left_join_test.order_summary_mv
ENGINE = CnchMergeTree
PARTITION BY order_date
ORDER BY (category, username, product_name)
REFRESH ASYNC START('2024-09-12 15:43:48') EVERY(INTERVAL 5 SECOND) AS
WITH 
    price_categories AS (
        SELECT
            product_id,
            multiIf(
                price <= 50, 'Low',
                price <= 100, 'Medium',
                'High'
            ) as price_category
        FROM async_mv_left_join_test.products
    )
SELECT
    toYYYYMM(addYears(addDays(o.order_date, 2), 1))as order_date,
    assumeNotNull(u.username) as username,
    p.product_name as product_name,
    assumeNotNull(p.category) as category,
    o.order_amount as order_amount,
    assumeNotNull(pc.price_category) as price_category,
    p.price as product_price
FROM async_mv_left_join_test.orders o
LEFT JOIN async_mv_left_join_test.users u ON o.user_id = u.user_id
LEFT JOIN async_mv_left_join_test.products p ON o.product_id = p.product_id
LEFT JOIN price_categories pc ON o.product_id = pc.product_id
WHERE o.order_amount > 0 AND p.price > 0 
SETTINGS 
  max_memory_usage = 68719476736,
  max_threads = 8,
  virtual_warehouse = 'hdfs-staging',
  max_memory_usage_for_user = 242292621312,
  exchange_queue_bytes = 1073741824,
  max_execution_time = 3600 
PROPERTIES 
  async_mv_refresh_execution_time = 3600,
  async_mv_enable_refresh_execute_serial = 1,
  async_mv_max_refresh_task_num = 8,
  async_mv_enbale_query_rewrite = 1,
  async_mv_enable_refresh = 1,
  async_mv_refresh_work_period = '00:00-23:59/1,2,3,4,5,6,7|Asia/Shanghai',
  async_mv_refresh_task_bsp_mode = 1;
```


<span id="d694c460"></span>
## View match rewrite

By expressing the query as SPJG standard form (Select\-Project\-Join\-GroupBy), the optimizer extracts various expression information, and rewrites it through a series of rules to match and rewrite it with the materialized view.

<span id="8401019d"></span>
## Ability to rewrite


|FIlter match |* Exact match<br><br>* Partial match<br><br>   * Query: `a = 1 and b = 1`View: `a = 1`<br><br>* Range matching:<br><br>   * Query: `a > 50` View: `a > 0`<br><br>   * Query: `a = 1` View: `a in (1, 2, 3)` |
|---|---|
|Join Match |* Support all Join types: left outer join/right outer join/semi/anti<br><br>* Exact match<br><br>* Support Self Join<br><br>* Partial match<br><br>   * Join compensation: Query has more Joins than MV.<br><br>   * Join elimination: Query has fewer Joins than MV, but Joins satisfy PK\-FK.<br><br>   * Join Derived: MV's Outer Join can match Query's Inner Join, etc. |
|Agg match |* Direct match<br><br>* AggregateState + Merge match<br><br>* Aggregate Rollup<br><br>   * Query: `count(d) group by a` View: `count(d) group by a, b, c` |
|Consistency check |* Partition level consistency check |
|Partial result set rewrite |* Range part rewrite<br><br>* Partition level rewrite<br><br>   If the MV contains only partial data, or if the consistency check is not satisfied, the necessary data can be read from the MV and the remaining data can be obtained from the query. |


<span id="ed5db998"></span>
## Rewrite limit


1. The view can only contain OrderBy/Aggregate/Join/Projection/Filter/TableScan, not Limit/Window, etc.

2. There is at most one Aggregate, which must be after Join, that is, Subquery cannot contain Aggregate. Note that Select Distinct in the query will be converted to Aggregate

3. If there is a non\-inner join (left join/semi join), it must be Star\-Join. Cross Join and Full Outer Join are not supported, for example, T1 left join T2 left join T3 is supported, T1 left join is not supported (T2 left join T3)


<span id="f90a963d"></span>
## Consistency check and partition level rewrite

After each refresh of the multi\-table view, the partition version information of the base table is stored in the catalog, which is used to calculate the partition diff of the next refresh, determine which partitions have been updated, and then refresh the partition level.

The optimizer view rewriting needs to obtain exactly which partitions of the original table are consistent with the materialized table partition, and which are inconsistent, and perform view rewriting.


* Get query SQL used to base table partition version list

* Get the list of corresponding partitition versions last refreshed by the base table


Two versioned partition lists are compared: different rewriting logic is performed according to whether it is a refresh dependent base table and partition comparison result

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/38f05a1786814390a3b655d0d9ccbff9~tplv-goo7wpa0wc-image.image) </span>

<span id="9c3480d7"></span>
# View hit status

In order to better perceive whether the query hits the view, the state of the view hit can be seen in different ways, as follows:

<span id="12728bb4"></span>
## TCP

Execute the query directly through cli, tcp.

```SQL
WITH price_categories AS
    (
        SELECT
            product_id,
            multiIf(price <= 50, 'Low', price <= 100, 'Medium', 'High') AS price_category
        FROM async_mv_left_join_test.products
    )
SELECT
    toYYYYMM(addYears(addDays(o.order_date, 2), 1)) AS order_date,
    assumeNotNull(u.username) AS username,
    p.product_name AS product_name,
    assumeNotNull(p.category) AS category,
    o.order_amount AS order_amount,
    assumeNotNull(pc.price_category) AS price_category,
    p.price AS product_price
FROM async_mv_left_join_test.orders AS o
LEFT JOIN async_mv_left_join_test.users AS u ON o.user_id = u.user_id
LEFT JOIN async_mv_left_join_test.products AS p ON o.product_id = p.product_id
LEFT JOIN price_categories AS pc ON o.product_id = pc.product_id
WHERE (o.order_amount > 0) AND (p.price > 0) settings enable_optimizer = 1, enable_materialized_view_rewrite =1;
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/66e9bf94f4254c0cae5d79754931cc32~tplv-goo7wpa0wc-image.image" width="2072px" /></div>


<span id="441026a5"></span>
## JSON FORMAT

Execute the query directly through cli and tcp, bring format JSON, and get whether the view is hit in the returned result data.

```SQL
WITH price_categories AS
    (
        SELECT
            product_id,
            multiIf(price <= 50, 'Low', price <= 100, 'Medium', 'High') AS price_category
        FROM async_mv_left_join_test.products
    )
SELECT
    toYYYYMM(addYears(addDays(o.order_date, 2), 1)) AS order_date,
    assumeNotNull(u.username) AS username,
    p.product_name AS product_name,
    assumeNotNull(p.category) AS category,
    o.order_amount AS order_amount,
    assumeNotNull(pc.price_category) AS price_category,
    p.price AS product_price
FROM async_mv_left_join_test.orders AS o
LEFT JOIN async_mv_left_join_test.users AS u ON o.user_id = u.user_id
LEFT JOIN async_mv_left_join_test.products AS p ON o.product_id = p.product_id
LEFT JOIN price_categories AS pc ON o.product_id = pc.product_id
WHERE (o.order_amount > 0) AND (p.price > 0) format JSON settings enable_optimizer = 1, enable_materialized_view_rewrite =1;
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4954938a9eec4cfdb55007dc1af8d6d6~tplv-goo7wpa0wc-image.image" width="1928px" /></div>


<span id="92210dae"></span>
## HTTP

Through http, in the returned result header, you can see whether the view is hit.

```SQL
echo "WITH price_categories AS (SELECT product_id, multiIf(price <= 50, 'Low', price <= 100, 'Medium', 'High') AS price_category FROM async_mv_left_join_test.products) SELECT toYYYYMM(addYears(addDays(o.order_date, 2), 1)) AS order_date, assumeNotNull(u.username) AS username, p.product_name AS product_name, assumeNotNull(p.category) AS category, o.order_amount AS order_amount, assumeNotNull(pc.price_category) AS price_category, p.price AS product_price FROM async_mv_left_join_test.orders AS o LEFT JOIN async_mv_left_join_test.users AS u ON o.user_id = u.user_id LEFT JOIN async_mv_left_join_test.products AS p ON o.product_id = p.product_id LEFT JOIN price_categories AS pc ON o.product_id = pc.product_id WHERE (o.order_amount > 0) AND (p.price > 0) format JSON settings enable_optimizer = 1, enable_materialized_view_rewrite =1" | sed 's/[[:space:]]+/ /g' | curl -is -H "X-ClickHouse-User: default" -H "X-ClickHouse-Key: P8rZPviauQIIIQIL" 'http://127.0.0.1:9477' --data-binary @-
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b1183055658b476e9a4b2596d6c013a8~tplv-goo7wpa0wc-image.image" width="2806px" /></div>


<span id="909b8805"></span>
## QueryLog

After the query finishes, you can see in the query log whether the materialized_views field query hit the view.

```SQL
SELECT *
FROM system.query_log
WHERE (query_id = 'd2c44842-3105-4f58-a43e-6547fd36a1df') AND (type = 2)
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db6515e93eb04471925303f83659e90d~tplv-goo7wpa0wc-image.image" width="3840px" /></div>


<span id="587108aa"></span>
## QueryPlan

You can get the execution logical plan through the explain command to see if the view is hit before execution.

```SQL
EXPLAIN
WITH price_categories AS
    (
        SELECT
            product_id,
            multiIf(price <= 50, 'Low', price <= 100, 'Medium', 'High') AS price_category
        FROM async_mv_left_join_test.products
    )
SELECT
    toYYYYMM(addYears(addDays(o.order_date, 2), 1)) AS order_date,
    assumeNotNull(u.username) AS username,
    p.product_name AS product_name,
    assumeNotNull(p.category) AS category,
    o.order_amount AS order_amount,
    assumeNotNull(pc.price_category) AS price_category,
    p.price AS product_price
FROM async_mv_left_join_test.orders AS o
LEFT JOIN async_mv_left_join_test.users AS u ON o.user_id = u.user_id
LEFT JOIN async_mv_left_join_test.products AS p ON o.product_id = p.product_id
LEFT JOIN price_categories AS pc ON o.product_id = pc.product_id
WHERE (o.order_amount > 0) AND (p.price > 0)
FORMAT JSON
SETTINGS enable_optimizer = 1, enable_materialized_view_rewrite = 1
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c1010d3384174cb38095070680557a9a~tplv-goo7wpa0wc-image.image" width="3812px" /></div>


<span id="9e6e1929"></span>
# Best Practices

An example of creating an asynchronous materialized view illustrates best practices for actual use.

<span id="b617d00a"></span>
## Business requirements background

A large online shopping platform that offers a wide range of goods, such as electronics, clothing, household goods, books, and sports equipment.

Business goals of data analytics:


* User behavior tracking: The platform records various user behaviors, including browsing products (view), clicking on product details (click), and purchasing products.

* Promotional activities: The platform often conducts various promotional activities, and special attention needs to be paid to the performance of the promotional products.

* Multi\-dimensional analysis: Management and marketing teams need to analyze platform performance and user behavior from multiple dimensions (e.g. date, event type, product category).


The use of asynchronous materialized views to accelerate data queries is designed to provide an efficient, multi\-dimensional data analytics tool for e\-commerce platforms, supporting all aspects from strategic decision\-making to day\-to\-day operations. It greatly improves the efficiency and flexibility of data analytics by pre\-calculating and storing key metrics, enabling business teams to quickly gain insights and make data\-driven decisions.

Data base table definition:

```SQL
--Database creation
DROP DATABASE IF EXISTS async_mv_join_agg_test;
CREATE DATABASE async_mv_join_agg_test;

--Purchase Behavior Event Table
CREATE TABLE async_mv_join_agg_test.events
(
`event_date` Date,
`event_type` String,
`user_id` UInt32,
`item_id` UInt32,
`price` Decimal(10, 2),
`quantity` UInt16,
`tags` Array(String),
`session_duration` UInt32
)
ENGINE = CnchMergeTree
PARTITION BY toStartOfMonth(event_date)
ORDER BY (event_type, user_id, item_id);

--Dimension Table for Purchasing Items
CREATE TABLE async_mv_join_agg_test.items
(
`item_id` UInt32,
`category` String,
`brand` String,
`is_promo` UInt8
)
ENGINE = CnchMergeTree
PARTITION BY item_id % 10
ORDER BY item_id;

--Event behavior data import
INSERT INTO async_mv_join_agg_test.events 
SELECT
toDate(now()) - toIntervalDay(364 - (number % 365)) AS event_date,['view', 'click', 'purchase'][1 + (number % 3)] AS event_type,1 + (number % 1000) AS user_id,1 + (number % 10000) AS item_id,round(10 + ((number * 17) % 990), 2) AS price,1 + ((number * 31) % 5) AS quantity,
arrayMap(x -> ['promo', 'sale', 'new', 'seasonal'][1 + ((number + x) % 4)], range(1 + ((number * 13) % 3))) AS tags,10 + ((number * 23) % 3590) AS session_duration
FROM numbers(1, 10000);

--Import product data
INSERT INTO async_mv_join_agg_test.items
SELECT
number AS item_id,
['Electronics', 'Clothing', 'Home', 'Books', 'Sports'][1 + (number % 5)] AS category,
['BrandA', 'BrandB', 'BrandC', 'BrandD', 'BrandE'][1 + ((number * 7) % 5)] AS brand,
number % 2 AS is_promo
FROM numbers(1, 10000);
```


<span id="f458f878"></span>
## Constructing asynchronous materialized views

<span id="a5ff2d3a"></span>
### Step 1: Determine the materialized query

It provides a comprehensive view of the e\-commerce platform, covering multiple aspects such as sales, user behavior, product performance, and marketing effectiveness. It supports data\-driven decision making and business optimization. It is necessary to build view queries to accelerate the analysis process. The following is the determination of materialized queries.

```SQL
SELECT
    toStartOfMonth(e.event_date) AS dim_event_month,
    e.event_type,
    i.category,
    count() AS event_count,
    uniqExact(e.user_id) AS unique_users,
    sum(e.price * e.quantity) AS total_revenue,
    min(e.price) AS min_price,
    max(e.price) AS max_price,
    avg(e.price) AS avg_price,
    median(e.price) AS median_price,
    quantile(0.95)(e.price) AS price_95th_percentile,
    sumMap(e.tags, arrayMap(x -> 1, e.tags)) AS tag_counts,
    groupArray(e.item_id) AS sample_items,
    countIf(e.quantity > 1) AS multi_quantity_purchases
FROM async_mv_join_agg_test.events AS e
INNER JOIN async_mv_join_agg_test.items AS i ON e.item_id = i.item_id
WHERE e.event_type IN ('view', 'click', 'purchase')
  AND e.price > 0
  AND e.price < 10000
  AND i.is_promo = 1
  AND e.session_duration < 3600 
GROUP BY toStartOfMonth(e.event_date), e.event_type, i.category;
```


<span id="2ed26983"></span>
### Step 2: Evaluate the materialized query

**EXPLAIN VALIDATE_MATERIALIZED_VIEW SQL** The explain result will show whether SQL can build a view, the reason for not building a view, the specific statement of building a view, and can automatically rewrite the relevant aggregation operator to return the column type definition required by the view, dimension column, aggregation column, recommended partition key, corresponding field name (valid_mv, reason, mv_sql, table_columns, aggregate_function_columns, dimension_columns, partition_columns).

```SQL
EXPLAIN VALIDATE_MATERIALIZED_VIEW
SELECT
  toStartOfMonth(e.event_date) AS dim_event_month,
  e.event_type AS event_type,
  i.category AS category,
  countState() AS event_count,
  uniqExactState(e.user_id) AS unique_users,
  sum(e.price * e.quantity) AS total_revenue,
  min(e.price) AS min_price,
  max(e.price) AS max_price,
  avgState(e.price) AS avg_price,
  medianState(e.price) AS median_price,
  quantileState(0.95)(e.price) AS price_95th_percentile,
  sumMap(e.tags, arrayMap(x -> 1, e.tags)) AS tag_counts,
  groupArrayState(e.item_id) AS sample_items,
  countIfState(e.quantity > 1) AS multi_quantity_purchases
FROM
  async_mv_join_agg_test.events AS e
  INNER JOIN async_mv_join_agg_test.items AS i ON e.item_id = i.item_id
WHERE
  (e.event_type IN ('view', 'click', 'purchase'))
  AND (e.price > 0)
  AND (e.price < 10000)
  AND (i.is_promo = 1)
  AND (e.session_duration < 3600)
GROUP BY
  toStartOfMonth(e.event_date),
  e.event_type,
  i.category;
```


Return result:

```SQL
valid_mv:                   1
reason:
mv_sql:                     SELECT toStartOfMonth(e.event_date) AS dim_event_month, e.event_type AS event_type, i.category AS category, countState() AS event_count, uniqExactState(e.user_id) AS unique_users, sum(e.price * e.quantity) AS total_revenue, min(e.price) AS min_price, max(e.price) AS max_price, avgState(e.price) AS avg_price, medianState(e.price) AS median_price, quantileState(0.95)(e.price) AS price_95th_percentile, sumMap(e.tags, arrayMap(x -> 1, e.tags)) AS tag_counts, groupArrayState(e.item_id) AS sample_items, countIfState(e.quantity > 1) AS multi_quantity_purchases FROM async_mv_join_agg_test.events AS e INNER JOIN async_mv_join_agg_test.items AS i ON e.item_id = i.item_id WHERE (e.event_type IN ('view', 'click', 'purchase')) AND (e.price > 0) AND (e.price < 10000) AND (i.is_promo = 1) AND (e.session_duration < 3600) GROUP BY toStartOfMonth(e.event_date), e.event_type, i.category
table_columns:              {'dim_event_month':'Date','event_type':'String','category':'String','event_count':'AggregateFunction(count)','unique_users':'AggregateFunction(uniqExact, UInt32)','total_revenue':'Decimal(38, 2)','min_price':'Decimal(10, 2)','max_price':'Decimal(10, 2)','avg_price':'AggregateFunction(avg, Decimal(10, 2))','median_price':'AggregateFunction(quantile, Decimal(10, 2))','price_95th_percentile':'AggregateFunction(quantile(0.95), Decimal(10, 2))','tag_counts':'Tuple(Array(String), Array(UInt64))','sample_items':'AggregateFunction(groupArray, UInt32)','multi_quantity_purchases':'AggregateFunction(countIf, UInt8)'}
aggregate_function_columns: {'event_count':'AggregateFunction(count)','unique_users':'AggregateFunction(uniqExact, UInt32)','total_revenue':'Decimal(38, 2)','min_price':'Decimal(10, 2)','max_price':'Decimal(10, 2)','avg_price':'AggregateFunction(avg, Decimal(10, 2))','median_price':'AggregateFunction(quantile, Decimal(10, 2))','price_95th_percentile':'AggregateFunction(quantile(0.95), Decimal(10, 2))','tag_counts':'Tuple(Array(String), Array(UInt64))','sample_items':'AggregateFunction(groupArray, UInt32)','multi_quantity_purchases':'AggregateFunction(countIf, UInt8)'}
dimension_columns:          {'dim_event_month':'Date','event_type':'String','category':'String'}
partition_columns:          ['dim_event_month']
subquery:                   0
```


<span id="570478a5"></span>
### Step 3: Build the asynchronous view

The information obtained from step 2 can be used to build an asynchronous view, and it is also necessary to determine the engine type, sort key, partition key, refresh interval, refresh start time, view refresh work time, and use refresh resource name according to business requirements.


* **Engine Type:** For asynchronous views due to refresh the minimum granularity when partitioning, generally use CnchMergeTree, there is no need to use CnchAggregatingMergeTree, because view partitions are aggregated data, there is no need for secondary aggregation, generally recommended to use implicit table construction view, can avoid creating a destination table, to avoid determining the target table column name and type, the target table and view chart bound together, the default deletion view will delete the destination table together.

* **Partition key:** In order for an asynchronous view to be built in granular increments according to partitions, the partition key of the destination table of the asynchronous view needs to be represented by the partition key of a base table in the view query, either directly or using expression transformation. In the example, choose the same partition key as the base table dim_event_month

* **Sort key:** In the query, the dimension column that appears where intermediate frequency is higher but the dimension cardinality is smaller can be used as the first ranking key. In the example, select (event_type, category)

* **Bucket configuration:** In order to speed up the query performance after view matching, you can configure the target for cluster bucketing, for the aggregation calculation of cluster key, there can be less memory occupation and shorter execution time, two or more tables for the join of cluster key can get the optimization of co\-located join, greatly reduce the amount of shuffle data and get shorter execution time, so the example can define the group by dimension column as the cluster key, bucket number according to the integer multiple of the number of pods calculated vw hdfs\-staging\-default, define


`CLUSTER BY EXPRESSION cityHash64(event_type) % 8 INTO 8 BUCKETS`


* **Refresh interval:** According to actual business needs, determine the refresh interval, recommended minute level, 1 minute\ 5 minutes, favorable refresh task fails to retry

* **start time**: According to actual business needs, if the set time is earlier than the creation time, the refresh will be started immediately, or the future start time will be scheduled

* **working hours**: If there is no separate vw resource for view refresh, in order not to affect the normal query load during working hours view refresh, you can configure the view to run during low peaks, for example: set async_mv_refresh_work_period = '21:00\-23:59/1,2,3,4,5,6,7; 00:00\-08:59/1,2,3,4,5,6,7 | Asia/Shanghai', if there is a separate refresh vw resource, no need to configure or configure all\-day running async_mv_refresh_work_period = '00:00\-23:59/1,2,3,4,5,6,7 | Asia/Shanghai'.

* **View query configuration:** View refresh requires stability, can accept longer running time, use lower resources, so according to the refresh resource configuration reasonable settings query configuration, in order to isolate the refresh load, you can configure virtual_warehouse specifically for refresh, the recommended configuration is as follows:


```SQL
SETTINGS
  max_memory_usage = 68719476736,
  max_threads = 8,
  virtual_warehouse = 'hdfs-staging-default',
  max_memory_usage_for_user = 242292621312,
  exchange_queue_bytes = 1073741824,
  max_execution_time = 3600
```



* **View properties:** Generally, in order to reduce the resource occupied by the view, the view will be run serially, and the parallelism configuration is relatively low. Turn on view refresh and rewrite, and set the bsp operation mode. The recommended configuration is as follows:


```SQL
PROPERTIES 
  async_mv_enable_refresh_execute_serial = 1,
  async_mv_max_refresh_task_num = 8,
  async_mv_enbale_query_rewrite = 1,
  async_mv_enable_refresh = 1,
  async_mv_refresh_work_period = '00:00-23:59/1,2,3,4,5,6,7|Asia/Shanghai',
  async_mv_refresh_task_bsp_mode = 1;
```


**Finalize the view definition (pay attention to the naming of aliases during the definition of views, which can be modified as needed)** 

```SQL
CREATE MATERIALIZED VIEW async_mv_join_agg_test.events_items_summary
ENGINE = CnchMergeTree
PARTITION BY dim_event_month
CLUSTER BY EXPRESSION cityHash64(event_type) % 8 INTO 8 BUCKETS
ORDER BY (event_type, category)
REFRESH ASYNC START('2024-11-01 15:43:48') EVERY(INTERVAL 1 MINUTE) AS
SELECT
  toStartOfMonth(e.event_date) AS dim_event_month,
  e.event_type AS event_type,
  i.category AS category,
  countState() AS event_count,
  uniqExactState(e.user_id) AS unique_users,
  sum(e.price * e.quantity) AS total_revenue,
  min(e.price) AS min_price,
  max(e.price) AS max_price,
  avgState(e.price) AS avg_price,
  medianState(e.price) AS median_price,
  quantileState(0.95)(e.price) AS price_95th_percentile,
  sumMap(e.tags, arrayMap(x -> 1, e.tags)) AS tag_counts,
  groupArrayState(e.item_id) AS sample_items,
  countIfState(e.quantity > 1) AS multi_quantity_purchases
FROM
  async_mv_join_agg_test.events AS e
  INNER JOIN async_mv_join_agg_test.items AS i ON e.item_id = i.item_id
WHERE
  (e.event_type IN ('view', 'click', 'purchase'))
  AND (e.price > 0)
  AND (e.price < 10000)
  AND (i.is_promo = 1)
  AND (e.session_duration < 3600)
GROUP BY
  toStartOfMonth(e.event_date),
  e.event_type,
  i.category
SETTINGS max_memory_usage = 68719476736,
  max_threads = 8,
  virtual_warehouse = 'hdfs-staging-default',
  max_memory_usage_for_user = 242292621312,
  exchange_queue_bytes = 1073741824,
  max_execution_time = 3600 
PROPERTIES 
  async_mv_enable_refresh_execute_serial = 1,
  async_mv_max_refresh_task_num = 8,
  async_mv_enbale_query_rewrite = 1,
  async_mv_enable_refresh = 1,
  async_mv_refresh_work_period = '00:00-23:59/1,2,3,4,5,6,7|Asia/Shanghai',
  async_mv_refresh_task_bsp_mode = 1;
```


<span id="0ebe6f67"></span>
### Step 4: Configure the global queue

In order to ensure that the view refresh task resource load remains manageable, it is necessary to configure the global queue maximum concurrency of view refresh tasks to ensure that all view submitted tasks run under a limited number of tasks. The recommended configuration is as follows:

```SQL
--Add matching rule, query id contains async_defresh, match in high queue
ALTER WAREHOUSE `hdfs-staging-default` ADD RULE SET query_id = '.*async_refresh.*' , rule_name = 'async_mv_refresh_rule' WHERE queue_name = 'highest';

--Update the waiting queue length for high to 30
ALTER WAREHOUSE `hdfs-staging-default` MODIFY RULE SET query_queue_size = 30 WHERE queue_name = 'highest';

---The maximum concurrent number for updating view refresh tasks is 6
ALTER WAREHOUSE `hdfs-staging-default` MODIFY RULE SET max_concurrency = 6 WHERE queue_name = 'highest';

---Check if this is correct
SELECT * FROM system.virtual_warehouse_queue WHERE rule_name = 'async_mv_refresh_rule';
```


<span id="bc93b739"></span>
### Step 5: Monitor view running


* **View view status**


By querying the system table to determine the running state of the view system.cnch_view_tables, you can see that some partitions are not materialized, the execution status of the task, the relevant view definition, and the information of the base table and the alignment table. The destination table will automatically build the name:`async_mv_join_agg_test.`.inner_id.173bf69a\-653d\-4cb6\-9830\-d3c71efba0ca``

Implicit view object table naming rules: inner_id + materialized_view_uuid

```SQL
select * from system.cnch_view_tables where database = 'async_mv_join_agg_test' and table = 'events_items_summary';
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb6ac99e3ab043b7944c303040b73ec4~tplv-goo7wpa0wc-image.image" width="3798px" /></div>


Waiting for add_partitions in partition_diffs, drop_partitions are empty indicates that the view has been refreshed.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0289a3f010a94ef385117d307bba684e~tplv-goo7wpa0wc-image.image" width="3828px" /></div>



* **View refresh task status**


Query the latest 10 completed tasks:

```SQL
SELECT *
FROM cnch_system.cnch_view_refresh_task_log
WHERE (database = 'async_mv_join_agg_test') AND (view = 'events_items_summary') AND (status >= 2) and event_date = today() 
ORDER BY event_time_microseconds DESC
LIMIT 10;
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/50d77ea5fcc940de8069d2fdce81c604~tplv-goo7wpa0wc-image.image" width="3830px" /></div>


According to the task QueryId, further execution status can be obtained in the query log:

```SQL
select
  *
from
  cnch(`hdfs-staging-default`, system.query_log)
where
  initial_query_id = '4c4b447b-4011-4a22-b6c2-e418cdc8a2f5_async_refresh_async_mv_join_agg_test.events_items_summary'
  and type >= 2;
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e1dc884cfc7e4511a36b6255c78a9d7f~tplv-goo7wpa0wc-image.image" width="3840px" /></div>


Query whether there is any exception in the execution of the task today:

```SQL
SELECT *
FROM cnch_system.cnch_view_refresh_task_log
WHERE (database = 'async_mv_join_agg_test') AND (view = 'events_items_summary') AND notEmpty(exception)
ORDER BY event_time_microseconds DESC
LIMIT 10;
```



* **Verify query match**


Execute the daily query of the business, the business will generally use format JSON to get whether the view is hit in the returned results, and check whether the query results are consistent by turning off view matching and turning on view matching.

**enable_materialized_view_rewrite = 1**

```SQL
-- 开启视图匹配(with materialized view rewrite enabled)
SELECT
    e.event_type AS event_type,
    i.category AS category,
    count() AS event_count,
    sum(e.price * e.quantity) AS total_revenue,
    min(e.price) AS min_price,
    max(e.price) AS max_price,
    avg(e.price) AS avg_price
FROM async_mv_join_agg_test.events AS e
INNER JOIN async_mv_join_agg_test.items AS i ON e.item_id = i.item_id
WHERE (e.event_type IN ('view')) AND (e.price > 0) AND (e.price < 10000) AND (i.is_promo = 1) AND (e.session_duration < 3600)
GROUP BY
    e.event_type,
    i.category
ORDER BY
    e.event_type ASC,
    i.category ASC
LIMIT 10
SETTINGS enable_optimizer = 1, enable_materialized_view_rewrite = 1 format JSON;
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/93e7d0ea753248b98f46604e9317e5ad~tplv-goo7wpa0wc-image.image" width="750px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca898586664e4175bb0279ae7e853fe6~tplv-goo7wpa0wc-image.image" width="754px" /></div>


**enable_materialized_view_rewrite = 0**

```SQL
-- Disable view match (with materialized view rewrite disabled)
SELECT
    e.event_type AS event_type,
    i.category AS category,
    count() AS event_count,
    sum(e.price * e.quantity) AS total_revenue,
    min(e.price) AS min_price,
    max(e.price) AS max_price,
    avg(e.price) AS avg_price
FROM async_mv_join_agg_test.events AS e
INNER JOIN async_mv_join_agg_test.items AS i ON e.item_id = i.item_id
WHERE (e.event_type IN ('view')) AND (e.price > 0) AND (e.price < 10000) AND (i.is_promo = 1) AND (e.session_duration < 3600)
GROUP BY
    e.event_type,
    i.category
ORDER BY
    e.event_type ASC,
    i.category ASC
LIMIT 10
SETTINGS enable_optimizer = 1, enable_materialized_view_rewrite = 0 format JSON;
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b871f1c1e834993899ae83293ff9ab5~tplv-goo7wpa0wc-image.image" width="842px" /></div>


The query results are consistent, indicating that the matching and rewriting are successful.


* **View the rewritten execution plan**


```C++
EXPLAIN
SELECT
    e.event_type AS event_type,
    i.category AS category,
    count() AS event_count,
    sum(e.price * e.quantity) AS total_revenue,
    min(e.price) AS min_price,
    max(e.price) AS max_price,
    avg(e.price) AS avg_price
FROM async_mv_join_agg_test.events AS e
INNER JOIN async_mv_join_agg_test.items AS i ON e.item_id = i.item_id
WHERE (e.event_type IN ('view')) AND (e.price > 0) AND (e.price < 10000) AND (i.is_promo = 1) AND (e.session_duration < 3600)
GROUP BY
    e.event_type,
    i.category
ORDER BY
    e.event_type ASC,
    i.category ASC
LIMIT 10
SETTINGS enable_optimizer = 1, enable_materialized_view_rewrite = 1
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/260b76b1ed1f40e49a51c7e1053ec9a2~tplv-goo7wpa0wc-image.image" width="3830px" /></div>


&nbsp;
