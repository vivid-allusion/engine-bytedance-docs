---
title: "Type Conversion Function"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/type-conversion-function"
---

<span id="数值类型转换常见的问题"></span>
## Common Problems with Numeric Type Conversions
When you convert a value from one type to another, it is important to note that this is an unsafe operation that might lead to data loss. Data loss usually occurs when you convert a large data type to a smaller one, or when you convert two different data types to each other.
ClickHouse and C++ have the same type conversion behavior.
<span id="toint-8-16-32-64"></span>
## toInt(8|16|32|64)
Convert an input value to Int type. This function includes:

* `toInt8(expr)` — results in `Int8` data type.
* `toInt16(expr)` — results in `Int16` data type.
* `toInt32(expr)` — the result is of `Int32` data type.
* `toInt64(expr)` — the result is of `Int64` data type.

Parameters

* `expr` — expression returns a number or a string representing a numeric type. Does not support binary, octal, or hexadecimal number forms; zeros before the valid digits are also ignored.

Return Value
Integer types in `Int8`, `Int16`, `Int32`, or `Int64` data types.
The function uses [rounding towards zero](https://en.wikipedia.org/wiki/Rounding#Rounding_towards_zero) principle, which means it truncates and discards the fractional part.
NaN and Inf conversion is uncertain. For specific usage, please refer to the **Common Issues with Numeric Type Conversions** at the top of the article.
Example
```SQL
SELECT toInt64(nan), toInt32(32), toInt16('16'), toInt8(8.8)
```

```plaintext
┌─────────toInt64(nan)─┬─toInt32(32)─┬─toInt16('16')─┬─toInt8(8.8)─┐
│ -9223372036854775808 │          32 │            16 │           8 │
└──────────────────────┴─────────────┴───────────────┴─────────────┘
```

<span id="toint-8-16-32-64-orzero"></span>
## toInt(8|16|32|64)OrZero
This function requires a character type argument and tries to convert it to `Int (8 | 16 | 32 | 64)`. If the conversion fails, it directly returns 0.
Example
```SQL
select toInt64OrZero('123123'), toInt8OrZero('123qwe123')
```

```plaintext
┌─toInt64OrZero('123123')─┬─toInt8OrZero('123qwe123')─┐
│                  123123 │                         0 │
└─────────────────────────┴───────────────────────────┘
```

<span id="toint-8-16-32-64-ornull"></span>
## toInt(8|16|32|64)OrNull
This function requires a character type argument and tries to convert it to `Int (8 | 16 | 32 | 64)`. If the conversion fails, it directly returns `NULL`.
Example
```SQL
select toInt64OrNull('123123'), toInt8OrNull('123qwe123')
```

```plaintext
┌─toInt64OrNull('123123')─┬─toInt8OrNull('123qwe123')─┐
│                  123123 │                      ᴺᵁᴸᴸ │
└─────────────────────────┴───────────────────────────┘
```

<span id="touint-8-16-32-64"></span>
## toUInt(8|16|32|64)
Convert an input value into UInt type. This function includes:

* `toUInt8(expr)` — results in `UInt8` data type.
* `toUInt16(expr)` — results in `UInt16` data type.
* `toUInt32(expr)` — results in `UInt32` data type.
* `toUInt64(expr)` — results in `UInt64` data type.

Parameters

* `expr` — expression returns a number or a string representing a numeric type. Binary, octal, and hexadecimal forms of numbers are not supported; leading zeros in valid numbers are also ignored.

Return Value
Integer data types in `UInt8`, `UInt16`, `UInt32`, or `UInt64`.
The function uses [rounding towards zero](https://en.wikipedia.org/wiki/Rounding#Rounding_towards_zero) principle, which means it truncates the fractional part of the number.
The conversion result is undefined for negative numbers and NaN and Inf. If you pass a negative number, such as `'-32'`, ClickHouse will throw an exception. For specific usage, please refer to **common issues with numeric type conversions**.
Example
```SQL
SELECT toUInt64(nan), toUInt32(-32), toUInt16('16'), toUInt8(8.8)
```

```plaintext
┌───────toUInt64(nan)─┬─toUInt32(-32)─┬─toUInt16('16')─┬─toUInt8(8.8)─┐
│ 9223372036854775808 │    4294967264 │             16 │            8 │
└─────────────────────┴───────────────┴────────────────┴──────────────┘
```

<span id="touint-8-16-32-64-orzero"></span>
## toUInt(8|16|32|64)OrZero
<span id="touint-8-16-32-64-ornull"></span>
## toUInt(8|16|32|64)OrNull
<span id="tofloat-32-64"></span>
## toFloat(32|64)
<span id="tofloat-32-64-orzero"></span>
## toFloat(32|64)OrZero
<span id="tofloat-32-64-ornull"></span>
## toFloat(32|64)OrNull
<span id="todate"></span>
## toDate
<span id="todateorzero"></span>
## toDateOrZero
<span id="todateornull"></span>
## toDateOrNull
<span id="todatetime"></span>
## toDateTime
<span id="todatetimeorzero"></span>
## toDateTimeOrZero
<span id="todatetimeornull"></span>
## toDateTimeOrNull
<span id="todecimal-32-64-128"></span>
## toDecimal(32|64|128)
Convert `value` to a Decimal type with precision `S`. `Value` can be a number or a string. `S` specifies the precision of decimal places.

* `toDecimal32(value, S)`
* `toDecimal64(value, S)`
* `toDecimal128(value, S)`

<span id="todecimal-32-64-128-ornull"></span>
## toDecimal(32|64|128)OrNull
Convert an input character to a Nullable(Decimal(P,S)) type data. This function includes:

* `toDecimal32OrNull(expr, S)` — results in a `Nullable(Decimal32(S))` data type.
* `toDecimal64OrNull(expr, S)` — The result is of `Nullable(Decimal64(S))` data type.
* `toDecimal128OrNull(expr, S)` — The result is of `Nullable(Decimal128(S))` data type.

If you want to receive a `NULL` value instead of throwing an exception when an error occurs while parsing the input value, you can use this function.
Parameters

* `expr` — Expression returns a data of String type. ClickHouse tends to represent numerical values with decimal types in text format, such as `'1.111'`.
* `S` — Precision of the decimal places.

Return Value
Data of type `Nullable(Decimal(P,S))`, including:

* If applicable, decimal places `S`.
* If a parsing error occurs or the number of decimal places in the entered number exceeds `S`, the result will be `NULL`.

Example
```SQL
SELECT toDecimal32OrNull(toString(-1.111), 5) AS val, toTypeName(val)
```

```SQL
┌──────val─┬─toTypeName(toDecimal32OrNull(toString(-1.111), 5))─┐
│ -1.11100 │ Nullable(Decimal(9, 5))                            │
└──────────┴────────────────────────────────────────────────────┘
```

```SQL
SELECT toDecimal32OrNull(toString(-1.111), 2) AS val, toTypeName(val)
```

```plaintext
┌──val─┬─toTypeName(toDecimal32OrNull(toString(-1.111), 2))─┐
│ ᴺᵁᴸᴸ │ Nullable(Decimal(9, 2))                            │
└──────┴────────────────────────────────────────────────────┘
```

<span id="todecimal-32-64-128-orzero"></span>
## toDecimal(32|64|128)OrZero
Convert the input value to data type Decimal(P,S). This function includes:

* `toDecimal32OrZero(expr, S)` — Results in `Decimal32(S)` data type.
* `toDecimal64OrZero(expr, S)` — Results in `Decimal64(S)` data type.
* `toDecimal128OrZero(expr, S)` — Results in `Decimal128(S)` data type.

When a parsing error occurs and you want to get a `0` value without throwing an exception, you can use this function.
Parameter

* `expr` — Expression returns a data of String type. ClickHouse prefers to represent numerical values with decimal types as text, such as `'1.111'`.
* `S` — Precision of decimal places.

Return Value
A value in the `Nullable(Decimal(P,S))` data type. The value contains:

* If applicable, the number of decimal places `S`.
* If there is a parsing error or if the number of decimal places in the input exceeds `S`, the result will be a 0 with a decimal precision of S. Example`0 with a decimal precision of S`. Example

```SQL
SELECT toDecimal32OrZero(toString(-1.111), 5) AS val, toTypeName(val)
```

```SQL
┌──────val─┬─toTypeName(toDecimal32OrZero(toString(-1.111), 5))─┐
│ -1.11100 │ Decimal(9, 5)                                      │
└──────────┴────────────────────────────────────────────────────┘
```

```SQL
SELECT toDecimal32OrZero(toString(-1.111), 2) AS val, toTypeName(val)
```

```SQL
┌──val─┬─toTypeName(toDecimal32OrZero(toString(-1.111), 2))─┐
│ 0.00 │ Decimal(9, 2)                                      │
└──────┴────────────────────────────────────────────────────┘
```

<span id="tostring"></span>
## toString
These functions are used for conversions between numbers, strings (excluding FixedString), Date, and DateTime. All functions take one argument.
When converting other types to strings or from strings to other types, formatting or parsing of the string value adheres to the same rules as the TabSeparated format. If the string cannot be parsed, an exception is thrown, and the query is cancelled.
When converting a Date to a number or vice versa, Date corresponds to the number of days in the Unix timestamp. When converting DateTime to a number or vice versa, DateTime corresponds to the number of seconds in the Unix timestamp.
The definitions for date and datetime formats in toDate/toDateTime functions are as follows:
```plaintext
YYYY-MM-DD
YYYY-MM-DD hh:mm:ss
```

However, if UInt32, Int32, UInt64, or Int64 numeric values are converted to Date type and the corresponding values are greater than or equal to 65536, the values will be parsed as Unix timestamps (instead of the corresponding number of days). This means that it is permissible to write 'toDate(unix_timestamp)', a common scenario, otherwise, it would be an error, and it would require writing the more cumbersome 'toDate(toDateTime(unix_timestamp))'.
The conversion between Date and DateTime occurs in a more natural way: by adding an empty time or removing time.
The conversion between numeric types follows the same rules as the assignment between different numeric types in C++.
Furthermore, the toString function of the DateTime parameter can include a timezone name in the second parameter. For example: `Asia/Yekaterinburg` in this case, the time is formatted according to the specified timezone.
SELECT now() AS now_local, toString(now(), 'Asia/Yekaterinburg') AS now_yekat
```plaintext
┌───────────now_local─┬─now_yekat───────────┐
│ 2016-06-15 00:11:21 │ 2016-06-15 02:11:21 │
└─────────────────────┴─────────────────────┘
```

Also see the `toUnixTimestamp` function.
<span id="tofixedstring-s-n"></span>
## toFixedString(s,N)
Convert a String type parameter into a FixedString(N) type value (a string with a fixed length N). N must be a constant. If the number of bytes in the string is less than N, it will be right-padded with null bytes. If the number of bytes in the string exceeds N, an exception is thrown.
<span id="tostringcuttozero-s"></span>
## toStringCutToZero(s)
Accepts either a String or a FixedString parameter. Returns a String, which content is truncated at the first zero byte found.
Example:
```SQL
SELECT toFixedString('foo', 8) AS s, toStringCutToZero(s) AS s_cut
```

```plaintext
┌─s─────────────┬─s_cut─┐
│ foo\0\0\0\0\0 │ foo   │
└───────────────┴───────┘
```

```SQL
SELECT toFixedString('foo\0bar', 8) AS s, toStringCutToZero(s) AS s_cut
```

```plaintext
┌─s──────────┬─s_cut─┐
│ foo\0bar\0 │ foo   │
└────────────┴───────┘
```

<span id="reinterpretasuint-8-16-32-64"></span>
## reinterpretAsUInt(8|16|32|64)
<span id="reinterpretasint-8-16-32-64"></span>
## reinterpretAsInt(8|16|32|64)
<span id="reinterpretasfloat-32-64"></span>
## reinterpretAsFloat(32|64)
<span id="reinterpretasdate"></span>
## reinterpretAsDate
<span id="reinterpretasdatetime"></span>
## reinterpretAsDateTime
These functions take a string and interpret the bytes at the beginning of the string as numbers in host order (little endian). If the string is not long enough, the functions act as if the string were padded with the necessary number of null bytes. If the string is longer than necessary, the extra bytes are ignored. Date is interpreted as the number of days in a Unix timestamp, and DateTime is interpreted as a Unix timestamp.
<span id="reinterpretasstring"></span>
## reinterpretAsString
This function accepts numbers, Date, or DateTime, and returns a string containing bytes representing the corresponding value in host order (little-endian). Remove trailing null bytes. For example, the UInt32 type value 255 is a string one byte long.
<span id="reinterpretasfixedstring"></span>
## reinterpretAsFixedString
This function accepts numbers, Date, or DateTime, and returns a FixedString containing bytes representing the corresponding value in host order (little-endian). Remove trailing null bytes. For example, the UInt32 type value 255 is a FixedString one byte long.
<span id="cast-x-t"></span>
## CAST(x, T)
Convert 'x' to 't' data type. It also supports the syntax CAST (x AS t).
Example:
```SQL
SELECT'2016-06-15 23:00:00' AS timestamp, CAST(timestamp AS DateTime) AS datetime, CAST(timestamp AS Date) AS date, CAST(timestamp, 'String') AS string, CAST(timestamp, 'FixedString(22)') AS fixed_string
```

```plaintext
┌─timestamp───────────┬────────────datetime─┬───────date─┬─string──────────────┬─fixed_string──────────────┐
│ 2016-06-15 23:00:00 │ 2016-06-15 23:00:00 │ 2016-06-15 │ 2016-06-15 23:00:00 │ 2016-06-15 23:00:00\0\0\0 │
└─────────────────────┴─────────────────────┴────────────┴─────────────────────┴───────────────────────────┘
```

Convert arguments to FixedString(N), applicable only to String or FixedString(N) types.
Supports converting data into nullable types. For instance:
```plaintext
SELECT toTypeName(x) FROM t_null

┌─toTypeName(x)─┐
│ Int8          │
│ Int8          │
└───────────────┘

SELECT toTypeName(CAST(x, 'Nullable(UInt16)')) FROM t_null

┌─toTypeName(CAST(x, 'Nullable(UInt16)'))─┐
│ Nullable(UInt16)                        │
│ Nullable(UInt16)                        │
└─────────────────────────────────────────┘
```

<span id="tointerval-year-quarter-month-week-day-hour-minute-second"></span>
## toInterval(Year|Quarter|Month|Week|Day|Hour|Minute|Second)
Convert a numeric value into an [Interval](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/en/sql-reference/data-types/special-data-types/interval.md) type.
Syntax
toIntervalSecond(number) toIntervalMinute(number) toIntervalHour(number) toIntervalDay(number) toIntervalWeek(number) toIntervalMonth(number) toIntervalQuarter(number) toIntervalYear(number)
Parameters

* `number` — A positive integer representing a duration.

Return Value

* The Interval value of time.

Example
```SQL
WITH toDate('2019-01-01') AS date, INTERVAL 1 WEEK AS interval_week, toIntervalWeek(1) AS interval_to_week SELECTdate + interval_week, date + interval_to_week
```

```plaintext
┌─plus(date, interval_week)─┬─plus(date, interval_to_week)─┐
│                2019-01-08 │                   2019-01-08 │
└───────────────────────────┴──────────────────────────────┘
```

<span id="parsedatetimebesteffort"></span>
## parseDateTimeBestEffort
Converts a time date of type String into a DateTime data type.
This function can parse formats including [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601), [RFC 1123 - 5.2.14 RFC-822 Date and Time Specification](https://tools.ietf.org/html/rfc1123#page-55), or other ClickHouse specific date and time formats.
Syntax
parseDateTimeBestEffort(time_string [, time_zone]);
Parameter

* `time_string` — Character type of time and date.
* `time_zone` — Character type of timezone.

Support for non-standard formats

* 9 or 10-digit numeric time, [unix timestamp](https://en.wikipedia.org/wiki/Unix_time).
* String composed of time and date: `YYYYMMDDhhmmss`, `DD/MM/YYYY hh:mm:ss`, `DD-MM-YY hh:mm`, `YYYY-MM-DD hh:mm:ss`, and others.
* String containing only date: `YYYY`, `YYYYMM`, `YYYY*MM`, `DD/MM/YYYY`, `DD-MM-YY`, and others.
* String containing only day and time: `DD`, `DD hh`, `DD hh:mm`. In this case, `YYYY-MM` defaults to `2000-01`.
* Includes date, time, and timezone information: `YYYY-MM-DD hh:mm:ss ±h:mm`, and others. For example: `2020-12-12 17:36:00 -5:00`.

This function parses the month using the full month name or the first three characters of the month name, for example: `24/DEC/18`, `24-Dec-18`, `01-September-2018`.
Return Value

* `DateTime` type data.

Example
Query:
```SQL
SELECT parseDateTimeBestEffort('12/12/2020 12:12:57') AS parseDateTimeBestEffort;
```

Result:
```plaintext
┌─parseDateTimeBestEffort─┐
│     2020-12-12 12:12:57 │
└─────────────────────────┘
```

Query:
```SQL
SELECT parseDateTimeBestEffort('Sat, 18 Aug 2018 07:22:16 GMT', 'Europe/Moscow') AS parseDateTimeBestEffort
```

Result:
```plaintext
┌─parseDateTimeBestEffort─┐
│     2018-08-18 10:22:16 │
└─────────────────────────┘
```

Query:
```SQL
SELECT parseDateTimeBestEffort('1284101485') AS parseDateTimeBestEffort
```

Result:
```plaintext
┌─parseDateTimeBestEffort─┐
│     2015-07-07 12:04:41 │
└─────────────────────────┘
```

Query:
```SQL
SELECT parseDateTimeBestEffort('2018-12-12 10:12:12') AS parseDateTimeBestEffort
```

Result:
```plaintext
┌─parseDateTimeBestEffort─┐
│     2018-12-12 10:12:12 │
└─────────────────────────┘
```

Query:
```SQL
SELECT parseDateTimeBestEffort('10 20:19')
```

Result:
```plaintext
┌─parseDateTimeBestEffort('10 20:19')─┐
│                 2000-01-10 20:19:00 │
└─────────────────────────────────────┘
```

<span id="parsedatetimebesteffortornull"></span>
## parseDateTimeBestEffortOrNull
This function is essentially identical to parseDateTimeBestEffort, except that it returns `NULL` if the parsing fails.
<span id="parsedatetimebesteffortorzero"></span>
## parseDateTimeBestEffortOrZero
This function is essentially identical to parseDateTimeBestEffort, except that it returns `0` if the parsing fails.
<span id="tolowcardinality"></span>
## toLowCardinality
Convert input values to the same type of data in LowCardianlity.
Use CAST function to convert data of LowCardinalCAST function to convert data of LowCardinality type to other types. For example, `CAST(x as String)`.
Grammar
toLowCardinality(expr)
Param

* `expr` — Expression is a type of supported data type.

Return value

* The result of `expr`.

Type: `LowCardinality(expr_result_type)`
Examples
Search:
```SQL
SELECT toLowCardinality('1')
```

As a result:
```plaintext
┌─toLowCardinality('1')─┐
│ 1                     │
└───────────────────────┘
```

<span id="tounixtimestamp64milli"></span>
## toUnixTimestamp64Milli
<span id="tounixtimestamp64micro"></span>
## toUnixTimestamp64Micro
<span id="tounixtimestamp64nano"></span>
## toUnixTimestamp64Nano
Convert a `DateTime64` type data to `Int64` type data, the result contains fixed sub-second precision. The change in the input value depends on the precision of the input. Please note that the output value is a UTC Timestamp, not a `DateTime64` value in the same Timezone.
Syntax
toUnixTimestamp64Milli(value)
Param

* `value` — Any precision of DateTime64 type data.

Return value

* `Data type Int64` value.

Example
Search:
```SQL
WITH toDateTime64('2019-09-16 19:20:12.345678910', 6) AS dt64 SELECT toUnixTimestamp64Milli(dt64)
```

As a result:
```plaintext
┌─toUnixTimestamp64Milli(dt64)─┐
│                1568650812345 │
└──────────────────────────────┘
```

```SQL
WITH toDateTime64('2019-09-16 19:20:12.345678910', 6) AS dt64 SELECT toUnixTimestamp64Nano(dt64)
```

As a result:
```plaintext
┌─toUnixTimestamp64Nano(dt64)─┐
│         1568650812345678000 │
└─────────────────────────────┘
```

<span id="fromunixtimestamp64milli"></span>
## fromUnixTimestamp64Milli
<span id="fromunixtimestamp64micro"></span>
## fromUnixTimestamp64Micro
<span id="fromunixtimestamp64nano"></span>
## fromUnixTimestamp64Nano
Convert `Int64` type data to `DateTime64` type data, which includes fixed sub-second accuracy and an optional timezone. The increase or decrease of the input value depends on its precision. It is important to note that the input value is a UTC timestamp, not a timestamp that includes a timezone.
Syntax
fromUnixTimestamp64Milli(value [, ti])
Parameters

* `value` — `Int64` type data, which can be of any precision.
* `timezone` — `String` type timezone

Return Value

* `value` — Data of DateTime64 type.

Example
```SQL
WITH CAST(1234567891011, 'Int64') AS i64 SELECT fromUnixTimestamp64Milli(i64, 'UTC')
```

```plaintext
┌─fromUnixTimestamp64Milli(i64, 'UTC')─┐
│              2009-02-13 23:31:31.011 │
└──────────────────────────────────────┘
```
