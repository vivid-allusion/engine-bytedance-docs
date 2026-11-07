---
title: "Canal-JSON"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Canal-JSON"
---

Canal is a Change Data Capture tool that can real\-time transmit MySQL changes to other systems. Canal provides a unified data format for change logs and supports serializing messages in JSON.

Flink supports parsing Canal\-JSON messages into INSERT / UPDATE / DELETE messages into the Flink SQL system. In many cases, using this feature is very useful, for example:


* Synchronizing incremental data from databases to other systems.

* Log auditing.

* Real\-time materialized views of databases.

* Linking the change history of dimension databases, among others.

> Flink also supports encoding INSERT / UPDATE / DELETE messages in Flink SQL into Canal formatted JSON messages, outputting to storages like Kafka. It should be noted that Flink currently does not support merging UPDATE_BEFORE and UPDATE_AFTER into one UPDATE message. Thus, Flink encodes UPDATE_BEFORE and UPDATE_AFTER as DELETE and INSERT types of Canal messages, respectively.

> Note: Only applicable to Flink version 1.16.


<span id="1926c0dd"></span>
## How to Use Canal Format

Canal provides a unified format for change logs, below is a simple example of capturing an update operation from the MySQL `products` table:

```JSON
{
  "data": [
    {
      "id": "111",
      "name": "scooter",
      "description": "Big 2-wheel scooter",
      "weight": "5.18"
    }
  ],
  "database": "inventory",
  "es": 1589373560000,
  "id": 9,
  "isDdl": false,
  "mysqlType": {
    "id": "INTEGER",
    "name": "VARCHAR(255)",
    "description": "VARCHAR(512)",
    "weight": "FLOAT"
  },
  "old": [
    {
      "weight": "5.15"
    }
  ],
  "pkNames": [
    "id"
  ],
  "sql": "",
  "sqlType": {
    "id": 4,
    "name": 12,
    "description": 12,
    "weight": 7
  },
  "table": "products",
  "ts": 1589373560798,
  "type": "UPDATE"
}
```


The MySQL `products` table has 4 columns (`id`, `name`, `description`, and `weight`). The above JSON message is an update event on the `products` table, indicating the weight field value of the row with id = 111 ch`weight field value of the row with id = 111` changed from `5.15` to `5.18`. Assuming the message has been synchronized to a Kafka topic: `products_binlog`, you can then use the following DDL to consume messages from this topic and parse the change events.

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
 'format' = 'canal-json'  -- Use the 'canal-json' format
)
```


Upon registering the Kafka topic as a Flink table, Canal messages can be used as a source for the change logs.

```SQL
-- A real-time materialized view of the MySQL "products" table.
-- Calculate the latest average weight of the same product.
SELECT name, AVG(weight) FROM topic_products GROUP BY name;

-- Synchronize all data and incremental changes from the MySQL “products” table 
-- to the Elasticsearch “products” index for future search purposes.
INSERT INTO elasticsearch_products
SELECT * FROM topic_products;
```


<span id="99552654"></span>
## Available Metadata

> Note: Available Metadata is only applicable to Flink version 1.16.


The following format metadata can be exposed in the table definition as read\-only `VIRTUAL` columns.

Note: Format metadata fields are only available when the corresponding connector supports the respective format metadata. Currently, only the Kafka connector is able to expose format metadata fields.


|Key |Data Type |Description |
|---|---|---|
|`database` |`STRING NULL` |Original database. If applicable, corresponds to the `database` field in the Canal record. |
|`table` |`STRING NULL` |Source database table. If applicable, corresponds to the `table` field in the Canal record. |
|`sql-type` |`MAP<STRING, INT> NULL` |Mapping of various sql types. Corresponds to the `sqlType` field in Canal records (if available). |
|`pk-names` |`ARRAY<STRING> NULL` |Array of Primary Key names. If available, corresponds to the `pkNames` field in Canal records. |
|`ingestion-timestamp` |`TIMESTAMP_LTZ(3) NULL` |Timestamp of the connector processing the event. Corresponds to the `ts` field in the Canal record. |


The following example demonstrates how to access the Canal metadata fields in Kafka:

```SQL
CREATE TABLE KafkaTable (
  origin_database STRING METADATA FROM 'value.database' VIRTUAL,
  origin_table STRING METADATA FROM 'value.table' VIRTUAL,
  origin_sql_type MAP<STRING, INT> METADATA FROM 'value.sql-type' VIRTUAL,
  origin_pk_names ARRAY<STRING> METADATA FROM 'value.pk-names' VIRTUAL,
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
  'value.format' = 'canal-json'
);
```


<span id="86c255f1"></span>
## Format Parameters


|Parameter |Required |Default |Type |Description |
|---|---|---|---|---|
|<span id="471dd143"></span><br>##### format |Required |(none) |String |Specify the format to use here, which should be `'canal-json'`. |
|<span id="82e7e3ba"></span><br>##### canal\-json.ignore\-parse\-errors |Optional |false |Boolean |When parsing exceptions occur, should you skip the current field or row, or throw an error and fail (default is false, i.e., throw an error and fail). If ignoring the parsing exception of a field, the value of that field will be set to `null`. |
|<span id="c434f9ee"></span><br>##### canal\-json.timestamp\-format.standard |Optional |`'SQL'` |String |Specify the input and output timestamp formats. The current supported values are `'SQL'` and `'ISO-8601'`:<br><br><br>* The option `'SQL'` will parse input timestamps in the format "yyyy\-MM\-dd HH:mm:ss.s{precision}" such as '2020\-12\-30 12:13:14.123', and outputs timestamps in the same format.<br><br>* The option `'ISO-8601'` will parse input timestamps in the format "yyyy\-MM\-ddTHH:mm:ss.s{precision}" such as '2020\-12\-30T12:13:14.123', and outputs timestamps in the same format. |
|<span id="ee91d89b"></span><br>##### canal\-json.map\-null\-key.mode |Optional |`'FAIL'` |String |Specify the method for handling null key values in Map. Current supported values include `'FAIL'`, `'DROP'`, and `'LITERAL'`:<br><br><br>* Option `'FAIL'` will throw an exception if it encounters a Map with a null key value.<br><br>* Option `'DROP'` will discard Map entries with a null key value.<br><br>* Option `'LITERAL'` will replace null key values in the Map with a string constant. The value of the string constant is defined by `'canal-json.map-null-key.literal'`. |
|<span id="50b89380"></span><br>##### canal\-json.map\-null\-key.literal |Optional |'null' |String |When `'canal-json.map-null-key.mode'` is LITERAL, it specifies the string constant to replace null key values in the Map. |
|<span id="0daa62c6"></span><br>##### canal\-json.encode.decimal\-as\-plain\-number |optional |false |Boolean |Keep all DECIMAL type data as is, without using scientific notation. Example: `0.000000027` is by default represented as `2.7E-8`. When this option is set to true, it will be represented as `0.000000027`. |
|<span id="fbc5ac16"></span><br>##### canal\-json.database.include |optional |(none) |String |An optional regular expression that matches the "database" meta field in Canal records to read the changelog records of only specified databases. The regex string is compatible with Java's [Pattern](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html). |
|<span id="d69b112d"></span><br>##### canal\-json.table.include |optional |(none) |String |An optional regular expression that matches the "table" meta field in Canal records to read the changelog records of only specified tables. The regex string is compatible with Java's [Pattern](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html). |


<span id="5016d215"></span>
## Data Type Mapping

Currently, the Canal Format uses JSON Format for serialization and deserialization.

The table below lists the mapping of data types in Flink to data types in JSON.


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


<span id="d1f7e899"></span>
## Precautions


* Duplicate change events.


In a normal operating environment, the Canal application can deliver each change event with exactly\-once semantics. In this case, Flink consuming the change events produced by Canal can operate well. However, in the event of a failure, the Canal application can only guarantee `at-least-once` delivery semantics. This means that, under abnormal conditions, Canal might deliver duplicate change events to the message queue, and when Flink consumes from the message queue, it will retrieve duplicate events. This could lead to Flink queries yielding incorrect results or encountering unexpected exceptions. Therefore, it is recommended in such situations to set the job parameter `table.exec.source.cdc-events-duplicate` to true and define a `Primary Key` on that data source. The framework will generate an additional stateful operator that uses the primary key to deduplicate change events, thereby producing a normalized change data stream.
