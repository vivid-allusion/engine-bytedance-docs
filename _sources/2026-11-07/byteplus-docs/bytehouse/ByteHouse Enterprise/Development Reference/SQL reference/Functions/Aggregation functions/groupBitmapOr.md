---
title: "groupBitmapOr"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/groupbitmapor-function"
---

<span id="c4f9b3e1"></span>
# groupBitmapOr
Calculate the `OR` of bitmap columns, return `UInt64` type cardinality; if you add the suffix `State`, it returns a bitmap object.
**Syntax**
```SQL
groupBitmapOr(expr)
```

**Parameters**
`expr` – An expression of type `AggregateFunction(groupBitmap, UInt*)`.
**Return value**
A value of type `UInt64`.
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

SELECT groupBitmapOr(z) FROM bitmap_column_expr_test2 WHERE like(tag_id, 'tag%');
┌─groupBitmapOr(z)─┐
│             15   │
└──────────────────┘

SELECT arraySort(bitmapToArray(groupBitmapOrState(z))) FROM bitmap_column_expr_test2 WHERE like(tag_id, 'tag%');
┌─arraySort(bitmapToArray(groupBitmapOrState(z)))─┐
│ [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15]           │
└─────────────────────────────────────────────────┘
```
