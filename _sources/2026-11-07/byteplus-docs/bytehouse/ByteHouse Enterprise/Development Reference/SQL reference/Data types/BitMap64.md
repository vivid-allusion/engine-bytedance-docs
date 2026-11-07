---
title: "BitMap64"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/bitmap64"
---

<span id="d7cb096d"></span>
# Differences between ByteHouse bitmap and the community
ClickHouse community provides bitmap data processing capabilities, see [Bitmap Functions | ClickHouse Docs](https://clickhouse.com/docs/en/sql-reference/functions/bitmap-functions). Around the same time, ByteHouse also developed its own type and related functions for processing bitmap data. The similarities and differences between the two are as follows:
**Similarities:**

* Both use RoaringBitmap as the storage structure for bitmap data.
* The common functions on ClickHouse's community official website are compatible with ByteHouse and can also be used.
* The bitmap data structure naturally de-duplicates and the data is stored in ascending order.

**Differences:**

* The user types are different.
   * The ClickHouse community provides users with the type `AggregateFunction(groupBitmap, UIntX)`, where X can be 8, 16, 32, or 64, representing the bit length of the upstream data.
   * ByteHouse provides users with the type `BitMap64`, with the default choice being a 64-bit integer value.
* Differences in usage methods.
   * In ByteHouse, BitMap64 is more independent and can be directly inserted in insert statements and printed directly through select queries.
   * ByteHouse's BitMap64 offers more advanced functions, enabling the writing of complex SQL in a more intuitive and concise manner.

<span id="5f0bdd27"></span>
# Define ByteHouse BitMap64 type
You can define a bitmap type in the table using the type keyword `BitMap64`. Example as follows:
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

<span id="f55bd30f"></span>
# Create ByteHouse BitMap64 type data
Currently, there are two constructors for bitmap: use the `bitmapFromColumn` function to construct from a column of data, or use the `arrayToBitmap` function to construct from an array. As follows:
```SQL
select bitmapFromColumn(number) as rbm, toTypeName(rbm) from numbers(10);
-- {0,1,2,3,4,5,6,7,8,9}, "BitMap64"

select arrayToBitmap(groupArray(number)) as rbm, toTypeName(rbm) from numbers(10);
-- {0,1,2,3,4,5,6,7,8,9}, "BitMap64"
```

<span id="b460dd98"></span>
# Write data of ByteHouse BitMap64 type
This section is divided into two parts: external system writing into ByteHouse tables and internal writing in ByteHouse.
<span id="f2401eeb"></span>
### External system writing
Currently, it is mainly done by importing files in text formats (CSV, JSONEachRow) and Parquet format.
In text files, collection data can be wrapped with `{}` or `[]`, which the engine automatically parses;
In Parquet, collection data can be stored using LIST, which the engine automatically converts.
Import of files in CSV format is as follows:
```SQL
cat ./test_bitmap_input.csv
--
"2024-01-01",0,11,"a","{0,1,2,3,4,5,6,7,8,9}"


insert into test.bitmap_test format CSV infile 'test_bitmap_input.csv';
```

Import of files in Parquet format is as follows:
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

<span id="b70c1b69"></span>
### ByteHouse internal writing
This is typically achieved by calculating a bitmap from one table and then writing it into a target table, usually implemented using `insert select`. At this point, it might be necessary to use it in conjunction with the constructor from "Creating BitMap64 Data".
Example as follows:

* After calculating from the bitmap table, write back to the table.

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


* Build a bitmap from a column of data and write it into the table.

```SQL
INSERT INTO test.bitmap_test SELECT
    '2024-01-01' as p_date,
    1 as slice_id
    101 AS tag_id,
    'test2' as tag_value,
    bitmapFromColumn(number) as uids
FROM numbers(10)
```


* A few parts are directly written into by insert values explicitly.

```SQL
INSERT INTO test.bitmap_test values ('2024-01-01', 1, 102, 'test3', [1,2,3,4]);
```

<span id="7dc6ef09"></span>
# ByteHouse BitMap64 type queries
<span id="5d5594c8"></span>
## Direct query
ByteHouse BitMap64 type can be directly queried and displayed through select. However, note that if the bitmap has a large number of elements (for example, tens of thousands), printing it on the screen takes a long time, and direct printing is not recommended.
```SQL
SELECT
    tag_id,
    uids
FROM test.bitmap_test
WHERE tag_id = 101
```

<div style="text-align: center"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1889a0d802ab47a598ff06cee13216f7~tplv-goo7wpa0wc-image.image" width="892px" /></div>

If the bitmap has many elements, it is advisable to print the number of elements for inspection.
```SQL
SELECT
    tag_id,
    bitmapCardinality(uids)
FROM test.bitmap_test
WHERE tag_id = 101
```

<div style="text-align: center"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9e6c933c6989442ab0e03c38920e4a51~tplv-goo7wpa0wc-image.image" width="800px" /></div>

<span id="a8255bc3"></span>
## Use JDBC drivers
Please refer to the guidelines provided by [ByteHouse BitMap64 in JDBC usage](https://bytedance.larkoffice.com/wiki/TX1gwTcWDisW7RkWKBAcEWiMnpg?from=from_copylink).
<span id="288495d3"></span>
## General functions
> The function takes a record or a BitMap64 object and returns a result row.


| | | | | | \
|Order No. |Function Interface |Parameter Description |Return Value |Function Explanation |
|---|---|---|---|---|
| | | | | | \
|1 |arrayToBitmap([x1, …]) |\
| |-> bitmap |Array of UIntN type |\
| | |N={8, 16, 32, 64} |BitMap64 object |\
| | | | |Create a bitmap object using an array |
| | | | | | \
|2 |*bitmapToArray(bitmap)* |\
| |-> [x1,...] |A BitMap64 object |UInt64 array |Convert a bitmap object to array format |
| | | | | | \
|3 |*bitmapAnd(bitmap1, bitmap2)* |\
| |-> bitmap |Two BitMap64 objects |\
| | | |BitMap64 object |bitmap's **intersection** operation |
| | | | | | \
|4 |*bitmapOr(bitmap1, bitmap2)* |\
| |-> bitmap |Two BitMap64 objects |BitMap64 object |Bitmap's **AND** operation |
| | | | | | \
|5 |*bitmapXor(bitmap1, bitmap2)* |\
| |-> bitmap |Two BitMap64 objects |BitMap64 object |Bitmap's **XOR** operation |
| | | | | | \
|6 |*bitmapAndnot(bitmap1, bitmap2)* |\
| |-> bitmap |Two BitMap64 objects |BitMap64 object |bitmap **poor** calculation |\
| | | | | |
| | | | | | \
|7 |*bitmapCardinality(bitmap)* |\
| |-> *integer* |A BitMap64 object |UInt64 numerical value |The number of elements in the bitmap |\
| | | | | |
| | | | | | \
|8 |*bitmapMin(bitmap)* |\
| |-> *integer* |A BitMap64 object |Numerical value of UInt64 |Find the smallest element in the bitmap |\
| | | | | |
| | | | | | \
|9 |*bitmapMax(bitmap)* |\
| |-> *integer* |A BitMap64 object |Numerical value of UInt64 |The largest element in bitmap |\
| | | | | |
| | | | | | \
|10 |*bitmapAndCardinality* |\
| |*(bitmap1, bitmap2)* |\
| |-> *integer* |Two BitMap64 objects |UInt64 value |The number of elements after the **intersection** operation of bitmap |
| | | | | | \
|11 |*bitmapOrCardinality* |\
| |*(bitmap1, bitmap2)* |\
| |-> *integer* |Two BitMap64 objects |UInt64 value |Number of elements after the **AND** operation of bitmap |
| | | | | | \
|12 |*bitmapXorCardinality* |\
| |*(bitmap1, bitmap2)* |\
| |-> *integer* |Two BitMap64 objects |UInt64 Value |Number of elements after the **XOR** operation on the bitmap |
| | | | | | \
|13 |*bitmapAndnotCardinality* |\
| |*(bitmap1, bitmap2)* |\
| |-> *integer* |Two BitMap64 objects |\
| | | |UInt64 Value |Number of elements after the **difference** operation on the bitmap |
| | | | | | \
|14 |*bitmapContains(bitmap, integer)* |\
| |-> bool |A BitMap64 object |\
| | |A number of type UIntN, |\
| | |N={8, 16, 32, 64} |UInt8 enumeration |\
| | | |1->true |\
| | | |0->false |Check if the bitmap contains the specified element |
| | | | | | \
|15 |*bitmapHasAll* |\
| |*(bitmap, sub_bitmap)* |\
| |-> bool |Two BitMap64 objects |UInt8 enumeration |\
| | | |1->true |\
| | | |0->false |Check if sub_bitmap is a subset of bitmap |\
| | | | |(returns 1 if equal as well) |
| | | | | | \
|16 |*bitmapHasAny* |\
| |*(bitmap1, bitmap2)* |\
| |-> bool |Two BitMap64 objects |UInt8 enumeration |\
| | | |1->true |\
| | | |0->false |Check if two bitmaps have any intersection |
| | | | | | \
|17 |*bitmapSubsetInRange* |\
| |(bitmap, range_start, range_end) |\
| |-> bitmap |A BitMap64 object, two UIntN numbers, indicating the range of values |\
| | |N={8, 16, 32, 64} |BitMap64 object |Check and return a bitmap consisting of values within the given **size range** in the bitmap. |\
| | | | |The function filters data, and the returned bitmap contains elements that are greater than or equal to range_start and less than range_end. |
| | | | | | \
|18 |*bitmapSubsetLimit* |\
| |(bitmap, range_start, cardinality_limit) |\
| |-> bitmap |A BitMap64 object, two UIntN numbers, indicate the start index range and the subset size |BitMap64 object |\
| | | | |Check and return a bitmap composed of elements starting from the specified **element** in the bitmap, not exceeding a specified number of elements. |\
| | | | |The function filters data and returns a bitmap where elements are greater than or equal to range_start and the total number of elements does not exceed cardinality_limit. |\
| | | | | |
| | | | | | \
|19 |\
| |subBitmap(bitmap, start_offset, length) |A BitMap64 object, |\
| | |Two UIntN type numbers, |\
| | |N={8, 16, 32, 64} |BitMap64 object |\
| | | | |Extracts data from the specified **index range** in the bitmap, analogous to subString. |\
| | | | |It is important to note that start_offset starts from 0, representing the first actual stored value, similar to an array index. Exceeding the number of bitmap elements with start_offset and length is meaningless. |

These functions are mainly compatible with functions related to the ClickHouse community. For details, refer to the [bitmap functions](https://clickhouse.tech/docs/en/sql-reference/functions/bitmap-functions/) doc.
See the "Function Examples" section for usage examples.
<span id="edbb4fb1"></span>
## Aggregate functions
<span id="632d9f0f"></span>
### Standard aggregate functions
> The function processes multiple records, performs aggregation, and returns a result row.


| | | | | | \
|Serial number |Function Interface |Parameter Description |Return value |Function Explanation |
|---|---|---|---|---|
| | | | | | \
|41 |\
| |bitmapColumnAnd |\
| |(bitmap_column) |\
| |-> bitmap |A column of data of the BitMap64 type |BitMap64 object |Receives a column of bimap, performing **intersection** operation on all bitmaps |
| | | | | | \
|42 |bitmapColumnOr |\
| |(bitmap_column) |\
| |-> bitmap |A column of data of type BitMap64 |BitMap64 object |Receives a bitmap column and performs an **AND** operation on all bitmaps |\
| | | | | |
| | | | | | \
|43 |bitmapColumnXor |\
| |(bitmap_column) |\
| |-> bitmap |A column of data of type BitMap64 |BitMap64 object |Receives a bitmap column and carries out an **XOR** operation on all bitmaps |\
| | | | | |
| | | | | | \
|44 |bitmapColumnCardinality |\
| |(bitmap_column) |\
| |-> UInt64 |A column of BitMap64 type data |UInt64 value |Receives a bitmap column, performs an **AND** operation on all bitmaps in the column, and returns the count of elements in the final result bitmap |
| | | | | | \
|45 |bitmapColumnHas |\
| |(bitmap_column, integer) |\
| |-> bool |A column of data of type BitMap64 |\
| | |A number of type UIntN, |\
| | |N={8, 16, 32, 64} |UInt8 enumeration |\
| | | |1->true |\
| | | |0->false |Receives a bitmap column, checks if it contains a specified element |\
| | | | | |
| | | | | | \
|46 |bitmapFromColumn(id) -> bitmap |Integer sequence |\
| | |UIntN type numbers, |\
| | |N={8, 16, 32, 64} |BitMap64 object |Receive a series of integers and aggregate them into a bitmap |

<span id="26af4345"></span>
### Advanced aggregate functions
Imagine a scenario: there are several bitmap objects, how can they be computed in a given way? For example, take the union of the first and second, and then intersect with the third. 。 。 You might think of using JOIN and the "normal functions" mentioned above for pairwise calculations. If there are 100 or even 1000 such bitmaps, there might be 100 or 1000 JOINS, making the SQL complexity, readability, and computational performance extremely poor. Is there a more intuitive and concise method to achieve this requirement? This is the advanced aggregate functions that will be introduced next.
ByteHouse provides a range of aggregate functions for batch processing of complex calculations between large numbers of bitmaps. By assigning each bitmap to be calculated a serial number and using these numbers to express set union, intersection, and difference operations, ByteHouse can perform the corresponding bitmap operations based on the specified operation expression, directly visualizing and simplifying the calculations, significantly enhancing the SQL writing experience!
Here is a simple illustration:
<div style="text-align: center"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84feb58f8c2f41309aaff9f78424931d~tplv-goo7wpa0wc-image.image" width="787px" /></div>

Advanced aggregate functions with expressions
> This type of function has two parentheses for passing parameters:
> The first parenthesis, called parameter, controls the behavior of the aggregate function (control flow)
> The second parenthesis, called argument, passes input data columns to the aggregate function (data flow)

:::tip
This high-order function is not complex, but textual explanation of the function is difficult. Refer to the figure above and the detailed "Function Example" section later in the text.
:::

| | | | | | \
|Index |Function interface |Parameter description |Return value |Functional Definitions |
|---|---|---|---|---|
| | | | | | \
|61 |bitmapCount |\
| |(expression) |\
| |(idx, bitmap) |\
| |-> integer |expression is a set operation with `&` representing intersection, `|` representing union, and `~` representing difference |\
| | |idx is the identifier for each bitmap row, using **positive integers of Int16/32 type** |\
| | | |UInt64 value |For each row in the bitmap column, take its identifier idx and store it in the map. The computation is carried out according to the method specified by expression, and the number of elements in the final bitmap is returned. |\
| | | | | |
| | | | | | \
|62 |bitmapExtract |\
| |(idx, bitmap) |\
| |-> bitmap |expression is an AND/OR/DIFF expression, `&` denotes intersection, `|` denotes union, `~` denotes difference |\
| | |idx represents markers corresponding to each bitmap row, using **positive integer Int16/32 type** |\
| | | |BitMap64 object |\
| | | | |For each row in the bitmap column, take its idx and compute using the method specified by expression, returning the final computed bitmap |\
| | | | | |
| | | | | | \
|63 |bitmapMultiCount |\
| |(expr1, expr2, ...) |\
| |(idx, bitmap) |\
| |-> [int1, int2, ...] |\
| | |expression denotes set operations with `&` for intersection, `|` for union, and `~` for difference |\
| | |idx represents the marker for each row of bitmap, using **positive integer of Int16/32 type** |\
| | | |UInt64 array |For each row in the bitmap column, fetch its identifier idx, and perform multiple bitmap operations as specified by each expr, returning the count of elements in the result bitmap for **each group of expr** |\
| | | | | |
| | | | | | \
|64 |bitmapMultiExtract |\
| |(expr1, expr2, ...) |\
| |(idx, bitmap) |\
| |-> [bitmap1, bitmap2, ...] |\
| | |expression is the expression for union, intersection, or difference where `&` represents intersection, `|` represents union, and `~` represents difference |\
| | |idx refers to the marker corresponding to each bitmap row, using **positive integer Int16/32 type** |BitMap64 array |For each row in the bitmap column, take its number idx, and perform multiple bitmap calculations based on the calculation method specified by each expr, returning **bitmap data for each group of expr** calculations |
| | | | | | \
|65 |bitmapMultiCountWithDate |\
| |(expr1, expr2, ...) |\
| |(date, idx, bitmap) |\
| |-> [int1, int2, ...] |Expression is a set operation with intersection (`&`), union (`|`), and difference (`~`) |\
| | |Date is in the Int64 date format |\
| | |Idx corresponds to labels for each row of bitmap, using **positive Int16/32 type integers** |UInt64 array |On top of bitmapMultiCount, a date dimension has been added to differentiate identifiers across different dates. While bitmapMultiCount supports only one identifier dimension, this function additionally includes a date dimension. |
| | | | | | \
|66 |bitmapMultiExtractWithDate |\
| |(expr1, expr2, ...) |\
| |(date, idx, bitmap) |\
| |-> [bitmap1, bitmap2, ...] |\
| |Note: Added in vanilla-1.5, not available in earlier versions |expression is an and/or/difference expression, `&` represents intersection, `|` represents union, `~` represents difference set |\
| | |date is in the Int64 date format |\
| | |idx refers to the marker for each row's bitmap, using **positive integers Int16/32 type** |BitMap64 array |\
| | | | |Added a date dimension to bitmapMultiExtract to distinguish labels across different dates. While bitmapMultiExtract supports only one identification dimension, this function additionally adds a date dimension. |

**Tips**:

* If there are multiple rows with the same index number, the aggregate function will automatically merge multiple bitmaps through the OR operation to participate in the calculation. During the final calculation, one index number corresponds to one bitmap.
* Searching the function name in this article will lead you to examples.

<span id="47606e22"></span>
## Function usage example
<span id="90c1a3b9"></span>
### Building test tables
Example table test.bitmap_test, schema see the section on 【Defining ByteHouse BitMap64 Type】.
<span id="05d9cd34"></span>
### Writing data
Data involves two tags, tag_id=11, with two values 'a' and 'b'; tag_id=12, with one value 'c'.
Each tag value has two rows, each having a different slice_id. slice_id is used to split large bitmaps, reducing the scale of each row's bitmap to optimize construction efficiency and memory usage, and also provide sharding credentials for distributed storage.
```SQL
insert into test.bitmap_test values ('2024-01-01', 0, 11, 'a', [1,2,3,4,5]), ('2024-01-02', 1, 11,'a', [11,12,13,14,15]);
insert into test.bitmap_test values ('2024-01-01', 0, 11, 'b', [3,4,5,6,7,8]), ('2024-01-02', 1, 11,'b', [13, 14,15,16]);
insert into test.bitmap_test values ('2024-01-01', 0, 12, 'c', [3,4,6,7,9]), ('2024-01-02', 1, 12,'c', [13,15,16,18]);
```

<span id="d3235675"></span>
### Ordinary functions
The use of ordinary functions, community demos, and other functions are no different. Here are just a few examples.
<span id="a5264b19"></span>
#### Array to Bitmap
```SQL
SELECT arrayToBitmap([1, 2, 3, 4, 5])
FORMAT TSV

-- Result:
{1,2,3,4,5}
```

<span id="eb661849"></span>
#### Bitmap to Array
```SQL
SELECT bitmapToArray(uids)
FROM test.bitmap_test
WHERE tag_value = 'a'
FORMAT TSV

-- Result:
[11,12,13,14,15]
[1,2,3,4,5]


SELECT bitmapToArray(arrayToBitmap([1, 2, 3, 4, 5]))
FORMAT TSV

-- Result:
[1,2,3,4,5]
```

<span id="f2dc3b81"></span>
#### Count Elements in Bitmap
```SQL
SELECT bitmapCardinality(arrayToBitmap([1, 2, 3, 4, 5]))
FORMAT TSV

-- Result:
5
```

<span id="fb320886"></span>
### Aggregation function
<span id="29643b96"></span>
#### Operations on multiple Bitmaps: Intersection/Union/XOR
```SQL
-- Find the intersection of two bitmaps.
SELECT bitmapColumnAnd(uids)
FROM test.bitmap_test
WHERE (slice_id = 0) AND (tag_value IN ('a', 'b'))
FORMAT TSV

-- Result:
{3,4,5}

-- Find the union of two bitmaps (the two functions have the same meaning).
SELECT
    bitmapCardinality(bitmapColumnOr(uids)),
    bitmapColumnCardinality(uids)
FROM test.bitmap_test
WHERE (slice_id = 0) AND (tag_value IN ('a', 'b'))
FORMAT TSV

-- Result:
8        8

-- Determine whether a given element exists in a certain bitmap.
SELECT bitmapColumnHas(uids, 12)
FROM test.bitmap_test
WHERE tag_value = 'a'
FORMAT TSV

-- Result:
1
```

<span id="f90fcf03"></span>
#### Aggregate a Bitmap
```Plain
SELECT bitmapFromColumn(number)
FROM
(
    SELECT number
    FROM system.numbers
    LIMIT 100, 10
)
FORMAT TSV

-- Result:
{100,101,102,103,104,105,106,107,108,109}
```

<span id="92adef9f"></span>
#### bitmapCount function
**Usage:** Perform complex set operations like intersection, union, and difference among multiple bitmaps. User inputs an expression to represent bitmap operations, which the function then interprets and calculates accordingly. Refer to the example in the section "Aggregation Function" - "Advanced Aggregation Functions".
**Input:** ID column, bitmap column. The ID column is used to identify bitmaps and can be a table field (e.g., tag_id) or a user-defined variable (e.g., idx).
**Expression:** One ID anchors one bitmap. The ID expression uses AND, OR, and DIFF operations corresponding to the intersection, union, and difference operations of bitmaps.
Supported ID operators:

* OR operation: represented by a comma ('1,2') or a vertical bar ('1|2')
* AND operation: represented by an ampersand ('1&2')
* Set difference operation: represented by a tilde ('1~2')

**Output:** The number of elements in the resulting bitmap after intersection, union, and difference operations.
Case 1: Calculate the total number of elements for label 'a':
```SQL
SELECT bitmapColumnCardinality(uids)
FROM test.bitmap_test
WHERE tag_value = 'a'
FORMAT TSV

-- Result:
10

-- Find the total number of elements with the label 'a'. It is equivalent to the calculation of bitmapColumnCardinality.
SELECT bitmapCount('1')(If(tag_value = 'a', toInt32(1), toInt32(999)) AS idx, uids) AS card
FROM test.bitmap_test
WHERE tag_value = 'a'
FORMAT TSV

-- Result:
10

-- Find the total number of elements with the label 'a'. Since the label is a string, a string expression can be directly used.
SELECT bitmapCount('a')(tag_value, uids)
FROM test.bitmap_test
WHERE tag_value = 'a'
FORMAT TSV

-- Result:
10
```

Case 2: Find the intersection of tags 'a' and 'b'
```SQL
SELECT bitmapCardinality(bitmapColumnAnd(uids)) AS card
FROM test.bitmap_test
WHERE (tag_value IN ('a', 'b')) AND (slice_id = 0)
FORMAT CSV

-- Result:
10

-- It is equivalent to the calculation of bitmapCardinality(bitmapColumnAnd).
SELECT bitmapCount('1&2')(multiIf(tag_value = 'a', toInt32(1), tag_value = 'b', 2, toInt32(999)) AS idx, uids) AS card
FROM test.bitmap_test
WHERE (tag_value IN ('a', 'b')) AND (slice_id = 0)
FORMAT TSV

-- Result:
3

-- Another way of writing the above SQL, which is suitable for complex SQL nesting.
SELECT bitmapCount('1&2')(idx, uids)
FROM
(
    SELECT
        toInt32(1) AS idx,
        uids
    FROM test.bitmap_test
    WHERE (slice_id = 0) AND (tag_value IN ('a'))
    UNION ALL
    SELECT
        toInt32(2) AS idx,
        uids
    FROM test.bitmap_test
    WHERE (slice_id = 0) AND (tag_value IN ('b'))
)
FORMAT TSV

-- Result:
3
```

Case 3: More tag set operations
```SQL
-- Option 1
SELECT bitmapCount('1&2|3')(multiIf(tag_value = 'a', toInt32(1), tag_value = 'b', toInt32(2), tag_value = 'c', toInt32(3), toInt32(999)) AS idx, uids) AS card
FROM test.bitmap_test
FORMAT TSV

-- Result:
11

-- Option 2: Since the tag_value is exactly of the string type, a string expression can be used.
SELECT bitmapCount('a&b|c')(tag_value, uids)
FROM test.bitmap_test
FORMAT TSV

-- Result:
11
```

<span id="70c14e05"></span>
#### bitmapExtract
This function calculates in the same way as bitmapCount, the difference is that it **returns the calculated bitmap**, not the count.
How to combine tags is the same as the bitmapCount function. bitmapCount uses tag_value as an example; here we have a case using tag_id as an example to show: Find the intersection of two tags:
```SQL
SELECT bitmapExtract('1&2')(multiIf(tag_id = 11, toInt32(1), tag_id = 12, 2, toInt32(999)) AS idx, uids) AS card
FROM test.bitmap_test
WHERE (tag_id IN (1,2)) AND (slice_id = 0)
FORMAT TSV

-- Result (no intersection):
{}

Another option: 
SELECT bitmapExtract('11&12')(tag_id, uids)
FROM test.bitmap_test
WHERE (tag_id IN (1, 2)) AND (slice_id = 0)
FORMAT TSV

-- Result (no intersection):
{}
```

<span id="9516f7e4"></span>
#### bitmapMultiCount function
This aggregate function builds on bitmapCount and **supports multiple sets of expressions**.
**Purpose:** Performs complex set operations among multiple bitmaps, while supporting multiple groups of operations and reuse of operations. Users express bitmap operations through input expressions, which the function then analyzes and computes accordingly. Refer to the "Aggregate Functions" - "Advanced Aggregate Functions" section in the diagrams above.
**Input:** ID column, bitmap column. The ID column is used to identify the bitmap, which can be a field in the table (such as tag_id) or a manually defined variable (such as idx).
**Expression:** One ID anchors one bitmap. ID expressions involve and/or/subtract operations, corresponding to the bitmap's intersection/union/difference calculations. Multiple expressions can be provided simultaneously; the function carries out corresponding calculations in sequence and returns all the results together.
Supported ID operators:

* Or operation: use commas ('1,2') or vertical lines ('1|2')
* And operation: use & ('1&2')
* Difference operation: use ~ ('1~2')
* Expression Reuse: Reuse the outcome of a particular expression by using an underline followed by a location number. For example, "_3" reuses the third expression (counting starts from one).

**Output:** The number of elements in the bitmap after the bitmap's union, intersection, and difference operations. Each expression corresponds to a result, stored in an array.
```SQL
-- '_3|3' is equivalent to '(1&2)|3'.
SELECT bitmapMultiCount('1', '2', '1&2', '_3|3')(multiIf(tag_value = 'a', toInt32(1), tag_value = 'b', toInt32(2), tag_value = 'c', toInt32(3), toInt32(999)) AS idx, uids) AS card
FROM test.bitmap_test
WHERE slice_id = 0
FORMAT TSV

-- Result:
[5,6,3,6]

-- Since the tag_value is exactly of the string type, a string expression can also be used.
SELECT bitmapMultiCount('a', 'b', 'a&b', '_3|c')(tag_value, uids) AS card
FROM test.bitmap_test
WHERE slice_id = 0
FORMAT TSV

-- Result:
[5,6,3,6]
```

`_3` indicates the reuse of the expression located at position 3, specifically '1&2'.
A set of relationships is available to verify correctness. This relationship is
A + B = AUB + A intersection B
```SQL
SELECT bitmapMultiCount('1', '2', '1&2', '1|2')(multiIf(tag_value = 'a', toInt32(1), tag_value = 'b', toInt32(2), tag_value = 'c', toInt32(3), toInt32(999)) AS idx, uids) AS card
FROM test.bitmap_test
WHERE slice_id = 0
FORMAT TSV

-- Result:
[5,6,3,8]

-- Since the tag_value is exactly of the string type, a string expression can also be used.
SELECT bitmapMultiCount('a', 'b', 'a&b', 'a|b')(tag_value, uids)
FROM test.bitmap_test
WHERE slice_id = 0
FORMAT TSV

-- Result:
[5,6,3,8]
```

<span id="dc741da2"></span>
#### bitmapMultiExtract
User purpose for bitmapMultiCount is the same, but the return value differs; it returns bitmap data.
```SQL
SELECT bitmapMultiExtract('1', '2', '1&2', '1|2')(multiIf(tag_value = 'a', toInt32(1), tag_value = 'b', toInt32(2), tag_value = 'c', toInt32(3), toInt32(999)) AS idx, uids) AS card
FROM test.bitmap_test
WHERE slice_id = 0
FORMAT TSV

[{1,2,3,4,5},{3,4,5,6,7,8},{3,4,5},{1,2,3,4,5,6,7,8}]

-- tSince the tag_value is exactly of the string type, a string expression can also be used.
SELECT bitmapMultiExtract('a', 'b', 'a&b', 'a|b')(tag_value, uids)
FROM test.bitmap_test
WHERE slice_id = 0
FORMAT TSV

-- Result:
[{1,2,3,4,5},{3,4,5,6,7,8},{3,4,5},{1,2,3,4,5,6,7,8}]
```

<span id="66344c67"></span>
#### bitmapMultiCountWithDate
**Purpose:** This function builds on bitmapMultiCount by incorporating a date dimension, allowing for differentiation between tags on different dates in expressions.
Note that the date column must be of Int64 type; dates are usually in Date type and need to use the toYYYYMMDD function to convert.
**Input:** Date column, ID column, bitmap column.
**Expression:** A date and an ID together form a bitmap anchor and cannot be used separately. Therefore, `date_ID` is used as a whole, as in the example '20240101_1' to identify a bitmap. The function bitmapMultiCount mentioned earlier only requires '1', this is the difference between them.
**Output:** The number of elements in the result bitmap after bitmap set operations. Each expression corresponds to a result stored in an array.
```SQL
SELECT bitmapMultiCountWithDate('20240101_1', '20240102_2', '20240101_1|20240102_2')(CAST(toYYYYMMDD(p_date), 'Int64') AS date1, multiIf((tag_value = 'a') AND (p_date = '2024-01-01'), toInt64(1), (tag_value = 'b') AND (p_date = '2024-01-02'), toInt64(2), (tag_value = 'c') and (p_date = '2024-01-01'), toInt64(3),toInt32(999)) AS idx, uids) AS card
FROM test.bitmap_test
FORMAT TSV

-- Result:
[5,4,9]

-- Since the tag_value is exactly of the string type, a string expression can also be used.
SELECT bitmapMultiCountWithDate('20240101_a', '20240102_b', '20240101_a|20240102_b')(CAST(toYYYYMMDD(p_date), 'Int64') AS date1, tag_value, uids) AS card
FROM test.bitmap_test
FORMAT TSV

-- Result:
[5,4,9]
```

<span id="e3d566e9"></span>
#### bitmapMultiExtractWithDate
Function and usage are the same as bitmapMultiCountWithDate, the difference is in the return value, it returns bitmap data.
```SQL
SELECT bitmapMultiExtractWithDate('20240101_1', '20240102_2', '20240101_1|20240102_2')(CAST(toYYYYMMDD(p_date), 'Int64') AS date1, multiIf((tag_value = 'a') AND (p_date = '2024-01-01'), toInt64(1), (tag_value = 'b') AND (p_date = '2024-01-02'), toInt64(2), (tag_value = 'c') and (p_date = '2024-01-01'), toInt64(3),toInt32(999)) AS idx, uids) AS card
FROM test.bitmap_test
FORMAT TSV

-- Result:
[{1,2,3,4,5},{13,14,15,16},{1,2,3,4,5,13,14,15,16}]


-- Since the tag_value is exactly of the string type, a string expression can also be used.
SELECT bitmapMultiExtractWithDate('20240101_a', '20240102_b', '20240101_a|20240102_b')(CAST(toYYYYMMDD(p_date), 'Int64') AS date1, tag_value, uids) AS card
FROM test.bitmap_test
FORMAT TSV

-- Result:
[{1,2,3,4,5},{13,14,15,16},{1,2,3,4,5,13,14,15,16}]
```
