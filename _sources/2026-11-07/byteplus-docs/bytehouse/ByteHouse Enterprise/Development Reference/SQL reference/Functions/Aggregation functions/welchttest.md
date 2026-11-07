---
title: "welchttest"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/welchttest-function"
---

Apply the Welch's t-test on the samples of two overall groups.
**Grammar**
```sql
welchTTest(sample_data, sample_index)
```

Values of both samples are in the `sample_data` column. If `sample_index` equals to 0, then the values in this row belong to the sample of the first overall group. Otherwise, it belongs to the sample of the second overall group.
The zero hypothesis is that the average of the groups are equal. Assumed to be normally distributed. The overall groups may have unequal variances.
**Param**
`sample_data` — Sample data. Integer, Float or Decimal.
`sample_index` — Sample index. Integer.
**Return value**

* Tuple, consists of two elements:
* Calculated T-statistic. Float64。
* Calculated P-value. Float64。

**Example**
Input table:
```text
┌─sample_data─┬─sample_index─┐
│        20.3 │            0 │
│        22.1 │            0 │
│        21.9 │            0 │
│        18.9 │            1 │
│        20.3 │            1 │
│          19 │            1 │
└─────────────┴──────────────┘
```

Search:
```sql
SELECT welchTTest(sample_data, sample_index) FROM welch_ttest;
```

As a result:
```text
┌─welchTTest(sample_data, sample_index)─────┐
│ (2.7988719532211235,0.051807360348581945) │
└───────────────────────────────────────────┘
```
