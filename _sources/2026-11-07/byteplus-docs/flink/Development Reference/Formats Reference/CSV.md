---
title: "CSV"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/CSV"
---

CSV format allows us to parse and generate CSV data based on the CSV schema. The current CSV schema is inferred based on the table schema.

<span id="14774cb0"></span>
## How to create a table using the CSV format

Here is an example of creating a table using the Kafka connector and CSV format.

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
 'format' = 'csv',
 'csv.ignore-parse-errors' = 'true',
 'csv.allow-comments' = 'true'
)
```


<span id="bd5149b5"></span>
## Format parameters


|Parameter |Required |Default |Type |Description |
|---|---|---|---|---|
|<span id="72f324b5"></span><br>##### format |Required |(none) |String |Specify the format to use, which should be `'csv'`. |
|<span id="76496cd5"></span><br>##### csv.field\-delimiter |Optional |`,` |String |Field delimiter (default `','`), must be a single character. You can specify some special characters using the backslash character, such as `'\t'` representing a tab. You can also specify some special characters in plain SQL text through unicode encoding, such as `'csv.field-delimiter' = U&'\0001'` representing `0x01` character. |
|<span id="702f8ec3"></span><br>##### csv.disable\-quote\-character |Optional |false |Boolean |Whether to disable the use of quotes for referenced values (default is false). If disabled, the option `'csv.quote-character'` cannot be set. |
|<span id="b9746f66"></span><br>##### csv.quote\-character |Optional |`"` |String |The quote character used to enclose field values (default `"`). |
|<span id="1adb588c"></span><br>##### csv.allow\-comments |Optional |false |Boolean |Whether to allow ignoring comment lines (by default, this is not allowed), where comment lines start with `'#'`. If comment lines are allowed, ensure that `csv.ignore-parse-errors` is also enabled to allow blank lines. |
|<span id="80c77be2"></span><br>##### csv.ignore\-parse\-errors |Optional |false |Boolean |When a parsing error occurs, whether to skip the current field or row, or to throw an error and fail (the default is false, i.e., to throw an error and fail). If the field parsing exception is ignored, the field value will be set to `null`. |
|<span id="109f518f"></span><br>##### csv.array\-element\-delimiter |Optional |`;` |String |String that separates array and row elements (default `';'`) |
|<span id="4fbef317"></span><br>##### csv.escape\-character |Optional |(none) |String |Escape characters (disabled by default). |
|<span id="2a5a8358"></span><br>##### csv.null\-literal |Optional |(none) |String |Whether to convert the "null" string to a null value. |
|<span id="ca2fb64f"></span><br>##### csv.write\-bigdecimal\-in\-scientific\-notation |Optional |true |Boolean |Settings configure BigDecimal data to use scientific notation (by default true, meaning it's converted to scientific notation), such as a BigDecimal value of 100000, set to true, the result is '1E+5'; set to false, the result is 100000. Note: Scientific notation is applied only when the value is non\-zero and a multiple of 10.<br><br>> Note: Applicable only to Flink version 1.16, scientific notation is applied only when the value is nonzero and a multiple of 10. |


<span id="f0d7da67"></span>
## Data type mapping

The schema for CSV is currently inferred from the table schema. Defining the CSV schema explicitly is not supported yet. The CSV format data in Flink uses the jackson databind API to parse CSV strings.

The table below lists the corresponding relationships between Flink data and CSV data.


|Flink SQL Data Types |CSV Data Types |
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
|`INTERVAL` |`number` |
|`ARRAY` |`array` |
|`ROW` |`object` |
