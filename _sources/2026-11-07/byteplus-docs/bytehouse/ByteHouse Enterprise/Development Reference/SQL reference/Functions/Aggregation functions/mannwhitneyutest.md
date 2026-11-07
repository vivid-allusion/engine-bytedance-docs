---
title: "mannwhitneyutest"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/mannwhitneyutest-function"
---

Apply the Mann-Whitney rank test to the samples of two populations.
**Grammar**
```sql
mannWhitneyUTest[(alternative[, continuity_correction])](sample_data, sample_index)
```

Values of both samples are in the `sample_data` column. If `sample_index` equals 0, then the values belong to the sample of the first population. Otherwise, they belong to the sample of the second population.
The null hypothesis is that both populations are randomly equal. It's also possible to test a one-sided hypothesis. This test does not assume that the data has a normal Distribution.
**Param**
`Sample data` — Sample data. Integer, Float or Decimal.
`Sample index` — Sample index. Integer.
**Param**
`Alternative` — Alternative hypothesis. (Optional, default is: `'two-sided'`.) String.
`'two-sided'`;
`'greater'`;
`'less'`。
`continuity_correction` — If not zero, a continuity adjustment is applied for normal approximation of the P-value. (Optional, default: 1) UInt64.
**Return value**
Tuple containing two elements:

* Calculates the U-statistic. Float64。
* Calculated P-value. Float64。

**Example**
Input table:
```text
┌─sample_data─┬─sample_index─┐
│          10 │            0 │
│          11 │            0 │
│          12 │            0 │
│           1 │            1 │
│           2 │            1 │
│           3 │            1 │
└─────────────┴──────────────┘
```

Search:
```sql
SELECT mannWhitneyUTest('greater')(sample_data, sample_index) FROM mww_ttest;
```

As a result:
```text
┌─mannWhitneyUTest('greater')(sample_data, sample_index)─┐
│ (9,0.04042779918503192)                                │
└────────────────────────────────────────────────────────┘
```

**See**
[Mann–Whitney U test](https://en.wikipedia.org/wiki/Mann%E2%80%93Whitney_U_test)
[Stochastic ordering](https://en.wikipedia.org/wiki/Stochastic_ordering)
