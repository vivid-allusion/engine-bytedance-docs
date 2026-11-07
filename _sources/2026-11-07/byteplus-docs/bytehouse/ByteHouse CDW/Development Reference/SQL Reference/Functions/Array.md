---
title: "Array"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-array"
---

<span id="a3aa937e"></span>
### **array**

Create an array from function arguments.

The parameters must be constant and of a type that has the least common type. At least one argument must be passed. Otherwise, it is unclear which type of array to create. That is, you cannot use this function to create an empty array (for this, use the "emptyArray\*" function described above).

**Syntax**

\*\*```SQL

array(x1, …)

```Plain Text
**
**Parameters**

* `x1,...` – Must be constant and of a type that has the least common type.

**Return Value**

* Returns a result of type “Array(T)” where “T” is the smallest common type among the passed arguments.

**Example**
**```SQL
SELECT array(1,2,3);
```


\*\*

\*\*```Plain Text

┌─array(1, 2, 3)─┐

│ [1, 2, 3] │

└────────────────┘

```Plain Text
**
<span id="94f5cb2d"></span>
### **arrayAll**
`func` returns 1 if all elements have a return value other than 0. `arr` otherwise, returns 0.
Please note that `arrayAll` is a higher-order function. You can pass a lambda function as the first argument to it.
**Syntax**
**```SQL
arrayAll([func,] arr1, …)
```


\*\*

**Parameters**


* `func` – High\-order functions must return UInt8

* `arr1,..` arrays serve as the input for functions


**Return Value**


* `func` returns 1 if all returned elements are non\-zero `arr`


**Example**

\*\*```SQL

SELECT arrayAll((x,y)\-\>x==y,[1,2,3],[4,5,6]);

```Plain Text
**
**```Plain Text
┌─arrayAll(lambda(tuple(x, y), equals(x, y)), [1, 2, 3], [4, 5, 6])─┐
│ 0                                                                 │
└───────────────────────────────────────────────────────────────────┘
```


\*\*

\*\*```SQL

SELECT arrayAll((x,y)\-\>x==y,[1,2,3],[1,2,3]);

```Plain Text
**
**```Plain Text
┌─arrayAll(lambda(tuple(x, y), equals(x, y)), [1, 2, 3], [1, 2, 3])─┐
│ 1                                                                 │
└───────────────────────────────────────────────────────────────────┘
```


\*\*

<span id="1e1f9007"></span>
### **empty**

Check if the input array is empty.

**Syntax**

\*\*```SQL

empty([x])

```Plain Text
**
If an array contains no elements, it is an empty array.
**Parameter**

* `[x]` — The input array of type array.

**Return Value**

* For an empty array, return `1`; for a non-empty array, return `0`.

**Type**: UInt8.
**Example**
**Query Statement**:
**```SQL
SELECT empty([]);
```


\*\*

**Result:** 

\*\*```Plain Text

┌─empty(array())─┐

│ 1 │

└────────────────┘

```Plain Text
**
<span id="2ff8ca9f"></span>
### **notEmpty**
Check if the input array is not empty.
**Syntax**
**```SQL
notEmpty([x])
```


\*\*

If an array contains at least one element, then it is a non\-empty array.

**Parameter**


* `[x]` — The input array of type array.


**Return Value**


* For an empty array, return `0`; for a non\-empty array, return `1`.


**Type**: UInt8.

**Example**

**Query Statement:** 

\*\*```SQL

SELECT notEmpty([1,2]);

```Plain Text
**
**Result:**
**```Plain Text
┌─notEmpty([1, 2])─┐
│                1 │
└──────────────────┘
```


\*\*

<span id="e2c02cbe"></span>
### **length**

Returns the number of elements in the array. The result type is UInt64. This function is also applicable to strings.

**Example**

\*\*```SQL

SELECT length(arr) FROM table

```Plain Text
**
<span id="a98b33ce"></span>
### **emptyArrayString**
Accepts no parameters and returns an empty array of the appropriate type.
<span id="9b6fe0cf"></span>
### **emptyArrayToSingle**
Accepts an empty array and returns an array containing only one default value element.
<span id="7ff31179"></span>
### **range**
Returns an array of integer numbers from start to end - 1 using step as the increment `start to end - 1 using end - 1 using step` as the increment step, supporting types include `UInt8`, `UInt16`, `UInt32`, `UInt64`, `Int8`, `Int16`, `Int32`, `Int64`.
**Grammar**
**```SQL
range([start, ] end [, step])
```


\*\*

**Parameters**


* `start` — The first element of the array. Optional. If `step` is set, `start` is also required, with a default value of 0.

* `end` — Counts up to `end` but does not include `end`, required.

* `step` — Determines the increment step length between each element in the array. Optional, with a default value of 1.


**Return Value**


* A numerical array from start to end \- 1 with step as the increment `start to end - 1 with send - 1 with step` as the increment step length.


**Notes**


* All parameters `start`, `end`, `step` must belong to one of the following types: `UInt8`, `UInt16`, `UInt32`, `UInt64`, `Int8`, `Int16`, `Int32`, `Int64`. The element data type of the result array must also belong to one of these aforementioned types as the minimum superclass of all input types.


**Example**

**Query statement:** 

\*\*```SQL

SELECT range(5), range(1, 5), range(1, 5, 2), range(\-1, 5, 2);

```Plain Text
**
**Result:**
**```Plain Text
┌─range(5)────┬─range(1, 5)─┬─range(1, 5, 2)─┬─range(-1, 5, 2)─┐
│ [0,1,2,3,4] │ [1,2,3,4]   │ [1,3]          │ [-1,1,3]        │
└─────────────┴─────────────┴────────────────┴─────────────────┘
```


\*\*

<span id="76b10c6f"></span>
### **arrayConcat**

Merge all arrays passed in the parameters.

**Syntax**

\*\*```SQL

arrayConcat(arrays)

```Plain Text
**
**Parameters**

* `arrays` - Any number of parameters of [array](https://clickhouse.com/docs/zh/sql-reference/functions/array-functions) type.

**Example**
**```SQL
SELECT arrayConcat([1, 2], [3, 4], [5, 6]) AS res
```


\*\*

\*\*```Plain Text

┌─res───────────┐

│ [1,2,3,4,5,6] │

└───────────────┘

```Plain Text
**
<span id="3b063750"></span>
### **arr**
Retrieve the element at index «n» from the array `arr`. `n` must be any integer type. Indexing in arrays starts from one. Negative indices are supported. In this case, it selects the corresponding element numbered from the end. For example, `arr[-1]` is the last item in the array.
**Syntax**
**```SQL
arr[n]
```


\*\*

If the index is beyond the array bounds, a default value is returned (zero for numbers, empty string for strings, etc.).

<span id="b61c75e9"></span>
### **has**

Check if the 'arr' array contains the 'elem' element. If the element is not in the array, return 0; if it is, return 1.

**Syntax**

\*\*```SQL

has(arr,elem)

```Plain Text
**
**Example**
**```SQL
SELECT has([1, 2, NULL], NULL)

┌─has([1, 2, NULL], NULL)─┐
│                       1 │
└─────────────────────────┘
```


\*\*

<span id="3bebdb01"></span>
### **hasAll**

Check if one array is a subset of another array.

**Syntax**

\*\*```SQL

hasAll(set, subset)

```Plain Text
**
**Parameter**

* `Set` - An array of any type that has a set of elements.
* `Subset` – Any type of array whose elements should be tested as a `set` subset.

**Return value**

* `1`, if `set` contains all elements of `subset`.
* `0`, otherwise.

**Special definitions**

* An empty array is a subset of any array.
* «Null» is treated as an element value in the array.
* Ignore the order of element values in both arrays.

**Example**
**```SQL
SELECT hasAll([], []) -- Return 1
SELECT hasAll([1, Null], [Null]) --Return 1
SELECT hasAll([1.0, 2, 3, 4], [1, 3]) -- Return 1
SELECT hasAll(['a', 'b'], ['a']) --Return 1
SELECT hasAll([1], ['a']) --Return 0
SELECT hasAll([[1, 2], [3, 4]], [[1, 2], [3, 5]]) --Return 0
```


\*\*

<span id="c11dd812"></span>
### **hasAny**

Check if two arrays have an intersection.

**Syntax**

\*\*```SQL

hasAny(array1, array2)

```Plain Text
**
**Parameters**

* `array1` – An array of any type with a set of elements.
* `array2` – An array of any type with a set of elements.

**Return Value**

* `1`, if `array1` and `array2` have an intersection.
* `0`, otherwise.

**Special Definitions**

* «Null» is treated as an element value in the array.
* Ignore the order of element values in the two arrays.

**Example**
**```SQL
SELECT hasAny([1], []) --Return 0
SELECT hasAny([Null], [Null, 1]) --Return 1
SELECT hasAny([-128, 1., 512], [1]) --Return 1
SELECT hasAny([[1, 2], [3, 4]], ['a', 'c']) --Return 0
SELECT hasAll([[1, 2], [3, 4]], [[1, 2], [1, 2]]) --Return 1
```


\*\*

<span id="c00e229c"></span>
### **hasSubstr**

Check if all elements of array2 appear in array1 in the same order. When `array1 = prefix + array2 + suffix`, the function will return 1.

**Syntax**

\*\*```SQL

hasSubstr(array1, array2)

```Plain Text
**
In other words, the function will check if all elements of `array2` are included in `array1`, similar to the `hasAll` function. Additionally, it will check if the order of elements in "array1" and "array2" is the same.
**Example**
**```SQL
hasSubstr([1,2,3,4], [2,3]) --Return 1
hasSubstr([1,2,3,4], [3,2]) --Return 0

hasSubstr([1,2,3,4], [1,2,3]) --Return 1
hasSubstr([1,2,3,4], [1,2,4]) --Return 0
```


\*\*

**Parameters**


* `array1` – Any type of array with a set of elements.

* `array2` – Any type of array with a set of elements.


**Return Value**


* If `array1` contains `array2`, return `1`.

* In other cases, return `0`.


**Special Attributes**


* When `array2` is an empty array, the function will return `1`.

* `Null` is treated as a value. In other words, `hasSubstr([1, 2, NULL, 3, 4], [2, 3])` will return `0`. However, `hasSubstr([1, 2, NULL, 3, 4], [2, NULL, 3])` will return `1`.

* The order of values in the two arrays will affect the function result.


**Example**

\*\*```SQL

SELECT hasSubstr([], []) \-\-Return 1

SELECT hasSubstr([1, Null], [Null]) \-\-Return 1

SELECT hasSubstr([1.0, 2, 3, 4], [1, 3]) \-\-Return 0

SELECT hasSubstr(['a', 'b'], ['a']) \-\-Return1

SELECT hasSubstr(['a', 'b' , 'c'], ['a', 'b']) \-\-Return 1

SELECT hasSubstr(['a', 'b' , 'c'], ['a', 'c']) \-\-Return 0

SELECT hasSubstr([[1, 2], [3, 4], [5, 6]], [[1, 2], [3, 4]]) \-\-Return 1

```Plain Text
**
<span id="e1763bf2"></span>
### **indexOf**
Returns the index of the first 'x' element in the array (starting from 1). If 'x' does not exist in the array, it returns 0.
**Syntax**
**```SQL
indexOf(arr,x)
```


\*\*

**Example**

\*\*```SQL

SELECT indexOf([1, 3, NULL, NULL], NULL)

```Plain Text
**
**```Plain Text
┌─indexOf([1, 3, NULL, NULL], NULL)─┐
│                                 3 │
└───────────────────────────────────┘
```


\*\*

Elements set to «NULL» will be treated as normal element values.

<span id="7f2933ea"></span>
### **arrayCount**

Returns the number of elements in the arr array for which func returns a non\-zero value. If "func" is not specified, it returns the number of non\-zero elements in the array.

Please note, this `arrayCount` is a higher\-order function. You can pass a lambda function as the first argument to it.

**Syntax**

\*\*```SQL

arrayCount([func,] arr1, …)

```Plain Text
**
**Parameters**

* `func` must return UInt8
* `arr1,..` arrays serve as the input to the function

**Return value**

* Number of elements in the arr array where func returns a non-zero value

**Example**
**```SQL
SELECT arrayCount((x,y)->x==y,[1,2,3],[1,5,3]);
```


\*\*

\*\*```Plain Text

┌─arrayCount(lambda(tuple(x, y), equals(x, y)), [1, 2, 3], [1, 5, 3])─┐

│ 2 │

└─────────────────────────────────────────────────────────────────────┘

```Plain Text
**
<span id="4ad8e17e"></span>
### **arrayCumSum**
Array of partial sums of elements in the source array (running sum). If `func` specifies this function, it transforms the values of the elements before summing them.
Please note, `arrayCumSum` is a higher-order function. You can pass a lambda function as the first argument to it.
**Syntax**
**```SQL
arrayCumSum([func,] arr1, …)
```


\*\*

**Parameters**


* `func` – a higher\-order function

* `arr1,..` arrays as input to the function


**Return values**


* Array of partial sums of elements in the source array.


**Example**

\*\*```SQL

SELECT arrayCumSum([1, 1, 1, 1]) AS res

```Plain Text
**
**```Plain Text
┌─res──────────┐
│ [1, 2, 3, 4] │
└──────────────┘
```


\*\*

\*\*```SQL

SELECT arrayCumSum(x\-\>x+1,[1, 1, 1, 1]) AS res

```Plain Text
**
**```Plain Text
┌─res──────────┐
│ [2, 4, 6, 8] │
└──────────────┘
```


\*\*

<span id="3978dd15"></span>
### **arrayCumSumNonNegative**

Similar to `arrayCumSum`, it returns an array of partial sums of elements in the source array (running sum). The difference is that in `arrayCumSum`, when the returned values contain values less than zero, these values will be replaced by zero, and subsequent calculations will be performed using zero as the parameter. For example:

Please note that this `arraySumNonNegative` is a higher\-order function. You can pass a lambda function as the first parameter to it.

**Syntax**

\*\*```SQL

arrayCumSumNonNegative([func,] arr1, …)

```Plain Text
**
**Parameters**

* `func` – A higher-order function.
* `arr1` array as the input to a function

**Return value**

* Array of the partial sums of the elements in the source array

**Example**
**```SQL
SELECT arrayCumSumNonNegative([1, 1, -4, 1]) AS res
```


\*\*

\*\*```Plain Text

┌─res──────────┐

│ [1, 2, 0, 1] │

└──────────────┘

```Plain Text
**
**```SQL
SELECT arrayCumSumNonNegative(x->x-2,[1, 1, -4, 3]) AS res
```


\*\*

\*\*```Plain Text

┌─res──────────┐

│ [0, 0, 0, 1] │

└──────────────┘

```Plain Text
**
<span id="412354b1"></span>
### **countEqual**
Returns the count of elements in the array that are equal to x. Equivalent to arrayCount(elem -> elem = x, arr).
`NULL` values are treated as distinct element values.
**Example**
**```SQL
SELECT countEqual([1, 2, NULL, NULL], NULL)
```


\*\*

\*\*```Plain Text

┌─countEqual([1, 2, NULL, NULL], NULL)─┐

│ 2 │

└──────────────────────────────────────┘

```Plain Text
**
<span id="b6b24f6a"></span>
### **arrayEnumerate**
Returns an array [1, 2, 3, ..., length(arr)]
This function is usually used in conjunction with ARRAY JOIN. It allows calculation for each array once after applying ARRAY JOIN.
**Example**
**```SQL
SELECT
    count() AS Reaches,
    countIf(num = 1) AS Hits
FROM test.hits
ARRAY JOIN
    GoalsReached,
    arrayEnumerate(GoalsReached) AS num
WHERE CounterID = 160656
LIMIT 10
```


\*\*

\*\*```Plain Text

┌─Reaches─┬──Hits─┐

│ 95606 │ 31406 │

└─────────┴───────┘

```Plain Text
**
In this example, Reaches are the number of conversions (the string received after applying ARRAY JOIN), and Hits are the number of views (the string before applying ARRAY JOIN). In this special case, you can achieve the same result more easily:
**```SQL
SELECT
    sum(length(GoalsReached)) AS Reaches,
    count() AS Hits
FROM test.hits
WHERE (CounterID = 160656) AND notEmpty(GoalsReached)
```


\*\*

\*\*```Plain Text

┌─Reaches─┬──Hits─┐

│ 95606 │ 31406 │

└─────────┴───────┘

```Plain Text
**
This function can also be used in higher order functions. For example, you can use it to get the array indices of elements matching a condition.
<span id="ab50bb93"></span>
### **arrayEnumerateUniq**
Returns an array of the same size as the source array, where each element represents the number of occurrences of the element at that index in the source array. For example: arrayEnumerateUniq([10,20,10,30]) = [1,1,2,1].
This function is very useful when using ARRAY JOIN and aggregating array elements.
**Example**
**```SQL
SELECT
    Goals.ID AS GoalID,
    sum(Sign) AS Reaches,
    sumIf(Sign, num = 1) AS Visits
FROM test.visits
ARRAY JOIN
    Goals,
    arrayEnumerateUniq(Goals.ID) AS num
WHERE CounterID = 160656
GROUP BY GoalID
ORDER BY Reaches DESC
LIMIT 10
```


\*\*

\*\*```Plain Text

┌──GoalID─┬─Reaches─┬─Visits─┐

│ 53225 │ 3214 │ 1097 │

│ 2825062 │ 3188 │ 1097 │

│ 56600 │ 2803 │ 488 │

│ 1989037 │ 2401 │ 365 │

│ 2830064 │ 2396 │ 910 │

│ 1113562 │ 2372 │ 373 │

│ 3270895 │ 2262 │ 812 │

│ 1084657 │ 2262 │ 345 │

│ 56599 │ 2260 │ 799 │

│ 3271094 │ 2256 │ 812 │

└─────────┴─────────┴────────┘

```Plain Text
**
In this example, each GoalID calculates the number of conversions (each element in the goal nested data structure is a reached goal, which we call a conversion) and the number of sessions. If there is no ARRAY JOIN, we would count the total number of sessions (Sign). However, in this special case, with rows multiplied by the nested Goals structure, in order to count each session once afterwards, we apply a condition to the value of the arrayEnumerateUniq(Goals.ID) function.
The arrayEnumerateUniq function can use multiple arrays of the same size as the argument. In this case, uniqueness is considered for tuples of elements at the same positions across all arrays.
**```SQL
SELECT arrayEnumerateUniq([1, 1, 1, 2, 2, 2], [1, 1, 2, 1, 1, 2]) AS res
```


\*\*

\*\*```Plain Text

┌─res───────────┐

│ [1,2,1,1,2,1] │

└───────────────┘

```Plain Text
**
This is necessary when using ARRAY JOIN with nested data structures and further aggregating across multiple elements within this structure.
<span id="c3adedd0"></span>
### **arrayPopBack**
Remove the last item from the array.
**```SQL
arrayPopBack(array)
```


\*\*

**Parameter**


* `array` – Array.


**Example**

\*\*```SQL

SELECT arrayPopBack([1, 2, 3]) AS res

```Plain Text
**
**```Plain Text
┌─res───┐
│ [1,2] │
└───────┘
```


\*\*

<span id="d5dd3c8a"></span>
### **arrayPopFront**

Remove the first item from the array.

**Syntax**

\*\*```SQL

arrayPopFront(array)

```Plain Text
**
**Parameter**

* `array` – Array.

**Example**
**```SQL
SELECT arrayPopFront([1, 2, 3]) AS res
```


\*\*

\*\*```Plain Text

┌─res───┐

│ [2,3] │

└───────┘

```Plain Text
**
<span id="a2dc172a"></span>
### **arrayPushBack**
Add an element to the end of an array.
**Syntax**
**```SQL
arrayPushBack(array, single_value)
```


\*\*

**Parameters**


* `array` – Array.

* `single_value` – Single value. Only numbers can be added to arrays of numbers, and only strings can be added to arrays of strings. When numbers are added, ByteHouse will automatically set the data type of the array to `single_value` type.


**Example**

\*\*```SQL

SELECT arrayPushBack(['a'], 'b') AS res

```Plain Text
**
**```Plain Text
┌─res───────┐
│ ['a','b'] │
└───────────┘
```


\*\*

<span id="83bcb21c"></span>
### **arrayPushFront**

Add an element to the beginning of an array.

**Syntax**

\*\*```SQL

arrayPushFront(array, single_value)

```Plain Text
**
**Parameters**

* `array` – Array.
* `single_value` – Single value. Only numbers can be added to an array of numbers, and only strings can be added to an array of strings. When adding numbers, ByteHouse automatically sets the data type of the array to `single_value` type. `This function adds a «NULL» element to the array, converting the type of the array elements to` Nullable`.

**Example**
**```SQL
SELECT arrayPushFront(['b'], 'a') AS res
```


\*\*

\*\*```Plain Text

┌─res───────┐

│ ['a','b'] │

└───────────┘

```Plain Text
**
<span id="13ce3e0e"></span>
### **arrayResize**
Change the length of the array.
**Syntax**
**```SQL
arrayResize(array, size[, extender])
```


\*\*

**Parameters:** 


* `array` — The array.

* `size` — The required length of the array.

   * If `size` is smaller than the original size of the array, the array will be truncated from the right.

* If `size` is greater than the initial size of the array, the array will be extended to the right using `extender` value or the default value of the data type of the array items.

* `extender` — The value used to extend the array. It can be ’NULL’.


**Return value:** 

An array of `size` length.

**Example**

\*\*```SQL

SELECT arrayResize([1], 3);

```Plain Text
**
**```Plain Text
┌─arrayResize([1], 3)─┐
│ [1,0,0]             │
└─────────────────────┘
```


\*\*

\*\*```SQL

SELECT arrayResize([1], 3, NULL);

```Plain Text
**
**```Plain Text
┌─arrayResize([1], 3, NULL)─┐
│ [1,NULL,NULL]             │
└───────────────────────────┘
```


\*\*

<span id="2f9a0896"></span>
### **arraySlice**

Returns a subarray, containing elements of a specified length from a specified position.

**Syntax**

\*\*```SQL

arraySlice(array, offset[, length])

```Plain Text
**
**Parameters**

* `array` – Array.
* `offset` – Offset in the array. A positive value indicates the offset from the left, while a negative value indicates the indentation from the right. Array indices start from 1.
* `Length` of the subarray. If a negative value is specified, the function returns `[offset, array_length - length]`. If this value is omitted, the function returns `[offset, the_end_of_array]`.

**Example**
**```SQL
SELECT arraySlice([1, 2, NULL, 4, 5], 2, 3) AS res
```


\*\*

\*\*```Plain Text

┌─res────────┐

│ [2,NULL,4] │

└────────────┘

```Plain Text
**
Array elements set to «NULL» are treated as regular array element values.
<span id="c3ebf00f"></span>
### **arraySort**
Sorts the elements of the `arr` array in ascending order. If a `func` function is specified, the sorting order is determined by the results of the `func` function call. If the `func` accepts multiple parameters, the `arraySort` function will also parse the same number of array parameters as the `func` function's parameters. More detailed examples are found at the end of `arraySort`.
**Grammar**
**```SQL
arraySort([func,] arr, ...)
```


\*\*

**Integer sorting example:** 

\*\*```SQL

SELECT arraySort([1, 3, 3, 0]);

```Plain Text
**
**```Plain Text
┌─arraySort([1, 3, 3, 0])─┐
│ [0,1,3,3]               │
└─────────────────────────┘
```


\*\*

**String sorting example:** 

\*\*```SQL

SELECT arraySort(['hello', 'world', '!']);

```Plain Text
**
**```Plain Text
┌─arraySort(['hello', 'world', '!'])─┐
│ ['!','hello','world']              │
└────────────────────────────────────┘
```


\*\*

`NULL`, `NaN` and `Inf` sorting order:

\*\*```SQL

SELECT arraySort([1, nan, 2, NULL, 3, nan, \-4, NULL, inf, \-inf]);

```Plain Text
**
**```Plain Text
┌─arraySort([1, nan, 2, NULL, 3, nan, -4, NULL, inf, -inf])─┐
│ [-inf,-4,1,2,3,inf,nan,nan,NULL,NULL]                     │
└───────────────────────────────────────────────────────────┘
```


\*\*


* `-Inf` is the first in the array.

* `NULL` is the last in the array.

* `NaN` is in front of `NULL`.

* `Inf` is in front of `NaN`.


Note: `arraySort` is a higher\-order function. You can pass a lambda function as the first argument to it. In this case, the sorting order is determined by the result of the lambda function call.

Let's take a look at the following example:

\*\*```SQL

SELECT arraySort((x) \-\> \-x, [1, 2, 3]) as res;

```Plain Text
**
**```Plain Text
┌─res─────┐
│ [3,2,1] │
└─────────┘
```


\*\*

For each element of the source array, the lambda function returns a sorting key, i.e. [1 \-\> \-1, 2 \-\> \-2, 3 \-\> \-3]. Since the `arraySort` function sorts the keys in ascending order, the result is [3, 2, 1]. Thus, the `(x) -> -x` lambda function sets the sorting to descending order.

The lambda function can accept multiple arguments. In this case, you need to pass arrays to `arraySort` that match the number of lambda parameters. The function uses the elements from the first input array to compose the return result; it uses the subsequent arrays as sorting keys. For example:

\*\*```SQL

SELECT arraySort((x, y) \-\> y, ['hello', 'world'], [2, 1]) as res;

```Plain Text
**
**```Plain Text
┌─res────────────────┐
│ ['world', 'hello'] │
└────────────────────┘
```


\*\*

Here, the sorting keys for the corresponding elements of the first array (['hello', 'world']) are defined in the second array ([2, 1]), i.e., ['hello' \-\> 2, 'world' \-\> 1]. Since `x` is not used in the lambda function, the actual values in the source array do not influence the order of the results. Therefore, 'world' will be the first element in the results, and 'hello' will be the second element.

Other examples are as follows.

\*\*```SQL

SELECT arraySort((x, y) \-\> y, [0, 1, 2], ['c', 'b', 'a']) as res;

```Plain Text
**
**```Plain Text
┌─res─────┐
│ [2,1,0] │
└─────────┘
```


\*\*

\*\*```SQL

SELECT arraySort((x, y) \-\> \-y, [0, 1, 2], [1, 2, 3]) as res;

```Plain Text
**
**```Plain Text
┌─res─────┐
│ [2,1,0] │
└─────────┘
```


\*\*

<span id="94a93b0a"></span>
### **arrayReverseSort**

Sorts the elements of the `arr` array in descending order. If a `func` function is specified, the sorting order is determined by the results of the `func` function call. If the `func` accepts multiple parameters, the `arrayReverseSort` function will also resolve arrays with the same number of parameters as the `func` function. More detailed examples can be found at the end of `arrayReverseSort`.

**Syntax**

\*\*```SQL

arrayReverseSort([func,] arr, ...)

```Plain Text
**
**Examples**
**Integer Sorting:**
**```SQL
SELECT arrayReverseSort([1, 3, 3, 0]);
```


\*\*

\*\*```Plain Text

┌─arrayReverseSort([1, 3, 3, 0])─┐

│ [3,3,1,0] │

└────────────────────────────────┘

```Plain Text
**
**String Sorting:**
**```SQL
--String sorting
SELECT arrayReverseSort(['hello', 'world', '!']);
```


\*\*

\*\*```Plain Text

┌─arrayReverseSort(['hello', 'world', '!'])─┐

│ ['world','hello','!'] │

└───────────────────────────────────────────┘

```Plain Text
**
**`NULL`, `NaN`, and `Inf` Sorting Order:**
**```SQL
SELECT arrayReverseSort([1, nan, 2, NULL, 3, nan, -4, NULL, inf, -inf]) as res;
```


\*\*

\*\*```Plain Text

┌─res───────────────────────────────────┐

│ [inf,3,2,1,\-4,\-inf,nan,nan,NULL,NULL] │

└───────────────────────────────────────┘

```Plain Text
**

* `Inf` is the first in the array.
* `NULL` is the last in the array.
* `NaN` is before `NULL`.
* `-Inf` is before `NaN`.

Note: `arraySort` is a higher-order function. You can pass a lambda function as the first parameter to it. As shown in the example below.
**```SQL
SELECT arrayReverseSort((x) -> -x, [1, 2, 3]) as res;
```


\*\*

\*\*```Plain Text

┌─res─────┐

│ [1,2,3] │

└─────────┘

```Plain Text
**
Arrays are sorted as follows:

1. First, sort the source array ([1, 2, 3]) based on the results of calling a lambda function. The result is [3, 2, 1].
2. Reverse the array obtained from the previous step. Thus, the final result is [1, 2, 3].

A lambda function can accept multiple parameters. In this case, you need to pass an array with the same number of elements as the lambda parameters to `arrayReverseSort`. The function forms the return result using elements from the first input array; the subsequent arrays are used as sorting keys. For example:
**```SQL
SELECT arrayReverseSort((x, y) -> y, ['hello', 'world'], [2, 1]) as res;
```


\*\*

\*\*```Plain Text

┌─res───────────────┐

│ ['hello','world'] │

└───────────────────┘

```Plain Text
**
In this example, the arrays are sorted as follows:

1. Firstly, sort the source array (['hello', 'world']) based on the result of a lambda function call. Within the second array ([2,1]), the sorting keys for the corresponding elements in the source array are defined. Thus, the sorting result is ['world', 'hello'].
2. Reverse the sorted array obtained in the previous step. Therefore, the final result is ['hello', 'world'].

Additional examples are shown below.
**```SQL
SELECT arrayReverseSort((x, y) -> y, [4, 3, 5], ['a', 'b', 'c']) AS res;
```


\*\*

\*\*```Plain Text

┌─res─────┐

│ [5,3,4] │

└─────────┘

```Plain Text
**
**```SQL
SELECT arrayReverseSort((x, y) -> -y, [4, 3, 5], [1, 2, 3]) AS res;
```


\*\*

\*\*```Plain Text

┌─res─────┐

│ [4,3,5] │

└─────────┘

```Plain Text
**
<span id="5338f539"></span>
### **arrayUniq**
If one parameter is passed, it calculates the number of distinct elements in the array. If multiple parameters are passed, it calculates the number of tuples of distinct elements at the corresponding positions across multiple arrays.
**Syntax**
**```SQL
arrayUniq(arr, ...)
```


\*\*

To obtain a list of unique items in an array, you can use arrayReduce('groupUniqArray', arr).

<span id="c2ac7934"></span>
### **arrayJoin**

This is a very useful function.

**Syntax**

\*\*```SQL

arrayJoin(arr)

```Plain Text
**
Regular functions do not change the number of rows in the result set, but simply calculate the values in each row (map). Aggregate functions compress multiple rows into one row (fold or reduce). The 'arrayJoin' function takes each row and expands them into multiple rows (unfold).
This function takes an array as a parameter and duplicates the row in the result set by the number of elements in the array. Besides the values in the column where this function is applied, simply duplicate all values in the column; they are replaced by the corresponding array values.
Multiple `arrayJoin` functions can be used in a query. In this situation, the conversion is performed multiple times.
Please note the ARRAY JOIN syntax in the SELECT query, which offers a wider range of possibilities.
**Example**
**```SQL
SELECT arrayJoin([1, 2, 3] AS src) AS dst, 'Hello', src
```


\*\*

\*\*```Plain Text

┌─dst─┬─'Hello'─┬─src─────┐

│ 1 │ Hello │ [1,2,3] │

│ 2 │ Hello │ [1,2,3] │

│ 3 │ Hello │ [1,2,3] │

└─────┴───────────┴─────────┘

```Plain Text
**
<span id="a2b575fe"></span>
### **arrayDifference**
Calculates the differences between adjacent array elements. Returns an array where the first element is 0, and the second is the difference `a[1] - a[0]` and so on. The type of elements in the result array is determined by the type inference rules for subtraction, such as `UInt8` - `UInt8` = `Int16`.
**Syntax**
**```SQL
arrayDifference(array)
```


\*\*

**Parameters**


* `array` – of type array.


**Return Value**

Returns an array of differences between adjacent elements.

**Type:**  UInt\*, Int\*, Float\*.

**Example**

**Query Statement:** 

\*\*```SQL

SELECT arrayDifference([1, 2, 3, 4]);

```Plain Text
**
**Result:**
**```Plain Text
┌─arrayDifference([1, 2, 3, 4])─┐
│ [0,1,1,1]                     │
└───────────────────────────────┘
```


\*\*

Example of overflow due to the result type being Int64:

**Query Statement:** 

\*\*```SQL

SELECT arrayDifference([0, 10000000000000000000]);

```Plain Text
**
**Result:**
**```Plain Text
┌─arrayDifference([0, 10000000000000000000])─┐
│ [0,-8446744073709551616]                   │
└────────────────────────────────────────────┘
```


\*\*

<span id="6d8bc0cf"></span>
### **arrayDistinct**

Returns an array containing all distinct elements from all arrays.

**Syntax**

\*\*```SQL

arrayDistinct(array)

```Plain Text
**
**Parameters**

* `array` – An array type.

**Return Value**
Returns an array containing distinct elements.
**Example**
**Query Statement:**
**```SQL
SELECT arrayDistinct([1, 2, 2, 3, 1]);
```


\*\*

**Result:** 

\*\*```Plain Text

┌─arrayDistinct([1, 2, 2, 3, 1])─┐

│ [1,2,3] │

└────────────────────────────────┘

```Plain Text
**
<span id="ae83e555"></span>
### **arrayEnumerateDense**
Returns an array of the same size as the source array, indicating the first occurrence position of each element in the source array. For example: arrayEnumerateDense([10,20,10,30]) = [1,2,1,3].
**Syntax**
**```SQL
arrayEnumerateDense(arr)
```


\*\*

**Example**

\*\*```SQL

SELECT arrayEnumerateDense([10, 20, 10, 30])

```Plain Text
**
**```Plain Text
┌─arrayEnumerateDense([10, 20, 10, 30])─┐
│ [1,2,1,3]                             │
└───────────────────────────────────────┘
```


\*\*

<span id="fb0ceefe"></span>
### **arrayIntersect**

Returns the intersection of all array elements.

**Syntax**

\*\*```SQL

arrayIntersect(arr)

```Plain Text
**
**Example**
**```SQL
SELECT
    arrayIntersect([1, 2], [1, 3], [2, 3]) AS no_intersect,
    arrayIntersect([1, 2], [1, 3], [1, 4]) AS intersect
```


\*\*

\*\*```Plain Text

┌─no_intersect─┬─intersect─┐

│ [] │ [1] │

└──────────────┴───────────┘

```Plain Text
**
<span id="24151b8c"></span>
### **arrayReduce**
Applies an aggregation function to the array elements and returns the result. The names of the aggregation functions are passed as strings in quotes, like `'max'` and `'sum'`. When using parameterized aggregation functions, the parameters are indicated after the function name in parentheses, like “uniqUpTo(6)”.
**Syntax**
**```SQL
arrayReduce(agg_func, arr1, arr2, ..., arrN)
```


\*\*

**Parameters**


* `agg_func` — The name of the aggregation function, which should be a constant string.

* `arr` — Any number of array type columns as parameters for the aggregation function.


**Return Value**

**Examples**

**Query statement:** 

\*\*```SQL

SELECT arrayReduce('max', [1, 2, 3]);

```Plain Text
**
**Result:**
**```Plain Text
┌─arrayReduce('max', [1, 2, 3])─┐
│                             3 │
└───────────────────────────────┘
```


\*\*

If the aggregate function takes multiple parameters, it must be applied to multiple arrays of the same size.

**Query statement:** 

\*\*```SQL

SELECT arrayReduce('maxIf', [3, 5], [1, 0]);

```Plain Text
**
**Result:**
**```Plain Text
┌─arrayReduce('maxIf', [3, 5], [1, 0])─┐
│                                    3 │
└──────────────────────────────────────┘
```


\*\*

**Example with parameterized aggregate functions:** 

**Query statement:** 

\*\*```SQL

SELECT arrayReduce('uniqUpTo(3)', [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]);

```Plain Text
**
**Result:**
**```Plain Text
┌─arrayReduce('uniqUpTo(3)', [1, 2, 3, 4, 5, 6, 7, 8, 9, 10])─┐
│                                                           4 │
└─────────────────────────────────────────────────────────────┘
```


\*\*

<span id="c6832813"></span>
### **arrayReduceInRanges**

Applies the aggregate function to array elements within specified ranges and returns an array containing results corresponding to each range. This function returns the same result as multiple `arrayReduce(agg_func, arraySlice(arr1, index, length), ...)`.

**Syntax**

\*\*```SQL

arrayReduceInRanges(agg_func, ranges, arr1, arr2, ..., arrN)

```Plain Text
**
**Parameter**

* `agg_func` — The name of the aggregation function, should be a constant string.
* `ranges` — The ranges to aggregate should be an array of tuples, each containing a range of index and length.
* `arr` — Any number of array type columns as the arguments for the aggregation function.

**Return Value**

* Array containing the results of aggregation functions within the specified ranges.

**Type:** Array.
**Example**
**Query Statement:**
**```SQL
SELECT arrayReduceInRanges(
    'sum',
    [(1, 5), (2, 3), (3, 4), (4, 4)],
    [1000000, 200000, 30000, 4000, 500, 60, 7]
) AS res
```


\*\*

**Result:** 

\*\*```Plain Text

┌─res─────────────────────────┐

│ [1234500,234000,34560,4567] │

└─────────────────────────────┘

```Plain Text
**
<span id="be89fc28"></span>
### **arrayReverse**
Returns an array of the same size as the original, containing elements in the reverse order.
**Syntax**
**```SQL
arrayReverse(arr)
```


\*\*

**Example**

\*\*```SQL

SELECT arrayReverse([1, 2, 3])

```Plain Text
**
**```Plain Text
┌─arrayReverse([1, 2, 3])─┐
│ [3,2,1]                 │
└─────────────────────────┘
```


\*\*

<span id="18c69d71"></span>
### **reverse**

Has the same effect as "arrayReverse".

**Syntax**

\*\*```SQL

reverse(arr)

```Plain Text
**
<span id="646fcded"></span>
### **arrayFlatten**
Flattens nested arrays.
**Function:**

* Suitable for nested arrays of any depth.
* Does not alter arrays that are already flattened.

The flattened array contains all elements from all source arrays.
**Syntax**
**```SQL
flatten(array_of_arrays)
```


\*\*

**Alias:**  `flatten`.

**Parameters**


* `array_of_arrays` — Nested arrays. For example: `[[1,2,3], [4,5]]`.


**Example**

\*\*```SQL

SELECT flatten([[[1]], [[2], [3]]]);

```Plain Text
**
**```Plain Text
┌─flatten(array(array([1]), array([2], [3])))─┐
│ [1,2,3]                                     │
└─────────────────────────────────────────────┘
```


\*\*

<span id="79b7ea26"></span>
### **arrayCompact**

Remove consecutive duplicate elements from the array. The order of the result values is determined by the order in the source array.

**Syntax**

\*\*```SQL

arrayCompact(arr)

```Plain Text
**
**Parameters**
`arr` — An array type.
**Return Value**
An array without duplicate elements.
Type: `Array`.
**Example**
**Query Statement:**
**```SQL
SELECT arrayCompact([1, 1, nan, nan, 2, 3, 3, 3]);
```


\*\*

**Result:** 

\*\*```Plain Text

┌─arrayCompact([1, 1, nan, nan, 2, 3, 3, 3])─┐

│ [1,nan,nan,2,3] │

└────────────────────────────────────────────┘

```Plain Text
**
<span id="58cdc084"></span>
### **arrayZip**
Combines multiple arrays into one array. The resulting array contains elements of source arrays grouped into tuples in the order of the parameters listed.
**Syntax**
**```SQL
arrayZip(arr1, arr2, ..., arrN)
```


\*\*

**Parameters**


* `arrN` — N arrays.


This function can take an arbitrary number of arrays of different types. All input arrays must be of the same size.

**Return Value**


* Group elements from the source array into an array of tuples. The data types in the tuple are the same as those in the input array and in the same order as the array passed.


**Type:**  array.

**Example**

**Query statement:** 

\*\*```SQL

SELECT arrayZip(['a', 'b', 'c'], [5, 2, 1]);

```Plain Text
**
**Result:**
**```Plain Text
┌─arrayZip(['a', 'b', 'c'], [5, 2, 1])─┐
│ [('a',5),('b',2),('c',1)]            │
└──────────────────────────────────────┘
```


\*\*

<span id="9de911d7"></span>
### **arrayAUC**

Calculate AUC.

AUC: Area under the ROC curve, a concept in machine learning. For more details, please see [Area under the curve](https://en.wikipedia.org/wiki/Receiver_operating_characteristic#Area_under_the_curve).

**Syntax**

\*\*```SQL

arrayAUC(arr_scores, arr_labels)

```Plain Text
**
**Parameter**

* `arr_scores` — Given by the score prediction model.
* `arr_labels` — Labels of samples, usually 1 represents positive samples, 0 represents negative samples.

**Return Value**
Returns a Float64 type AUC value.
**Example**
**Query Statement:**
**```SQL
select arrayAUC([0.1, 0.4, 0.35, 0.8], [0, 0, 1, 1]);
```


\*\*

**Result:** 

\*\*```Plain Text

┌─arrayAUC([0.1, 0.4, 0.35, 0.8], [0, 0, 1, 1])─┐

│ 0.75 │

└───────────────────────────────────────────────┘

```Plain Text
**
<span id="de03057d"></span>
### **arrayMap**
Returns the array obtained from the original application of the `func` function to each element in the `arr` array.
**Grammar**
**```SQL
arrayMap(func, arr1, ...)
```


\*\*

**Example:** 

\*\*```SQL

SELECT arrayMap(x \-\> (x + 2), [1, 2, 3]) as res;

```Plain Text
**
**```Plain Text
┌─res─────┐
│ [3,4,5] │
└─────────┘
```


\*\*

The following example demonstrates how to create a tuple from different arrays:

\*\*```SQL

SELECT arrayMap((x, y) \-\> (x, y), [1, 2, 3], [4, 5, 6]) AS res

```Plain Text
**
**```Plain Text
┌─res─────────────────┐
│ [(1,4),(2,5),(3,6)] │
└─────────────────────┘
```


\*\*

Please note, `arrayMap` is a higher\-order function. You must pass a lambda function as the first argument to it, and it cannot be omitted.

<span id="11ab16f9"></span>
### **arrayFilter**

Returns an array containing only the elements from `arr1` where the value returned by `func` is not 0.

**Grammar**

\*\*```SQL

arrayFilter(func, arr1, ...)

```Plain Text
**
**Example**
**```SQL
SELECT arrayFilter(x -> x LIKE '%World%', ['Hello', 'abc World']) AS res
```


\*\*

\*\*```Plain Text

┌─res───────────┐

│ ['abc World'] │

└───────────────┘

```Plain Text
**
**```SQL
SELECT
    arrayFilter(
        (i, x) -> x LIKE '%World%',
        arrayEnumerate(arr),
        ['Hello', 'abc World'] AS arr)
    AS res
```


\*\*

\*\*```Plain Text

┌─res─┐

│ [2] │

└─────┘

```Plain Text
**
Please note, `arrayFilter` is a higher-order function. You must pass the lambda function as the first parameter and it cannot be omitted.
<span id="824e7111"></span>
### **arrayFill**
Scan `arr1` from the first element to the last, if `func` returns 0, replace arr1[i] with arr1[i - 1]`arr1[i] with arr1[i - 1]`. The first element of `arr1` will not be replaced.
**Syntax**
**```SQL
arrayFill(func, arr1, ...)
```


\*\*

**Example**

\*\*```SQL

SELECT arrayFill(x \-\> not isNull(x), [1, null, 3, 11, 12, null, null, 5, 6, 14, null, null]) AS res

```Plain Text
**
**```Plain Text
┌─res──────────────────────────────┐
│ [1,1,3,11,12,12,12,5,6,14,14,14] │
└──────────────────────────────────┘
```


\*\*

Please note that `arrayFill` is a higher\-order function. You must pass the lambda function as the first parameter and it cannot be omitted.

<span id="7e0429ff"></span>
### **arrayReverseFill**

Scan `arr1` from the last element to the first, if `func` returns 0, replace arr1[i] with arr1[i + 1]`arr1[i] with arr1[i + 1]`. The last element of `arr1` will not be replaced.

**Syntax**

\*\*```SQL

arrayReverseFill(func, arr1, ...)

```Plain Text
**
**Example**
**```SQL
SELECT arrayReverseFill(x -> not isNull(x), [1, null, 3, 11, 12, null, null, 5, 6, 14, null, null]) AS res
```


\*\*

\*\*```Plain Text

┌─res────────────────────────────────┐

│ [1,3,3,11,12,5,5,5,6,14,NULL,NULL] │

└────────────────────────────────────┘

```Plain Text
**
Please note that `arrayReverseFill` is a higher-order function. You must pass the lambda function as the first argument to it, and it cannot be omitted.
<span id="2d30d267"></span>
### **arraySplit**
Split `arr1` into multiple arrays. When `func` returns a non-zero value, the array will split on the left side of the element. The array will not split before the first element.
**Syntax**
**```SQL
arraySplit(func, arr1, ...)
```


\*\*

**Example**

\*\*```SQL

SELECT arraySplit((x, y) \-\> y, [1, 2, 3, 4, 5], [1, 0, 0, 1, 0]) AS res

```Plain Text
**
**```Plain Text
┌─res─────────────┐
│ [[1,2,3],[4,5]] │
└─────────────────┘
```


\*\*

Please note that `arraySplit` is a higher\-order function. You must pass a lambda function as the first argument to it, and you cannot omit it.

<span id="74c0d6b3"></span>
### **arrayReverseSplit**

Split `arr1` into multiple arrays. When `func` returns a value other than 0, the array will be split to the right of the element. The array will not be split after the last element.

**Syntax**

\*\*```SQL

arrayReverseSplit(func, arr1, ...)

```Plain Text
**
**Example**
**```SQL
SELECT arrayReverseSplit((x, y) -> y, [1, 2, 3, 4, 5], [1, 0, 0, 1, 0]) AS res
```


\*\*

\*\*```Plain Text

┌─res───────────────┐

│ [[1],[2,3,4],[5]] │

└───────────────────┘

```Plain Text
**
Please note that `arrayReverseSplit` is a higher-order function. You must pass the lambda function as the first argument to it and you cannot omit it.
<span id="7ced03e2"></span>
### **arrayExists**
If there is at least one element in `arr` where `func` returns a value other than 0, it returns 1. Otherwise, it returns 0.
Please note, `arrayExists` is a higher-order function.
**Syntax**
**```SQL
arrayExists([func,] arr1, …)
```


\*\*

**Parameters**


* `func` – A higher\-order function that must return UInt8

* `arr1,..` – Arrays as inputs to the function


**Return Value**


* If arr returns a non\-zero value for at least one element in the for loop, it returns 1. Otherwise, it returns 0.


**Example**

\*\*```SQL

SELECT arrayExists((x,y)\-\>x==y,[1, 2, 2, 3, 1],[4, 5, 6, 7, 8]);

```Plain Text
**
**```Plain Text
┌─arrayExists(lambda(tuple(x, y), equals(x, y)), [1, 2, 2, 3, 1], [4, 5, 6, 7, 8])─┐
│ 0                                                                                │
└──────────────────────────────────────────────────────────────────────────────────┘
```


\*\*

\*\*```SQL

SELECT arrayExists((x,y)\-\>x==y,[1, 2, 2, 3, 1],[1, 5, 6, 7, 8]);

```Plain Text
**
**```Plain Text
┌─arrayExists(lambda(tuple(x, y), equals(x, y)), [1, 2, 2, 3, 1], [1, 5, 6, 7, 8])─┐
│ 1                                                                                │
└──────────────────────────────────────────────────────────────────────────────────┘
```


\*\*

<span id="3259032c"></span>
### **arrayAll**

If `func` returns non\-zero values for all elements in `arr`, then it returns 1. Otherwise, it returns 0.

**Syntax**

\*\*```SQL

arrayAll([func,] arr1, ...)

```Plain Text
**
Please note that `arrayAll` is a higher-order function. You can pass a lambda function as the first parameter to it, and it cannot be omitted.
<span id="3f3d9d1d"></span>
### **arrayFirst**
Return the first element in the `arr1` array where `func` returns a non-zero value. If this value doesn't exist, it returns the default value.
**Syntax**
**```SQL
arrayFirst(func, arr1, ...)
```


\*\*

Please note that `arrayFirst` is a higher\-order function. You must pass a lambda function as the first argument to it, and it cannot be omitted.

<span id="cef6414d"></span>
### **arrayLast**

Return the last element in the `arr1` array where `func` returns a non\-zero value. If this value doesn't exist, it returns the default value.

**Syntax**

\*\*```SQL

arrayLast(func, arr1, ...)

```Plain Text
**
Please note that `arrayLast` is a higher-order function. You must pass a lambda function as the first argument to it, and it cannot be omitted.
<span id="11fd3be8"></span>
### **arrayFirstIndex**
Returns the index of the first element in the `arr1` array where `func` does not return 0. If this value doesn't exist, it returns 0.
**Syntax**
**```SQL
arrayFirstIndex(func, arr1, ...)
```


\*\*

Please note that `arrayFirstIndex` is a higher\-order function. You must pass a lambda function as the first argument and it cannot be omitted.

<span id="ef1d21e7"></span>
### **arrayLastIndex**

Returns the index of the last element in the `arr1` array where `func` does not return 0. If this value doesn't exist, it returns 0.

**Syntax**

\*\*```SQL

arrayLastIndex(func, arr1, ...)

```Plain Text
**
Please note that `arrayLastIndex` is a higher-order function. You must pass a lambda function as the first argument and it cannot be omitted.
<span id="51fb9555"></span>
### **arrayMin**
Returns the smallest element in the source array.
If a `func` function is specified, it returns the minimum value of the elements transformed by this function.
Please note that `arrayMin` is a higher-order function. You can pass a lambda function as the first parameter to it, which cannot be omitted.
**Syntax**
**```SQL
arrayMin([func,] arr)
```


\*\*

**Parameters**


* `func` — Type: expression.

* `arr` — Type: array.


**Return Value**


* The minimum value of the function value (or array minimum).


**Type:**  If `func` is specified, it matches the return type of `func`, otherwise it matches the array element type.

**Example**

**Query statement:** 

\*\*```SQL

SELECT arrayMin([1, 2, 4]) AS res;

```Plain Text
**
**Result:**
**```Plain Text
┌─res─┐
│   1 │
└─────┘
```


\*\*

**Query statement:** 

\*\*```SQL

SELECT arrayMin(x \-\> (\-x), [1, 2, 4]) AS res;

```Plain Text
**
**Result:**
**```Plain Text
┌─res─┐
│  -4 │
└─────┘
```


\*\*

<span id="5fd56db6"></span>
### **arrayMax**

Returns the maximum value of the elements in the source array.

If a `func` function is specified, it returns the maximum value of the elements transformed by this function.

Please note, `arrayMax` is a higher\-order function. You can pass the lambda function as the first argument and it cannot be omitted.

**Syntax**

\*\*```SQL

arrayMax([func,] arr)

```Plain Text
**
**Parameters**

* `func` — Type: expression.
* `arr` — Type: array.

**Return value**

* The maximum value of the function (or maximum value of the array).

**Type:** If `func` is specified, it matches the return type of `func`; otherwise, it matches the type of array elements.
**Example**
**Query statement:**
**```SQL
SELECT arrayMax([1, 2, 4]) AS res;
```


\*\*

**Result:** 

\*\*```Plain Text

┌─res─┐

│ 4 │

└─────┘

```Plain Text
**
**Query statement:**
**```SQL
SELECT arrayMax(x -> (-x), [1, 2, 4]) AS res;
```


\*\*

**Result:** 

\*\*```Plain Text

┌─res─┐

│ \-1 │

└─────┘

```Plain Text
**
<span id="d9c14af3"></span>
### **arraySum**
Returns the sum of the elements in the source array.
If a `func` function is specified, then it returns the sum of the elements transformed by this function.
Please note that `arraySum` is a higher-order function. You can pass a lambda function as the first parameter to it, and it cannot be omitted.
**Syntax**
**```SQL
arraySum([func,] arr)
```


\*\*

**Parameters**


* `func` — An expression type.

* `arr` — An array type.


**Return Value**


* Sum of the function values (or array sum).


**Type:**  Decimal numbers from the source array (or converted values, if `func` is specified) \- Decimal128, for floating\-point numbers \- Float64, for unsigned numbers \- UInt64, for signed numbers \- Int64.

**Examples**

**Query Statement:** 

\*\*```SQL

SELECT arraySum([2, 3]) AS res;

```Plain Text
**
**Result:**
**```Plain Text
┌─res─┐
│   5 │
└─────┘
```


\*\*

**Query Statement:** 

\*\*```SQL

SELECT arraySum(x \-\> x\*x, [2, 3]) AS res;

```Plain Text
**
**Result:**
**```Plain Text
┌─res─┐
│  13 │
└─────┘
```


\*\*

<span id="d739f03b"></span>
### **arrayAvg**

Returns the average value of elements in the source array.

If a function specified as func is provided, returns the average value of the elements transformed by this function.

Please note that `arrayAvg` is a higher\-order function. You can pass a lambda function as the first parameter to it, which cannot be omitted.

**Syntax**

\*\*```SQL

arrayAvg([func,] arr)

```Plain Text
**
**Parameters**

* `func` — Type: Expression.
* `arr` — Type: Array.

**Return value**

* The average value of the function or the array.

**Type:** Float64.
**Example**
**Search Query:**
**```SQL
SELECT arrayAvg([1, 2, 4]) AS res;
```


\*\*

**As a result:** 

\*\*```Plain Text

┌────────────────res─┐

│ 2.3333333333333335 │

└────────────────────┘

```Plain Text
**
**Search Query:**
**```SQL
SELECT arrayAvg(x -> (x * x), [2, 4]) AS res;
```


\*\*

**As a result:** 

\*\*```Plain Text

┌─res─┐

│ 10 │

└─────┘

```Plain Text
**
<span id="509cf223"></span>
### **arrayCumSum**
Returns an array of the partial sums of elements in the source array (running total). If a function is specified, the values of the array elements are transformed by that function before summation.
**Grammar**
**```SQL
arrayCumSum([func,] arr1, ...)
```


\*\*

**Example:** 

\*\*```SQL

SELECT arrayCumSum([1, 1, 1, 1]) AS res

```Plain Text
**
**```Plain Text
┌─res──────────┐
│ [1, 2, 3, 4] │
└──────────────┘
```


\*\*

Please note, `arrayCumSum` is a higher\-order function. You can pass a lambda function as the first parameter to it, and it must not be omitted.

<span id="1b6e83ab"></span>
### **arrayCumSumNonNegative**

Similar to `arrayCumSum`, it returns an array of partial sums (running total) of elements in the source array. Unlike `arrayCumSum`, when the return value contains values smaller than zero, it replaces that value with zero and executes subsequent calculations with zero.

**Example:** 

\*\*```SQL

arrayCumSumNonNegative(arr)

```Plain Text
**
**Example**
**```SQL
SELECT arrayCumSumNonNegative([1, 1, -4, 1]) AS res
```


\*\*

\*\*```Plain Text

┌─res───────┐

│ [1,2,0,1] │

└───────────┘

```Plain Text
**
Please note `arraySumNonNegative` is a higher-order function. You can pass the lambda function as the first argument to it and it cannot be omitted.
<span id="bbf5395b"></span>
### **arrayProduct**
Multiply the elements in an array.
**Syntax**
**```SQL
arrayProduct(arr)
```


\*\*

**Param**


* `arr` — Type Numerical value array.


**Return value**


* The product of the array elements.


**Type:**  Float64.

**Example**

**Search Query:** 

\*\*```SQL

SELECT arrayProduct([1,2,3,4,5,6]) as res;

```Plain Text
**
**Result:**
**```Plain Text
┌─res───┐
│ 720   │
└───────┘
```


\*\*

**Search Query:** 

\*\*```SQL

SELECT arrayProduct([toDecimal64(1,8), toDecimal64(2,8), toDecimal64(3,8)]) as res, toTypeName(res);

```Plain Text
**
**Return value type is always Float64. Result:**
**```Plain Text
┌─res─┬─toTypeName(arrayProduct(array(toDecimal64(1, 8), toDecimal64(2, 8), toDecimal64(3, 8))))─┐
│ 6   │ Float64                                                                                  │
└─────┴──────────────────────────────────────────────────────────────────────────────────────────┘
```


\*\*

<span id="0644eea7"></span>
### **arrayElement**

`n` retrieves an element with index from the array `arr`. `n` must be of any integer type.

The index in the array starts at one.

Negative indexing is supported. In this case, it selects the corresponding element numbered from the end. For example, `arr[-1]` is the last item in the array.

If the index exceeds the boundaries of the array, it will return a default value (Number as 0, String is empty, etc.), except for non\-constant arrays with a constant index of 0 (in this case, an error `Array indices are 1-based` occurs).

**Syntax**

\*\*```SQL

arrayElement(array, n)

```Plain Text
**
**Param**

* `array` array.
* `n` index in the array.

**Return value**

* `n` retrieves the element with the index from the array `arr`

**Example**
**```SQL
SELECT arrayElement([1, 2, 2, 3, 1],3);
```


\*\*

\*\*```Plain Text

┌─arrayElement([1, 2, 2, 3, 1], 3)─┐

│ 2 │

└──────────────────────────────────┘

```Plain Text
**
 **** 

```
