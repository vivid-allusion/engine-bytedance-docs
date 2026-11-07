---
title: "varsamp"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/varsamp-function"
---

Calculate `Σ((x - x̅)^2) / (n - 1)`, here `n` is the sample size, `x̅` is the average value of `x`.
It represents an unbiased estimate of the variance of the random variable if the passed values form its sample.
Return `Float64`. When `n <= 1`, return `+∞`.
:::warning
This function uses a numerically unstable algorithm. If you need numerical stability in computing, use the varSampStable function. It works slower but provides lower computational errors.
:::
