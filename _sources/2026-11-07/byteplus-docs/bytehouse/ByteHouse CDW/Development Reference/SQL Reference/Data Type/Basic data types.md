---
title: "Basic data types"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-data-types"
---

In its default mode, ByteHouse supports data types similar to those supported by the ClickHouse community edition. It is advised to refer to the examples in the manual for use. Some examples and content in this article have been modified with reference to [community documentation](https://clickhouse.com/docs/en/sql-reference/data-types/) to ensure normal usage in ByteHouse.

Additionally, starting from version 2.0, the ByteHouse cloud data warehouse edition has enhanced compatibility with commonly used features and syntax of MySQL 5.7 and MySQL 8.0, allowing seamless integration with MySQL client applications and tools. This article will also introduce the compatibility of data types with MySQL.

<span id="4dafd2c6"></span>
## Data Type Overview

<span id="1b7ed0ad"></span>
### Supported Data Types in Default Mode (ClickHouse)


|Classification |Data type |
|---|---|
|Numerical type |* Int8 (TINYINT), Int16(SMALLINT),Int32(INT, INTEGER), Int64(BIGINT), Int128, Int256, UInt8, UInt16, UInt32, UInt64, UInt128, Uint256<br><br>* Float32(FLOAT) Float64(DOUBLE)<br><br>* Decimal(DEC), Decimal32, Decimal64, Decimal128, Decimal256 |
|String and binary types |* String, TEXT, TINYTEXT, MEDIUMTEXT, LONGTEXT, BLOB, TINYBLOB, MEDIUMBLOB , LONGBLOB, CHAR, VARCHAR<br><br>* FixedString, BINARY |
|Date and time types |* Date, Date32<br><br>* DateTime, DateTime64, TIMESTAMP<br><br>* Time |
|Semi\-structured data type |* Array<br><br>* Map<br><br>* Tuple<br><br>* Enum8 Enum16<br><br>* Nested |
|Geographical coordinate type |* Point<br><br>* Ring<br><br>* Polygon<br><br>* MultiPolygon |
|Other special data types |* IPv4 IPv6<br><br>* Nullable<br><br>* UUID |


<span id="d4bcfc22"></span>
### New Data Types Compatible with MySQL


|Data type |Remark |
|---|---|
|`BOOLEAN`/ `BOOL` |None |
|`NUMERIC`/<br><br>`DECIMAL(M ,D)` |ByteHouse currently supports a maximum precision limit of 76, not 1000 |
|`TIME` |Supports 3\-9 digits of precision |
|`Point` |For more details, please see the function introduction of GIS |


<span id="9edcf0b7"></span>
### Other MySQL Data Type Compatibility Differences


|Data type |Remark |
|---|---|
|`DECIMAL(M ,D)` |Under MySQL Mode, the current maximum precision support is limited to 76, not 1000 |
|`VARCHAR` |In ByteHouse, it is an alias for String Type, with no length restriction.<br><br>In MySQL, the length is limited to 0\-65535 bytes. |
|`BINARY` |In ByteHouse, it is an alias for Fixedstring Type. |
|`DATE` |1. Date16 ranges between 1970 and 2149<br><br>2. Date32 ranges between 1900 and 2299 |
|`DATETIME` |1. ByteHouse is divided into data types Datetime and Datetime64. Datetime does not support numbers, while Datetime64 supports 0\-9 digits.<br><br>2. Datetime occupies 4 bytes, while Datetime64 occupies 8 bytes.<br><br>3. It is suggested to use the behavior of Datetime64 to implement the same behavior as MySQL.<br><br>4. DateTime/DateTime64 stores time as Unix timestamps.<br><br>5. The value itself is independent of the timezone. In binary format, it is represented as a Unix timestamp.<br><br>6. In text format, it is serialized into the format YYYY\-MM\-DD hh:MM:ss and parsed from there. Text format depends on the timezone.<br><br>7. The scope of DateTime/DateTime64 is the same as that of Date/Date32. |
|`TIMESTAMP` |Use numeric type and convert internally to datetime |
|`Array` |Data type supported. |
|`Map` |Data type supported. |
|`JSON` |Data type supported. |


<span id="d31e081a"></span>
## Numerical Types

<span id="0c06431d"></span>
### Integer Types

UInt8, UInt16, UInt32, UInt64, UInt128, UInt256, Int8, Int16, Int32, Int64, Int128, Int256

Fixed\-length integers.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When creating a table, you can set numeric parameters for integers (e.g., TINYINT(8), SMALLINT(16), INT(32), BIGINT(64)), but ByteHouse will automatically ignore these parameters.</div>


**Aliases**


* `Int8` — `TINYINT`

* `Int16` — `SMALLINT`

* `Int32` — `INT`,`INTEGER`.

* `Int64` — `BIGINT`.


**Int value range**


* `Int8` — [\-128 : 127]

* `Int16` — [\-32768 : 32767]

* `Int32` — [\-2147483648 : 2147483647]

* `Int64` — [\-9223372036854775808 : 9223372036854775807]

* `Int128` — [\-170141183460469231731687303715884105728 : 170141183460469231731687303715884105727]

* `Int256` — [\-57896044618658097711785492504343953926634992332820282019728792003956564819968 : 57896044618658097711785492504343953926634992332820282019728792003956564819967]


**UInt Value Range**


* `UInt8` — [0 : 255]

* `UInt16` — [0 : 65535]

* `UInt32` — [0 : 4294967295]

* `UInt64` — [0 : 18446744073709551615]

* `UInt256` — [0 : 115792089237316195423570985008687907853269984665640564039457584007913129639935]


<span id="1301d5e2"></span>
### Floating Point Types

Float32, Float64

**Alias**


* `Float32` — `FLOAT`.

* `Float64` — `DOUBLE`.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When creating a table, you can set numerical parameters for floating\-point numbers (e.g., FLOAT(12), FLOAT(15, 22), DOUBLE(12), DOUBLE(4, 18)), but ByteHouse will ignore them.</div>


**Numerical Range**


* `Float32`: Conforms to IEEE 754 standard, single\-precision floating\-point number.

* `Float64`: Conforms to IEEE 754 standard, double\-precision floating\-point number.


<span id="d06491d4"></span>
### Decimal Types

Decimal(P, S), Decimal32(S), Decimal64(S), Decimal128(S)

Signed fixed\-point numbers that maintain precision during addition, subtraction, and multiplication operations. For division, the least significant digit will be discarded (not rounded).

**Alias**


* `Decimal` — `DEC`


**Parameter**


* P \- precision, accuracy, range [1:76], indicates the number of significant digits (including decimals).

* S \- scale, size, range [0:P], indicates the number of digits to the right of the decimal point.


When the P parameter value in Decimal(P, S) falls within the following ranges, it is equivalent to the latter:


* P in [1:9], equivalent to Decimal32(S)

* P in [10:18], equivalent to Decimal64(S)

* P in [19:38], equivalent to Decimal128(S)


**Decimal number range**


* Decimal32(S) ：( \-1 \* 10^(9 \- S), 1 \* 10^(9 \- S) )

* Decimal64(S) ：( \-1 \* 10^(18 \- S), 1 \* 10^(18 \- S) )

* Decimal128(S) ： ( \-1 \* 10^(38 \- S), 1 \* 10^(38 \- S) )


For example, Decimal32(4) can include numbers ranging from \-99999.9999 to 99999.9999.

<span id="442dbfa5"></span>
## String type

<span id="24964f69"></span>
### String

**Alias**


* `String` — `char`/`nchar`/`character`/`varchar`/`text` etc., compatible with MySQL syntax.


String of any length. Length is not limited. This value can contain any set of bytes, including null bytes.

The String type has replaced VARCHAR, BLOB, CLOB, and other types in other databases.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When creating a table, you can set numerical parameters for string fields (such as VARCHAR(255)), but ByteHouse will ignore them.</div>


**Encoding**

ByteHouse does not conceptually involve encoding. Strings can contain any set of bytes which are stored and output as\-is.

If you need to store text, we recommend using UTF\-8 encoding. At least, if your terminal uses UTF\-8 (recommended), you can read and write your values without conversion.

Similarly, some functions for processing strings have separate variants that work assuming the string contains a set of bytes representing UTF\-8 encoded text.

For example, the "length" function calculates the string length in bytes, while the "lengthUTF8" function calculates the string length in Unicode code points, assuming the value is UTF\-8 encoded.

<span id="a085af6e"></span>
### Fixedstring(N)

**Alias**


* `Fixedstring` — `binary(N)`


A string of fixed length N (where N is a positive natural number).

You can declare a column as `FixedString` type using the syntax below:

```Plain
<column_name> FixedString(N)
```


Where N is a natural number.

When the data length is exactly N bytes, the FixedString type is very efficient. In other cases, it may reduce efficiency.

Examples of values that can be effectively stored in a `FixedString` type column:


* Binary representation of IP addresses (IPv6 uses `FixedString(16)`).

* Language codes (ru_RU, en_US, etc.).

* Currency codes (USD, RUB, etc.).

* Binary representation of hash values (MD5 uses `FixedString(16)`, SHA256 uses `FixedString(32)`).


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If you need to store UUID values, please use the UUID data type.</div>


When inserting data into ByteHouse:


* If the number of bytes in the string is less than N, the string is padded with null bytes.

* If the number of bytes in the string exceeds N bytes, a `Too Large value for FixString(N)` exception is raised.


When querying data, ByteHouse does not remove trailing null bytes from strings. If using a `WHERE` clause, manually add null bytes to match fixed string values.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



1. <div data-tips="true" data-tips-type="warning">This method is different from MySQL's <code>CHAR</code> type (MySQL uses spaces for padding and deletes them in the output).</div>


2. <div data-tips="true" data-tips-type="warning">The length of a FixedString(N) value is constant. Even if a FixedString(N) value is filled only with empty bytes, the length function will return N, but in this case, the empty function will return 1.</div>



<span id="89c91114"></span>
## Date and Time Types

<span id="6a47f948"></span>
### Date

Takes up two bytes, storing the number of days since 1970\-01\-01 (unsigned), with an upper limit up to the year 2148.

Stored values do not include time zones.

<span id="dfe29de9"></span>
### DateTime

alias:


* `DateTime` — `TIMESTAMP`


Stores Unix Timestamps using four bytes (unsigned). Displayed as a calendar date and a specific time of the day. Accuracy to the second.

```Plain
DateTime([timezone])
```


Supported Value Range: [1970\-01\-01 00:00:00, 2106\-02\-07 14:28:15].

<span id="8716f2b0"></span>
### DateTime64

This type allows storage of time values of a specific moment in the form of a date and time, with defined sub\-second accuracy.

Syntax:

```SQL
DateTime64(precision, [timezone])
```


Internally, this type stores data as an Int64 type number of ticks since the Linux Epoch (1970\-01\-01 00:00:00 UTC). The resolution of time scale is determined by the precision parameter. Moreover, **`DateTime64`** type can store timezone information like other data columns, which affects how the **`DateTime64`** type values are displayed in text format and how time data specified in string form ('2020\-01\-01 05:00:01.000') is parsed. The timezone is not stored in the rows of the table (nor in the resultset), but in the column metadata. For more details, please refer to the [DateTime](https://clickhouse.com/docs/sql-reference/data-types/datetime) data type.

Value range: [1900\-01\-01 00:00:00, 2299\-12\-31 23:59:59.99999999] (Note: Maximum precision is 8).

**Example**


1. Create a table with a **`DateTime64`** type column and insert data into it:

   ```SQL
   CREATE TABLE dida.dt
   (
       `timestamp` DateTime64(3, 'Asia/Istanbul'),
       `event_id` UInt8
   )
   ENGINE = CnchMergeTree()
   order by event_id;
   
   INSERT INTO dt Values (1546300800000, 1), ('2019-01-01 00:00:00', 2);
   SELECT * FROM dt;
   ```
   

   ```Plain
   ┌───────────────timestamp─┬─event_id─┐
   │ 2019-01-01 03:00:00.000 │        1 │
   │ 2019-01-01 00:00:00.000 │        2 │
   └─────────────────────────┴──────────┘
   ```
   

   * When inserting datetimes as integer types, it will be considered as appropriately scaled Unix timestamps (UTC). **`1546300800000`** (precision 3) represents  **`'2019-01-01 00:00:00'`**  UTC. However, since the **`timestamp`** column is set to the Timezone of **`Asia/Istanbul`** (UTC+3), when output as a string, it will be displayed as  **`'2019-01-01 03:00:00'`** 

   * When inserting a string as a datetime, it will be assigned timezone information.  **`'2019-01-01 00:00:00'`**  is considered to be in the **`Asia/Istanbul`** timezone and stored as **`1546290000000`**.

2. Filter values of **`DateTime64`** Type

   ```SQL
   SELECT * FROM dt WHERE timestamp = toDateTime64('2019-01-01 00:00:00', 3, 'Asia/Istanbul')
   ```
   

   ```Plain
   ┌───────────────timestamp─┬─event_id─┐
   │ 2019-01-01 00:00:00.000 │        2 │
   └─────────────────────────┴──────────┘
   ```
   

   Unlike **`DateTime`**, values of **`DateTime64`** Type do not automatically convert from **`String`** values.

3. Retrieve timezone information for **`DateTime64`** Type values:

   ```SQL
   SELECT toDateTime64(now(), 3, 'Asia/Istanbul') AS column, toTypeName(column) AS x
   ```
   

   ```Plain
   ┌──────────────────column─┬─x──────────────────────────────┐
   │ 2019-10-16 04:12:04.000 │ DateTime64(3, 'Asia/Istanbul') │
   └─────────────────────────┴────────────────────────────────┘
   ```
   

4. Converse timezone.

   ```SQL
   SELECT
   toDateTime64(timestamp, 3, 'Europe/London') as lon_time,
   toDateTime64(timestamp, 3, 'Asia/Istanbul') as mos_time
   FROM dt
   ```
   

   ```Plain
   ┌───────────────lon_time──┬────────────────mos_time─┐
   │ 2019-01-01 00:00:00.000 │ 2019-01-01 03:00:00.000 │
   │ 2018-12-31 21:00:00.000 │ 2019-01-01 00:00:00.000 │
   └─────────────────────────┴─────────────────────────┘
   ```
   


<span id="55f36235"></span>
## **Other Types**

Other special data types.

<span id="e0bd8996"></span>
### UUID

The general unique identifier (UUID) is a 16\-byte number used to identify records.

Examples of UUID value types are as follows:

```Plain
61f0c404-5cb3-11e7-907b-a6006ad3dba0
```


When a new record is inserted and the UUID column value is not specified, the UUID value will be filled with zeros:

```Plain
00000000-0000-0000-0000-000000000000
```


<span id="5ffdb702"></span>
### Nullable(T)

Special markers [NULL](https://clickhouse.com/docs/sql-reference/data-types/nullable) can represent "missing values" and can be stored together with the normal values of `TypeName`. For example, columns of type `Nullable(Int8)` can store values of type `Int8`, while rows without values will store `NULL`.

For `TypeName`, composite data types such as [arrays](https://clickhouse.com/docs/sql-reference/data-types/array) and [tuples](https://clickhouse.com/docs/sql-reference/data-types/tuple) cannot be used. Composite data types can contain `Nullable` type values, such as `Array(Nullable(Int8))`.

`Nullable` type fields cannot be included in table indexes.

Unless otherwise stated in the ClickHouse server configuration, `NULL` is the default value for any `Nullable` type.
