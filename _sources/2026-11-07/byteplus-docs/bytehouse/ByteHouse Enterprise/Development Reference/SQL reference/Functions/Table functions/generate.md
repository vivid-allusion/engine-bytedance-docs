---
title: "generate"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/generate-function"
---

Generate random data using a given pattern.
Allows you to fill test tables with data.
Supports all data types that can be stored in the table, except for `LowCardinality` and `AggregateFunction`.
```sql
generateRandom('name TypeName[, name TypeName]...', [, 'random_seed'[, 'max_string_length'[, 'max_array_length']]]);
```

**Param**
`Name` — Name of the corresponding column.
`TypeName` — Type of the corresponding column.
`max_array_length` — Maximum length for generating arrays. Default is 10.
`max_string_length` — Maximum length for generating strings. Default is Oct.
`random_seed` — Manually specify a random seed to generate stable results. If it is NULL, the seed is randomly generated.
**Return value**
A table object with the requested mode.
**Usage example**
```sql
SELECT * FROM generateRandom('a Array(Int8), d Decimal32(4), c Tuple(DateTime64(3), UUID)', 1, 10, 2) LIMIT 3;
```

```text
┌─a────────┬────────────d─┬─c──────────────────────────────────────────────────────────────────┐
│ [77]     │ -124167.6723 │ ('2061-04-17 21:59:44.573','3f72f405-ec3e-13c8-44ca-66ef335f7835') │
│ [32,110] │ -141397.7312 │ ('1979-02-09 03:43:48.526','982486d1-5a5d-a308-e525-7bd8b80ffa73') │
│ [68]     │  -67417.0770 │ ('2080-03-12 14:17:31.269','110425e5-413f-10a6-05ba-fa6b3e929f15') │
└──────────┴──────────────┴────────────────────────────────────────────────────────────────────┘
```
