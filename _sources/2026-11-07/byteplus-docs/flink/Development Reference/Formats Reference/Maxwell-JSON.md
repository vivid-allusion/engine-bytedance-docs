---
title: "Maxwell-JSON"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Maxwell-JSON"
---

Maxwell is a Change Data Capture tool that can stream changes from MySQL to Kafka, Kinesis, and other streaming connectors in real time. Maxwell provides a unified format schema for change logs and supports using JSON to serialize messages.

Flink supports interpreting Maxwell\-JSON messages as INSERT/UPDATE/DELETE messages in the Flink SQL system. In many cases, this functionality is very useful, for example:


* Synchronizing incremental data from a database to other systems.

* Log auditing.

* Real\-time materialized views of the database.

* Associating the change history of dimension databases and more.


Flink also supports encoding INSERT/UPDATE/DELETE messages in Flink SQL into Maxwell\-JSON messages and sending them to external systems like Kafka. Currently, Flink cannot combine UPDATE_BEFORE and UPDATE_AFTER into a single UPDATE message. Therefore, Flink encodes UPDATE_BEFORE and UDPATE_AFTER as DELETE and INSERT Maxwell messages.

<span id="14774cb0"></span>
## How to Use Maxwell\-JSON

Maxwell provides a unified format for the change log, here is a simple example of an UPDATE operation captured from the MySQL product table in JSON format:

```JSON
{
   "database":"test",
   "table":"e",
   "type":"insert",
   "ts":1477053217,
   "xid":23396,
   "commit":true,
   "position":"master.000006:800911",
   "server_id":23042,
   "thread_id":108,
   "primary_key": [1, "2016-10-21 05:33:37.523000"],
   "primary_key_columns": ["id", "c"],
   "data":{
     "id":111,
     "name":"scooter",
     "description":"Big 2-wheel scooter",
     "weight":5.15
   },
   "old":{
     "weight":5.18,
   }
}
```


The MySQL product table has 4 columns (`id`, `name`, `description`, `weight`). The JSON message above is an update event on the `products` table, where the `id = 111` row's `weight` value changed from `5.18` to `5.15`. If this message has been synchronized to the Kafka topic `products_binlog`, you can use the following DDL to use this topic and parse the change events.

```SQL
CREATE TABLE topic_products (
  -- schema is totally the same to the MySQL "products" table
  id BIGINT,
  name STRING,
  description STRING,
  weight DECIMAL(10, 2)
) WITH (
 'connector' = 'kafka',
 'topic' = 'products_binlog',
 'properties.bootstrap.servers' = 'localhost:9092',
 'properties.group.id' = 'testGroup',
 'format' = 'maxwell-json'
)
```


After registering the topic as a Flink table, you can use Maxwell messages as a change log source.

```SQL
-- a real-time materialized view on the MySQL "products"
-- which calculate the latest average of weight for the same products
SELECT name, AVG(weight) FROM topic_products GROUP BY name;

-- synchronize all the data and incremental changes of MySQL "products" table to
-- Elasticsearch "products" index for future searching
INSERT INTO elasticsearch_products
SELECT * FROM topic_products;
```


<span id="055b32b6"></span>
## Available Metadata

The following format metadata can be exposed as read\-only (`VIRTUAL`) columns in the table definition.

Note: Format metadata fields are only available when the corresponding connector supports them. Currently, only the Kafka connector can expose format metadata fields.


|Key |Data Type |Description |
|---|---|---|
|`database` |`STRING NULL` |Original database. Corresponds to the `database` field in Maxwell records (if available). |
|`table` |`STRING NULL` |Original database table. Corresponds to the `table` field in Maxwell records (if available). |
|`primary-key-columns` |`ARRAY<STRING> NULL` |Array of primary key names. Corresponds to the `primary-key-columns` field in Maxwell records (if available). |
|`ingestion-timestamp` |`TIMESTAMP_LTZ(3) NULL` |Timestamp when the connector processes the event. Corresponds to the `ts` field in the Maxwell record. |


The following example demonstrates how to access Maxwell metadata fields in Kafka:

```SQL
CREATE TABLE KafkaTable (
  origin_database STRING METADATA FROM 'value.database' VIRTUAL,
  origin_table STRING METADATA FROM 'value.table' VIRTUAL,
  origin_primary_key_columns ARRAY<STRING> METADATA FROM 'value.primary-key-columns' VIRTUAL,
  origin_ts TIMESTAMP(3) METADATA FROM 'value.ingestion-timestamp' VIRTUAL,
  user_id BIGINT,
  item_id BIGINT,
  behavior STRING
) WITH (
  'connector' = 'kafka',
  'topic' = 'user_behavior',
  'properties.bootstrap.servers' = 'localhost:9092',
  'properties.group.id' = 'testGroup',
  'scan.startup.mode' = 'earliest-offset',
  'value.format' = 'maxwell-json'
);
```


<span id="16be044b"></span>
## Format Parameters


|Parameter |Required |Default Value |Type |Description |
|---|---|---|---|---|
|<span id="873172f7"></span><br>##### format |required |(none) |String |Specify the format to use, here it should be `'maxwell-json'`. |
|<span id="b87c7d79"></span><br>##### maxwell\-json.ignore\-parse\-errors |optional |false |Boolean |Skip fields and rows with parsing errors instead of failing. If an error occurs, the field will be set to `null`. |
|<span id="f6343ac0"></span><br>##### maxwell\-json.timestamp\-format.standard |optional |`'SQL'` |String |Declare the input and output timestamp formats. Current supported formats include `'SQL'` and `'ISO-8601'`:<br><br><br>* Optional parameter `'SQL'` will parse timestamps in the format "yyyy\-MM\-dd HH:mm:ss.s{precision}", such as '2020\-12\-30 12:13:14.123', and will output in the same format.<br><br>* Optional parameter `'ISO-8601'` will parse input timestamps in the format "yyyy\-MM\-ddTHH:mm:ss.s{precision}", such as '2020\-12\-30T12:13:14.123', and will output in the same format. |
|<span id="127e5d96"></span><br>##### maxwell\-json.map\-null\-key.mode |optional |`'FAIL'` |String |Specifies the method to handle null key values in the Map. 。 Supported values include `'FAIL'`, `'DROP'`, and `'LITERAL'`:<br><br><br>* Option `'FAIL'` throws an exception when encountering data with null key values in the Map.<br><br>* Option `'DROP'` discards data items with null key values in the Map.<br><br>* Option `'LITERAL'` uses a string constant to replace the null key values in the Map. The value of the string constant is defined by `'maxwell-json.map-null-key.literal'`. |
|<span id="baf06b9d"></span><br>##### maxwell\-json.map\-null\-key.literal |optional |'null' |String |When `'maxwell-json.map-null-key.mode'` is LITERAL, a specified string constant replaces null key values in the Map. |
|<span id="8446401c"></span><br>##### maxwell\-json.encode.decimal\-as\-plain\-number |optional |false |Boolean |Keep all DECIMAL type data as is, not representing it in scientific notation. Example: `0.000000027` is by default represented as `2.7E-8`. When this option is set to true, it will represent as `0.000000027`. |


<span id="28e9d9f4"></span>
## Data Type Mapping

Currently, Maxwell\-JSON uses JSON Format for serialization and deserialization.

The table below lists the mapping between data types in Flink and data types in JSON.


|Flink SQL Data Types |JSON Data Types |
|---|---|
|`CHAR / VARCHAR / STRING` |`string` |
|`BOOLEAN` |`boolean` |
|`BINARY / VARBINARY` |`string with encoding: base64` |
|`DECIMAL` |`number` |
|`TINYINT` |`number` |
|`SMALLINT` |`number` |
|`INT` |`number` |
|`BIGINT` |`number` |
|`FLOAT` |`number` |
|`DOUBLE` |`number` |
|`DATE` |`string with format: date` |
|`TIME` |`string with format: time` |
|`TIMESTAMP` |`string with format: date-time` |
|`TIMESTAMP_WITH_LOCAL_TIME_ZONE` |`string with format: date-time (with UTC time zone)` |
|`INTERVAL` |`number` |
|`ARRAY` |`array` |
|`MAP / MULTISET` |`object` |
|`ROW` |`object` |


<span id="936eb1c5"></span>
## Precautions


* Duplicate change events.

   In a normal operating environment, the Maxwell application can deliver each change event with **exactly\-once** semantics. In this situation, Flink can work well to process change events produced by Maxwell. If Maxwell delivers each change event with **at\-least\-once** semantics, it may send duplicate change events to Kafka, and Flink will receive duplicate events. This may cause Flink to obtain incorrect results or unexpected exceptions. Therefore, it is recommended to set the job parameter `table.exec.source.cdc-events-duplicate` to `true` in this situation and define a PRIMARY KEY on that source. The framework will generate an additional stateful operator, using the primary key to deduplicate change events and produce a standardized changelog stream.
