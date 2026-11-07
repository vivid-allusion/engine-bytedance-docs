---
title: "Array Functions"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/array-functions"
---

<span id="empty"></span>
## empty
Returns 1 for empty arrays and 0 for non-empty arrays. The result type is UInt8. This function is also applicable to strings.
<span id="notempty"></span>
## notEmpty
Returns 0 for empty arrays and 1 for non-empty arrays. The result type is UInt8. This function is also applicable to strings.
<span id="length"></span>
## length
Returns the number of elements in the array. The result type is UInt64. This function is also applicable to strings.
<span id="emptyarrayuint8-emptyarrayuint16-emptyarrayuint32-emptyarrayuint64"></span>
## emptyArrayUInt8,emptyArrayUInt16,emptyArrayUInt32,emptyArrayUInt64
<span id="emptyarrayint8-emptyarrayint16-emptyarrayint32-emptyarrayint64"></span>
## emptyArrayInt8,emptyArrayInt16,emptyArrayInt32,emptyArrayInt64
<span id="emptyarrayfloat32-emptyarrayfloat64"></span>
## emptyArrayFloat32,emptyArrayFloat64
<span id="emptyarraydate，emptyarraydatetime"></span>
## emptyArrayDate，emptyArrayDateTime
<span id="emptyarraystring"></span>
## emptyArrayString
Accepts no arguments and returns an empty array of the appropriate type.
<span id="emptyarraytosingle"></span>
## emptyArrayToSingle
Accepts an empty array and returns an array containing only a single default value element.
<span id="range-n"></span>
## range(N)
Returns an array of numbers from 0 to N-1. In case an array with a total length exceeding 100,000,000 elements is created within a data block, an exception is thrown.
<span id="array-x1-…-operator-x1-…"></span>
## array(x1, …), operator [x1, …]
Create an array using the arguments of the function as the elements of the array. The arguments must be constants and of the type with the minimum common type. At least one argument must be passed, otherwise it will not be clear what type of array to create. That is to say, you cannot use this function to create an empty array (for this, use the 'emptyArrayToSingle' function described above). Returns an 'Array(T)' type result, where 'T' is the smallest common type among the parameters passed.
<span id="arrayconcat"></span>
## arrayConcat
Merges all arrays passed in the parameters.
```plaintext
arrayConcat(arrays)
```

Parameters

* `arrays` - Arguments of any number of [array](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/en/sql-reference/functions/array-functions.md) types. Examples

SELECT arrayConcat([1, 2], [3, 4], [5, 6]) AS res
<span id="arrayelement-arr-n-运算符arr-n"></span>
## ```plaintext
┌─res───────────┐
│ [1,2,3,4,5,6] │
└───────────────┘
```

<span id="arrayelement-arr-n-运算符arr-n"></span>
## arrayElement(arr, n), operator arr[n]
Retrieves the element at index «n» from the array `arr`. `n` must be of any integer type. Indexes in the array start from one. Negative indexes are supported. In this case, it selects the corresponding elements numbered from the end of the array. For example, `arr [-1]` is the last item in the array.
If the index is out of the array bounds, it returns the default value (zero for numbers, empty string for strings, etc.).
<span id="has-arr-elem"></span>
## has(arr,elem)
Checks if the 'arr' array contains the 'elem' element. If the element is not in the array, it returns 0; if it is, it returns 1.
`Handling of NULL` values.
<span id="hasall"></span>
## ```plaintext
SELECT has([1, 2, NULL], NULL)
┌─has([1, 2, NULL], NULL)─┐
│                       1 │
└─────────────────────────┘
```

<span id="hasall"></span>
## hasAll
Check if an array is a subset of another array.
```plaintext
hasAll(set, subset)
```

Parameter

* `set` - An array of any type with a set of elements.
* `subset` - An array of any type whose elements should be tested as a subset of `set`.

Return Value

* `1`, if `set` contains all elements in `subset`.
* `0`, otherwise.

Special Definition

* An empty array is a subset of any array.
* «Null» is treated as an element value in the array.
* Ignore the order of element values in the two arrays.

Example
`SELECT hasAll([], [])` returns 1.
`SELECT hasAll([1, Null], [Null])` returns 1.
`SELECT hasAll([1.0, 2, 3, 4], [1, 3])` returns 1.
`SELECT hasAll(['a', 'b'], ['a'])` returns 1.
`SELECT hasAll([1], ['a'])` returns 0.
`SELECT hasAll([[1, 2], [3, 4]], [[1, 2], [3, 5]])` returns 0.
<span id="hasany"></span>
## hasAny
Check if two arrays have any intersection.
```plaintext
hasAny(array1, array2)
```

Parameter

* `array1` – Any type of array with a set of elements.
* `array2` – Any type of array with a set of elements.

Return Value

* `1`, if `array1` and `array2` have an intersection.
* `0`, otherwise.

Special Definition

* "Null" is treated as an element value in the array.
* Ignore the order of element values in both arrays.

Example
`SELECT hasAny([1], [])` returns `0`.
`SELECT hasAny([Null], [Null, 1])` returns `1`.
`SELECT hasAny([-128, 1., 512], [1])` returns `1`.
`SELECT hasAny([[1, 2], [3, 4]], ['a', 'c'])` returns `0`.
`SELECT hasAll([[1, 2], [3, 4]], [[1, 2], [1, 2]])` returns `1`.
<span id="indexof-arr-x"></span>
## indexOf(arr,x)
Returns the index of the first 'x' element in the array (starting from 1), if the 'x' element does not exist in the array, then it returns 0.
Example:
```plaintext
:) SELECT indexOf([1,3,NULL,NULL],NULL)
SELECT indexOf([1, 3, NULL, NULL], NULL)
┌─indexOf([1, 3, NULL, NULL], NULL)─┐
│                                 3 │
└───────────────────────────────────┘
```

Elements set to "NULL" will be treated as regular element values.
<span id="countequal-arr-x"></span>
## countEqual(arr,x)
Return the number of elements in the array that are equal to x. Equivalent to arrayCount(elem -> elem = x, arr).
`NULL` values are treated as distinct element values.
Example:
<span id="arrayenumerate-arr"></span>
## ```plaintext
SELECT countEqual([1, 2, NULL, NULL], NULL)
┌─countEqual([1, 2, NULL, NULL], NULL)─┐
│                                    2 │
└──────────────────────────────────────┘
```

<span id="arrayenumerate-arr"></span>
## arrayEnumerate(arr)
Returns Array [1, 2, 3, …, length(arr)].
This function is commonly used with ARRAY JOIN. It allows for a calculation to be performed once for each array after applying ARRAY JOIN. For example:
SELECT count() AS Reaches, countIf(num = 1) AS Hits FROM test.hits ARRAY JOIN GoalsReached, arrayEnumerate(GoalsReached) AS num WHERE CounterID = 160656 LIMIT 10
```plaintext
┌─Reaches─┬──Hits─┐
│   95606 │ 31406 │
└─────────┴───────┘
```

In this example, "Reaches" represents the number of transformations (strings received after using ARRAY JOIN), and "Hits" represent view counts (strings before ARRAY JOIN). In this special case, you can more easily achieve the same result:
SELECT sum(length(GoalsReached)) AS Reaches, count() AS Hits FROM test.hits WHERE (CounterID = 160656) AND notEmpty(GoalsReached)
```plaintext
┌─Reaches─┬──Hits─┐
│   95606 │ 31406 │
└─────────┴───────┘
```

This feature can also be used in higher-order functions. For instance, you can use it to obtain the array indexes of elements that match specific conditions.
<span id="arrayenumerateuniq-arr-…"></span>
## arrayEnumerateUniq(arr, …)
It returns an array of the same size as the source array, where each element represents the count of occurrences of the corresponding source array element at that index. For example: arrayEnumerateUniq([10,20,10,30]) = [1,1,2,1].
This function is useful when using ARRAY JOIN and aggregating array elements.
Example:
SELECTGoals.ID AS GoalID, sum(Sign) AS Reaches, sumIf(Sign, num = 1) AS Visits FROM test.visits ARRAY JOIN Goals, arrayEnumerateUniq(Goals.ID) AS num WHERE CounterID = 160656GROUP BY GoalID ORDER BY Reaches DESCLIMIT 10
```plaintext
┌──GoalID─┬─Reaches─┬─Visits─┐
│   53225 │    3214 │   1097 │
│ 2825062 │    3188 │   1097 │
│   56600 │    2803 │    488 │
│ 1989037 │    2401 │    365 │
│ 2830064 │    2396 │    910 │
│ 1113562 │    2372 │    373 │
│ 3270895 │    2262 │    812 │
│ 1084657 │    2262 │    345 │
│   56599 │    2260 │    799 │
│ 3271094 │    2256 │    812 │
└─────────┴─────────┴────────┘
```

In this example, each GoalID calculates conversion counts (each element in the goal-nested data structure represents a reached goal, which we call a conversion) and the number of sessions. If there is no ARRAY JOIN, the number of sessions would be counted as the total of (Sign). In this special case, multiplying the line by the nested Goals structure, a condition is applied to the value of the arrayEnumerateUniq(Goals.ID) function to count each session once afterward.
The arrayEnumerateUniq function can use multiple arrays that are the same size as the parameter. In this case, uniqueness is considered for elements in all arrays that are in the same position in each tuple.
SELECT arrayEnumerateUniq([1, 1, 1, 2, 2, 2], [1, 1, 2, 1, 1, 2]) AS res
```plaintext
┌─res───────────┐
│ [1,2,1,1,2,1] │
└───────────────┘
```

This is necessary when using ARRAY JOIN with a nested data structure and further aggregating across multiple elements in this structure.
<span id="arraypopback"></span>
## arrayPopBack
Remove the last item from the array.
```plaintext
arrayPopBack(array)
```

Parameters

* `array` – An array.

Example
SELECT arrayPopBack([1, 2, 3]) AS res
<span id="arraypopfront"></span>
## ```plaintext
┌─res───┐
│ [1,2] │
└───────┘
```

<span id="arraypopfront"></span>
## arrayPopFront
Remove the first item from the array.
```plaintext
arrayPopFront(array)
```

Parameters

* `array` – An array.

Example
SELECT arrayPopFront([1, 2, 3]) AS res
<span id="arraypushback"></span>
## ```plaintext
┌─res───┐
│ [2,3] │
└───────┘
```

<span id="arraypushback"></span>
## arrayPushBack
Add a single element to the end of an array.
```plaintext
arrayPushBack(array, single_value)
```

Parameter

* `array` – The array.
* `single_value` – A single value. Only numbers can be added to an array containing numbers, and only strings can be added to a string array. When adding numbers, ClickHouse will automatically set the data type of the array to `single_value` type. For more information about data types in ClickHouse, please refer to "[Data Types](https://github.com/ClickHouse/ClickHouse/tree/21.8/docs/en/sql-reference/data-types)". It can be 'NULL`.`' `This function adds a 'NULL' element to the array, and the type of the array elements is converted to` Nullable.

Example
SELECT arrayPushBack(['a'], 'b') AS res
<span id="arraypushfront"></span>
## ```plaintext
┌─res───────┐
│ ['a','b'] │
└───────────┘
```

<span id="arraypushfront"></span>
## arrayPushFront
Add an element to the beginning of the array.
```plaintext
arrayPushFront(array, single_value)
```

Parameters

* `array` – Array.
* `single_value` – Single value. You can only add numbers to an array of numbers, and strings to an array of strings. When adding numbers, ClickHouse automatically sets the data type of the array to `single_value` type. For more information about data types in ClickHouse, see «[Data Types](https://github.com/ClickHouse/ClickHouse/tree/21.8/docs/en/sql-reference/data-types)». It can be 'NULL`.` `The function adds a "NULL" element to the array,` converting the element type to Nullable`.

Example
SELECT arrayPushFront(['b'], 'a') AS res
<span id="arrayresize"></span>
## ```plaintext
┌─res───────┐
│ ['a','b'] │
└───────────┘
```

<span id="arrayresize"></span>
## arrayResize
Changes the length of the array.
```plaintext
arrayResize(array, size[, extender])
```

Parameters:

* `array` — Array.
* `size` — The required length of the array.
   * If `size` is less than the original size of the array, the array will be truncated from the right.
* If `size` is larger than the initial size of the array, the array is extended to the right using `extender` value or the default value of the data type of the array elements.
* `Extender` — Value to extend the array. Can be 'NULL'.

Return value:
An array of length `size`.
Call example
<span id="arrayslice"></span>
## ```plaintext
SELECT arrayResize([1], 3)
┌─arrayResize([1], 3)─┐
│ [1,0,0]             │
└─────────────────────┘
SELECT arrayResize([1], 3, NULL)
┌─arrayResize([1], 3, NULL)─┐
│ [1,NULL,NULL]             │
└───────────────────────────┘
```

<span id="arrayslice"></span>
## arraySlice
Returns a subarray that contains elements of the specified length from the specified position.
```plaintext
arraySlice(array, offset[, length])
```

Parameters

* `Array` — The array.
* `Offset` - offset of the array. Positive values represent offsets to the left, while negative values represent indentation to the right. Array indices start from 1.
* `Length` - length of the subarray. If a negative value is specified, the function returns `[offset, array_length - length`. If the value is omitted, the function returns `[offset, the_end_of_array]`.

Example
SELECT arraySlice([1, 2, NULL, 4, 5], 2, 3) AS res
```plaintext
┌─res────────┐
│ [2,NULL,4] │
└────────────┘
```

Array elements set to «NULL» are treated as normal array element values.
<span id="arraysort-func-arr-…"></span>
## arraySort([func,] arr, …)
Sorts the elements of the `arr` array in ascending order. If the `func` function is specified, the sorting order is determined by the results of the `func` function calls. If `func` accepts multiple arguments, the `arraySort` function will also parse arrays of the same number of arguments that correspond to the `func` function. More detailed examples are available at the end of `arraySort`.
Example of sorting integers:
SELECT arraySort([1, 3, 3, 0]);
```plaintext
┌─arraySort([1, 3, 3, 0])─┐
│ [0,1,3,3]               │
└─────────────────────────┘
```

Example of sorting strings:
SELECT arraySort(['hello', 'world', '!']);
```plaintext
┌─arraySort(['hello', 'world', '!'])─┐
│ ['!','hello','world']              │
└────────────────────────────────────┘
```

The sorting order of `NULL`, `NaN`, and `Inf`:
SELECT arraySort([1, nan, 2, NULL, 3, nan, -4, NULL, inf, -inf]);
```plaintext
┌─arraySort([1, nan, 2, NULL, 3, nan, -4, NULL, inf, -inf])─┐
│ [-inf,-4,1,2,3,inf,nan,nan,NULL,NULL]                     │
└───────────────────────────────────────────────────────────┘
```


* `-Inf` is the first in the array.
* `NULL` is the last element in the array.
* `NaN` is before `NULL`.
* `Inf` comes before `NaN`.

Note: `arraySort` is a [higher-order function](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/zh/sql-reference/functions/higher-order-functions.md). You can pass a lambda function as the first argument to it. In this case, the sorting order is determined by the result of the lambda function's call.
Let's look at the following example:
SELECT arraySort((x) -> -x, [1, 2, 3]) as res;
```plaintext
┌─res─────┐
│ [3,2,1] │
└─────────┘
```

For each element of the source array, the lambda function returns a sorting key, namely [1 -> -1, 2 -> -2, 3 -> -3]. Since the `arraySort` function sorts keys in ascending order, the result is [3, 2, 1]. Therefore, `(x) -> -x` lambda function sets the order to [Desc](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/en/sql-reference/functions/array-functions.md).
Lambda functions can accept multiple parameters. In this case, you need to pass an array to `arraySort` with the same number of elements as lambda parameters. The function uses the elements from the first input array to form the result; the subsequent arrays passed are used as sorting keys. Example:
SELECT arraySort((x, y) -> y, ['hello', 'world'], [2, 1]) as res;
```plaintext
┌─res────────────────┐
│ ['world', 'hello'] │
└────────────────────┘
```

Here, the sorting keys for the elements of the first array (['hello', 'world']) are defined in the second array ([2, 1]), that is ['hello' -> 2, 'world' -> 1]. Since `x` is not used in the lambda function, the actual values in the source array do not affect the order of the results. Thus, 'world' will be the first element in the results, and 'hello' will be the second.
Other examples are as follows.
```SQL
SELECT arraySort((x, y) -> y, [0, 1, 2], ['c', 'b', 'a']) as res;
┌─res─────┐ 
│ [2,1,0] │ 
└─────────┘
SELECT arraySort((x, y) -> -y, [0, 1, 2], [1, 2, 3]) as res;
┌─res─────┐ 
│ [2,1,0] │ 
└─────────┘
```

:::warning
To improve sorting efficiency, [Schwartzian transform](https://en.wikipedia.org/wiki/Schwartzian_transform) is used.
:::
<span id="arrayreversesort-func-arr-…"></span>
## arrayReverseSort([func,] arr, …)
Sort the elements of the array `arr` in descending order. If `func` function is specified, the order of sorting is determined by the result of the `func` function call. If the `func` takes multiple parameters, then the `arrayReverseSort` function will also resolve arrays with the same number of elements as parameters to the `func` function. More detailed examples are at the end of `arrayReverseSort`.
Integer sorting example:
SELECT arrayReverseSort([1, 3, 3, 0]);
```plaintext
┌─arrayReverseSort([1, 3, 3, 0])─┐
│ [3,3,1,0]                      │
└────────────────────────────────┘
```

String sorting example:
SELECT arrayReverseSort(['hello', 'world', '!']);
```plaintext
┌─arrayReverseSort(['hello', 'world', '!'])─┐
│ ['world','hello','!']                     │
└───────────────────────────────────────────┘
```

`NULL`, `NaN` and `Inf` sorting order:
```SQL
SELECT arrayReverseSort([1, nan, 2, NULL, 3, nan, -4, NULL, inf, -inf]) as res;
┌─res───────────────────────────────────┐ 
│ [inf,3,2,1,-4,-inf,nan,nan,NULL,NULL] │ 
└───────────────────────────────────────┘
```


* `Inf` is the first in the array.
* `NULL` is the last in the array.
* `NaN` is before `NULL`.
* `-Inf` is before `NaN`.

Advisory: `arraySort` is a [high-order function](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/zh/sql-reference/functions/higher-order-functions.md). You can pass a lambda function as the first argument to it. As shown in the following example.
SELECT arrayReverseSort((x) -> -x, [1, 2, 3]) as res;
```plaintext
┌─res─────┐
│ [1,2,3] │
└─────────┘
```

Arrays are sorted as follows:

1. First, sort the source array ([1, 2, 3]) based on the results of lambda function calls. As a result, the array is [3, 2, 1].
2. Reverse the array obtained in the previous step. So, the final result is [1, 2, 3].

Lambda functions can accept multiple parameters. In this case, you need to pass an array with the same number of lambda parameters to `arrayReverseSort`. The function constructs the return result using the elements from the first input array; it uses the subsequent arrays passed in as sorting keys. For example:
SELECT arrayReverseSort((x, y) -> y, ['hello', 'world'], [2, 1]) as res;
```plaintext
┌─res───────────────┐
│ ["hello","world"] │
└───────────────────┘
```
