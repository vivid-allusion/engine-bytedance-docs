---
title: "skewpop"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/skewpop-function"
---

Calculate the skewness of a given sequence (https://en.wikipedia.org/wiki/Skewness).
**Syntax**
```sql
skewPop(expr)
```

**Param**
`expr` — Expression returns a Number.
**Return value**
Skewness of the given Distribution. Type — Float64
**Example**
```sql
SELECT skewPop(value) FROM series_with_value_column;
```
