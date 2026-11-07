---
title: "corr"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/corr-function"
---

<span id="9cacb305"></span>
# corr
**Grammar**
```SQL
`corr(x, y)`
```

Calculate the Pearson correlation coefficient: `Σ((x - x̅)(y - y̅)) / sqrt(Σ((x - x̅)^2) * Σ((y - y̅)^2))`.
:::warning
This function uses an algorithm that is not numerically stable. If you need [numerical stability](https://en.wikipedia.org/wiki/Numerical_stability) in the calculating process, use `corrStable` function. Its operation is slower, but it provides reduced calculation errors.
:::
