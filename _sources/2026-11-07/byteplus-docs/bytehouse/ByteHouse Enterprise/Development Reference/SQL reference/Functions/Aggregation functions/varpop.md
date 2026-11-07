---
title: "varpop"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/varpop-function"
---

Calculate `Σ((x - x̅)^2) / n`, where `n` is the sample size, and `x̅` is the mean of `x`.
In other words, calculate the deviation of a dataset. Return `Float64`.
:::warning
This function uses a numerically unstable algorithm. If you need [numerical stability](https://en.wikipedia.org/wiki/Numerical_stability) in calculations, use the `varPopStable` function. It operates slower but provides lower calculation errors.
:::
