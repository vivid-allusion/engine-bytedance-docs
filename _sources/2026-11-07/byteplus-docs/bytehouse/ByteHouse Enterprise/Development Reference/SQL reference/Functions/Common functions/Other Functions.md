---
title: "Other Functions"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/other-functions"
---

<span id="hostname"></span>
## hostName
Returns a string containing the name of the host on which this function is executed. For distributed processing, if this function is executed on a remote server, the name of the remote server host will be returned.
<span id="basename"></span>
## basename
The string text after the last slash or backslash. This function is commonly used to extract the filename from a path.
```plaintext
basename( expr )
```

Parameters

* `expr` — Any expression that returns a string result.

Return Value
A String type value, which contains:

* The text content after the last slash or backslash.

```plaintext
If the input string ends with a forward slash or a backslash, for example: `/` or `c:\`, the function will return an empty string. 
```


* If the input string does not contain a slash or backslash, the function returns the input string itself.

Example
```SQL
SELECT 'some/long/path/to/file' AS a, basename(a)
```

```plaintext
┌─a──────────────────────┬─basename('some\\long\\path\\to\\file')─┐
│ some\long\path\to\file │ file                                   │
└────────────────────────┴────────────────────────────────────────┘
```

```SQL
SELECT 'some\\long\\path\\to\\file' AS a, basename(a)
```

```plaintext
┌─a──────────────────────┬─basename('some\\long\\path\\to\\file')─┐
│ some\long\path\to\file │ file                                   │
└────────────────────────┴────────────────────────────────────────┘
```

```SQL
SELECT 'some-file-name' AS a, basename(a)
```

```plaintext
┌─a──────────────┬─basename('some-file-name')─┐
│ some-file-name │ some-file-name             │
└────────────────┴────────────────────────────┘
```

<span id="visiblewidth-x"></span>
## visibleWidth(x)
When outputting values to the console in text format (tab-delimited), it calculates the approximate width. The system uses this function to implement the Pretty format. When outputting values to the console in text format (tab-separated), calculate the approximate width. This function is used by the system to implement nice formatting.
`NULL` is represented as corresponding to `NULL` in `Pretty` format.
```plaintext
SELECT visibleWidth(NULL)

┌─visibleWidth(NULL)─┐
│                  4 │
└────────────────────┘
```

<span id="totypename-x"></span>
## toTypeName(x)
Returns a string that contains the type name of the parameter.
If `NULL` is passed as a parameter to the function, it returns a `Nullable (Nothing)` type which corresponds to ClickHouse's internal `NULL`.
<span id="blocksize"></span>
## blockSize()
Fetches the size of a Block. In ClickHouse, queries always operate on Blocks (a collection of parts containing columns). This function allows you to obtain the size of the block it is called from.
<span id="materialize-x"></span>
## materialize(x)
Turns a constant column into a non-constant column. In ClickHouse, constant columns and non-constant columns are represented differently in memory. Although the function always returns the same result for constant and non-constant columns, their operation might be entirely different (executing different code). This function is used for debugging such behavior.
<span id="ignore-…"></span>
## ignore(…)
Accepts any arguments, including `NULL`. Always returns 0. However, the function's arguments are always evaluated. This function can be used for benchmarking.
<span id="sleep-s"></span>
## sleep(s)
Sleep for 'seconds' seconds on each block. Can be an integer or a floating-point number.
<span id="sleepeachrow-s"></span>
## sleepEachRow(s)
Sleep for 'seconds' seconds on each row. Can be an integer or a floating-point number.
<span id="currentdatabase"></span>
## currentDatabase()
Returns the name of the current database. When you need to specify the database in the table engine parameters in CREATE TABLE, you can use this function.
<span id="isfinite-x"></span>
## isFinite(x)
Accepts parameters of Float32 or Float64 type. If the parameter is not infinite and not NaN, it returns 1; otherwise, it returns 0.
<span id="isinfinite-x"></span>
## isInfinite(x)
Accepts parameters of Float32 or Float64 type, and returns 1 if the parameter is infinite; otherwise, returns 0. Note that NaN returns 0.
<span id="isnan-x"></span>
## isNaN(x)
Accepts parameters of Float32 or Float64 type. If the parameter is NaN, returns 1; otherwise, returns 0.
<span id="hascolumnintable-‘hostname’-‘username’-‘password’-‘database’-‘table’-‘column’"></span>
## hasColumnInTable([‘hostname’[, ‘username’[, ‘password’]],] ‘database’, ‘table’, ‘column’)
Accepts constant strings: database name, table name, and column name. If the column exists, returns a UInt8 constant expression equal to 1; otherwise, returns 0. If the hostname parameter is set, the test will run on a remote server. If the table does not exist, the function will throw an exception. For elements in nested data structures, the function checks if the column exists. For the nested data structure itself, the function returns 0.
<span id="bar"></span>
## bar
Build charts using unicode.
`bar(x, min, max, width)` draws a band whose width is proportional to (x - min) and equal to width when x = max.`(x - min) and equal to width when xwidth when x = max`.
Parameters:

* `x` — the dimension to display.
* `min, max` — integer constants, which must be `Int64`.
* `width` — a constant, which can be a positive integer or decimal.

The precision of string led drawing is one eighth of symbols.
Example:
```SQL
SELECT toHour(EventTime) AS h, count() AS c, bar(c, 0, 600000, 20) AS bar FROM test.hitsGROUP BY h ORDER BY h ASC
```

```plaintext
┌──h─┬──────c─┬─bar────────────────┐
│  0 │ 292907 │ █████████▋         │
│  1 │ 180563 │ ██████             │
│  2 │ 114861 │ ███▋               │
│  3 │  85069 │ ██▋                │
│  4 │  68543 │ ██▎                │
│  5 │  78116 │ ██▌                │
│  6 │ 113474 │ ███▋               │
│  7 │ 170678 │ █████▋             │
│  8 │ 278380 │ █████████▎         │
│  9 │ 391053 │ █████████████      │
│ 10 │ 457681 │ ███████████████▎   │
│ 11 │ 493667 │ ████████████████▍  │
│ 12 │ 509641 │ ████████████████▊  │
│ 13 │ 522947 │ █████████████████▍ │
│ 14 │ 539954 │ █████████████████▊ │
│ 15 │ 528460 │ █████████████████▌ │
│ 16 │ 539201 │ █████████████████▊ │
│ 17 │ 523539 │ █████████████████▍ │
│ 18 │ 506467 │ ████████████████▊  │
│ 19 │ 520915 │ █████████████████▎ │
│ 20 │ 521665 │ █████████████████▍ │
│ 21 │ 542078 │ ██████████████████ │
│ 22 │ 493642 │ ████████████████▍  │
│ 23 │ 400397 │ █████████████▎     │
└────┴────────┴────────────────────┘
```

<span id="transform"></span>
## transform
By definition, transform certain elements into others. This function can be used in two ways:

1. `transform(x, array_from, array_to, default)`

`x` - the value to be transformed.
`array_from` - the constant array used for the transformation.
`array_to` - the constant array to transform ‘from’ values into.
`Default` – If 'x' is not equal to any value in 'from', it converts to the default value.
`Array_from` and `array_to` – Arrays of the same size.
Type constraints:
`transform(T, Array(T), Array(U), U) -> U`
`T` and `U` can be String, Date, DateTime, or any numeric type. For the same letter (T or U), if a numeric type, they need not be exactly the same but should have the same type category. For example, the first parameter is Int64 type, and the second parameter is Array(UInt16) type.
If 'x' equals an element in 'array_from', it will return a corresponding element from 'array_to' (same index). Otherwise, it returns 'default'. If 'array_from' matches multiple elements, it returns the first matched element.
Example:
```SQL
SELECT transform(SearchEngineID, [2, 3], ['Yandex', 'Google'], 'Other') AS title, count() AS c FROM test.hitsWHERE SearchEngineID != 0GROUP BY title ORDER BY c DESC
```

```plaintext
┌─title─────┬──────c─┐
│ Yandex    │ 498635 │
│ Google    │ 229872 │
│ Other     │ 104472 │
└───────────┴────────┘
```


1. `transform(x, array_from, array_to)`

Differs from the first method by omitting the 'default' parameter. If the value of 'x' matches an element in the 'array_from', it will return the corresponding element from 'array_to' (same index). Otherwise, it returns 'x'.
Type constraints:
`transform(T, Array(T), Array(T)) -> T`
Example:
```SQL
SELECT transform(domain(Referer), ['yandex.ru', 'google.ru', 'vk.com'], ['www.yandex', 'example.com']) AS s, count() AS c FROM test.hitsGROUP BY domain(Referer) ORDER BY count() DESCLIMIT 10
```

```plaintext
┌─s──────────────┬───────c─┐
│                │ 2906259 │
│ www.yandex     │  867767 │
│ ███████.ru     │  313599 │
│ mail.yandex.ru │  107147 │
│ ██████.ru      │  100355 │
│ █████████.ru   │   65040 │
│ news.yandex.ru │   64515 │
│ ██████.net     │   59141 │
│ example.com    │   57316 │
└────────────────┴─────────┘
```

<span id="formatreadablesize-x"></span>
## formatReadableSize(x)
Accepts size in bytes. Returns a string with suffixes (KiB, MiB, etc.).
Example:
```SQL
SELECT arrayJoin([1, 1024, 1024*1024, 192851925]) AS filesize_bytes, formatReadableSize(filesize_bytes) AS filesize
```

```plaintext
┌─filesize_bytes─┬─filesize───┐
│              1 │ 1.00 B     │
│           1024 │ 1.00 KiB   │
│        1048576 │ 1.00 MiB   │
│      192851925 │ 183.92 MiB │
└────────────────┴────────────┘
```

<span id="least-a-b"></span>
## least(a,b)
Returns the minimum value between a and b.
<span id="greatest-a-b"></span>
## greatest(a,b)
Returns the maximum value between a and b.
<span id="uptime"></span>
## uptime()
Returns the number of seconds the service is back to normal operation.
<span id="version"></span>
## version()
Returns the server's version as a string.
<span id="timezone"></span>
## timeZone()
Returns the server's time zone.
<span id="blocknumber"></span>
## blockNumber
Returns the serial number of the Block where the row is located.
<span id="rownumberinblock"></span>
## rowNumberInBlock
Returns the serial number of the row in the Block where it is located. Always recalculated for different Blocks.
<span id="rownumberinallblocks"></span>
## rowNumberInAllBlocks()
Returns the serial number of the row within the result set. This function only considers the affected Block.
<span id="runningdifference-x"></span>
## runningDifference(x)
Calculates the difference between the values of adjacent rows in the data block. Returns 0 for the first row and the difference from the previous row for each subsequent row.
The result of the function depends on the affected Block and the data order within the Block. If a subquery is created using ORDER BY and the function is called from outside the subquery, the expected results can be obtained.
Example:
```SQL
SELECT EventID, EventTime, runningDifference(EventTime) AS delta FROM ( SELECT EventID, EventTime FROM events WHERE EventDate = '2016-11-24'ORDER BY EventTime ASCLIMIT 5 )
```

```plaintext
┌─EventID─┬───────────EventTime─┬─delta─┐
│    1106 │ 2016-11-24 00:00:04 │     0 │
│    1107 │ 2016-11-24 00:00:05 │     1 │
│    1108 │ 2016-11-24 00:00:05 │     0 │
│    1109 │ 2016-11-24 00:00:09 │     4 │
│    1110 │ 2016-11-24 00:00:10 │     1 │
└─────────┴─────────────────────┴───────┘
```

<span id="runningdifferencestartingwithfirstvalue"></span>
## runningDifferenceStartingWithFirstValue
Similar to runningDifference, but the difference is that the first row returns the value of the first row, and each subsequent row returns the difference from the previous row.
<span id="macnumtostring-num"></span>
## MACNumToString(num)
Accepts a UInt64 type number. Interprets it as a MAC address in big endian. Returns a string containing the corresponding MAC address in the format AA:BB:CC:DD:EE:FF (hexadecimal numbers separated by colons).
<span id="macstringtonum-s"></span>
## MACStringToNum(s)
Opposite of MACNumToString. If the MAC address format is invalid, returns 0.
<span id="macstringtooui-s"></span>
## MACStringToOUI(s)
Accept MAC addresses in the format AA:BB:CC:DD:EE:FF (hexadecimal numbers separated by colons). Return the first three octets as a UInt64 number. If the MAC address format is invalid, return 0.
<span id="getsizeofenumtype"></span>
## getSizeOfEnumType
Return the number of enumerators in the enum.
```plaintext
getSizeOfEnumType(value)
```

Parameters:

* `Value` — a value of type `Enum`.

Return value

* The number of enumerators in `the enum`.
* If the type is not `an enum`, throw an exception.

Example
```plaintext
SELECT getSizeOfEnumType( CAST('a' AS Enum8('a' = 1, 'b' = 2) ) ) AS x

┌─x─┐
│ 2 │
└───┘
```

<span id="tocolumntypename"></span>
## toColumnTypeName
Returns the name of the data type of the column in RAM.
```plaintext
toColumnTypeName(value)
```

Parameters:

* `value` — Any type of value.

Return Value

* A string, which is the type name of `value` in RAM.

`toTypeName` and toColumnTypeName difference example
```plaintext
:) select toTypeName(cast('2018-01-01 01:02:03' AS DateTime))

SELECT toTypeName(CAST('2018-01-01 01:02:03', 'DateTime'))

┌─toTypeName(CAST('2018-01-01 01:02:03', 'DateTime'))─┐
│ DateTime                                            │
└─────────────────────────────────────────────────────┘

1 rows in set. Elapsed: 0.008 sec.

:) select toColumnTypeName(cast('2018-01-01 01:02:03' AS DateTime))

SELECT toColumnTypeName(CAST('2018-01-01 01:02:03', 'DateTime'))

┌─toColumnTypeName(CAST('2018-01-01 01:02:03', 'DateTime'))─┐
│ Const(UInt32)                                             │
└───────────────────────────────────────────────────────────┘
```

The example shows the `DateTime` data type stored in memory as `Const(UInt32)`.
<span id="dumpcolumnstructure"></span>
## dumpColumnStructure
Output the detailed data results in RAM.
```plaintext
dumpColumnStructure(value)
```

Parameters:

* `Value` — Any type of value.

Return Value

* A string that provides a detailed description of the data structure of `value` in RAM.

Example
```plaintext
SELECT dumpColumnStructure(CAST('2018-01-01 01:02:03', 'DateTime'))

┌─dumpColumnStructure(CAST('2018-01-01 01:02:03', 'DateTime'))─┐
│ DateTime, Const(size = 1, UInt32(size = 1))                  │
└──────────────────────────────────────────────────────────────┘
```

<span id="defaultvalueofargumenttype"></span>
## defaultValueOfArgumentType
Outputs the default value of the data type.
Does not include the default values of custom columns set by the user.
```plaintext
defaultValueOfArgumentType(expression)
```

Parameters:

* `Expression` — Any type of value or expression that results in a value of any type.

Return value

* Numerical types return `0`.
* String types return an empty string.
* Nullable types return `NULL`.

Example
```plaintext
:) SELECT defaultValueOfArgumentType( CAST(1 AS Int8) )

SELECT defaultValueOfArgumentType(CAST(1, 'Int8'))

┌─defaultValueOfArgumentType(CAST(1, 'Int8'))─┐
│                                           0 │
└─────────────────────────────────────────────┘

1 rows in set. Elapsed: 0.002 sec.

:) SELECT defaultValueOfArgumentType( CAST(1 AS Nullable(Int8) ) )

SELECT defaultValueOfArgumentType(CAST(1, 'Nullable(Int8)'))

┌─defaultValueOfArgumentType(CAST(1, 'Nullable(Int8)'))─┐
│                                                  ᴺᵁᴸᴸ │
└───────────────────────────────────────────────────────┘

1 rows in set. Elapsed: 0.002 sec.
```

<span id="indexhint"></span>
## indexHint
Outputs all data within the range of selected indexes, without filtering using the expressions in the parameters.
The expression arguments passed to the function will not be computed, but ClickHouse uses the expressions in the parameters for index filtering.
Return value
Example
This is a test table that contains a dataset with [ontime](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/zh/getting-started/example-datasets/ontime.md).
```plaintext
SELECT count() FROM ontime

┌─count()─┐
│ 4276457 │
└─────────┘
```

The table uses `(FlightDate, (Year, FlightDate))` as an index.
Query the table as follows:
```plaintext
:) SELECT FlightDate AS k, count() FROM ontime GROUP BY k ORDER BY k

SELECT
    FlightDate AS k,
    count()
FROM ontime
GROUP BY k
ORDER BY k ASC

┌──────────k─┬─count()─┐
│ 2017-01-01 │   13970 │
│ 2017-01-02 │   15882 │
........................
│ 2017-09-28 │   16411 │
│ 2017-09-29 │   16384 │
│ 2017-09-30 │   12520 │
└────────────┴─────────┘

273 rows in set. Elapsed: 0.072 sec. Processed 4.28 million rows, 8.55 MB (59.00 million rows/s., 118.01 MB/s.)
```

In this query, since the index is not utilized, ClickHouse processes all data in the entire table (`Processed 4.28 million rows`). Try the following query to utilize the index:
```plaintext
:) SELECT FlightDate AS k, count() FROM ontime WHERE k = '2017-09-15' GROUP BY k ORDER BY k

SELECT
    FlightDate AS k,
    count()
FROM ontime
WHERE k = '2017-09-15'
GROUP BY k
ORDER BY k ASC

┌──────────k─┬─count()─┐
│ 2017-09-15 │   16428 │
└────────────┴─────────┘

1 rows in set. Elapsed: 0.014 sec. Processed 32.74 thousand rows, 65.49 KB (2.31 million rows/s., 4.63 MB/s.)
```

In the last line display, through the index, the number of rows processed by ClickHouse has notably decreased (`Processed 32.74 thousand rows`).
Now, pass the expression `k = '2017-09-15'` to the `indexHint` function:
```plaintext
:) SELECT FlightDate AS k, count() FROM ontime WHERE indexHint(k = '2017-09-15') GROUP BY k ORDER BY k

SELECT
    FlightDate AS k,
    count()
FROM ontime
WHERE indexHint(k = '2017-09-15')
GROUP BY k
ORDER BY k ASC

┌──────────k─┬─count()─┐
│ 2017-09-14 │    7071 │
│ 2017-09-15 │   16428 │
│ 2017-09-16 │    1077 │
│ 2017-09-30 │    8167 │
└────────────┴─────────┘

4 rows in set. Elapsed: 0.004 sec. Processed 32.74 thousand rows, 65.49 KB (8.97 million rows/s., 17.94 MB/s.)
```

For this request, ClickHouse applied the index in the same manner as the previous occasion (`Processed 32.74 thousand rows`). However, the result set ultimately did not filter the results based on the expression `k = '2017-09-15'`.
Due to the use of sparse indexes in ClickHouse, "additional" data will be included in the index results when reading ranges (adjacent dates in this example). The `indexHint` function can be used to see them.
<span id="replicate"></span>
## replicate
Fill an array with a single value.
Used for the internal implementation of arrayJoin.
```plaintext
replicate(x, arr)
```

Parameters:

* `arr` — The original array. ClickHouse creates a new array of the same length as the original data and fills it with value `x`.
* `x` — The value with which the generated array will be filled.

Output

* An array filled with `x`.

Example
```plaintext
SELECT replicate(1, ['a', 'b', 'c'])

┌─replicate(1, ['a', 'b', 'c'])─┐
│ [1,1,1]                       │
└───────────────────────────────┘
```

<span id="filesystemavailable"></span>
## filesystemAvailable
Return information on remaining disk space (in bytes). Evaluate this information using the path configuration in the configuration file.
<span id="filesystemcapacity"></span>
## filesystemCapacity
Return disk capacity information, in bytes. Evaluate this information using the path configuration in the configuration file.
<span id="finalizeaggregation"></span>
## finalizeAggregation
Retrieve the state of the aggregate function. Return the aggregate result (final state).
<span id="runningaccumulate"></span>
## runningAccumulate
Retrieve the state of the aggregate function and return its specific value. This is the cumulative result of all rows from the first row to the current row.
For example, obtaining the state of the aggregate function (Example: runningAccumulate(uniqState(UserID))), returns the result of the aggregate function merged from all previous rows and the current row for each row of the data block. Therefore, the result of the function depends on the order of the data blocks in the partition and the order of the rows in the data blocks.
<span id="joinget-‘join-storage-table-name’-‘get-column’-join-key-joingetjoin-storage-table-name-get-column-join-key"></span>
## joinGet(‘join_storage_table_name’, ‘get_column’,join_key) {#joingetjoin-storage-table-name-get-column-join-key}
Use the specified join key to retrieve data from the table of the Join type engine.
<span id="modelevaluate-model-name-…"></span>
## modelEvaluate(model_name, …)
Use external models for calculation. Accept the name and parameters of the model. Return a Float64 type value.
<span id="throwif-x"></span>
## throwIf(x)
If the parameter is not zero, then throw an exception.
