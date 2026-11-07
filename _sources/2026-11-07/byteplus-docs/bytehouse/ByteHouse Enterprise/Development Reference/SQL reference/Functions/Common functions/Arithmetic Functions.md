---
title: "Arithmetic Functions"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/arithmetic-functions"
---

For all arithmetic functions, the result type is the smallest suitable numerical type if such a type exists. The smallest numerical type is determined based on the number of digits, whether it is signed, and whether it is a floating-point type. If there are not enough digits, the highest bit type is adopted.
Example:
```sql
SELECT toTypeName(0), toTypeName(0 + 0), toTypeName(0 + 0 + 0), toTypeName(0 + 0 + 0 + 0)
```

```SQL
┌─toTypeName(0)─┬─toTypeName(plus(0, 0))─┬─toTypeName(plus(plus(0, 0), 0))─┬─toTypeName(plus(plus(plus(0, 0), 0), 0))─┐
│ UInt8         │ UInt16                 │ UInt32                          │ UInt64                                   │
└───────────────┴────────────────────────┴─────────────────────────────────┴──────────────────────────────────────────┘
```

Arithmetic functions are applicable to any type among UInt8, UInt16, UInt32, UInt64, Int8, Int16, Int32, Int64, Float32, or Float64.
The way overflow is generated is the same as in C++.
<span id="plus-a-b-a-b-operator"></span>
## plus(a, b), a + b operator
Calculates the total sum of numerical values. You can also add a Date or DateTime to an integer. In the case of Date, adding integers to an integer means adding the corresponding number of days. For DateTime, this means adding the corresponding number of seconds.
<span id="minus-a-b-a-b-operator"></span>
## minus(a, b), a - b operator
Calculate the difference between numerical values, the result is always signed.
You can also subtract an integer from a Date or DateTime. See the above 'plus'.
<span id="multiply-a-b-a-b-operator"></span>
## multiply(a, b), a * b operator
Calculate the product of numerical values.
<span id="divide-a-b-a-b-operator"></span>
## divide(a, b), a / b operator
Calculate the quotient of numerical values. The result type is always a floating-point number. It is not integer division. For integer division, use the 'intDiv' function. When divided by zero, you get 'inf', '-inf', or 'nan'.
<span id="intdiv-a-b"></span>
## intDiv(a,b)
Calculates the quotient of numerical values, rounding down (by absolute value). Throws an exception when dividing by zero or when the smallest negative number is divided by -1.
<span id="intdivorzero-a-b"></span>
## intDivOrZero(a,b)
The difference with 'intDiv' is that it returns zero when dividing by zero or when the smallest negative number is divided by -1.
<span id="modulo-a-b-a-b-operator"></span>
## modulo(a, b), a % b operator
Calculate the remainder after division. If the parameters are floating-point numbers, they are pre-converted to integers by removing the decimal part. The remainder has the same meaning as in C++. Truncated division is used for negative numbers. An exception is thrown when dividing by zero or dividing the smallest negative number by -1.
<span id="moduloorzero-a-b"></span>
## moduloOrZero(a, b)
Unlike [modulo](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/en/sql-reference/functions/arithmetic-functions.md), when dividing by zero, the result returns zero.
<span id="negate-a-a-operator"></span>
## negate(a), -a operator
By changing the sign bit of the numerical value, negation always results in a signed value.
<span id="abs-a"></span>
## abs(a)
Calculate the absolute value of (a). That is, if a < 0, it returns -a. For unsigned types, it does nothing. For signed integer types, it returns an unsigned number.
<span id="gcd-a-b"></span>
## gcd(a,b)
Returns the greatest common divisor of the numerical values. Throws an exception when dividing by zero or dividing the smallest negative number by -1.
<span id="lcm-a-b"></span>
## lcm(a,b)
Returns the least common multiple of the numerical values. Throws an exception when dividing by zero or dividing the smallest negative number by -1.
