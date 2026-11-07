---
title: "groupBitmapXor"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/groupbitmapxor-function"
---

<span id="1a1b203b"></span>
# groupBitmapXor
Calculate the XOR of bitmap columns, returning a UInt64 type value. If suffix State is added, it returns a bitmap object.
**Syntax**
```SQL
groupBitmapXor(expr)
```

**Parameters**
`expr` – an expression that yields a type of `AggregateFunction(groupBitmap, UInt*)`.
**Return Value**
Returns a value of type `UInt64`.
**Examples**
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

SELECT groupBitmapXor(z) FROM bitmap_column_expr_test2 WHERE like(tag_id, 'tag%');
┌─groupBitmapXor(z)─┐
│              10   │
└───────────────────┘

SELECT arraySort(bitmapToArray(groupBitmapXorState(z))) FROM bitmap_column_expr_test2 WHERE like(tag_id, 'tag%');
┌─arraySort(bitmapToArray(groupBitmapXorState(z)))─┐
│ [1,3,5,6,8,10,11,13,14,15]                       │
└──────────────────────────────────────────────────┘
```
