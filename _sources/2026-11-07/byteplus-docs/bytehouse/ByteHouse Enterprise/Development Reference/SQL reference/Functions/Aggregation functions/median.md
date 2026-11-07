---
title: "median"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/median-function"
---

<span id="median {#median}"></span>
# median {#median}
`median*` is an `quantile*` alias. They calculate the median of numerical data samples.
Functions:

* `median` — quantile alias.
* `medianDeterministic` — quantileDeterministic alias.
* `medianExact` — quantileExact alias.
* `medianExactWeighted` — quantileExactWeighted alias.
* `medianTiming` — quantileTiming alias.
* `medianTimingWeighted` is an alias for quantileTimingWeighted.
* `medianTDigest` is an alias for quantileTDigest.
* `medianTDigestWeighted` is an alias for quantileTDigestWeighted.

**Example**
Input table:
```text
┌─val─┐
│   1 │
│   1 │
│   2 │
│   3 │
└─────┘
```

Search:
```sql
SELECT medianDeterministic(val, 1) FROM t
```

As a result:
```text
┌─medianDeterministic(val, 1)─┐
│                         1.5 │
└─────────────────────────────┘
```
