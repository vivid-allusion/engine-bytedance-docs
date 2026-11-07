---
title: "Debezium-JSON"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Debezium-JSON"
---

Debezium is a Change Data Capture tool that can stream changes from MySQL, PostgreSQL, Oracle, Microsoft SQL Server, and many other databases in real\-time to Kafka. Debezium provides a unified format structure for change logs and supports serializing messages with JSON and Apache Avro.

Flink supports parsing Debezium JSON messages into INSERT / UPDATE / DELETE messages within the Flink SQL system. In many cases, using this feature is very beneficial, for example.


* Synchronizing incremental data from databases to other systems.

* Log auditing

* Real\-time materialized views of databases.

* Associating the change history of dimensional databases, and more.


Flink also supports encoding INSERT / UPDATE / DELETE messages from Flink SQL into Debezium format JSON messages, for output to storage like Kafka. However, it is important to note that Flink currently does not support merging UPDATE_BEFORE and UPDATE_AFTER into a single UPDATE message. Therefore, Flink encodes UPDATE_BEFORE and UPDATE_AFTER as DELETE and INSERT types of Debezium messages respectively.

<span id="f4b1c7e2"></span>
## How to Use Debezium\-JSON

Debezium provides a unified format for change logs, here is a simple example of an update operation captured from the MySQL product table in JSON format:

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
  "source": {...},
  "op": "u",
  "ts_ms": 1589362330904,
  "transaction": null
}
```


The MySQL product table has 4 columns (`id`, `name`, `description`, `weight`). The JSON message above is an update event on the `products` table, in which the `id = 111` line's `weight` value changed from `5.18` to `5.15`. Assuming this message has been synchronized to the Kafka topic `products_binlog`, you can use the following DDL to utilize this topic and parse change events:

```SQL
CREATE TABLE topic_products (
  -- The schema is identical to the products table in MySQL.
  id BIGINT,
  name STRING,
  description STRING,
  weight DECIMAL(10, 2)
) WITH (
 'connector' = 'kafka',
 'topic' = 'products_binlog',
 'properties.bootstrap.servers' = 'localhost:9092',
 'properties.group.id' = 'testGroup',
  -- Use the 'debezium-json' format to parse Debezium JSON messages.
 'format' = 'debezium-json'
)
```


In some cases, when setting up the Debezium Kafka Connect, users may enable Kafka's configuration `'value.converter.schemas.enable'`, to include schema information in the message body. Then, the Debezium JSON message may look like this:

To parse this type of information, you need to add the option `'debezium-json.schema-include' = 'true'` (default is false) in the aforementioned DDL WITH clause. Under normal circumstances, it is advisable not to include a schema description, as this can make messages very verbose and reduce parsing performance.

After registering the topic as a Flink table, Debezium messages can be used as a change log source.

```SQL
-- A real-time materialized view of the MySQL "products" table.
-- Calculate the latest average weight of the same product.
SELECT name, AVG(weight) FROM topic_products GROUP BY name;

-- Synchronize all data and incremental changes from the MySQL “products” table 
-- to the Elasticsearch “products” index for future search purposes.
INSERT INTO elasticsearch_products
SELECT * FROM topic_products;
```


<span id="7924a20f"></span>
## Supported Metadata (Available Metadata)

> Note: Only applicable for Flink version 1.16.


The following format metadata can be exposed as read\-only (`VIRTUAL`) columns in the table definition.

Note: Format metadata fields are only available if the corresponding connector supports the respective format metadata. Currently, only the Kafka connector is capable of exposing format metadata fields.


|Key |Data Type |Description |
|---|---|---|
|`schema` |`STRING NULL` |Describes the JSON string pattern of the payload. If the pattern is not included in the Debezium record, it is null. |
|`ingestion-timestamp` |`TIMESTAMP_LTZ(3) NULL` |Timestamp when the connector processes the event. Corresponds to the `ts_ms` field in Debezium records. |
|`source.timestamp` |`TIMESTAMP_LTZ(3) NULL` |Timestamp of the event created by the source system. Corresponds to the `source.ts_ms` field in Debezium records. |
|`source.database` |`STRING NULL` |Source database. Corresponds to the `source.db` field in Debezium records (if any). |
|`source.schema` |`STRING NULL` |Source database schema. Corresponds to the `source.schema` field in Debezium records (if available). |
|`source.table` |`STRING NULL` |Source database table. Corresponds to the `source.table` or `source.collection` in Debezium records (if available). |
|`source.properties` |`MAP<STRING, STRING> NULL` |Mapping of various source properties. Corresponds to the `source` field in Debezium records. |


The example below shows how to access Debezium metadata fields in Kafka:

```SQL
CREATE TABLE KafkaTable (
  origin_ts TIMESTAMP(3) METADATA FROM 'value.ingestion-timestamp' VIRTUAL,
  event_time TIMESTAMP(3) METADATA FROM 'value.source.timestamp' VIRTUAL,
  origin_database STRING METADATA FROM 'value.source.database' VIRTUAL,
  origin_schema STRING METADATA FROM 'value.source.schema' VIRTUAL,
  origin_table STRING METADATA FROM 'value.source.table' VIRTUAL,
  origin_properties MAP<STRING, STRING> METADATA FROM 'value.source.properties' VIRTUAL,
  user_id BIGINT,
  item_id BIGINT,
  behavior STRING
) WITH (
  'connector' = 'kafka',
  'topic' = 'user_behavior',
  'properties.bootstrap.servers' = 'localhost:9092',
  'properties.group.id' = 'testGroup',
  'scan.startup.mode' = 'earliest-offset',
  'value.format' = 'debezium-json'
);
```


<span id="9ca81df6"></span>
## Format Parameters

Flink offers two formats, `debezium-avro-confluent` and `debezium-json`, to parse Debezium\-generated JSON and Avro format messages. Please use `debezium-avro-confluent` to parse Debezium's Avro messages, and `debezium-json` to parse Debezium's JSON messages.


|Parameter |Required |Default |Type |Description |
|---|---|---|---|---|
|<span id="42b6ae9d"></span><br>##### format |Required |(none) |String |Specify the format to use, which should be `'debezium-json'`. |
|<span id="34f5ee48"></span><br>##### debezium\-json.schema\-include |Optional |false |Boolean |When setting up Debezium Kafka Connect, users can enable the Kafka configuration `'value.converter.schemas.enable'` to include the schema in messages. This option indicates whether Debezium JSON messages contain schema. |
|<span id="df1da33f"></span><br>##### debezium\-json.ignore\-parse\-errors |Optional |false |Boolean |When parsing exceptions occur, skip the current field or row, or throw an error failure (the default is false, i.e., throw an error failure). If a field's parsing exception is ignored, the field value will be set to `null`. |
|<span id="4ce73b88"></span><br>##### debezium\-json.timestamp\-format.standard |Optional |`'SQL'` |String |Declare the timestamp format for input and output. The currently supported formats are `'SQL'` and `'ISO-8601'`.<br><br><br>* Optional parameter `'SQL'` will parse the timestamp in the format "yyyy\-MM\-dd HH:mm:ss.s{precision}", e.g., '2020\-12\-30 12:13:14.123', and output in the same format.<br><br>* The optional parameter `'ISO-8601'` will parse the input timestamp in the format "yyyy\-MM\-ddTHH:mm:ss.s{precision}" such as '2020\-12\-30T12:13:14.123', and will output in the same format. |
|<span id="f4a39341"></span><br>##### debezium\-json.map\-null\-key.mode<br><br>> Note: Only applicable for Flink version 1.16 |Optional |`'FAIL'` |String |Specifies the method to handle null key values in a Map. 。 Supported values include `'FAIL'`, `'DROP'`, and `'LITERAL'`:<br><br><br>* Option `'FAIL'` will throw an exception if it encounters data with null key values in a Map.<br><br>* Option `'DROP'` will discard Map entries with null key values.<br><br>* Option `'LITERAL'` will use a string literal to replace null key values in the Map. The value of the string constant is defined by `'debezium-json.map-null-key.literal'`. |
|<span id="e6520bac"></span><br>##### debezium\-json.map\-null\-key.literal<br><br>> Note: Only applicable to Flink version 1.16 |Optional |'null' |String |When `'debezium-json.map-null-key.mode'` is LITERAL, a specific string constant replaces null key values in the Map. |
|<span id="f2f7eda2"></span><br>##### debezium\-json.encode.decimal\-as\-plain\-number<br><br>> Note: Only applicable to Flink1.16 version |Optional |false |Boolean |Keep all DECIMAL type data as is, without using scientific notation. Example: `0.000000027` is normally represented as `2.7E-8`. When this option is set to true, it will be represented as `0.000000027`. |


<span id="ab5bbf1a"></span>
## Data Type Mapping

Currently, Debezium Format uses JSON Format for serialization and deserialization.

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


<span id="8fcea5e5"></span>
## Precautions


* Handle duplicate change events.


In a normal operating environment, the Debezium application can deliver each change event with exactly\-once semantics. In this case, Flink consuming the change events produced by Debezium operates smoothly. However, in the event of a failure, the Debezium application can only guarantee at\-least\-once delivery semantics. You can refer to the official Debezium documentation for more information about Debezium's message delivery semantics. This means that under abnormal conditions, Debezium may deliver duplicate change events to Kafka, and when Flink consumes from Kafka, it will encounter duplicate events. This could lead to Flink queries yielding incorrect results or encountering unexpected exceptions. Therefore, it is recommended in such cases to set the job parameter "table.exec.source.cdc\-events\-duplicate" to true, and define a Primary Key on that data source. The framework will generate an additional stateful operator that uses the Primary Key to deduplicate change events and produce a normalized change log stream.


* Consuming data produced by the Debezium Postgres Connector


If you are using the Debezium PostgreSQL Connector to capture changes to Kafka, ensure that the REPLICA IDENTITY of the monitored table is configured to FULL, which defaults to DEFAULT. Otherwise, Flink SQL will not be able to correctly parse the Debezium data.

When configured to FULL, update and delete events will fully include the previous values of all columns. However, if configured differently, the "before" field in update and delete events will only contain values of the primary key fields, or be null (in cases without a primary key). You can change the configuration of REPLICA IDENTITY by running "ALTER TABLEREPLICA IDENTITY FULL".
