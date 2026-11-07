---
title: "Quantile"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/quantile-function"
---

<span id="quantile"></span>
# quantile
Calculate the approximate quantiles of a numeric sequence.
This function uses [reservoir sampling](https://en.wikipedia.org/wiki/Reservoir_sampling) with a reservoir size up to 8192 and samples using a random number generator.
The result is uncertain. To obtain an exact quantile, use the quantileExact function.
When using multiple different levels of `quantile*` in a query, the internal states are not combined (i.e., the query's efficiency is lower than in combined situations). In this case, use the quantiles function.
**Syntax**
```sql
quantile(level)(expr)
```

Alias: `median`.
**Parameters**

* `level` — Quantile level. Optional parameter. A float type constant from 0 to 1. We recommend the range of `level` values to be `[0.01, 0.99]`. Default value: 0.5. When `level=0.5`, the function calculates the median.
* `expr` — An evaluation expression of numeric data types data types, Date, or DateTime.

**Return value**

* Specifies the quantile for a certain level.

Type:

* Float64 for numeric data type inputs.
* Date if the input value is of `Date` type.
* DateTime if the input value is of `DateTime` type.

**Example**
Input table:
```text
┌─val─┐
│   1 │
│   1 │
│   2 │
│   3 │
└─────┘
```

Query:
```sql
SELECT quantile(val) FROM t
```

Result:
```text
┌─quantile(val)─┐
│           1.5 │
└───────────────┘
```

<span id="quantiledeterministic"></span>
# quantileDeterministic
Calculates the approximate quantile of a sequence of numbers.
This function uses [reservoir sampling](https://en.wikipedia.org/wiki/Reservoir_sampling), with a maximum storage of 8192 and a random number generator for sampling. The result is nondeterministic. To obtain precise quantiles, use the quantileExact function.
When multiple different levels of `quantile*` are used in one query, internal states are not combined (i.e., the query's efficiency is lower than when combined). In such cases, use the quantiles function.
**Syntax**
```sql
quantileDeterministic(level)(expr, determinator)
```

Alias: `medianDeterministic`.
**Parameters**

* `Level` — quantile level. Optional parameter. A float that ranges from 0 to 1. We recommend a `level` value range of `[0.01, 0.99]`. Default value: 0.5. When `level=0.5`, the function calculates the median.
* `Expr` — evaluation expression of numeric type data types, Date, or DateTime.

**Return value**

* Quantile designated level.

Type:

* Float64 used for numerical data type input.
* Date if the input value is of `Date` type.
* DateTime if the input value is of `DateTime` type.

**Example**
Input table:
```text
┌─val─┐
│   1 │
│   1 │
│   2 │
│   3 │
└─────┘
```

Query:
```sql
SELECT quantileDeterministic(val, 1) FROM t
```

Result:
```text
┌─quantileDeterministic(val, 1)─┐
│                           1.5 │
└───────────────────────────────┘
```

<span id="quantileexact-quantileexact"></span>
# quantileExact
Accurately calculate the quantile of a numeric sequence.
To calculate accurately, all input data is merged into a single array and partially sorted. Therefore, this function requires `O(n)` memory, where n is the number of input data. However, for a small amount of data, this function is still very effective.
When using multiple different levels of `quantile*` in a query, the internal state is not combined (i.e., the efficiency of the query is lower than in combined situations). In such cases, use the quantiles function.
**Syntax**
```sql
quantileExact(level)(expr)
```

Alias: `medianExact`.
**Parameters**

* `level` — Quantile level. Optional parameter. A constant of type float ranging from 0 to 1. We recommend a `level` value range of `[0.01, 0.99]`. Default value: 0.5. When `level=0.5`, the function calculates the median.
* `expr` — evaluation expression, data types as numeric typesdata types, Date or DateTime.

**Return value**

* Specifies the quantile for a given level.

Type:

* Float64 used for numeric data type input.
* Date If the input is of type `Date`.
* DateTime If the input is of type `DateTime`.

**Example**
Query:
```sql
SELECT quantileExact(number) FROM numbers(10)
```

Result:
```text
┌─quantileExact(number)─┐
│                     5 │
└───────────────────────┘
```

<span id="quantileexactlow-quantileexactlow"></span>
# quantileExactLow {#quantileexactlow}
Similar to `quantileExact`, it accurately calculates the [quantile](https://en.wikipedia.org/wiki/Quantile) of a numerical sequence.
To ensure accuracy, all input data is merged into a single array and fully sorted. The complexity of this [sorting algorithm](https://en.cppreference.com/w/cpp/algorithm/sort) is `O(N·log(N))`, where `N = std::distance(first, last)` is compared.
The return value depends on the quantile level and the number of elements selected, that is, if the level is 0.5, the function returns the lower median of an even number of elements and the median of an odd number of elements. The calculation of the median is similar to the implementation of [median_low](https://docs.python.org/3/library/statistics.html#statistics.median_low) in Python.
For all other levels, it returns the element value corresponding to the index of `level * size_of_array`.
For example:
```sql
SELECT quantileExactLow(0.1)(number) FROM numbers(10)

┌─quantileExactLow(0.1)(number)─┐
│                             1 │
└───────────────────────────────┘
```

When using multiple different levels of `quantile*` in a query, the internal state is not combined (meaning the query operates less efficiently than if combined). In this case, use the quantiles function.
**Syntax**
```sql
quantileExactLow(level)(expr)
```

Alias: `medianExactLow`.
**Parameters**

* `level` — Quantile level. Optional parameters. From 0 to 1, a float type constant. We recommend the `level` value range to be `[0.01, 0.99]`. Default value: 0.5. When `level=0.5`, the function calculates the median.
* `expr` — Evaluation expression, data types: Numerical Type, Date or DateTime.
* **Return value**
* Specifies the percentile for the level.
* Type:
* Float64 is used for numerical data type inputs.
* Date if the input value is of `Date` type.
* DateTime If the input is `DateTime` type.

**Example**
Search:
```sql
SELECT quantileExactLow(number) FROM numbers(10)
```

As a result:
```text
┌─quantileExactLow(number)─┐
│                        4 │
└──────────────────────────┘
```

<span id="quantileexacthigh"></span>
# quantileExactHigh
Similar to `quantileExact`, it accurately calculates the [quantile](https://en.wikipedia.org/wiki/Quantile) of a numerical sequence.
To ensure accurate calculation, all input data are merged into one array and then completely sorted. The complexity of this sorting [algorithm](https://en.cppreference.com/w/cpp/algorithm/sort) is `O(N·log(N))`, where `N = std::distance(first, last)` is compared.
The return value depends on the quantile level and the number of selected elements, i.e., if the level is 0.5, the function returns the lower median of even elements and the median of odd elements. The calculation of the median is similar to the implementation of [median_high](https://docs.python.org/3/library/statistics.html#statistics.median_high) used in Python.
For all other levels, return the element value at the index corresponding to the `level * size_of_array` value.
This implementation is completely similar to the current `quantileExact` implementation.
When using multiple different levels of `quantile*` in a query, the internal state is not combined (i.e., the query's efficiency is lower than when combined). In this case, use the quantiles function.
**Syntax**
```sql
quantileExactHigh(level)(expr)
```

Alias: `medianExactHigh`.
**Parameters**

* `level` — Quantile level. Optional parameter. A float constant from 0 to 1. We recommend the range of `level` values to be `[0.01, 0.99]`. Default: 0.5. When `level=0.5`, this function calculates the median.
* `expr` — Expression to be evaluated, with types: numerical Data type, Date or DateTime.
* **Return value**
* Specifies the percentile for the given level.
* Type:
* Float64 for numerical data type inputs.
* Date if the input value is of `Date` type.
* DateTime if the input value is of `DateTime` type.

**Example**
Search:
```sql
SELECT quantileExactHigh(number) FROM numbers(10)
```

As a result:
```text
┌─quantileExactHigh(number)─┐
│                         5 │
└───────────────────────────┘
```

<span id="quantileexactweighted"></span>
# quantileExactWeighted
Considering the weight of each element, then accurately calculates the [percentiles](https://en.wikipedia.org/wiki/Quantile) of the numerical sequence.
To compute accurately, all input data are merged into an array and partially sorted. Each input value must be computed by summing according to the `weight`. The algorithm uses a hash table. Due to this, the memory used when there is a lot of data repetition is less than quantileExact. You can use this function instead of `quantileExact` and specify `weight` as 1.
When using multiple different levels of `quantile*` in a query, the internal state is not combined (i.e., the query's efficiency is lower than if combined). In this case, use the quantiles function.
**Syntax**
```sql
quantileExactWeighted(level)(expr, weight)
```

Alias: `medianExactWeighted`.
**Parameters**

* `level` — Quantile level. Optional parameter. A constant of type float from 0 to 1. We recommend a `level` range of `[0.01, 0.99]`. Default: 0.5. When `level=0.5`, the function calculates the median.
* `expr` — Evaluation expression, type includes Data type, Date or DateTime.
* `weight` — Weight sequence. The weight is a numerical value that represents the occurrence of data.

**Return value**

* Specifies the quantile of a particular level.

Type:

* Float64 is used for numerical data type input.
* Date if the input is of `Date` type.
* DateTime if the input is of `DateTime` type.

**Example**
Input table:
```text
┌─n─┬─val─┐
│ 0 │   3 │
│ 1 │   2 │
│ 2 │   1 │
│ 5 │   4 │
└───┴─────┘
```

Search:
```sql
SELECT quantileExactWeighted(n, val) FROM t
```

As a result:
```text
┌─quantileExactWeighted(n, val)─┐
│                             1 │
└───────────────────────────────┘
```

<span id="quantiles"></span>
# quantiles
**Syntax**
```sql
quantiles(level1, level2, …)(x)
```

All quantile functions (quantile) also have corresponding functions: `quantiles`, `quantilesDeterministic`, `quantilesTiming`, `quantilesTimingWeighted`, `quantilesExact`, `quantilesExactWeighted`, `quantilesTDigest`. These functions calculate all the quantiles listed at one time and return an array of result values.
<span id="quantiletdigest"></span>
# quantileTDigest
Use [t-digest](https://github.com/tdunning/t-digest/blob/master/docs/t-digest-paper/histo.pdf) algorithm to calculate approximate [quantiles](https://en.wikipedia.org/wiki/Quantile) for a number sequence.
The maximum error is 1%. Memory consumption is `log(n)`, where `n` is the number of values. The result depends on the order in which queries are run and is uncertain.
This function performs less than quantile or quantileTiming. In terms of the ratio of state size to precision, this function is superior to `quantile`.
When using multiple different levels of `quantile*` in a query, the internal state is not combined (i.e., the operational efficiency of the query is lower than in combined situations). In this case, use the quantiles function.
**Syntax**
```sql
quantileTDigest(level)(expr)
```

Alias: `medianTDigest`.
**Parameters**

* `Level` — quantile levels. Optional parameter. A float constant from 0 to 1. We recommend that the `level` range be `[0.01, 0.99]`. Default value: 0.5. When `level=0.5`, the function calculates the median.
* `expr` — an evaluation expression, Type:Data types, Date or DateTime.

**Return value**

* Quantiles at the specified level.

Type:

* Float64 is used for numerical data type input.
* Date if the input value is of `Date` type.
* DateTime if the input value is of `DateTime` type.

**Example**
Query:
```sql
SELECT quantileTDigest(number) FROM numbers(10)
```

Result:
```text
┌─quantileTDigest(number)─┐
│                     4.5 │
└─────────────────────────┘
```

<span id="quantiletdigestweighted"></span>
# quantileTDigestWeighted
Calculates approximate quantiles of a number sequence using the t-digest al[quantiles of a number sequence using the t-digest](https://en.wikipedia.org/wiki/Quantile) algorithm. This function considers the weight of each sequence member. The maximum error is 1%. Memory consumption is `log(n)`, where `n` represents the number of values.
The performance of this function is lower than that of quantile or quantileTiming. In terms of the ratio of state size to accuracy, this function is superior to `quantile`.
The result depends on the order of the query execution and is uncertain.
When using multiple different levels of `quantile*` in a single query, internal states are not combined, resulting in lower efficiency than if combined. In this case, use the quantiles function.
**Syntax**
```sql
quantileTDigestWeighted(level)(expr, weight)
```

Alias: `medianTDigestWeighted`.
**Parameters**

* `level` — Quantile level. Optional parameter. A constant of type float ranging from 0 to 1. We recommend that the value for `level` range between `[0.01, 0.99]`. Default value: 0.5. When `level=0.5`, this function calculates the median.
* `expr` — evaluation expression, types include numerical data types, Date, or DateTime.
* `weight` — sequence of weights. Weight is a numeric occurrence of data.

**Return value**

* Specifies the percentile for a given level.

Type:

* Float64 is used for numeric data type input.
* Date if the input value is of `Date` type.
* DateTime if the input value is of `DateTime` type.

**Example**
Query:
```sql
SELECT quantileTDigestWeighted(number, 1) FROM numbers(10)
```

Result:
```text
┌─quantileTDigestWeighted(number, 1)─┐
│                                4.5 │
└────────────────────────────────────┘
```

<span id="quantiletiming"></span>
# quantileTiming
Calculates the quantiles of a numeric data series with fixed precision.
The result is deterministic (it does not depend on the query processing order). This function has been optimized for sequences that describe distributions of webpage loading times or backend response times.
When using multiple levels of `quantile*` in a query, the internal states are not combined (i.e., the query's efficiency is lower than in combined scenarios). In such cases, use the quantiles function.
**Syntax**
```sql
quantileTiming(level)(expr)
```

Alias: `medianTiming`.
**Parameters**

* `Level` — Quantile level. Optional parameters. A constant of type float ranging from 0 to 1. We recommend a range value for `level` of `[0.01, 0.99]`. Default value: 0.5. When `level=0.5`, this function calculates the median.
* `expr` — The evaluation expression returns a Float* type value.
   * If a negative value is entered, the result is unpredictable.
   * If the input value exceeds 30000 (page loading time exceeds 30s), we assume it as 30000.

**Precision**
The calculation is accurate if:

* The total number of values does not exceed 5670.
* The total value exceeds 5670, but the page loading time is less than 1024ms.

Otherwise, the calculation result will be rounded to the nearest multiple of 16 milliseconds.
:::warning
This function is more efficient and accurate than quantile for calculating page load time quantiles.
:::
**Return value**

* Specified level quantiles.

Type: `Float32`.
:::warning
If no values are passed to the function (when using `quantileTimingIf`), NaN is returned. The purpose of this is to distinguish these cases from those resulting in zero. See the ORDER BY clause for advisory on sorting `NaN` values.
:::
**Example**
Input table:
```text
┌─response_time─┐
│            72 │
│           112 │
│           126 │
│           145 │
│           104 │
│           242 │
│           313 │
│           168 │
│           108 │
└───────────────┘
```

Query:
```sql
SELECT quantileTiming(response_time) FROM t
```

Result:
```text
┌─quantileTiming(response_time)─┐
│                           126 │
└───────────────────────────────┘
```

<span id="quantiletimingweighted-quantiletimingweighted"></span>
# quantileTimingWeighted
Calculates the quantile [of a numerical sequence](https://en.wikipedia.org/wiki/Quantile) with definite precision based on the weight of each sequence member.
The result is deterministic (it does not depend on the order of query processing). The function is optimized for sequences describing distributions like webpage loading times or backend response times.
When using multiple different levels of `quantile*` in one query, the internal states are not combined (i.e., the query's performance is lower than when combined). In such cases, use the quantiles feature.
**Syntax**
```sql
quantileTimingWeighted(level)(expr, weight)
```

Alias: `medianTimingWeighted`.
**Parameters**

* `Level` — Quantile level. Optional parameter. A constant of type float from 0 to 1. We recommend a range for the `level` value of `[0.01, 0.99]`. Default value: 0.5. When `level=0.5`, the function calculates the [median](https://en.wikipedia.org/wiki/Median).
* `expr` — The evaluation expression returns a Float* type value.
   * If a negative value is input, the result is unpredictable.
   * If the input value exceeds 30000 (page load time greater than 30s), we assume it to be 30000.
* `weight` — weight sequence. Weight is a number that represents the occurrence of data.

**Precision**
The calculation is accurate, if:

* The total number of values does not exceed 5670.
* Total value exceeds 5670, but the page load time is less than 1024ms.

Otherwise, the result will be rounded to the nearest multiple of 16 milliseconds.
:::warning
This function is more efficient and accurate than quantile for calculating page load time quantiles.
:::
**Return Value**

* Specified quantile level.

Type: `Float32`.
:::warning
If no value is passed to the function (when using `quantileTimingIf`), NaN is returned. The purpose of this is to distinguish these cases from those that result in zero. See ORDER BY clause for considerations on sorting `NaN` values.
:::
**Example**
Input Table:
```text
┌─response_time─┬─weight─┐
│            68 │      1 │
│           104 │      2 │
│           112 │      3 │
│           126 │      2 │
│           138 │      1 │
│           162 │      1 │
└───────────────┴────────┘
```

Query:
```sql
SELECT quantileTimingWeighted(response_time, weight) FROM t
```

Result:
```text
┌─quantileTimingWeighted(response_time, weight)─┐
│                                           112 │
└───────────────────────────────────────────────┘
```

<span id="quantilestimingweighted"></span>
# quantilesTimingWeighted
Similar to `quantileTimingWeighted`, but accepts multiple quantile level parameters and returns an array consisting of these quantile values.
**Example**
Input table:
```text
┌─response_time─┬─weight─┐
│            68 │      1 │
│           104 │      2 │
│           112 │      3 │
│           126 │      2 │
│           138 │      1 │
│           162 │      1 │
└───────────────┴────────┘
```

Search:
```sql
SELECT quantilesTimingWeighted(0,5, 0.99)(response_time, weight) FROM t
```

As a result:
```text
┌─quantilesTimingWeighted(0.5, 0.99)(response_time, weight)─┐
│ [112,162]                                                 │
└───────────────────────────────────────────────────────────┘
```
