---
title: "Mathematical function"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-mathematical"
---

<span id="e0a974e5"></span>
### COVAR_POP

Calculate the value of `Σ((x - x̅)(y - y̅)) / n`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This function uses a numerically unstable algorithm. If you need stability in your calculations, please use the <code>covarPopStable</code> function. It runs slower but has lower calculation errors.</div>


**Syntax**

```SQL
covarPop(x, y)
```


**Parameters**


* `x` \- a set of numbers.

* `y` a set of numbers.


**Return Value**


* Population covariance.


Type: `Float64`

**Example**

```SQL
CREATE TABLE test.test_covarPop(days_employed Int32, salary Int32) ENGINE = CnchMergeTree ORDER BY days_employed; -- create sample table
INSERT INTO test.test_covarPop(days_employed,salary) VALUES(300,3000),(600,4000),(900,4500),(1200,4800),(1500,5000); -- insert data to table
SELECT covarPop(days_employed,salary) FROM test.test_covarPop; -- find out the population covariance for days employed and salary
```


Result:

```Plain
┌─covarPop(days_employed, salary)─┐
│ 2.88e+05                        │
└─────────────────────────────────┘
```


<span id="c244d1f2"></span>
### COVAR_SAMP

Calculate the value of `Σ((x - x̅)(y - y̅)) / (n - 1)`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This function uses a numerically unstable algorithm. If you need numerical stability in your calculations, please use the <a href="https://en.wikipedia.org/wiki/Numerical_stability">numerical stability</a><code>covarSampStable</code> function. It runs slower but has lower calculation errors.</div>


**Syntax**

```SQL
covarSamp(x, y)
```


**Parameters**


* `x`— a collection of numbers.

* `y`— a collection of numbers.


**Return Value**


* When `n <= 1`, the sample covariance returns +∞.


Type: `Float64`

**Example**

```SQL
CREATE TABLE test.test_covarSamp(days_employed Int32, salary Int32) ENGINE = CnchMergeTree ORDER BY days_employed; -- create sample table
INSERT INTO test.test_covarSamp(days_employed,salary) VALUES(300,3000),(600,4000),(900,4500),(1200,4800),(1500,5000); -- insert data to table
SELECT covarSamp(days_employed,salary) FROM test.test_covarSamp; -- find out the sample covariance for days employed and salary
```


Result:

```Plain
┌─covarSamp(days_employed, salary)─┐
│ 3.6e+05                          │
└──────────────────────────────────┘
```


<span id="4c2a3fdc"></span>
### acos

Inverse cosine.

**Syntax**

```SQL
acos(x)
```


**Parameters**


* `x` \- in radians.


**Return Value**


* Returns in radians.


Type: `Float64`

**Example**

```SQL
SELECT acos(-1);
```


Result:

```Plain
┌─ACOS(-1)──────────────┐
│ 3.141592653589793e+00 │
└───────────────────────┘
```


<span id="5695de14"></span>
### asin

Inverse sine.

**Syntax**

```SQL
asin(x)
```


**Parameters**


* `x` – in radians.


**Return Value**


* Returns the angle in radians.


Type: `Float64`

**Example**

```SQL
SELECT asin(-1);
```


Result:

```Plain
┌─asin(1)────────────────┐
│ 1.5707963267948966e+00 │
└────────────────────────┘
```


<span id="d6e1f35e"></span>
### atan

Inverse tangent.

**Syntax**

```SQL
atan(x)
```


**Parameter**


* `x` – in radians.


**Return value**


* Returns the radians.


Type: `Float64`

**Example**

```SQL
SELECT atan(-1);
```


Result:

```Plain
┌─atan(-1)───────────────┐
│ -7.853981633974483e-01 │
└────────────────────────┘
```


<span id="53f749cd"></span>
### cbrt

Accepts a numerical parameter and returns a Float64 number close to the cube root of the parameter.

**Syntax**

```SQL
cbrt(x)
```


**Parameter**


* `x` number.


**Return Value**


* The root of the argument.


Type: `Float64`

**Example**

```SQL
SELECT cbrt(8)
```


Result:

```Plain
┌─cbrt(8)─┐
│ 2e+00   │
└─────────┘
```


<span id="3a8b88a7"></span>
### ceil

Returns the smallest integer greater than or equal to `x`. In other respects, it is the same as the `floor` function (see above).

**Syntax**

```SQL
ceil(x[, N])
```


**Parameter**


* `x` number.

* `N`—`decimal-places`, an integer value.


**Return Value**


* Integer.


Type: `Float64`

**Example**

```SQL
SELECT ceil(1.99,2);
```


Result:

```Plain
┌─ceil(1.99, 2)─┐
│ 1.99e+00      │
└───────────────┘
```


Other Examples:

```SQL
SELECT ceil(1.99,1);
```


Result:

```Plain
┌─ceil(1.99, 1)─┐
│ 2e+00         │
└───────────────┘
```


<span id="bd28ee5d"></span>
### ceiling

Returns the smallest integer greater than or equal to `x`. In other respects, it's similar to the `floor` function (see above).

**Syntax**

```SQL
ceiling(x[, N]) 
```


**Parameters**


* `x` Number.

* Round `N` to an integer at the decimal point.


**Return Value**


* Integer.


Type: `Float64`

**Example**

```SQL
SELECT ceiling(1.99,2);
```


Result:

```Plain
┌─ceil(1.99, 2)─┐
│ 1.99e+00      │
└───────────────┘
```


Other Examples:

```SQL
SELECT ceiling(1.99,1);
```


Result:

```Plain
┌─ceil(1.99, 1)─┐
│ 2e+00         │
└───────────────┘
```


<span id="17e2b779"></span>
### cos

Cosine.

**Syntax**

```SQL
cos(x)
```


**Parameters**


* `x` \- radians.


**Return values**


* Returns the radians.


Type: `Float64`

**Examples**

```SQL
SELECT cos(pi())
```


Result:

```Plain
┌─cos(pi())─┐
│ -1e+00    │
└───────────┘
```


<span id="14b2adf3"></span>
### erf

Error function `erf(x)=2√π∫x0e−t2dt erf(x)`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If "x" is non\-negative, then the probability of a random variable with a <code>erf(x / σ√2)</code> normal distribution having a standard deviation "σ" deviates from the expected value by more than "x".</div>


**Syntax**

```SQL
erf(x)
```


**Parameter**


* `x` number.


**Return Value**


* Probability.


Type: `Float64`

**Example**

```SQL
SELECT erf(3 / sqrt(2));
```


```Plain
┌─erf(divide(3, sqrt(2)))─┐
│ 9.973002039367398e-01   │
└─────────────────────────┘
```


Note: The Three Sigma Rule

<span id="d671b93d"></span>
### erfc

The complementary error function follows the formula: erfc(x) = 1 − erf(x).

Accepts a numeric parameter and returns a Float64 number close to 1 \- erf(x), without causing precision loss for large `x` values.

**Syntax**

```SQL
erfc(x)
sql
```


**Parameter**


* `x` number.


**Return Value**


* Probability.


Type: `Float64`

**Example**

```SQL
SELECT erfc(3 / sqrt(2));
```


```Plain
┌─erfc(divide(3, sqrt(2)))─┐
│ 2.6997960632601913e-03   │
└──────────────────────────┘
```


Note: the three sigma rule

<span id="af760bce"></span>
### exp

Accepts a numeric argument and returns a Float64 number close to its exponential value.

**Syntax**

```SQL
exp(x)
```


**Parameter**


* `x` number.


**Return Value**


* The computed result.


Type: `Float64`

**Example**

```SQL
SELECT exp(1);
```


Result:

```Plain
┌─exp(1)────────────────┐
│ 2.718281828459045e+00 │
└───────────────────────┘
```


<span id="1bb03117"></span>
### exp10

Accepts a numeric argument and returns a Float64 number close to the power of 10 `x`.

**Syntax**

```SQL
exp10(x)
```


**Parameters**


* `x` number.


**Return Value**


* Calculated result.


Type: `Float64`

**Example**

```SQL
SELECT exp10(3);
```


Result:

```Plain
┌─exp10(3)─┐
│ 1e+03    │
└──────────┘
```


<span id="bb668b4a"></span>
### exp2

Accepts a numeric parameter and returns a Float64 number close to the power of 2 `x`.

**Syntax**

```SQL
exp2(x)
```


**Parameters**


* `X` number.


**Return Value**


* Computed result.


Calculation

Type: `Float64`

**Example**

```SQL
SELECT exp2(3);
```


Result:

```Plain
┌─exp2(3)─┐
│ 8e+00   │
└─────────┘
```


<span id="2945ceb5"></span>
### floor

Returns the largest integer less than or equal to `x`. The integers are multiples of 1/10N; if 1/10N is not exact, they are the nearest number to the corresponding data type.


* `N` is an integer constant, an optional parameter. By default, it is zero, meaning rounding to the nearest integer.

* `N` can be negative.

* `x` is of any numeric type. The result is a number of the same type.


For integer parameters, using a negative value for rounding makes sense `N` (for non\-negative numbers `N`, the function does nothing).

If rounding causes overflow (for example, floor(\-128, \-1)), a result specific to the implementation is returned.

**Syntax**

```SQL
floor(x[, N])
```


**Parameters**


* `x` number.

* `N` – Round to an integer.


**Return value**


* The computed result.


Type: `Float64`

**Example**

```SQL
SELECT floor(123.45, 1);
```


Result:

```Plain
┌─floor(123.45, 1)─┐
│ 1.234e+02        │
└──────────────────┘
```


Other Examples:

```SQL
select floor(123.45, -1);
```


Result:

```Plain
┌─floor(123.45, -1)─┐
│ 1.2e+02           │
└───────────────────┘
```


<span id="df6b3818"></span>
### intExp10

Accepts a numeric argument and returns a UInt64 number approximating the power of 10 raised to x.

**Syntax**

```SQL
intExp10(x)
```


**Parameters**


* `x` Number.


**Return Value**


* The result of the calculation.


Type: `UInt64`

**Example**

```SQL
SELECT intExp10(3);
```


Result:

```Plain
┌─intExp10(3)─┐
│ 1000        │
└─────────────┘
```


<span id="5af858dd"></span>
### intExp2

Accepts a numeric parameter and returns a UInt64 number close to 2 raised to the power of x.

**Syntax**

```SQL
intExp2(x)
```


**Parameter**


* `x` number.


**Return Value**


* The result of the calculation.


Type: `UInt64`

**Example**

```SQL
SELECT intExp2(3);
```


Result:

```Plain
┌─intExp2(3)─┐
│ 8          │
└────────────┘
```


<span id="91c8eddd"></span>
### lgamma

The logarithm of the gamma function.

**Syntax**

```SQL
lgamma(x)
```


**Parameters**


* `x` number.


**Return value**


* The result of the calculation.


Type: `Float64`

**Example**

```SQL
SELECT lgamma(3);
```


The result:

```Plain
┌─lgamma(3)─────────────┐
│ 6.931471805599453e-01 │
└───────────────────────┘
```


<span id="c721a824"></span>
### ln

Accepts a numerical argument and returns a Float64 number close to the natural logarithm of the argument.

**Syntax**

```SQL
ln(x)
```


**Parameter**


* `x` number.


**Return value**


* The calculation result.


Type: `Float64`

**Example**

```SQL
select ln(2.7182818)
```


As a result:

```Plain
┌─ln(2.7182818)─────────┐
│ 9.999999895305024e-01 │
└───────────────────────┘
```


<span id="0266470e"></span>
### log10

Accepts a numerical parameter and returns a Float64 number that approximates the decimal logarithm of the parameter.

**Syntax**

```SQL
log10(x)
sql
```


**Param**


* `x` number.


**Return value**


* The calculation result.


Type: `Float64`

**Example**

```SQL
SELECT log10(3);
```


Result:

```Plain
┌─log10(3)───────────────┐
│ 4.7712125471966244e-01 │
└────────────────────────┘
```


<span id="7d416f4b"></span>
### log2

Accepts a numerical argument and returns a Float64 number close to the binary logarithm of that parameter.

**Syntax**

```SQL
log2(x)
```


**Parameter**


* `x` number.


**Return value**


* The result of the calculation.


Type: `Float64`

**Example**

```SQL
select log2(3);
```


Result:

```Plain
┌─log2(3)───────────────┐
│ 1.584962500721156e+00 │
└───────────────────────┘
```


<span id="7c640245"></span>
### pi

Returns a Float64 number close to π.

**Syntax**

```SQL
pi()
```


**Parameter**


* Not applicable


**Return value**


* The value of π.


Type: `Floating-point number`

**Example**

```SQL
SELECT pi();
```


As a result:

```Plain
┌─pi()──────────────────┐
│ 3.141592653589793e+00 │
└───────────────────────┘
```


<span id="23608763"></span>
### pow

Accepts two numerical value parameters x and y. Returns a Floating\-point number close to the yth power of x.

**Syntax**

```SQL
pow(x, y)
```


**Param**


* `x` Number.


**Return value**


* Calculation result.


Type: `Float64`

**Example**

```SQL
SELECT pow(2, 3);
```


Result:

```Plain
┌─pow(2, 3)─┐
│ 8e+00     │
└───────────┘
```


<span id="52a9730f"></span>
### power

Accepts two numerical values, x and y. Returns a Float64 number approximating x to the power of y.

Alias: [pow](https://docs.byteplus.com/docs/bytehouse/docs-mathematical#23608763).

<span id="ff03d6ae"></span>
### round

Round the value to the specified number of decimal places.

This function returns the closest number in the specified order. If the distance between the given number and the surrounding numbers is equal, the function uses banker's rounding for floating\-point numbers and rounds from zero for other number types.

**Syntax**

```SQL
round(expression [, decimal_places])
```


**Parameters**


* `expression`— The number to be rounded. It can be any expression that returns a numerical data type.

* `decimal-places`— An integer value.

   * If `decimal-places > 0`, then the function rounds the value to the right of the decimal point.

   * If `decimal-places < 0`, then the function rounds the value to the left of the decimal point.

   * If `decimal-places = 0` is set, the function will round the value to an integer. In this case, the parameter can be omitted.


**Return value:** 


* The rounded number will be the same type as the input numbers.


Type: `Float64`

**Example**

```SQL
SELECT round(1.1234);
```


Result:

```Plain
┌─round(1.1234)─┐
│ 1e+00         │
└───────────────┘
```


Other examples

```SQL
SELECT round(1.1234,2);
```


Result:

```Plain
┌─round(1.1234, 2)─┐
│ 1.12e+00         │
└──────────────────┘
```


<span id="c01b0124"></span>
### roundAge

Accept a number. If the number is smaller than 17, return 17. Otherwise, round the number down to a number in the following set: 17, 25, 35, 45, 55. This function is specific to Yandex.Metrica and is used to implement user age reports.

**Syntax**

```SQL
roundAge(num)
```


**Param**


* `num` Age.


**Return Value**


* A rounded value.


Type: `UInt8`

**Example**

```SQL
SELECT roundAge(50);
```


As a result:

```Plain
┌─roundAge(50)─┐
│ 45           │
└──────────────┘
```


Other examples

```SQL
SELECT roundAge(16), roundAge(17),roundAge(18);
```


As a result:

```Plain
┌─roundAge(16)─┬─roundAge(17)─┬─roundAge(18)─┐
│ 17           │ 17           │ 18           │
└──────────────┴──────────────┴──────────────┘
```


<span id="bfd89cd0"></span>
### roundDown

Accepts a number and rounds it down to an element in the specified array. If the value is smaller than the lowest boundary or bigger than the highest boundary, then return the lowest or highest boundary.

**Syntax**

```SQL
roundDown(number, array)
```


**Param**


* `Number` number.

* `Array` – arrangement.


**Return value**


* The result after rounding.


**Example**

```SQL
SELECT roundDown(2, [6, 7, 8]);
```


As a result:

```Plain
┌─roundDown(2, [6, 7, 8])─┐
│ 6                       │
└─────────────────────────┘
```


<span id="7a6f1f88"></span>
### roundDuration

Accepts a `number`. If the number is less than one, return 0. Otherwise, it rounds the number down to one of the following set of numbers: 1, 10, 30, 60, 120, 180, 240, 300, 600, 1200, 1800, 3600, 7200, 18000, 36000. This function is specific to Yandex. Metrica, used for implementing session duration reports.

**Grammar**

```SQL
roundDuration(number)
```


**Param**


* `x` number.


**Return value**


* The result rounded.


**Example**

```SQL
SELECT roundDuration(230);
```


As a result:

```Plain
┌─roundDuration(230)─┐
│ 180                │
└────────────────────┘
```


<span id="5ade79b6"></span>
### roundToExp2

Accepts `number`. If `number` is smaller than one, then return 0. Otherwise, round `number` down to the nearest (non\-negative integer) power of two.

**Syntax**

```SQL
roundToExp2(number)
```


**Parameter**


* `Number`.


**Return value**


* The result of rounding.


**Example**

```SQL
SELECT roundToExp2(31);
```


As a result:

```Plain
┌─roundToExp2(31)─┐
│ 16              │
└─────────────────┘
```


<span id="2b6ed328"></span>
### sin

Sine.

**Grammar**

```SQL
sin(x)
```


**Param**


* `x` \- in radians.


**Return value**


* Returns the radian.


Type: `Float64`

**Example**

```SQL
SELECT sin(pi()/2)
```


As a result:

```Plain
┌─sin(divide(pi(), 2))─┐
│ 1e+00                │
└──────────────────────┘
```


<span id="5037ed87"></span>
### sqrt

Accepts a numerical argument and returns a Float64 number close to the square root of the argument.

**Syntax**

```SQL
sqrt(x)
```


**Param**


* `x` number.


**Return value**


* Square root.


Type: `Float64`

**Example**

```SQL
SELECT sqrt(4);
```


As a result:

```Plain
┌─sqrt(4)─┐
│ 2e+00   │
└─────────┘
```


<span id="8b5ba4cc"></span>
### tan

Tangent.

**Grammar**

```SQL
tan(x)
```


**Param**


* `x` \- in radians.


**Return value**


* Returns radians.


Type: `Float64`

**Example**

```SQL
SELECT tan(pi()/4);
```


As a result:

```Plain
┌─tan(divide(pi(), 4))──┐
│ 9.999999999999999e-01 │
└───────────────────────┘
```


Advisory: The result has specific precision

<span id="dd866d56"></span>
### tgamma

Calculate the gamma function of arg.

**Syntax**

```SQL
tgamma(x)
```


**Param**


* `x` number.


**Return value**


* As a result of the calculation.


**Example**

```SQL
select tgamma(10);
```


Result:

```Plain
┌─tgamma(10)─────────────┐
│ 3.6287999999999994e+05 │
└────────────────────────┘
```


<span id="2bde8323"></span>
### trunc

Return the integer with the largest absolute value that is less than or equal to `x`. In all other respects, it functions the same as the "floor" function (see above).

**Example**

```SQL
trunc(x[, N])
truncate(x[, N])
```


**Param**


* `x` Number.

* `N` rounded to an integer after the decimal point.


**Return value**


* Routing number.


**Example**

```SQL
SELECT trunc(100.11, 1)
```


As a result:

```Plain
┌─trunc(100.11, 1)─┐
│ 1.001e+02        │
└──────────────────┘
```


<span id="1af7df69"></span>
### truncate

Delete all data from the table. When `IF EXISTS` clause is omitted, if the table does not exist, the query returns an error.

`TRUNCATE` query does not support views, files, URLs, buffers, and empty table engines.

**Syntax**

```SQL
TRUNCATE TABLE [IF EXISTS] [db.]name 
```


**Parameter**


* `Name` \- table name.

* `[IF EXISTS]` Optional, if the table does not exist, the query returns an Error.

* `[db.]` Optional, database name.

* Optional, cluster name.


**Return value**


* Not applicable


**Example**

```SQL
CREATE TABLE test.test_truncate (id Int32) ENGINE = CnchMergeTree ORDER BY id;
INSERT INTO test.test_truncate(id) VALUES(1),(2),(3),(4),(5); -- insert 1,2,3,4,5 to table
SELECT * FROM test.test_truncate; -- check the date before truncate
```


```Plain
┌─id─┐
│ 1  │
│ 2  │
│ 3  │
│ 4  │
│ 5  │
└────┘
```


```SQL
TRUNCATE TABLE test.test_truncate
SELECT * FROM test.test_truncate
```
