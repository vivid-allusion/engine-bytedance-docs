---
title: "Fixed-point types: Decimal(P,S), Decimal32(S), Decimal64(S), Decimal128(S)"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/fixed-point-types"
---

Signed fixed-point numbers maintain precision during addition, subtraction, and multiplication operations. For division, the least significant digits are discarded (not rounded).
<span id="9a6a7592"></span>
## Parameter

* P - Precision. Valid range: [1:38], determines how many decimal digits can exist (including fractions).
* S - Scale. Valid range: [0:P], determines the number of decimal places in the decimal part of the number.

Decimal(P) is equivalent to Decimal(P, 0). Similarly, the syntax Decimal is equivalent to Decimal(10, 0).
For different values of the P parameter in Decimal representation, the following examples are synonymous:

* P in [1:9] corresponds with Decimal32(S)
* P in [10:18] corresponds with Decimal64(S)
* P in [19:38] corresponds with Decimal128(S)

<span id="f5fdb351"></span>
## Decimal value range

* Decimal32(S) - ( -1 * 10^(9 - S), 1 * 10^(9 - S) )
* Decimal64(S) - ( -1 * 10^(18 - S), 1 * 10^(18 - S) )
* Decimal128(S) - ( -1 * 10^(38 - S), 1 * 10^(38 - S) )

For example, Decimal32(4) can represent numerical values from -99999.9999 to 99999.9999, with a step size of 0.0001.
<span id="010e1d39"></span>
## Internal representation method
Data uses signed integers of the same bit-width for storage. The actual range of this number in memory is higher than stated above, and corresponding checks are conducted when converting from String to decimal numbers.
Since modern CPUs do not support 128-bit numbers, operations on Decimal128 are simulated by software. Therefore, computation speed on Decimal128 is significantly slower than that of Decimal32/Decimal64.
<span id="27cae829"></span>
## Computation and result type
Binary operations on Decimal result in a wider result type regardless of the order of parameters.

* `Decimal64(S1)Decimal32(S2) -> Decimal64(S)`
* `Decimal128(S1)Decimal32(S2) -> Decimal128(S)`
* `Decimal128(S1)Decimal64(S2) -> Decimal128(S)`

Rules of precision change:

* Addition, subtraction: S = max(S1, S2).
* Multiplication: S = S1 + S2.
* Division: S = S1.

For similar calculations between Decimals and integers, the result is a Decimal of the same size as the parameters.
Operations between Decimal and Float32/Float64 are undefined. If such operations need to be performed, you can use toDecimal32, toDecimal64, toDecimal128, or toFloat32, toFloat64, requiring explicit conversion of one of the parameters. Note that the result will lose accuracy, and type conversion is a computationally expensive operation.
Some functions on Decimal return the result as Float64 (for example, var or stddev). Intermediate calculations may still be performed in Decimal form, which could lead to different outcomes between inputs of Float64 and Decimal with the same value.
<span id="a03c0f53"></span>
## Overflow check
Integer overflow may occur during Decimal calculation. Excessive digits in the fraction part will be discarded (without rounding). Too many digits in the integer part can cause exceptions.
```SQL
SELECT toDecimal32(2, 4) AS x, x / 3 
```

```SQL
┌──────x─┬─divide(toDecimal32(2, 4), 3)─┐
│ 2.0000 │                       0.6666 │
└────────┴──────────────────────────────┘
```

```SQL
SELECT toDecimal32(4.2, 8) AS x, x * x
```

```SQL
DB::Exception: Scale is out of bounds.
```

```SQL
SELECT toDecimal32(4.2, 8) AS x, 6 * x
```

```SQL
DB::Exception: Decimal math overflow.
```

Overflow checks can slow down the calculations. If an overflow is known to be impossible, it can be disabled through `decimal_check_overflow` settings. In this case, an overflow will result in incorrect outcomes.
```SQL
SET decimal_check_overflow = 0;
SELECT toDecimal32(4.2, 8) AS x, 6 * x 
```

```SQL
┌──────────x─┬─multiply(6, toDecimal32(4.2, 8))─┐
│ 4.20000000 │                     -17.74967296 │
└────────────┴──────────────────────────────────┘
```

Overflow checks occur not only in arithmetic operations but also in comparison operations.
```SQL
SELECT toDecimal32(1, 8) < 100 
```

```SQL
DB::Exception: Can't compare.
```
