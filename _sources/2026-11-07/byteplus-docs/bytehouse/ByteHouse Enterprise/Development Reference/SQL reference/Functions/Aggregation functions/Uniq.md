---
title: "Uniq"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/uniq-function"
---

<span id="uniq"></span>
# uniq
Calculates the approximate number of unique values for parameters.
**Syntax**
```sql
uniq(x[, ...])
```

**Param**
This function adopts a variable quantity of parameters. Params can be `Tuple`, `Array`, `Date`, `DateTime`, `String`, or a numerical type.
**Return value**

* UInt64 numerical value.

**Implementation Details**
Function:

* Calculate the hash values of all parameters in the Aggregate, then use them in the calculation.
* Use the Adaptive Sampling algorithm. For calculating the state, this function uses a sample of up to 65536 Element hash values.

This algorithm is very accurate and is also highly efficient for the CPU. If the search contains some such functions, then compared with other aggregate functions, `uniq` is almost equally fast.

* Provides results deterministically (it does not depend on the order of query processing).

We suggest using this function in almost all cases.
<span id="uniqcombined-agg-function-uniqcombined"></span>
# uniqCombined
Calculate the approximate quantity of different parameter values.
**Syntax**
```sql
uniqCombined(HLL_precision)(x[, ...])
```

The `uniqCombined` function is a good choice for calculating the quantity of distinct values.
**Parameter**
The function adopts a variable number of parameters. Parameters can be `Tuple`, `Array`, `Date`, `DateTime`, `String`, or numerical types.
`HLL_precision` is the logarithm of the number of cells based on 2 in [HyperLogLog](https://en.wikipedia.org/wiki/HyperLogLog). Optionally, you can use this function as `uniqCombined(x[, ...])`. The default value for `HLL_precision` is 17, which is an effective 96KiB of space (2^17 cells, each 6 bits).
**Return value**

* A UInt64 type number.

**Implementation details**
Function:

* Calculates the hash for all parameters in the Aggregate (64-bit hash for `String` Type and 32-bit for others) and then uses it in Calculating.
* Uses a combination of three algorithms: arrays, hash tables, and HyperLogLog with an error correction table.

For a small number of different values, use arrays. For more values, use hash tables. For a large quantity of data, use HyperLogLog, which occupies a fixed memory space.

* Provides results deterministically (it does not depend on the order of query Processing).

:::warning
Because it uses a 32-bit hash for non-`String` types, and there's a significant error in results when cardinality is much greater than `UINT_MAX`, with error rates increasing rapidly after hundreds of billions of different values, you should use uniqCombined64 in this scenario.
In comparison with the uniq function, `uniqCombined`

* Requires much less memory consumption.
* Provides several times higher calculating accuracy.
* Generally has slightly lower performance. In some cases, `uniqCombined` performs better than `uniq`, for example, when using distributed queries that transmit large aggregate states over the network.
:::
<span id="uniqcombined64"></span>
# uniqCombined64
Similar to uniqCombined, but uses a 64-bit hash for all data types.
<span id="uniqexact"></span>
# uniqExact
Calculates the exact number of different parameter values.
**Syntax**
```sql
uniqExact(x[, ...])
```

If you absolutely need an exact result, use the `uniqExact` function. Otherwise, use the uniq function.
The `uniqExact` function uses more memory than `uniq` as the state size grows unbounded with the increasing number of different values.
**Parameters**
This function accepts a variable number of parameters. Parameters can be `Tuple`, `Array`, `Date`, `DateTime`, `String`, or numerical type.
<span id="uniqhll12"></span>
# uniqHLL12
Calculate approximate quantities for different parameter values using [HyperLogLog](https://en.wikipedia.org/wiki/HyperLogLog) algorithm.
**Syntax**
```sql
uniqHLL12(x[, ...])
```

**Parameter**
This function adopts a variable number of parameters. The parameters can be `Tuple`, `Array`, `Date`, `DateTime`, `String`, or numerical type.
**Return value**

* A number of type UInt64.

**Implementation details**
Function:

* Calculate the hashes of all Params in the Aggregate and use it in Calculating.
* Use the HyperLogLog algorithm to approximate the Quantity of different Parameter values.

Use 4096 five-bit cells. The Size of the State is slightly more than 2.5KB. For small Data sets (<10K Elements), the results are not very Accurate (error up to 10%). However, for high-cardinality Data sets (10K-100M), the results are quite Accurate, with a Max error of about 1.6%. Starting from 100M, the estimation error increases, and the function will return very inaccurate results for data sets with extremely high cardinality (1B+ elements).

* Provides confirmed results (it does not depend on the order of Search Processing).

We do not recommend the use of this function. In most cases, use the uniq or uniqCombined Function.
