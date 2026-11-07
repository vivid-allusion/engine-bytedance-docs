---
title: "Introduction to Commonly Used Functions"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Introduction_to_Commonly_Used_Functions"
---

<span id="_1-概述"></span>
# 1. Overview

The product supports a variety of functions, including numerical, text, time, and array functions. During use, you can perform various calculations in datasets and dashboards by adding formulas or functions. Since the product provides data import and query services based on ClickHouse, this document only introduces the commonly used syntax of relevant ClickHouse functions.

**More reference materials:** 

[ClickHouse official function documentation](https://clickhouse.com/docs)

[LOD Expression](https://docs.byteplus.com/docs/DataWind/LOD_Expression)

[2. Table calculation functions](https://docs.byteplus.com/docs/DataWind/Common_Functions_Usage#_2-%E8%A1%A8%E8%AE%A1%E7%AE%97%E5%87%BD%E6%95%B0)

<span id="_2-聚合函数"></span>
# 2. Aggregate functions

<span id="_2-1-常用函数快速入门"></span>
## 2.1 Quick start with commonly used functions

Aggregate functions are used to quickly aggregate metrics according to the desired logic, such as sum, count, and more.

<span id="_2-1-1-计数"></span>
### 2.1.1 Count

Format: count(xxx), which counts xxx

Example:


|Field A |
|---|
|1 |
|1 |
|3 |
|4 |


Calculating count(Field A) yields an aggregate result of 4. To perform a distinct count, use count(distinct Field A), which yields a result of 3.

<span id="_2-1-2-求和"></span>
### 2.1.2 Sum

Format: sum(xxx), which sums xxx

Example:


|Field A |
|---|
|1 |
|1 |
|3 |
|4 |


Calculating sum(Field A) yields an aggregate result of 9.

**Further explanation:**  The difference between SUM(Field A/Field B) and SUM(Field A)/SUM(Field B) is illustrated with two examples


* **Example 1**: If there is a table with detailed data as shown below, when grouping by "Dimension", and SUM(Field A/Field B) and SUM(Field A)/SUM(Field B) are aggregated respectively

   
   |Dimension |Field A |Field B |Field A/Field B |
   |---|---|---|---|
   |Dimension item 1 |1 |2 |0.5 |
   |Dimension item 1 |1 |2 |0.5 |
   |Dimension item 1 |2 |2 |1 |
   |Dimension item 1 |1 |4 |0.25 |
   |Dimension item 2 |3 |3 |1 |
   |Dimension item 2 |2 |4 |0.5 |
   |Dimension item 2 |1 |5 |0.2 |
   

   **Aggregation results:** 

   SUM(Field A/Field B) calculates the sum of A/B values in the raw data, that is, division first and then addition; while SUM(Field A)/SUM(Field B) calculates the quotient of the total values of Field A and Field B, that is, addition first and then division. The results may differ significantly.

   
   |Dimension |SUM(Field A) |SUM(Field B) |SUM(Field A/Field B) |SUM(Field A)/SUM(Field B) |
   |---|---|---|---|---|
   |Dimension item 1 |5 |10 |2.25 |0.5 |
   |Dimension item 2 |6 |12 |1.7 |0.5 |
   

* **Example 2:**  Application combined with the product's [Total](https://docs.byteplus.com/docs/DataWind/Total)functionality

   If the expression is changed to **SUM(Field A)/SUM(Field B)**  and **Auto** is used in the analysis\-totaling feature, the calculation result is **SUM(Field A)/SUM(Field B)** , that is, sum A and B separately, then perform the division. This is generally used to calculate overall conversion rates and more.

   
   |Dimension |Field A |Field B |Field A/Field B |
   |---|---|---|---|
   |Total |3 |10 |0.3 |
   |Dimension item 1 |1 |5 |0.2 |
   |Dimension item 2 |2 |5 |0.4 |
   


<span id="_2-1-3求平均"></span>
### 2.1.3 Average

Format: average(xxx), which calculates the mean of xxx

Example:


|Field A |
|---|
|1 |
|1 |
|3 |
|4 |


Calculating average(Field A) yields an aggregate result of 2.25.

<span id="_2-1-4-求最大-最小值"></span>
### 2.1.4 Maximum/minimum values

Format: maximum value max(xxx), minimum value min(xxx)

Example:


|Field A |
|---|
|1 |
|1 |
|3 |
|4 |


Calculating max(Field A) yields 4; calculating min(Field A) yields 1.

<span id="_2-1-5-分位数"></span>
### 2.1.5 Quantiles

Format: quantile(level)(xxx) or quantileExact(level)(xxx), which returns the level quantile of xxx. The latter returns the exact value, while the former has some error but better performance.

Example:


|Field A |
|---|
|1 |
|1 |
|3 |
|4 |


Calculating quantile(0.75)(Field A) yields the 75th percentile of Field A, which is 3.

<span id="_2-2-功能详解"></span>
## 2.2 Functionality details


|Function name |Function format |Purpose |Example |
|---|---|---|---|
|avg |avg(x) |Returns the average value of all values in the expression. Can only be used for numeric fields |avg( profit ) returns the average profit |
|max |max(x) |Returns the maximum value of all values in the expression. Can only be used for numeric fields |max( profit ) returns the maximum profit |
|min |min(x) |Returns the minimum value of all values in the expression. Can only be used for numeric fields |min( profit ) returns the minimum profit |
|count |count(x) |Counts the number of rows |count( p_date ) returns the total number of days |
|sum |sum(x) |Returns the sum of all values in the expression. Can only be used for numeric fields |sum( profit ) returns the total profit |
|uniqCombined |uniqCombined(HLL_precision)(x[, ...]) |Calculates the approximate number of distinct values of the parameters. For large sets (200 million or more elements), due to poor hash function selection, the estimation error will be greater than the theoretical value. | |
|quantile |quantile(level)(x) |Returns the quantile of all values in the expression. Can only be used for numeric fields. level range 0\-1 |quantile(0.5)(x) returns the 0.5 quantile of x |
|uniq |uniq(x) |Count distinct. Has the same effect as count(distinct), with an accuracy error of 0.5%. For exact values, use count(distinct), but the query takes longer and may not return results due to timeout. Not recommended. | |
|argMax |argMax(arg,val) |Calculates the maximum value based on the field val. Then takes the value of the Arg field in the record row where the maximum value is located | |
|groupArray |groupArray(n)(fieldname) |Returns the first n records. Returns an array. | |
|any |any(x) |Returns the first value encountered. | |
|quantileExact |quantileExact(level)(x) |Returns the quantile of all values in the expression. Can only be used for numeric fields. level range 0\-1. Same effect as quantile, but is an exact query. When using quantileExact, the query takes longer and may not return results due to timeout. Not recommended. |quantileExact(0.5)(x) returns the 0.5 quantile of x |


<span id="_3-日期函数"></span>
# 3. Date functions

<span id="_3-1-常用函数快速入门"></span>
## 3.1 Quick start with common functions

Date functions are used for time format conversion, time processing, obtaining specified dates, and more.

<span id="_3-1-1-将文本转换为时间或日期"></span>
### 3.1.1 Convert text to time or date

Format:


* toDate(xxx) and to_date(xxx) convert string fields in yyyymmdd or yyyy\-mm\-dd format to date format.

* toDateTime(xxx) converts strings in yyyy\-mm\-dd hh:mm:ss format to datetime format.

* toDateOrNull(xxx) and toDateTimeOrNull(xxx) have the same functionality as the above two, and are suitable for cases where the field contains dirty data, converting dirty data to null values.


Example:


|Field A |toDate(Field A) |toDateTime(Field A) |
|---|---|---|
|2020/12/21 |2020/12/21 |2020/12/21 0:00 |
|20201221 |2020/12/21 |2020/12/21 0:00 |
|2020/12/21 18:00 |2020/12/21 |2020/12/21 18:00 |


Field A is of string type; toDate(Field A) and toDateTime(Field A) convert it to date or datetime format.

<span id="_3-1-2-时间与时间戳相互转换"></span>
### 3.1.2 Convert between time and timestamp

Format: Use toUnixTimestamp(xxx) to convert time or text\-type time to a timestamp, that is, convert yyyy\-mm\-dd hh:mm:ss to a timestamp.

Example:


|Field A |toUnixTimestamp(Field A) |Extension: toDateTime(toUnixTimestamp(Field A)+28800) |
|---|---|---|
|2020/12/21 18:00 |1608544800 |2020/12/22 2:00 |


Extension: For the converted timestamp, add the time difference of 8 hours (28800) to complete the conversion from UTC+0 to UTC+8, and then use the toDateTime function to convert it to a more readable datetime format.

<span id="_3-1-3-返回当前日期"></span>
### 3.1.3 Return the current date

Format: now(), generates a dynamic parameter that changes with the system's real\-time clock.

Example: If the current time is 2020\-12\-21 18:00:00, entering now() as a field will result in the field's current value being 2020\-12\-21 18:00:00, and one hour later it will be 2020\-12\-21 19:00:00.

<span id="_3-1-4-返回本周周一的日期"></span>
### 3.1.4 Return the date of this week's Monday

Format: toMonday(xx), retrieves the date corresponding to this week's Monday for the given date field.

Example:


|Field A |toMonday(Field A) |
|---|---|
|2020/12/22 |2020/12/21 |


<span id="_3-2-功能详解"></span>
## 3.2 Functionality details


|Function name |Function format |Purpose |Example |
|---|---|---|---|
|toDateTime |toDateTime(x) |Converts a string\-formatted date and time to a date\-time type. |toDateTime('2018\-12\-24 10:10:00') |
|toStartOfFiveMinute |toStartOfFiveMinute（x） |Rounds the date and time down to the nearest multiple of 5 minutes (then sets the seconds to zero), and returns the date. |toStartOfFiveMinute(toDateTime('2018\-12\-11 11:12:13')) returns 2018\-12\-11 11:10:00 |
|now |now（) |Generate the current date and time |now() returns 2018\-12\-13 10:10:12 |
|toStartOfFifteenMinutes |toStartOfFifteenMinutes（x) |Rounds the date and time down to the nearest multiple of 15 minutes (then sets the seconds to zero), and returns the date. |toStartOfFifteenMinute(toDateTime('2018\-12\-11 11:12:13')) returns 2018\-12\-11 11:00:00 |
|toStartOfInterval |toStartOfInterval(time_or_data, INTERVAL x unit [, time_zone]) |This is the general function for all functions named toStartOf\*. For example, toStartOfInterval(t, INTERVAL 1 year) returns the same result as toStartOfYear(t), toStartOfInterval(t, INTERVAL 1 month) returns the same result as toStartOfMonth(t), toStartOfInterval(t, INTERVAL 1 day) returns the same result as toStartOfDay(t), and toStartOfInterval(t, INTERVAL 15 minute) returns the same result as toStartOfFifteenMinutes(t). |toStartOfInterval(toDateTime('2019\-10\-10 09:09:20'), INTERVAL 1 year) returns 2019\-01\-01 |
|toIntervalDay |toIntervalDay(x) |Convert date to timestamp at the day level. |toIntervalDay(toDateTime('2019\-08\-12 11:12:13')) returns 1565579533 |
|toIntervalMinute |toIntervalMinute(x) |Convert date to timestamp at the minute level. |toIntervalMinute(toDateTime('2019\-08\-14 11:12:13')) returns 1565579533 |
|toIntervalHour |toIntervalHour(x) |Convert date to timestamp at the hour level. |toIntervalHour(toDateTime('2019\-08\-14 11:12:13')) returns 1565579533 |
|toMonday |toMonday(x) |Round Date or DateTime down to Monday of the current week. Returns Date type. |toMonday(toDateTime('2019\-08\-14 11:12:13')) returns 2019\-08\-12 |
|toStartOfHour |toStartOfHour(x) |Round DateTime down to the start of the current hour. |toStartOfHour(toDateTime('2018\-12\-11 11:12:13')) returns 11 |
|today |today( ) |Generate today's date. |today() returns 2018\-12\-13 |
|toHour |toHour(x) |Extract the hour from a date and time. |toHour(toDateTime('2018\-12\-11 11:12:13')) returns 11 |
|toStartOfTenMinutes |toStartOfTenMinutes(x) |Round DateTime down to the nearest ten\-minute mark. |toStartOfTenMinutes(toDateTime('2018\-12\-11 11:12:13')) returns 2018\-12\-11 11:00:00 |
|toStartOfDay |toStartOfMinute(string date time) |Round DateTime down to the start of the day. | |
|toYear |toYear(string date) |Returns the year from the date. | |
|toRelativeWeekNum |toRelativeWeekNum(date) |Convert Date or DateTime to the week number, starting from a fixed point in the past. | |
|toMonth |toMonth(string date) |Returns the month from the date. | |
|toStartOfMinute |toStartOfMinute( ) |Truncate date and time to the minute (set seconds to zero), returns date. |toStartOfMinute(toDateTime('2018\-12\-11 11:12:13')) returns 2018\-12\-11 11:12:00 |
|toUnixTimestamp |toUnixTimestamp( ) |Convert DateTime to unix timestamp. | |
|addDays |addDays(date_time,int) |The function adds a time interval to Date/DateTime, then returns Date/DateTime. | |
|toRelativeYearNum |toRelativeYearNum(date_time) |Convert Date or DateTime to the year number, starting from a fixed point in the past. | |
|year |year(Date/DateTime/String date) |Returns the year from the date. |year(toDateTime('2018\-12\-11 11:12:13')) returns 2018 |
|month |month(Date/DateTime/String date) |Returns the month from the date. |month(toDateTime('2018\-12\-11 11:12:13')) returns 12 |
|quarter |quarter(Date/DateTime/String date) |Returns the quarter from the date. |quarter(toDateTime('2018\-12\-11 11:12:13')) returns 12 |
|day |day(Date/DateTime/String) |Returns the day of the month. |day('2019\-09\-12') returns 12 |
|last_day |last_day(Date/DateTime/String date) |Returns the last day of the month for the given date. |last_day(toDateTime('2018\-12\-11 11:12:13')) returns 2018\-12\-31 |
|next_day |next_day(Date/DateTime/String date, string day_of_week) |Returns the next day_of_week for the given date. |next_day(toDate('2015\-01\-14'), 'TU') returns 2015\-01\-20 |
|dateDiff |dateDiff(Date/DateTime date1, Date/DateTime date2 [, String timezone])； dateDiff(String unit, Date/DateTime date1, Date/DateTime date2 [, String timezone]) |Returns the difference between two dates. |dateDiff(now(), yesterday()) returns \-1 |
|date_sub |date_sub (string/Date/DateTime startdate, int days) |Returns the date/time days before start_time. |date_sub('2019\-09\-08', 1) returns '2019\-09\-07' |
|date_add |date_add (string/Date/DateTime startdate, int days) |Returns the date/time days after start_time. |date_add('2019\-09\-08', 1) returns '2019\-09\-09' |
|from_unixtime |from_unixtime(Date/DateTime/UInt32 date, String parttern[, String timezone]) |Convert date or timestamp to a string in the specified pattern. |from_unixtime(toDateTime('2019\-09\-09 09:00:00'), 'time: %F %T', 'Asia/Shanghai') returns 'time: 2019\-09\-09 09:00:00' |
|to_date,toDate |to_date(String/UInt16 date) |Convert a string or the number of days since 1970\-01\-01 to a date type. |toDate('20190909') returns '2019\-09\-09' |
|date_format |date_format(Date/DateTime/String, String pattern) |Output the date in the specified format. |date_format('2019\-09\-09', 'yyyy') returns '2019' |
|unix_timestamp |unix_timestamp(Date/DateTime/String) |Convert date to timestamp. |unix_timestamp(toDateTime('2019\-09\-09 09:00:00'), 'time: %F %T', 'Asia/Shanghai') returns 'time: 2019\-09\-09 09:00:00' |
|toWeek |toWeek(date[,mode]) |Returns the week number for the date, range [0, 53]. |toWeek(toDate('2019\-12\-06'), 3) returns 49 |
|toDayOfWeek |todayofweek(date) |Returns the day of the week for the date, range [1, 7]. |toDayOfWeek('2020\-01\-01') returns 3 |


<span id="_4-类型转换函数"></span>
# 4. Type conversion functions

<span id="_4-1-常用函数快速入门"></span>
## 4.1 Quick start with common functions

Type conversion functions are used to convert the type of a field, such as converting between text and numbers.

<span id="_4-1-1-强制转换任意类型"></span>
### 4.1.1 Force conversion to any type

Format: cast(xxx, 'type'), converts xxx to a specified type.

Example:

cast(Field A, 'string') converts Field A to string format.

<span id="_4-1-2-转换成字符串-文本"></span>
### 4.1.2 Convert to string (text)

Format: toString(xxx), converts field xxx to string format; can convert fields of types such as numbers, characters, dates, and more.

Example:


|Field A |toString(Field A) |
|---|---|
|143876768892010 |143876768892010 |


Before conversion, Field A is in numeric format and may be displayed in scientific notation due to its length during analysis; after conversion to string, it can be stored stably.

<span id="_4-1-3-转换成整数值"></span>
### 4.1.3 Convert to integer value

Format: toInt64(xxx), converts field xxx to an integer; xxx can only contain numbers.


|Field A |toInt64(Field A) |
|---|---|
|143876768892010 |143876768892010 |
|123a |Conversion failed |


<span id="_4-2-功能详解"></span>
## 4.2 Functionality details


|Function name |Function format |Purpose |Example |
|---|---|---|---|
|cast |cast(X, 'Y') |General type conversion function, converts data of any type X to format Y. |Convert uid of int type to String type CAST (uid, 'String') |
|toString |toString(x) |Convert numeric, character, date, and other types to character type |toString('2018\-12\-24') returns 2018\-12\-24 |
|toInt64 |toInt64(x) |Convert data type to int64 format (64\-bit integer) |toInt64(123.883) returns 123 |
|toUInt8OrZero |toUInt8OrZero(x) |Convert an unsigned integer string to an integer type; otherwise, returns 0 |toUInt8OrZero('123.12') returns 0 |
|toDateOrZero |toDateOrZero(x) |Convert data type to DATE format; otherwise, returns 0 |toDateOrZero(toDateTime('2018\-12\-11 11:12:13')) returns 2018\-12\-11 |
|toUInt16OrZero |toUInt16OrZero(x) |Convert an unsigned integer string to an integer type; otherwise, returns 0 |toUInt8OrZero('123') returns 123 |
|toUInt64OrZero |toUInt64OrZero(x) |Convert data type to int64 format (64\-bit integer); returns 0 if conversion fails |toUInt64OrZero('123') returns 123 |
|toDateOrNull |toDateOrNull(a) |Convert the data type of a to date or null | |
|toUInt32OrZero |toUInt32OrZero(x) |Convert data type to int32 format (32\-bit integer); returns 0 if conversion fails | |
|toFloat32OrZero |toFloat32OrZero( ) |Convert a numeric string to a numeric type |toFloat32OrZero('−123') returns −123 |
|toIntervalMonth |toIntervalMonth( ) |Convert a numeric parameter to the Interval type (time interval) | |
|toInt32 |toInt32(a) |Convert the data type of a to int32 | |
|toDateTimeOrNull |toDateTimeOrNull(a) |Convert the data type of a to datetime or null | |
|toFloat64 |toFloat64(a) |Convert the data type of a to float64 | |
|toUInt8 |toUInt8(a) |Convert the data type of a to UInt8 | |
|toFloat64OrZero |toFloat64OrZero(a) |Convert the data type of a to float64 or zero | |
|toUInt32 |toUInt32(a) |Convert the data type of a to UInt32 | |
|parseDateTimeBestEffort |parseDateTimeBestEffort() |Parse numeric parameter as Date or DateTime type. Unlike toDate and toDateTime, parseDateTimeBestEffort can handle more complex date formats. | |
|parseDateTimeBestEffortOrNull |parseDateTimeBestEffortOrNull() |Parse numeric parameter as Date or DateTime type; returns null if the date format cannot be processed | |
|parseDateTimeBestEffortOrZero |parseDateTimeBestEffortOrZero() |Parse numeric parameter as Date or DateTime type; returns zero Date or zero DateTime if the date format cannot be processed | |


<span id="_5-字符串函数"></span>
# 5. String functions

<span id="_5-1-常用函数快速入门"></span>
## 5.1 Quick start with common functions

String functions are used to concatenate or extract text.

<span id="_5-1-1-字符串拼接"></span>
### 5.1.1 String concatenation

Format: concat(xxx, xxx, xxx, ...), concatenates multiple fields together without separators

Example: concat(Field A, Field B, Field C) results in: 门前大桥下，123


|Field A |Field B |Field C |
|---|---|---|
|Under the bridge in front of the gate |， |123 |


<span id="_5-1-2-字符串截取"></span>
### 5.1.2 Substring

Format: substr(xxx, offset x, length y) or substring(xxx, offset x, length y), which means extracting a substring of length y from the string field xxx starting at position x.

Example:


|Field A |substr(Field A,1,10) |
|---|---|
|2020/12/22 18:00 |2020/12/22 |


substr(Field A, 1, 10) extracts 10 characters from Field A starting from the first character, resulting in the output as above.

**Extension:**  Combination of concat and substr


|Field A |Field B |
|---|---|
|Xiaoming |8,9,8 |
|concat(Field A, 'the score of the second item is', substr(Field B,3,1)) yields the result: Xiaoming's score for the second item is 9 | |


<span id="_5-1-3-返回字符串长度"></span>
#### 5.1.3 Returning the string length

Format: length(xxx), calculates the length of the string field xxx

Example:


|Field A |length(Field A) |
|---|---|
|2020/12/22 18:00:00 |19 |


<span id="_5-2-功能详解"></span>
## 5.2 Detailed function explanation


|Function name |Function format |Purpose |Example |
|---|---|---|---|
|substring |substring(s, offset, length) |Substring extraction |substring('123abcABC', 2, 3) returns 23a |
|empty |empty(x) |Returns 1 if the string is empty; otherwise, returns 0 |empty('123a') returns 0 |
|length |length(x) |Returns the length of the string |length('123a') returns 4 |
|extractAll |extractAll(haystack,pattern) |Returns all matched substrings as a list |extractAll('iioomAj12123124OOBJ123B', '\d+') returns [12123124,123] |
|splitByChar |splitByChar(separator, s) |Split string by a single character | |
|concat |concat(s1, s2, ...) |Concatenate multiple strings in the parameters without a separator |concat('123', 'abc', 'ABC') returns 123abcABC |
|lower |lower(string) |Convert string to lowercase | |
|char_length |char_length(string) |Assuming the string is composed of UTF\-8 encoded text, returns the Unicode character length of the string. If the input string is not UTF\-8 encoded, the function may return an unexpected value (no exception will be thrown). | |
|startsWith |startsWith(s, prefix) |Returns whether the string starts with the specified prefix. If the string starts with the specified prefix, returns 1; otherwise, returns 0. | |
|replaceRegexpAll |replaceRegexpAll(haystack,pattern,replacement) |Replaces all substrings matching the pattern using regular expression matching. |replaceOne('asd123cbbj464sd', 'sd', '\-') returns a\-123cbbj464\- |
|replaceRegexpOne |replaceRegexpOne(haystack, pattern, replacement) |Replaces using the 'pattern' regular expression. | |
|replaceAll |replaceAll(haystack, pattern, replacement) |Replaces all occurrences of 'pattern' in 'haystack' with the 'replacement' substring. | |
|split |split(string str, string pat) |Splits str by the pat string and returns an array of the resulting substrings. |split('abc', 'b') returns ['a', 'c'] |
|concat_ws |concat_ws(String delimiter, String str1, String str2, ...) |Returns a string joined by the 'delimiter'. |concat_ws('_', 'abc', 'def') returns 'abc_def' |
|substring |substring(String str, int start, int len)，substr(String str, int start, int len) |Returns the substring of length len starting from position start. |substring('abc', 2); returns 'bc' |
|lpad,rpad |lpad(String, len, pad_str) |Pads str on the left with pad to a total length of len. |lpad('abcd', 10, '.') returns '......abcd' |
|regexp_replace |regexp_replace(String str, String str1, String str2) |Returns the result of replacing str1 in str with str2; supports re2 regular expressions. |regexp_replace('world.', '^', 'hello ') returns 'hello world.' |


<span id="_6-条件函数"></span>
# 6. Conditional functions

<span id="_6-1-常用函数快速入门"></span>
## 6.1 Quick start with common functions

Returns the corresponding value based on the specified condition. For example, if a \> 1, returns 1; if a < 1, returns 0. This needs to be implemented using conditional functions.

<span id="_6-1-1-if-函数"></span>
### 6.1.1 if function

Format: if(condition, a, b), returns value a if the condition is true, returns value b if the condition is false

Example:


|Field A |if(Field A \> 0, 'positive', 'negative') |
|---|---|
|200 |positive |


<span id="_6-1-2-case-when-函数"></span>
### 6.1.2 case when function

Format:

case

when condition 1 then result 1

when condition 2 then result 2

……

else result n

end

This function is relatively long, but the structure is simple. Conditions are checked from top to bottom. When condition 1 is met, result 1 is returned and no further conditions are checked. If none of the conditions are met, result n is returned.

Example:


|Field A |case when Field A \> 300 then '\>300' when Field A \> 200 then '(200,300]' else null end |
|---|---|
|250 |(200,300] |
|105 | |
|350 |> 300 |


<span id="_6-2-功能详解"></span>
## 6.2 Detailed function explanation


|Function name |Function format |Purpose |Example |
|---|---|---|---|
|multiIf |multiIf(cond_1, then_1, cond_2, then_2...else) |Allows you to write CASE operators more concisely in queries. Parameters: \*cond_N — the condition for the function to return then_N. \*then_N — the result of the function when executed. \*else — the result of the function if none of the conditions are met. |multiIf(1 \> 2, 'correct', 2 < 0, 'correct', 'incorrect') returns incorrect |
|if |if(cond, then, else), cond ? operator then : else |If cond != 0, returns then; if cond = 0, returns else. cond must be of type UInt8, and then and else must have the lowest common type. if(1 \> 2, 'correct', 'incorrect') returns incorrect |case |
|case |CASE WHEN a THEN b [WHEN c THEN d]\* [ELSE e] END |Function name | |


<span id="_7-用户名函数"></span>
# 7. Username functions

The username function is not an official ClickHouse function, but is combined with project user information to return specified information of the current user.

USERNAME() can return the username of the current user, as shown below. This function can also be used in combination with other functions.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2e9016bb5b18470b4d9e9f7da7570c52.png) </span>

<span id="_8-json-函数"></span>
# 8. JSON functions


|Function format |Purpose |Example |visitParamExtractInt |
|---|---|---|---|
|visitParamExtractInt |visitParamExtractUInt(params, name) |If this is a string field, the function will attempt to parse a number from the beginning of the string. If the field does not exist, or a number cannot be parsed from it, returns 0. visitParamExtractFloat | |
|visitParamExtractFloat |visitParamExtractFloat(params, name) |visitParamExtractBool | |
|visitParamExtractBool |visitParamExtractBool(params, name) |The result is UInt8. visitParamHas | |
|visitParamHas |visitParamHas(params, name) |visitParamExtractRaw | |
|visitParamExtractRaw |visitParamExtractRaw(params, name) |visitParamExtractRaw('{"abc":{"def":[1,2,3]}}', 'abc') = '{"def":[1,2,3]}' |visitParamExtractRaw('{"abc":{"def":[1,2,3]}}', 'abc') = '{"def":[1,2,3]}' |
|get_json_object |get_json_object(string json_string, string path) |Returns the element specified by path in the JSON. |get_json_object('{"n_s" : [{"ac":"abc","xz":"xz"}, {"def":"def"}], "n_i" : [1, 23]}', '$.n_s[0].ac'); returns 'abc' |


<span id="_9-数学函数"></span>
# 9. Mathematical functions


|Function name |Function format |Purpose |Example |
|---|---|---|---|
|power |power(x, y) |Takes two parameters, x and y. Returns x raised to the power of y. | |
|pow |pow(x, y) |Takes two parameters, x and y. Returns x raised to the power of y. |pow(2, 3) returns 8 |
|sqrt |sqrt(x) |Takes a numeric parameter and returns its square root. |sqrt(4) returns 2 |


<span id="_10-nullable-处理函数"></span>
# 10. Nullable processing functions


| | | | |
|---|---|---|---|
|Function name |Function format |Purpose |Example |
|isNotNull |isNotNull(x) |Checks whether the parameter is not NULL. Returns 1 if true, 0 if false |sNotNull('abc') returns 1 |
|isNull |isNull(x) |Checks whether the parameter is NULL. Returns 1 if NULL, otherwise returns 0. |isNull(null) returns 1 |
|coalesce |coalesce(x,...) |Checks from left to right for a "NULL" parameter and returns the first non\-NULL parameter. |coalesce(null, null, a, b, null) returns a |
|assumeNotNull |assumeNotNull( ) |Converts a value of Nullable type to a value of non\-Nullable type | |


<span id="_11-进制转换函数"></span>
# 11. Base conversion functions


|Function name |Function format |Purpose |Example |
|---|---|---|---|
|conv |conv(String/Int num, Int from_base, Int to_base) |Base conversion |conv('10', 10, 2) returns '1010' |
|bin |bin(Int/DateTime/String) |Converts to a binary number |bin(10) returns '1010' |


<span id="_12-hash-函数"></span>
# 12. Hash functions


|Function name |Function format |Purpose |
|---|---|---|
|cityHash64 |cityHash64O() |Calculates the CityHash64 of any number of strings, or uses a specific implementation of a hash function to calculate the hash of any number of other types. |
|intHash64 |intHash64( ) |Calculates a 64\-bit hash code from any type of integer |


<span id="_13-url-函数"></span>
# 13. URL functions


|Function name |Function format |Purpose |Example |
|---|---|---|---|
|domain |domain(x) |Returns the domain name of a URL |domain('[http://www.baidu.com.cn](http://www.baidu.com.cn)') returns [www.baidu.com.cn](http://www.baidu.com.cn) |
|cutToFirstSignificantSubdomain |cutToFirstSignificantSubdomain( ) |Returns the content between the top\-level domain and the first significant subdomain |cutToFirstSignificantSubdomain('[https://news.yandex.com.tr/')](https://news.yandex.com.tr/')) = '[yandex.com](http://yandex.com).tr' |
|parse_url |parse_url(String url, String name) |Returns the part of the url corresponding to name. If parsing fails, returns an empty string. |parse_url('[https://bytedance.feishu.cn/space/xx#PN78WD',](https://bytedance.feishu.cn/space/xx#PN78WD',) 'PROTOCOL') returns https |


<span id="_14-map-函数"></span>
# 14. Map functions


|Function name |Function format |Purpose |Example |
|---|---|---|---|
|map key |[map field name] |Extracts a field value from a map type field |select deductions{'Federal Taxes'} from employees limit 1; |
|map |map(KeyType k1, ValueType v1, KeyType k2, ValueType v2 ...) |Constructs map type data |map('a', 'b', 'c', 'd') returns |
|str_to_map |map(String value, String kv_delimiter, String item_delimiter) |Converts a String to map type |str_to_map('a:b,c:d', ',', ':') returns |


<span id="十四、数组函数"></span>
# 15. Array functions


|Function name |Function format |Purpose |Example |
|---|---|---|---|
|arrayConcat |arrayConcat(array) |Merges all arrays passed as parameters. |SELECT arrayConcat([1, 2], [3, 4], [5, 6]) AS res ┌─res─────┐ │ [1,2,3,4,5,6] │ └───────┘ |
|notEmpty |notEmpty() |Returns 0 for an empty string, and 1 for a non\-empty string | |


<span id="十五、arrayjoin函数"></span>
# 16. ArrayJoin function


|Function name |Function format |Purpose |Example |
|---|---|---|---|
|arrayJoin |arrayJoin(array) |This function takes an array as a parameter and duplicates the row in the result set as many times as there are elements in the array. Except for the values in the column where this function is applied, all other column values are simply duplicated; they are replaced by the corresponding array values. |SELECT arrayJoin([1, 2, 3] AS src) AS dst, 'Hello', src ┌dst\-┬'Hello'\-┬─src──┐ │ 1 │ Hello │ [1,2,3] │ │ 2 │ Hello │ [1,2,3] │ │ 3 │ Hello │ [1,2,3] │ └ ─ ┴ ─ ─ ┴─ ───┘ |


<span id="十六、取模函数"></span>
# 17. Modulo functions


|Function name |Function format |Purpose |Example |
|---|---|---|---|
|pmod |pmod(Int a, Int b) |Floating\-point numbers are converted to integers for modulo operation. If there are special requirements, support can be added later. |pmod(10, 3) returns 1 |


<span id="十七、取整函数"></span>
# 18. Rounding functions


|Function name |Function format |Purpose |Example |
|---|---|---|---|
|round |round(x,[N]) |Rounds the value to the specified number of decimal places. This function returns the nearest number in order. If the given number has multiple nearest numbers, the function returns the one closest to an even number (banker's rounding). |round(123.883, 1) returns 123.9 |


<span id="十八、算术函数"></span>
# 19. Arithmetic functions


|Function name |Function format |Purpose |
|---|---|---|
|abs |abs(a) |Calculates the absolute value of the number (a) |


<span id="十九、位操作函数"></span>
# 20. Bitwise operation functions


|Function name |Function format |Purpose |
|---|---|---|
|bitAnd |bitAnd(a, b) |The result type is an integer, and its bit width is equal to the maximum bit width of its parameters. If at least one parameter is a signed integer, the result is a signed integer. If a parameter is a floating\-point number, it is forcibly converted to Int64. |


<span id="二十、随机函数"></span>
# 21. Random functions


|Function name |Function format |Purpose |
|---|---|---|
|rand |rand( ) |Returns a random number of type UInt32, and all numbers of type UInt32 have an equal probability of being generated. |


<span id="二十一、其他函数"></span>
# 22. Other functions


|Function name |Function format |Purpose |Example |
|---|---|---|---|
|hostName |hostName() |Returns a string containing the name of the host on which this function is executed. | |
|size |size(Array/Map/String) |Returns the number of elements inside |size(map('a', 'b', 'c', 'd')) returns 2 |
