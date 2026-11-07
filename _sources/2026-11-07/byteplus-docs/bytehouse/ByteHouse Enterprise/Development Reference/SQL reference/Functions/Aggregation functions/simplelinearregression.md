---
title: "simplelinearregression"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/simplelinearregression-function"
---

Run one-dimensional linear regression.
**Syntax**
```sql
simpleLinearRegression(x, y)
```

**Parameters**
`x` — x-axis.
`y` — y-axis.
**Return value**
Constants `y = a*x + b` that meet expectation `(a, b)`.
**Example**
```sql
SELECT arrayReduce('simpleLinearRegression', [0, 1, 2, 3], [0, 1, 2, 3])
```

```text
┌─arrayReduce('simpleLinearRegression', [0, 1, 2, 3], [0, 1, 2, 3])─┐
│ (1,0)                                                             │
└───────────────────────────────────────────────────────────────────┘
```

```sql
SELECT arrayReduce('simpleLinearRegression', [0, 1, 2, 3], [3, 4, 5, 6])
```

```text
┌─arrayReduce('simpleLinearRegression', [0, 1, 2, 3], [3, 4, 5, 6])─┐
│ (1,3)                                                             │
└───────────────────────────────────────────────────────────────────┘
```
