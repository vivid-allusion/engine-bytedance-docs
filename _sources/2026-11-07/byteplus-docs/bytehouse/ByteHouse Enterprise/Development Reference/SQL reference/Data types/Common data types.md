---
title: "Common data types"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/common-data-types"
---

In ByteHouse's default mode, the supported data types are similar to those in the ClickHouse community edition, and it is advised to refer to the manual for details. Some examples and content in the text were modified based on [community documentation](https://clickhouse.com/docs/en/sql-reference/data-types/) to ensure normal usage in ByteHouse.

Moreover, starting from version 2.4.0, ByteHouse Enterprise Edition has enhanced compatibility with common features and syntax of MySQL 5.7 and MySQL 8.0, allowing seamless integration with MySQL client applications and tools. This article also introduces the compatibility of data types with MySQL.

<span id="2b6ee6bb"></span>
## Data type overview

<span id="9e7813f5"></span>
### Data types supported under the default mode (ClickHouse)


|Classification |Data type |
|---|---|
|Numerical Value Type |* Int8, TINYINT Int16, SMALLINT Int32, INT, INTEGER Int64, BIGINT UInt8 UInt16 UInt32 UInt64<br><br>* Float32, FLOAT Float64, DOUBLE<br><br>* Decimal, DEC Decimal32 Decimal64 Decimal128 |
|String and Binary Type |* String, TEXT, TINYTEXT, MEDIUMTEXT, LONGTEXT, BLOB, TINYBLOB, MEDIUMBLOB , LONGBLOB, CHAR, VARCHAR<br><br>* FixedString, BINARY |
|Date and Time Date Type |* Date<br><br>* DateTime, TIMESTAMP |
|Semi\-structured Data Type |* Array<br><br>* Map<br><br>* Tuple<br><br>* Enum8 Enum16<br><br>* Nested |
|Boolean Type |* Bool<br><br>* Boolean |
|Other Special Data Types |* IPv4 IPv6<br><br>* Nullable<br><br>* UUID |


<span id="971a28f3"></span>
### New data types compatible with MySQL


|Data Type |Remark |
|---|---|
|`BOOLEAN` |For more details, refer to [bool](https://docs.byteplus.com/docs/bytehouse/bool). |
|`NUMERIC`/<br><br>`DECIMAL(M ,D)` |ByteHouse currently supports a Max precision limit of 76, not 1000 |
|`TIME` |Supports 3\-9 digits of precision |
|`Point` |For more details, please refer to the Function Introduction on GIS capabilities |


<span id="cb5cfb51"></span>
### Differences in compatibility with other MySQL data types


|Data type |Remark |
|---|---|
|`DECIMAL(M ,D)` |In MySQL mode, the current max precision limit is 76, not 1000 |
|`VARCHAR` |In ByteHouse, it is an alias for the String type, with no length limit.<br><br>In MySQL, its length limit ranges from 0\-65535 bytes. |
|`BINARY` |In ByteHouse, it is an alias for the Fixedstring type, with no length limit. |
|`DATE` |1. Date16 scope is 1970 \- 2149<br><br>2. Date32 scope is 1900\-2299 |
|`DATETIME` |1. ByteHouse is divided into the Data types Datetime and Datetime64. Datetime does not support numbers; Datetime64 supports 0\-9 digits.<br><br>2. Datetime occupies 4 bytes, Datetime64 occupies 8 bytes.<br><br>3. Suggestion: Use the behavior of Datetime64 to achieve the same behavior as MySQL.<br><br>4. DateTime/DateTime64 stores time as a Unix Timestamp.<br><br>5. The value itself is independent of the timezone. In binary format, it is represented as a Unix Timestamp.<br><br>6. In the text format, it is serialized as YYYY\-MM\-DD hh:MM:ss format and parsed from that. The text format depends on the timezone.<br><br>7. The range of DateTime/DateTime64 is the same as Date/Date32. |
|`TIMESTAMP` |Use the number type and internally convert it to datetime. |
|`Array` |This data type is not supported yet under MySQL mode. |
|`Map` |This data type is not supported yet under MySQL mode. |
|`JSON` |Not supported yet for this data type under MySQL mode. |


<span id="cfafd353"></span>
## Numerical types

<span id="7b2aac9f"></span>
### UInt8, UInt16, UInt32, UInt64, UInt256, Int8, Int16, Int32, Int64, Int128, Int256

Fixed\-length integers.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When creating a table, integer number parameters (such as TINYINT(augt), SMALLINT(16), INT(32), BIGINT(64)) can be set, but ByteHouse will automatically ignore these parameters.</div>


**Alias**


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


**UInt value range**


* `UInt8` — [0 : 255]

* `UInt16` — [0 : 65535]

* `UInt32` — [0 : 4294967295]

* `UInt64` — [0 : 18446744073709551615]

* `UInt256` — [0 : 115792089237316195423570985008687907853269984665640564039457584007913129639935]


<span id="4ce2d114"></span>
### Float32, Float64

**Alias**


* `Float32` — `FLOAT`.

* `Float64` — `DOUBLE`.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When creating a table, floating\-point numerical parameters (such as FLOAT(dec), FLOAT(15, 22), DOUBLE(dec), DOUBLE(apr, 18)) can be set, but ByteHouse will ignore them.</div>


<span id="9d381be1"></span>
### Decimal(P, S), decimal32(S), decimal64(S), decimal128(S)

Signed fixed\-point numbers can maintain precision during addition, subtraction, and multiplication operations. For division, the least significant digit will be discarded (not rounded).

**Alias**


* `Decimal` — `DEC`


**Parameters**


* P \- precision, with a range of [1 : 76], represents the significant digits in the number (including decimals).

* S \- scale, with a range of [0 : P], represents the number of digits to the right of the decimal point.


In Decimal(P, S), when the P parameter is within the following ranges, it is equivalent to the latter:


* P in [1 : 9], equivalent to Decimal32(S)

* P in [10 : 18], equivalent to Decimal64(S)

* P is equivalent to Decimal128(S) at [19:38].


**Decimal number range**


* Decimal32(S) ：( \-1 \* 10^(9 \- S), 1 \* 10^(9 \- S) )

* Decimal64(S) ：( \-1 \* 10^(18 \- S), 1 \* 10^(18 \- S) )

* Decimal128(S) ： ( \-1 \* 10^(38 \- S), 1 \* 10^(38 \- S) )


For example, Decimal32(4) can include numbers from \-99999.9999 to 99999.9999.

<span id="e790d165"></span>
## String and binary types

<span id="ea13fd1a"></span>
### String

Strings of any length. Unlimited length. The value can contain any set of bytes, including null bytes.

The String type has replaced other types such as VARCHAR, BLOB, CLOB in other databases.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When creating a table, string field numerical parameters (such as VARCHAR(255)) can be set, but ByteHouse will ignore them.</div>


**Encoding**

ByteHouse does not have a concept of encoding. Strings can contain any set of bytes, which are stored and output as they are.

If you need to store text, we recommend using UTF\-8 encoding. At a minimum, if your terminal uses UTF\-8 (recommended), you can read and write your values without conversion.

Similarly, some functions that handle strings also have separate variants that work assuming the string contains a set of bytes representing UTF\-8 encoded text.

For example, the "length" function calculates the length of the string in bytes, whereas the "lengthUTF8" function calculates the length of the string in Unicode code points, assuming the value is UTF\-8 encoded.

<span id="85e1a42c"></span>
### Fixedstring(N)

Strings of fixed length N (N is a positive integer).

You can use the following syntax to declare columns of `FixedString` type:

```Plain
 FixedString(N)
```


Where N is a natural number.

When the data length is exactly N bytes, the FixedString type is very efficient. In other cases, it may decrease efficiency.

Examples of values that can be stored efficiently in `FixedString` type columns:


* Binary representation of IP addresses (IPv6 uses `FixedString(16)`).

* Language codes (ru_RU, en_US, etc.).

* Currency codes (USD, RUB, etc.).

* Binary representation of hash values (MD5 uses `FixedString(16)`, SHA256 uses `FixedString(32)`).


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If you want to store UUID values, use the UUID data type.</div>


When inserting data into ByteHouse:


* If the byte count of a string is less than N, the string will be padded with null bytes.

* If the byte count of a string exceeds N bytes, it raises a `Too Large value for FixString(N)`exception.


When querying data, ByteHouse does not remove trailing null bytes from strings. If using the `WHERE` clause, manually add null bytes to match the fixed string values.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



1. <div data-tips="true" data-tips-type="warning">This method is different from MySQL's <code>CHAR</code> type (MySQL pads with spaces and removes them on output).</div>


2. <div data-tips="true" data-tips-type="warning">The length of FixedString(N) values is constant. Even if FixedString(N) values are only padded with null bytes, the length function will return N, but in this case, the empty function will return 1.</div>



<span id="685ce128"></span>
## Date and time data types

<span id="5d6cbb3c"></span>
### Date

Occupies two bytes, storing the number of days since 1970\-01\-01 (unsigned), with an upper limit of the year 2148.

The stored value does not contain a timezone.

<span id="0f1fbeb0"></span>
### DateTime

Alias:


* `DateTime` — `TIMESTAMP`


Stores Unix timestamps using four bytes (unsigned). Represented as a calendar date and time of day. Precision to the second.

```Plain
DateTime([timezone])
```


Supported value range: [1970\-01\-01 00:00:00, 2105\-12\-31 23:59:59].

<span id="2c838c6b"></span>
## Semi\-structured data type

<span id="ef86a502"></span>
### Array(T)

Array(T), an array consisting of elements of type T. T can be any type, including array types. The maximum size of the array is one million elements.

**For example**

You can use functions to create arrays:

```Plain
array(T)
```


You can also use square brackets.

```Plain
[]
```


<span id="124850fe"></span>
### Map(key, value)

`Map(Key, Value)` can store `Key:Value` pairs.


* `Key` — Key of the pair, the type can be: [String](https://clickhouse.com/docs/sql-reference/data-types/string), [Integer](https://clickhouse.com/docs/sql-reference/data-types/int-uint), [LowCardinality](https://clickhouse.com/docs/sql-reference/data-types/lowcardinality), or [FixedString](https://clickhouse.com/docs/sql-reference/data-types/fixedstring).

* `Value` — Value of the pair, the type can be: [String](https://clickhouse.com/docs/sql-reference/data-types/string), [Integer](https://clickhouse.com/docs/sql-reference/data-types/int-uint), [Array](https://clickhouse.com/docs/sql-reference/data-types/array), [LowCardinality](https://clickhouse.com/docs/sql-reference/data-types/lowcardinality), or [FixedString](https://clickhouse.com/docs/sql-reference/data-types/fixedstring).


Using `a['Key']` you can retrieve the corresponding value from a `a Map('Key', 'Value')` column, which is a linear complexity query.

**Basic usage**

Example table:

```Plain
CREATE TABLE table_map (a Map(String, UInt64)) ENGINE=Memory;

INSERT INTO table_map VALUES ({'key1':1, 'key2':10}), ({'key1':2,'key2':20}), ({'key1':3,'key2':30});
```


Search all values for `Key2`:

```Plain
SELECT a{'key2'} FROM table_map;
```


Query results:

```Plain
┌─mapElement(a, 'key2')─┐

│                    10  │

│                    20  │

│                    30  │

└────────────── ┘
```


<span id="dd10dd74"></span>
### Tuple(T1,T2...)

Tuple(T1, T2, ...) tuple, each element has a separate Type.

**Basic Usage**

You can use functions to create tuples:

```Plain
tuple(T1, T2, ...)
```


Example of creating a tuple:

```Plain
SELECT tuple(1,'a') AS x, toTypeName(x)
```


<span id="264a9928"></span>
### Enum8, Enum 16

Enumeration Type composed of named values.

The name value must be declared as `'string' = integer` correctly. ByteHouse only stores numbers but supports manipulating values by name.

ByteHouse supports:


* Enum8: 8\-bit enumeration. It can contain up to 256 values of enumeration within the range [\-128, 127].

* Enum16: 16\-bit enumeration. It can contain up to 65536 values of enumeration within the range [\-32768, 32767].


**Basic usage**

```Plain
CREATE TABLE t_enum(x Enum8('hello' = 1, 'world' = 2)) ENGINE = Memory;

INSERT INTO t_enum VALUES ('hello'), ('world'), ('hello');
```


Column x can only store values listed in the type definition: `'hello'` or `'world'`. If you try to save any other value, ByteHouse will raise an exception.

When you query data from the table, ByteHouse outputs the string value in `Enum`.

```Plain
SELECT * FROM t_enum
```


<span id="66a4a999"></span>
### Nested(n1 T1, n2 T2, …)

Nested data structures are similar to nested tables. The parameters (column name and type) of nested data structures are similar to those in a CREATE query. Each table can contain any number of rows of nested data structures.

**Basic usage**

```Plain
CREATE TABLE visits(Goals Nested(ID UInt32, Price Int64)) ENGINE = Memory;

INSERT INTO visits values ([1],[1]);
```


The above example declares a nested data structure named `Goals`, which contains conversion data related to visitors (the goals that visitors have reached). In the 'visits' table, each row can correspond to zero or any number of conversion data.

Only single\-level nesting is supported. In the columns of the nested structure, if the type of a column is an array, that column is actually the same as a multi\-dimensional array, so the support for nesting levels is very limited (such columns are not supported for storage in the MergeTree engine).

In most cases, a single column is specified for processing nested data structures. To achieve this, the column names are connected by a dot. These columns form a set of matching types. In the same nested data, all columns have the same length.

```Plain
SELECT Goals.ID, Goals.Price FROM visits WHERE length(Goals.ID) < 5 LIMIT 10;
```


<span id="88eaec65"></span>
## Other special data types

<span id="6bc5d0eb"></span>
### IPv4

`IPv4` is a Domain type compatible with the `UInt32` type in binary, used to store the values of IPv4 addresses. It provides more compact binary storage while supporting more readable input\-output formats.

**Basic use**

```Plain
CREATE TABLE hits (url String, from IPv4) ENGINE = Memory;

DESCRIBE TABLE hits;
```


When writing and querying, the `IPv4` type recognizes more user\-friendly input\-output formats:

```Plain
INSERT INTO hits (url, from) VALUES ('https://wikipedia.org', '116.253.40.133')('https://clickhouse.tech', '183.247.232.58')('https://clickhouse.tech/docs/en/', '116.106.34.242');

SELECT * FROM hits;
```


<span id="5c9ffd6e"></span>
### IPv6

`IPv6` is a Domain Type that is binary\-compatible with `FixedString(16)` Type and is used to store the values of IPv6 addresses. It offers a more compact binary storage while supporting the recognition of more user\-friendly input and output formats.

**Basic usage**

```Plain
CREATE TABLE hits (url String, from IPv6) ENGINE = Memory;

DESCRIBE TABLE hits;
```


When writing and querying, the `IPv6` Type can recognize more user\-friendly input and output formats:

```Plain
INSERT INTO hits (url, from) VALUES ('https://wikipedia.org', '2a02:aa08:e000:3100::2')('https://clickhouse.tech', '2001:44c8:129:2632:33:0:252:2')('https://clickhouse.tech/docs/en/', '2a02:e980:1e::1');

SELECT * FROM hits;
```


<span id="bc071d7e"></span>
### UUID

UUID (Universal Unique Identifier) is a 16\-byte number used to identify records.

Examples of UUID Type values are as follows:

```Plain
61f0c404-5cb3-11e7-907b-a6006ad3dba0
```


If the UUID column value is not specified when inserting a new record, the UUID value will be filled with zero:

```Plain
00000000-0000-0000-0000-000000000000
```


**Basic usage**

This example demonstrates the creation of a table with a UUID type column and inserting a value into the table.

```Plain
CREATE TABLE t_uuid (x UUID, y String) ENGINE=Memory;

INSERT INTO t_uuid SELECT generateUUIDv4(), 'Example 1';

SELECT * FROM t_uuid
```


<span id="93a98dbd"></span>
### Nullable(T)

Allows using special marks ([NULL](https://clickhouse.com/docs/sql-reference/data-types/nullable)) to indicate "missing values," which can be stored together with the normal values of `TypeName`. For example, a column of type `Nullable(Int8)` can store values of type `Int8`, and rows without values will store `NULL`.

For `TypeName`, composite data types [Array](https://clickhouse.com/docs/sql-reference/data-types/array) and [Tuple](https://clickhouse.com/docs/sql-reference/data-types/tuple) are not allowed. Composite data types can contain values of type `Nullable`, such as `Array(Nullable(Int8))`.

`Nullable` type fields cannot be included in table indexes.

Unless otherwise specified in the ClickHouse server configuration, `NULL` is the default value for any `Nullable` type.

**Basic use**

```SQL
CREATE TABLE t_null(x Int8, y Nullable(Int8)) ENGINE = Memory;

INSERT INTO t_null VALUES (1, NULL), (2, 3);

SELECT x + y FROM t_null;
```


<span id="关于-nullable"></span>
##### About Nullable

The current column may be empty. All basic types can be nullable, formatted as: Nullable(T), for example, Nullable(Int64). Except under the following conditions:


* Complex types Map and Array cannot be nullable.

* Specific fields during table creation cannot be nullable:

   * Partition key

   * Shard key

   * Order\-by key
