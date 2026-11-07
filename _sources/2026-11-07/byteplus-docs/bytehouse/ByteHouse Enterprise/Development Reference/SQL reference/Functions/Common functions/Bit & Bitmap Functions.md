---
title: "Bit & Bitmap Functions"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/bit-and-bitmap-functions"
---

:::warning
This function is not applicable to ByteHouse's proprietary BitEngine Type; for details, please refer to [BitEngine Function](/docs/bytehouse/46748).
:::
Bitmap functions are used to compute between two bitmap objects, returning a bitmap object for any such function, including operations like and, or, xor, not, etc.
There are two construction methods for bitmap objects. One is constructed by the aggregate function groupBitmapState, and the other is constructed from an Array Object. Bitmap objects can also be converted into array objects.
We use RoaringBitmap to store bitmap objects; when the cardinality is less than or equal to 32, it uses Set for storage. When the cardinality is greater than 32, it uses RoaringBitmap for storage. This is also why storage of low cardinality sets is faster.
For more information about RoaringBitmap, please see: [RoaringBitmap](https://github.com/RoaringBitmap/CRoaring).
<span id="bitmapbuild"></span>
## bitmapBuild
Build a bitmap object from an unsigned integer array.
```plaintext
bitmapBuild(array)
```

Parameters

* `array` - Unsigned integer array.

Example
SELECT bitmapBuild([1, 2, 3, 4, 5]) AS res
<span id="bitmaptoarray"></span>
## bitmapToArray
Convert a bitmap into an integer array.
```plaintext
bitmapToArray(bitmap)
```

Parameters

* `bitmap` - Bitmap object.

Example
SELECT bitmapToArray(bitmapBuild([1, 2, 3, 4, 5])) AS res
```plaintext
┌─res─────────┐
│ [1,2,3,4,5] │
└─────────────┘
```

<span id="bitmapsubsetinrange"></span>
## bitmapSubsetInRange
Convert the specified range of a bitmap (excluding range_end) into another bitmap.
```plaintext
bitmapSubsetInRange(bitmap, range_start, range_end)
```

Parameters

* `bitmap` – Bitmap object.
* `range_start` – Start point of the range (inclusive).
* `range_end` – End point of the range (exclusive).

Example
SELECT bitmapToArray(bitmapSubsetInRange(bitmapBuild([0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,100,200,500]), toUInt32(30), toUInt32(200))) AS res
```plaintext
┌─res───────────────┐
│ [30,31,32,33,100] │
└───────────────────┘
```

<span id="bitmapsubsetlimit"></span>
## bitmapSubsetLimit
Convert a specified range (start point and upper limit) of the bitmap into another bitmap.
```plaintext
bitmapSubsetLimit(bitmap, range_start, limit)
```

Parameters

* `bitmap` – Bitmap object.
* `range_start` – Start point of the range (inclusive).
* `limit` – Upper limit for the subset bitmap.

Example
SELECT bitmapToArray(bitmapSubsetLimit(bitmapBuild([0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,100,200,500]), toUInt32(30), toUInt32(200))) AS res
```plaintext
┌─res───────────────────────┐
│ [30,31,32,33,100,200,500] │
└───────────────────────────┘
```

<span id="bitmapcontains"></span>
## bitmapContains
Check if the bitmap contains the specified element.
```plaintext
bitmapContains(haystack, needle)
```

Parameter

* `Haystack` – Bitmap object.
* `Needle` – Element, type UInt32.

Example
SELECT bitmapContains(bitmapBuild([1,5,7,9]), toUInt32(9)) AS res
```plaintext
┌─res─┐
│  1  │
└─────┘
```

<span id="bitmaphasany"></span>
## bitmapHasAny
Similar to `hasAny(array, array)`, returns 1 if the bitmap has any common elements, otherwise returns 0. For an empty bitmap, returns 0.
```plaintext
bitmapHasAny(bitmap,bitmap)
```

Parameter

* `Bitmap` – bitmap object.

Example
SELECT bitmapHasAny(bitmapBuild([1,2,3]),bitmapBuild([3,4,5])) AS res
```plaintext
┌─res─┐
│  1  │
└─────┘
```

<span id="bitmaphasall"></span>
## bitmapHasAll
Similar to `hasAll(array, array)`, this returns 1 if the first bitmap contains all elements of the second bitmap, otherwise it returns 0. If the second parameter is an empty bitmap, it returns 1.
```plaintext
bitmapHasAll(bitmap,bitmap)
```

Parameters

* `bitmap` – bitmap object.

Example
SELECT bitmapHasAll(bitmapBuild([1,2,3]),bitmapBuild([3,4,5])) AS res
```plaintext
┌─res─┐
│  0  │
└─────┘
```

<span id="位图和"></span>
## Bitmap and
Performs an AND operation on two bitmap objects and returns a new bitmap object.
```plaintext
bitmapAnd(bitmap1,bitmap2)
```

Parameters

* `bitmap1` – Bitmap object.
* `bitmap2` – Bitmap object.

Example
SELECT bitmapToArray(bitmapAnd(bitmapBuild([1,2,3]),bitmapBuild([3,4,5]))) AS res
```plaintext
┌─res─┐
│ [3] │
└─────┘
```

<span id="位图或"></span>
## Bitmap OR
Performs an OR operation on two bitmap objects and returns a new bitmap object.
```plaintext
bitmapOr(bitmap1,bitmap2)
```

Parameters

* `bitmap1` – Bitmap object.
* `bitmap2` – Bitmap object.

Example
SELECT bitmapToArray(bitmapOr(bitmapBuild([1,2,3]),bitmapBuild([3,4,5]))) AS res
```plaintext
┌─res─────────┐
│ [1,2,3,4,5] │
└─────────────┘
```

<span id="bitmapxor"></span>
## bitmapXor
Performs an XOR operation on two bitmap objects, returning a new bitmap object.
```plaintext
bitmapXor(bitmap1,bitmap2)
```

Parameters

* `bitmap1` – Bitmap object.
* `bitmap2` – Bitmap object.

Example
SELECT bitmapToArray(bitmapXor(bitmapBuild([1,2,3]),bitmapBuild([3,4,5]))) AS res
```plaintext
┌─res───────┐
│ [1,2,4,5] │
└───────────┘
```

<span id="bitmapandnot"></span>
## bitmapAndnot
Calculate the difference between two bitmaps and return a new bitmap object.
```plaintext
bitmapAndnot(bitmap1,bitmap2)
```

Parameters

* `bitmap1` – Bitmap object.
* `bitmap2` – Bitmap object.

Example
SELECT bitmapToArray(bitmapAndnot(bitmapBuild([1,2,3]),bitmapBuild([3,4,5]))) AS res
```plaintext
┌─res───┐
│ [1,2] │
└───────┘
```

<span id="bitmapcardinality"></span>
## bitmapCardinality
Returns a UInt64 type number indicating the cardinality of the bitmap object.
```plaintext
bitmapCardinality(bitmap)
```

Parameters

* `bitmap` – Bitmap object.

Example
SELECT bitmapCardinality(bitmapBuild([1, 2, 3, 4, 5])) AS res
```plaintext
┌─res─┐
│   5 │
└─────┘
```

<span id="bitmapmin"></span>
## bitmapMin
Returns a UInt64 value indicating the minimum value in the bitmap. If the bitmap is empty, returns UINT32_MAX.
```plaintext
bitmapMin(bitmap)
```

Parameter

* `bitmap` – Bitmap object.

Example
SELECT bitmapMin(bitmapBuild([1, 2, 3, 4, 5])) AS res
```plaintext
┌─res─┐
│   1 │
└─────┘
```

<span id="bitmapmax"></span>
## bitmapMax
Returns a UInt64 Type number representing the Maximum value in the bitmap. If the bitmap is Empty, returns 0.
```plaintext
bitmapMax(bitmap)
```

Param

* `bitmap` – bitmap object.

Example
SELECT bitmapMax(bitmapBuild([1, 2, 3, 4, 5])) AS res
```plaintext
┌─res─┐
│   5 │
└─────┘
```

<span id="位图和标准性"></span>
## Bitmap and Standardization
Performs an AND operation on two bitmap objects and returns the cardinality of the result bitmap.
```plaintext
bitmapAndCardinality(bitmap1,bitmap2)
```

Param

* `bitmap1` – Bitmap object.
* `bitmap2` – Bitmap object.

Example
SELECT bitmapAndCardinality(bitmapBuild([1,2,3]),bitmapBuild([3,4,5])) AS res;
```plaintext
┌─res─┐
│   1 │
└─────┘
```

<span id="bitmaporcardinality"></span>
## bitmapOrCardinality
Performs an 'or' operation on two bitmap objects, returning the cardinality of the resulting bitmap.
```plaintext
bitmapOrCardinality(bitmap1,bitmap2)
```

Parameter

* `bitmap1` – Bitmap object.
* `bitmap2` – Bitmap object.

Example
SELECT bitmapOrCardinality(bitmapBuild([1,2,3]),bitmapBuild([3,4,5])) AS res;
```plaintext
┌─res─┐
│   5 │
└─────┘
```

<span id="bitmapxorcardinality"></span>
## bitmapXorCardinality
Perform an XOR operation on two bitmaps and return the cardinality of the resulting bitmap.
```plaintext
bitmapXorCardinality(bitmap1,bitmap2)
```

Param

* `bitmap1` – Bitmap object.
* `bitmap2` – Bitmap object.

Example
SELECT bitmapXorCardinality(bitmapBuild([1,2,3]),bitmapBuild([3,4,5])) AS res;
```plaintext
┌─res─┐
│   4 │
└─────┘
```

<span id="位图和非标准性-bitmapandnotcardinality"></span>
## Bitmap and Non-standardness
Calculate the difference between two bitmaps and return the cardinality of the resulting bitmap.
```plaintext
bitmapAndnotCardinality(bitmap1,bitmap2)
```

Param

* `bitmap1` - Bitmap object.
* `bitmap2` - Bitmap object.

Example
SELECT bitmapAndnotCardinality(bitmapBuild([1,2,3]),bitmapBuild([3,4,5])) AS res;
```plaintext
┌─res─┐
│   2 │
└─────┘
```
