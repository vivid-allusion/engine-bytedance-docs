---
title: "minmap"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/minmap-function"
---

**Syntax**
```sql
minMap(key, value)
or
minMap(Tuple(key, value))
```

Calculate the minimum based on the specified keys in the `Key` array and `value` array.
Passing a tuple of `Key` and `value` arrays is synonymous with passing two separate arrays of `Key` and `value`.
The number of `Key` and `value` elements in each row to be totaled must be the same.
Return a tuple of two arrays: the sorted `Key` and the corresponding `Key`'s `value` calculated (minimum).
**Example**
```sql
SELECT minMap(a, b)
FROM values('a Array(Int32), b Array(Int64)', ([1, 2], [2, 2]), ([2, 3], [1, 1]))
```

```text
┌─minMap(a, b)──────┐
│ ([1,2,3],[2,1,1]) │
└───────────────────┘
```
