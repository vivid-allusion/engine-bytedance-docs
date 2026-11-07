---
title: "Arithmetic"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-arithmetic"
---

For all arithmetic functions, the result type is the smallest numeric type that fits the result if such a type exists. The smallest numeric type is determined based on the number of bits, whether it is signed, and whether it is a floating\-point type. If there are not enough bits, the highest bit type is used.

For example:

```SQL
SELECT toTypeName(0), toTypeName(0 + 0), toTypeName(0 + 0 + 0), toTypeName(0 + 0 + 0 + 0)
```


```Plain
┌─toTypeName(0)─┬─toTypeName(plus(0, 0))─┬─toTypeName(plus(plus(0, 0), 0))─┬─toTypeName(plus(plus(plus(0, 0), 0), 0))─┐
│ UInt8         │ UInt16                 │ UInt32                          │ UInt64                                   │
└───────────────┴────────────────────────┴─────────────────────────────────┴──────────────────────────────────────────┘
```


Arithmetic functions are applicable to any type among UInt8, UInt16, UInt32, UInt64, Int8, Int16, Int32, Int64, Float32, or Float64.

The generation of overflow is the same as in C++.

<span id="35b30bec"></span>
### plus

Calculates the sum of the values. You can also add a Date or DateTime with an integer. When it comes to Date, adding integers to it means adding the corresponding number of days. For DateTime, this means adding the corresponding number of seconds.

**Syntax**

```SQL
select plus(a, b) -- a + b operator
```


Parameters


* `a` – Number.

* `b` – Number.


Return Value


* Returns the sum of the numbers.


**Example**

```SQL
select plus(1,2);
```


**Result**

```SQL
┌─plus(1, 2)─┐
│ 3          │
└────────────┘
```


<span id="4d326514"></span>
### minus

Calculates the difference between values, and the result is always signed. You can also subtract integers from Date or DateTime. See 'plus' above.

**Syntax**

```SQL
minus(a, b) -- a-b operator 
```


Parameters


* `a` – Number.

* `b` – Number.


Return Value


* Returns the difference between numbers.


**Example**

```SQL
SELECT minus(10, 3);
```


**Result**

```SQL
┌─minus(10, 3)─┐
│ 7            │
└──────────────┘
```


<span id="ffc41abd"></span>
### multiply

Calculate the product of numerical values.

**Syntax**

```SQL
multiply(a, b) -- a * b operator 
```


Parameters


* `a` \- Numeric.

* `b` \- Numeric.


Return Value


* Returns the product of numerical values.


**Example**

```SQL
SELECT multiply(3,12);
```


**Result**

```SQL
┌─multiply(3, 12)─┐
│ 36              │
└─────────────────┘
```


<span id="2078a410"></span>
### divide

Calculates the quotient of numerical values. The result type is always a floating point type. It is not integer division. For integer division, please use the 'intDiv' function. When dividing by zero, you get 'inf', '\-inf', or 'nan'.

**Syntax**

```SQL
divide(a, b) -- a / b operator
```


Parameters


* `a` – number.

* `b` – number.


Return value


* Return float type.


**Example**

```SQL
SELECT divide(50, 2);
```


**Result**

```SQL
┌─divide(50, 2)─┐
│ 2.5e+01       │
└───────────────┘
```


<span id="c0d57a7b"></span>
### intDiv

Calculates the quotient of numerical values, rounding down towards zero (by absolute value). Throws an exception when dividing by zero or dividing the smallest negative number by \-1.

**Syntax**

```SQL
intDiv(a, b)
```


Parameter


* `a` \- number.

* `b` \- number.


Return value


* Returns the quotient of the numbers.


**Example**

```SQL
SELECT intDiv(10, 2);
```


**Result**

```SQL
┌─intDiv(10, 2)─┐
│ 5             │
└───────────────┘
```


<span id="8ec96a22"></span>
### intDivOrZero

The difference between this and 'intDiv' is that it returns zero when dividing by zero or when the smallest negative number is divided by \-1.

**Syntax**

```SQL
intDivOrZero(a, b)
```


Parameter


* `a` – digit.

* `b` – digit.


Return Value


* Return the quotient of a numeric value.


**Example**

```SQL
SELECT intDivOrZero(10, -2);
```


**Result**

```SQL
┌─intDivOrZero(10, -2)─┐
│ -5                   │
└──────────────────────┘
```


<span id="ad03c6b5"></span>
### modulo

Calculate the remainder after division. If both inputs are integers, the result type is integer. If one of the inputs is a floating point number, the result is a floating point number. The rest is the same as in C++. Truncation division is used for negative numbers. An exception is thrown when dividing by zero or dividing the smallest negative number by \-1.

**Syntax**

```SQL
modulo(a, b) --a % b operator
```


Parameters


* `a` – number.

* `b` – number.


Return Value


* Returns the remainder after division.


**Example**

```SQL
SELECT modulo(10, 3);
```


**Result**

```SQL
┌─modulo(10, 3)─┐
│ 1             │
└───────────────┘
```


<span id="54a260c3"></span>
### moduloOrZero

Unlike modulo, when dividing by zero, the result returns zero

**Syntax**

```SQL
moduloOrZero(a, b) --a % b operator
```


Parameters


* `a` – Number.

* `b` – Number.


Return Value


* Returns the remainder after division.


**Example**

```SQL
SELECT moduloOrZero(10, 0);
```


**As a result**

```SQL
┌─moduloOrZero(10, 0)─┐
│ 0             │
└───────────────┘
```


<span id="ccdaba93"></span>
### negate

By changing the sign bit of the numerical value, the result is always signed

**Grammar**

```SQL
negate(a) -- -a operator
```


Param


* `x` \- number.


Return value


* Return the negative of the number.


**Example**

```SQL
SELECT negate(20);
```


**As a result**

```SQL
┌─negate(20)─┐
│ -20        │
└────────────┘
```


<span id="7ea96729"></span>
### abs

Calculate the absolute value of number a. That is, if a < 0, it returns \-a. For unsigned types, it doesn't perform any action. For signed integer types, it returns an unsigned number.

**Syntax**

```SQL
abs(x)
```


Param


* `x` – Number.


Return value


* Return the absolute value of the number.


**Example**

```SQL
SELECT abs(-2);
```


**As a result**

```SQL
┌─abs(-2)─┐
│ 2       │
└─────────┘
```


<span id="412a3c21"></span>
### gcd

Returns the greatest common divisor of numerical values. Throws an exception when dividing by zero or dividing the smallest negative number by \-1.

**Syntax**

```SQL
gcd(a, b)
```


Param


* `a` \- Number.

* `b` \- Number.


Return value


* Returns the greatest common divisor of the numerical values.


**Example**

```SQL
SELECT gcd(27,18);
```


**As a result**

```SQL
┌─gcd(27, 18)─┐
│ 9           │
└─────────────┘
```


<span id="6173646a"></span>
### lcm

Returns the least common multiple of the numerical values. Throws an exception when dividing by zero or dividing the smallest negative number by \-1.

**Syntax**

```SQL
lcm(a, b)
```


Param


* `a` \- Number.

* `a` – Number.


Return value


* Calculates the least common multiple of numerical values.


**Example**

```SQL
SELECT lcm(27,18);
```


**As a result**

```SQL
┌─lcm(27, 18)─┐
│ 54          │
└─────────────┘
```


<span id="2873d552"></span>
### max2

Compares two values and returns the maximum. Convert the return value to Float64.

**Syntax**

```SQL
max2(value1, value2)
```


**Param**


* **`Value1`** — The first value, type: Int/UInt or Float.

* **`Value2`** — The second value, type: Int/UInt or Float.


**Return value**


* The maximum of the two values.


Type: Float.

**Example**

Search query:

```SQL
SELECT max2(-1, 2);
```


As a result:

```Plain
┌─max2(-1, 2)─┐
│           2 │
└─────────────┘
```


<span id="0d2cff2b"></span>
### min2

Compares two values and returns the minimum. Return value type converted to Float64.

**Syntax**

```SQL
min2(value1, value2)
```


**Param**


* **`value1`** — The first value, type: Int/UInt or Float.

* **`value2`** — The second value, type: Int/UInt or Float.


**Return value**


* The minimum of the two values.


Type: Float.

**Example**

Search query:

```SQL
SELECT min2(-1, 2);
```


As a result

```Plain
┌─min2(-1, 2)─┐
│          -1 │
└─────────────┘
```
