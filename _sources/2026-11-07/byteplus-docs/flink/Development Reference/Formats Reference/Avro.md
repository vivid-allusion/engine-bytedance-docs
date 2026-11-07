---
title: "Avro"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Avro"
---

Apache Avro format allows reading and writing Avro data based on the Avro schema. Currently, the Avro schema is derived from the table schema.

<span id="14774cb0"></span>
## How to Create Tables Using Avro Format

This is an example of creating tables using Kafka connector and Avro format.

```SQL
CREATE TABLE user_behavior (
  user_id BIGINT,
  item_id BIGINT,
  category_id BIGINT,
  behavior STRING,
  ts TIMESTAMP(3)
) WITH (
 'connector' = 'kafka',
 'topic' = 'user_behavior',
 'properties.bootstrap.servers' = 'localhost:9092',
 'properties.group.id' = 'testGroup',
 'format' = 'avro'
)
```


<span id="eb42b8e0"></span>
## Format Parameters


|Parameter |Required |Default |Type |Description |
|---|---|---|---|---|
|<span id="1cf67833"></span><br>##### format |Required |(none) |String |Specify the format to use, here it should be `'avro'`. |
|<span id="484e5d22"></span><br>##### avro.codec |Optional |(none) |String |Avro compression codec, used only for filesystem. Default snappy compression. Currently supported: null, deflate, snappy, bzip2, xz. |


<span id="5ffd8b62"></span>
## Data Type Mapping

Currently, the Avro schema is typically derived from the table schema. Explicitly defining Avro schema is not yet supported. Therefore, the table below lists the type mappings from Flink types to Avro types.


|Flink SQL data types |Avro Data Types |Avro Logical Types |
|---|---|---|
|CHAR / VARCHAR / STRING |string | |
|`BOOLEAN` |`boolean` | |
|`BINARY / VARBINARY` |`bytes` | |
|`DECIMAL` |`fixed` |`decimal` |
|`TINYINT` |`int` | |
|`SMALLINT` |`int` | |
|`INT` |`int` | |
|`BIGINT` |`long` | |
|`FLOAT` |`float` | |
|`DOUBLE` |`double` | |
|`DATE` |`int` |`date` |
|`TIME` |`int` |`time-millis` |
|`TIMESTAMP` |`long` |`timestamp-millis` |
|`ARRAY` |`array` | |
|`MAP`<br><br>(key must be of type string/char/varchar) |`map` | |
|`MULTISET`<br><br>(elements must be of type string/char/varchar) |`map` | |
|`ROW` |`record` | |


Aside from the types listed above, Flink supports reading/writing nullable types. Flink maps nullable types to Avro `union(something, null)`, where `something` is an Avro type converted from a Flink type.
