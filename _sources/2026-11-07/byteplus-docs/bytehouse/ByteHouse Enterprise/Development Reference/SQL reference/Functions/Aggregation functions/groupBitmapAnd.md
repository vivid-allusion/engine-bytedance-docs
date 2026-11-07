---
title: "groupBitmapAnd"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/groupbitmapand-function"
---

<span id="a1468630"></span>
# groupBitmapAnd
Calculate the column's `AND` and return a `UInt64` type of Value; if the suffix `State` is added, then return a bitmap object.
**Syntax**
```SQL
groupBitmapAnd(expr)
```

**Parameters**
`expr` – An Expression that results in an `AggregateFunction(groupBitmap, UInt*)` type.
**Return Value**
A `UInt64` type of Value.
**Example**
```SQL
DROP TABLE IF EXISTS bitmap_column_expr_test2;
CREATE TABLE bitmap_column_expr_test2
(
    tag_id String,
    z AggregateFunction(groupBitmap, UInt32)
)
ENGINE = MergeTree
ORDER BY tag_id;

INSERT INTO bitmap_column_expr_test2 VALUES ('tag1', bitmapBuild(cast([1,2,3,4,5,6,7,8,9,10] as Array(UInt32))));
INSERT INTO bitmap_column_expr_test2 VALUES ('tag2', bitmapBuild(cast([6,7,8,9,10,11,12,13,14,15] as Array(UInt32))));
INSERT INTO bitmap_column_expr_test2 VALUES ('tag3', bitmapBuild(cast([2,4,6,8,10,12] as Array(UInt32))));

SELECT groupBitmapAnd(z) FROM bitmap_column_expr_test2 WHERE like(tag_id, 'tag%');
┌─groupBitmapAnd(z)─┐
│               3   │
└───────────────────┘

SELECT arraySort(bitmapToArray(groupBitmapAndState(z))) FROM bitmap_column_expr_test2 WHERE like(tag_id, 'tag%');
┌─arraySort(bitmapToArray(groupBitmapAndState(z)))─┐
│ [6,8,10]                                         │
└──────────────────────────────────────────────────┘
```
