---
title: "BitMap function"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/bitmap-function"
---

<span id="6c77bc0d"></span>
# Background information

The ClickHouse community provides bitmap data processing capabilities, for details, see [Bitmap Functions | ClickHouse Docs](https://clickhouse.com/docs/en/sql-reference/functions/bitmap-functions). Around the same time, ByteHouse also developed its own set of bitmap data types and related functions. Differences and similarities exist in data storage and usage between the two. For more information on the comparison of BitMap type data, refer to [BitMap64](https://docs.byteplus.com/docs/bytehouse/complex-data-types#cb459f3c).

ByteHouse provides you with a rich set of function interfaces for querying BitMap64 data types, which can be broadly categorized into normal functions, aggregate functions, and higher\-order aggregate functions. Here is the interface list and usage instructions for ByteHouse's BitMap functions.

<span id="7ca4fa46"></span>
# Normal functions

ByteHouse's BitMap normal functions accept either a record or a `BitMap64` object and return a result row.

This part of the function interface, except for the first function `arrayToBitmap`, is consistent with community function interfaces.


|**Order No.**  |**Function interface** |**Parameter description** |**Return value** |**Function description** |
|---|---|---|---|---|
|1 |arrayToBitmap([x1, …])<br><br>\-\> bitmap |Array of UIntN type<br><br>N= |BitMap64 object |Construct a bitmap object using an array |
|2 |*bitmapToArray(bitmap)* <br><br>\-\> [x1,...] |A BitMap64 object |UInt64 array |Convert a bimap object into an array format |
|3 |*bitmapAnd(bitmap1, bitmap2)* <br><br>\-\> bitmap |Two BitMap64 objects |BitMap64 object |BitMap's **intersection** operation |
|4 |*bitmapOr(bitmap1, bitmap2)* <br><br>\-\> bitmap |Two BitMap64 objects |BitMap64 object |BitMap's **union** operation |
|5 |*bitmapXor(bitmap1, bitmap2)* <br><br>\-\> bitmap |Two BitMap64 objects |BitMap64 object |bitmap **XOR** operation |
|6 |*bitmapAndnot(bitmap1, bitmap2)* <br><br>\-\> bitmap |Two BitMap64 objects |BitMap64 object |bitmap's **Poor** operation |
|7 |*bitmapCardinality(bitmap)* <br><br>\-\> *integer* |A BitMap64 object |UInt64 numerical value |Number of elements in bitmap |
|8 |*bitmapMin(bitmap)* <br><br>\-\> *integer* |One BitMap64 object |UInt64 numerical value |The smallest element in the bitmap |
|9 |*bitmapMax(bitmap)* <br><br>\-\> *integer* |One BitMap64 object |UInt64 numerical value |The largest element in the bitmap |
|10 |*bitmapAndCardinality*<br><br> *(bitmap1, bitmap2)* <br><br>\-\> *integer* |Two BitMap64 objects |UInt64 numerical value |The number of elements after the bitwise **AND** operation on the bitmap |
|11 |*bitmapOrCardinality*<br><br> *(bitmap1, bitmap2)* <br><br>\-\> *integer* |Two BitMap64 objects |UInt64 numerical value |The number of elements after the **AND** operation on the bitmap |
|12 |*bitmapXorCardinality*<br><br> *(bitmap1, bitmap2)* <br><br>\-\> *integer* |Two BitMap64 objects |UInt64 numerical value |The number of elements after the **XOR** operation on the bitmap |
|13 |*bitmapAndnotCardinality*<br><br> *(bitmap1, bitmap2)* <br><br>\-\> *integer* |Two BitMap64 objects |UInt64 numerical value |The number of elements after the subtraction operation of bitmap |
|14 |*bitmapContains(bitmap, integer)* <br><br>\-\> bool |A BitMap64 object<br><br>A UIntN type number,<br><br>N= |UInt8 enumeration<br><br>1\-\>true<br><br>0\-\>false |Check if the bitmap contains the specified element |
|15 |*bitmapHasAll*<br><br> *(bitmap, sub_bitmap)* <br><br>\-\> bool |Two BitMap64 objects |UInt8 enumeration<br><br>1\-\>true<br><br>0\-\>false |Check if sub_bitmap is a subset of bitmap<br><br>(equals returns 1 as well) |
|16 |*bitmapHasAny*<br><br> *(bitmap1, bitmap2)* <br><br>\-\> bool |Two BitMap64 objects |UInt8 enum<br><br>1\-\>true<br><br>0\-\>false |Check if two bitmaps have an intersection |
|17 |*bitmapSubsetInRange*<br><br>(bitmap, range_start, range_end)<br><br>\-\> bitmap |A BitMap64 object, two UIntN numbers, identifying the value range<br><br>N= |BitMap64 object |Check and return a bitmap composed of values that meet the given **element size range**.<br><br>The function filters data, the returned bitmap contains elements that are bigger than or equals to range_start and smaller than range_end. |
|18 |*bitmapSubsetLimit*<br><br>(bitmap, range_start, cardinality_limit)<br><br>\-\> bitmap |A BitMap64 object, two UIntN numbers, identifying the index start range, and the subset size |BitMap64 object |Check and return a bitmap consisting of elements starting **from specified element** within bitmap, not exceeding the specified number of elements.<br><br>The function filters data and returns a bitmap where elements are bigger than or equals to range_start, and the total number of elements does not exceed the cardinality_limit. |
|19 |subBitmap(bitmap, start_offset, length) |A BitMap64 object,<br><br>Two UIntN type numbers,<br><br>N= |BitMap64 object |Extract data within specified **index range** from bitmap, analogous to subString.<br><br>It should be noted that the start_offset begins from 0, which represents the first valid value stored, similar to an array index. The start_offset and length exceeding the number of bitmap elements are meaningless. |


<span id="1b6129c1"></span>
### bitmapAnd

The result of adding two bitmaps together is a new bitmap.

**Syntax**

```SQL
bitmapAnd(bitmap,bitmap)
```


**Param**


* `bitmap` – Bitmap object.


**Return Value**


* Bitmap object


**Example**

```SQL
SELECT bitmapToArray(bitmapAnd(bitmapBuild([1,2,3]),bitmapBuild([3,4,5]))) AS res;
```


As a result

```Plain
┌─res─┐
│ [3] │
└─────┘
```


<span id="92e72842"></span>
### bitmapAndCardinality

Calculate the sum of two bitmaps, returning a UInt64 type cardinality.

**Syntax**

```SQL
bitmapAndCardinality(bitmap,bitmap)
```


**Param**


* `bitmap` represents a bitmap object.


**Return value**


* Type `UInt64` in the cardinality.


Type: `Uint64`

**Example**

```SQL
SELECT bitmapAndCardinality(bitmapBuild([1,2,3]),bitmapBuild([3,4,5])) AS res;
```


As a result:

```Plain
┌─res─┐
│ 1   │
└─────┘
```


<span id="c51e871b"></span>
### bitmapAndnot

The sum of the two bitmaps is not calculated, resulting in a new bitmap.

**Syntax**

```SQL
bitmapAndnot(bitmap,bitmap)
```


**Param**


* `bitmap` – Bitmap object.


**Return value**


* Bitmap object


Type: `Bitmap object`.

**Example**

```SQL
SELECT bitmapToArray(bitmapAndnot(bitmapBuild([1,2,3]),bitmapBuild([3,4,5]))) AS res;
```


Result:

```Plain
┌─res────┐
│ [1, 2] │
└────────┘
```


<span id="bedb7966"></span>
### bitmapAndnotCardinality

Calculates the AND\-NOT for two bitmaps, returning a UInt64 type cardinality.

**Syntax**

```SQL
bitmapAndnotCardinality(bitmap,bitmap)
```


**Param**


* `bitmap` – Bitmap object.


**Return value**


* Cardinality in `UInt64`.


Type: `UInt64`

**Example**

```SQL
SELECT bitmapAndnotCardinality(bitmapBuild([1,2,3]),bitmapBuild([3,4,5])) AS res;
```


As a result:

```Plain
┌─res─┐
│ 2   │
└─────┘
```


<span id="dab051ee"></span>
### bitmapBuild

Build a bitmap from an unsigned integer array.

**Syntax**

```SQL
bitmapBuild(array)
```


**Param**


* `array` \- Unsigned integer array.


**Return value**


* Bitmap object


Type: `Bitmap object`.

**Example**

```SQL
SELECT toTypeName(bitmapBuild([1, 2, 3, 4, 5]));
```


As a result:

```Plain
┌─toTypeName(bitmapBuild([1, 2, 3, 4, 5]))─┐
│ AggregateFunction(groupBitmap, UInt8)    │
└──────────────────────────────────────────┘
```


<span id="6fdb6089"></span>
### bitmapCardinality

Returns a bitmap cardinality of type UInt64.

**Syntax**

```SQL
bitmapCardinality(bitmap)
```


**Param**


* `bitmap` – Bitmap object.


**Return value**


* The bitmap cardinality of type `UInt64`.


Type: `UInt64`.

**Example**

```SQL
SELECT bitmapCardinality(bitmapBuild([1, 2, 3, 4, 5])) AS res;
```


As a result:

```Plain
┌─res─┐
│ 5   │
└─────┘
```


<span id="870c838b"></span>
### bitmapContains

Check if the bitmap contains an element.

**Syntax**

```SQL
bitmapContains(haystack, needle)
```


**Param**


* `haystack`— [bitmap object], in which the function searches.

* `needle`— Value the function searches for. Type: [UInt32].


**Return value**


* 0 — If `haystack` does not contain `needle`.

* 1 — If `haystack` contains `needle`.


Type: `UInt8`.

**Example**

```SQL
SELECT bitmapContains(bitmapBuild([1,5,7,9]), toUInt32(9)) AS res;
```


Result:

```Plain
┌─res─┐
│ 1   │
└─────┘
```


<span id="349f1fae"></span>
### bitmapHasAll

`hasAll(array, array)` returns 1 if the first bitmap contains all elements of the second bitmap, Otherwise, it returns 0.

If the second parameter is an empty bitmap, it returns 1.

**Syntax**

```SQL
bitmapHasAll(bitmap,bitmap)
```


**Parameter**


* `bitmap` – Bitmap object.


**Return value**


* `1`, returns 1 if the first bitmap contains all elements of the second bitmap or if the second parameter is an empty bitmap.

* `0`, Otherwise.


Type: `UInt8`

**Example**

```SQL
SELECT bitmapHasAll(bitmapBuild([1,2,3]),bitmapBuild([3,4,5])) AS res;
```


As a result:

```Plain
┌─res─┐
│ 0   │
└─────┘
```


<span id="f1ef2767"></span>
### bitmapHasAny

Check if two bitmaps have any intersecting elements.

**Syntax**

```SQL
bitmapHasAny(bitmap1, bitmap2)
```


If you are sure `bitmap2` contains only one element, consider using the [bitmapContains] function. It works more efficiently.

**Parameter**


* `bitmap*` \- Bitmap object.


**Return value**


* `1`, if `bitmap1` and `bitmap2` have at least one similar element.

* `0`, otherwise.


**Example**

```SQL
SELECT bitmapHasAny(bitmapBuild([1,2,3]),bitmapBuild([3,4,5])) AS res;
```


As a result:

```Plain
┌─res─┐
│ 1   │
└─────┘
```


<span id="8b50055c"></span>
### bitmapMax

Returns the maximum UInt64 value in the set if the set is not empty, otherwise returns 0.

**Syntax**

```SQL
bitmapMax(bitmap)
```


**Param**


* `bitmap` \- Bitmap object.


**Return value**


* Returns the maximum UInt64 value in the set.


Type: `UInt64`

**Example**

```SQL
SELECT bitmapMax(bitmapBuild([1, 2, 3, 4, 5])) AS res;
```


As a result:

```Plain
┌─res─┐
│ 5   │
└─────┘
```


<span id="77419581"></span>
### bitmapMin

Returns the smallest UInt64 value in the collection, or UINT32_MAX if the collection is empty.

**Syntax**

```SQL
bitmapMin(bitmap)
```


**Parameters**


* `bitmap` – Bitmap object.


**Return value**


* Returns the smallest UInt64 value in the collection.


Type: `UInt64`

**Example**

```SQL
SELECT bitmapMin(bitmapBuild([1, 2, 3, 4, 5])) AS res;
```


As a result:

```Plain
┌─res─┐
│ 1   │
└─────┘
```


<span id="6c61744d"></span>
### bitmapOr

Carry out an OR calculation on two bitmaps, and the result is a new bitmap.

```SQL
bitmapOr(bitmap,bitmap)
```


**Param**


* `bitmap` – Bitmap object.


**Return value**


* Bitmap object


Type: `Bitmap object`.

**Example**

```SQL
SELECT bitmapToArray(bitmapOr(bitmapBuild([1,2,3]),bitmapBuild([3,4,5]))) AS res;
```


Result:

```Plain
┌─res─────────────┐
│ [1, 2, 3, 4, 5] │
└─────────────────┘
```


<span id="fcb8219d"></span>
### bitmapOrCardinality

Two bitmaps or calculations, returns a UInt64 type cardinality.

**Syntax**

```SQL
bitmapOrCardinality(bitmap,bitmap)
```


**Parameters**


* `bitmap` \- Bitmap object.


**Return value**


* Return or calculate the result in cardinal form.


Type: `UInt64`

**Example**

```SQL
SELECT bitmapOrCardinality(bitmapBuild([1,2,3]),bitmapBuild([3,4,5])) AS res;
```


Result:

```Plain
┌─res─┐
│ 5   │
└─────┘
```


<span id="c3870367"></span>
### bitmapSubsetInRange

Returns the subset within the specified range (excluding range_end).

**Syntax**

```SQL
bitmapSubsetInRange(bitmap, range_start, range_end)
```


**Parameters**


* `bitmap` – [Bitmap object].

* `range_start` – Starting point of the range. Type: [UInt32].

* `range_end` – Endpoint of the range (exclusive). Type: [UInt32].


**Return Value**


* Returns or calculates the result.


Type: `array`

**Example**

```SQL
SELECT bitmapToArray(bitmapSubsetInRange(bitmapBuild([0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,100,200,500]), toUInt32(30), toUInt32(200))) AS res;
```


As a result:

```Plain
┌─res───────────────────┐
│ [30, 31, 32, 33, 100] │
└───────────────────────┘
```


<span id="389778fb"></span>
### bitmapSubsetLimit

Create a subset of the bitmap that contains `range_start` and n elements `between` cardinality_limit.

**Syntax**

```SQL
bitmapSubsetLimit(bitmap, range_start, cardinality_limit)
```


**Parameters**


* `bitmap` – [Bitmap object].

* `range_start` – The starting point of the subset. Type: [UInt32].

* `cardinality_limit` \- Subset cardinality cap. Type: [UInt32].


**Return value**


* Subset.


Type: `Bitmap object`.

**Example**

```SQL
SELECT bitmapToArray(bitmapSubsetLimit(bitmapBuild([0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,100,200,500]), toUInt32(30), toUInt32(200))) AS res;
```


As a result:

```Plain
┌─res─────────────────────────────┐
│ [30, 31, 32, 33, 100, 200, 500] │
└─────────────────────────────────┘
```


<span id="0476ab5c"></span>
### bitmapToArray

Convert bitmap into an Integer set.

**Syntax**

```SQL
bitmapToArray(bitmap)
```


**Parameter**


* `bitmap` \- bitmap object.


**Return value**


* Array.


Type: `array`.

**Example**

```SQL
SELECT bitmapToArray(bitmapBuild([1, 2, 3, 4, 5])) AS res;
```


As a result:

```Plain
┌─res─────────────┐
│ [1, 2, 3, 4, 5] │
└─────────────────┘
```


<span id="8faaf698"></span>
### bitmapXor

Two bitmaps are xor'ed, resulting in a new bitmap.

```SQL
bitmapXor(bitmap,bitmap)
```


**Parameter**


* `Bitmap` \- Bitmap object.


**Return value**


* Bitmap object


Type: `Bitmap object`.

**Example**

```SQL
SELECT bitmapToArray(bitmapXor(bitmapBuild([1,2,3]),bitmapBuild([3,4,5]))) AS res;
```


Result:

```Plain
┌─res──────────┐
│ [1, 2, 4, 5] │
└──────────────┘
```


<span id="fc7fff5e"></span>
### bitmapXorCardinality

Calculate the XOR between two bitmaps, returning the cardinality as a UInt64.

**Syntax**

```SQL
bitmapXorCardinality(bitmap,bitmap)
```


**Parameter**


* `bitmap` – Bitmap object.

* 


**Return value**


* Bitmap object


Type: `Bitmap object`.

**Example**

```SQL
SELECT bitmapXorCardinality(bitmapBuild([1,2,3]),bitmapBuild([3,4,5])) AS res;
```


Result:

```Plain
┌─res─┐
│ 4   │
└─────┘
```


<span id="2077e224"></span>
### subBitmap

Extracts a subset data within a specified **index range** from the offset position in the bitmap. The maximum cardinality of the returned bitmap is `cardinality_limit`.

**Syntax**

```SQL
subBitmap(bitmap, offset, cardinality_limit)
```


**Parameter**


* `bitmap` \- [Bitmap Object]

* `Offset` \- Position of the first element in the subset, UInt32 type

* `Cardinality Limit` \- Maximum cardinality of the subset, UInt32 type


Note that the offset starts from 0, representing the first valid value actually stored, similar to an array index. If the offset and cardinality limit exceed the number of elements in the bitmap, they become meaningless.

**Return Value**


* Subset


**Example**

```SQL
SELECT bitmapToArray(subBitmap(bitmapBuild([0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,100,200,500]), toUInt32(10), toUInt32(10))) AS res;

--- It is equivalent to the following writing of ByteHouse BitMap64 type. 
SELECT bitmapToArray(subBitmap(arrayToBitmap([0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 100, 200, 500]), toUInt32(10), toUInt32(10))) AS res
```


```SQL
┌─res─────────────────────────────┐
│ [10,11,12,13,14,15,16,17,18,19] │
└─────────────────────────────────┘
```


<span id="86d3034e"></span>
# Aggregate function

The following aggregate functions take multiple records, perform aggregation, and return a single result.


|Order No. |Function interface |Parameter description |Return value |Function description |
|---|---|---|---|---|
|1 |bitmapColumnAnd<br><br>(bitmap_column)<br><br>\-\> bitmap |Column of data of type BitMap64 |BitMap64 object |Delivered a column of bimap, all bitmaps in which are **intersected** |
|2 |bitmapColumnOr<br><br>(bitmap_column)<br><br>\-\> bitmap |Column of data of type BitMap64 |BitMap64 object |Receive a bimap column, perform **AND** operation on all bitmaps in the column |
|3 |bitmapColumnXor<br><br>(bitmap_column)<br><br>\-\> bitmap |A column of BitMap64 type data |BitMap64 object |Receive a bimap column, perform **XOR** operation on all bitmaps in the column |
|4 |bitmapColumnCardinality<br><br>(bitmap_column)<br><br>\-\> UInt64 |A column of BitMap64 type data |UInt64 value |Receives a bitmap column, performs an **and** operation on all bitmaps in the column, and returns the count of elements in the resulting bitmap |
|5 |bitmapColumnHas<br><br>(bitmap_column, integer)<br><br>\-\> bool |A column of BitMap64 type data<br><br>Numbers of type UIntN,<br><br>N= |UInt8 enumeration<br><br>1\-\>true<br><br>0\-\>false |Receives a bitmap column and checks if it contains a specified element |
|6 |bitmapFromColumn(id) \-\> bitmap |Integer column<br><br>Numbers of type UIntN,<br><br>N= |BitMap64 object |Receive a column of integers and aggregate them into a bitmap |


Here are specific examples of functions:

<span id="6047ba34"></span>
### bitmapColumAnd

Calculates the intersection of a bitmap column.

**Syntax**

```SQL
bitmapColumnAnd(bitmap_column)
```


**Parameters**

`bitmap_column` \- A data column of type BitMap64.

**Return Value**


* A BitMap64 object


**Example**

```SQL
select bitmapColumnAnd(rbm) as result
from (
    select arrayToBitmap([1,2,3]) as rbm
    union all
    select arrayToBitmap([2,3,4]) as rbm
)
```


Result:

```SQL
┌─result─┐
│ {2,3}  │
└────────┘
```


<span id="d3e4f135"></span>
### bitmapColumnOr

Calculates the union of a bitmap column.

**Syntax**

```SQL
bitmapColumnOr(bitmap_column)
```


**Parameters**

`bitmap_column` \- A data column of type BitMap64.

**Return Value**


* A BitMap64 object


**Example**

```SQL
select bitmapColumnOr(rbm) as result
from (
    select arrayToBitmap([1,2,3]) as rbm
    union all
    select arrayToBitmap([2,3,4]) as rbm
)
```


Result:

```SQL
┌─result────┐
│ {1,2,3,4} │
└───────────┘
```


<span id="f153579b"></span>
### bitmapColumnXor

Calculate the XOR set of a bitmap column.

**Syntax**

```SQL
bitmapColumnXor(bitmap_column)
```


**Parameters**

`bitmap_column` \- Data column of BitMap64 type.

**Return Value**


* A BitMap64 object


**Example**

```SQL
select bitmapColumnXor(rbm) as result
from (
    select arrayToBitmap([1,2,3]) as rbm
    union all
    select arrayToBitmap([2,3,4]) as rbm
)
```


Result:

```SQL
┌─result─┐
│ {1,4}  │
└────────┘
```


<span id="105c5345"></span>
### bitmapColumnCardinality

Calculate the number of elements in the union of a column of bitmaps.

**Syntax**

```SQL
bitmapColumnCardinality(bitmap_column)
```


**Parameters**

`bitmap_column` \- A data column of type BitMap64.

**Return value**


* A UInt64 number representing the count of bitmap elements.


**Example**

```SQL
select bitmapColumnCardinality(rbm) as result
from (
    select arrayToBitmap([1,2,3]) as rbm
    union all
    select arrayToBitmap([2,3,4]) as rbm
)
```


Result:

```SQL
┌─result─┐
│      4 │
└────────┘
```


<span id="36c2fe9e"></span>
### bitmapColumnHas

Determine if a specified value is contained within a column of bitmaps.

**Syntax**

```SQL
bitmapColumnHas(bitmap_column, integer_number)
```


**Parameters**

`bitmap_column` \- A data column of BitMap64 type.

`integer_number` \- A constant numeric value. Type is a positive integer up to 64 bits.

**Return Value**


* A Bool value, 0 indicates the given value does not exist, 1 indicates it exists.

* The difference between the function `bitmapContains` and this function is that the latter returns a single row value for a column of bitmaps, whereas `bitmapContains` returns multiple rows.


**Example**

```SQL
select bitmapColumnHas(rbm, 3) as result
from (
    select arrayToBitmap([1,2,3]) as rbm
    union all
    select arrayToBitmap([2,3,4]) as rbm
)
```


Result:

```SQL
┌─result─┐
│      1 │
└────────┘
```


<span id="93527650"></span>
### bitmapFromColumn

Create a BitMap64 object from a column of values.

**Syntax**

```SQL
bitmapFromColumn(integer_column)
```


**Parameters**


* `integer_column` \- A column of non\-negative integers of up to 64 bits.


**Return Value**


* A BitMap64 object


**Example**

```SQL
select bitmapFromColumn(number) as res from numbers(10);
```


Result:

```SQL
┌─res───────────────────┐
│ {0,1,2,3,4,5,6,7,8,9} │
└───────────────────────┘
```


<span id="f15932e7"></span>
# Advanced aggregation functions

This function takes two sets of parentheses for passing parameters:


* The first parenthesis is called parameter, which controls the behavior of aggregate functions (control flow)

* The second parenthesis is called argument, which is used to pass input data columns to the aggregate function (data flow)


ByteHouse offers a range of aggregate functions for bulk processing complex calculations between numerous bitmaps. By assigning serial numbers to each bitmap to be calculated and using these numbers to express set operations of intersection, union, and difference, ByteHouse can perform bitmap calculations based on the specified expression, directly visualizing and simplifying the computation, greatly enhancing the SQL writing experience!

A simple illustration is as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2530eb9f822d4a44b7b76e01d769b3d4~tplv-goo7wpa0wc-image.image) </span>


|Index |Function interface |Parameter description |Return value |Function definition |
|---|---|---|---|---|
|1 |bitmapCount<br><br>(expression)<br><br>(idx, bitmap)<br><br>\-\> integer |expression is a set expression with `&` for intersection, `\|` for union, and `~` for difference<br><br>idx refers to labels for each row of bitmap, using **positive integer type Int16/32** |UInt64 value |For each row in the bitmap column, retrieve its label idx and store it in a map. Finally, perform bitmap operations as specified by the expression and return the count of elements in the final bitmap. |
|2 |bitmapExtract<br><br>(idx, bitmap)<br><br>\-\> bitmap |expression is a set operation expression where `&` represents intersection, `\|` represents union, and `~` represents difference set<br><br>idx is the marker corresponding to each row of bitmap, using **positive integer Int16/32 type** |BitMap64 object |For each row in the bitmap column, take its idx and perform bitmap operations specified by expression to return the final computed bitmap |
|3 |bitmapMultiCount<br><br>(expr1, expr2, ...)<br><br>(idx, bitmap)<br><br>\-\> [int1, int2, ...] |expression is an expression of union, intersection, and difference, `&` denotes intersection, `\|` denotes union, `~` denotes difference<br><br>idx is the marker for each row's bitmap, using **positive integer Int16/32 type** |UInt64 array |For each row in the bitmap column, take its index idx, and perform multiple bitmap operations according to the computational methods specified by each expr, returning the number of elements in the result bitmap for **each group expr** |
|4 |bitmapMultiExtract<br><br>(expr1, expr2, ...)<br><br>(idx, bitmap)<br><br>\-\> [bitmap1, bitmap2, ...] |"expression" is a Boolean expression where `&` represents intersection, `\|` represents union, and `~` represents difference<br><br>idx represents each row's bitmap index, using **positive integer of type Int16/32** |BitMap64 array |For each row in the bitmap column, obtain its index idx, perform bitmap operations according to the calculation method specified by each expr, and return the bitmap data of each group's expr calculation |
|5 |bitmapMultiCountWithDate<br><br>(expr1, expr2, ...)<br><br>(date, idx, bitmap)<br><br>\-\> [int1, int2, ...] |"expression" is a Boolean expression where `&` represents intersection, `\|` represents union, and `~` represents difference<br><br>The date is in Int64 date format<br><br>idx is a marker for each row bitmap, using **positive integer Int16/32 type** |UInt64 array |On top of bitmapMultiCount, a date dimension has been added to distinguish identifiers on different dates. While bitmapMultiCount only supports one identifier dimension, this function adds a date dimension. |
|6 |bitmapMultiExtractWithDate<br><br>(expr1, expr2, ...)<br><br>(date, idx, bitmap)<br><br>\-\> [bitmap1, bitmap2, ...] |"Expression" is an expression for unions/intersections/differences; `&` indicates intersection, `\|` indicates union, and `~` indicates difference.<br><br>"Date" is a date format of type Int64.<br><br>"Idx" denotes the label corresponding to each row in a bitmap, using **integer types Int16/32**. |BitMap64 array. |Based on bitmapMultiExtract, a date dimension has been added to distinguish tags across different dates. Whereas bitmapMultiExtract supports only one identification dimension, this function additionally incorporates a date dimension. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If multiple rows with the same "idx" exist, the aggregate function will automatically merge these rows' bitmaps through an OR operation to participate in the calculation. In the final calculation, one idx corresponds to one bitmap.</div>


Here are specific function descriptions.

<span id="c1c627af"></span>
### BitmapCount

Based on the user\-specified calculation expression, it performs the corresponding bitmap operations and returns the number of elements in the final bitmap.

**Syntax**

```SQL
BitMapCount(expr)(idx_column, bitmap_column)
```


**Parameter**


* `expr` \- Represents operations with "and" (`&`), "or" (`|`), and "difference" (`~`), where `&` indicates a bitmap intersection, `|` a bitmap union, and `~` a bitmap difference, supporting only one expression.

* `idx_column` \- A data column used to mark bitmaps, which can be an integer column (typically Int16/32/64 type), or a string column.

* `bitmap_column` \- A BitMap64 data column.


**Note 1**: The data in `idx_column` and `bitmap_column` do not need to correspond one\-to\-one. If `idx_column` contains duplicate data, multiple rows of bitmaps with the same value will first undergo a union operation to merge into a single unique bitmap for computation purposes.

**Note 2**: When the `idx_column` column type is a string, it **cannot** include the following reserved characters: `&`, `|`, `~`, `,`, `#`, `(`, `)`, `_` and spaces.

**Return Value**


* UInt64 \- The number of elements in the computed bitmap.


**Example**

```SQL
SELECT bitmapCount('a')(tag_value, uids) AS res
FROM
(
    SELECT
        'a' AS tag_value,
        arrayToBitmap([1, 2, 3]) AS uids
)
```


Result:

```SQL
┌─res─┐
│   3 │
└─────┘
```


```SQL
SELECT
    BitmapCount('((a&b)|c) ~ d')(tag_value, uids) AS res1,
    BitmapCount('((1&2)|3)~4')(multiIf(tag_value = 'a', toInt16(1), tag_value = 'b', toInt16(2), tag_value = 'c', toInt16(3), tag_value = 'd', toInt16(4), toInt16(0)) AS idx, uids) AS res2
FROM
(
    SELECT
        'a' AS tag_value,
        arrayToBitmap([1, 2, 3, 4, 5]) AS uids
    UNION ALL
    SELECT
        'b' AS tag_value,
        arrayToBitmap([3, 4, 5, 6]) AS uids
    UNION ALL
    SELECT
        'c' AS tag_value,
        arrayToBitmap([5, 7]) AS uids
    UNION ALL
    SELECT
        'd' AS tag_value,
        arrayToBitmap([7]) AS uids
)
```


Result

```SQL
┌─res1─┬─res2─┐
│    3 │    3 │
└──────┴──────┘
```


<span id="bc91a645"></span>
### BitmapExtract

Performs bitmap computations as specified by the user\-defined expression and returns the final bitmap.

**Syntax**

```SQL
BitMapExtract(expr)(idx_column, bitmap_column)
```


**Parameters**


* `expr` \- Uses numbers or strings for operations such as AND (`&`), OR (`|`), and NOT (`~`). `&` denotes the bitmap intersection, `|` denotes the bitmap union, and `~` denotes the bitmap difference. This function supports only one expression.

* `idx_column` \- Data column marking the bitmap, which can be a column of integers (typically Int16/32/64) or a string column.

* `bitmap_column` \- BitMap64 data column.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">There's no requirement for <code>idx_column</code> data to correspond one\-to\-one with <code>bitmap_column</code> data; if <code>idx_column</code> has duplicate data, bitmaps with the same values are first unified through a union operation to form a unique bitmap for participation in calculations.</div>


* <div data-tips="true" data-tips-type="warning">When <code>idx_column</code> is of string type, it <strong>cannot</strong> include the following reserved characters: <code>&</code>, <code>|</code>, <code>~</code>, <code>,</code>, <code>#</code>, <code>(</code>, <code>)</code>, <code>_</code> and spaces.</div>



**Return Value**


* BitMap64 \- Computed bitmap object.


**Example**

```SQL
SELECT bitmapExtract('a')(tag_value, uids) AS res
FROM
(
    SELECT
        'a' AS tag_value,
        arrayToBitmap([1, 2, 3]) AS uids
)
```


Result

```SQL
┌─res─────┐
│ {1,2,3} │
└─────────┘
```


```SQL
SELECT
    BitmapExtract('((a&b)|c) ~ d')(tag_value, uids) AS res1,
    BitmapExtract('((1&2)|3)~4')(multiIf(tag_value = 'a', toInt16(1), tag_value = 'b', toInt16(2), tag_value = 'c', toInt16(3), tag_value = 'd', toInt16(4), toInt16(0)) AS idx, uids) AS res2
FROM
(
    SELECT
        'a' AS tag_value,
        arrayToBitmap([1, 2, 3, 4, 5]) AS uids
    UNION ALL
    SELECT
        'b' AS tag_value,
        arrayToBitmap([3, 4, 5, 6]) AS uids
    UNION ALL
    SELECT
        'c' AS tag_value,
        arrayToBitmap([5, 7]) AS uids
    UNION ALL
    SELECT
        'd' AS tag_value,
        arrayToBitmap([7]) AS uids
)
```


Result:

```SQL
┌─res1────┬─res2────┐
│ {3,4,5} │ {3,4,5} │
└─────────┴─────────┘
```


<span id="be1f2e5c"></span>
### BitmapMultiCount

Based on a set of calculation expressions specified by the user, perform the corresponding bitmap operations for each group and return the number of elements in the final bitmap for each group.

**Syntax**

```SQL
BitmapMultiCount(expr1, expr2, expr3,...)(idx_column, bitmap_column)
```


**Parameters**


* `expr` \- Represents operations with: and (`&`), or (`|`), subtract (`~`). `&` denotes bitmap intersection, `|` denotes bitmap union, `~` denotes bitmap difference. This function supports multiple expressions.

* `idx_column` \- The data column used to mark the bitmap, which can be a column of integers (usually of type Int16/32/64) or a string column.

* `bitmap_column` \- BitMap64 data column.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Do not require <code>idx_column</code> data and <code>bitmap_column</code> data to correspond one\-to\-one. If <code>idx_column</code> contains repeated data, then rows with the same value will first undergo a union operation to merge into a unique bitmap for the calculation.</div>


* <div data-tips="true" data-tips-type="warning">When the type of the <code>idx_column</code> column is String, it <strong>must not</strong> contain the following reserved characters:<code>&</code>, <code>|</code>, <code>~</code>, <code>,</code>, <code>#</code>, <code>(</code>, <code>)</code>, <code>_</code> and English space.</div>


* <div data-tips="true" data-tips-type="warning">Supports result reuse. For example, <code>expr1='a&b'</code>, <code>expr2='(a&b)|c'</code>. Therefore, expr2 can be simplified as <code>expr2='_1|c'</code>. Using an underline followed by a number can specify an expression that has already appeared, simplifying complex expression formulations.</div>



**Return Value**


* UInt64 Array \- The number of elements in the bitmap resulting from each expression's evaluation. The size of the array matches the number of expressions.


**Example**

```SQL
SELECT BitmapMultiCount('a')(tag_value, uids) AS res
FROM
(
    SELECT
        'a' AS tag_value,
        arrayToBitmap([1, 2, 3]) AS uids
)
```


```SQL
┌─res─┐
│ [3] │
└─────┘
```


```SQL
SELECT BitmapMultiCount('1&2', '(1&2)|3', '_1|3', '((1&2)|3) ~ 4', '_2~4')(tag_value, uids) AS res
FROM
(
    SELECT
        toInt32(1) AS tag_value,
        arrayToBitmap([1, 2, 3, 4, 5]) AS uids
    UNION ALL
    SELECT
        toInt32(2) AS tag_value,
        arrayToBitmap([3, 4, 5, 6]) AS uids
    UNION ALL
    SELECT
        toInt32(3) AS tag_value,
        arrayToBitmap([5, 7]) AS uids
    UNION ALL
    SELECT
        toInt32(4) AS tag_value,
        arrayToBitmap([7]) AS uids
)
```


Result:

```SQL
┌─res─────────┐
│ [3,4,4,3,3] │
└─────────────┘
```


<span id="0e6a9e3f"></span>
### BitmapMultiExtract

Based on a set of expressions specified by the user, this function performs the corresponding bitmap operations for each group and returns the final bitmap for each.

**Syntax**

```SQL
BitmapMultiExtract(expr1, expr2, expr3,...)(idx_column, bitmap_column)
```


**Parameters**


* `expr` \- Uses numbers or strings for and (`&`), or (`|`), minus (`~`) operations. `&` denotes bitmap intersection, `|` denotes bitmap union, `~` denotes bitmap difference. The function supports multiple expressions.

* `idx_column` \- Data column used to mark the bitmap, which can be an integer column (usually of type Int16/32/64) or a string column.

* `bitmap_column` \- BitMap64 data column.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Do not require <code>idx_column</code> data and <code>bitmap_column</code> data to correspond one\-to\-one. If <code>idx_column</code> contains repeated data, then rows with the same value will first undergo a union operation to merge into a unique bitmap for the calculation.</div>


* <div data-tips="true" data-tips-type="warning">When the type of the <code>idx_column</code> column is String, it <strong>must not</strong> contain the following reserved characters: <code>&</code>, <code>|</code>, <code>~</code>, <code>,</code>, <code>#</code>, <code>(</code>, <code>)</code>, <code>_</code> and English space.</div>


* <div data-tips="true" data-tips-type="warning">Supports result reuse. For example, <code>expr1='a&b'</code>, <code>expr2='(a&b)|c'</code>. Thus, the notation of <code>expr2='_1|c'</code> simplifies expr2. Using an underscore + number can specify an already appeared expression, simplifying the notation of complex expressions.</div>



**Return value**


* BitMap64 array \- An array of bitmaps calculated for each expression, the size of the array equals the number of expressions.


**Example**

```SQL
SELECT BitmapMultiExtract('a')(tag_value, uids) AS res
FROM
(
    SELECT
        'a' AS tag_value,
        arrayToBitmap([1, 2, 3]) AS uids
)
```


```SQL
┌─res───────┐
│ [{1,2,3}] │
└───────────┘
```


```SQL
SELECT BitmapMultiExtract('1&2', '(1&2)|3', '_1|3', '((1&2)|3) ~ 4', '_2~4')(tag_value, uids) AS res
FROM
(
    SELECT
        toInt32(1) AS tag_value,
        arrayToBitmap([1, 2, 3, 4, 5]) AS uids
    UNION ALL
    SELECT
        toInt32(2) AS tag_value,
        arrayToBitmap([3, 4, 5, 6]) AS uids
    UNION ALL
    SELECT
        toInt32(3) AS tag_value,
        arrayToBitmap([5, 7]) AS uids
    UNION ALL
    SELECT
        toInt32(4) AS tag_value,
        arrayToBitmap([7]) AS uids
)
```


Result:

```SQL
┌─res───────────────────────────────────────────┐
│ [{3,4,5},{3,4,5,7},{3,4,5,7},{3,4,5},{3,4,5}] │
└───────────────────────────────────────────────┘
```


<span id="8859cd22"></span>
### BitmapMultiCountWithDate

Based on a set of expressions specified by the user, perform the corresponding bitmap operations for each group and return the number of elements in each final bitmap. Compared to the function `BitmapMultiCount`, this adds a date dimension to represent.

**Syntax**

```SQL
BitmapMultiCountWithDate(expr1, expr2, expr3,...)(date_column, idx_column, bitmap_column)
```


**Parameter**


* `expr` involves operations using numbers or strings with `&` (AND), `|` (OR), and `~` (Difference). `&` represents bitmap intersection, `|` represents bitmap union, `~` represents bitmap difference. This function supports multiple expressions, each comprising two parts: a date and a tag connected with an underscore. Example: `20240101_aaa&20240102_aaa`.

* `date_column` specifies the data date, which should be an Int64 type date column in the format YYYYMMDD.

* `idx_column` marks the bitmap data column, which can be a column of integers (usually Int16/32/64 types) or strings.

* `bitmap_column` \- BitMap64 data column.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">It is not mandatory for the data of <code>date_column+idx_column</code> to correspond one\-to\-one with <code>bitmap_column</code> data. If <code>date_column+idx_column</code> has repeated data, multiple bitmap rows with the same values will first undergo union operations to merge into a single unique bitmap for calculations.</div>


* <div data-tips="true" data-tips-type="warning">When the <code>idx_column</code> column's type is a string, it <strong>cannot</strong> include the following reserved characters: <code>&</code>, <code>|</code>, <code>~</code>, <code>,</code>, <code>#</code>, <code>(</code>, <code>)</code>, <code>_</code>, and English spaces.</div>


* <div data-tips="true" data-tips-type="warning">Support of results reuse. For instance, <code>expr1='a&b'</code>, <code>expr2='(a&b)|c'</code>. Thus, the notation of <code>expr2='_1|c'</code> simplifies expr2. Using an underscore + number can specify an already appeared expression, simplifying the notation of complex expressions.</div>



**Return value**


* UInt64 array \- contains counts of elements in the bitmap for each expression. The size of the array is equal to the number of expressions.


**Example**

```SQL
SELECT BitmapMultiCountWithDate('20240102_a~20240101_a', '20240101_a&20240102_a')(toInt64(toYYYYMMDD(date)), tag_value, uids) AS res
FROM
(
    SELECT
        'a' AS tag_value,
        '2024-01-01' AS date,
        arrayToBitmap([1, 2, 3]) AS uids
    UNION ALL
    SELECT
        'a' AS tag_value,
        '2024-01-02' AS date,
        arrayToBitmap([2, 3, 4, 5, 6]) AS uids
)
```


```SQL
┌─res───┐
│ [3,2] │
└───────┘
```


```SQL
SELECT BitmapMultiCountWithDate('20240101_1 & 20240102_2', '_1 | 20240101_3', '_2 ~ 20240101_4')(toInt64(toYYYYMMDD(date)), tag_value, uids) AS res
FROM
(
    SELECT
        toInt32(1) AS tag_value,
        '2024-01-01' AS date,
        arrayToBitmap([1, 2, 3, 4, 5]) AS uids
    UNION ALL
    SELECT
        toInt32(2) AS tag_value,
        '2024-01-02' AS date,
        arrayToBitmap([3, 4, 5, 6]) AS uids
    UNION ALL
    SELECT
        toInt32(3) AS tag_value,
        '2024-01-01' AS date,
        arrayToBitmap([5, 7]) AS uids
    UNION ALL
    SELECT
        toInt32(4) AS tag_value,
        '2024-01-01' AS date,
        arrayToBitmap([7]) AS uids
)
```


Result:

```SQL
┌─res─────┐
│ [3,4,3] │
└─────────┘
```


<span id="27e1197a"></span>
### BitmapMultiExtractWithDate

Based on a set of calculation expressions specified by the user, each set performs the corresponding bitmap operation, returning the final bitmap for each group. Compared to the function `BitmapMultiExtract`, it adds a dimension represented by a date.

**Syntax**

```SQL
BitmapMultiExtractWithDate(expr1, expr2, expr3,...)(date_column, idx_column, bitmap_column)
```


**Parameters**


* `expr` \- Uses numbers or strings to represent operations AND (`&`), OR (`|`), and DIFFERENCE (`~`); `&` represents bitmap intersection, `|` represents bitmap union, and `~` represents bitmap difference. The function supports multiple expressions, note that each expression consists of two parts: a date and a tag, connected by an underscore, with an example being `20240101_aaa&20240102_aaa`.

* `date_column` \- Specifies the data date, needed in Int64 type date column with format YYYYMMDD.

* `idx_column` \- Used to mark the data column of the bitmap, which can be an integer column (usually Int16/32/64 type) or a string column.

* `bitmap_column` \- BitMap64 data column.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">It is not mandatory for the data of <code>date_column+idx_column</code> to correspond one\-to\-one with <code>bitmap_column</code> data. If <code>date_column+idx_column</code> has repeated data, multiple bitmap rows with the same values will first undergo union operations to merge into a single unique bitmap for calculations.</div>


* <div data-tips="true" data-tips-type="warning">When the <code>idx_column</code> column's type is a string, it <strong>cannot</strong> include the following reserved characters: <code>&</code>, <code>|</code>, <code>~</code>, <code>,</code>, <code>#</code>, <code>(</code>, <code>)</code>, <code>_</code>, and English spaces.</div>


* <div data-tips="true" data-tips-type="warning">Supports result reuse. For example, <code>expr1='a&b'</code>, <code>expr2='(a&b)|c'</code>. Then the expression for expr2 can be simplified as <code>expr2='_1|c'</code>. Using an underline followed by a number can specify an expression that has already appeared, simplifying the writing of complex expressions.</div>



**Return Value**


* BitMap64 array \- An array of bitmap results for each expression, with the array size equal to the number of expressions.


**Example**

```SQL
SELECT BitmapMultiExtractWithDate('20240102_a~20240101_a', '20240101_a&20240102_a')(toInt64(toYYYYMMDD(date)), tag_value, uids) AS res
FROM
(
    SELECT
        'a' AS tag_value,
        '2024-01-01' AS date,
        arrayToBitmap([1, 2, 3]) AS uids
    UNION ALL
    SELECT
        'a' AS tag_value,
        '2024-01-02' AS date,
        arrayToBitmap([2, 3, 4, 5, 6]) AS uids
)
```


```SQL
┌─res─────────────┐
│ [{4,5,6},{2,3}] │
└─────────────────┘
```


```SQL
SELECT BitmapMultiExtractWithDate('20240101_1 & 20240102_2', '_1 | 20240101_3', '_2 ~ 20240101_4')(toInt64(toYYYYMMDD(date)), tag_value, uids) AS res
FROM
(
    SELECT
        toInt32(1) AS tag_value,
        '2024-01-01' AS date,
        arrayToBitmap([1, 2, 3, 4, 5]) AS uids
    UNION ALL
    SELECT
        toInt32(2) AS tag_value,
        '2024-01-02' AS date,
        arrayToBitmap([3, 4, 5, 6]) AS uids
    UNION ALL
    SELECT
        toInt32(3) AS tag_value,
        '2024-01-01' AS date,
        arrayToBitmap([5, 7]) AS uids
    UNION ALL
    SELECT
        toInt32(4) AS tag_value,
        '2024-01-01' AS date,
        arrayToBitmap([7]) AS uids
)
```


Result:

```SQL
┌─res─────────────────────────┐
│ [{3,4,5},{3,4,5,7},{3,4,5}] │
└─────────────────────────────┘
```


<span id="af91fd2b"></span>
# Other functions and operation interfaces

<span id="9af7dd49"></span>
## BitEngine Scenario Encoding and Decoding Functions


|No. |Function interface |Parameter description |Return value |Brief explanation |
|---|---|---|---|---|
|1 |EncodeNonBitEngineColumn(UInt64_column, database, table, dictionary，add_new_key_to_bitengine_dict)<br><br>\-\> UInt64<br><br>The last parameter is a new optional parameter. If not present, the default value is 0; if required, it must be provided and assigned a value of 1. |UInt64_column:<br><br>source input;<br><br>Database, table, dictionary: Specifies the source of the dictionary used, as a string<br><br>add_new_key_to_bitengine_dict, how to handle IDs not found in the dictionary? Join the dictionary or discard it? |UInt64 value |Use a regular UInt64 as the Key in a BitEngine K\-V dictionary to retrieve the value after dictionary encoding<br><br>Add:<br><br>add_new_key_to_bitengine_dict controls how to handle newly encountered ids:<br><br>0: Default behaviour, optional, not added to the dictionary;<br><br>1: Addition behaviour, must be included, when a new id is encountered during dictionary encoding, it is added to the dictionary. |
|2 |DecodeNonBitEngineColumn(UInt64_column, database, table, dictionary)<br><br>\-\> UInt64 |UInt64_column:<br><br>source input;<br><br>Database, table, dictionary: Specify the dictionary source used, string |UInt64 value |Use normal UInt64 as the value in BitEngine K\-V dictionary to get its value before dictionary encoding |
|3 |EncodeBitmap(bitmap, database, table, dictionary, add_new_key_to_bitengine_dict)<br><br>\-\> BitMap64<br><br>The last parameter is a newly added optional parameter. If not provided, the default value is 0, and if needed, it must be included and set to 1. |bitmap: source input;<br><br>Database, table, dictionary: Specify the dictionary source used, string |BitMap64 object |Encode a bitmap using the BitEngine dictionary<br><br>Add:<br><br>add_new_key_to_bitengine_dict controls how to handle new appearing IDs:<br><br>0: Default behaviour, optional, will not be added to the dictionary;<br><br>1: Add behaviour, mandatory, new IDs encountered during dictionary encoding are added to the dictionary. |
|4 |DecodeBitmap(bitmap, database, table, dictionary)<br><br>\-\>BitMap64 |bitmap: source input;<br><br>Database, table, dictionary: strings identify the dictionary source |BitMap64 object |Use BitEngine dictionary for decoding an bitmap |
|5 |arrayToBitmapWithEncode<br><br>([x1,...], 'db', 'tbl', 'dict_name',<br><br>add_new_key_to_bitengine_dict)<br><br>\-\> bitmap<br><br>The last parameter is a newly added optional parameter If not specified, the default value is 0; if required, it must be included, and assigned a value of 1 |Array of UIntN type,<br><br>N={8, 16, 32, 64},<br><br>db, tbl, dict_name correspond to database, table, and column respectively<br><br>How does add_new_key_to_bitengine_dict control the processing of newly appeared IDs? Join the dictionary or discard. |BitMap64 object |Use an already existed BitEngine dictionary to encode a new bitmap, returning the coded bitmap<br><br>Add:<br><br>How does control add_new_key_to_bitengine_dict handle newly appeared IDs:<br><br>0: Default behavior, optional, do not join the dictionary;<br><br>Add a new behavior, which must be brought along. When encountering a new id during dictionary coding, add it to the dictionary. |
|6 |bitmapToArrayWithDecode(bitmap, 'db', 'tbl', 'dict_name')<br><br>\-\> array |bitmap: source input;<br><br>Database, table, dictionary: strings identify the dictionary source |Array(UInt64) |Decode the bitmap and at the same time convert the bitmap into an array |


<span id="534892e0"></span>
# Replace community BitMap functions

If you have previously used community BitMap functions and now wish to migrate to ByteHouse, you can follow the rules below to replace the community BitMap functions.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">ClickHouse/ByteHouse supports the combination of aggregate functions with operators. For details, see <a href="https://clickhouse.com/docs/en/sql-reference/aggregate-functions/combinators">Aggregate Function Combinators</a>. The usage format is 【function name】+【Combinator】, common Combinators include <code>-If</code>, <code>-State</code>. For instance, <code>groupBitmapOrState</code>, <code>groupBitmapOrStateIf</code>. When replacing functions, only consider the <code>groupBitmapOr</code> function name; the Combinator part remains unchanged.</div>


<div data-tips="true" data-tips-type="warning">Common Combinator replacement rules:</div>



* <div data-tips="true" data-tips-type="warning"><code>-State</code>: remove directly</div>


* <div data-tips="true" data-tips-type="warning"><code>-If</code>: retain</div>


* <div data-tips="true" data-tips-type="warning"><code>-Merge</code>: remove directly</div>



<div data-tips="true" data-tips-type="warning">Example:</div>


<div data-tips="true" data-tips-type="warning"><code>groupBitmapStateIf</code> \-\> <code>bitmapFromColumnIf</code></div>


<div data-tips="true" data-tips-type="warning"><code>groupBitmapOrState</code> \-\> <code>bitmapColumnOr</code></div>


ByteHouse has adapted and supports all ClickHouse community bitmap functions, with the mapping relationship as follows:


|ClickHouse community function name |ByteHouse equivalent implementation |Example |
|---|---|---|
|bitmapBuild |arrayToBitmap |Example: `select arrayToBitmap([1,2,3])` |
|bitmapToArray |bitmapToArray |Example: `select bitmapToArray(arrayToBitmap([1,2,3]))` |
|bitmapSubsetInRange |bitmapSubsetInRange |Example: `select bitmapSubsetInRange(arrayToBitmap([1,2,3]), 1, 2)` |
|bitmapSubsetLimit |bitmapSubsetLimit |Example: `select bitmapSubsetLimit(arrayToBitmap([1,2,3]), 1, 1)` |
|subBitmap |subBitmap |Example: `select subBitmap(arrayToBitmap([1,2,3]), 2, 2)` |
|bitmapContains |bitmapContains |Example: `select bitmapContains(arrayToBitmap([1,2,3]), 2)` |
|bitmapHasAny |bitmapHasAny |Example: `select bitmapHasAny(arrayToBitmap([1,2,3]), arrayToBitmap([2,3]))` |
|bitmapHasAll |bitmapHasAll |Example: `select bitmapHasAll(arrayToBitmap([1,2,3]), arrayToBitmap([2,3]))` |
|bitmapCardinality |bitmapCardinality |Example: `select bitmapCardinality(arrayToBitmap([1,2,3]))` |
|bitmapMin |bitmapMin |Example: `select bitmapMin(arrayToBitmap([1,2,3]))` |
|bitmapMax |bitmapMax |Example: `select bitmapMax(arrayToBitmap([1,2,3]))` |
|bitmapTransform |bitmapTransform |Example: `select bitmapTransform(arrayToBitmap([1,2,3]), [2,3], [3,4])` |
|bitmapAnd |bitmapAnd |Example: `select bitmapAnd(arrayToBitmap([1,2,3]), arrayToBitmap([2,3]))` |
|bitmapOr |bitmapOr |Example: `select bitmapOr(arrayToBitmap([1,2,3]), arrayToBitmap([2,3]))` |
|bitmapXor |bitmapXor |Example: `select bitmapXor(arrayToBitmap([1,2,3]), arrayToBitmap([2,3]))` |
|bitmapAndnot |bitmapAndnot |Example: `select bitmapAndnot(arrayToBitmap([1,2,3]), arrayToBitmap([2,3]))` |
|bitmapAndCardinality |bitmapAndCardinality |Example: `select bitmapAndCardinality(arrayToBitmap([1,2,3]), arrayToBitmap([2,3]))` |
|bitmapOrCardinality |bitmapOrCardinality |Example: `select bitmapOrCardinality(arrayToBitmap([1,2,3]), arrayToBitmap([2,3]))` |
|bitmapXorCardinality |bitmapXorCardinality |Example: `select bitmapXorCardinality(arrayToBitmap([1,2,3]), arrayToBitmap([2,3]))` |
|bitmapAndnotCardinality |bitmapAndnotCardinality |Example: `select bitmapAndnotCardinality(arrayToBitmap([1,2,3]), arrayToBitmap([2,3]))` |
|groupBitmap |bitmapCardinality(bitmapFromColumn(number)) |Example: `select bitmapCardinality(bitmapFromColumn(number)) from numbers(Oct);` |
|groupBitmapState |bitmapFromColumn |Example: `select bitmapFromColumn(number) from numbers(Oct);` |
|groupBitmapOr |bitmapColumnCardinality |Example: `select bitmapColumnCardinality(rbm) from (select bitmapFromColumn(number) as rbm from numbers(Oct));` |
|groupBitmapOrState |bitmapColumnOr |Example: `select bitmapColumnOr(rbm) from (select bitmapFromColumn(number) as rbm from numbers(10));` |
|groupBitmapAnd |bitmapCardinality(bitmapColumnAnd(bitmap_column)) |Example: `select bitmapCardinality(bitmapColumnAnd(rbm)) from (select bitmapFromColumn(number) as rbm from numbers(10));` |
|groupBitmapAndState |bitmapColumnAnd |Example: `select bitmapColumnAnd(rbm) from (select bitmapFromColumn(number) as rbm from numbers(10));` |
|groupBitmapXor |bitmapCardinality(bitmapColumnXor(bitmap_column)) |Example: `select bitmapCardinality(bitmapColumnXor(rbm)) from (select bitmapFromColumn(number) as rbm from numbers(Oct));` |
|groupBitmapXorState |bitmapColumnXor |Example: `select bitmapColumnXor(rbm) from (select bitmapFromColumn(number) as rbm from numbers(Oct));` |


<span id="8a5faa72"></span>
# Function usage example

<span id="57a3fa2e"></span>
## Build test Table

Example of using table test.bitmap_test.

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


<span id="29a2bf2e"></span>
## Write data

Data involves two tags, tag_id=11 with two tag values 'a' and 'b'; tag_id=12 with one tag value 'c'.

Each tag value has two rows, each with a different slice_id. The slice_id is used to split a large bitmap into smaller parts, reducing the size of each bitmap row, optimizing construction efficiency and memory usage, and also providing sharding credentials for distributed storage.

```SQL
insert into test.bitmap_test values ('2024-01-01', 0, 11, 'a', [1,2,3,4,5]), ('2024-01-02', 1, 11,'a', [11,12,13,14,15]);
insert into test.bitmap_test values ('2024-01-01', 0, 11, 'b', [3,4,5,6,7,8]), ('2024-01-02', 1, 11,'b', [13, 14,15,16]);
insert into test.bitmap_test values ('2024-01-01', 0, 12, 'c', [3,4,6,7,9]), ('2024-01-02', 1, 12,'c', [13,15,16,18]);
```


<span id="ca3a9256"></span>
## Example: standard function

The use of standard functions, community demos, and other functions are no different. Just a few examples.

<span id="c8d617a7"></span>
### Array to bitmap

```SQL
SELECT arrayToBitmap([1, 2, 3, 4, 5])
FORMAT TSV

-- Result
{1,2,3,4,5}
```


<span id="7d4cc2c4"></span>
### Bitmap to array

```SQL
SELECT bitmapToArray(uids)
FROM test.bitmap_test
WHERE tag_value = 'a'
FORMAT TSV

-- Result
[11,12,13,14,15]
[1,2,3,4,5]


SELECT bitmapToArray(arrayToBitmap([1, 2, 3, 4, 5]))
FORMAT TSV

-- Result
[1,2,3,4,5]
```


<span id="5e9086cf"></span>
### Count the number of elements in a bitmap

```SQL
SELECT bitmapCardinality(arrayToBitmap([1, 2, 3, 4, 5]))
FORMAT TSV

-- Result
5
```


<span id="54a0d088"></span>
## Example: Aggregate Functions

<span id="e22726a3"></span>
### Operations on multiple bitmaps: intersection/union/xor

```SQL
-- Find the intersection of two bitmaps
SELECT bitmapColumnAnd(uids)
FROM test.bitmap_test
WHERE (slice_id = 0) AND (tag_value IN ('a', 'b'))
FORMAT TSV

-- Result
{3,4,5}

-- Find the union of two bitmaps (the two functions have the same meaning)
SELECT
    bitmapCardinality(bitmapColumnOr(uids)),
    bitmapColumnCardinality(uids)
FROM test.bitmap_test
WHERE (slice_id = 0) AND (tag_value IN ('a', 'b'))
FORMAT TSV

-- Result
8        8

-- Determine whether a given element exists in a certain bitmap
SELECT bitmapColumnHas(uids, 12)
FROM test.bitmap_test
WHERE tag_value = 'a'
FORMAT TSV

--Result
1
```


<span id="c2137a2d"></span>
### Aggregate a bitmap

```Plain
SELECT bitmapFromColumn(number)
FROM
(
    SELECT number
    FROM system.numbers
    LIMIT 100, 10
)
FORMAT TSV

-- Result
{100,101,102,103,104,105,106,107,108,109}
```


<span id="b7f87275"></span>
### bitmapCount function

**Usage:**  Implement complex set operations such as intersection, union, and difference among multiple bitmaps. Users express bitmap operations through input expressions, which the function parses and calculates accordingly. Refer to the example in the section "Aggregate Functions" \- "Advanced Aggregate Functions" above.

**Input:**  ID column, bitmap column. The ID column identifies the bitmap, which can be a field in the table (such as tag_id) or a user\-defined variable (such as idx).

**Expression:**  A code anchors a bitmap. The numbering expression corresponds to the intersection, union, and difference operations on the bitmap.

Supported numbering operators:


* Or operation: Denoted by a comma ('1,2') or vertical bar ('1|2').

* And operation: Denoted by an ampersand ('1&2').

* Difference operation: Denoted by a tilde ('1~2').


**Output:**  The element count in the bitmap after performing intersection, union, and difference operations.

Case 1: Calculate the total number of items for a specific tag 'a'.

```SQL
SELECT bitmapColumnCardinality(uids)
FROM test.bitmap_test
WHERE tag_value = 'a'
FORMAT TSV

-- Result
10

-- Find the total number of elements with the label 'a'. It is equivalent to the calculation of bitmapColumnCardinality
SELECT bitmapCount('1')(If(tag_value = 'a', toInt32(1), toInt32(999)) AS idx, uids) AS card
FROM test.bitmap_test
WHERE tag_value = 'a'
FORMAT TSV

-- Result
10

-- Find the total number of elements with the label 'a'. Since the label is a string, a string expression can be directly used
SELECT bitmapCount('a')(tag_value, uids)
FROM test.bitmap_test
WHERE tag_value = 'a'
FORMAT TSV

-- Result
10
```


Case 2: Calculate the intersection of two tags 'a' and 'b'.

```SQL
SELECT bitmapCardinality(bitmapColumnAnd(uids)) AS card
FROM test.bitmap_test
WHERE (tag_value IN ('a', 'b')) AND (slice_id = 0)
FORMAT CSV

-- Result
10

-- It is equivalent to the calculation of bitmapCardinality(bitmapColumnAnd).
SELECT bitmapCount('1&2')(multiIf(tag_value = 'a', toInt32(1), tag_value = 'b', 2, toInt32(999)) AS idx, uids) AS card
FROM test.bitmap_test
WHERE (tag_value IN ('a', 'b')) AND (slice_id = 0)
FORMAT TSV

-- Result
3

-- Another way of writing the above SQL, which is suitable for nested complex SQL
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

-- Result
3
```


Case 3: More complex intersection, union, and difference operations for multiple tags.

```SQL
-- Option 1
SELECT bitmapCount('1&2|3')(multiIf(tag_value = 'a', toInt32(1), tag_value = 'b', toInt32(2), tag_value = 'c', toInt32(3), toInt32(999)) AS idx, uids) AS card
FROM test.bitmap_test
FORMAT TSV

-- Result
11

-- Option 2: Since the tag_value is exactly of the string type, a string expression can be used
SELECT bitmapCount('a&b|c')(tag_value, uids)
FROM test.bitmap_test
FORMAT TSV

-- Result
11
```


<span id="6e66c28f"></span>
### bitmapExtract

This function calculates in the same way as bitmapCount, the difference is that it **returns the bitmap of the calculation result**, not just the count.

The way tags are combined is the same as in the bitmapCount function. bitmapCount used tag_value as an example; here, we present a case using tag_id as an example: Calculate the intersection of two tags:

```SQL
SELECT bitmapExtract('1&2')(multiIf(tag_id = 11, toInt32(1), tag_id = 12, 2, toInt32(999)) AS idx, uids) AS card
FROM test.bitmap_test
WHERE (tag_id IN (1,2)) AND (slice_id = 0)
FORMAT TSV

-- Result (no intersection)
{}

Another option:
SELECT bitmapExtract('11&12')(tag_id, uids)
FROM test.bitmap_test
WHERE (tag_id IN (1, 2)) AND (slice_id = 0)
FORMAT TSV

-- Result (no intersection)
{}
```


<span id="f3fbe1ac"></span>
### bitmapMultiCount function

This aggregate function, building on bitmapCount, **supports multiple sets of expressions**.

**Purpose:**  To perform complex union, intersection, and difference operations among multiple bitmaps, also supporting multiple operations and operation reusability. Users express the operations on bitmaps through input expressions, and the function performs the corresponding calculations after parsing. See the example in the previous section "Aggregate Functions" \- "Advanced Aggregate Functions" for a visual illustration.

**Input:**  ID column, bitmap column. Identification columns are used to identify bitmaps, which can be fields in a table (like tag_id) or manually defined variables (like idx).

**Expression:**  An identification anchors a bitmap. Identification expressions operate with and, or, and difference actions, corresponding to bitmap's intersect, union, and difference calculations. Multiple expressions can also be provided; the function executes the corresponding calculations sequentially, returning all results together.

Supported identification operators:


* OR operation: use a comma ('1,2') or a vertical line ('1|2')

* AND operation: use an ampersand ('1&2')

* Difference set operation: use a tilde ('1~2')

* Expression reuse: reuse a specific expression's result by using an underline followed by a position number. For example, "_3" indicates reusing the third expression (counting starts at one).


Output: **The result** of the bitmap after the bitmap union, intersection, and difference calculations is the number of elements in the bitmap. Each expression corresponds to a result, stored in the array.

```SQL
-- '_3|3' equals with '(1&2)|3'
SELECT bitmapMultiCount('1', '2', '1&2', '_3|3')(multiIf(tag_value = 'a', toInt32(1), tag_value = 'b', toInt32(2), tag_value = 'c', toInt32(3), toInt32(999)) AS idx, uids) AS card
FROM test.bitmap_test
WHERE slice_id = 0
FORMAT TSV

-- Result
[5,6,3,6]

-- tag_value is a string type, so a string expression can also be used.
SELECT bitmapMultiCount('a', 'b', 'a&b', '_3|c')(tag_value, uids) AS card
FROM test.bitmap_test
WHERE slice_id = 0
FORMAT TSV

-- Result
[5,6,3,6]
```


`_3` means reusing the expression at position 3, that is '1&2'.

There is a set of collection relationships that can be verified for correctness. I'm sorry, there is no content to translate

A + B = AUB + A AND B

```SQL
SELECT bitmapMultiCount('1', '2', '1&2', '1|2')(multiIf(tag_value = 'a', toInt32(1), tag_value = 'b', toInt32(2), tag_value = 'c', toInt32(3), toInt32(999)) AS idx, uids) AS card
FROM test.bitmap_test
WHERE slice_id = 0
FORMAT TSV

-- Result
[5,6,3,8]

-- tag_value is a string type, so a string expression can also be used.
SELECT bitmapMultiCount('a', 'b', 'a&b', 'a|b')(tag_value, uids)
FROM test.bitmap_test
WHERE slice_id = 0
FORMAT TSV

-- Result
[5,6,3,8]
```


<span id="dacb4e1c"></span>
### bitmapMultiExtract

The difference between including the user and bitmapMultiCount lies in the return value, returning bitmap data.

```SQL
SELECT bitmapMultiExtract('1', '2', '1&2', '1|2')(multiIf(tag_value = 'a', toInt32(1), tag_value = 'b', toInt32(2), tag_value = 'c', toInt32(3), toInt32(999)) AS idx, uids) AS card
FROM test.bitmap_test
WHERE slice_id = 0
FORMAT TSV

[{1,2,3,4,5},{3,4,5,6,7,8},{3,4,5},{1,2,3,4,5,6,7,8}]

-- tag_value is a string type, so a string expression can also be used.
SELECT bitmapMultiExtract('a', 'b', 'a&b', 'a|b')(tag_value, uids)
FROM test.bitmap_test
WHERE slice_id = 0
FORMAT TSV

-- Result
[{1,2,3,4,5},{3,4,5,6,7,8},{3,4,5},{1,2,3,4,5,6,7,8}]
```


<span id="75490630"></span>
### bitmapMultiCountWithDate

**Purpose:**  Based on bitmapMultiCount, this function adds a date dimension, enabling the differentiation of tags on different dates within the expression.

Note that the date column needs to be of the Int64 type. Generally, the date is of the Date type, and the toYYYYMMDD function should be used for conversion.

**Input:**  Date column, order number column, bitmap column.

**Expression:**  A date combined with an order number anchors a bitmap, which cannot be used alone. Therefore, `date_order number` is used as a whole, as in the example '20240101_1', to identify a bitmap. The function bitmapMultiCount only requires '1', highlighting the difference between the two.

**Output:**  The number of elements in the result bitmap after bitmap union, intersection, and difference operations. Each expression corresponds to a result stored in an array.

```SQL
SELECT bitmapMultiCountWithDate('20240101_1', '20240102_2', '20240101_1|20240102_2')(CAST(toYYYYMMDD(p_date), 'Int64') AS date1, multiIf((tag_value = 'a') AND (p_date = '2024-01-01'), toInt64(1), (tag_value = 'b') AND (p_date = '2024-01-02'), toInt64(2), (tag_value = 'c') and (p_date = '2024-01-01'), toInt64(3),toInt32(999)) AS idx, uids) AS card
FROM test.bitmap_test
FORMAT TSV

-- Result
[5,4,9]

-- tag_value is a string type, so a string expression can also be used.
SELECT bitmapMultiCountWithDate('20240101_a', '20240102_b', '20240101_a|20240102_b')(CAST(toYYYYMMDD(p_date), 'Int64') AS date1, tag_value, uids) AS card
FROM test.bitmap_test
FORMAT TSV

-- Result
[5,4,9]
```


<span id="880fc654"></span>
### bitmapMultiExtractWithDate

The function and usage are the same as bitmapMultiCountWithDate, with the difference being in the Return value, returning bitmap data.

```SQL
SELECT bitmapMultiExtractWithDate('20240101_1', '20240102_2', '20240101_1|20240102_2')(CAST(toYYYYMMDD(p_date), 'Int64') AS date1, multiIf((tag_value = 'a') AND (p_date = '2024-01-01'), toInt64(1), (tag_value = 'b') AND (p_date = '2024-01-02'), toInt64(2), (tag_value = 'c') and (p_date = '2024-01-01'), toInt64(3),toInt32(999)) AS idx, uids) AS card
FROM test.bitmap_test
FORMAT TSV

-- Result
[{1,2,3,4,5},{13,14,15,16},{1,2,3,4,5,13,14,15,16}]


-- tag_value is a string type, so a string expression can also be used.
SELECT bitmapMultiExtractWithDate('20240101_a', '20240102_b', '20240101_a|20240102_b')(CAST(toYYYYMMDD(p_date), 'Int64') AS date1, tag_value, uids) AS card
FROM test.bitmap_test
FORMAT TSV

-- Result
[{1,2,3,4,5},{13,14,15,16},{1,2,3,4,5,13,14,15,16}]
```
