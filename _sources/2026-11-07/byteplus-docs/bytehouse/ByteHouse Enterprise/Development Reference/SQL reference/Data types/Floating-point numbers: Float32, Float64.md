---
title: "Floating-point numbers: Float32, Float64"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/floating-point-numbers"
---

Floating-point number type.
Alias:

* `Float32` — `FLOAT`.
* `Float64` — `DOUBLE`.

:::warning
When creating a table, you can set parameters for floating-point numbers (e.g., FLOAT(12), FLOAT(15, 22), DOUBLE(12), DOUBLE(4, 18)), but ByteHouse will ignore them.
:::
<span id="cc358c15"></span>
## Use floating-point numbers

* Calculations with floating-point numbers may cause rounding errors.

```SQL
SELECT 1 - 0.9
```

```Plain
┌───────minus(1, 0.9)─┐
│ 0.09999999999999998 │
└─────────────────────┘
```


* The result of the calculation depends on the computing method (processor type and architecture of the computer system)
* Floating-point calculation results may be something like infinity (`INF`) and "not a number" (`NaN`). When calculating floating-point numbers, this should be taken into account.
* When reading floating-point numbers line by line, the result may not be the closest numerical value displayed by the machine.

<span id="0cb564c2"></span>
## NaN and Inf
Compared to standard SQL, ByteHouse supports the following categories of floating-point numbers:

* `Inf` - positive infinity

```SQL
SELECT 0.5 / 0
```

```Plain
┌─divide(0.5, 0)─┐
│            inf │
└────────────────┘
```


* `-Inf` - negative infinity

```SQL
SELECT -0.5 / 0
```

```Plain
┌─divide(-0.5, 0)─┐
│            -inf │
└─────────────────┘
```


* `NaN` - not a number

```Plain
┌─divide(0, 0)─┐
│          nan │
└──────────────┘
```

You can view more rules about NaN sorting in the ORDER BY cl`NaN sorting in the ORDER BY clause`.
