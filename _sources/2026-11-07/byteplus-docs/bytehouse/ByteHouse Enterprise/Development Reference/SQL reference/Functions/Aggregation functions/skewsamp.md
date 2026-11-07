---
title: "skewsamp"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/skewsamp-function"
---

Calculate the [sample skewness] of a given sequence (https://en.wikipedia.org/wiki/Skewness).
If the values passed form its sample, it represents an unbiased estimate of the skewness of a random variable.
**Syntax**
```sql
skewSamp(expr)
```

**Parameter**
`expr` — Expression returns a Number.
**Return value**
Skewness of the given distribution. Type — Float64. If `n <= 1` (`n` Size of the sample), the function returns `nan`.
**Example**
```sql
SELECT skewSamp(value) FROM series_with_value_column;
```
