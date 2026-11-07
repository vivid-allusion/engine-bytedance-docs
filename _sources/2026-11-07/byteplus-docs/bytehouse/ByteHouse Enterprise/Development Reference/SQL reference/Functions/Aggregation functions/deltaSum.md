---
title: "deltaSum"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/deltasum-function"
---

Calculate the sum of differences between successive rows. If the difference is negative, ignore it.
**Syntax**
```SQL
deltaSum(value)
```

**Param**

* `value` — must be Integer or Float.

**Return value**

* `Integer` or `Float` sum of arithmetic differences.

**Example**
Search:
```SQL
SELECT deltaSum(arrayJoin([1, 2, 3]));
```

As a result
```Plain
┌─deltaSum(arrayJoin([1, 2, 3]))─┐
│                              2 │
└────────────────────────────────┘
```

Search
```SQL
SELECT deltaSum(arrayJoin([1, 2, 3, 0, 3, 4, 2, 3]));
```

As a result
```Plain
┌─deltaSum(arrayJoin([1, 2, 3, 0, 3, 4, 2, 3]))─┐
│                                             7 │
└───────────────────────────────────────────────┘
```

Search
```SQL
SELECT deltaSum(arrayJoin([2.25, 3, 4.5]));
```

As a result
```Plain
┌─deltaSum(arrayJoin([2.25, 3, 4.5]))─┐
│                                2.25 │
└─────────────────────────────────────┘
```
