---
title: "rankCorr"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/rankcorr-function"
---

Calculate the rank correlation coefficient.
**Syntax**
```sql
rankCorr(x, y)
```

**Param**
`x` - any value. Float32 or Float64.
`y` - any value. Float32 or Float64.
**Return value**
Returns the rank correlation coefficient of ranks for x and y. The range of correlation coefficients is from -1 to +1. If fewer than two parameters are passed, the function will return an exception. Values close to +1 indicate a high degree of linear relationship, where an increase in one random variable also increases the second random variable. Values close to -1 indicate a high degree of linear relationship, where an increase in one random variable decreases the second random variable. Values close to or equal to 0 indicate no relationship between the two random variables.
Type: Float64.
**Example**
Search:
```sql
SELECT rankCorr(number, number) FROM numbers(100);
```

Result:
```text
┌─rankCorr(number, number)─┐
│                        1 │
└──────────────────────────┘
```

Search:
```sql
SELECT roundBankers(rankCorr(exp(number), sin(number)), 3) FROM numbers(100);
```

As a result:
```text
┌─roundBankers(rankCorr(exp(number), sin(number)), 3)─┐
│                                              -0.037 │
└─────────────────────────────────────────────────────┘
```

**For more information, refer to** [Spearman's rank correlation coefficient](https://en.wikipedia.org/wiki/Spearman%27s_rank_correlation_coefficient).
