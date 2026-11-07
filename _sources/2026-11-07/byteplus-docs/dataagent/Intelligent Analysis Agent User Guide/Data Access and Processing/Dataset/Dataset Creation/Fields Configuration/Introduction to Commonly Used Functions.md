---
title: "Introduction to Commonly Used Functions"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Introduction_to_Commonly_Used_Functions"
---

<span id="13ed1e70"></span>
# 1. Overview

The product supports a variety of functions, including numeric, text, time, and array functions. During use, you can perform diverse calculations in datasets by adding formulas or functions. Since the product provides data import and query services based on ClickHouse, this document only introduces the commonly used syntax for relevant ClickHouse functions.

**More reference materials:** 

[ClickHouse official function documentation](https://ClickHouse.tech/docs/zh/sql-reference/functions/)

<span id="8ffdd6f4"></span>
# 2. Aggregate functions

<span id="e2c640a9"></span>
## 2.1 Quick start with commonly used functions

Aggregate functions are used to quickly perform metric aggregation calculations according to the desired logic, such as sum and count.

<span id="c2ce7336"></span>
### 2.1.1 Count

Format: count(xxx), which counts xxx

Example:


|Field A |
|---|
|1 |
|1 |
|3 |
|4 |


Calculate count(Field A) to obtain the aggregate result 4. To perform distinct counting, use count(distinct Field A) to obtain the result 3.

<span id="6519a9df"></span>
### 2.1.2 Sum

Format: sum(xxx), which sums xxx

Example:


|Field A |
|---|
|1 |
|1 |
|3 |
|4 |


Calculate sum(Field A) to obtain the aggregate result 9.

**Further explanation:**  The difference between SUM(Field A/Field B) and SUM(Field A)/SUM(Field B) is illustrated with two cases.


* **Case 1**: If there is a table of detailed data as shown below, when "Dimension" is used as the dimension and aggregation is performed on SUM(Field A/Field B) and SUM(Field A)/SUM(Field B) respectively

   
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

   SUM(Field A/Field B) calculates the sum of A/B values in the raw data, that is, division first then addition; whereas SUM(Field A)/SUM(Field B) calculates the quotient of the total values of Field A and Field B, that is, addition first then division. The results may differ significantly.

   
   |Dimension |SUM(Field A) |SUM(Field B) |SUM(Field A/Field B) |SUM(Field A)/SUM(Field B) |
   |---|---|---|---|---|
   |Dimension item 1 |5 |10 |2.25 |0.5 |
   |Dimension item 2 |6 |12 |1.7 |0.5 |
   

* **Case 2:**  Combined application with the product's total feature

   If the expression is changed to **SUM(Field A)/SUM(Field B)**  and **Auto** is used in the analysis and total feature, the calculation result is **SUM(Field A)/SUM(Field B)** , which means summing A and B separately and then performing division. This is generally used for calculating overall conversion rates and similar metrics.

   
   |Dimension |Field A |Field B |Field A/Field B |
   |---|---|---|---|
   |Total |3 |10 |0.3 |
   |Dimension 1 |1 |5 |0.2 |
   |Dimension 2 |2 |5 |0.4 |
   


<span id="9fa7ce7e"></span>
### 2.1.3 Average

Format: average(xxx), which calculates the mean of xxx

Example:


|Field A |
|---|
|1 |
|1 |
|3 |
|4 |


Calculate average(Field A) to obtain the aggregate result 2.25.

<span id="14f0c92a"></span>
### 2.1.4 Maximum/minimum values

Format: maximum value max(xxx), minimum value min(xxx)

Example:


|Field A |
|---|
|1 |
|1 |
|3 |
|4 |


Calculate max(Field A) to obtain 4; calculate min(Field A) to obtain 1.

<span id="85fc3b7c"></span>
### 2.1.5 Quantiles

Format: quantile(level)(xxx) or quantileExact(level)(xxx), which returns the level quantile of xxx. The latter provides an exact value, while the former has some error but offers better performance.

Example:


|Field A |
|---|
|1 |
|1 |
|3 |
|4 |


Calculate quantile(0.75)(Field A) to obtain the 75% quantile of Field A, which is 3.

<span id="c9b680ef"></span>
## 2.2 Detailed function description


|Function name |Function format |Purpose |Example |
|---|---|---|---|
|avg |avg(x) |Returns the average value of all values in the expression. Can only be used for numeric fields. |avg( profit ) returns the average profit. |
|max |max(x) |Returns the maximum value of all values in the expression. Can only be used for numeric fields. |max( profit ) returns the maximum profit. |
|min |min(x) |Returns the minimum value of all values in the expression. Can only be used for numeric fields. |min( profit ) returns the minimum profit. |
|count |count(x) |Counts the number of rows. |count( p_date ) returns the total number of days. |
|sum |sum(x) |Returns the sum of all values in the expression. Can only be used for numeric fields. |sum( profit ) returns the total profit. |
|uniqCombined |uniqCombined(HLL_precision)(x[, ...]) |Calculates the approximate number of distinct parameter values. For large sets (200 million or more elements), due to poor hash function selection, the estimation error will be greater than the theoretical value. | |
|quantile |quantile(level)(x) |Returns the quantile of all values in the expression. Can only be used for numeric fields. Level range: 0–1 |quantile(0.5)(x) returns the 0.5 quantile of x. |
|uniq |uniq(x) |Counts distinct values. Has the same effect as count(distinct), with a 0.5% margin of error in accuracy. To obtain an exact value, use count(distinct). However, its query takes longer and may fail to return a result due to timeout, so it is not recommended. | |
|argMax |argMax(arg,val) |Calculates the maximum value based on the field val. Then retrieves the value of the arg field in the record where the maximum value is found. | |
|groupArray |groupArray(n)(fieldname) |Retrieves the first n records. The result is an array. | |
|any |any(x) |Returns the first value encountered. | |
|quantileExact |quantileExact(level)(x) |Returns the quantile of all values in the expression. Can only be used for numeric fields. Level range: 0–1. Has the same effect as quantile, but performs an exact query. When using quantileExact, the query takes longer and may fail to return a result due to timeout, so it is not recommended. |quantileExact(0.5)(x) returns the 0.5 quantile of x. |


<span id="6353d076"></span>
# 3. Date functions

<span id="e1c0a28c"></span>
## 3.1 Quick start with common functions

Date functions are used for time format conversion, time processing, retrieving specific dates, and so on.

<span id="ccb7816e"></span>
### 3.1.1 Convert text to time or date

Format:


* toDate(xxx) and to_date(xxx) convert string fields in yyyymmdd or yyyy\-mm\-dd format to date format.

* toDateTime(xxx) converts strings in yyyy\-mm\-dd hh:mm:ss format to time format.

* toDateOrNull(xxx) and toDateTimeOrNull(xxx) have the same functionality as the above two functions, and are suitable for cases where there is invalid data in the field, converting such data to null values.


Example:


|Field A |toDate(Field A) |toDateTime(Field A) |
|---|---|---|
|2020/12/21 |2020/12/21 |2020/12/21 0:00 |
|20201221 |2020/12/21 |2020/12/21 0:00 |
|2020/12/21 18:00 |2020/12/21 |2020/12/21 18:00 |


Field A is of string type; toDate(Field A) and toDateTime(Field A) convert it to date/time format.

<span id="5d38db32"></span>
### 3.1.2 Convert between time and timestamp

Format: Convert time or text\-type time to timestamp using toUnixTimestamp(xxx), that is, convert yyyy\-mm\-dd hh:mm:ss to a timestamp.

Example:


|Field A |toUnixTimestamp(Field A) |Additionally: toDateTime(toUnixTimestamp(Field A)+28800) |
|---|---|---|
|2020/12/21 18:00 |1608544800 |2020/12/22 2:00 |


Tip: For the converted timestamp, add 28800 seconds (the offset for 8 hours) to convert from UTC+0 to UTC+8, and then use the toDateTime function to convert it to a more readable time format.

<span id="d6318b65"></span>
### 3.1.3 Return the current date

Format: now(), generates a dynamic parameter that changes with the system time.

Example: If the current time is 2020\-12\-21 18:00:00, writing now() as a field means the current value of this field is 2020\-12\-21 18:00:00, and one hour later it will be 2020\-12\-21 19:00:00.

<span id="07794889"></span>
### 3.1.4 Return the date of this week's Monday

Format: toMonday(xx), returns the date of the Monday of the current week for the given date field.

Example:


|Field A |toMonday(Field A) |
|---|---|
|2020/12/22 |2020/12/21 |


<span id="3d8d0677"></span>
## 3.2 Detailed function description


|Function name |Function format |Purpose |Example |
|---|---|---|---|
|toDateTime |toDateTime(x) |Converts a string date and time to a date and time type. |toDateTime('2018\-12\-24 10:10:00') |
|toStartOfFiveMinute |toStartOfFiveMinute（x） |Rounds down the datetime to the nearest multiple of 5 minutes, returns the datetime. |toStartOfFiveMinute(toDateTime('2018\-12\-11 11:12:13')) returns 2018\-12\-11 11:10:00 |
|now |now（) |Generates the current date and time. |now() returns 2018\-12\-13 10:10:12 |
|toStartOfFifteenMinutes |toStartOfFifteenMinutes（x) |Rounds down the datetime to the nearest multiple of 15 minutes, returns the datetime. |toStartOfFifteenMinutes(toDateTime('2018\-12\-11 11:12:13')) returns 2018\-12\-11 11:00:00 |
|toStartOfInterval |toStartOfInterval(time_or_data, INTERVAL x unit [, time_zone]) |This is the general function for all functions named toStartOf\*. For example, toStartOfInterval(t, INTERVAL 1 year) returns the same result as toStartOfYear(t), toStartOfInterval(t, INTERVAL 1 month) returns the same result as toStartOfMonth(t), toStartOfInterval(t, INTERVAL 1 day) returns the same result as toStartOfDay(t), and toStartOfInterval(t, INTERVAL 15 minute) returns the same result as toStartOfFifteenMinutes(t). |toStartOfInterval(toDateTime('2019\-10\-10 09:09:20'), INTERVAL 1 year) returns 2019\-01\-01 |
|toIntervalDay |toIntervalDay(x) |Converts a date to a timestamp at the day level. |toIntervalDay(toDateTime('2019\-08\-12 11:12:13')) returns 1565579533 |
|toIntervalMinute |toIntervalMinute(x) |Converts a date to a timestamp at the minute level. |toIntervalMinute(toDateTime('2019\-08\-14 11:12:13')) returns 1565579533 |
|toIntervalHour |toIntervalHour(x) |Converts a date to a timestamp at the hour level. |toIntervalHour(toDateTime('2019\-08\-14 11:12:13')) returns 1565579533 |
|toMonday |toMonday(x) |Rounds Date or DateTime down to the Monday of the current week. Returns a Date type. |toMonday(toDateTime('2019\-08\-14 11:12:13')) returns 2019\-08\-12 |
|toStartOfHour |toStartOfHour(x) |Rounds DateTime down to the start of the current hour. |toStartOfHour(toDateTime('2018\-12\-11 11:12:13')) returns 11 |
|today |today( ) |Generates today's date. |today() returns 2018\-12\-13 |
|toHour |toHour(x) |Extracts the hour from a date and time. |toHour(toDateTime('2018\-12\-11 11:12:13')) returns 11 |
|toStartOfTenMinutes |toStartOfTenMinutes(x) |Rounds DateTime down to the nearest ten\-minute interval. |toStartOfTenMinute(toDateTime('2018\-12\-11 11:12:13')) returns 2018\-12\-11 11:00:00 |
|toStartOfDay |toStartOfMinute(string date time) |Rounds DateTime down to the start of the day. | |
|toYear |toYear(string date) |Returns the year from the date. | |
|toRelativeWeekNum |toRelativeWeekNum(date) |Converts Date or DateTime to the week number, starting from a fixed point in the past. | |
|toMonth |toMonth(string date) |Returns the month from the date. | |
|toStartOfMinute |toStartOfMinute( ) |Truncates date and time to the minute (zeroes out seconds), returns the date. |toStartOfMinute(toDateTime('2018\-12\-11 11:12:13')) returns 2018\-12\-11 11:12:00 |
|toUnixTimestamp |toUnixTimestamp( ) |Converts DateTime to a Unix timestamp. | |
|addDays |addDays(date_time,int) |The function adds a time interval to Date/DateTime and then returns Date/DateTime. | |
|toRelativeYearNum |toRelativeYearNum(date_time) |Converts Date or DateTime to the year number, starting from a fixed point in the past. | |
|year |year(Date/DateTime/String date) |Returns the year from the date. |year(toDateTime('2018\-12\-11 11:12:13')) returns 2018 |
|month |month(Date/DateTime/String date) |Returns the month from the date. |month(toDateTime('2018\-12\-11 11:12:13')) returns 12 |
|quarter |quarter(Date/DateTime/String date) |Returns the quarter number from the date. |quarter(toDateTime('2018\-12\-11 11:12:13')) returns 12 |
|day |day(Date/DateTime/String) |Returns dayOfMonth. |day('2019\-09\-12') returns 12 |
|last_day |last_day(Date/DateTime/String date) |Returns the last day of the month for the given date. |last_day(toDateTime('2018\-12\-11 11:12:13')) returns 2018\-12\-31 |
|next_day |next_day(Date/DateTime/String date, string day_of_week) |Returns the next day_of_week for the given date. |next_day(toDate('2015\-01\-14'), 'TU') returns 2015\-01\-20 |
|dateDiff |dateDiff(Date/DateTime date1, Date/DateTime date2 [, String timezone])； dateDiff(String unit, Date/DateTime date1, Date/DateTime date2 [, String timezone]) |Returns the difference between two dates. |dateDiff(now(), yesterday()) returns \-1 |
|date_sub |date_sub (string/Date/DateTime startdate, int days) |Returns the date/time days before start_time. |date_sub('2019\-09\-08', 1) returns '2019\-09\-07' |
|date_add |date_add (string/Date/DateTime startdate, int days) |Returns the date/time days after start_time. |date_add('2019\-09\-08', 1) returns '2019\-09\-09' |
|from_unixtime |from_unixtime(Date/DateTime/UInt32 date, String parttern[, String timezone]) |Converts a date or timestamp to a string in the specified pattern format. |from_unixtime(toDateTime('2019\-09\-09 09:00:00'), 'time: %F %T', 'Asia/Shanghai') returns 'time: 2019\-09\-09 09:00:00' |
|to_date,toDate |to_date(String/UInt16 date) |Converts a string or the date number since 1970\-01\-01 to a date type. |toDate('20190909') returns '2019\-09\-09' |
|date_format |date_format(Date/DateTime/String, String pattern) |Outputs the date in the specified format. |date_format('2019\-09\-09', 'yyyy') returns '2019' |
|unix_timestamp |unix_timestamp(Date/DateTime/String) |Converts a date to a timestamp. |unix_timestamp(toDateTime('2019\-09\-09 09:00:00'), 'time: %F %T', 'Asia/Shanghai') returns 'time: 2019\-09\-09 09:00:00' |
|toWeek |toWeek(date[,mode]) |Returns the week number for the date, range [0, 53] |toWeek(toDate('2019\-12\-06'), 3) returns 49 |
|toDayOfWeek |todayofweek(date) |Returns the day of the week for the date, range [1, 7] |todayofweek('2020\-01\-01') returns 3 |


<span id="4f197965"></span>
# 4. Type conversion functions

<span id="67eb49eb"></span>
## 4.1 Quick start with common functions

Type conversion functions are used to convert field types, such as converting text to numbers and vice versa.

<span id="ec09779c"></span>
### 4.1.1 Force conversion to any type

Format: cast(xxx, 'type'), converts xxx to a specific type.

Example:

cast(Field A, 'string') converts Field A to string format.

<span id="5248f41b"></span>
### 4.1.2 Convert to string (text)

Format: toString(xxx), converts field xxx to string format. This can convert fields of types such as numbers and dates.

Example:


|Field A |toString(Field A) |
|---|---|
|143876768892010 |143876768892010 |


Before conversion, Field A is in numeric format, which may be displayed in scientific notation during analysis due to its length; after converting to string, it can be preserved accurately.

<span id="3e58b6b3"></span>
### 4.1.3 Convert to integer value

Format: toInt64(xxx), converts field xxx to an integer. Only numbers are allowed in xxx.


|Field A |toInt64(Field A) |
|---|---|
|143876768892010 |143876768892010 |
|123a |Conversion failed |


<span id="bb49f365"></span>
## 4.2 Detailed function description


|Function name |Function format |Purpose |Example |
|---|---|---|---|
|cast |cast(X, 'Y') |General type casting function. Converts any data of type X to format Y. |Convert uid of int type to String type CAST (uid, 'String') |
|toString |toString(x) |Convert numeric, string, date, and other types to string type |toString('2018\-12\-24') returns 2018\-12\-24 |
|toInt64 |toInt64(x) |Convert data type to int format (64 bits) |toInt64(123.883) returns 123 |
|toUInt8OrZero |toUInt8OrZero(x) |Convert an unsigned integer string type to an integer type; otherwise, returns 0 |toUInt8OrZero('123.12') returns 0 |
|toDateOrZero |toDateOrZero(x) |Convert data type to DATE format; otherwise, returns 0 |toDateOrZero(toDateTime('2018\-12\-11 11:12:13')) returns 2018\-12\-11 |
|toUInt16OrZero |toUInt16OrZero(x) |Convert an unsigned integer string type to an integer type; otherwise, returns 0 |toUInt8OrZero('123') returns 123 |
|toUInt64OrZero |toUInt64OrZero(x) |Convert data type to int format (64 bits); returns 0 if failed |toUInt64OrZero('123') returns 123 |
|toDateOrNull |toDateOrNull(a) |Convert the data type of a to date or null | |
|toUInt32OrZero |toUInt32OrZero(x) |Convert data type to int format (32 bits); returns 0 if failed | |
|toFloat32OrZero |toFloat32OrZero( ) |Convert a numeric string to a numeric type |toFloat32OrZero('\-123') returns \-123 |
|toIntervalMonth |toIntervalMonth( ) |Convert a numeric parameter to an Interval type (time interval) | |
|toInt32 |toInt32(a) |Convert the data type of a to int32 | |
|toDateTimeOrNull |toDateTimeOrNull(a) |Convert the data type of a to datetime or null | |
|toFloat64 |toFloat64(a) |Convert the data type of a to float64 | |
|toUInt8 |toUInt8(a) |Convert the data type of a to UInt8 | |
|toFloat64OrZero |toFloat64OrZero(a) |Convert the data type of a to float64 or zero | |
|toUInt32 |toUInt32(a) |Convert the data type of a to UInt32 | |
|parseDateTimeBestEffort |parseDateTimeBestEffort() |Parse a numeric parameter as Date or DateTime type. Unlike toDate and toDateTime, parseDateTimeBestEffort can handle more complex date formats. | |
|parseDateTimeBestEffortOrNull |parseDateTimeBestEffortOrNull() |Parse a numeric parameter as Date or DateTime type; returns null if the date format cannot be processed | |
|parseDateTimeBestEffortOrZero |parseDateTimeBestEffortOrZero() |Parse a numeric parameter as Date or DateTime type; returns zero Date or zero DateTime if the date format cannot be processed | |


<span id="9345524b"></span>
# 5. String functions

<span id="ee997557"></span>
## 5.1 Quick start for commonly used functions

String functions are used to concatenate or extract text.

<span id="c07f4f68"></span>
### 5.1.1 String concatenation

Format: concat(xxx, xxx, xxx...), concatenates multiple fields together without separators.

Example: concat(Field A, Field B, Field C) results in: 门前大桥下, 123


|Field A |Field B |Field C |
|---|---|---|
|Under the bridge in front of the gate |， |123 |


<span id="10495bdd"></span>
### 5.1.2 String extraction

Format: substr(xxx, offset x, length y) or substring(xxx, offset x, length y), meaning to extract a substring from the string field xxx, starting from position x and taking y characters.

Example:


|Field A |substr(Field A,1,10) |
|---|---|
|2020/12/22 18:00 |2020/12/22 |


substr(Field A, 1, 10) extracts 10 characters from Field A starting at position 1, resulting in the output as shown above.

**Extension:**  Combination of concat and substr


|Field A |Field B |
|---|---|
|Xiaoming |8,9,8 |
|concat(Field A, 'the score of the second item is', substr(Field B, 3, 1)) yields the result: Xiaoming's score for the second item is 9 | |


<span id="8b7de120"></span>
#### 5.1.3 Return string length

Format: length(xxx), calculates the length of the string\-type field xxx

Example:


|Field A |length(Field A) |
|---|---|
|2020/12/22 18:00:00 |19 |


<span id="bdd27fb1"></span>
## 5.2 Function details


|Function name |Function format |Purpose |Example |
|---|---|---|---|
|substring |substring(s, offset, length) |Extract substring |substring('123abcABC', 2, 3) returns 23a |
|empty |empty(x) |Returns 1 if the string is empty; otherwise, returns 0 |empty('123a') returns 0 |
|length |length(x) |Returns the length of the string |length('123a') returns 4 |
|extractAll |extractAll(haystack,pattern) |Returns all matched substrings as a list |extractAll('iioomAj12123124OOBJ123B', '\d+') returns [12123124,123] |
|splitByChar |splitByChar(separator, s) |Split string by a single character | |
|concat |concat(s1, s2, ...) |Concatenate multiple strings in the parameters without a separator |concat('123', 'abc', 'ABC') returns 123abcABC |
|lower |lower(string) |Convert string to lowercase | |
|char_length |char_length(string) |Assuming the string is UTF\-8 encoded text, returns the number of Unicode characters in the string. If the input string is not UTF\-8 encoded, the function may return an unexpected value (no exception will be thrown). | |
|startsWith |startsWith(s, prefix) |Returns whether the string starts with the specified prefix. If the string starts with the specified prefix, returns 1; otherwise, returns 0. | |
|replaceRegexpAll |replaceRegexpAll(haystack,pattern,replacement) |Replaces all occurrences matching the pattern using regular expressions. |replaceOne('asd123cbbj464sd', 'sd', '\-') returns a\-123cbbj464\- |
|replaceRegexpOne |replaceRegexpOne(haystack, pattern, replacement) |Replaces using the 'pattern' regular expression. | |
|replaceAll |replaceAll(haystack, pattern, replacement) |Replaces all occurrences of the 'pattern' substring in 'haystack' with the 'replacement' substring. | |
|split |split(string str, string pat) |Splits str by the pat string and returns an array of the resulting substrings. |split('abc', 'b') returns ['a', 'c'] |
|concat_ws |concat_ws(String delimiter, String str1, String str2, ...) |Returns a string joined by the 'delimiter'. |concat_ws('_', 'abc', 'def') returns 'abc_def' |
|substring |substring(String str, int start, int len)，substr(String str, int start, int len) |Returns the substring of length len starting from position start. |substring('abc', 2); returns 'bc' |
|lpad,rpad |lpad(String, len, pad_str) |Pads str on the left with pad_str until it reaches length len. |lpad('abcd', 10, '.') returns '......abcd' |
|regexp_replace |regexp_replace(String str, String str1, String str2) |Returns the result of replacing str1 in str with str2; supports re2 regular expressions. |regexp_replace('world.', '^', 'hello ') returns 'hello world.' |


<span id="a4c35d35"></span>
# 6. Conditional functions

<span id="e8ce5852"></span>
## 6.1 Quick start for commonly used functions

Returns the corresponding value based on the specified condition. For example, if a \> 1, returns 1; if a < 1, returns 0. This must be implemented using conditional functions.

<span id="11676a1d"></span>
### 6.1.1 if function

Format: if(condition, a, b), returns value a if the condition is true, returns value b if the condition is false

Example:


|Field A |if(Field A \> 0, 'positive', 'negative') |
|---|---|
|200 |positive |


<span id="75285fac"></span>
### 6.1.2 case when function

Format:

case

when condition 1 then result 1

when condition 2 then result 2

……

else result n

end

This function is relatively long, but its structure is simple. Conditions are checked from top to bottom. When condition 1 is met, result 1 is returned and no further conditions are checked. If none of the conditions are met, result n is returned.

Example:


|Field A |case when Field A \> 300 then '\>300' when Field A \> 200 then '(200,300]' else null end |
|---|---|
|250 |(200,300] |
|105 | |
|350 |> 300 |


<span id="adfab87e"></span>
## 6.2 Function details


|Function name |Function format |Purpose |Example |
|---|---|---|---|
|multiIf |multiIf(cond_1, then_1, cond_2, then_2...else) |Allows you to write CASE operators more concisely in queries. Parameters: \*cond_N — the condition for the function to return then_N. \*then_N — the result of the function when executed. \*else — the result of the function if none of the conditions are met. |multiIf(1 \> 2, 'correct', 2 < 0, 'correct', 'incorrect') returns incorrect |
|if |if(cond, then, else), cond ? operator then : else |If cond != 0, returns then; if cond = 0, returns else. cond must be of type UInt8, and then and else must have the lowest common type. |if(1 \> 2, 'correct', 'incorrect') returns incorrect |
|case |CASE WHEN a THEN b [WHEN c THEN d]\* [ELSE e] END |If a is TRUE, returns b; if c is TRUE, returns d; otherwise, returns e. | |


<span id="6581928e"></span>
# 7. Username function

The username function is not an official ClickHouse function, but is a custom function that works with project user information to return specified information about the current user.

USERNAME() can return the username of the current user, as shown below. This function can also be used in combination with other functions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e4425ed839b444f8812dcabf82fe02ec~tplv-goo7wpa0wc-image.image) </span>

<span id="f884e5a4"></span>
# 8. JSON function


|Function name |Function format |Purpose |Example |
|---|---|---|---|
|visitParamExtractInt |visitParamExtractUInt(params, name) |Parses the value of the field named "name" as UInt64. If this is a string field, the function will attempt to parse a number from the beginning of the string. If the field does not exist or a number cannot be parsed from it, returns 0. | |
|visitParamExtractFloat |visitParamExtractFloat(params, name) |Parses the value of the field named "name" as float64. | |
|visitParamExtractBool |visitParamExtractBool(params, name) |Parses a true/false value. The result is UInt8. | |
|visitParamHas |visitParamHas(params, name) |Checks whether a field named "name" exists. | |
|visitParamExtractRaw |visitParamExtractRaw(params, name) |Returns the value of the field, including whitespace characters. |visitParamExtractRaw('{"abc":{"def":[1,2,3]}}', 'abc') = '{"def":[1,2,3]}' |
|get_json_object |get_json_object(string json_string, string path) |Returns the element specified by path in the JSON. |get_json_object('{"n_s" : [{"ac":"abc","xz":"xz"}, {"def":"def"}], "n_i" : [1, 23]}', '$.n_s[0].ac'); returns 'abc' |


<span id="219a0b7e"></span>
# 9. Mathematical function


|Function name |Function format |Purpose |Example |
|---|---|---|---|
|power |power(x, y) |Takes two parameters, x and y. Returns x raised to the power of y. | |
|pow |pow(x, y) |Takes two parameters, x and y. Returns x raised to the power of y. |pow(2, 3) returns 8 |
|sqrt |sqrt(x) |Takes a numeric parameter and returns its square root. |sqrt(4) returns 2 |


<span id="a9f5c53d"></span>
# 10. Nullable handling function


| | | | |
|---|---|---|---|
|Function name |Function format |Purpose |Example |
|isNotNull |isNotNull(x) |Checks whether the parameter is not NULL. Returns 1 if true, 0 if false |sNotNull('abc') returns 1 |
|isNull |isNull(x) |Checks whether the parameter is NULL. Returns 1 if NULL, 0 otherwise. |isNull(null) returns 1 |
|coalesce |coalesce(x,...) |Checks each parameter from left to right and returns the first parameter that is not 'NULL'. |coalesce(null,null,a,b,null) returns a |
|assumeNotNull |assumeNotNull( ) |Converts a value of Nullable type to a non\-Nullable type | |


<span id="654f1d62"></span>
# 11. Base conversion function


|Function name |Function format |Purpose |Example |
|---|---|---|---|
|conv |conv(String/Int num, Int from_base, Int to_base) |Base conversion |conv('10',10,2) returns '1010' |
|bin |bin(Int/DateTime/String) |Converts to a binary number |bin(10) returns '1010' |


<span id="28617dca"></span>
# 12. Hash function


|Function name |Function format |Purpose |
|---|---|---|
|cityHash64 |cityHash64O() |Computes CityHash64 for any number of strings or computes a hash for any number of other types using a specific hash function implementation |
|intHash64 |intHash64( ) |Computes a 64\-bit hash code from any type of integer |


<span id="7af8871d"></span>
# 13. URL function


|Function name |Function format |Purpose |Example |
|---|---|---|---|
|domain |domain(x) |Returns the domain name of a URL |domain('[http://www.baidu.com.cn](http://www.baidu.com.cn)') returns [www.baidu.com.cn](http://www.baidu.com.cn) |
|cutToFirstSignificantSubdomain |cutToFirstSignificantSubdomain( ) |Returns the content between the top\-level domain and the first significant subdomain |cutToFirstSignificantSubdomain('[https://news.yandex.com.tr/')](https://news.yandex.com.tr/')) = '[yandex.com](http://yandex.com).tr' |
|parse_url |parse_url(String url, String name) |Returns the part of the url specified by name. If parsing fails, returns an empty string. |parse_url('[https://bytedance.feishu.cn/space/xx#PN78WD',](https://bytedance.feishu.cn/space/xx#PN78WD',) 'PROTOCOL') returns https |


<span id="adc3ac8f"></span>
# 14. Map function


|Function name |Function format |Purpose |Example |
|---|---|---|---|
|map key |[map field name] |Extracts a specific field's data from a map\-type field |select deductions{'Federal Taxes'} from employees limit 1; |
|map |map(KeyType k1, ValueType v1, KeyType k2, ValueType v2 ...) |Constructs map\-type data |map('a', 'b', 'c', 'd') returns |
|str_to_map |map(String value, String kv_delimiter, String item_delimiter) |Converts a String to map type |str_to_map('a:b,c:d', ',', ':') returns |


<span id="84675582"></span>
# 15. Array function


|Function name |Function format |Purpose |Example |
|---|---|---|---|
|arrayConcat |arrayConcat(array) |Merges all arrays passed as parameters. |SELECT arrayConcat([1, 2], [3, 4], [5, 6]) AS res ┌─res─────┐ │ [1,2,3,4,5,6] │ └───────┘ |
|notEmpty |notEmpty() |Returns 0 for empty strings, 1 for non\-empty strings | |


<span id="577c8aff"></span>
# 16. ArrayJoin function


|Function name |Function format |Purpose |Example |
|---|---|---|---|
|arrayJoin |arrayJoin(array) |This function takes an array as a parameter and duplicates the row in the result set for each array element. Except for the values in the column where this function is applied, all values in the columns are simply duplicated; they are replaced by the corresponding array values. |SELECT arrayJoin([1, 2, 3] AS src) AS dst, 'Hello', src ┌dst\-┬'Hello'\-┬─src──┐ │ 1 │ Hello │ [1,2,3] │ │ 2 │ Hello │ [1,2,3] │ │ 3 │ Hello │ [1,2,3] │ └ ─ ┴ ─ ─ ┴─ ───┘ |


<span id="09690408"></span>
# 17. Modulo function


|Function name |Function format |Purpose |Example |
|---|---|---|---|
|pmod |pmod(Int a, Int b) |Floating\-point numbers are converted to integers for modulo operations. If there are special requirements, support can be added later. |pmod(10, 3) returns 1 |


<span id="592379d9"></span>
# 18. Rounding function


|Function name |Function format |Purpose |Example |
|---|---|---|---|
|round |round(x,[N]) |Rounds the value to the specified number of decimal places. This function returns the nearest number in sequence. If the given number has multiple nearest numbers, the function returns the number closest to an even number (banker's rounding method). |round(123.883, 1) returns 123.9 |


<span id="32059472"></span>
# 19. Arithmetic function


|Function name |Function format |Purpose |
|---|---|---|
|abs |abs(a) |Calculates the absolute value of the number (a). |


<span id="bd475204"></span>
# 20. Bitwise operation function


|Function name |Function format |Purpose |
|---|---|---|
|bitAnd |bitAnd(a, b) |The result type is an integer, with the number of bits equal to the maximum number of bits among its parameters. If at least one parameter is a signed number, the result is a signed number. If a parameter is a floating\-point number, it is converted to Int64. |


<span id="580f3215"></span>
# 21. Random function


|Function name |Function format |Purpose |
|---|---|---|
|rand |rand( ) |Returns a random number of type UInt32, where all UInt32 values have an equal probability of being generated. |


<span id="49190314"></span>
# 22. Other functions


|Function name |Function format |Purpose |Example |
|---|---|---|---|
|hostName |hostName() |Returns a string containing the name of the host executing this function. | |
|size |size(Array/Map/String) |Returns the number of elements. |size(map('a', 'b', 'c', 'd')) returns 2 |
