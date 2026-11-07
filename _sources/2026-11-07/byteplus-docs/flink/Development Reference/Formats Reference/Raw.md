---
title: "Raw"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Raw"
---

Raw format allows reading and writing raw (byte\-based) values as a single column.

Note: This format encodes `null` values into `byte[]` type `null`. Using `upsert-kafka` in this way might be limited because `upsert-kafka` treats `null` values as Tombstone messages (delete on key). Therefore, if the field may have a `null` value, we recommend avoiding using the `upsert-kafka` connector and the `raw` format as the `value.format`.

The connector is built\-in.

<span id="ded1aec7"></span>
## Example

For instance, you might have raw log data in Kafka and want to read and analyze such data using Flink SQL.

```Plain
47.29.201.179 - - [28/Feb/2019:13:17:10 +0000] "GET /?p=1 HTTP/2.0" 200 5316 "https://domain.com/?p=1" "Mozilla/5.0 (Windows NT 6.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/72.0.3626.119 Safari/537.36" "2.75"
```


The code below creates a table, using `raw` format to read (and also write) the underlying Kafka topic message content as string values encoded in UTF\-8:

```SQL
CREATE TABLE nginx_log (
  log STRING
) WITH (
  'connector' = 'kafka',
  'topic' = 'nginx_log',
  'properties.bootstrap.servers' = 'localhost:9092',
  'properties.group.id' = 'testGroup',
  'format' = 'raw'
)
```


Then, you can read the original data as a plain string and use a custom function to split it into multiple fields for further analysis. For example, in the case of `my_split`.

```SQL
SELECT t.hostname, t.datetime, t.url, t.browser, ...
FROM(
  SELECT my_split(log) as t FROM nginx_log
);
```


Correspondingly, you can also write a STRING type column into a Kafka topic using UTF\-8 encoding.

<span id="4ea2e1cb"></span>
## Format parameter


|Parameter |Required |Default |Type |Description |
|---|---|---|---|---|
|<span id="f4939680"></span><br>##### format |Required |(none) |String |Specify the format to use, which should be 'raw'. |
|<span id="9067919f"></span><br>##### raw.charset |Optional |UTF\-8 |String |Specify the character set to encode the text strings. |
|<span id="cf3ba531"></span><br>##### raw.endianness |Optional |big\-endian |String |Specify the byte order for encoding numeric values. Valid values are 'big\-endian' and 'little\-endian'. |


<span id="47428c2d"></span>
## Data type mapping

The table below details the SQL types supported by this format, including information on the serialization and deserialization classes used for encoding and decoding.


|Flink SQL Type |Value |
|---|---|
|`CHAR / VARCHAR / STRING` |Text strings encoded in UTF\-8 (default).<br><br>The character encoding can be configured through 'raw.charset'. |
|`BINARY / VARBINARY / BYTES` |The byte sequence itself. |
|`BOOLEAN` |A single byte representing a boolean value, where 0 means false and 1 means true. |
|`TINYINT` |A single byte of a signed numeric value. |
|`SMALLINT` |Two bytes encoded in big\-endian (default).<br><br>The byte order can be configured through 'raw.endianness'. |
|`INT` |Four bytes encoded in big\-endian (default).<br><br>Byte order can be configured through 'raw.endianness'. |
|`BIGINT` |Eight bytes encoded in big\-endian (default).<br><br>Byte order can be configured through 'raw.endianness'. |
|`FLOAT` |Four bytes encoded in IEEE 754 format and big\-endian (default).<br><br>Byte order can be configured through 'raw.endianness'. |
|`DOUBLE` |Eight bytes encoded in IEEE 754 format and big\-endian (default).<br><br>The byte order can be configured through 'raw.endianness'. |
|`RAW` |Byte sequence serialized through the underlying TypeSerializer of the RAW type. |
