---
title: "covarPop"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/covarpop-function"
---

<span id="06ef173a"></span>
# covarPop
**Syntax**
```SQL
covarPop(x, y)
```

Calculate the value of `Σ((x - x̅)(y - y̅)) / n`.
:::warning
This function uses an algorithm that is not numerically stable. If you need [numerical stability](https://en.wikipedia.org/wiki/Numerical_stability) in computation, use `covarPopStable` function. It works slower, but provides lower computational errors.
:::
