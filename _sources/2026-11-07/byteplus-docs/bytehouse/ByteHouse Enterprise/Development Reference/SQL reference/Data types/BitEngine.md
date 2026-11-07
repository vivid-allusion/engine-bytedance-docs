---
title: "BitEngine"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/bitengine"
---

BitEngine is an efficient **dataset** processing model, part of the query analysis Database ClickHouse. BitEngine is based on the MergeTree Family storage engine and introduces the `BitMap64` type, developing a series of related calculation functions. BitEngine's `BitMap64` type is suitable for expressing sets of a large number of entity IDs with specific relationships, converting set operations of union, intersection, and complement to `bitmap` operations, thereby achieving performance metrics far exceeding normal queries. Tests with released services have shown that using BitEngine results in a 10 to 50-fold improvement in query speed compared to conventional and Array or user table methods.
Meanwhile, we can also improve the computing performance of user-inputted bitmaps through **dictionary encoding**. Dictionary encoding is a data compression method, one part of BitEngine, used to encode user-inputted IDs in increasing numerical order, solving the problem of excessively sparse Bitmap storage, which cannot maximize its advantages.
Without using dictionary encoding, one can still use BitEngine’s functions and aggregate functions.
:::warning
BitEngine does not support HaUniqueMergeTree engine, only the Default HaMergeTree or MergeTree engine types.
:::
<span id="bb5e86a0"></span>
# Basic usage
Here, we use a standalone test as an example to introduce the basic methods of creating tables and importing data.
<span id="d9b0f420"></span>
## Create tables
BitEngine provides the `BitMap64` data type. When creating tables, we need to set the data type for storing cohort packages to `BitMap64`, for example:
```sql
CREATE TABLE [db.]table_name (
p_date Date, 
slice_id UInt64, 
tag String, 
ids BitMap64
) ENGINE = MergeTree PARTITION BY p_date ORDER BY tag_id 
SETTINGS index_granularity = 128
```

The dictionary encoding process in BitEngine is automatically completed by the engine. Users can activate dictionary encoding by adding the `BitMap64` type with the `BitEngineEncode` attribute. For example:
```SQL
CREATE TABLE [db.]table_name (
tag String,
slice_id UInt64, 
p_date Date,
ids BitMap64 BitEngineEncode
)ENGINE = HaMergeTree('/clickhouse/xxxx/{shard}', '{replica}')
PARTITION BY p_date
ORDER BY tag
SETTINGS index_granularity = 128
```

If you are creating tables on the ByteHouse console, click on customize and then manually input the `BitMap64` or `BitMap64 BitEngineEncode` type.
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24ab096216554689aa82e99e62203330~tplv-goo7wpa0wc-image.image =764x)
<span id="0228bf6b"></span>
## Import data
The primary data storage format in BitEngine is `BitMap64`. When importing data, users can directly use types like `Array(UInt64)` for data import methods, for example:
```sql
INSERT INTO TABLE [db.]table_name values ('2020-01-01', 1, 'male', [1,2,3,4,5])
```

BitEngine automatically stores `Array` type data as `BitMap64` type, and thereafter, both storage and calculation types are `BitMap64` type.
File import methods support the use of CSV, JSON, and others, similar to the methods supported for importing `Array` type data.
<span id="1542974e"></span>
## Search
BitEngine supports all query methods of ClickHouse and can use the original functions of ClickHouse to operate `BitMap64` type, but they might not be highly efficient. For this reason, we have developed a series of functions for efficient operation of BitMap64 type, For details, refer to [BitEngine Function](/docs/bytehouse/46748).
For example, we can use the bitmapColumnHas`(bitmap_column, integer)` function to receive a column of BitMap64 data type and check if the column contains a specified element:
```SQL
select bitmapColumnHas(ids, 1) from [db.]table_name
```

<span id="e61faa61"></span>
# Function and operation interface
For details, refer to  [BitEngine Function](/docs/bytehouse/46748).
