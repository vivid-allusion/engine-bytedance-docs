---
title: "ORC"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/ORC"
---

Apache ORC Format supports reading and writing ORC data.

<span id="f6cfa0ca"></span>
## How to create a table using ORC format

This is an example of creating a table with the Filesystem connector and ORC format.

```SQL
CREATE TABLE user_behavior (
  user_id BIGINT,
  item_id BIGINT,
  category_id BIGINT,
  behavior STRING,
  ts TIMESTAMP(3),
  dt STRING
) PARTITIONED BY (dt) WITH (
 'connector' = 'filesystem',
 'path' = '/tmp/user_behavior',
 'format' = 'orc'
)
```


<span id="b320cc92"></span>
## Format parameters


|Parameter |Required |Default Value |Type |Description |
|---|---|---|---|---|
|**format** |Required |(none) |String |Specifies the format to use, which should be 'orc'. |


The ORC format also supports table properties sourced from Table properties. For instance, you can set `orc.compress=SNAPPY` to enable Snappy compression.


|**Parameter** |**Default value** |**Description** |
|---|---|---|
|orc.compress |ZLIB |high level compression ＝ |
|orc.compress.size |262,144 |compression chunk size |
|orc.stripe.size |67,108,864 |memory buffer in bytes for writing |
|orc.row.index.stride |10,000 |number of rows between index entries |
|orc.create.index |true |whether the ORC writer creates indexes as part of the file or not |
|orc.bloom.filter.columns |”” |comma separated list of column names |
|orc.bloom.filter.fpp |0.01 |bloom filter false positive rate |


<span id="f1e53374"></span>
## Data type mapping

The type mapping in ORC format is compatible with Apache Hive. The following table lists the mapping relationships between Flink data types and ORC data types.


|Flink data types |Orc physical types |Orc logical types |
|---|---|---|
|CHAR |bytes |CHAR |
|VARCHAR |bytes |VARCHAR |
|STRING |bytes |STRING |
|BOOLEAN |long |BOOLEAN |
|BYTES |bytes |BINARY |
|DECIMAL |decimal |DECIMAL |
|TINYINT |long |BYTE |
|SMALLINT |long |SHORT |
|INT |long |INT |
|BIGINT |long |LONG |
|FLOAT |double |FLOAT |
|DOUBLE |double |DOUBLE |
|DATE |long |DATE |
|TIMESTAMP |timestamp |TIMESTAMP |
|ARRAY<br><br>> Note: Only applicable to Flink1.16 version |*  |LIST |
|MAP<br><br>> Note: Only applicable to Flink1.16 version |*  |MAP |
|ROW<br><br>> Note: Only applicable to Flink1.16 version |*  |STRUCT |
