---
title: "JSON"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/JSON"
---

JSON Format can read and write JSON data. Currently, JSON schema is automatically derived from table schema.

<span id="642e91f1"></span>
## How to create a table based on JSON Format

Here is an example of building a table using Kafka and JSON Format.

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
 'format' = 'json',
 'json.fail-on-missing-field' = 'false',
 'json.ignore-parse-errors' = 'true'
)
```


<span id="329893a7"></span>
## Format parameter


|Parameters |Required |Default |Type |Description |
|---|---|---|---|---|
|<span id="fe91979b"></span><br>##### format |Required |(none) |String |Declare the format used, which should be `'json'`. |
|<span id="6edd9956"></span><br>##### json.fail\-on\-missing\-field |Optional |false |Boolean |When a parsing field is missing, it either skips the current field or line, or throws an error to fail (default is false, which means it throws an error to fail). |
|<span id="fbd4f3ef"></span><br>##### json.ignore\-parse\-errors |Optional |false |Boolean |When a parsing exception occurs, it either skips the current field or line, or throws an error to fail (default is false, which means it throws an error to fail). If the parsing exception for a field is ignored, the field value will be set to `null`. |
|<span id="e156c838"></span><br>##### json.timestamp\-format.standard |Optional |`'SQL'` |String |Declare the formats of `TIMESTAMP` and `TIMESTAMP_LTZ` for input and output. The currently supported formats include `'SQL'` and `'ISO-8601'`.<br><br><br>* Optional parameter `'SQL'` will parse the TIMESTAMP in the format "yyyy\-MM\-dd HH:mm:ss.s{precision}" such as "2020\-12\-30 12:13:14.123", and parse the TIMESTAMP_LTZ in the format "yyyy\-MM\-dd HH:mm:ss.s{precision}'Z'" such as "2020\-12\-30 12:13:14.123Z", and output in the same format.<br><br>* Optional parameter `'ISO-8601'` will parse the input TIMESTAMP in the format "yyyy\-MM\-ddTHH:mm:ss.s{precision}" such as "2020\-12\-30T12:13:14.123", and parse the TIMESTAMP_LTZ in the format "yyyy\-MM\-ddTHH:mm:ss.s{precision}'Z'" such as "2020\-12\-30T12:13:14.123Z", and output in the same format. |
|<span id="df9d85ee"></span><br>##### json.map\-null\-key.mode<br><br>> Note: Only applicable for Flink 1.16 version. |Optional |`'FAIL'` |String |Specify the method for handling null key values in the Map. 。 The currently supported values are `'FAIL'`, `'DROP'`, and `'LITERAL'`:<br><br><br>* Option `'FAIL'` will throw an exception if it encounters null key values in the Map.<br><br>* Option `'DROP'` will discard data items with null key values in the Map.<br><br>* Option `'LITERAL'` will use a string constant to replace the null key values in the Map. The value of the string constant is defined by `'json.map-null-key.literal'`. |
|<span id="63fe4547"></span><br>##### json.map\-null\-key.literal<br><br>> Note: Only applicable to Flink1.16 version |Optional |'null' |String |When `'json.map-null-key.mode'` is LITERAL, specify a string constant to replace the null key value in the Map. |
|<span id="e25130f1"></span><br>##### json.encode.decimal\-as\-plain\-number<br><br>> Note: Only applicable to Flink1.16 version |Optional |false |Boolean |Keep all DECIMAL data as\-is without using scientific notation. Example: `0.000000027` is usually represented as `2.7E-8`. When this option is set to true, it will be represented as `0.000000027`. |


<span id="ca2698cf"></span>
## Data type mapping relationships

Currently, JSON schema will be automatically derived from the table schema. Explicitly defining JSON schema is not supported.

In Flink, JSON Format uses the jackson databind API to parse and generate JSON.

The table below shows the mapping of data types in Flink to data types in JSON.


|Flink SQL data types |JSON data types |
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


<span id="d6aa5b30"></span>
## Precautions


* JSON types are parsed based on the column names and column types declared by the user in `create table`. The current SQL task has only implemented partial automatic adaptation. For example, a column declared as `int` type, but actually represented as an `int` type string in JSON, can be automatically recognized and converted back to `int` type by SQL. However, if it is declared as `int` but actually a `long` type, or declared as `int` but actually is a string containing letters, SQL cannot directly convert and will throw an error.

* JSON types support nesting. For example, `{"a": "a", "b": {"c": 1, "d": "s"}}`, when declaring nested structures, it should be declared as `b Row<c int, d varchar>`, indicating that the fields `c` and `d` are nested within the field `b`. JSON also supports array forms.

   * If it is a simple array, such as `"a": [1,2,3,4]`, it can be declared as `a Array`, meaning that `a` is an array of type `int`. It is important to note that when performing a `select` operation, the index starts from 1. For example, `"a": [6,7,8,9]`, executing `select a[1]` will return 6.

   * If it is a nested JSON array, for example `"a": [{"b": 3}, {"b": 6}]`, it can be declared as `a Array<Row>`, indicating that `a` is an array of object types, within the structure of `a`, there is a column b of type int. Access`b of type int`. Accessing data like `select a[1].b` will return 3.


<span id="c552d1ca"></span>
## Frequently Asked Questions


* Error during deserialization: `Invalid UTF-8 start byte`.


Our internal implementation uses Jackson, and only supports encoding types UTF\-8, UTF\-16, and UTF\-32 during deserialization; using other encoding types will result in the aforementioned error. Furthermore, the exception messages printed may be garbled (converted to strings in UTF\-8 format).

If it is possible to ignore such messages, you can set `json.ignore-parse-errors` to overlook them; if it's necessary to parse such messages, you can specify the `format` as `bytes` and write a UDF (User Defined Function) for parsing.
