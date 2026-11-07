---
title: "Ogg-JSON"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Ogg-JSON"
---

Oracle GoldenGate (also known as ogg) is a comprehensive software package that enables real\-time data integration and replication across heterogeneous IT environments. This product suite supports high availability solutions, real\-time data integration, transactional change data capture, and replication, transformation, and validation of data between operational and analytical enterprise systems. Ogg provides a unified format structure for change logs and supports using JSON for message serialization.

Flink supports parsing Ogg's JSON messages as INSERT/UPDATE/DELETE messages and importing them into the Flink SQL system. In many cases, leveraging this feature is very beneficial, for example:


* Synchronizing incremental data from databases to other systems;

* Conducting log auditing;

* Building real\-time materialized views of databases;

* Associating changes in the history of dimension databases, and more.


Flink also supports encoding messages from Flink SQL such as INSERT/UPDATE/DELETE into Ogg JSON format and outputting them to storage systems like Kafka. However, it should be noted that Flink currently does not support merging UPDATE_BEFORE and UPDATE_AFTER into a single UPDATE message. Therefore, Flink encodes UPDATE_BEFORE and UPDATE_AFTER separately into DELETE and INSERT type Ogg messages, respectively.

<span id="14774cb0"></span>
## How to Use Ogg\-JSON

Ogg provides a unified format for change logs, illustrated by a simple example of an update operation captured in the Oracle `PRODUCTS` table in JSON format:

```JSON
{
  "before": {
    "id": 111,
    "name": "scooter",
    "description": "Big 2-wheel scooter",
    "weight": 5.18
  },
  "after": {
    "id": 111,
    "name": "scooter",
    "description": "Big 2-wheel scooter",
    "weight": 5.15
  },
  "op_type": "U",
  "op_ts": "2020-05-13 15:40:06.000000",
  "current_ts": "2020-05-13 15:40:07.000000",
  "primary_keys": [
    "id"
  ],
  "pos": "00000000000000000000143",
  "table": "PRODUCTS"
}
```


The Oracle `PRODUCTS` table has 4 columns (`id`, `name`, `description` and `weight`). The JSON message above represents an update event on the `PRODUCTS` table, where the weight value of the row with id = 111 ch`weight value of the row with id = 111` changed from `5.18` to `5.15`. Assuming this message is synced to Kafka's Topic `products_ogg`, you can use the following DDL to access this Topic and parse the update event.

```SQL
CREATE TABLE topic_products (
  -- schema is totally the same to the Oracle "products" table
  id BIGINT,
  name STRING,
  description STRING,
  weight DECIMAL(10, 2)
) WITH (
  'connector' = 'kafka',
  'topic' = 'products_ogg',
  'properties.bootstrap.servers' = 'localhost:9092',
  'properties.group.id' = 'testGroup',
  'format' = 'ogg-json'
)
```


After registering the Kafka Topic as a Flink table, you can turn OGG messages into a change log source.

```SQL
-- a real-time materialized view on the Oracle "PRODUCTS"
-- which calculate the latest average of weight for the same products
SELECT name, AVG(weight)
FROM topic_products
GROUP BY name;

-- synchronize all the data and incremental changes of Oracle "PRODUCTS" table to
-- Elasticsearch "products" index for future searching
INSERT INTO elasticsearch_products
SELECT *
FROM topic_products;
```


<span id="c5e204a0"></span>
## Available Metadata

The following format metadata can be exposed as read\-only `VIRTUAL` columns in table definitions.

Note: Format metadata fields are only available when the corresponding connector supports the relevant format metadata. Currently, only the Kafka connector can expose format metadata fields.


|Key |Data Type |Description |
|---|---|---|
|`table` |`STRING NULL` |Contains the fully qualified table name. The format for the fully qualified table name is: CATALOG NAME.SCHEMA NAME.TABLE NAME |
|`primary-keys` |`ARRAY<STRING> NULL` |Array variable that stores the column names of the source table's primary keys. Only when the `includePrimaryKeys` configuration property is set to true, the primary key fields are included in the JSON output. |
|`ingestion-timestamp` |`TIMESTAMP_LTZ(6) NULL` |Timestamp of the event processed by the connector. Corresponds to the `current_ts` field in Ogg record. |
|`event-timestamp` |`TIMESTAMP_LTZ(6) NULL` |Timestamp of the event created by the source system. Corresponds to the `op_ts` field in Ogg record. |


The following example shows how to access the Ogg metadata fields in Kafka:

```SQL
CREATE TABLE KafkaTable (
  origin_ts TIMESTAMP(3) METADATA FROM 'value.ingestion-timestamp' VIRTUAL,
  event_time TIMESTAMP(3) METADATA FROM 'value.event-timestamp' VIRTUAL,
  origin_table STRING METADATA FROM 'value.table' VIRTUAL,
  primary_keys ARRAY<STRING> METADATA FROM 'value.primary_keys' VIRTUAL,
  user_id BIGINT,
  item_id BIGINT,
  behavior STRING
) WITH (
  'connector' = 'kafka',
  'topic' = 'user_behavior',
  'properties.bootstrap.servers' = 'localhost:9092',
  'properties.group.id' = 'testGroup',
  'scan.startup.mode' = 'earliest-offset',
  'value.format' = 'ogg-json'
);
```


<span id="d661d7d0"></span>
## Format Parameters


|Parameter |Required |Default |Type |Description |
|---|---|---|---|---|
|<span id="1d81825d"></span><br>##### format |Required |(none) |String |Specify the format to be used, which should be `'ogg-json'`. |
|<span id="7ff744a0"></span><br>##### ogg\-json.ignore\-parse\-errors |Optional |false |Boolean |When a parsing exception occurs, choose whether to skip the current field or row, or to throw an error and fail (default is false, which throws an error). If parsing exceptions for a field are ignored, the field's value will be set to null. |
|<span id="531e4248"></span><br>##### ogg\-json.timestamp\-format.standard |Optional |`'SQL'` |String |Declare the input and output timestamp formats. The current supported formats are `'SQL'` and `'ISO-8601'`:<br><br><br>* Optional parameter `'SQL'` will parse timestamps in the format "yyyy\-MM\-dd HH:mm:ss.s{precision}", for example '2020\-12\-30 12:13:14.123', and will output in the same format.<br><br>* The optional parameter `'ISO-8601'` will parse the input timestamp in the format "yyyy\-MM\-ddTHH:mm:ss.s{precision}", such as '2020\-12\-30T12:13:14.123', and will output in the same format. |
|<span id="b37ed15b"></span><br>##### ogg\-json.map\-null\-key.mode |Optional |`'FAIL'` |String |Specifies the method for handling keys with null values in a Map. Currently supported values include `'FAIL'`, `'DROP'`, and `'LITERAL'`:<br><br><br>* Option `'FAIL'` will throw an exception.<br><br>* Option `'DROP'` will discard data items in the Map with null key values.<br><br>* Option `'LITERAL'` will replace null key values in the Map with string constants. The value of the string constant is defined by `ogg-json.map-null-key.literal`. |
|<span id="bec73eca"></span><br>##### ogg\-json.map\-null\-key.literal |Optional |'null' |String |When `'ogg-json.map-null-key.mode'` is LITERAL, a specified string constant replaces the null key value in the Map. |


<span id="219968d5"></span>
## Data Type Mapping

Currently, the Ogg format uses JSON format for serialization and deserialization.

The table below lists the mapping relationships between data types in Flink and data types in JSON.


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
