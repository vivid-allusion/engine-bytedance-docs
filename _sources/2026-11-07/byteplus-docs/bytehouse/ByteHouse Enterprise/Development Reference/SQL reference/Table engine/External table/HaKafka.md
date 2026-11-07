---
title: "HaKafka"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/hakafka"
---

HaKafka is a special table engine, modified from the community Kafka engine. Using Kafka / HaKafka engines allows subscribing to topics on Kafka, pulling and parsing messages from the topic, then writing the data parsed from Kafka/HaKafka into the target table (usually HaMergeTree) through MaterializedView.
In ByteHouse GUI, creating a Kafka import task is essentially creating two tables, HaKafka and MaterializedView.
![Image](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f8b2f9e6047ebe5a1a753bac54c1096d.png =1408x)
In ByteHouse, the community's Kafka engine has basically not been modified and lacks high availability features; it is not recommended to use it. The following only introduces HaKafka.
<span id="建表示例"></span>
# Creating table example
<span id="sql-建表"></span>
## SQL create table
<span id="建表语法"></span>
### Create table syntax
The syntax to create a HaKafka table is as follows:
```sql
CREATE TABLE [IF NOT EXISTS] [db.]table_name [ON CLUSTER cluster]
(
    name1 [type1] [DEFAULT|MATERIALIZED|ALIAS expr1],
    name2 [type2] [DEFAULT|MATERIALIZED|ALIAS expr2],
    ...
) ENGINE = HaKafka('{shard}', '{replica}')
SETTINGS (.....)
```

<span id="settings"></span>
### SETTINGS

| | | | | \
|**Parameter Name** |**Type** |**REQUIRED/Default** |**Description** |
|---|---|---|---|
| | | | | \
|kafka_broker_list |String |REQUIRED |ip:port。 Multiple entries allowed, separated by commas |
| | | | | \
|kafka_topic_list |String |REQUIRED |Multiple allowed, separated by commas. |
| | | | | \
|kafka_group_name |String |REQUIRED |Consumer group name. |
| | | | | \
|kafka_format |String |REQUIRED |Message format; currently, JSONEachRow is most commonly used. |
| | | | | \
|kafka_row_delimiter |String |'\0' |Generally use '\n'. |
| | | | | \
|kafka_schema |String |'' |Protobuf format requires this parameter. |
| | | | | \
|kafka_num_consumers |UInt64 |1 |Number of consumers, each consumer will create a thread. |\
| | | |It is recommended to set it to 1 - 4, with each thread having a write performance of about 20MB/s. |
| | | | | \
|kafka_max_block_size |UInt64 |65536 |Write block_size |\
| | | |Default 65536 MB |
| | | | | \
|kafka_leader_priority |String |'0' |They will be stored on zk, as a pair of consumers acting as primary and backup where only the one with the smallest leader_priority will activate consumption. Tables on other nodes will not consume. Can be replaced by a macro. |
| | | | | \
|kafka_partition_num |String |'-1' |'-1' indicates the use of dynamic allocation (kafka subscribe API); |\
| | | |'>= 0' indicates the use of static allocation (kafka assign API). |
| | | | | \
|kafka_shard_count |String |'1' |The number of shards in a cluster determines the rules for static allocation. |
| | | | | \
|kafka_auto_offset_reset |String |'' |When launching consumption or when data expires, you can set the offset as "earliest" or "latest". |
| | | | | \
|extra_librdkafka_config |String |'' |JSON format; can pass any parameters supported by librdkafka. Please refer to: https://github.com/edenhill/librdkafka/blob/master/CONFIGURATION.md. |

<span id="影响-hakafka-的-users-xml-参数"></span>
### Parameters in users.xml affecting HaKafka

| | | | \
|**Name** |**Default** |**Description** |
|---|---|---|
| | | | \
|stream_flush_interval_ms |7500 |ms, timeout time for polling data after consuming each batch. |
| | | | \
|stream_poll_timeout_ms |500 |ms, wait time for polling rdkafka data, affecting stop consume and Timeout judge. |
| | | | \
|kafka_session_timeout_ms |180000 |ms, Kafka session timeout time, only activates during static assignment. |
| | | | \
|kafka_max_partition_fetch_bytes |1048576 |Bytes, the max size of data fetched from topic partition, affects the performance of POLL data. |

<span id="使用示例"></span>
# Use Example
<span id="手动建导入任务"></span>
## Create Import tasks manually
You can create import tasks automatically through the control panel; however, if you need to manually create them, you must create a HaKafka table, a Materialized View, and a HaMergeTree (or HaUniqueMergeTree) base table. The following demonstrates an example of creating tables manually.
<span id="步骤1：建-hakafka-表"></span>
### Step 1: Create a HaKafka table
```sql
CREATE TABLE TEST.CONSUMER_tce_service_resource_usage_local ON CLUSTER default (
    `current_ts` Int64,
    `psm` String,
    `cpu_limit_pod` Float64
) ENGINE = HaKafka('/clickhouse/experiment/TEST.CONSUMER_tce_service_resource_usage_local_233/{shard}', '{replica}')
SETTINGS 
    kafka_cluster = 'xxx_cluster',  -- Replace with the Kafka cluster name.
    kafka_topic_list = 'xxx_topic', -- Replace with the business topic.
    kafka_group_name = 'xxx_group_name', -- Replace with the desired group name.
    kafka_format = 'JSONEachRow', -- Generally use JSON.
    kafka_row_delimiter = '\n', -- Usually '\n'.
```

After the table is created, you can directly select data from it (generally used for Debug, not for production use)
```sql
SELECT * FROM TEST.CONSUMER_tce_service_resource_usage_local LIMIT 3 FORMAT CSVWithNames;
-- "current_ts","psm","cpu_limit_pod"

-- 1567666740,"toutiao.video.user_packer",4

-- 1567666740,"ad.bi.datacore",4

-- 1567666740,"tce.sysprobe.probeagent",2
```

<span id="步骤2-建本地表与物化视图表"></span>
### Step 2 Create local table and Materialized view table
A HaKafka table defines how to consume (analyze) data from a Kafka topic. To write the data to disk, you need to create a target table powered by HaMergeTree engine (or HaUniqueMergeTree), and a materialized view as well.
```sql
--- Prepare a HaMergeTree table for storing data.
CREATE TABLE TEST.tce_service_resource_usage_local ON CLUSTER default (
    `current_ts` Int64,
    `psm` String,
    `cpu_limit_pod` Float64
) ENGINE = HaMergeTree('/clickhouse/experiment/TEST.tce_service_resource_usage_local_666/{shard}', '{replica}')
PARTITION BY toDate(current_ts) ORDER BY psm

--- Then create a materialized view, which means selecting data from the HaKafka table and writing it into the HaMergeTree table.
CREATE MATERIALIZED VIEW TEST.VIEW_tce_service_resource_usage_local ON CLUSTER default
TO TEST.tce_service_resource_usage_local
AS SELECT 
    current_ts,  
    psm, 
    cpu_limit_pod 
    FROM TEST.CONSUMER_TEST_tce_service_resource_usage_local
```

After creating the three tables, the data will be written to the target table periodically (depending on the stream_flush_interval_ms parameter and the data persistence time). Afterwards, just search the target table.
<span id="其他操作"></span>
# Other actions
<span id="开启-关闭-重启消费"></span>
## Activate / Terminate / Restart consumption
**SQL syntax:**
```sql
SYSTEM START/STOP/RESTART CONSUME 
```

**Meaning:**
Activate/Terminate/Restart consumption of the HaKafka engine. This will change the consumption state of the HaKafka table (ON/OFF), and persist it on the disk; the original state will be maintained even after a restart.

1. All three actions are idempotent and can be performed multiple times. Multiples START/STOP only take effect the first time, while multiple RESTARTs take effect every time.
2. STOP/RESTART will **destroy the current consumer**.
3. Consumption can be checked through the consumer_switch field in system.kafka_tables to see if it is activated or terminated.

<span id="更改设置"></span>
## Modify settings
You can change HaKafka table settings using the following statement; after modifications, consumption will automatically restart.
```sql
ALTER TABLE db.table MODIFY SETTING  = ,  = 
```

<span id="virtual-columns"></span>
## Virtual columns
Some business users need to obtain Kafka message metadata (e.g., message partition, offset, and others). We can use the virtual columns function to meet this requirement. Virtual columns do not need to be specified when creating tables; they are an inherent attribute of the table engine. When querying with a SELECT statement, virtual columns can be explicitly selected (they can also be included in the SELECT statement of a VIEW table):
```sql
-- 
SELECT 
    _topic,    -- String
    _partition,    -- UInt64
    _key,    -- String
    _offset,    -- UInt64
    _content,  -- String: The complete message content
    *    -- Normal columns can be expanded using *, but virtual columns cannot.
FROM TEST.CONSUMER_tce_service_resource_usage_local LIMIT 10
```
