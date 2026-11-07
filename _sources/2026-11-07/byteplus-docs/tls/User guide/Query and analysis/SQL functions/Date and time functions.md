---
title: "Date and time functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Date-and-time-functions-2"
---

This document describes the syntax of date and time functions supported by TLS and provides usage examples for common scenarios.

<span id="06646c4b"></span>
## Function list

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Description</div>



* <div data-tips="true" data-tips-type="default">In TLS, log timestamps are accurate to the millisecond, so the time format (format) can be configured to the millisecond level.</div>


* <div data-tips="true" data-tips-type="default">By default, TLS adds the metadata field <code>__time__</code> to each log. The value of this field is in UNIX timestamp format, with a unit of milliseconds.</div>


* <div data-tips="true" data-tips-type="default">In TLS analysis statements (SQL statements), characters representing strings must be enclosed in single quotes (''), while characters not enclosed or enclosed in double quotes ("") are field names or column names. For example, <code>'time'</code> represents a string, <code>time</code> or <code>"time"</code> represents a field name or column name.</div>




|Function type |Function name |Syntax |Description |
|---|---|---|---|
|Date and time functions |[CURRENT_DATE function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#c1f35224) |CURRENT_DATE |Query the current date. |
||[CURRENT_TIME function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#cd19e45d) |CURRENT_TIME |Query the current time and time zone. |
||[CURRENT_TIMESTAMP function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#c0f702cf) |CURRENT_TIMESTAMP |Query the current date, time, and time zone. |
||[CURRENT_TIMEZONE function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#f102eb04) |CURRENT_TIMEZONE() |Query the current time zone. |
||[DATE function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#e6b74c1d) |DATE(KEY) |Extract the date part from a date and time value. |
||[DATE_FORMAT function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#3d86dd7a) |DATE_FORMAT(KEY, format) |Convert a date or time of Timestamp type to another specified format. |
||[DATE_PARSE function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#6f219f00) |DATE_PARSE(KEY, format) |Convert a date and time string to another specified format. |
||[FROM_ISO8601_DATE function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#d9d13813) |FROM_ISO8601_DATE(KEY) |Convert a date in ISO8601 format to a date of Date type. |
||[FROM_ISO8601_TIMESTAMP function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#03c6b6e4) |FROM_ISO8601_TIMESTAMP(KEY) |Convert a date and time in ISO8601 format to a date and time of Timestamp type. |
||[FROM_UNIXTIME function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#0771d686) |FROM_UNIXTIME(KEY) |Convert a UNIX timestamp to a date and time of Timestamp type without a time zone. |
|||FROM_UNIXTIME(KEY, time zone) |Convert a UNIX timestamp to a date and time of Timestamp type with a time zone. |
|||FROM_UNIXTIME(KEY, hours, minutes) |Convert a UNIX timestamp to a date and time of Timestamp type with a time zone, and support setting the time zone offset. |
||[LOCALTIME function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#14a4926e) |LOCALTIME |Query the current local time. |
||[LOCALTIMESTAMP function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#c9695529) |LOCALTIMESTAMP |Query the current local date and time. |
||[NOW function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#1c00b3eb) |NOW() |Query the current date and time.<br><br>The NOW function is equivalent to the CURRENT_TIMESTAMP function. |
||[TO_ISO8601 function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#413a051d) |TO_ISO8601(KEY) |Convert date and time values of the Date type or Timestamp type to ISO8601 formatted date and time. |
||[TO_UNIXTIME function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#29aa121d) |TO_UNIXTIME(KEY) |Convert date and time values of the Timestamp type to a UNIX timestamp. |
|Date and time extraction functions |[DAY function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#c64e234b) |DAY(KEY)<br><br> |Extract the day component from a date and time, using the month as the cycle.<br><br>The DAY function is equivalent to the DAY_OF_MONTH function. |
||[DAY_OF_MONTH function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#c177d181) |DAY_OF_MONTH(KEY) |Extract the day component from a date and time, using the month as the cycle.<br><br>The DAY_OF_MONTH function is equivalent to the DAY function. |
||[DAY_OF_WEEK function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#37844286) |DAY_OF_WEEK(KEY) |Extract the day component from a date and time, using the week as the cycle.<br><br>The DAY_OF_WEEK function is equivalent to the DOW function. |
||[DAY_OF_YEAR function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#592ecc11) |DAY_OF_YEAR(KEY) |Extract the day component from a date and time, using the year as the cycle.<br><br>The DAY_OF_YEAR function is equivalent to the DOY function. |
||[DOW function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#ce586ed9) |DOW(KEY) |Extract the day component from a date and time, using the week as the cycle.<br><br>The DOW function is equivalent to the DAY_OF_WEEK function. |
||[DOY function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#c241bd88) |DOY(KEY) |Extract the day component from a date and time, using the year as the cycle.<br><br>The DOY function is equivalent to the DAY_OF_YEAR function. |
||[EXTRACT function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#8af84787) |EXTRACT(field from KEY) |Extract the date or time part from a date and time value by specifying the field. |
||[HOUR function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#8f0eb941) |HOUR(KEY) |Extract the hour component from a date and time, using the 24\-hour format. |
||[MINUTE function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#bc3a8a60) |MINUTE(KEY) |Extract the minute component from a date and time. |
||[MONTH function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#ebcb16c9) |MONTH(KEY) |Extract the month component from a date and time. |
||[QUARTER function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#a16bf1dc) |QUARTER(KEY) |Return the quarter in which the date falls. |
||[SECOND function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#fc1a81e9) |SECOND(KEY) |Extract the second component from a date and time. |
||[TIMEZONE_HOUR function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#70a6f2ad) |TIMEZONE_HOUR(KEY) |Calculate the hour offset of the time zone. |
||[TIMEZONE_MINUTE function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#54ebffd2) |TIMEZONE_MINUTE(KEY) |Calculate the minute offset of the time zone. |
||[WEEK function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#87965bba) |WEEK(KEY) |Calculate which week of the year the target date falls in.<br><br>The WEEK function is equivalent to the WEEK_OF_YEAR function. |
||[WEEK_OF_YEAR function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#12eeb06a) |WEEK_OF_YEAR(KEY) |Calculate which week of the year the target date falls in.<br><br>The WEEK_OF_YEAR function is equivalent to the WEEK function. |
||[YEAR function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#2240d512) |YEAR(KEY) |Extract the year component from a date and time. |
||[YEAR_OF_WEEK function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#67eb132a) |YEAR_OF_WEEK(KEY) |Extract the year of the target date in the ISO week calendar.<br><br>The YEAR_OF_WEEK function is equivalent to the YOW function. |
||[YOW function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#849be187) |YOW(KEY)<br><br> |Extract the year of the target date in the ISO week calendar.<br><br>The YOW function is equivalent to the YEAR_OF_WEEK function. |
|Time interval functions |[DATE_ADD function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#fd1d74b9) |DATE_ADD(unit, N, KEY) |Add or subtract a specified time interval to or from a date and time value. |
||[DATE_DIFF function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#f12bb917) |DATE_DIFF(unit, KEY1, KEY2) |Calculate the difference between two dates or time points.<br><br> |
||[DATE_TRUNC function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#d1f8ea12) |DATE_TRUNC(unit, KEY) |Truncate a date or time value to the unit you specify, aligning to milliseconds, seconds, minutes, hours, days, months, or years. Supported UNIX timestamps for parsing are at the second or millisecond level. |
||[DATE_TRUNC_SEC function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#6ba081bf) |DATE_TRUNC_SEC(unit, KEY) |Truncate the date or time according to the time unit you specify, and align it to milliseconds, seconds, minutes, hours, days, months, or years. Only second\-level UNIX timestamps are supported for parsing. |
|Time series completion function |[TIME_SERIES function](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2#691f29e7) |TIME_SERIES(KEY, window_time, format, padding_data) |Complete missing data within the query time window. |


<span id="c1f35224"></span>
## CURRENT_DATE function

The CURRENT_DATE function is used to query the current date.

<span id="5873e734"></span>
### Function **syntax**


* Syntax format

   ```SQL
   CURRENT_DATE
   ```
   

* Return value description

   The return value is of type Date, formatted as `YYYY-MM-DD`.


<span id="d6610459"></span>
### Function example


* Scenarios

   Query the current date.

* Query and analysis statement

   ```SQL
   * | SELECT CURRENT_DATE
   ```
   

* Query and analysis result

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/54bb351c63dd4a559bf891f41f289fc5) </span>


<span id="cd19e45d"></span>
## CURRENT_TIME function

The CURRENT_TIME function is used to query the current time and time zone.

<span id="3348b2c6"></span>
### Function **syntax**


* Syntax format

   ```SQL
   CURRENT_TIME
   ```
   

* Return value description

   The return value is of type Time, formatted as `HH:MM:SS.Ms Time_zone`.


<span id="41ee5dfd"></span>
### Function example


* Scenarios

   Query the current time and time zone.

* Query and analysis statement

   ```SQL
   * | SELECT CURRENT_TIME
   ```
   

* Query and analysis result

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/610683800e774f4e86f42c026835dec7) </span>


<span id="c0f702cf"></span>
## CURRENT_TIMESTAMP function

The CURRENT_TIMESTAMP function is used to query the current date, time, and time zone.

<span id="62c6dcbb"></span>
### Function **syntax**


* Syntax format

   ```SQL
   CURRENT_TIMESTAMP
   ```
   

* Return value description

   The return value is of type Timestamp, formatted as `YYYY-MM-DD HH:MM:SS.Ms Time_zone`.


<span id="91c68a30"></span>
### Function example


* Scenarios

   Query the current date, time, and time zone.

* Query and analysis statement

   ```SQL
   * | SELECT CURRENT_TIMESTAMP
   ```
   

* Query and analysis result

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/3c35257f9c9a478ba820184da6df821a) </span>


<span id="f102eb04"></span>
## CURRENT_TIMEZONE function

The CURRENT_TIMEZONE function is used to query the current time zone.

<span id="1d6a39c5"></span>
### **Syntax format**


* Syntax format

   ```SQL
   CURRENT_TIMEZONE()
   ```
   

* Return value description

   The return value is of type Varchar.


<span id="784294b4"></span>
### Function example


* Scenarios

   Query the current time zone.

* Query and analysis statement

   ```SQL
   * | SELECT CURRENT_TIMEZONE()
   ```
   

* Query and analysis result

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/bc26e9d9d74e4a758e68e035eb18710d) </span>


<span id="e6b74c1d"></span>
## DATE function

The DATE function is used to extract the date part from a date and time value.

<span id="f2eb6d2c"></span>
### Function **syntax**


* Syntax format

   ```SQL
   DATE(KEY)
   ```
   

* Parameters description

   
   |Parameters |Description |
   |---|---|
   |KEY |Field or expression, with a value of type Date or Timestamp. |
   

* Return value description

   The return value is of type Date.


<span id="b01435a3"></span>
### Function example


* Scenarios

   Use the CURRENT_TIMESTAMP function to obtain the current date and time, then use the DATE function to extract the date part.

* Query and analysis statement

   ```SQL
   * | SELECT CURRENT_TIMESTAMP AS timestamp, DATE(CURRENT_TIMESTAMP) AS date
   ```
   

* Query and analysis result

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/d1051b3f8add4da9979b10ac8c5f8d7a) </span>


<span id="3d86dd7a"></span>
## DATE_FORMAT function

The DATE_FORMAT function is used to convert a Timestamp\-type date or time to another specified format.

<span id="e80b66aa"></span>
### Function syntax


* Syntax format

   ```SQL
   DATE_FORMAT(KEY, format)
   ```
   

* Parameters description

   
   |Parameters |Description |
   |---|---|
   |KEY |Field or expression, with a value of type Timestamp. |
   |format |Conversion format. Details are shown in the following table. |
   

* Format description

   
   |format |Description |
   |---|---|
   |E |Abbreviation for the day of the week. For example, Mon, Tues. |
   |MMM |Abbreviation for the month. For example, Jan, Feb. |
   |M |Month. Value range: 1~12. |
   |dd |Day of the month. Decimal format, value range: 01~31. |
   |d |Day of the month. Decimal format, value range: 1~31. |
   |H |Hour, 24\-hour format. |
   |h |Hour, 12\-hour format. |
   |mm |Minute. Value range: 00~59. |
   |DDD |Day of the year. Value range: 001~366. |
   |MMMM |Full English name of the month, for example, January, February. |
   |MM |Month. Value range: 01~12. |
   |a |AM or PM. |
   |hh:mm:ss a |12\-hour time format, in the form `hh:mm:ss AM/PM`. |
   |ss |Second. Value range: 00~59. |
   |HH:mm:ss |24\-hour time format, in the form `HH:mm:ss`. |
   |ww |When Sunday is considered the first day of the week, ww indicates the week number of the year. Value range: 01~53. |
   |EEEE |Name of the day of the week. For example, Monday, Tuesday. |
   |u |Four\-digit year. For example, 2024. |
   |Y |Four\-digit year. For example, 2024. |
   |y |Four\-digit year. For example, 2024. |
   |G |Era designator. For example, AD (after Christ) or BC (before Christ). |
   |L |Month of the year (standalone form). |
   |F |Number of days elapsed in the week; for example, Tuesday is 1, indicating 1 day has passed in the week. |
   |k |Hour of the day. Value range: 0~23. |
   |K |Hour in AM/PM. Value range: 0~11. |
   

* Return value description

   The return value is of type Varchar.


<span id="a6c19215"></span>
### Function example


* Scenarios

   Aggregate data by the month in the `sli_time` field value.

* Log example

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/422d8508ed1d45aa9f9678827ff866aa) </span>

* Query and analysis statement

   ```SQL
   * | SELECT DATE_FORMAT(date_trunc('second', sli_time), 'yyyy-MM-dd HH') AS M GROUP BY M
   ```
   

* Query and analysis result

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/75c7aebc536747fdbeaf75fa841942c1) </span>


<span id="6f219f00"></span>
## DATE_PARSE function

The DATE_PARSE function is used to convert date and time strings to another specified format.

<span id="d74c5d67"></span>
### Function **syntax**


* Syntax format

   ```SQL
   DATE_PARSE(KEY, format)
   ```
   

* Parameters description

   
   |Parameters |Description |
   |---|---|
   |KEY |Field or expression, with a value as a date and time string. |
   |format |Conversion format. Details are shown in the following table. |
   

* Format description

   
   |format |Description |
   |---|---|
   |%a |Abbreviation for the English name of the day of the week. For example, Sun, Sat. |
   |%b |Abbreviation for the English name of the month. For example, Jan, Dec. |
   |%c |Month. Value range: 1 ~ 12. |
   |%D |Day of the month with suffix, for example, 0th, 1st, 2nd, 3rd. |
   |%d |Day of the month in decimal format, value range: 01 ~ 31. |
   |%e |Day of the month in decimal format, value range: 1 ~ 31. |
   |%H |Hour, 24\-hour format. |
   |%h |Hour, 12\-hour format. |
   |%i |Minute, value range: 00 ~ 59. |
   |%j |Day of the year, value range: 001 ~ 366. |
   |%k |Hour, value range: 0 ~ 23. |
   |%l |Hour, value range: 1 ~ 12. |
   |%M |English name of the month, for example January, December. |
   |%m |Month in numeric format, value range: 01 ~ 12. |
   |%p |AM, PM. |
   |%r |Time in 12\-hour format, formatted as `hh:mm:ss AM/PM`. |
   |%S |Second, value range: 00 ~ 59. |
   |%s |Second, value range: 00 ~ 59. |
   |%f |Millisecond, value range: 000 ~ 999. |
   |%T |Time in 24\-hour format, formatted as `hh:mm:ss`. |
   |%v |Week number of the year, Monday is the first day of the week, value range: 01 ~ 53. |
   |%W |English name of the day of the week. For example Sunday, Saturday. |
   |%Y |4\-digit year. For example 2024. |
   |%y |2\-digit year. For example 24. |
   |%% |Escape character for %. |
   

* Return value description

   The return value is of the Timestamp type.


<span id="5b311eb0"></span>
### Function example


* Scenarios

   Convert the value of the `time_str` field to the `%Y-%m-%d %H:%i:%s` format.

* Log example

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/3ff96e7b8dea48f4a9b7b3c87c31393f" width="1282px" />   </div>
   

* Query and analysis statement

   ```SQL
   *|SELECT DATE_PARSE(time_str, '%Y-%m-%d %H:%i:%s')
   ```
   

* Query and analysis result

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/8f7e32285e9c47a690ea1a3d5bfd55e2" width="1282px" />   </div>
   


<span id="d9d13813"></span>
## FROM_ISO8601_DATE function

The FROM_ISO8601_DATE function is used to convert a date in ISO8601 format to a date of the Date type.

<span id="fb64fd9d"></span>
### Function **syntax**


* Syntax format

   ```SQL
   FROM_ISO8601_DATE(KEY)
   ```
   

* Parameters description

   
   |Parameters |Description |
   |---|---|
   |KEY |Field or expression, value is in ISO8601 format. |
   

* Return value description

   The return value is of the Date type, in the format `YYYY-MM-DD`.


<span id="0a6896e6"></span>
### Function example


* Scenarios

   Convert the string `2023-01-01` to a date of the DATE type.

* Query and analysis statement

   ```SQL
   * | SELECT FROM_ISO8601_DATE('2023-01-01')
   ```
   

* Query and analysis result

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/14c1772221784e9bbb740617c1b8343e) </span>


<span id="03c6b6e4"></span>
## FROM_ISO8601_TIMESTAMP function

The FROM_ISO8601_TIMESTAMP function is used to convert a date and time in ISO8601 format to a date and time of the Timestamp type.

<span id="5e3058d6"></span>
### Function **syntax**


* Syntax format

   ```SQL
   FROM_ISO8601_TIMESTAMP(KEY)
   ```
   

* Parameters description

   
   |Parameters |Description |
   |---|---|
   |KEY |Field or expression, value is in ISO8601 format. |
   

* Return value description

   The return value is of the Timestamp type, in the format `YYYY-MM-DD HH:MM:SS.Ms Time_zone`.


<span id="beff2b7f"></span>
### Function example


* Scenarios

   Convert the string `2023-09-06T12:20:35` to a date and time of the Timestamp type.

* Query and analysis statement

   ```SQL
   * | SELECT FROM_ISO8601_TIMESTAMP('2023-09-06T12:20:35')
   ```
   

* Query and analysis result

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/8686e1f1b9de49a38c0c646dcef1aae7) </span>


<span id="0771d686"></span>
## FROM_UNIXTIME function

The FROM_UNIXTIME function is used to convert a UNIX timestamp to a date and time of the Timestamp type.

<span id="9f91a5b2"></span>
### Function **syntax**


* Syntax format

   * Convert to a date and time of the Timestamp type without a time zone.

      ```SQL
      FROM_UNIXTIME(KEY)
      ```
      

   * Convert to a date and time of the Timestamp type with a time zone.

      ```SQL
      FROM_UNIXTIME(KEY,time zone)
      ```
      

   * Convert to a date and time of the Timestamp type with a time zone, and support setting the time zone offset.

      ```SQL
      FROM_UNIXTIME(KEY, hours, minutes)
      ```
      

* Parameters description

   
   |Parameters |Description |
   |---|---|
   |KEY |Field or expression, value is a UNIX timestamp. |
   |time zone |Time zone, for example `Asia/shanghai`. |
   |hours |Hour offset of the time zone, for example +07, \-09. |
   |minutes |Minute offset of the time zone, for example +30, \-45. |
   

* Return value description

   The return value is of the Timestamp type, in the format `YYYY-MM-DD HH:MM:SS.Ms` or `YYYY-MM-DD HH:MM:SS.Ms Time_zone`.


<span id="b1027ea7"></span>
### Function example


* Scenarios

   Convert the value of the `__time__` field to a date and time of the Timestamp type with a time zone.

* Log example

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/82b22b5b493a43909768916c09bec9ac" width="1282px" />   </div>
   

* Query and analysis statement

   ```SQL
   * | SELECT FROM_UNIXTIME(__time__/1000,'Asia/shanghai')
   ```
   

* Query and analysis result

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/a978e7424f6c43fbb8e1ab12817d0a1b" width="1284px" />   </div>
   


<span id="14a4926e"></span>
## LOCALTIME function

The LOCALTIME function is used to query the current local time.

<span id="1edc6629"></span>
### Function **syntax**


* Syntax format

   ```SQL
   LOCALTIME
   ```
   

* Return value description

   The return value is of the Time type, in the format `HH:MM:SS.Ms`.


<span id="17f6d915"></span>
### Function example


* Scenarios

   Query the local time.

* Query and analysis statement

   ```SQL
   * | SELECT LOCALTIME
   ```
   

* Query and analysis result

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/2e3136bc6b564fbb87c7e586b87a39b4) </span>


<span id="c9695529"></span>
## LOCALTIMESTAMP function

The LOCALTIMESTAMP function is used to query the current local date and time.

<span id="e890ea46"></span>
### **Syntax format**


* Syntax format

   ```SQL
   LOCALTIMESTAMP
   ```
   

* Return value description

   The return value is of the Timestamp type, in the format `YYYY-MM-DD HH:MM:SS.Ms`.


<span id="e2cf04c5"></span>
### Function example


* Scenarios

   Query the local date and time.

* Query and analysis statement

   ```SQL
   * | SELECT LOCALTIMESTAMP
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/c8b2bbe0f141436db260081dd1dd6e17) </span>


<span id="1c00b3eb"></span>
## NOW function

The NOW function is used to return the current date and time. The NOW function is equivalent to the CURRENT_TIMESTAMP function.

<span id="0511feab"></span>
### Function **syntax**


* Syntax format

   ```SQL
   NOW()
   ```
   

* Return value description

   The return value type of the function is Timestamp. The format is `YYYY-MM-DD HH:MM:SS.Ms Time_zone`.


<span id="44167d34"></span>
### Function example


* Scenarios

   Query the current date and time.

* Query and analysis statement

   ```SQL
   * | SELECT NOW()
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/84b70eaa0e6c4ff9bb8d1d687a96f3da) </span>


<span id="413a051d"></span>
## TO_ISO8601 function

The TO_ISO8601 function is used to convert a value of type Date or Timestamp to a date and time in ISO8601 format.

<span id="1e8ef66d"></span>
### Function **syntax**


* Syntax format

   ```SQL
   TO_ISO8601(KEY)
   ```
   

* Parameters description

   
   |Parameters |Description |
   |---|---|
   |KEY |Field or expression, value is of Date or Timestamp type. |
   

* Return value description

   The return value is of type Varchar.


<span id="45a8b525"></span>
### Function example


* Scenarios

   Use the CURRENT_TIMESTAMP function to obtain the current date and time, then use the TO_ISO8601 function to convert the current date and time to ISO8601 format.

* Query and analysis statement

   ```SQL
   * | SELECT TO_ISO8601(CURRENT_TIMESTAMP) AS ISO8601
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/225212f19cac450a8a2fbf087dd418b8) </span>


<span id="29aa121d"></span>
## TO_UNIXTIME function

The TO_UNIXTIME function is used to convert a value of type Timestamp to a UNIX timestamp.

<span id="451a99fd"></span>
### Function **syntax**


* Syntax format

   ```SQL
   TO_UNIXTIME(KEY)
   ```
   

* Parameters description

   
   |Parameters |Description |
   |---|---|
   |KEY |Field or expression, value is of Timestamp type. |
   

* Return value description

   The return value is of type Double.


<span id="55de06cc"></span>
### Function example


* Scenarios

   Query the UNIX timestamp corresponding to the current time.

* Query and analysis statement

   ```SQL
   * | SELECT TO_UNIXTIME(NOW())
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/5ee4177ba5334549be04ae85a6b61a93) </span>


<span id="c64e234b"></span>
## DAY function

The DAY function is used to extract the day from a date and time, using the month as the cycle. The DAY function is equivalent to the DAY_OF_MONTH function.

<span id="75333aeb"></span>
### Function **syntax**


* Syntax format

   ```SQL
   DAY(KEY)
   ```
   

* Parameters description

   
   |Parameters |Description |
   |---|---|
   |KEY |Field or expression, value is of Timestamp or Date type. |
   

* Return value description

   The return value is of type Bigint, ranging from 1 to 31.


<span id="a1fd0fae"></span>
### Function example


* Scenarios

   Use the CURRENT_DATE function to obtain the current date, then use the DAY function to extract the day of the month for the current date.

* Query and analysis statement

   ```SQL
   * | SELECT CURRENT_DATE, DAY(CURRENT_DATE)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/0f9bfa825697497c9d8c734fcbc445ab) </span>


<span id="c177d181"></span>
## DAY_OF_MONTH function

The DAY_OF_MONTH function is used to extract the day from a date and time, using the month as the cycle. The DAY_OF_MONTH function is equivalent to the DAY function.

<span id="ab41f3e4"></span>
### Function **syntax**


* Syntax format

   ```SQL
   DAY_OF_MONTH(KEY)
   ```
   

* Parameters description

   
   |Parameters |Description |
   |---|---|
   |KEY |Field or expression, value is of Timestamp or Date type. |
   

* Return value description

   The return value is of type Bigint.


<span id="ce483be5"></span>
### Function example


* Scenarios

   Use the CURRENT_DATE function to obtain the current date, then use the DAY_OF_MONTH function to extract the day of the month for the current date.

* Query and analysis statement

   ```SQL
   * | SELECT CURRENT_DATE, DAY_OF_MONTH(CURRENT_DATE)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/451c4212a87e4b109eaf9118a2bba60f) </span>


<span id="37844286"></span>
## DAY_OF_WEEK function

The DAY_OF_WEEK function is used to extract the day from a date and time, using the week as the cycle.

<span id="3888914d"></span>
### Function **syntax**


* Syntax format

   ```SQL
   DAY_OF_WEEK(KEY)
   ```
   

* Parameters description

   
   |Parameters |Description |
   |---|---|
   |KEY |Field or expression, value is of Timestamp or Date type. |
   

* Return value description

   The return value is of BIGINT type.


<span id="2cc85bbf"></span>
### Function example


* Scenarios

   Use the CURRENT_DATE function to obtain the current date, then use the DAY_OF_WEEK function to determine the day of the week for the current date.

* Query and analysis statements

   ```SQL
   * | SELECT CURRENT_DATE, DAY_OF_WEEK(CURRENT_DATE)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/4e08d4c0a8fd4fc08ee93e53c0f96aec) </span>


<span id="592ecc11"></span>
## DAY_OF_YEAR function

The DAY_OF_YEAR function is used to extract the day of the year from a date and time.

<span id="ec25d3f2"></span>
### Function**syntax**


* Syntax format

   ```SQL
   DAY_OF_YEAR(KEY)
   ```
   

* Parameters description

   
   |Parameters |Description |
   |---|---|
   |KEY |Field or expression, value is of Timestamp or Date type. |
   

* Return value description

   The return value is of BIGINT type.


<span id="5011ea3c"></span>
### Function example


* Scenarios

   Use the CURRENT_DATE function to obtain the current date, then use the DAY_OF_YEAR function to determine the day of the year for the current date.

* Query and analysis statements

   ```SQL
   * | SELECT CURRENT_DATE, DAY_OF_YEAR(CURRENT_DATE)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/4e08d4c0a8fd4fc08ee93e53c0f96aec) </span>


<span id="ce586ed9"></span>
## DOW function

The DOW function is used to extract the day of the week from a date and time. The DOW function is equivalent to the DAY_OF_WEEK function.

<span id="5e738e6a"></span>
### Function**syntax**


* Syntax format

   ```SQL
   DOW(KEY)
   ```
   

* Parameters description

   
   |Parameters |Description |
   |---|---|
   |KEY |Field or expression, value is of Timestamp or Date type. |
   

* Return value description

   The return value is of BIGINT type.


<span id="b9066cad"></span>
### Function example


* Scenarios

   Use the CURRENT_DATE function to obtain the current date, then use the DOW function to determine the day of the week for the current date.

* Query and analysis statements

   ```SQL
   * | SELECT CURRENT_DATE, DOW(CURRENT_DATE)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/4e08d4c0a8fd4fc08ee93e53c0f96aec) </span>


<span id="c241bd88"></span>
## DOY function

The DOY function is used to extract the day of the year from a date and time. The DOY function is equivalent to the DAY_OF_YEAR function.

<span id="325e0c86"></span>
### Function**syntax**


* Syntax format

   ```SQL
   DOY(KEY)
   ```
   

* Parameters description

   
   |Parameters |Description |
   |---|---|
   |KEY |Field or expression, value is of Timestamp or Date type. |
   

* Return value description

   The return value is of BIGINT type.


<span id="a88f57fd"></span>
### Function example


* Scenarios

   Use the CURRENT_DATE function to obtain the current date, then use the DOY function to determine the day of the year for the current date.

* Query and analysis statements

   ```SQL
   * | SELECT CURRENT_DATE, DOY(CURRENT_DATE)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/4e08d4c0a8fd4fc08ee93e53c0f96aec) </span>


<span id="8af84787"></span>
## EXTRACT function

The EXTRACT function extracts a date or time part from a date and time by specifying a field.

<span id="8302bae8"></span>
### Function**syntax**


* Syntax format

   ```SQL
   EXTRACT(field from KEY)
   ```
   

* Parameters description

   
   |Parameters |Description |
   |---|---|
   |field |Possible values: year, quarter, month, week, day, day_of_month, day_of_week, dow, day_of_year, doy, year_of_week, yow, hour, minute, second, timezone_hour, timezone_minute. |
   |KEY |Field or expression, value is of Date, Time, Timestamp, or interval (actual varchar(9)) type. |
   

* Return value description

   The return value is of BIGINT type.


<span id="488afcde"></span>
### Function example


* Scenarios

   Use the CURRENT_DATE function to obtain the current date, then use the EXTRACT function to extract the year from the current date.

* Query and analysis statements

   ```SQL
   * | SELECT CURRENT_DATE, EXTRACT(year from CURRENT_DATE)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/2b505ab68bb444c2a241aec2d0b8c4f4) </span>


<span id="8f0eb941"></span>
## HOUR function

The HOUR function is used to extract the hour from a date and time in 24\-hour format.

<span id="0fe6754d"></span>
### Function**syntax**


* Syntax format

   ```SQL
   HOUR(KEY)
   ```
   

* Parameters description

   
   |Parameters |Description |
   |---|---|
   |KEY |Field or expression, value is of Timestamp type. |
   

* Return value description

   The return value is of BIGINT type.


<span id="a9b590f9"></span>
### Function example


* Scenarios

   Use the CURRENT_TIMESTAMP function to obtain the current date and time, then use the HOUR function to extract the hour from the current time.

* Query and analysis statement

   ```SQL
   * | SELECT CURRENT_TIMESTAMP, HOUR(CURRENT_TIMESTAMP)
   ```
   

* Query and analysis result

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ef1eab0ba8cc43adbed4cfb9205d14c6) </span>


<span id="bc3a8a60"></span>
## MINUTE function

The MINUTE function is used to extract the minute from a date and time.

<span id="773020c9"></span>
### Function**syntax**


* Syntax format

   ```SQL
   MINUTE(KEY)
   ```
   

* Parameters description

   
   |Parameters |Description |
   |---|---|
   |KEY |Field or expression, value is of Timestamp type. |
   

* Return value description

   The return value is of BIGINT type.


<span id="1f348eb3"></span>
### Function example


* Scenarios

   Use the CURRENT_TIMESTAMP function to obtain the current date and time, then use the MINUTE function to extract the minute from the current time.

* Query and analysis statement

   ```SQL
   * | SELECT CURRENT_TIMESTAMP, MINUTE(CURRENT_TIMESTAMP)
   ```
   

* Query and analysis result

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/25cdccd73a3a4638bf75e2eaadfbebaf) </span>


<span id="ebcb16c9"></span>
## MONTH function

The MONTH function is used to extract the month from a date and time.

<span id="09c63653"></span>
### Function**syntax**


* Syntax format

   ```SQL
   MONTH(KEY)
   ```
   

* Parameters description

   
   |Parameters |Description |
   |---|---|
   |KEY |Field or expression, value is of Timestamp or Date type. |
   

* Return value description

   The return value is of BIGINT type.


<span id="c57728a7"></span>
### Function example


* Scenarios

   Use the CURRENT_TIMESTAMP function to obtain the current date and time, then use the MONTH function to extract the month from the current date.

* Query and analysis statement

   ```SQL
   * | SELECT CURRENT_TIMESTAMP, MONTH(CURRENT_TIMESTAMP)
   ```
   

* Query and analysis result

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/563c6853bbc54037bd690c92a6069d74) </span>


<span id="a16bf1dc"></span>
## QUARTER function

The QUARTER function is used to determine the quarter of a given date.

<span id="0fad4589"></span>
### Function**syntax**


* Syntax format

   ```SQL
   QUARTER(KEY)
   ```
   

* Parameters description

   
   |Parameters |Description |
   |---|---|
   |KEY |Field or expression, value is of Timestamp or Date type. |
   

* Return value description

   The return value is of BIGINT type. For example, 1 indicates the first quarter.


<span id="f11892f6"></span>
### Function example


* Scenarios

   Use the CURRENT_TIMESTAMP function to obtain the current date and time, then use the QUARTER function to determine the quarter of the current date.

* Query and analysis statement

   ```SQL
   * | SELECT CURRENT_TIMESTAMP, QUARTER(CURRENT_TIMESTAMP)
   ```
   

* Query and analysis result

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/9ea2f94cef744b09a869092693fe1799) </span>


<span id="fc1a81e9"></span>
## SECOND function

The SECOND function is used to extract the second from a date and time.

<span id="b440d4a5"></span>
### Function**syntax**


* Syntax format

   ```SQL
   SECOND(KEY)
   ```
   

* Parameters description

   
   |Parameters |Description |
   |---|---|
   |KEY |Field or expression, value is of Timestamp type. |
   

* Return value description

   The return value is of BIGINT type.


<span id="8df88328"></span>
### Function example


* Scenarios

   Use the CURRENT_TIMESTAMP function to obtain the current date and time, then use the SECOND function to extract the second from the current time.

* Query and analysis statement

   ```SQL
   * | SELECT CURRENT_TIMESTAMP,SECOND(CURRENT_TIMESTAMP)
   ```
   

* Query and analysis result

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/4b7565179d3c4976890daa13ccd22cc4) </span>


<span id="70a6f2ad"></span>
## TIMEZONE_HOUR function

The TIMEZONE_HOUR function is used to calculate the hour offset of a time zone.

<span id="befbdeb0"></span>
### Function**syntax**


* Syntax format

   ```SQL
   TIMEZONE_HOUR(KEY)
   ```
   

* Parameters description

   
   |Parameters |Description |
   |---|---|
   |KEY |Field or expression, value is of Timestamp type. |
   

* Return value description

   The return value is of BIGINT type.


<span id="2df51c1e"></span>
### Function example


* Scenarios

   Use the CURRENT_TIMESTAMP function to obtain the current date and time, then use the TIMEZONE_HOUR function to calculate the hour offset of the current time zone.

* Query and analysis statements

   ```SQL
   * | SELECT CURRENT_TIMESTAMP, TIMEZONE_HOUR(CURRENT_TIMESTAMP)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/11df6f5a2ae841f18e68105e4afea3c0) </span>


<span id="54ebffd2"></span>
## TIMEZONE_MINUTE function

The TIMEZONE_MINUTE function is used to calculate the minute offset of a time zone.

<span id="2eed48bf"></span>
### Function **syntax**


* Syntax format

   ```SQL
   TIMEZONE_MINUTE(KEY)
   ```
   

* Parameters description

   
   |Parameters |Description |
   |---|---|
   |KEY |Field or expression, value is of Timestamp type. |
   

* Return value description

   The return value is of the Bigint type.


<span id="fc317ce7"></span>
### Function example


* Scenarios

   Use the CURRENT_TIMESTAMP function to obtain the current date and time, and then use the TIMEZONE_MINUTE function to calculate the minute offset of the time zone to which the current time belongs.

* Query and analysis statements

   ```SQL
   * | SELECT CURRENT_TIMESTAMP,TIMEZONE_MINUTE(CURRENT_TIMESTAMP)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/1d2e147338ef458ca6791ce04b261ba5) </span>


<span id="87965bba"></span>
## WEEK function

The WEEK function is used to calculate which week of the year the target date falls in. The WEEK function is equivalent to the WEEK_OF_YEAR function.

<span id="88f24b9a"></span>
### Function **syntax**


* Syntax format

   ```SQL
   WEEK(KEY)
   ```
   

* Parameters description

   
   |Parameters |Description |
   |---|---|
   |KEY |Field or expression, value is of Timestamp or Date type. |
   

* Return value description

   The return value is of the Bigint type.


<span id="a5db5073"></span>
### Function example


* Scenarios

   Use the CURRENT_TIMESTAMP function to obtain the current date and time, and then use the WEEK function to calculate which week of the year the current date falls in.

* Query and analysis statements

   ```SQL
   * | SELECT CURRENT_TIMESTAMP, WEEK(CURRENT_TIMESTAMP)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/65a9c6acad214ceba43e8354a4826ce9) </span>


<span id="12eeb06a"></span>
## WEEK_OF_YEAR function

The WEEK_OF_YEAR function is used to calculate which week of the year the target date falls in. The WEEK_OF_YEAR function is equivalent to the WEEK function.

<span id="17e6e171"></span>
### **Syntax format**


* Syntax format

   ```SQL
   WEEK_OF_YEAR(KEY)
   ```
   

* Parameters description

   
   |Parameters |Description |
   |---|---|
   |KEY |Field or expression, value is of Timestamp or Date type. |
   

* Return value description

   The return value is of the Bigint type.


<span id="2749dfc8"></span>
### Function example


* Scenarios

   Use the CURRENT_TIMESTAMP function to obtain the current date and time, and then use the WEEK_OF_YEAR function to calculate which week of the year the current date falls in.

* Query and analysis statements

   ```SQL
   * | SELECT CURRENT_TIMESTAMP, WEEK_OF_YEAR(CURRENT_TIMESTAMP)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/72d460e3adce4e8c9538ee1348fe6ecb) </span>


<span id="2240d512"></span>
## YEAR function

The YEAR function is used to extract the year from a date and time.

<span id="bbbdc1dd"></span>
### Function **syntax**


* Syntax format

   ```SQL
   YEAR(KEY)
   ```
   

* Parameters description

   
   |Parameters |Description |
   |---|---|
   |KEY |Field or expression, value is of Timestamp or Date type. |
   

* Return value description

   The return value is of the Bigint type.


<span id="59bb7a16"></span>
### Function example


* Scenarios

   Use the CURRENT_TIMESTAMP function to obtain the current date and time, and then use the YEAR function to extract the year from the current date.

* Query and analysis statements

   ```SQL
   * | SELECT CURRENT_TIMESTAMP,YEAR(CURRENT_TIMESTAMP)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/7957fdebd4904efab13b65ccea3798ff) </span>


<span id="67eb132a"></span>
## YEAR_OF_WEEK function

The YEAR_OF_WEEK function is used to return the year of the target date in the ISO week calendar. The YEAR_OF_WEEK function is equivalent to the YOW function.

<span id="876f29c4"></span>
### Function **syntax**


* Syntax format

   ```SQL
   YEAR_OF_WEEK(KEY)
   ```
   

* Parameters description

   
   |Parameters |Description |
   |---|---|
   |KEY |Field or expression, value is of Timestamp or Date type. |
   

* Return value description

   The return value is of the Bigint type.


<span id="e70e2f9d"></span>
### Function example


* Scenarios

   Use the CURRENT_TIMESTAMP function to obtain the current date and time, and then use the YEAR_OF_WEEK function to return the year of the current date in the ISO week calendar.

* Query and analysis statement

   ```SQL
   * | SELECT CURRENT_TIMESTAMP,YEAR_OF_WEEK(CURRENT_TIMESTAMP)
   ```
   

* Query and analysis result

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/7957fdebd4904efab13b65ccea3798ff) </span>


<span id="849be187"></span>
## YOW function

The YOW function returns the year of the target date in the ISO week calendar. The YOW function is equivalent to the YEAR_OF_WEEK function.

<span id="a8b64dd9"></span>
### Function **syntax**


* Syntax format

   ```SQL
   YOW(KEY)
   ```
   

* Parameters description

   
   |Parameters |Description |
   |---|---|
   |KEY |Field or expression, value is of Timestamp or Date type. |
   

* Return value description

   The return value is of Bigint type.


<span id="54c6f24d"></span>
### Function example


* Scenarios

   Use the CURRENT_TIMESTAMP function to obtain the current date and time, then use the YOW function to return the year of the current date in the ISO week calendar.

* Query and analysis statement

   ```SQL
   * | SELECT CURRENT_TIMESTAMP, YOW(CURRENT_TIMESTAMP)
   ```
   

* Query and analysis result

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/7957fdebd4904efab13b65ccea3798ff) </span>


<span id="fd1d74b9"></span>
## DATE_ADD function

The DATE_ADD function is used to add or subtract a specified time interval to a date and time.

<span id="8f811d5c"></span>
### Function **syntax**


* Syntax format

   ```SQL
   DATE_ADD(unit, n, KEY)
   ```
   

* Parameters description

   
   |Parameters |Description |
   |---|---|
   |unit |Time unit, possible values: millisecond, second, minute, hour, day, week, month, quarter, year.  |
   |n |Time interval. |
   |KEY |Field or expression, with a value of the Timestamp type. |
   

* Return value description

   The return value type is Timestamp.


<span id="ea038141"></span>
### Function example


* Scenarios

   Query the current timestamp, then subtract 1 to obtain the timestamp at the same time yesterday.

* Query and analysis statement

   ```SQL
   * | SELECT TO_UNIXTIME(DATE_ADD('DAY', -1, CURRENT_TIMESTAMP))
   ```
   

* Query and analysis result

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/8a564071dc0642e5a1c94d0c272dc9d9) </span>


<span id="f12bb917"></span>
## DATE_DIFF function

The DATE_DIFF function is used to calculate the difference between two dates or time points.

<span id="abc6393a"></span>
### Function **syntax**


* Syntax format

   ```SQL
   DATE_DIFF(unit, KEY1, KEY2)
   ```
   

* The parameters are described below:

   
   |Parameters |Description |
   |---|---|
   |unit |Time unit. Supported values are millisecond, second, minute, hour, day, week, month, quarter, year.  |
   |KEY |Field or expression, with a value of the Timestamp type. |
   

* Return value description

   The return value is of Bigint type.


<span id="a0fdc8af"></span>
### Function example


* Scenarios

   Convert the value of the `time` field to Timestamp type, then calculate the hour difference between it and the current time.

* Log example

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/85032e81787844138d857a982ec9e4f2) </span>

* Query and analysis statement

   ```SQL
   * | SELECT DATE_DIFF('hour', CAST(time AS TIMESTAMP), CURRENT_TIMESTAMP) AS "Time difference (hour)"
   ```
   

* Query and analysis result

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/20bccef22131415993339919dd8b58a3) </span>


<span id="d1f8ea12"></span>
## DATE_TRUNC function

The DATE_TRUNC function truncates a date or time according to the specified time unit, aligning it to milliseconds, seconds, minutes, hours, days, months, or years. Supported UNIX timestamps for parsing are at the second or millisecond level.

<span id="bc3e6102"></span>
### Function syntax


* Syntax format

   ```SQL
   DATE_TRUNC(unit, KEY)
   ```
   

   Parameters description

   
   |Parameters |Description |
   |---|---|
   |unit |Time unit. Supported values are millisecond, second, minute, hour, day, week, month, quarter, year.  |
   |KEY |Field or expression, with a value of a UNIX timestamp in seconds or milliseconds. |
   


<span id="e610833c"></span>
### Function example


* Scenarios

   Aggregate data by minute dimension based on the `apply_time` field.

* Log example

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/c1d510125a844a4fbfc059618fbc672f) </span>

* Query and analysis statement

   ```SQL
   * | SELECT DATE_TRUNC('minute', apply_time) AS time GROUP BY time
   ```
   

* Query and analysis result

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/5d436cc732d843bdb6359179ac7be3d3) </span>


<span id="6ba081bf"></span>
## DATE_TRUNC_SEC function

The DATE_TRUNC_SEC function truncates a date or time according to the specified time unit, aligning it to milliseconds, seconds, minutes, hours, days, months, or years. Supported UNIX timestamps for parsing are at the second level.

<span id="3e13e5fd"></span>
### Function syntax


* Syntax format

   ```SQL
   DATE_TRUNC_SEC(unit, KEY)
   ```
   

   Parameters description

   
   |Parameters |Description |
   |---|---|
   |unit |Time unit. Supported values are millisecond, second, minute, hour, day, week, month, quarter, year.  |
   |KEY |Field or expression, with a value of a UNIX timestamp in seconds. |
   


<span id="621e33bd"></span>
### Function example


* Scenarios

   Aggregate data by minute dimension based on the `sli_time` field.

* Log example

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/c395ee97ee264fc0b22e73f0a87788d6) </span>

* Query and analysis statements

   ```SQL
   * | SELECT DATE_TRUNC_SEC('minute', sli_time) AS time GROUP BY time
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/315ea90bd3544c5f90fd4b6742618706) </span>


<span id="691f29e7"></span>
## TIME_SERIES function

The TIME_SERIES function is used to fill in missing data within the query time window.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div>


<div data-tips="true" data-tips-type="default">The TIME_SERIES function groups, aggregates, and analyzes log data based on a fixed time interval. It must be used with the GROUP BY and ORDER BY clauses, and ORDER BY does not support descending (DESC) sorting.</div>


<span id="a54d8a47"></span>
### Function syntax


* Syntax format

   ```SQL
   TIME_SERIES(KEY, window_time, format, padding_data)
   ```
   

* Parameters description

   
   |Parameters |Description |
   |---|---|
   |KEY |The field representing time, for example `__time__`. The value of this field should be a LONG\-type UNIX timestamp (milliseconds). |
   |window_time |Window size, that is, the time interval. Units are s (second), m (minute), h (hour), d (day). For example, 10h means 10 hours, 5d means 5 days. |
   |format |The time format of the returned result. Detailed information is shown in the following table. |
   |padding_data |Content used for padding. Supported settings include:<br><br><br>* 0: Set all missing field values to 0.<br><br>* null: Set all missing field values to null.<br><br>* last: Set missing field values to the value at the previous time point.<br><br>* next: Set missing field values to the value at the next time point.<br><br>* avg: Set missing field values to the average of the values at the previous and next time points. |
   

* Format description

   
   |format |Description |
   |---|---|
   |%a |Abbreviation of the weekday name in English. For example, Sun, Sat. |
   |%b |Abbreviation of the month name in English. For example, Jan, Dec. |
   |%c |Month. Value range: 1 ~ 12. |
   |%D |The day of the month, with a suffix, for example 0th, 1st, 2nd, 3rd. |
   |%d |The day of the month in decimal format. Value range: 01 ~ 31. |
   |%e |The day of the month in decimal format. Value range: 1 ~ 31. |
   |%H |Hour, 24\-hour format. |
   |%h |Hour, 12\-hour format. |
   |%i |Minute. Value range: 00 ~ 59. |
   |%j |The day of the year. Value range: 001 ~ 366. |
   |%k |Hour. Value range: 0 ~ 23. |
   |%l |Hour. Value range: 1 ~ 12. |
   |%M |Month name in English, for example January, December. |
   |%m |Month in numeric format. Value range: 01 ~ 12. |
   |%p |AM, PM. |
   |%r |Time in 12\-hour format, in the format `hh:mm:ss AM/PM`. |
   |%S |Second. Value range: 00 ~ 59. |
   |%s |Second. Value range: 00 ~ 59. |
   |%f |Milliseconds, range: 000–999. |
   |%T |Time, 24\-hour format, in the format `hh:mm:ss`. |
   |%v |Week number of the year, with Monday as the first day of the week, range: 01–53. |
   |%W |English name of the day of the week. For example, Sunday, Saturday. |
   |%Y |Four\-digit year. For example, 2024. |
   |%y |Two\-digit year. For example, 24. |
   |%% |Escape character for %. |
   

* Return value description

   The return value is of Varchar type.


<span id="495560ad"></span>
### Function example


* Scenarios 1: Single\-field grouping and sorting

   Complete the missing data based on an hourly granularity, setting all missing values to 0.

* Log example

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/4e85a6b1520b43a1a3eb737905f214b2) </span>

* Query and analysis statements

   ```SQL
   * | SELECT TIME_SERIES(sli_time, '1h', '%Y-%m-%d %H:%i:%s', '0') AS time, COUNT(*) AS num GROUP BY time ORDER BY time
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/6a9d0876d6964e2996eb1abfa59c8f1d) </span>

* Scenarios 2: Multi\-field grouping and sorting

   Complete the data that is grouped by level based on a 30\-second granularity and uniformly set missing values to 0.

* Query and analysis statements

   ```SQL
   * | SELECT level, TIME_SERIES(__time__, '30s', '%Y-%m-%d %H:%i:%s', '0') AS time, COUNT(*) AS cnt GROUP BY level, time ORDER BY level, time
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/e73e57ddef0d4ea5812b704dc0cf57a2) </span>


<span id="3ad17aea"></span>
## Unit description


|unit |Description |
|---|---|
|millisecond |Millisecond |
|second |Second |
|minute |Minute |
|hour |Hour |
|day |Day |
|week |Week |
|month |Month |
|quarter |Quarter |
|year |Year |
