---
title: "Higher-order functions"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/higher-order-functions"
---

<span id="运算符-lambda-params-expr-函数"></span>
## Operator, lambda(params, expr) function
Used to describe a lambda function that is passed to other higher-order functions. The left side of the arrow has a formal parameter, which can be an identifier or a tuple consisting of multiple identifiers. The right side of the arrow is an expression, in which any identifier from the list of formal parameters or any column name from the table can be used.
Example: `x -> 2 * x, str -> str != Referer.` Higher-order functions can only accept lambda functions as their parameters.
Higher-order functions can accept lambda functions with multiple parameters as their parameters, in which case the higher-order function needs to pass several arrays of equal length, which will be passed to the lambda parameters.
All other functions except 'arrayMap' and 'arrayFilter' can omit the first parameter (lambda function). In this case, it defaults to returning the element itself.
<span id="arraymap-func-arr1-…"></span>
### arrayMap(func, arr1, …)
The function 'func' returns the array from the original application to each element in the 'arr' array. Return each element of the 'arr' array from the original application in the 'func' function.
<span id="arrayfilter-func-arr1-…"></span>
### arrayFilter(func, arr1, …)
Return an array containing only the elements of 'arr1' for which 'func' returns a non-zero value.
Example:
SELECT arrayFilter(x -> x LIKE '%World%', ['Hello', 'abc World']) AS res
```plaintext
┌─res───────────┐
│ ['abc World'] │
└───────────────┘
```

SELECT arrayFilter( (i, x) -> x LIKE '%World%', arrayEnumerate(arr), ['Hello', 'abc World'] AS arr) AS res
<span id="arraycount-func-arr1-…"></span>
### ```plaintext
┌─res─┐
│ [2] │
└─────┘
```

<span id="arraycount-func-arr1-…"></span>
### arrayCount([func,] arr1, …)
Return the quantity of non-zero elements in the array 'arr', determined by the return value of 'func', if specified.
<span id="arrayexists-func-arr1-…"></span>
### arrayExists([func,] arr1, …)
Determine whether there are non-zero elements in the array 'arr'. If 'func' is specified, use the return value of 'func' to determine if the elements are non-zero.
<span id="arrayall-func-arr1-…"></span>
### arrayAll([func,] arr1, …)
Determine whether there are zero elements in the array 'arr'. If 'func' is specified, use the return value of 'func' to determine if the elements are zero.
<span id="arraysum-func-arr1-…"></span>
### arraySum([func,] arr1, …)
Calculate the sum of the array arr. If 'func' is specified, the sum is calculated using the return value of 'func'.
<span id="arrayfirst-func-arr1-…"></span>
### arrayFirst(func, arr1, …)
Returns the first matching element in the array, using 'func' to match all elements until the first match is found.
<span id="arrayfirstindex-func-arr1-…"></span>
### arrayFirstIndex(func, arr1, …)
Returns the index of the first matching element in the array, using 'func' to match all elements until the first match is found.
<span id="arraycumsum-func-arr1-…"></span>
### arrayCumSum([func,] arr1, …)
Returns the sum of a part of the source array. If a `function` is specified, it calculates the sum using the return values from `function`.
Example:
SELECT arrayCumSum([1, 1, 1, 1]) AS res
<span id="arraycumsumnonnegative-arr"></span>
### ```plaintext
┌─res──────────┐
│ [1, 2, 3, 4] │
└──────────────┘
```

<span id="arraycumsumnonnegative-arr"></span>
### arrayCumSumNonNegative(arr)
Similar to arrayCumSum, it returns the sum of a part of the source array. Unlike arrayCumSum, if the return value contains values smaller than zero, these values are replaced with zero and the calculation continues using zero. For example:
SELECT arrayCumSumNonNegative([1, 1, -4, 1]) AS res
<span id="arraysort-func-arr1-…"></span>
### ```plaintext
┌─res───────┐
│ [1,2,0,1] │
└───────────┘
```

<span id="arraysort-func-arr1-…"></span>
### arraySort([func,] arr1, …)
Returns the result of sorting `arr1` in ascending order. If a `func` function is specified, the sorting order is determined by the result of `func`.
[Schwartzian transform](https://en.wikipedia.org/wiki/Schwartzian_transform) is used to enhance sorting efficiency.
Example:
SELECT arraySort((x, y) -> y, ['hello', 'world'], [2, 1]);
```plaintext
┌─res────────────────┐
│ ['world', 'hello'] │
└────────────────────┘
```

Please note that NULL and NaN are at the end (NaN before NULL). For example:
```SQL
SELECT arraySort([1, nan, 2, NULL, 3, nan, 4, NULL])
```

<span id="arrayreversesort-func-arr1-…"></span>
### ```plaintext
┌─arraySort([1, nan, 2, NULL, 3, nan, 4, NULL])─┐
│ [1,2,3,4,nan,nan,NULL,NULL]                   │
└───────────────────────────────────────────────┘
```

<span id="arrayreversesort-func-arr1-…"></span>
### arrayReverseSort([func,] arr1, …)
Returns the result of descending sort for `arr1`. If a `func` function is specified, the sorting order is determined by the result of `func`.
Please note that NULL and NaN are at the end (NaN before NULL). For instance:
```SQL
SELECT arrayReverseSort([1, nan, 2, NULL, 3, nan, 4, NULL])
```

```plaintext
┌─arrayReverseSort([1, nan, 2, NULL, 3, nan, 4, NULL])─┐
│ [4,3,2,1,nan,nan,NULL,NULL]                          │
└──────────────────────────────────────────────────────┘
```
