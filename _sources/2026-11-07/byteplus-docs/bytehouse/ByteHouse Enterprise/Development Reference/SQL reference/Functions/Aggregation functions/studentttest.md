---
title: "studentttest"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/studentttest-function"
---

Apply a T-test to samples from two populations.
**Grammar**
```sql
studentTTest(sample_data, sample_index)
```

Values for both samples are `sample_data` in the column. If `sample_index` equals 0, the value is from the sample of the first population. Otherwise, it belongs to the second population.
The null hypothesis is that the means of the populations are equal. The assumption is a normal distribution with equal variances.
**Parameter**
`sample_data` — Sample data. Integer, Float or Decimal.
`sample_index` — sample index. Integer。
**Return value**
Tuple, with two elements:
Calculated T-statistic. Float64。
Calculated P-value. Float64。
**Example**
Input table:
```text
┌─sample_data─┬─sample_index─┐
│        20.3 │            0 │
│        21.1 │            0 │
│        21.9 │            1 │
│        21.7 │            0 │
│        19.9 │            1 │
│        21.8 │            1 │
└─────────────┴──────────────┘
```

Search:
```sql
SELECT studentTTest(sample_data, sample_index) FROM student_ttest;
```

As a result:
```text
┌─studentTTest(sample_data, sample_index)───┐
│ (-0.21739130434783777,0.8385421208415731) │
└───────────────────────────────────────────┘
```
