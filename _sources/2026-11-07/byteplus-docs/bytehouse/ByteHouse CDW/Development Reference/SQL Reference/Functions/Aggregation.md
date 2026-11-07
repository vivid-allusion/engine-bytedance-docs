---
title: "Aggregation"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-aggregate"
---

<span id="9818ed12"></span>
### any

Select the first encountered value.

The execution of the query can be in any order, and it can even differ each time, therefore the result of this function is unpredictable.

To obtain a certain result, you can use the "min" or "max" functions instead of "any".

In some cases, you can rely on the execution order. This applies in situations where the SELECT comes from a subquery using ORDER BY.

When a `SELECT` query includes a `GROUP BY` clause or at least one aggregate function, ByteHouse (unlike MySQL) requires that all expressions in the clause are derived from the `SELECT` key or aggregate functions. In other words, every column selected from the table must be used in the key or aggregate functions. To achieve behavior similar to MySQL, you can include other columns within the aggregate functions.

**Grammar**

```SQL
any(column)
```


**Parameters**


* `Column` – Column name.


**Return Value**


* The first encountered value. Type is the same as the input column.


**Example**

```SQL
SELECT any(number) FROM numbers(10);
```


```SQL
┌─any(number)─┐
│ 0           │
└─────────────┘
```


<span id="42c41087"></span>
### anyHeavy

[Heavy hitters](http://www.cs.umd.edu/~samir/498/karp.pdf) algorithm selects a frequently occurring value. If in each execution thread of the query there is a value that appears in more than half of the cases, that value is returned. Usually, the outcome is uncertain.

**Grammar**

```SQL
anyHeavy(column)
```


**Parameters**


* `Column` \- Column name.


**Return Value**


* The most common value. Type is the same as the input column.


**Example**

```SQL
CREATE TABLE IF NOT EXISTS test.functionAnyHeavy(id Int) ENGINE=CnchMergeTree() ORDER BY id;
INSERT INTO test.functionAnyHeavy values (1),(1),(1),(2),(3);
SELECT anyHeavy(id) FROM test.functionAnyHeavy;
```


```SQL
┌─anyHeavy(id)─┐
│ 1            │
└──────────────┘
```


<span id="98ddbbe8"></span>
### anyLast

Select the last value encountered.

The result is equally uncertain.

**Grammar**

```SQL
anyLast(column)
sql
```


**Parameter**


* `Column` \- column name.


**Return value**


* The last value encountered. The type is the same as the input column.


**Example**

```SQL
SELECT anyLast(number) FROM numbers(10);
```


```SQL
┌─anyLast(number)─┐
│ 9               │
└─────────────────┘
```


<span id="cfbe97b4"></span>
### argMax

Computes the maximum value of `arg`. If the maximum `val` has multiple different values, return the first value encountered. `argval`

**Syntax**

```SQL
argMax(arg, val)
sql
```


**Parameters**


* `arg` argument.

* `val` value.


**Return Value**


* The arg value corresponding to the maximum val. Type is the same as arg type.


**Example**

```SQL
CREATE TABLE IF NOT EXISTS test.functionArgMax (user String, salary Int) Engine=CnchMergeTree() ORDER BY user;
INSERT INTO test.functionArgMax VALUES ('director',5000),('manager',3000),('worker',1000);
SELECT argMax(user, salary) FROM test.functionArgMax;
```


```SQL
┌─argMax(user, salary)─┐
│ director             │
└──────────────────────┘
```


<span id="5b796018"></span>
### argMin

Compute the minimum value of `arg`. If there are multiple different values for the minimum `val`, return the first value encountered. `argval`

**Syntax**

```SQL
argMin(arg, val)
```


**Parameters**


* `arg` argument.

* `val` value.


**Return Value**


* arg value corresponding to the minimum val. Type corresponds to the same type as arg.


**Example**

```SQL
CREATE TABLE IF NOT EXISTS test.functionArgMin (user String, salary Int) Engine=CnchMergeTree() ORDER BY user;
INSERT INTO test.functionArgMin VALUES ('director',5000),('manager',3000),('worker',1000);
SELECT argMin(user, salary) FROM test.functionArgMin;
```


```SQL
┌─argMin(user, salary)─┐
│ worker               │
└──────────────────────┘
```


<span id="51bb73e6"></span>
### avg

Calculates the arithmetic mean.

**Syntax**

```SQL
avg(x)
```


**Parameters**


* `x`— Input value, must be an integer, a floating number, or a decimal.


**Return value**


* Arithmetic mean, always a Float64.

* `NaN` when the input parameter `x` is empty.


**Example**

```SQL
CREATE TABLE IF NOT EXISTS test.functionAvg (x Int8) ENGINE=CnchMergeTree() ORDER BY x;
INSERT INTO test.functionAvg SELECT * FROM numbers(6);
SELECT avg(x) FROM test.functionAvg;
```


```SQL
┌─avg(x)──┐
│ 2.5e+00 │
└─────────┘
```


```SQL
CREATE TABLE IF NOT EXISTS test.functionAvg (x Int8) ENGINE=CnchMergeTree() ORDER BY x;
SELECT avg(x) FROM test.functionAvg;
```


```SQL
┌─avg(x)─┐
│ NaN    │
└────────┘
```


<span id="a3de21c0"></span>
### corr

Calculate the Pearson correlation coefficient: `Σ((x - x̅)(y - y̅)) / sqrt(Σ((x - x̅)^2) * Σ((y - y̅)^2))`.

This function uses an algorithm that is not numerically stable. If you need [numerical stability](https://en.wikipedia.org/wiki/Numerical_stability) in calculation, please use `corrStable` function. It runs more slowly, but with lower calculation errors.

**Syntax**

```SQL
corr(x, y)
```


**Parameters**


* `x`— Input value, must be an integer or a floating\-point number.

* `y`— Input value, must be an integer or a floating\-point number.


**Return Value**


* Pearson correlation coefficient, always a Float64.


**Example**

```SQL
CREATE TABLE IF NOT EXISTS test.functionCorr (x Int8, y Int8) ENGINE=CnchMergeTree() ORDER BY x;
INSERT INTO test.functionCorr VALUES (1,5),(2,4),(3,3),(4,2),(5,1);
SELECT corr(x,y) FROM test.functionCorr;
```


```SQL
┌─corr(x, y)─┐
│ -1e+00     │
└────────────┘
```


<span id="0a70c9d1"></span>
### covarPop

Calculates the value `Σ((x - x̅)(y - y̅)) / n`.

This function uses a numerically unstable algorithm. If you need to compute numerical stability in [numerical stability](https://en.wikipedia.org/wiki/Numerical_stability) `covarPopStable`, please use this function. It runs slower but has lower calculation errors.

**Syntax**

```SQL
covarPop(x, y)
```


**Parameters**


* `x`— Input value, must be an integer or a floating\-point number.

* `y`— Input value, must be an integer or a floating\-point number.


**Return value**


* `Σ((x - x̅)(y - y̅)) / n`, always a Float64.


**Example**

```SQL
CREATE TABLE IF NOT EXISTS test.functionCovarPop (x Int8, y Int8) ENGINE=CnchMergeTree() ORDER BY x;
INSERT INTO test.functionCovarPop VALUES (1,5),(2,4),(3,3),(4,2),(5,1);
SELECT covarPop(x,y) FROM test.functionCovarPop;
```


```SQL
┌─covarPop(x, y)─┐
│ -2e+00         │
└────────────────┘
```


<span id="59c5ba34"></span>
### covarSamp

Computes the value `Σ((x - x̅)(y - y̅)) / (n - 1)`.

This function uses a numerically unstable algorithm. If you need numerical stability in covarSampStable computation, please use this function. It operates more slowly but with lower computational error.

**Grammar**

```SQL
covarSamp(x, y)
```


**Parameters**


* `x`— Input value, must be an integer or float.

* `y`— Input value, must be an integer or float.


**Return value**


* `Σ((x - x̅)(y - y̅)) / (n - 1)`, always returns as Float64.

* When n <= 1, returns NaN.


**Example**

```SQL
CREATE TABLE IF NOT EXISTS test.functionCovarSamp (x Int8, y Int8) ENGINE=CnchMergeTree() ORDER BY x;
INSERT INTO test.functionCovarSamp VALUES (1,5),(2,4),(3,3),(4,2),(5,1);
SELECT covarSamp(x,y) FROM test.functionCovarSamp;
```


```SQL
┌─covarSamp(x, y)─┐
│ -2.5e+00        │
└─────────────────┘
```


```SQL
CREATE TABLE IF NOT EXISTS test.functionCovarSamp (x Int8, y Int8) ENGINE=CnchMergeTree() ORDER BY x;
INSERT INTO test.functionCovarSamp VALUES (1,5);
SELECT covarSamp(x,y) FROM test.functionCovarSamp;
```


```SQL
┌─covarSamp(x, y)─┐
│ NaN             │
└─────────────────┘
```


<span id="4d38e5f6"></span>
### groupArray

Create an array of parameter values.

Values can be added to the array in any undefined order.

The second version, with the `max_size` parameter, limits the size of the result array to `max_size` elements. For example, `groupArray(1)(x)` is equivalent to `[any (x)]`.

In some cases, you can still rely on the execution order. This applies to `SELECT` from subqueries using `ORDER BY`.

**Syntax**

```SQL
groupArray(x)
groupArray(max_size)(x)
```


**Parameters**


* `x`— Input value.


**Return values**


* Array of values. Type is an array.


**Example**

```SQL
select groupArray(number) from numbers(10);
```


```SQL
┌─groupArray(number)─────────────┐
│ [0, 1, 2, 3, 4, 5, 6, 7, 8, 9] │
└────────────────────────────────┘
```


```SQL
select groupArray(5)(number) from numbers(10);
```


```SQL
┌─groupArray(5)(number)─┐
│ [0, 1, 2, 3, 4]       │
└───────────────────────┘
```


<span id="8e387e38"></span>
### groupBitAnd

`AND` applies bitwise to a series of numbers.

**Syntax**

```SQL
groupBitAnd(expr)
```


**Parameters**


* `expr` – expression that produces a type `UInt*`.


**Return Value**


* Value of type `UInt*`.


**Example**

```SQL
CREATE TABLE IF NOT EXISTS test.groupBitAnd (num UInt8) ENGINE=CnchMergeTree() ORDER BY num;
INSERT INTO test.groupBitAnd VALUES (44),(28),(13),(85);
SELECT groupBitAnd(num) FROM test.groupBitAnd;
```


```SQL
┌─groupBitAnd(num)─┐
│ 4                │
└──────────────────┘
```


The bit representations of 44, 28, 13, and 85 are 00101100, 00011100, 00001101, and 01010101 respectively, with a bit sum of 00000100, equaling 4.

<span id="a5dc92ff"></span>
### groupBitOr

`OR` is applied bitwise to a series of numbers.

**Syntax**

```SQL
groupBitOr(expr)
```


**Parameters**


* `expr` \- An expression producing a type of `UInt*`.


**Return value**


* A value of type `UInt*`.


**Examples**

```SQL
CREATE TABLE IF NOT EXISTS test.functionGroupBitOr (num UInt8) ENGINE=CnchMergeTree ORDER BY num;
INSERT INTO test.functionGroupBitOr VALUES (44),(28),(13),(85);
SELECT groupBitOr(num) FROM test.functionGroupBitOr;
```


```SQL
┌─groupBitOr(num)─┐
│ 125             │
└─────────────────┘
```


The bit representations of 44, 28, 13, and 85 are 00101100, 00011100, 00001101 and 01010101 respectively, and the bitwise OR of these numbers is 01111101, equal to 125.

<span id="7e1db771"></span>
### groupBitXor

`XOR` applies bitwise to a series of numbers.

**Syntax**

```SQL
groupBitXor(expr)
```


**Parameters**


* `expr` – an expression that yields a type `UInt*`.


**Return Value**


* The value of type `UInt*`.


**Examples**

```SQL
CREATE TABLE IF NOT EXISTS test.functionGroupBitXor (num UInt8) ENGINE=CnchMergeTree ORDER BY num;
INSERT INTO test.functionGroupBitXor VALUES (44),(28),(13),(85);
SELECT groupBitXor(num) FROM test.functionGroupBitXor;
```


```SQL
┌─groupBitXor(num)─┐
│ 104              │
└──────────────────┘
```


The bitwise representations of 44, 28, 13, and 85 are 00101100, 00011100, 00001101, and 01010101, respectively. The bitwise XOR result of these four numbers is 01101000, which equals 104.

<span id="a080c74e"></span>
### groupBitmap

Performs bitmap or aggregate calculations on a series of unsigned integers, returning a cardinality of type UInt64, and returns a bitmap object if a suffix \-State is added.

**Syntax**

```SQL
groupBitmap(expr)
```


**Parameters**


* `expr` – An expression that produces a type of `UInt*`.


**Return Value**


* Value of type `UInt64`.


**Example**

```SQL
SELECT groupBitmap(number) FROM numbers(4);
```


```SQL
┌─groupBitmap(number)─┐
│ 4                   │
└─────────────────────┘
```


<span id="e68ffee5"></span>
### groupBitmapAnd

Calculates the AND of bitmap columns, returning a cardinality of type UInt64, and returns a bitmap object if a suffix \-State is added.

**Grammar**

```SQL
groupBitmapAnd(expr)
```


**Parameters**


* `expr` – An expression that generates a type `AggregateFunction(groupBitmap, UInt*)`.


**Return value**


* Type's value `UInt64`.


**Examples**

```SQL
DROP TABLE IF EXISTS bitmap_column_expr_test2;

CREATE TABLE bitmap_column_expr_test2(tag_id String,z AggregateFunction(groupBitmap, UInt32)) ENGINE = CnchMergeTree ORDER BY tag_id;

INSERT INTO bitmap_column_expr_test2 VALUES ('tag1', bitmapBuild(cast([1,2,3,4,5,6,7,8,9,10] as Array(UInt32))));
INSERT INTO bitmap_column_expr_test2 VALUES ('tag2', bitmapBuild(cast([6,7,8,9,10,11,12,13,14,15] as Array(UInt32))));
INSERT INTO bitmap_column_expr_test2 VALUES ('tag3', bitmapBuild(cast([2,4,6,8,10,12] as Array(UInt32))));

SELECT groupBitmapAnd(z) FROM bitmap_column_expr_test2 WHERE like(tag_id, 'tag%');
┌─groupBitmapAnd(z)─┐
│               3   │
└───────────────────┘

SELECT arraySort(bitmapToArray(groupBitmapAndState(z))) FROM bitmap_column_expr_test2 WHERE like(tag_id, 'tag%');
┌─arraySort(bitmapToArray(groupBitmapAndState(z)))─┐
│ [6,8,10]                                         │
└──────────────────────────────────────────────────┘
```


<span id="2637e2b0"></span>
### groupBitmapOr

Calculates the OR operation on bitmap columns, returns the cardinality as a UInt64 type, and returns a bitmap object if the suffix \-State is added. This is equivalent to `groupBitmapMerge`.

**Grammar**

```SQL
groupBitmapOr(expr)
```


**Parameter**


* `expr` \- Expression producing type `AggregateFunction(groupBitmap, UInt*)`.


**Return Value**


* Type value `UInt64`.


**Example**

```SQL
DROP TABLE IF EXISTS bitmap_column_expr_test2;
CREATE TABLE bitmap_column_expr_test2(tag_id String,z AggregateFunction(groupBitmap, UInt32)) ENGINE = CnchMergeTree ORDER BY tag_id;

INSERT INTO bitmap_column_expr_test2 VALUES ('tag1', bitmapBuild(cast([1,2,3,4,5,6,7,8,9,10] as Array(UInt32))));
INSERT INTO bitmap_column_expr_test2 VALUES ('tag2', bitmapBuild(cast([6,7,8,9,10,11,12,13,14,15] as Array(UInt32))));
INSERT INTO bitmap_column_expr_test2 VALUES ('tag3', bitmapBuild(cast([2,4,6,8,10,12] as Array(UInt32))));

SELECT groupBitmapOr(z) FROM bitmap_column_expr_test2 WHERE like(tag_id, 'tag%');
┌─groupBitmapOr(z)─┐
│             15   │
└──────────────────┘

SELECT arraySort(bitmapToArray(groupBitmapOrState(z))) FROM bitmap_column_expr_test2 WHERE like(tag_id, 'tag%');
┌─arraySort(bitmapToArray(groupBitmapOrState(z)))─┐
│ [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15]           │
└─────────────────────────────────────────────────┘
```


<span id="06da4cb2"></span>
### groupBitmapXor

Calculates the bitwise XOR for bitmap columns, returns a UInt64 type cardinality, and returns a bitmap object if the suffix \-State is added.

**Syntax**

```SQL
groupBitmapOr(expr)
```


**Parameter**


* `expr` \- Expression producing type `AggregateFunction(groupBitmap, UInt*)`.


**Return value**


* Type value `UInt64`.


**Example**

```SQL
DROP TABLE IF EXISTS bitmap_column_expr_test2;
CREATE TABLE bitmap_column_expr_test2(tag_id String, z AggregateFunction(groupBitmap, UInt32)) ENGINE = CnchMergeTree ORDER BY tag_id;

INSERT INTO bitmap_column_expr_test2 VALUES ('tag1', bitmapBuild(cast([1,2,3,4,5,6,7,8,9,10] as Array(UInt32))));
INSERT INTO bitmap_column_expr_test2 VALUES ('tag2', bitmapBuild(cast([6,7,8,9,10,11,12,13,14,15] as Array(UInt32))));
INSERT INTO bitmap_column_expr_test2 VALUES ('tag3', bitmapBuild(cast([2,4,6,8,10,12] as Array(UInt32))));

SELECT groupBitmapXor(z) FROM bitmap_column_expr_test2 WHERE like(tag_id, 'tag%');
┌─groupBitmapXor(z)─┐
│              10   │
└───────────────────┘

SELECT arraySort(bitmapToArray(groupBitmapXorState(z))) FROM bitmap_column_expr_test2 WHERE like(tag_id, 'tag%');
┌─arraySort(bitmapToArray(groupBitmapXorState(z)))─┐
│ [1,3,5,6,8,10,11,13,14,15]                       │
└──────────────────────────────────────────────────┘
```


<span id="04002b8f"></span>
### groupUniqArray

Create an array based on different parameter values. Memory consumption is the same as the uniqExact function.

The second version (with `max_size` parameter) limits the size of the resulting array to `max_size` elements.

**Syntax**

```SQL
groupUniqArray(x)
groupUniqArray(max_size)(x)
```


**Parameters**


* `x`— Input value.


**Return Value**


* Value Array. Type as Array.


**Example**

```SQL
select groupUniqArray(number) from numbers(10);
```


```SQL
┌─groupUniqArray(number)─────────┐
│ [0, 8, 3, 9, 7, 2, 1, 6, 4, 5] │
└────────────────────────────────┘
```


```SQL
select groupUniqArray(5)(number) from numbers(10); 
```


```SQL
┌─groupArray(5)(number)─┐
│ [0, 1, 2, 3, 4]       │
└───────────────────────┘
```


<span id="1e3dd800"></span>
### histogram

Calculates the adaptive histogram. It does not guarantee accurate results.

This function utilizes [Streaming Parallel Decision Tree Algorithm](http://jmlr.org/papers/volume11/ben-haim10a/ben-haim10a.pdf). When new data enters the function, the boundaries of the histogram bins are adjusted. Typically, the widths of the bins are unequal.

**Syntax**

```SQL
histogram(number_of_bins)(values)
```


**Param**


* `number_of_bins`— The cap for the number of bins in the histogram. The function automatically calculates the number of bins. It attempts to achieve the specified number of bins, but if it fails, it will use fewer bins.

* `values`— The expression that produces the input values.


**Return value**


* Array of tuples in the following format:

* [(lower_1, upper_1, height_1), ... (lower_N, upper_N, height_N)]


`lower`

— Lower bound of the bin.

`upper`

— Upper bound of the bin.

`height` — Calculated height of the bin.

**Example**

```SQL
SELECT histogram(5)(number + 1) FROM numbers(20);
```


```SQL
┌─histogram(5)(plus(number, 1))───────────────────────────────────────────┐
│ [(1,4.5,4),(4.5,8.5,4),(8.5,12.75,4.125),(12.75,17,4.625),(17,20,3.25)] │
└─────────────────────────────────────────────────────────────────────────┘
```


You can use the bar function to visualize histograms, for example:

```SQL
WITH histogram(5)(rand() % 100) AS hist
SELECT
    arrayJoin(hist).3 AS height,
    bar(height, 0, 6, 5) AS bar
FROM numbers(20);
```


```SQL
┌─height─┬─bar───┐
│  2.125 │ █▋    │
│   3.25 │ ██▌   │
│  5.625 │ ████▏ │
│  5.625 │ ████▏ │
│  3.375 │ ██▌   │
└────────┴───────┘
```


In this case, you should remember that you do not know the bounds of the histogram bins.

<span id="ba6000d4"></span>
### max

Aggregate function to calculate the maximum value of a set of values.

**Syntax**

```SQL
max(values)
```


**Param**


* `values`— Enter a value.


**Return value**


* Maximum. Type is the same as the value


**Example**

```SQL
SELECT max(number) FROM numbers(20);
```


```SQL
┌─max(number)─┐
│ 19          │
└─────────────┘
```


If a non\-aggregate function is needed to select up to two values, see `greatest`:

```SQL
SELECT greatest(a, b) FROM table;
```


<span id="3facaeed"></span>
### median

These `median*` functions are aliases for `quantile*`. They calculate the median of numerical value data samples.

Function:


* `median`— Alias for quantile.

* `medianDeterministic`— Alias for quantileDeterministic.

* `medianExact`— Alias for quantileExact.

* `medianExactWeighted`— Alias for quantileExactWeighted.

* `medianTiming`— Alias for quantileTiming.

* `medianTimingWeighted`— Alias for quantileTimingWeighted.

* `medianTDigest`— Alias for quantileTDigest.

* `medianTDigestWeighted`— Alias for quantileTDigestWeighted.

* `medianBFloat16`— Alias for quantileBFloat16.


<span id="ae89411e"></span>
### medianDeterministic

Alias for quantileDeterministic.

<span id="56201381"></span>
### medianExact

Alias for quantileExact.

<span id="244e2fe3"></span>
### medianExactWeighted

Alias for quantileExactWeighted.

<span id="bc2369f6"></span>
### medianTDigest

Alias for quantileTDigest.

<span id="ab58f791"></span>
### medianTDigestWeighted

Alias for quantileTDigestWeighted.

<span id="e0a29e2e"></span>
### medianTiming

Alias for quantileTiming.

<span id="bd6e5c3b"></span>
### medianTimingWeighted

Alias for quantileTimingWeighted.

<span id="dcae620f"></span>
### quantile

Calculates the approximate [quantile](https://en.wikipedia.org/wiki/Quantile) of a numerical data series.

This function uses [reservoir sampling,](https://en.wikipedia.org/wiki/Reservoir_sampling) with a maximum reservoir size of 8192, and samples using a random number generator. The result is uncertain. To obtain accurate quantiles, use the quantileExact function.

When using multiple functions at different levels in a query, the `quantile*` internal state does not merge (i.e., the query efficiency is lower than it should be). In this case, please use the quantile function.

**Grammar**

```SQL
quantile(level)(expr)
```


Alias: `median`.

**Param**


* `level`— Quantile level. Optional parameter. Constants between 0 and 1 as floating\-point numbers. We suggest using values within the range of `level` `[0.01, 0.99]`. Default: 0.5. level=0.5 calculates the median in functions.

* `Expression`— Evaluates the column values, resulting in a number, date, or datetime.


**Return value**


* Specifies the approximate percentile for a given level.


Type:


* Float64 for numerical data type input.

* If the input value is of `Date` type, then it's for Date.

* If the input value is of `DateTime` type, then it's for DateTime.


**Example**

```SQL
SELECT quantile(number) FROM numbers(10);
```


```SQL
┌─quantile(number)─┐
│ 4.5e+00          │
└──────────────────┘
```


<span id="81e03234"></span>
### quantileDeterministic

Calculates the approximate [percentile](https://en.wikipedia.org/wiki/Quantile) for a series of numerical data.

This function utilizes [reservoir sampling](https://en.wikipedia.org/wiki/Reservoir_sampling), with a reservoir size up to 8192, and the sampling algorithm is deterministic. The result is deterministic. To obtain accurate quantiles, use the quantileExact function.

When using multiple functions with different levels in queries `quantile*`, internal states do not merge (i.e., the efficiency of the query is less than it should be). In such cases, please use the quantile function.

**Syntax**

```SQL
quantileDeterministic(level)(expr, determinator)
sql
```


Alias: `medianDeterministic`.

**Param**


* `Level`— Quantile level. Optional param. Constant floating\-point numbers between 0 and 1. We recommend using values within the `level` range of `[0.01, 0.99]`. Default value: 0.5. `level=0.5` involved in the calculation of [digits](https://en.wikipedia.org/wiki/Median).

* `expr`—Calculates expressions on column values to yield a numerical, eitheror datetime.

* `determinator`—Uses hash values instead of random number generators in reservoir sampling algorithms to ensure the sample results are determinate. As a determinator, you may use any deterministic positive number, such as aID or anID. If the same determinator value occurs too frequently, the function will not work properly.


**Return value**


* Specifies the approximate median of the designated level.


Type:


* Floating\-point number for numerical data type input.

* If the input value is of `Date` type, it is a date.

* If the input value is of `DateTime` type, it is DateTime.


**Example**

```SQL
SELECT quantileDeterministic(number, 1) FROM numbers(10);
sql
```


```SQL
┌─quantileDeterministic(number, 1)─┐
│ 4.5e+00                          │
└──────────────────────────────────┘
```


<span id="bf3bc782"></span>
### quantileExact

Accurately calculates the quantiles of a numerical data series.

To acquire precise values, all passed values are combined into an array, and then partially sorted. Therefore, the function consumes `O(n)` memory, where `n` is the quantity of passed values. However, for a small number of values, this function is very effective.

When using multiple functions with different levels in the query using `quantile*`, the internal states do not merge (i.e., query efficiency is lower than it should be). In this case, please use the quantile function.

**Syntax**

```SQL
quantileExact(level)(expr)
```


Alias: `medianExact`.

**Parameters**


* `Level` — Quantile level. Optional parameter. A constant floating\-point number between 0 and 1. We recommend using values within the `level` range `[0.01, 0.99]`. Default value: 0.5. `level=0.5` uses the [number of digits](https://en.wikipedia.org/wiki/Median) in function calculation.

* `expr`— Evaluates column values through expression, resulting in a numerical data type, such as date or datetime.


**Return value**


* Specifies the quantile for a given level.


Type:


* Float64 is used for numerical data type input.

* If the input value is of the `Date` type, it is a Date.

* If the input value is of the `DateTime` type, it is DateTime.


**Example**

```SQL
SELECT quantileExact(number) FROM numbers(10);
```


```SQL
┌─quantileExact(number)─┐
│                     5 │
└───────────────────────┘
```


<span id="3388b8ed"></span>
### quantileExactWeighted

Accurately calculate the numerical data sequence's [quantiles](https://en.wikipedia.org/wiki/Quantile), considering the weight of each element.

To obtain an accurate value, all passed values are combined into an array and then partially sorted. Each value is calculated with its weight, as if it were a `current value`. The algorithm uses a hash table. Therefore, if the passed values are often repeated, this function consumes less RAM compared with quantileExact. You can use this function instead of `quantileExact` and specify a weight of 1.

When using multiple functions with different levels within a query `quantile*`, the internal state is not merged (i.e., the efficiency of the query is lower than it should be). In this case, use the quantile function.

**Syntax**

```SQL
quantileExactWeighted(level)(expr, weight)
```


Alias: `medianExactWeighted`.

**Parameter**


* `level`— Quantile level. Optional parameter. Constant floating\-point number between 0 and 1. We recommend using values within the `level` range `[0.01, 0.99]`. Default value: 0.5. `level=0.5` function calculates [digits](https://en.wikipedia.org/wiki/Median).

* `expr`— Expression for column values to derive numbers, dates, or datetime.

* `weight`— Weight column for sequence members. Weight is the frequency of occurrence of values.


**Return value**


* Specified level quantiles.


Type:


* Float64 for numeric data type input.

* If the input value has `Date` type, it is for date.

* If the input value has `DateTime` type, it is for DateTime.


**Example**

```SQL
CREATE TABLE IF NOT EXISTS test.functionQuantileExactWeighted (n UInt8, val UInt8) ENGINE=CnchMergeTree ORDER BY n;
INSERT INTO test.functionQuantileExactWeighted VALUES (0,3),(1,2),(2,1),(5,4);
SELECT quantileExactWeighted(n, val) FROM test.functionQuantileExactWeighted;
```


```SQL
┌─quantileExactWeighted(n, val)─┐
│                             1 │
└───────────────────────────────┘
```


<span id="038dce39"></span>
### quantileTDigest

[Using the t-digest](https://github.com/tdunning/t-digest/blob/master/docs/t-digest-paper/histo.pdf) algorithm to calculate approximate [quantiles](https://en.wikipedia.org/wiki/Quantile) for a sequence of numerical values.

Memory consumption is `log(n)`, where `n` is numerical. The result depends on the order of the executed queries and is uncertain.

The function's performance is less than that of quantile or quantileTiming. Considering the ratio of state size to precision, this function is much better than `quantile`.

When multiple `quantile*` functions with different levels are used in the query, internal states are not merged (i.e., the efficiency of the query is less than expected). In such cases, use the quantile function.

**Syntax**

```SQL
quantileTDigest(level)(expr)
```


Alias: `medianTDigest`.

**Param**


* `Level`— Quantile level. Optional param. Constants of floating\-point numbers between 0 to 1. We suggest using values within the `level` range `[0.01, 0.99]`. Default value: 0.5. `level=0.5` computations involve [digits](https://en.wikipedia.org/wiki/Median).

* `expr`— Express through the column values to derive numerical data type, i.e., Date or datetime.


**Return value**


* Specified level of approximate median.


Type:


* Float64 for numerical data type inputs.

* If the input value is of `Date` type, then for Date.

* If the input value has the type `DateTime`, then it is DateTime.


**Example**

```SQL
SELECT quantileTDigest(number) FROM numbers(10)
```


```SQL
┌─quantileTDigest(number)─┐
│ 4.5e+00                 │
└─────────────────────────┘
```


<span id="5e5767c1"></span>
### quantileTDigestWeighted

[Using the t-digest](https://github.com/tdunning/t-digest/blob/master/docs/t-digest-paper/histo.pdf) algorithm to calculate the approximate [percentiles](https://en.wikipedia.org/wiki/Quantile) of a series of numerical data. This function considers the weight of each member in the series. The maximum error is 1%. Memory consumption is, in terms of the quantity of values. `log(n)n`

The performance of this function is less than that of quantile or quantileTiming. From the ratio of state size to accuracy, this function is much better than `quantile`.

The result depends on the order in which queries are run and is uncertain.

When using multiple functions with different levels in the query `quantile*`, the internal state does not merge (i.e., the efficiency of the query is less than it should be). In this case, please use the quantile function.

<span id="76cb362d"></span>
### sum

Calculates the sum. Only works for numbers.

**Syntax**

```SQL
sum(num)
```


**Parameters**


* `num`: Column of numeric values. [(U)Int*](https://clickhouse.com/docs/sql-reference/data-types/int-uint), [Float*](https://clickhouse.com/docs/sql-reference/data-types/float), [Decimal*](https://clickhouse.com/docs/sql-reference/data-types/decimal).


**Returned value**


* The sum of the values. [(U)Int*](https://clickhouse.com/docs/sql-reference/data-types/int-uint), [Float*](https://clickhouse.com/docs/sql-reference/data-types/float), [Decimal*](https://clickhouse.com/docs/sql-reference/data-types/decimal).


**Example**


1. Create a table `employees` and insert some fictional employee data into it.

   ```SQL
   CREATE TABLE employees
   (
       `id` UInt32,
       `name` String,
       `salary` UInt32
   )
   ENGINE = Log
   ```
   

   ```SQL
   INSERT INTO employees VALUES
       (87432, 'John Smith', 45680),
       (59018, 'Jane Smith', 72350),
       (20376, 'Ivan Ivanovich', 58900),
       (71245, 'Anastasia Ivanovna', 89210);
   ```
   

2. Query for the total amount of the employee salaries using the `sum` function.

   Query:

   ```SQL
   SELECT sum(salary) FROM employees;
   ```
   

   Result:

   ```SQL
      ┌─sum(salary)─┐
   1. │      266140 │
      └─────────────┘
   ```
