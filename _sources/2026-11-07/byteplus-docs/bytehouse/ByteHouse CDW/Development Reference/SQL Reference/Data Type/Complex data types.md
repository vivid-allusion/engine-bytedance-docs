---
title: "Complex data types"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/complex-data-types"
---

<span id="9f700f12"></span>
# Map Type

<span id="57befa05"></span>
## Definition

Map type stores `k-v` key\-value pairs, similar to Java's Map. Primarily divided into Implicit Column Map (the default type, also known as ByteMap) and KV Map. The main difference lies in the data storage method, where the Implicit Column Map stores all values corresponding to each key as separate implicit columns, whereas KV Map is similar to Array(Tuple(K, V)), storing all appearing keys and values together.

Map keys allowed include `Integers` (such as `Int8`, `UInt64`, etc.), `Float32`, `Float64`, `Date`, `DateTime`, `String`, `FixedString`, `LowCardinality`, `UUID`, `Enums`, and `Nullable` is not supported.

There are no restrictions on the value types for KV Map, whereas the Implicit Column Map value types can include `Integers` (such as `Int8`, `UInt64`, etc.), `Float32`, `Float64`, `Date`, `DateTime`, `String`, `FixedString`, `LowCardinality`(Nullable()), `Array`. It is `Not supported` as the top level or if it contains `Tuple` type.

Adding a `KV` suffix to the type during definition allows for the use of KV Map, otherwise it defaults to Implicit Column Map. For example, `Map(Int16, String)`, `Map(String, Array(Int32)) KV`, `Map(String, LowCardinality(Nullable(String)))`.

<span id="7485bf45"></span>
## Important Notes


* Implicit column Maps are suitable for scenarios where only a small number of map keys are queried at a time, such as`SELECT m{'k1'} FROM xx`. Query performance can be improved using curly braces`{}`(equivalent to`mapElement`function);

* KV Maps are suitable for querying the entire map column, as in`SELECT m FROM xx`;

* When a large number of keys occur in a single partition, implicit column maps may affect writing speed and resource consumption. It is recommended not to exceed 1000 keys (equivalent to a wide table with 1000 columns);

* Map columns do not support index building, so using them directly in SQL query statements without other filtering conditions is not advisable. Minimize the amount of data scanned.

* For a single map record, KV Maps allow duplicate keys, but implicit column Maps only save the value of the first occurrence of a key.

* The order of key insertion is not guaranteed. For example, when the entry`{"a":1,"b":2,"d":3}`is written, the search result will be`{"d":3, "a":1, "b":2}`.


<span id="cba98743"></span>
## Create tables

When creating tables, you can specify the data type of columns as`Map`.

```SQL
CREATE TABLE example_map_table (
    id UInt64,
    m1 Map(String, String),   -- Implicit column Map
    m2 Map(String, String) KV -- KV Map
) ENGINE = CnchMergeTree()
ORDER BY id;
```


<span id="2ef9a240"></span>
## Insert Data

When inserting data, you can use the key\-value pair format or use the `map` function in SELECT.

```SQL
-- INSERT INTO xx VALUES, use a format similar to JSON (replace with single quotes).
INSERT INTO example_map_table (id, m1, m2) VALUES
(1, {'name': 'Alice', 'age': '30'}, {'name': 'Bob', 'age': '25'});

-- INSERT INTO xx SELECT, you can use the map function to generate data of the Map type.
INSERT INTO example_map_table (id, m1, m2)
SELECT 2, map('name', 'Alice', 'age', '31'), map('name', 'Bob', 'age', '26');
```


<span id="304472e7"></span>
## Query Data

Using functions provided by Map facilitates querying and processing Map data.

Query specific Key in Map data

```SQL
-- 1. Use {} or the mapElement function.
-- The return value type is Nullable(ValueType). It returns Null when the key does not exist.
-- When querying the implicit column Map, you can read only the data of the corresponding implicit column, which has good performance.
SELECT
    id,
    m1{'name'} AS m1_name,
    toTypeName(m1_name) AS m1_name_type,
    mapElement(m2, 'city') AS m2_city,
    toTypeName(m2_city) AS m2_city_type
FROM example_map_table;

-- result:
-- 1    'Alice'    'Nullable(String)'    NULL    'Nullable(String)'
-- 2    'Alice'    'Nullable(String)'    NULL    'Nullable(String)'


-- 1. Use [] or the arrayElement function.
-- The return value type is ValueType. It returns the default value when the key does not exist.
-- When querying the implicit column Map, you need to read out the entire Map first, and the performance is relatively poor.
SELECT
    id,
    m1['name'] AS m1_name,
    toTypeName(m1_name) AS m1_name_type,
    arrayElement(m2, 'city') AS m2_city,
    toTypeName(m2_city) AS m2_city_type
FROM example_map_table;
-- 1    'Alice'    'String'    ''    'String'
-- 2    'Alice'    'String'    ''    'String'
```


Query the entire Map column

```SQL
-- When the number of keys in the implicit column Map is large, the performance of this kind of query is poor, and you can consider using the KV Map.
SELECT 
    id,
    m1,
    m2
FROM example_map_table;

-- result:
-- 1    {'age':'30','name':'Alice'}    {'name':'Bob','age':'25'}
-- 2    {'age':'31','name':'Alice'}    {'name':'Bob','age':'26'}
```


Use Map Key (corresponding Value) as filter conditions

```SQL
SELECT
    id,
    m1{'age'}
FROM example_map_table
WHERE m1{'name'} = 'Alice' AND m2{'age'} = '26';

-- result:
-- 2    31
```


<span id="a0286f3c"></span>
## Using examples

**Example 1: Dynamic attribute storage**

In some application scenarios, different records may have different attributes. The MAP data type can conveniently store these dynamic properties.

```SQL
CREATE TABLE dynamic_attributes (
    entity_id UInt64,
    attributes Map(String, String)
) ENGINE = CnchMergeTree()
ORDER BY entity_id;

INSERT INTO dynamic_attributes (entity_id, attributes) VALUES
(1, {'color': 'red', 'size': 'M')),
(2, {'brand': 'Nike', 'material': 'cotton'));
```


We can query all records with specific attributes:

```SQL
SELECT
    entity_id,
    attributes
FROM dynamic_attributes
WHERE attributes{'color'} = 'red';
```


<span id="328f23ae"></span>
# ARRAY

<span id="af4f67dc"></span>
## Definition

ARRAY is an array composed of elements of type **`T`**.

**`T`** can be of any type, including the array type. However, using multi\-dimensional arrays is not recommended, as ByteHouse has limited support for multi\-dimensional arrays. For example, multi\-dimensional arrays cannot be stored in a `MergeTree` table.

<span id="26b11a6e"></span>
## Create array

You can create arrays using the array function.

```Plain
array(T)
```


Example:

```SQL
SELECT array(1, 2) AS x, toTypeName(x)
```


```Plain
┌─x─────┬─toTypeName(array(1, 2))─┐
│ [1,2] │ Array(UInt8)            │
└───────┴─────────────────────────┘
```


```SQL
SELECT [1, 2] AS x, toTypeName(x)
```


```Plain
┌─x─────┬─toTypeName([1, 2])─┐
│ [1,2] │ Array(UInt8)       │
└───────┴────────────────────┘
```


<span id="518cb641"></span>
## Use array

ByteHouse will automatically detect array elements and calculate the minimum data type for storing these elements. If NULL or nullable elements exist within the elements, the array's element type will become nullable.

If ByteHouse cannot determine the data type, it will generate an exception. This happens when attempting to create an array containing both strings and numbers simultaneously (SELECT array(1, 'a')).

Automatic Data Type Detection Example:

```SQL
SELECT array(1, 2, NULL) AS x, toTypeName(x)
```


```Plain
┌─x──────────┬─toTypeName(array(1, 2, NULL))─┐
│ [1,2,NULL] │ Array(Nullable(UInt8))        │
└────────────┴───────────────────────────────┘
```


If you try to create an array with incompatible data types, ByteHouse will raise an exception:

```SQL
SELECT array(1, 'a')
```


```Plain
Code: 386, Error: DB::Exception: There is no supertype for types There is no supertype for types UInt8, String because some of them are String/FixedString and some of them are not SQLSTATE: HY000
```


<span id="008925b4"></span>
## Array size

You can find the size of an array using the **`size0`** subcolumn without reading the entire column. For multi\-dimensional arrays, you can use **`sizeN-1`**, where **`N`** is the desired dimension.

**Example**

SQL query:

```SQL
CREATE TABLE t_arr (`arr` Array(Array(Array(UInt32)))) ENGINE = CnchMergeTree ORDER BY tuple();

INSERT INTO t_arr VALUES ([[[12, 13, 0, 1],[12]]]);

SELECT arr.size0, arr.size1, arr.size2 FROM t_arr;
```


As a result:

```Plain
┌─arr.size0─┬─arr.size1─┬─arr.size2─┐
│         1 │ [2]       │ [[4,1]]   │
└───────────┴───────────┴───────────┘
```


<span id="68e03e00"></span>
# Tuple

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each element of the tuple has its separate Type.</div>


<div data-tips="true" data-tips-type="tip">Tuples cannot be stored in tables (except in\-memory tables). They can be used for temporary column grouping. In the query, IN expressions and lambda functions with specific parameters can be used to group temporary columns</div>


<div data-tips="true" data-tips-type="tip">Tuples can be the result of a query. In this case, for text formats other than JSON, the values in the brackets are separated by commas. In Json format, tuples are output as arrays (in square brackets).</div>


<span id="59032c9e"></span>
## Create Tuple

Tuples can be created using functions:

```Plain
tuple(T1, T2, ...)
```


Example of creating a tuple:

```SQL
SELECT tuple(1,'a') AS x, toTypeName(x)
```


```Plain
┌─x───────┬─toTypeName(tuple(1, 'a'))─┐
│ (1,'a') │ Tuple(UInt8, String)      │
└─────────┴───────────────────────────┘
```


<span id="397cf292"></span>
## Data types in tuples

When dynamically creating tuples, ByteHouse automatically assigns the smallest expressible type for each parameter of the tuple. If the parameter is [NULL](https://clickhouse.com/docs/zh/sql-reference/data-types/tuple#null-literal), then the corresponding tuple element is [nullable](https://clickhouse.com/docs/zh/sql-reference/data-types/nullable).

Automatic data type detection example:

```SQL
SELECT tuple(1, NULL) AS x, toTypeName(x)
```


```Plain
┌─x────────┬─toTypeName(tuple(1, NULL))──────┐
│ (1,NULL) │ Tuple(UInt8, Nullable(Nothing)) │
└──────────┴─────────────────────────────────┘
```


<span id="f5839655"></span>
# Enumeration

It includes the **`Enum8`** and **`Enum16`** types. An **`Enum`** stores the correspondence of  **`'string' = integer`**. In ClickHouse, although users use string constants, all operations involving the **`Enum`** data type are performed based on the values containing integers. This is more efficient in terms of performance compared to using the **`String`** data type.


* **`Enum8`** is described using  **`'String' = Int8`**.

* **`Enum16`** is described by  **`'String' = Integer`**.


<span id="341fac73"></span>
## Usage example

Create a column with an enumeration type **`Enum8('hello' = 1, 'world' = 2)`** :

```SQL
CREATE TABLE t_enum
(
    x Enum8('hello' = 1, 'world' = 2)
)
ENGINE = TinyLog
```


This **`x`** column can only store the values listed in the type definition:  **`'hello'`**  or  **`'world'`** . If you try to save any other value, ClickHouse throws an exception.

```SQL
INSERT INTO t_enum VALUES ('hello'), ('world'), ('hello')
```


```Plain
Ok.

3 rows in set. Elapsed: 0.002 sec.
```


```SQL
INSERT INTO t_enum VALUES('a')
```


```Plain
Exception on client:
Code: 49. DB::Exception: Unknown element 'a' for type Enum8('hello' = 1, 'world' = 2)
```


When you query data from a table, ClickHouse outputs string values from **`Enum`**.

```SQL
SELECT * FROM t_enum
```


```Plain
┌─x─────┐
│ hello │
│ world │
│ hello │
└───────┘
```


If you want to see the numerical value of corresponding rows, you must convert the **`Enum`** values to integer type.

```SQL
SELECT CAST(x, 'Int8') FROM t_enum
```


```Plain
┌─CAST(x, 'Int8')─┐
│               1 │
│               2 │
│               1 │
└─────────────────┘
```


To create enumeration values in a query, you also need to use **`CAST`**.

```SQL
SELECT toTypeName(CAST('a', 'Enum8(\'a\' = 1, \'b\' = 2)'))
```


```Plain
┌─toTypeName(CAST('a', 'Enum8(\'a\' = 1, \'b\' = 2)'))─┐
│ Enum8('a' = 1, 'b' = 2)                              │
└──────────────────────────────────────────────────────┘
```


<span id="25713bd8"></span>
## Rules and usage

Each value range for the **`Enum8`** type is  **`-128 ...`**  **`127`**, each value range for the **`Enum16`** type is  **`-32768 ...`**  **`32767`**。 Every number or string must be different. Empty strings are allowed. If an Enum type is specified (at the time of table definition), the numbers can be in any order. However, the order doesn't matter.

**`Enum`** strings and numerical values cannot be NULL.

**`Enum`** is included in the nullable types. Therefore, if you create a table using this query

```SQL
CREATE TABLE t_enum_nullable
(
    x Nullable( Enum8('hello' = 1, 'world' = 2) )
)
ENGINE = TinyLog
```


Not only can you store  **`'hello'`**  and  **`'world'`** , but you can also store **`NULL`**.

```SQL
INSERT INTO t_enum_nullable Values('hello'),('world'),(NULL)
```


In memory, the storage method of `Enum` columns is the same as the corresponding numerical `Int8` or `Int16`.

When read in text format, ClickHouse parses the value into a string and then searches in the enumeration value set for the corresponding string. If not found, an exception is thrown. When reading text format, it looks for the corresponding numerical value based on the string read. If not found, an exception is thrown.

When writing in text form, ClickHouse parses the value into a string for input. If the column data contains garbage data (numbers not from a valid set), an exception is thrown. Enum types are read and written in binary in the same way as `Int8` and `Int16`.

The implicit default value is the smallest numerical value.

In `ORDER BY`, `GROUP BY`, `IN`, `DISTINCT` and others, Enum behaves the same as the corresponding numbers. For example, sorting by number. For equality and comparison operators, Enum works the same as they do on underlying numbers.

Enum values cannot be compared with numbers. Enums can be compared with constant strings. If the string compared is not a valid Enum value, an exception will be thrown. You can use the IN operator to check whether an Enum exists in an Enum set, with the Enum in the set represented by a string.

Most operations involving numbers and strings are not applicable to Enums; for example, an Enum type cannot be added to a numerical value. However, Enum has a native `toString` function that returns its string value.

Enum values can be converted to numerical types using the `toT` function, where T is a numerical type. If `T` corresponds exactly to the underlying numerical type of the Enum, this conversion is zero\-cost.

Enum types can be changed with `ALTER` at no cost to modify corresponding set values. Enum members can be added or removed through an `ALTER` operation (safe so long as the table has not used that value). As a security measure, changing previously used Enum members will throw an exception.

Through the use of `ALTER` actions, `Enum8` can be converted to `Enum16` and vice versa, similar to converting `Int8` to `Int16`.

<span id="cb459f3c"></span>
# BitMap64

BitMap64 is a Data Type provided in ByteHouse which is similar to the Data Type offered by the ClickHouse community; the contrast between them is introduced as follows.

<span id="dfa64953"></span>
## Difference between ByteHouse bitmap and the community

ClickHouse community provides bitmap Data processing capabilities, for details, see [Bitmap Functions | ClickHouse Docs](https://clickhouse.com/docs/en/sql-reference/functions/bitmap-functions). Meanwhile, ByteHouse has also developed its own set of bitmap Data types and related functions. The similarities and differences are as follows:


|Similarities |Differences |
|---|---|
|* The underlying structure uses RoaringBitmap as the storage structure for bitmap data;<br><br>* Normal functions on the ClickHouse Official website are compatible with ByteHouse and can also be used;<br><br>* The bitmap data structure naturally de\-duplicates and the data is stored in order from smallest to largest |* User types are different<br><br>   * The ClickHouse community provides the user type `AggregateFunction(groupBitmap, UIntX)`, where X can be 8, 16, 32, 64, representing the bit length of upstream data.<br><br>   * ByteHouse provides the user type `BitMap64`, with a default selection of 64\-bit integer values.<br><br>* Differences in usage methods.<br><br>   * In ByteHouse, BitMap64 is more independent, allowing direct insertion during insert operations and can be printed directly through select.<br><br>   * BitMap64 in ByteHouse offers more advanced functions, allowing for more intuitive and concise writing of complex SQL. |


<span id="5885e415"></span>
## Define ByteHouse BitMap64 Type

You can define a bitmap Type using the keyword `BitMap64` in a table. Examples are as follows:

```SQL
CREATE TABLE test.bitmap_test (
    `p_date` Date, 
    `slice_id` UInt64,
    `tag_id` Int32,
    `tag_value` String, 
    `uids` BitMap64
) ENGINE = MergeTree 
PARTITION BY p_date
ORDER BY (tag_id, tag_value)
SETTINGS index_granularity = 128;
```


<span id="6241736f"></span>
## Create ByteHouse BitMap64 Type Data

Bitmap currently has two constructors: one uses `bitmapFromColumn` to construct from a column of data, or `arrayToBitmap` to construct from an array. Examples are as follows:

```SQL
=== number type is UInt64
select bitmapFromColumn(number) as rbm, toTypeName(rbm) from numbers(10);
-- {0,1,2,3,4,5,6,7,8,9}, "BitMap64"

select arrayToBitmap(groupArray(number)) as rbm, toTypeName(rbm) from numbers(10);
-- {0,1,2,3,4,5,6,7,8,9}, "BitMap64"
```


<span id="7a38183c"></span>
## Data writing for ByteHouse BitMap64 type

This section is divided into two parts: writing from external systems to ByteHouse tables and internal writing within ByteHouse.

<span id="554f8cf5"></span>
### External system import

Currently, data is mainly imported through files in text formats (CSV, JSONEachRow) and Parquet format.

In text files, collection data can be wrapped with `{}` or `[]`, which the engine automatically parses.

In Parquet, collection data can be stored using LIST, which the engine automatically converts.


* Import of files in CSV format is as follows:

   ```SQL
   cat ./test_bitmap_input.csv
   --
   "2024-01-01",0,11,"a","{0,1,2,3,4,5,6,7,8,9}"
   
   
   insert into test.bitmap_test format CSV infile 'test_bitmap_input.csv';
   ```
   

* Import of files in Parquet format is as follows:

   ```SQL
   parquet-meta ./test_bitmap_input.parquet
   ---
   file schema: schema
   -------------------------------------------------
   p_date:      REQUIRED INT32 O:UINT_16 R:0 D:0
   slice_id:    REQUIRED INT64 O:UINT_64 R:0 D:0
   tag_id:      REQUIRED INT32 R:0 D:0
   tag_value:   REQUIRED BINARY O:UTF8 R:0 D:0
   uids:        REQUIRED F:1
   .list:       REPEATED F:1
   ..element:   OPTIONAL INT64 O:UINT_64 R:1 D:2
    
   INSERT INTO test.bitmap_test FORMAT Parquet INFILE 'test_bitmap_input.parquet'
   ```
   


<span id="ad71f047"></span>
### Internal writing within ByteHouse

This typically involves calculating a bitmap from one table and writing it into the target table, usually implemented using `insert select`, which may need to be used in conjunction with the constructor in "Create BitMap64 Type Data".

Examples are as follows:


* Write back to the table after calculating from the bitmap table

   ```SQL
   INSERT INTO test.bitmap_test SELECT
       p_date,
       slice_id,
       100 AS tag_id,
       'test2' as tag_value,
       uids
   FROM
   (
       SELECT p_date, slice_id, subBitmap(uids, 1, 2) AS uids
       FROM test.bitmap_test
       WHERE tag_id = 1 and tag_value = 't1'
   );
   ```
   

* Building bitmap from a column data and writing into the table

   ```SQL
   INSERT INTO test.bitmap_test SELECT
       '2024-01-01' as p_date,
       1 as slice_id
       101 AS tag_id,
       'test2' as tag_value,
       bitmapFromColumn(number) as uids
   FROM numbers(10)
   ```
   

* A small part is written directly by using insert values

   ```SQL
   INSERT INTO test.bitmap_test values ('2024-01-01', 1, 102, 'test3', [1,2,3,4]);
   ```
   


<span id="d7bce266"></span>
## Query of BitMap64 Type in ByteHouse

<span id="8654db8c"></span>
### Direct query

BitMap64 Type in ByteHouse can be directly queried and displayed using select. However, it's important to note that when the number of bitmap elements is large (for example, tens of thousands), it is time\-consuming to print on the screen and it is not recommended to print directly.

```SQL
SELECT
    tag_id,
    uids
FROM test.bitmap_test
WHERE tag_id = 101
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5bb0c61fecff45d8837d10f6bb5fad41~tplv-goo7wpa0wc-image.image) </span>

If the number of bitmap elements is large, it is suggested to print the count for review.

```SQL
SELECT
    tag_id,
    bitmapCardinality(uids)
FROM test.bitmap_test
WHERE tag_id = 101
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d909d96b41cc49b5a49ab3b9b235e849~tplv-goo7wpa0wc-image.image) </span>

<span id="a07faa61"></span>
## Bitmap function

ByteHouse offers a rich set of function interfaces for querying Bitmap64 type data, encompassing categories such as normal functions, aggregate functions, and advanced aggregate functions. For the list of supported functions, usage guidance, conversion amongst community functions. For more details, refer to [BitMap function](https://docs.byteplus.com/docs/bytehouse/bitmap-function).

<span id="6ffe61f9"></span>
# Low cardinality type

Convert other data types into dictionary\-encoded types.

<span id="dda8107a"></span>
## Syntax

```SQL
LowCardinality(data_type)
```


<span id="e5175471"></span>
## **Parameter**


* `data_type` — String, FixedString, Date, DateTime, including numerical types, but excluding Decimal. For some data types, `LowCardinality` is not efficient, see [allow_suspicious_low_cardinality_types](https://clickhouse.com/docs/operations/settings/settings#allow_suspicious_low_cardinality_types) setting description for details.


<span id="05f629de"></span>
## Description

`LowCardinality` is a concept that changes the methods of data storage and processing. ClickHouse performs dictionary coding on columns containing LowCardinal [dictionary coding](https://en.wikipedia.org/wiki/Dictionary_coder) on columns containing LowCardinality. For many applications, processing dictionary\-encoded data can significantly increase the speed of SELECT queries.

The efficiency of using `LowCarditality` data type depends on the diversity of the data. If a dictionary contains less than 10,000 distinct values, then ClickHouse can perform more efficient data storage and processing. On the other hand, if a dictionary has more than 10,000 distinct values, the efficiency tends to be poorer.

When using character types, consider using `LowCardinality` instead of Enum. `LowCardinality` is generally more flexible and efficient.

<span id="91728ef3"></span>
## Example

Create a column of type `LowCardinality`:

```SQL
CREATE TABLE lc_t
(
    `id` UInt16,
    `strings` LowCardinality(String)
)
ENGINE = MergeTree()
ORDER BY id
```


<span id="25fb924d"></span>
## Relevant Settings and Functions

Settings:


* [low_cardinality_max_dictionary_size](https://clickhouse.com/docs/operations/settings/settings#low_cardinality_max_dictionary_size)

* [low_cardinality_use_single_dictionary_for_part](https://clickhouse.com/docs/operations/settings/settings#low_cardinality_use_single_dictionary_for_part)

* [low_cardinality_allow_in_native_format](https://clickhouse.com/docs/operations/settings/settings#low_cardinality_allow_in_native_format)

* [allow_suspicious_low_cardinality_types](https://clickhouse.com/docs/operations/settings/settings#allow_suspicious_low_cardinality_types)


Functions:


* [toLowCardinality](https://clickhouse.com/docs/sql-reference/functions/type-conversion-functions#tolowcardinality)


<span id="db361303"></span>
# Network Type (IPv4/IPv6)

<span id="0651f44a"></span>
## IPv4

`IPv4` is a Domain Type binary\-compatible with `UInt32` that is used for storing IPv4 address values. It offers more compact binary storage while supporting friendlier input\-output formats.

```SQL
CREATE TABLE hits (url String, from IPv4) ENGINE = MergeTree() ORDER BY url;

DESCRIBE TABLE hits;
```


```Plain
┌─name─┬─type───┬─default_type─┬─default_expression─┬─comment─┬─codec_expression─┐
│ url  │ String │              │                    │         │                  │
│ from │ IPv4   │              │                    │         │                  │
└──────┴────────┴──────────────┴────────────────────┴─────────┴──────────────────┘
```


You can also use columns of `IPv4` Type as primary keys.

```SQL
CREATE TABLE hits (url String, from IPv4) ENGINE = MergeTree() ORDER BY from;
```


During writing and querying, the `IPv4` Type can recognize friendlier input\-output formats.

```SQL
INSERT INTO hits (url, from) VALUES ('https://wikipedia.org', '116.253.40.133')('https://clickhouse.com', '183.247.232.58')('https://clickhouse.com/docs/en/', '116.106.34.242');
SELECT * FROM hits;
```


```Plain
┌─url────────────────────────────────┬───────────from─┐
│ https://clickhouse.com/docs/en/ │ 116.106.34.242 │
│ https://wikipedia.org              │ 116.253.40.133 │
│ https://clickhouse.com          │ 183.247.232.58 │
└────────────────────────────────────┴────────────────┘
```


Meanwhile, it provides more compact binary storage formats.

```SQL
SELECT toTypeName(from), hex(from) FROM hits LIMIT 1;
```


```Plain
┌─toTypeName(from)─┬─hex(from)─┐
│ IPv4             │ B7F7E83A  │
└──────────────────┴───────────┘
```


It cannot be implicitly converted to any Type other than `UInt32`. If you want to convert the value of an `IPv4` Type into a string, you can explicitly use `IPv4NumToString()` for conversion.

```SQL
SELECT toTypeName(s), IPv4NumToString(from) as s FROM hits LIMIT 1;
```


```Plain
┌─toTypeName(IPv4NumToString(from))─┬─s──────────────┐
│ String                            │ 183.247.232.58 │
└───────────────────────────────────┴────────────────┘
```


Or you can use `CAST` to convert it to `UInt32` Type.

```SQL
SELECT toTypeName(i), CAST(from as UInt32) as i FROM hits LIMIT 1;
```


```Plain
┌─toTypeName(CAST(from, 'UInt32'))─┬──────────i─┐
│ UInt32                           │ 3086477370 │
└──────────────────────────────────┴────────────┘
```


<span id="34dc8e6e"></span>
## IPv6

`IPv6` is a Domain Type binary\-compatible with `FixedString(16)`, used for storing IPv6 address values. It offers a more compact binary storage while supporting formats that are more readable during input and output.

```SQL
CREATE TABLE hits (url String, from IPv6) ENGINE = MergeTree() ORDER BY url;

DESCRIBE TABLE hits;
```


```Plain
┌─name─┬─type───┬─default_type─┬─default_expression─┬─comment─┬─codec_expression─┐
│ url  │ String │              │                    │         │                  │
│ from │ IPv6   │              │                    │         │                  │
└──────┴────────┴──────────────┴────────────────────┴─────────┴──────────────────┘
```


Meanwhile, you can also use `IPv6` Type as the primary key:

```SQL
CREATE TABLE hits (url String, from IPv6) ENGINE = MergeTree() ORDER BY from;
```


When writing and querying, the `IPv6` Type can recognize more user\-friendly input and output formats:

```SQL
INSERT INTO hits (url, from) VALUES ('https://wikipedia.org', '2a02:aa08:e000:3100::2')('https://clickhouse.com', '2001:44c8:129:2632:33:0:252:2')('https://clickhouse.com/docs/en/', '2a02:e980:1e::1');

SELECT * FROM hits;
```


```Plain
┌─url────────────────────────────────┬─from──────────────────────────┐
│ https://clickhouse.com          │ 2001:44c8:129:2632:33:0:252:2 │
│ https://clickhouse.com/docs/en/ │ 2a02:e980:1e::1               │
│ https://wikipedia.org              │ 2a02:aa08:e000:3100::2        │
└────────────────────────────────────┴───────────────────────────────┘
```


Meanwhile, it provides a more compact binary storage format:

```SQL
SELECT toTypeName(from), hex(from) FROM hits LIMIT 1;
```


```Plain
┌─toTypeName(from)─┬─hex(from)────────────────────────┐
│ IPv6             │ 200144C8012926320033000002520002 │
└──────────────────┴──────────────────────────────────┘
```


It cannot be implicitly converted to any other type except `FixedString(16)`. If you want to convert the `IPv6` Type value into a string, you can explicitly use `IPv6NumToString()` for conversion:

```SQL
SELECT toTypeName(s), IPv6NumToString(from) as s FROM hits LIMIT 1;
```


```Plain
┌─toTypeName(IPv6NumToString(from))─┬─s─────────────────────────────┐
│ String                            │ 2001:44c8:129:2632:33:0:252:2 │
└───────────────────────────────────┴───────────────────────────────┘
```


Or use `CAST` to convert it to `FixedString(16)`:

```SQL
SELECT toTypeName(i), CAST(from as FixedString(16)) as i FROM hits LIMIT 1;
```


```Plain
┌─toTypeName(CAST(from, 'FixedString(16)'))─┬─i───────┐
│ FixedString(16)                           │  ��� │
└───────────────────────────────────────────┴─────────┘
```


<span id="b7163ed2"></span>
# Aggregate function type

The intermediate state of the aggregate function can be obtained by adding a `-State` suffix to the function name. Meanwhile, when you need to access the final state data of that type, you need to obtain the final state data by using the same aggregate function name with a `-Merge` suffix.

`AggregateFunction` — A parameterized data type.

<span id="5ce502ea"></span>
## **Param**


* Aggregate function name

   ```Plain
   If the function has multiple parameter lists, please specify the values in the other parameter lists here. 
   ```
   

* Type of the aggregate function's param


<span id="4e428ede"></span>
## **Example**

```SQL
CREATE TABLE t
(
    column1 AggregateFunction(uniq, UInt64),
    column2 AggregateFunction(anyIf, String, UInt8),
    column3 AggregateFunction(quantiles(0.5, 0.9), UInt64)
) ENGINE = ...
```


Among others, uniq, anyIf (any+if), and quantiles are supported by ClickHouse as aggregate functions.

<span id="fba57d59"></span>
## Data writing

When you need to write data, you need to include it in an `INSERT SELECT` statement, and for data of type `AggregateFunction`, you must use the corresponding function ending with `-State`.

<span id="b392de8a"></span>
## **Function usage example**

```SQL
uniqState(UserID)
quantilesState(0.5, 0.9)(SendTiming)
```


Unlike functions such as `uniq` and `quantiles` which return the final aggregate result, functions with the `-State` suffix always return the intermediate state of data of type `AggregateFunction`.

Regarding `SELECT`, the `AggregateFunction` Type is always presented in a specific binary form across all output formats. For instance, you can use the `SELECT` statement to dump the state data of the function in `TabSeparated` format while using the `INSERT` statement to dump the data back.

<span id="b447db41"></span>
## Query Data

When querying data from `AggregatingMergeTree` tables, for fields of the `AggregateFunction` Type, you need to use the same aggregation function with the `-Merge` suffix to aggregate data. For fields that are not of `AggregateFunction` Type, include them in the `GROUP BY` clause.

The aggregation functions with the `-Merge` suffix can combine multiple intermediate states of `AggregateFunction` Type to calculate the final aggregation result.

For example, the results returned by the following two queries are always consistent:

```SQL
SELECT uniq(UserID) FROM table

SELECT uniqMerge(state) FROM (SELECT uniqState(UserID) AS state FROM table GROUP BY RegionID)
```
