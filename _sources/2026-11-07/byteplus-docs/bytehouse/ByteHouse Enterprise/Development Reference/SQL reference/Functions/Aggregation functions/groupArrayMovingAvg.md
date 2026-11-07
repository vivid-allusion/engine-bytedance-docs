---
title: "groupArrayMovingAvg"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/grouparraymovingavg-function"
---

<span id="b27fa5c9"></span>
# groupArrayMovingAvg
Calculate the moving average of the input value.
**Grammar**
```SQL
groupArrayMovingAvg(numbers_for_summing)
groupArrayMovingAvg(window_size)(numbers_for_summing)
```

The function can take window size as a parameter. If not specified, the window size of the function equals the number of rows in the column.
**Param**

* `numbers_for_summing` — Expression generate numerical value data type values.
* `window_size` — Window size.

**Return value**

* An array of the same size as the input data.

For input data types Integer and floating-point, the corresponding return type is `Float64`. For input data types Decimal the return type is `Decimal128`.
This function uses rounding to zero for Decimal128.rounding to zero for Decimal128. It truncates meaningless decimal places to ensure the data type of the result.
**Example**
Sample table `t`:
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
    groupArrayMovingAvg(int) AS I,
    groupArrayMovingAvg(float) AS F,
    groupArrayMovingAvg(dec) AS D
FROM t
```

```Plain
┌─I────────────────────┬─F─────────────────────────────────────────────────────────────────────────────┬─D─────────────────────┐
│ [0.25,0.75,1.75,3.5] │ [0.2750000059604645,0.8250000178813934,1.9250000417232513,3.8499999940395355] │ [0.27,0.82,1.92,3.86] │
└──────────────────────┴───────────────────────────────────────────────────────────────────────────────┴───────────────────────┘
```

```SQL
SELECT
    groupArrayMovingAvg(2)(int) AS I,
    groupArrayMovingAvg(2)(float) AS F,
    groupArrayMovingAvg(2)(dec) AS D
FROM t
```

```Plain
┌─I───────────────┬─F───────────────────────────────────────────────────────────────────────────┬─D─────────────────────┐
│ [0.5,1.5,3,5.5] │ [0.550000011920929,1.6500000357627869,3.3000000715255737,6.049999952316284] │ [0.55,1.65,3.30,6.08] │
└─────────────────┴─────────────────────────────────────────────────────────────────────────────┴───────────────────────┘
```
