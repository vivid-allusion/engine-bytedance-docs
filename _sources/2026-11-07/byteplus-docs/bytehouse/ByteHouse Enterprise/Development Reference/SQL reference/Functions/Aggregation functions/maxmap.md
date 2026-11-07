---
title: "maxmap"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/maxmap-function"
---

**Grammar**
```sql
maxMap(key, value)
 or
maxMap(Tuple(key, value))
```

According to `Key`, calculate the maximum value for the `Value` array based on the specified keys.
Passing a tuple consisting of `Key` and `Value` arrays is synonymous with passing two separate arrays of `Key` and `Value`.
The quantity of `Key` and `Value` (array) elements in each total row must be identical.
Returns a tuple of the two arrays: sorted Key and the corresponding Key's calculated value (Maximum).
Example
```sql
SELECT maxMap(a, b)
FROM values('a Array(Int32), b Array(Int64)', ([1, 2], [2, 2]), ([2, 3], [1, 1]))
```

```text
┌─maxMap(a, b)──────┐
│ ([1,2,3],[2,2,1]) │
└───────────────────┘
```
