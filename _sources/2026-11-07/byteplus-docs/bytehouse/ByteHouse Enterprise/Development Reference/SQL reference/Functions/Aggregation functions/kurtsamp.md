---
title: "kurtsamp"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/kurtsamp-function"
---

Calculate the [kurtosis sample](https://en.wikipedia.org/wiki/Kurtosis) for the given sequence.
It represents the unbiased estimate of the random variable's kurtosis if the passed values form its sample.
**Syntax**
```sql
kurtSamp(expr)
```

**Parameters**
`expr` — an expression that results in a number.
**Return value**
The kurtosis of the given sequence. Type — Float64. If `n <= 1` (`n` is the sample size), then the function returns `nan`.
**Example**
```sql
SELECT kurtSamp(value) FROM series_with_value_column;
```
