---
title: "Parquet"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Parquet"
---

Apache Parquet format allows reading and writing Parquet data.

<span id="9e8e4360"></span>
## How to create a table based on Parquet format

Here is an example of creating a table with the Filesystem connector and Parquet format:

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
 'format' = 'parquet'
)
```


<span id="7af0c338"></span>
## Format Parameter


|Parameter |Required |Default |Type |Description |
|---|---|---|---|---|
|<span id="10ce276a"></span><br>##### format |Required |(none) |String |The designated format here should be "parquet". |
|<span id="61d5c4ee"></span><br>##### parquet.utc\-timezone<br><br>> Note: Only applicable to the Flink1.11 version |Optional |false |Boolean |Convert between epoch time and LocalDateTime using the UTC timezone or the local timezone. Hive 0.x/1.x/2.x use the local timezone, but Hive 3.x uses the UTC timezone. |


Parquet format also supports the configuration of ParquetOutputFormat. For example, you can configure `parquet.compression=GZIP` to enable GZIP compression.

<span id="1ba0d7b4"></span>
## Data Type Mapping

Currently, the Parquet format type mapping is compatible with Apache Hive but differs from Apache Spark:


* Timestamp: Regardless of precision, map timestamp type to int96.

* Decimal: Maps the decimal type to a fixed\-length byte array based on precision.


The table below lists the mapping relationships between data types in Flink and data types in Parquet.


|Flink data type |Parquet Type |Parquet Logical Type |
|---|---|---|
|CHAR / VARCHAR / STRING |BINARY |UTF8 |
|BOOLEAN |BOOLEAN | |
|BINARY / VARBINARY |BINARY | |
|DECIMAL |FIXED_LEN_BYTE_ARRAY |DECIMAL |
|TINYINT |INT32 |INT_8 |
|SMALLINT |INT32 |INT_16 |
|INT |INT32 | |
|BIGINT |INT64 | |
|FLOAT |FLOAT | |
|DOUBLE |DOUBLE | |
|DATE |INT32 |DATE |
|TIME |INT32 |TIME_MILLIS |
|TIMESTAMP |INT96 | |
|ARRAY<br><br>> Note: Only applicable to Flink 1.16 version |*  |LIST |
|MAP<br><br>> Note: Only applicable to Flink 1.16 version |*  |MAP |
|ROW<br><br>> Note: Only applicable for Flink 1.16 version |*  |STRUCT |
