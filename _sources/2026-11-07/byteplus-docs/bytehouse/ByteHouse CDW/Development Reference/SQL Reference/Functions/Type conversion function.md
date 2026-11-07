---
title: "Type conversion function"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-type-conversion"
---

<span id="7d4eb97a"></span>
### CAST

Converts the input value to the specified data type. Unlike the reinterpret function, `CAST` attempts to present the same value using the new data type. If the conversion cannot be completed, an exception is raised.

**Syntax**

```SQL
CAST(x, T)
CAST(x AS t)
```


**Parameter**


* `x`— The value to be converted. Can be of any type.

* `T`— The name of the target data type. String.

* `t`— Target data type.


**Return value**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Converted value.</div>


<div data-tips="true" data-tips-type="tip">If the input value is not as expected within the target scope, the result will overflow. For instance, <code>CAST(-1, 'UInt8')</code> returns <code>255</code>.</div>


**Example**

```SQL
SELECT CAST(toInt8(-1), 'UInt8') AS cast_int_to_uint, CAST(1.5 AS Decimal(3,2)) AS cast_float_to_decimal;
```


```Plain
┌─cast_int_to_uint─┬─cast_float_to_decimal─┐
│ 255              │ 1.50                  │
└──────────────────┴───────────────────────┘
```


```SQL
SELECT'2016-06-15 23:00:00' AS timestamp,CAST(timestamp AS DateTime) AS datetime,CAST(timestamp AS Date) AS date,CAST(timestamp, 'String') AS string,CAST(timestamp, 'FixedString(22)') AS fixed_string;
```


```Plain
┌─timestamp───────────┬─datetime────────────┬─date───────┬─string──────────────┬─fixed_string────────┐
│ 2016-06-15 23:00:00 │ 2016-06-15 23:00:00 │ 2016-06-15 │ 2016-06-15 23:00:00 │ 2016-06-15 23:00:00 │
└─────────────────────┴─────────────────────┴────────────┴─────────────────────┴─────────────────────┘
```


Conversion to FixedString(N) is only applicable to parameters of String or FixedString types.

Supports conversion to Nullable and reverting back.

```SQL
SELECT toTypeName(number) FROM numbers(2);
```


```Plain
┌─toTypeName(number)─┐
│ UInt64             │
│ UInt64             │
└────────────────────┘
```


```SQL
SELECT toTypeName(CAST(number, 'Nullable(UInt64)')) FROM numbers(2);
```


```Plain
┌─toTypeName(CAST(number, 'Nullable(UInt64)'))─┐
│ Nullable(UInt64)                             │
│ Nullable(UInt64)                             │
└──────────────────────────────────────────────┘
```


<span id="2737eb20"></span>
### reinterpretAsDate

These functions accept a string and interpret the initial bytes of the string as a number in host order (little\-endian). If the string is not long enough, these functions work as if filling the string with the necessary amount of null bytes. If the string is longer than needed, the extra bytes are ignored. The date is interpreted as the total number of days since the Unix epoch.

**Syntax**

```SQL
reinterpretAsDate(fixed_string)
```


**Param**


* `fixed_string`— A string represented in bytes.


**Return value**


* Appointment time.


**Example**

```SQL
SELECT reinterpretAsDate(reinterpretAsString(toDate('2019-01-01')));
```


```Plain
┌─reinterpretAsDate(reinterpretAsString(toDate('2019-01-01')))─┐
│ 2019-01-01                                                   │
└──────────────────────────────────────────────────────────────┘
```


<span id="6ae42a6b"></span>
### reinterpretAsDateTime

These functions accept a string and interpret the bytes at the beginning of the string as a number in host order (little\-endian). If the string is not long enough, the functions work as if the string were padded with the necessary number of null bytes. If the string is longer than needed, ignore the extra bytes. Dates are interpreted as the number of days since the Unix Epoch, and dates with time are interpreted as the number of seconds since the Unix Epoch.

**Syntax**

```SQL
reinterpretAsDateTime(fixed_string)
```


**Param**


* `fixed_string`— A string represented in bytes.


**Return value**


* Appointment time.


**Example**

```SQL
SELECT reinterpretAsDateTime(reinterpretAsString(toDateTime('2019-01-01 00:00:00')));
```


```Plain
┌─reinterpretAsDateTime(reinterpretAsString(toDateTime('2019-01-01 00:00:00')))─┐
│ 2019-01-01 00:00:00                                                           │
└───────────────────────────────────────────────────────────────────────────────┘
```


<span id="5b80782a"></span>
### reinterpretAsFixedString

This function accepts numbers or dates or dates with time, and returns a FixedString containing bytes that represent the corresponding values in host order (little\-endian). Trailing null bytes will be deleted. For example, a UInt32 type value of 255 is a FixedString one byte long.

**Syntax**

```SQL
reinterpretAsFixedString(x)
```


**Param**


* `x`— Number, Date, or Date with Time.


**Return value**


* Fixed String.


**Example**

```SQL
SELECT reinterpretAsFixedString(toDate('2019-01-01'));
```


```Plain
┌─reinterpretAsFixedString(toDate('2019-01-01'))─┐
│ �E                                             │
└────────────────────────────────────────────────┘
```


<span id="f267123d"></span>
### reinterpretAsString

This function accepts a number, date, or date with time, and returns a string containing bytes that represent the corresponding value in host order (little\-endian). Remove trailing null bytes. For example, the UInt32 type value 255 is a string of 1 byte in length.

**Syntax**

```SQL
reinterpretAsString(value)
```


**Parameters**


* `value`— A number, date, or date with time


**Return Value**


* String represented in bytes.


**Example**

```SQL
SELECT reinterpretAsString(toDate('2019-01-01'));
```


```Plain
┌─reinterpretAsString(toDate('2019-01-01'))─┐
│ �E                                        │
└───────────────────────────────────────────┘
```


<span id="bc2c1c26"></span>
### toDate

Converts strings, dates, date\-times, UInt\* numbers into date types

。 toDate

**Grammar**

```SQL
toDate(time)
```


**Param**


* `Time`— string, date, date\-time, UInt\* Number.


**Return value**


* Date


**Example**

```SQL
SELECT toDate('2019-01-01');
```


```Plain
┌─cast_int_to_uint─┬─cast_float_to_decimal─┐
│ 255              │ 1.50                  │
└──────────────────┴───────────────────────┘
```


```SQL
SELECT toDate(1);
```


```Plain
┌─toDate(1)──┐
│ 1970-01-02 │
└────────────┘
```


```SQL
SELECT toDate(toDateTime('2019-01-01 00:00:00'));
```


```Plain
┌─toDate(toDateTime('2019-01-01 00:00:00'))─┐
│ 2019-01-01                                │
└───────────────────────────────────────────┘
```


<span id="30a2c2d0"></span>
### toDecimal (32|64)

Convert `value` to a Decimal data type with precision `S`. `Value` can be a number or string. `S` (scale) parameter specifies the number of decimal places.

**Syntax**

```SQL
toDecimal32(value, S) SETTINGS output_format_decimal_trailing_zeros = 1
toDecimal64(value, S) SETTINGS output_format_decimal_trailing_zeros = 1
```


**Parameters**


* `Value` can be a number or string

* `S` (scale) parameter specifies the number of decimal places.

* `SETTINGS output_format_decimal_trailing_zeros`: Optional. It controls whether the trailing zeros of decimals are retained in the display. When set to 1, it forcibly retains all trailing zeros within the specified number of decimal places; when set to 0, it automatically omits the insignificant trailing zeros of decimals.


**Return value**


* Decimal


**Examples**

```SQL
SELECT toDecimal32(1, 2) SETTINGS output_format_decimal_trailing_zeros = 1
```


```Plain
┌─toDecimal32(1, 2)─┐
│ 1.00              │
└───────────────────┘
```


```SQL
SELECT toDecimal32('1', 2) SETTINGS output_format_decimal_trailing_zeros = 1
```


```Plain
┌─toDecimal32('1', 2)─┐
│ 1.00                │
└─────────────────────┘
```


<span id="7837af72"></span>
### toDecimal(32|64)OrNull

Convert the input string to a Nullable(Decimal(P,S)) data type value.

`toDecimal*()` should be used if you prefer to get a `NULL` value instead of an exception when there is a parsing error in the input value.

**Syntax**

```SQL
toDecimal32OrNull(expr, S)
toDecimal64OrNull(expr, S)
```


**Parameters**


* `expr` — an expression that returns a value of string data type. ByteHouse requires a decimal number's text representation. Example: `'1.111'`.

* `S` — Decimal number, the decimal places of the result value.


**Return value**

Value of data type `Nullable(Decimal(P,S))`. The value contains:


* `S`It's a number with decimals if ByteHouse interprets the input string as a number.

* `NULL`If ByteHouse cannot interpret the input string as a number, or if the input number contains more than`S`decimal places.


**Example**

```SQL
SELECT toDecimal32OrNull(toString(-1.111), 5) AS val, toTypeName(val);
```


```Plain
┌─val──────┬─toTypeName(toDecimal32OrNull(toString(-1.111), 5))─┐
│ -1.11100 │ Nullable(Decimal(9, 5))                            │
└──────────┴────────────────────────────────────────────────────┘
```


```SQL
SELECT toDecimal32OrNull(toString(-1.111), 2) AS val, toTypeName(val);
sql
```


```Plain
┌─val──┬─toTypeName(toDecimal32OrNull(toString(-1.111), 2))─┐
│ ᴺᵁᴸᴸ │ Nullable(Decimal(9, 2))                            │
└──────┴────────────────────────────────────────────────────┘
```


<span id="0e26e12f"></span>
### toDecimal(32|64)OrZero

Converts the input value to the Decimal(P,S) data type.

`toDecimal*()`You should use these functions instead if you want`0`to get the value instead of an exception when there's a parsing error in the input value.

**Syntax**

```SQL
toDecimal32OrZero( expr, S)
toDecimal64OrZero( expr, S)
```


**Parameters**


* `expr`— Expression data type. ByteHouse requires a text representation of decimal numbers. For example, `'1.111'`.

* `S`— Decimal number of the result value.


**Return value**

The value of the data type `Nullable(Decimal(P,S))`. This value includes:


* `S` If ClickHouse interprets the input string as a numeric value, it returns a number with decimals.

* `S` If ClickHouse cannot interpret the input string as a numeric value, or if the input number has more than `S` decimal places, it returns a zero with decimal places.


**Example**

```SQL
SELECT toDecimal32OrZero(toString(-1.111), 5) AS val, toTypeName(val);
```


```Plain
┌─val──────┬─toTypeName(toDecimal32OrZero(toString(-1.111), 5))─┐
│ -1.11100 │ Decimal(9, 5)                                      │
└──────────┴────────────────────────────────────────────────────┘
```


```SQL
SELECT toDecimal32OrZero(toString(-1.111), 2) AS val, toTypeName(val);
```


```Plain
┌─val──┬─toTypeName(toDecimal32OrZero(toString(-1.111), 2))─┐
│ 0.00 │ Decimal(9, 2)                                      │
└──────┴────────────────────────────────────────────────────┘
```


<span id="1c302f87"></span>
### toFixedString

Convert the String type parameter into a FixedString(N) Type, with a fixed length of N. N must be a constant.

If the byte count of the string is less than N, fill the right side with empty bytes. If the byte count of the string is more than N, throw an exception.

**Syntax**

```SQL
toFixedString(s, N)
```


**Param**


* `s` string.

* `N` — a constant.


**Return value**


* Fixed String


**Example**

```SQL
SELECT toFixedString('1234', 5)
```


```Plain
┌─toFixedString('1234', 5)─┐
│ 1234                     │
└──────────────────────────┘
```


<span id="1bcc8949"></span>
### toInt(8|16|32|64)

Converts the input value to an Int data type.

**Syntax**

```SQL
toInt8(expr)
toInt16(expr)
toInt32(expr)
toInt64(expr)
```


**Param**


* `expr`— Expression returns a number or a decimal represented numeric string. Binary, octal, and hexadecimal numeric representations are not supported. Leading zeros are deleted.


**Return value**


* Integer values of data types `Int8`, `Int16`, `Int32`, and `Int64`.


The function uses [rounding towards zero](https://en.wikipedia.org/wiki/Rounding#Rounding_towards_zero), which means it truncates the decimal part of the number.

The behaviour of functions with NaN and Inf parameters is undefined.

When you convert a value from one data type to another, you should keep in mind that this is generally an unsafe action and may lead to data loss. If you attempt to convert a value from a larger data type to a smaller data type, or convert values between different data types, data loss may occur.

**Example**

```SQL
SELECT toInt64(nan), toInt32(32), toInt16('16'), toInt8(8.8);
```


```Plain
┌─toInt64(nan)─────────┬─toInt32(32)─┬─toInt16('16')─┬─toInt8(8.8)─┐
│ -9223372036854775808 │ 32          │ 16            │ 8           │
└──────────────────────┴─────────────┴───────────────┴─────────────┘
```


<span id="b0ab74a0"></span>
### toInt(8|16|32|64)OrNull

It accepts a String type parameter and attempts to parse it as an Int (8|16|32|64). If unsuccessful, returns NULL.

**Syntax**

```SQL
toInt8OrNull(expr)
toInt16OrNull(expr)
toInt32OrNull(expr)
toInt64OrNull(expr)
```


**Parameters**


* `Expression`— An expression returns a number or a decimal numeral string. Binary, octal, and hexadecimal representations are not supported. Leading zeros are deleted.


**Return value**


* Data type `Int8`, `Int16`, `Int32`, `Int64` integer values.


Functions use [rounding towards zero](https://en.wikipedia.org/wiki/Rounding#Rounding_towards_zero), which means they truncate the decimal part of the number.

Function behavior with NaN and Inf parameters is undefined.

When converting values from one data type to another, you should be aware that it is generally an unsafe operation that may result in data loss. Data loss can occur if you try to convert a value from a larger data type to a smaller one, or between different data types.

**Example**

```SQL
SELECT toInt64OrNull('123123'), toInt8OrNull('123qwe123');
```


```Plain
┌─toInt64OrNull('123123')─┬─toInt8OrNull('123qwe123')─┐
│                  123123 │                      ᴺᵁᴸᴸ │
└─────────────────────────┴───────────────────────────┘
```


<span id="ee0dec7f"></span>
### toInt(8|16|32|64)OrZero

It accepts a String Type parameter and tries to parse it into an Int (8 | 16 | 32 | 64). If it fails, it returns Zero.

**Syntax**

```SQL
toInt8OrZero(expr)
toInt16OrZero(expr)
toInt32OrZero(expr)
toInt64OrZero(expr)
```


**Param**


* `expr`— The expression returns a Number or a decimal digit string. Not supported for binary, octal, and hexadecimal Number representations. Leading zeros are deleted.


**Return Value**


* Data type `Int8`, `Int16`, `Int32`, `Int64` Integer values.


The function uses [rounding towards zero](https://en.wikipedia.org/wiki/Rounding#Rounding_towards_zero), which means it will truncate the decimal part of the number.

The behavior of functions with NaN and Inf parameters is undefined.

When you convert values from one data type to another, you should remember that this is generally an unsafe operation that could result in data loss. If you try to convert values from a larger data type to a smaller one, or between different data types, data loss may occur.

**Example**

```SQL
SELECT toInt64OrZero('123123'), toInt8OrZero('123qwe123');
```


```Plain
┌─toInt64OrZero('123123')─┬─toInt8OrZero('123qwe123')─┐
│ 123123                  │ 0                         │
└─────────────────────────┴───────────────────────────┘
```


<span id="30fe6c32"></span>
### toInterval(Year|Quarter|Month|Week|Day|Hour|Minute|Second)

Convert numeric type parameters into interval data types.

**Syntax**

```SQL
toIntervalSecond(number)
toIntervalMinute(number)
toIntervalHour(number)
toIntervalDay(number)
toIntervalWeek(number)
toIntervalMonth(number)
toIntervalQuarter(number)
toIntervalYear(number)
```


**Parameters**


* `number`— interval duration. Positive integer.


**Return value**


* `Value of the Interval` data type.


**Example**

```SQL
WITH
    toDate('2019-01-01') AS date,INTERVAL 1 WEEK AS interval_week,
    toIntervalWeek(1) AS interval_to_week
SELECT date + interval_week,date + interval_to_week;
```


```Plain
┌─plus(date, interval_week)─┬─plus(date, interval_to_week)─┐
│ 2019-01-08                │ 2019-01-08                   │
└───────────────────────────┴──────────────────────────────┘
```


<span id="ae8f8d8f"></span>
### toLowCardinality

Converts the input parameter to a LowCardinality version of the same data type.

To convert data from the `LowCardinality` data type, use the CAST function. For example, `CAST(x as String)`.

**Syntax**

```SQL
toLowCardinality(expr)
```


**Parameter**


* `Expression` — Generates one of the supported data types.


**Return value**


* As a result of `Expression`. Type: `LowCardinality(expr_result_type)`


**Example**

```SQL
SELECT toLowCardinality('1');
```


```Plain
┌─toLowCardinality('1')─┐
│ 1                     │
└───────────────────────┘
```


<span id="fd9f75c1"></span>
### toString

Function to convert between numerics, strings (but not fixed strings), dates, and dates with time.

All these functions take one parameter.

When converting to or from strings, the format or parsing rules for the value follow the same as those in the TabSeparated format (and almost every other text format). If a string cannot be parsed, an exception is raised and the request is canceled.

When the date is converted to a number or vice versa, the date corresponds to the total days since the start of the Unix epoch.

When a date with time is converted to a number or vice versa, the date with time corresponds to the seconds since the start of the Unix epoch.

The date and datetime format definitions for the toDate/toDateTime functions are as follows:

```Plain
YYYY-MM-DD
YYYY-MM-DD hh:mm:ss
```


The exception is that if converting from UInt32, Int32, UInt64, or Int64 number types to Date, and the number is equal to or bigger than 65536, then the number will be interpreted as a Unix timestamp (not total days) and rounded to the nearest date. This allows support for the common “toDate(unix_timestamp)” write operation; otherwise, an error would occur, and the more cumbersome “toDate(toDateTime(unix_timestamp))” would need to be used.

Conversions between date and datetime occur naturally: by adding empty time or by deleting time.

The conversion between numeric types uses the same rules as assignments between different numeric types in C++.

Additionally, the toString function of a DateTime parameter can take a second String parameter that contains the timezone name. Example: `Asia/Yekaterinburg` in this case, the time is formatted according to the specified timezone.

**Syntax**

```SQL
toString(value)
```


**Param**


* `Value`— Number, String, Date, and Date Time


**Return value**


* String


**Example**

```SQL
SELECT
    now() AS now_local,
    toString(now(), 'Asia/Yekaterinburg') AS now_yekat;
```


```Plain
┌─now_local───────────┬─now_yekat───────────┐
│ 2021-08-18 15:25:59 │ 2021-08-18 12:25:59 │
└─────────────────────┴─────────────────────┘
```


<span id="3ea33ba1"></span>
### toStringCutToZero

Accepts a string or FixedString param. Returns a string that is truncated at the location of the first found zero byte.

**Syntax**

```SQL
toStringCutToZero(s)
```


**Param**


* `s`— String or fixed string.


**Return value**


* Truncate string


**Example**

```SQL
SELECT toFixedString('foo', 8) AS s, toStringCutToZero(s) AS s_cut;
```


```Plain
┌─s───┬─s_cut─┐
│ foo │ foo   │
└─────┴───────┘
```


```SQL
SELECT toFixedString('foo\0bar', 8) AS s, toStringCutToZero(s) AS s_cut;
```


```Plain
┌─s──────┬─s_cut─┐
│ foobar │ foo   │
└────────┴───────┘
```


<span id="a38db259"></span>
### toUInt8

Converts the Enter a value into a UInt Data type. This function series includes:

**Syntax**

```SQL
toUInt8(expr)
toUInt16(expr)
toUInt32(expr)
toUInt64(expr)
```


**Param**


* `expr`— Expression returns a Number or a Number string in decimal. Binary, octal, and hexadecimal number representations are not supported. Leading zeros are deleted.


**Return value**


* Data types `Int8`, `Int16`, `Int32`, and `Int64` Integer values.


The function uses [rounding towards zero](https://en.wikipedia.org/wiki/Rounding#Rounding_towards_zero), which means it truncates the decimal part of numbers.

The behavior of the function for negative numbers, NaN, and Inf parameters is undefined. If you pass a string with a negative number (e.g., `'-32'`), ByteHouse will raise an exception.

When you convert a value from one data type to another, you should keep in mind that, generally, it is an unsafe operation and may lead to data loss. If you attempt to convert a value from a larger data type to a smaller one or convert values between different data types, data loss may occur.

**Example**

```SQL
SELECT toUInt64(nan), toUInt32(-32), toUInt16('16'), toUInt8(8.8);
```


```Plain
┌─toUInt64(nan)───────┬─toUInt32(-32)─┬─toUInt16('16')─┬─toUInt8(8.8)─┐
│ 9223372036854775808 │ 4294967264    │ 16             │ 8            │
└─────────────────────┴───────────────┴────────────────┴──────────────┘
```


<span id="ba92961d"></span>
### toUnixTimestamp

For DateTime parameters: Convert the value to a number of Type: UInt32 — [Unix Timestamp](https://en.wikipedia.org/wiki/Unix_time).

For string parameters: Convert the input character string to datetime according to the Timezone (optional second parameter, default is server Timezone) and return the corresponding Unix Timestamp.

**Syntax**

```SQL
toUnixTimestamp(datetime)
toUnixTimestamp(str, [timezone])
sql
```


**Parameters**


* `datetime` appointment time

* `str` datetime string

* `timezone` (optional) \- Timezone


**Return value**


* Return Unix Timestamp. Type: `UInt32`.


**Example**

```SQL
SELECT toUnixTimestamp('2017-11-05 08:07:47', 'Asia/Tokyo') AS unix_timestamp
```


```Plain
┌─unix_timestamp─┐
│ 1509836867     │
└────────────────┘
```


```SQL
SELECT toUnixTimestamp(toDateTime('2017-11-05 08:07:47', 'Asia/Tokyo')) AS unix_timestamp
```


```Plain
┌─unix_timestamp─┐
│ 1509836867     │
└────────────────┘
```
