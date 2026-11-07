---
title: "covarSamp"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/covarsamp-function"
---

<span id="f856c25d"></span>
# <span style="background-color: rgb(255, 255, 255)">covarSamp</span>
<span style="background-color: rgb(255, 255, 255)"><strong>Grammar</strong></span>
covarSamp(x, y)
<span style="background-color: rgb(255, 255, 255)">Calculate </span>`Σ((x - x̅)(y - y̅)) / (n - 1)`<span style="background-color: rgb(255, 255, 255)"> value.</span>
<span style="background-color: rgb(255, 255, 255)">Returns Float64.</span> <span style="background-color: rgb(255, 255, 255)">When </span>`n <= 1`<span style="background-color: rgb(255, 255, 255)">, returns +∞.</span>
:::warning
This function uses a numerically unstable algorithm. If you need [numerical stability](https://en.wikipedia.org/wiki/Numerical_stability) in calculating, use `covarSampStable` function. Its working speed is slow, but it provides lower computational errors.
:::
