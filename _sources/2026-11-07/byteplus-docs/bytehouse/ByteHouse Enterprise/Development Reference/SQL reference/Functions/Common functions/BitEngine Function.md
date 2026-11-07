---
title: "BitEngine Function"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/bitengine-function"
---

<span id="普通函数"></span>
## Ordinary Function
The function takes either a line of record or a `BitMap64` object and returns a line of result.

| | | | | | \
|Serial Number |Function Interface |Parameter Description |Return Value |Function Description |
|---|---|---|---|---|
| | | | | | \
|1 |arrayToBitmap([x1, …]) |\
| |-> bitmap |Array of UIntN type |\
| | |N={8, 16, 32, 64} |BitMap64 object |Create a bitmap object through an array |
| | | | | | \
|2 |*bitmapToArray(bitmap)* |\
| |-> [x1,...] |A BitMap64 object |UInt64 array |Convert a bitmap object into array format |
| | | | | | \
|3 |*bitmapAnd(bitmap1, bitmap2)* |\
| |-> bitmap |two BitMap64 objects |BitMap64 object |bitmap's **intersection** operation |
| | | | | | \
|4 |*bitmapOr(bitmap1, bitmap2)* |\
| |-> bitmap |two BitMap64 objects |BitMap64 object |bitmap's **AND** operation |
| | | | | | \
|5 |*bitmapXor(bitmap1, bitmap2)* |\
| |-> bitmap |Two BitMap64 objects |BitMap64 object |bitmap's **XOR** operation |
| | | | | | \
|6 |*bitmapAndnot(bitmap1, bitmap2)* |\
| |-> bitmap |Two BitMap64 objects |BitMap64 object |Bitmap **difference** operation |
| | | | | | \
|7 |*bitmapCardinality(bitmap)* |\
| |-> *integer* |A BitMap64 object |UInt64 value |The number of elements in the bitmap |
| | | | | | \
|8 |*bitmapMin(bitmap)* |\
| |-> *integer* |A BitMap64 object |UInt64 value |The smallest element in the bitmap |
| | | | | | \
|9 |*bitmapMax(bitmap)* |\
| |-> *integer* |A BitMap64 object |UInt64 value |The largest element in bitmap |
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
| |-> *integer* |Two BitMap64 objects |UInt64 Value |Number of elements after **XOR** operation on bitmap |
| | | | | | \
|13 |*bitmapAndnotCardinality* |\
| |*(bitmap1, bitmap2)* |\
| |-> *integer* |Two BitMap64 objects |UInt64 Value |Number of elements after **difference** operation on bitmap |
| | | | | | \
|14 |*bitmapContains(bitmap, integer)* |\
| |-> bool |A BitMap64 object |\
| | |Number of type UIntN, |\
| | |N={8, 16, 32, 64} |UInt8 enumeration |\
| | | |1->true |\
| | | |0->false |Check if the bitmap contains the specified element |
| | | | | | \
|15 |*bitmapHasAll* |\
| |*(bitmap, sub_bitmap)* |\
| |-> bool |Two BitMap64 objects |UInt8 enumeration |\
| | | |1->true |\
| | | |0->false |Check if sub_bitmap is a subset of bitmap |\
| | | | |(also returns 1 if equal) |
| | | | | | \
|16 |*bitmapHasAny* |\
| |*(bitmap1, bitmap2)* |\
| |-> bool |Two BitMap64 objects |UInt8 enumeration |\
| | | |1->true |\
| | | |0->false |Check if two bitmaps have any intersection |
| | | | | | \
|17 |*bitmapSubsetInRange* |\
| |(bitmap, range_start, range_end) |\
| |-> bitmap |A BitMap64 object and two UIntN numbers, specifying the range of values |\
| | |N={8, 16, 32, 64} |BitMap64 object |Checks and returns a bitmap consisting of values within a specified range in the bitmap. |
| | | | | | \
|18 |*bitmapSubsetLimit* |\
| |(bitmap, index_start, cardinality_limit) |\
| |-> bitmap |A BitMap64 object, two UIntN numbers, representing the index start range and the subset size |BitMap64 object |Checks and returns a bitmap comprised of a specified number of elements starting from a specified position in the bitmap |

These functions are mainly compatible with the ClickHouse community's functions. For details, refer to [bitmap functions](https://clickhouse.tech/docs/en/sql-reference/functions/bitmap-functions/).
<span id="聚合函数"></span>
## Aggregate Function
The function takes multiple records, performs an aggregation operation, and returns a line of result.

| | | | | | \
|Serial number |Function interface |Parameter description |Return value |Function explanation |
|---|---|---|---|---|
| | | | | | \
|1 |bitmapColumnAnd |\
| |(bitmap_column) |\
| |-> bitmap |A column of BitMap64 type data |BitMap64 object |Receives a column of bitmap, performing **intersection** operations on all bitmaps |
| | | | | | \
|2 |bitmapColumnOr |\
| |(bitmap_column) |\
| |-> bitmap |A column of BitMap64 type data |BitMap64 Object |Receives a bitmap column, all bitmaps in the column undergo **AND** operation |
| | | | | | \
|3 |bitmapColumnXor |\
| |(bitmap_column) |\
| |-> bitmap |A column of data of BitMap64 type |BitMap64 Object |Receives a bitmap column, all bitmaps in the column undergo **XOR** operation |
| | | | | | \
|4 |bitmapColumnCardinality |\
| |(bitmap_column) |\
| |-> UInt64 |A column of BitMap64 type data |UInt64 value |Receives a bitmap column, performs an **AND** operation on all bitmaps in the column, and returns the count of elements in the resulting bitmap |
| | | | | | \
|5 |bitmapColumnHas |\
| |(bitmap_column, integer) |\
| |-> bool |A column of BitMap64 data |\
| | |A number of type UIntN, |\
| | |N={8, 16, 32, 64} |UInt8 enumeration |\
| | | |1->true |\
| | | |0->false |Receive a bitmap column and check if it contains a specified element |

<span id="1bc77418"></span>
## Advanced Aggregate Function with Expression
This type of function uses two parentheses to pass parameters:

* The first parenthesis is called parameter, which controls the behavior of the aggregate function (control flow).
* The second parenthesis is called 'argument' and is used for passing input data columns (data streams) to the aggregation function.

The operators in the expression represent union, intersection, and difference.
Intersection: 1&2
Union: 1|2, another form 1,2
Difference set: 1~2

| | | | | | \
|Index |Function interface |Parameter description |Return Value |Function Definition |
|---|---|---|---|---|
| | | | | | \
|1 |bitmapCount |\
| |(expression [, is_bitmap_execute] ) |\
| |(tag_idx, bitmap_column) |\
| |-> integer |expression is an AND/OR/NOT expression, is_bitmap_execute is for the BITMAP_EXECUTE model, default is 0 |\
| | |tag_idx represents the tag for each bitmap row, currently an Int, and a positive number |UInt64 value |For each row in the bitmap_column, retrieve its tag and perform bitmap operations according to the method specified in the expression, returning the number of elements in the final bitmap. |\
| | | | |SELECT BitmapCount('1&2')(tag_idx, bitmap) FROM ( SELECT multiIf(tag = 'a', toInt32(1), tag = 'b', toInt32(2), toInt32(-1000)) AS tag_idx, bitmap FROM test.test_table WHERE 1 ) |
| | | | | | \
|2 |bitmapMultiCount |\
| |(expr1, expr2, ...) |\
| |(tag_idx, bitmap_column) |\
| |-> [int1, int2, ...] |The expression is a logical AND/OR/NOT expression. |\
| | |tag_idx is the marker corresponding to each row's bitmap, currently an integer and positive. |Array of UInt64 |For each row in the bitmap_column, retrieve its tag and perform multiple bitmap operations according to the calculations specified by each expr, returning the count of elements in the result bitmap for each group of expr calculations. |\
| | | | |SELECT bitmapMultiCount('1&2', '(1&2) |\
| | | | |**'_1 |
| | | | | | \
|3 |bitmapMultiCountWithDate |\
| |(expr1, expr2, ...) |\
| |(date, tag_idx, bitmap_column) |\
| |-> [int1, int2, ...] |The expression involves AND, OR, NOT operators. |\
| | |tag_idx corresponds to the tag of each row in the bitmap and is currently a positive integer. |\
| | |The date is an integer representing the date in yyyyMMdd format. |UInt64 data |Based on bitmapMultiCount, different dates can be distinguished. |\
| | | | |select bitmapMultiCountWithDate('20220101_1')(date, tag_idx, bitmap) from (select cast(toYYYYMMDD(p_date) as Int64) as date1, If(tag='a', toInt64(1),toInt64(0)) as tag_idx, bitmap from test.test_table |\
| | | | |Tips: Pay attention that date1 and the field p_date in the table are different, otherwise it will cause an exception due to aliasing. |
| | | | | | \
|4 |bitmapExtract |\
| |(expression [, is_bitmap_execute] ) |\
| |(tag_idx, bitmap_column) |\
| |-> bitmap |"expression" is a logical expression involving AND, OR, NOT |\
| | |tag_idx refers to the label for each line in the bitmap, currently an integer and must be positive |BitMap64 object |For each row in bitmap_column, retrieve its tag and perform bitmap operations as specified by expression, returning the final computed bitmap |\
| | | | |SELECT BitmapExtract('1&2')(tag_idx, bitmap) FROM ( SELECT multiIf(tag = 'a', toInt32(1), tag = 'b', toInt32(2), toInt32(-1000)) AS tag_idx, bitmap FROM test.test_table WHERE 1 ) |

tag_idx is usually specified by users, and it is better to use **non-negative integers**, such as `toInt32(1) as tag_idx`. For negative numbers, please use smaller negative numbers (like -100) to prevent unnecessary interference in the calculation results (related to internal implementation). If there are multiple lines of data with the same tag_idx, the aggregation function will automatically merge the multiple line bitmaps through an OR operation into one and involve it in the calculation. At the time of the final calculation, one tag_idx corresponds to one bitmap.
<span id="1f41b1df"></span>
## Other functions and operational interfaces
<span id="05acc3be"></span>
### BitEngine Status Query
```Plain
select * from system.bitengine where xxxxx
```
