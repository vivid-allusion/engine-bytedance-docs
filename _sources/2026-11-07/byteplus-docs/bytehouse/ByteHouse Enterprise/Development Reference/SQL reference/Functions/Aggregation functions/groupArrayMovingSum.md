---
title: "groupArrayMovingSum"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/grouparraymovingsum-function"
---

<span id="da43ecc9"></span>
# groupArrayMovingSum
Calculate the moving sum of the input values.
**Syntax**
```SQL
groupArrayMovingSum(numbers_for_summing)groupArrayMovingSum(window_size)(numbers_for_summing)
```

This function can take the window size as a parameter. If not specified, the window size for this function equals to the number of rows in the column.
**Parameters**

* `numbers_for_summing` — Expression generates numerical data type values.
* `window_size` — Window size.

**Return value**

* An array of the same size as the input data. For input data of Decimal type, the element type is `Decimal128`. For other numerical types, obtain the corresponding `NearestFieldType`.

**Example**
Sample table:
```SQL
CREATE TABLE t
(
    `int` UInt8,
    `float` Float32,
    `dec` Decimal32(2)
)
ENGINE = TinyLog
```

```Plain
┌─int─┬─float─┬──dec─┐
│   1 │   1.1 │ 1.10 │
│   2 │   2.2 │ 2.20 │
│   4 │   4.4 │ 4.40 │
│   7 │  7.77 │ 7.77 │
└─────┴───────┴──────┘
```

Search:
```SQL
SELECT
    groupArrayMovingSum(int) AS I,
    groupArrayMovingSum(float) AS F,
    groupArrayMovingSum(dec) AS D
FROM t
```

```Plain
┌─I──────────┬─F───────────────────────────────┬─D──────────────────────┐
│ [1,3,7,14] │ [1.1,3.3000002,7.7000003,15.47] │ [1.10,3.30,7.70,15.47] │
└────────────┴─────────────────────────────────┴────────────────────────┘
```

```SQL
SELECT
    groupArrayMovingSum(2)(int) AS I,
    groupArrayMovingSum(2)(float) AS F,
    groupArrayMovingSum(2)(dec) AS D
FROM t
```

```Plain
┌─I──────────┬─F───────────────────────────────┬─D──────────────────────┐
│ [1,3,6,11] │ [1.1,3.3000002,6.6000004,12.17] │ [1.10,3.30,6.60,12.17] │
└────────────┴─────────────────────────────────┴────────────────────────┘
```
