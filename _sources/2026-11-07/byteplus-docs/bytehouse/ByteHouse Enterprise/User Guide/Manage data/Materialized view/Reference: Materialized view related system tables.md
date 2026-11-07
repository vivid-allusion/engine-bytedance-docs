---
title: "Reference: Materialized view related system tables"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/reference-materialized-view-related-system-tables"
---

<span id="46252594"></span>
# Related System Tables

<span id="08c480d2"></span>
## View State Table \- system.view_tables

<span id="9f2656fe"></span>
### Definition

```SQL
CREATE TABLE system.view_tables
(
    `database` String,
    `table` String,
    `uuid` UUID,
    `definition` String,
    `base_table_databases` Array(String),
    `base_table_tables` Array(String),
    `dependent_table_databases` Array(String),
    `dependent_table_tables` Array(String),
    `target_table_database` String,
    `target_table_table` String,
    `partition_diffs` Array(String),
    `latest_visible_partitions` Array(String),
    `previous_partitions` Array(String),
    `refresh_type` String,
    `refresh_start_time` String,
    `refresh_interval` String,
    `active` UInt8,
    `coordinator_address` String,
    `refresh_status` String
)
ENGINE = SystemViewTables
```


<span id="7ddf1c04"></span>
### Field


* Database, Table, uuid, definition \- database, table name, and the view creation statement.

* base_table_databases, base_table_tables \- base tables on which the view depends.

* dependent_table_databases, dependent_table_tables \- list of base tables aligned for the view refresh partitions.

* target_table_database, target_table_table \- destination table's database and table name.

* partition_diffs \- list of partition difference in the current view refresh from the last, with add_partitions representing new added partitions and drop_partitions representing current deleted partitions; the refresh constructs different refresh tasks based on the diffs list.

* latest_visible_partitions \- Information on partitions in the current view.

* previous_partitions \- Information on partitions stored in MySQL from the last refresh.

* refresh_type, refresh_start_time, refresh_interval \- The type of refresh, launch time, and refresh intervals.

* active \- Whether it is currently active. If modifications to the base table involve the view table, it will be set to an invalid view state, preventing rewriting, refreshing, and modifications to the invalid view state, unless deleted and rebuilt.

* coordinator_address \- The address information of the coordinator for the refresh task.

* refresh_status \- Whether the current refresh task is running, number of running tasks, 'Running', 'running_tasks'.


<span id="be2aadfd"></span>
### Example

```SQL
database:                  business_v2
table:                     goods_mv
uuid:                      6d96110d-931c-4436-b5fa-ee69c981a4f9
definition:                CREATE MATERIALIZED VIEW business_v2.goods_mv UUID '6d96110d-931c-4436-b5fa-ee69c981a4f9' TO business_v2.goods_info (`date` Date, `series_id` UInt64, `goods_id` Int64, `total_price` Float64, `max_price` Float64) REFRESH ASYNC START('2024-04-01 10:00:00') EVERY(INTERVAL 1 MINUTE) AS SELECT toDate(create_date) AS date, series_id, goods_id, sum(price) AS total_price, max(price) AS max_price FROM business_v2.goods WHERE date > '2024-01-01' GROUP BY date, series_id, goods_id properties async_mv_partition_refresh_max_limit = 10
base_table_databases:      ['business_v2']
base_table_tables:         ['goods']
dependent_table_databases: ['business_v2']
dependent_table_tables:    ['goods']
target_table_database:     business_v2
target_table_table:        goods_info
partition_diffs:           ['depend_storage_id: business_v2.goods (ef94f3c8-c8e2-40cf-92dc-0862a0f15a4c), add_partitions: [partition-\'2024-04-14\', versoins-5, -1, ], drop_partitions: []']
latest_visible_partitions: ['business_v2.goods:partition-\'2024-04-14\', versoins-5, -1|partition-\'2024-04-13\', versoins-4, -1']
previous_partitions:       ['business_v2.goods:partition-\'2024-04-13\', versoins-4, -1']
refresh_type:              ASYNC
refresh_start_time:        2024-04-01 10:00:00
refresh_interval:          1 Minute
active:                    1
coordinator_address:       host: 10.232.201.68,exchange_port: 9520,fabric_port: 12399
refresh_status:            running : true, running_tasks: 0
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d544e246a7644df4b41045534adb4dea~tplv-goo7wpa0wc-image.image" width="2714px" /></div>


<span id="2edc95d4"></span>
## Refresh task status table \- system.view_refresh_task_log

<span id="d68fd0a4"></span>
### Definition

```SQL
CREATE TABLE system.view_refresh_task_log
(
    `database` String,
    `view` String,
    `status` Enum8('START' = 1, 'FINISH' = 2, 'EXCEPTION_EXECUTE_TASK' = 3, 'EXCEPTION_BEFORE_START' = 4),
    `refresh_type` Enum8('NONE' = 1, 'PARTITION_REFRESH' = 2, 'FULL_REFRESH' = 3),
    `refresh_mode` Enum8('LOCAL_SYNC' = 1, 'GAOBAL_ASYNC' = 2),
    `event_date` Date,
    `event_time` DateTime,
    `event_time_microseconds` DateTime64(6),
    `duration_ms` UInt64,
    `exception` String,
    `partition_map` String,
    `insert_overwrite_query` String,
    `query_id` String,
    `insert_overwrite_query_id` String,
    `local_task_partition` String,
    `local_task_query` Map(String, String) KV
)
ENGINE = MergeTree
PARTITION BY toYYYYMM(event_date)
ORDER BY (event_date, event_time)
SETTINGS index_granularity = 8192;
```


<span id="1a24d836"></span>
### Field


* Database, view \- Database.table name.

* Status \- Refresh task status, including START, FINISH, EXCEPTION_EXECUTE_TASK, EXCEPTION_BEFORE_START.

* Refresh_type \- The refresh task type, PARTITION_REFRESH indicates the task refreshes according to partition granularity, FULL_REFRESH indicates the task refreshes all partitions.

* Refresh_mode \- Refresh task mode, LOCAL_SYNC represents synchronous local refresh, LOCAL_ASYNC represents asynchronous local refresh, DISTRIBUTED_ASYNC represents distributed asynchronous refresh (tasks type of asynchronous views).

* Event_date, event_time \- Time of execution.

* Duration_ms \- Execution duration.

* Exception \- Exception information.

* Partition_map \- The DISTRIBUTED_ASYNC type calculates the partition mapping relationship, and the destination table uses which base tables to calculate.

* Insert_overwrite_query \- Refresh task insert overwrite statement.

* Query_id \- Task query id.

* insert_overwrite_query_id \- The query ID for executing insert overwrite.

* local_task_partition \- Partition information for LOCAL_SYNC.

* local_task_query \- Information about the query executed in the LOCAL_SYNC view, Key: query_id, Value: query.


<span id="454d006f"></span>
### Example

<span id="a341b20f"></span>
#### Asynchronous view task

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f321e41f2594fc18975a42b1269b416~tplv-goo7wpa0wc-image.image" width="3832px" /></div>


<span id="b1ef2c7f"></span>
#### Synchronous view task

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/51354018323e452a962cde6dd44ba564~tplv-goo7wpa0wc-image.image" width="3828px" /></div>


<span id="85f65633"></span>
#### Retrieve the coordinator node's host address

```SQL
SELECT concat(if(isIPv6String(cluster.host_name), '[', ''), cluster.host_name, if(isIPv6String(cluster.host_name), ']', ''), ':', cluster.port) AS coodinator_address
FROM
(
    SELECT regexpExtract(coordinator_address, 'host: ([a-fA-F0-9:.]+)', 1) AS extracted_ip
    FROM system.view_tables
    WHERE (table = 'mv_1') AND (database = 'test')
) AS coodinator
INNER JOIN
(
    SELECT
        host_name,
        port
    FROM system.clusters
) AS cluster ON coodinator.extracted_ip = cluster.host_name
```


<span id="49ade16a"></span>
#### Read view_refresh_task_log from the coordinator node

```SQL
SELECT *
FROM remote('[fdbd:dc61:1a:393::30]:9030', system, view_refresh_task_log, 'default', 'P8rZPviauQIIIQIL')
WHERE event_date = today() and view = 'event_statistics_optimize_mv' and database = 'governance_vision_realtime_db';
```


Create system.view_refresh_task_log directly on each node

```SQL
CREATE TABLE system.view_refresh_task_log on cluster ch_rd_dev_mv_test
(
    `database` String,
    `view` String,
    `status` Enum8('START' = 1, 'FINISH' = 2, 'EXCEPTION_EXECUTE_TASK' = 3, 'EXCEPTION_BEFORE_START' = 4),
    `refresh_type` Enum8('NONE' = 1, 'PARTITION_REFRESH' = 2, 'FULL_REFRESH' = 3),
    `refresh_mode` Enum8('LOCAL_SYNC' = 1, 'GAOBAL_ASYNC' = 2),
    `event_date` Date,
    `event_time` DateTime,
    `duration_ms` UInt64,
    `exception` String,
    `partition_map` String,
    `insert_overwrite_query` String,
    `query_id` String,
    `insert_overwrite_query_id` String,
    `local_task_partition` String,
    `local_task_query` Map(String, String) KV
)
ENGINE = MergeTree
PARTITION BY toYYYYMM(event_date)
ORDER BY (event_date, event_time)
SETTINGS index_granularity = 8192;
```


<span id="905c21dc"></span>
# View hit state

<span id="f78068bb"></span>
## TCP

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6c33464647f3486e8314ef6d14076dcd~tplv-goo7wpa0wc-image.image" width="2372px" /></div>


<span id="ba01d6a1"></span>
## JSON FORMAT

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b19b0653d63249b7ba3f43f14a931690~tplv-goo7wpa0wc-image.image" width="1886px" /></div>


<span id="07a8627b"></span>
## HTTP

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/051edb7f9ff241539545f8363843d831~tplv-goo7wpa0wc-image.image" width="1780px" /></div>
