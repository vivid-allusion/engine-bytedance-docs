---
title: "kurtpop"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/kurtpop-function"
---

Calculate the [kurtosis](https://en.wikipedia.org/wiki/Kurtosis) of the given sequence.
**Syntax**
```sql
kurtPop(expr)
```

**Param**
`expr` — An expression that yields a number.
**Return value**
Kurtosis of the given distribution. Type — Float64
**Example**
```sql
SELECT kurtPop(value) FROM series_with_value_column;
```
