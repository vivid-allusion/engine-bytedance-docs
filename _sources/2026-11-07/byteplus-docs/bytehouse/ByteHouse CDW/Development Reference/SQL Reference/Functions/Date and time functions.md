---
title: "Date and time functions"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-date-times"
---

<span id="c277ff91"></span>
### addDate

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


`Add Date` returns the date after adding the specified time.

**Syntax**

```SQL
adddate(date, INTERVAL expr unit)
adddate(expr, days)
```


**Parameter Type**


* `date`

   * Date or date\-time expression to which time is added

   * Date/Date32/Datetime/Datetime64

   * String

* `INTERVAL expr unit`

   * Added time interval and unit

   * The unit can be: second, minute, hour, day, month, year, minute_second, hour_second, hour_minute, day_second, day_minute, day_hour, year_month

   * String

* `expr`

   * Added time interval

   * String

   * Int64

* `days`

   * Added days

   * String

   * Int64


**Return Type**

Date

**Example**

**Example 1:** 

```SQL
SELECT adddate(date '2024-07-21', INTERVAL '3' day) as result;
```


```Plain
┌─────result─┐
│ 2024-07-24 │
└────────────┘
```


**Example 2:** 

```SQL
SELECT adddate(datetime '2024-07-21', INTERVAL '3' day) as result;
```


```Plain
┌──────────────result─┐
│ 2024-07-24 00:00:00 │
└─────────────────────┘
```


**Example 3:** 

```SQL
SELECT adddate('2024-07-21', INTERVAL '3' day) as result;
```


```Plain
┌──────────────────result─┐
│ 2024-07-24 00:00:00.000 │
└─────────────────────────┘
```


**Example 4:** 

```SQL
SELECT adddate(datetime '2024-07-21', INTERVAL '3' second) as result;
```


```Plain
┌──────────────result─┐
│ 2024-07-21 00:00:03 │
└─────────────────────┘
```


**Example 5:** 

```SQL
SELECT adddate(datetime '2024-07-21', INTERVAL '3' minute) as result;
```


```Plain
┌──────────────result─┐
│ 2024-07-21 00:03:00 │
└─────────────────────┘
```


**Example 6:** 

```SQL
SELECT adddate(datetime '2024-07-21', INTERVAL '3' hour) as result;
```


```Plain
┌──────────────result─┐
│ 2024-07-21 03:00:00 │
└─────────────────────┘
```


**Example 7:** 

```SQL
SELECT adddate(datetime '2024-07-21', INTERVAL '3' month) as result;
```


```Plain
┌──────────────result─┐
│ 2024-10-21 00:00:00 │
└─────────────────────┘
```


**Example 8:** 

```SQL
SELECT adddate(datetime '2024-07-21', INTERVAL '3' year) as result;
```


```Plain
┌──────────────result─┐
│ 2027-07-21 00:00:00 │
└─────────────────────┘
```


**Example 9:** 

```SQL
SELECT adddate(datetime '2024-07-21', INTERVAL '01:01:10' hour_second) AS result;
```


```Plain
┌──────────────result─┐
│ 2024-07-21 01:01:10 │
└─────────────────────┘
```


**Example 10:** 

```SQL
SELECT adddate(datetime '2024-07-21', INTERVAL '00:10' hour_minute) AS result;
```


```Plain
┌──────────────result─┐
│ 2024-07-21 00:10:00 │
└─────────────────────┘
```


**Example 11:** 

```SQL
SELECT adddate(datetime '2024-07-21', INTERVAL '1 01:01:10' day_second) AS result;
```


```Plain
┌──────────────result─┐
│ 2024-07-22 01:01:10 │
└─────────────────────┘
```


**Example 12:** 

```SQL
SELECT adddate(datetime '2024-07-21', INTERVAL '01:10' minute_second) AS result;
```


```Plain
┌──────────────result─┐
│ 2024-07-21 00:01:10 │
└─────────────────────┘
```


**Example 13:** 

```SQL
SELECT adddate(datetime '2024-07-21', INTERVAL '1 01:01' day_minute) AS result;
```


```Plain
┌──────────────result─┐
│ 2024-07-22 01:01:00 │
└─────────────────────┘
```


**Example 14:** 

```SQL
SELECT adddate(datetime '2024-07-21', INTERVAL '1 01' day_hour) AS result;
```


```Plain
┌──────────────result─┐
│ 2024-07-22 01:00:00 │
└─────────────────────┘
```


**Example 15:** 

```SQL
SELECT adddate(datetime '2024-07-21 12:13:14', INTERVAL '2 2' year_month) AS result;
```


```Plain
┌──────────────result─┐
│ 2026-09-21 12:13:14 │
└─────────────────────┘
```


**Example 16:** 

```SQL
SELECT adddate('2024-07-21', '3');
```


```Plain
┌─addDays('2024-07-21', '3')─┐
│    2024-07-24 00:00:00.000 │
└────────────────────────────┘
```


**Example 17:** 

```SQL
SELECT adddate('2024-07-21', 3);
```


```Plain
┌─addDays('2024-07-21', 3)─┐
│  2024-07-24 00:00:00.000 │
└──────────────────────────┘
```


**Example 18:** 

```SQL
SELECT adddate(datetime '2024-07-21 12:13:14', 3);
```


```Plain
┌─addDays(toDateTime('2024-07-21 12:13:14'), 3)─┐
│                           2024-07-24 12:13:14 │
└───────────────────────────────────────────────┘
```


**Example 19:** 

```SQL
SELECT adddate(datetime '2024-07-21 12:13:14', '3');
```


```Plain
┌─addDays(toDateTime('2024-07-21 12:13:14'), '3')─┐
│                             2024-07-24 12:13:14 │
└─────────────────────────────────────────────────┘
```


**Example 20:** 

```SQL
SELECT adddate('2024-07-21 12:13:14', 3);
```


```Plain
┌─addDays('2024-07-21 12:13:14', 3)─┐
│           2024-07-24 12:13:14.000 │
└───────────────────────────────────┘
```


**Example 21:** 

```SQL
SELECT adddate('2024-07-21 12:13:14', '3');
```


```Plain
┌─addDays('2024-07-21 12:13:14', '3')─┐
│             2024-07-24 12:13:14.000 │
└─────────────────────────────────────┘
```


<span id="9b57ebe6"></span>
### addDays

The function adds a date/date\-time interval to a date/date\-time, then returns the date/date\-time.

**Syntax**

```SQL
addDays(date, interval)
addDays(datetime, interval)
```


**Parameters**


* `Date/DateTime` Date/DateTime

* `interval` date/date\-time


**Return value**


* Date/date\-time


**Example**

```SQL
WITH
    toDate('2018-01-01') AS date,
    toDateTime('2018-01-01 00:00:00') AS date_time
SELECT
    addDays(date, 1) AS add_days_with_date,
    addDays(date_time, 1) AS add_days_with_date_time
```


```Plain
┌─add_days_with_date─┬─add_days_with_date_time─┐
│ 2018-01-02         │ 2018-01-02 00:00:00     │
└────────────────────┴─────────────────────────┘
```


<span id="1038f586"></span>
### addHours

The function adds a date/date\-time interval to a date/date\-time, then returns the date/date\-time.

**Syntax**

```SQL
addHours(date, interval)
addHours(datetime, interval)
```


**Parameters**


* `date/datetime` date/date\-time

* `interval` date/date\-time


**Return Value**


* Date/DateTime


**Example**

```SQL
WITH
    toDate('2018-01-01') AS date,
    toDateTime('2018-01-01 00:00:00') AS date_time
SELECT
    addHours(date, 1) AS add_hours_with_date,
    addHours(date_time, 1) AS add_hours_with_date_time
```


```Plain
┌─add_hours_with_date─┬─add_hours_with_date_time─┐
│ 2018-01-01 01:00:00 │ 2018-01-01 01:00:00      │
└─────────────────────┴──────────────────────────┘
```


<span id="b5d6f6c9"></span>
### addMinutes

The function adds a date/datetime interval to a date/datetime and then returns the date/datetime.

**Syntax**

```SQL
addMinutes(date, interval)
addMinutes(datetime, interval)
```


**Parameters**


* `date/datetime` Date/DateTime

* `interval` Date/DateTime


**Return Value**


* Date/Date\-Time


**Example**

```SQL
WITH
    toDate('2018-01-01') AS date,
    toDateTime('2018-01-01 00:00:00') AS date_time
SELECT
    addMinutes(date, 1) AS add_minutes_with_date,
    addMinutes(date_time, 1) AS add_minutes_with_date_time
```


```Plain
┌─add_minutes_with_date─┬─add_minutes_with_date_time─┐
│ 2018-01-01 00:01:00   │ 2018-01-01 00:01:00        │
└───────────────────────┴────────────────────────────┘
```


<span id="5f6bc82d"></span>
### addMonths

The function adds a date/date\-time interval to a date/date\-time and then returns the date/date\-time. For example:

**Syntax**

```SQL
addMonths(date, interval)
addMonths(datetime, interval)
```


**Parameters**


* `Date/Date-Time` Date/Date\-Time

* `Interval` Date/Date\-Time


**Return Value**


* Date/Date\-Time


**Example**

```SQL
WITH
    toDate('2018-01-01') AS date,
    toDateTime('2018-01-01 00:00:00') AS date_time
SELECT
    addMonths(date, 1) AS add_months_with_date,
    addMonths(date_time, 1) AS add_months_with_date_time
```


```Plain
┌─add_months_with_date─┬─add_months_with_date_time─┐
│ 2018-02-01           │ 2018-02-01 00:00:00       │
└──────────────────────┴───────────────────────────┘
```


<span id="e25ddec7"></span>
### addQuarters

The function adds a date/date\-time interval to a date/date\-time, then returns the date/date\-time.

**Syntax**

```SQL
addQuarters(date, interval)
addQuarters(datetime, interval)
```


**Parameters**


* `Date/Datetime` Date/Date\-Time

* `Interval` Date/Date\-Time


**Return Value**


* Date/Date\-Time


**Example**

```SQL
WITH
    toDate('2018-01-01') AS date,
    toDateTime('2018-01-01 00:00:00') AS date_time
SELECT
    addQuarters(date, 1) AS add_quarters_with_date,
    addQuarters(date_time, 1) AS add_quarters_with_date_time
```


```Plain
┌─add_quarters_with_date─┬─add_quarters_with_date_time─┐
│ 2018-04-01             │ 2018-04-01 00:00:00         │
└────────────────────────┴─────────────────────────────┘
```


<span id="678b549d"></span>
### addSeconds

The function adds a date/date\-time interval to a date/date\-time and then returns the date/date\-time. For example:

**Syntax**

```SQL
addSeconds(date, interval)
addSeconds(datetime, interval)
```


**Parameters**


* `date/datetime` Date/Date\-Time

* `interval` Date/Date\-Time


**Return Value**


* Date/Date\-Time


**Example**

```SQL
WITH
    toDate('2018-01-01') AS date,
    toDateTime('2018-01-01 00:00:00') AS date_time
SELECT
    addSeconds(date, 1) AS add_seconds_with_date,
    addSeconds(date_time, 1) AS add_seconds_with_date_time
```


```Plain
┌─add_seconds_with_date─┬─add_seconds_with_date_time─┐
│ 2018-01-01 00:00:01   │ 2018-01-01 00:00:01        │
└───────────────────────┴────────────────────────────┘
```


<span id="ef213974"></span>
### addWeeks

The function adds weeks to a date/datetime interval and then returns the date/datetime.

**Syntax**

```SQL
addWeeks(date, interval)
addWeeks(datetime, interval)
```


**Parameters**


* `Date/datetime` Date/datetime

* `Interval` Date/datetime


**Return Value**


* Date/datetime


**Example**

```SQL
WITH
    toDate('2018-01-01') AS date,
    toDateTime('2018-01-01 00:00:00') AS date_time
SELECT
    addWeeks(date, 1) AS add_weeks_with_date,
    addWeeks(date_time, 1) AS add_weeks_with_date_time
```


```Plain
┌─add_weeks_with_date─┬─add_weeks_with_date_time─┐
│ 2018-01-08          │ 2018-01-08 00:00:00      │
└─────────────────────┴──────────────────────────┘
```


<span id="ee6f54a5"></span>
### addYears

The function adds a year or datetime interval to a date or datetime and then returns the date or datetime. For example:

**Syntax**

```SQL
addYears(date, interval)
addYears(datetime, interval)
```


**Parameters**


* `Date/datetime` \- Date or datetime

* `Interval` \- Date or datetime interval


**Return Value**


* Date or datetime


**Example**

```SQL
WITH
    toDate('2018-01-01') AS date,
    toDateTime('2018-01-01 00:00:00') AS date_time
SELECT
    addYears(date, 1) AS add_years_with_date,
    addYears(date_time, 1) AS add_years_with_date_time
```


```Plain
┌─add_years_with_date─┬─add_years_with_date_time─┐
│ 2019-01-01          │ 2019-01-01 00:00:00      │
└─────────────────────┴──────────────────────────┘
```


<span id="ddd9e071"></span>
### addTime

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


`Addtime` returns the time after adding specified time, that is, the result of `expr1` plus `expr2`.

Syntax

```SQL
addtime(expr1, expr2)
```


**Parameter Types**


* `expr1` Base Time

   * Date/Date32

   * Datetime/Datetime64

   * Time

   * String

* `expr2` Increment Time

   * Time

   * String


**Return Type**


* String


**Example**

**Example 1:** 

```SQL
SELECT addtime(DATE '2023-07-15', '02:30:30');
```


```Plain
┌─addtime(toDate('2023-07-15'), '02:30:30')─┐
│                   2023-07-15 02:30:30.000 │
└───────────────────────────────────────────┘
```


**Example 2:** 

```SQL
SELECT addtime(TIME '12:00:00', '02:30:30');
```


```Plain
┌─addtime(toTimeType('12:00:00'), '02:30:30')─┐
│                                14:30:30.000 │
└─────────────────────────────────────────────┘
```


**Example 3:** 

```SQL
SELECT addtime(DATETIME '2023-07-15 14:00:00', '02:30:30');
```


```Plain

┌─addtime(toDateTime('2023-07-15 14:00:00'), '02:30:30')─┐
│                                2023-07-15 16:30:30.000 │
└────────────────────────────────────────────────────────┘
```


**Example 4:** 

```SQL
SELECT addtime(TIMESTAMP '2023-07-15 14:00:00', Time'02:30:30');
```


```Plain
┌─addtime(toDateTime('2023-07-15 14:00:00'), '02:30:30')─┐
│                                2023-07-15 16:30:30.000 │
└────────────────────────────────────────────────────────┘
```


**Example 5:** 

```SQL
SELECT addtime('2023-07-15 14:00:00', '02:30:30');
```


```Plain
┌─addtime('2023-07-15 14:00:00', '02:30:30')─┐
│                    2023-07-15 16:30:30.000 │
└────────────────────────────────────────────┘
```


<span id="8b26cbf0"></span>
### convert_tz

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


`convert_tz` function is used to convert the date and time value from one time zone to another and returns the result.

**Syntax**

```SQL
convert_tz(expr, from_tz, to_tz)
```


**Parameters**


* `expr`

   * The date and time value to be converted

   * Datetime

* `from_tz`

   * The original time zone of the date and time value.

* `to_tz`

   * Target Time Zone to Convert To.


**Return Type**


* Datetime


**Example**

**Example 1:** 

```SQL
SELECT convert_tz('2023-06-15 09:30:00', '+00:00', '+08:00');
```


```Plain
┌─convert_tz('2023-06-15 09:30:00', '+00:00', '+08:00')─┐
│                                   2023-06-15 17:30:00 │
└───────────────────────────────────────────────────────┘
```


**Example 2:** 

```SQL
SELECT convert_tz('2023-12-25 18:45:00', 'UTC', 'CET');
```


```Plain
┌─convert_tz('2023-12-25 18:45:00', 'UTC', 'CET')─┐
│                             2023-12-25 19:45:00 │
└─────────────────────────────────────────────────┘
```


<span id="47e3d251"></span>
### curdate

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


`curdate` function returns the current date. Same as today()

**Syntax**

```SQL
curdate()
```


**Return Type**


* Date


**Example**

```SQL
SELECT curdate();
```


```Plain
┌────today()─┐
│ 2024-07-25 │
└────────────┘
```


<span id="835cf61e"></span>
### curtime

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


`curtime` function returns the current time.

**Syntax**

```SQL
curtime()
```


**Return Type**


* Time


**Example**

```SQL
SELECT curtime();
```


```Plain
┌────CURTIME()─┐
│ 16:39:50.844 │
└──────────────┘
```


<span id="9a4f5b4a"></span>
### date

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


`Date` returns the date from a date or datetime expression.

**Syntax**

```SQL
DATE(expr)
```


**Parameter types**


* `expr`

   * Date/Date32

   * Datetime/Datetime64

   * String


**Return type**


* Date


**Example**

**Example 1:** 

```SQL
SELECT DATE('2023-06-15 08:45:30'::Datetime);
```


```Plain
┌─DATE(CAST('2023-06-15 08:45:30', 'Datetime'))─┐
│                                    2023-06-15 │
└───────────────────────────────────────────────┘
```


**Example 2:** 

```SQL
SELECT DATE('2023-06-15 08:45:30'::Date);
```


```Plain
┌─DATE(CAST('2023-06-15 08:45:30', 'Date'))─┐
│                                2023-06-15 │
└───────────────────────────────────────────┘
```


**Example 3:** 

```SQL
SELECT DATE('2023-06-15 08:45:30');
```


```Plain
┌─DATE('2023-06-15 08:45:30')─┐
│                  2023-06-15 │
└─────────────────────────────┘
```


<span id="9f3c7773"></span>
### dateDiff

Returns the difference between two dates or dates with time values.

**Syntax**

```SQL
dateDiff('unit', startdate, enddate, [timezone])
```


**Parameters**


* `Unit`— Type of interval for the result. String. Possible values:

   * second

   * minute

   * hour

   * day

   * week

   * month

   * quarter

   * year

* `startdate`— The first time value to subtract (minuend). Date or datetime.

* `enddate`— The second time value to be subtracted (the minuend). Date or datetime.

* `timezone`— Optional timezone name. If specified, it applies to both the start date and the end date. If not specified, the timezone of the start date and end date is used. If they are different, the result is unspecified. String.


**Example**

```SQL
SELECT dateDiff('hour', toDateTime('2018-01-01 22:00:00'), toDateTime('2018-01-02 23:00:00'));
```


```Plain
┌─dateDiff('hour', toDateTime('2018-01-01 22:00:00'), toDateTime('2018-01-02 23:00:00'))─┐
│ 25                                                                                     │
└────────────────────────────────────────────────────────────────────────────────────────┘
```


<span id="31df9730"></span>
### date_format

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


Same as formatDateTime()

<span id="1f847958"></span>
### date_add

Adds a time interval or date interval to the provided date or datetime.

**Syntax**

```SQL
date_add(date, value)
date_add(datetime, value [,timezone])
```


**Parameters**


* `datevalue` — The date or datetime to which time is added. Date or datetime.

* `timezone` The timezone parameter is allowed only when the first argument is of DateTime type.


**Return Value**

The date or datetime obtained by adding `value`.

Type: Date or datetime.

**Example**

```SQL
SELECT date_add(toDate('2018-01-01'),3);
```


```Plain
┌─date_add(toDate('2018-01-01'), 3)─┐
│ 2018-01-04                        │
└───────────────────────────────────┘
```


```SQL
SELECT date_add(toDateTime('2018-01-01 00:00:00'), 3, 'UTC');
```


```Plain
┌─date_add(toDateTime('2018-01-01 00:00:00'), 3, 'UTC')─┐
│ 2018-01-03 16:00:00                                   │
└───────────────────────────────────────────────────────┘
```


<span id="5d51e5b1"></span>
### dateTrunc

Truncates a date and time value to the specified part of the date.

**Syntax**

```SQL
dateTrunc(unit, datetime[, timezone])
```


**Aliases**: `DATE_TRUNC`

**Arguments**


* `unit` — The type of interval to truncate the result. `unit` argument is case\-insensitive. `String`.The compatibility for different units is described as follows:

   
   |Unit |Compatibility |
   |---|---|
   |`nanosecond` |Compatible only with DateTime64 |
   |`microsecond` |Compatible only with DateTime64 |
   |`millisecond` |Compatible only with DateTime64 |
   |`second` |Compatible with DateTime64 and DateTime |
   |`minute` |Compatible with DateTime64 and DateTime |
   |`hour` |Compatible with DateTime64 and DateTime |
   |`day` |Compatible with DateTime64, DateTime and Date |
   |`week` |Compatible with DateTime64, DateTime and Date |
   |`month` |Compatible with DateTime64, DateTime and Date |
   |`quarter` |Compatible with DateTime64, DateTime and Date |
   |`year` |Compatible with DateTime64, DateTime and Date |
   

* `datetime` — Date and time. `Date` or `Date32` or `DateTime` or `DateTime64`.

* `timezone` — Optional. Timezone name for the returned datetime. If not specified, the function uses the timezone of the `datetime` parameter. `String`.


**Returned value**

Returns the truncated date and time value.


|Unit Argument |`datetime` Argument |Return Type |
|---|---|---|
|Year, Quarter, Month, Week |`Date32` or `DateTime64` or `Date` or `DateTime` |`Date32` or `Date` |
|Day, Hour, Minute, Second |`Date32`, `DateTime64`, `Date`, or `DateTime` |`DateTime64` or `DateTime` |
|Millisecond, Microsecond, |Any |`DateTime64` |
|Nanosecond | |with scale 3, 6, or 9 |


**Examples**

**Truncate without timezone**

Query:

```SQL
SELECT now(), dateTrunc('hour', now());
```


Response:

```SQL
┌───────────────now()─┬─dateTrunc('hour', now())──┐
│ 2020-09-28 10:40:45 │       2020-09-28 10:00:00 │
└─────────────────────┴───────────────────────────┘
```


**Truncate with specified timezone**

Query:

```SQL
SELECT now(), dateTrunc('hour', now(), 'Asia/Istanbul');
```


Response:

```SQL
┌───────────────now()─┬─dateTrunc('hour', now(), 'Asia/Istanbul')──┐
│ 2020-09-28 10:46:26 │                        2020-09-28 13:00:00 │
└─────────────────────┴────────────────────────────────────────────┘
```


<span id="bf68cd65"></span>
### date_sub

Subtract a time interval or date interval from the provided date or datetime.

**Syntax**

```SQL
date_sub(date, value)
date_sub(datetime, value [,timezone])
```


**Parameters**


* `datevalue` — The date or datetime to add time to. Date or datetime.

* `timezone` is allowed only when the first parameter is of DateTime type.


**Return value**

Date or datetime obtained by subtracting `value`.

Type: Date or date\-time.

**Example**

```SQL
SELECT date_sub(toDate('2018-01-01'),3);
```


```Plain
┌─date_sub(toDate('2018-01-01'), 3)─┐
│ 2017-12-29                        │
└───────────────────────────────────┘
```


```SQL
SELECT date_sub(toDateTime('2018-01-01 00:00:00'), 3, 'UTC');
```


```Plain
┌─date_sub(toDateTime('2018-01-01 00:00:00'), 3, 'UTC')─┐
│ 2017-12-28 16:00:00                                   │
└───────────────────────────────────────────────────────┘
```


<span id="8835f20b"></span>
### day/dayOfMonth

Returns the day in the date.

**Syntax**

```SQL
DAY(expr)
DAYOFMONTH(expr)
```


**Parameter type**


* `expr`

   * Date/Date32

   * Datetime/Datetime64

   * Time

   * String


**Return type**


* `UInt8`


**Example**

**Example 1:** 

```SQL
SELECT DAYOFMONTH('2022-01-22 12:23:09');
```


```Plain
┌─DAYOFMONTH('2022-01-22 12:23:09')─┐
│                                22 │
└───────────────────────────────────┘
```


**Example 2:** 

```SQL
SELECT DAYOFMONTH(TIME '17:01:10');
```


```SQL
-- use current date
┌─DAYOFMONTH(toTimeType('17:01:10'))─┐
│                                 25 │
└────────────────────────────────────┘
```


**Example 3:** 

```SQL
SELECT DAY('2022-01-22');
```


```Plain
┌─DAY('2022-01-22')─┐
│                22 │
└───────────────────┘
```


<span id="de0735d2"></span>
### **dayname**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


`Dayname` returns the name of the weekday corresponding to the date.

**Syntax**

```SQL
dayname(expr)
```


**Parameter Type**


* `expr`

   * Datetime/Datetime64

   * Date/Date32

   * String


**Return Type**


* String


**Example**

**Example 1:** 

```SQL
SELECT dayname(DATETIME '2023-04-21 03:01:00');
```


```Plain
┌─dayname(toDateTime('2023-04-21 03:01:00'))─┐
│ Friday                                     │
└────────────────────────────────────────────┘
```


**Example 2:** 

```SQL
SELECT dayname('2023-04-21 03:01:00');
```


```Plain
┌─dayname('2023-04-21 03:01:00')─┐
│ Friday                         │
└────────────────────────────────┘
```


<span id="c22885d1"></span>
### **dayOfWeek**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


`dayofweek` returns the day of the week index corresponding to the date, with Sunday as 1, as the start.

**Syntax**

```SQL
dayofweek(expr)
```


Parameter Types


* `expr`

   * Datetime/Datetime64

   * Date/Date32

   * String


**Return Type**


* UInt8


**Example**

**Example 1:** 

```SQL
SELECT dayofweek(DATETIME '2024-04-10 20:30:00');
```


```Plain
┌─DAYOFWEEK(toDateTime('2024-04-10 20:30:00'))─┐
│                                            4 │
└──────────────────────────────────────────────┘
```


**Example 2:** 

```SQL
SELECT dayofweek(DATE '2022-01-30');
```


```Plain
┌─DAYOFWEEK(toDate('2024-01-30'))─┐
│                               3 │
└─────────────────────────────────┘
```


**Example 3:** 

```SQL
SELECT dayofweek('2024-10-21');
```


```Plain
┌─DAYOFWEEK('2024-10-21')─┐
│                       2 │
└─────────────────────────┘
```


**dayOfYear**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


`dayofyear` returns the day number of the specified date in the current year, ranging from [1, 366].

**Syntax**

```SQL
dayofyear(expr)
```


**Type**


* `expr`

   * Datetime/Datetime64

   * Date/Date32

   * String


**Return Type**


* UInt64


**Example**

**Example 1:** 

```SQL
SELECT dayofyear(DATETIME '2024-07-21 13:13:13');
```


```Plain
┌─DAYOFYEAR(toDateTime('2024-07-21 13:13:13'))─┐
│                                          203 │
└──────────────────────────────────────────────┘
```


**Example 2:** 

```SQL
SELECT dayofyear('2024-07-21');
```


```Plain
┌─DAYOFYEAR('2024-07-21')─┐
│                     203 │
└─────────────────────────┘
```


<span id="32addd2b"></span>
### extract

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


`extract` returns a specific part of the date or time, such as year, month, day, hour, minute(s), as specified by `unit`.

**Syntax**

```SQL
extract(unit FROM date)
```


**Type of Parameters**


* `unit`

   * Time Unit

   * `Unit` values can be: second, minute, hour, day, month, year, minute_second, hour_second, hour_minute, day_second, day_minute, day_hour, year_month.

* `date`

   * Expression of the date or time part to be extracted

   * Date/Date32/Datetime/Datetime64/Time

   * String


**Return Type**


* Int64


**Example**

**Example 1:** 

```SQL
SELECT extract(second FROM '2024-07-21 12:13:14') as result;
```


```Plain
┌─result─┐
│     14 │
└────────┘
```


**Example 2:** 

```SQL
SELECT extract(minute FROM '2024-07-21 12:13:14') as result;
```


```Plain
┌─result─┐
│     13 │
└────────┘
```


**Example 3:** 

```SQL
SELECT extract(hour FROM '2024-07-21 12:13:14') as result;
```


```Plain
┌─result─┐
│     12 │
└────────┘
```


**Example 4:** 

```SQL
SELECT extract(day FROM '2024-07-21 12:13:14') as result;
```


```Plain
┌─result─┐
│     21 │
└────────┘
```


**Example 5:** 

```SQL
SELECT extract(month FROM '2024-07-21 12:13:14') as result;
```


```Plain
┌─result─┐
│      7 │
└────────┘
```


**Example 6:** 

```SQL
SELECT extract(year FROM timestamp '2024-07-21') as result;
```


```Plain
┌─result─┐
│   2024 │
└────────┘
```


**Example 7:** 

```SQL
SELECT extract(year FROM datetime '2024-07-21') as result;
```


```Plain
┌─result─┐
│   2024 │
└────────┘
```


**Example 8:** 

```SQL
SELECT extract(year FROM time '12:13:14') as result;
```


```Plain
┌─result─┐
│   2024 │
└────────┘
```


**Example 9:** 

```SQL
SELECT extract(minute_second FROM '2024-07-21 12:13:14') as result;
```


```Plain
┌─result─┐
│   1314 │
└────────┘
```


**Example 10:** 

```SQL
SELECT extract(hour_second FROM '2024-07-21 12:13:14') as result;
```


```Plain
┌─result─┐
│ 121314 │
└────────┘
```


**Example 11:** 

```SQL
SELECT extract(hour_minute FROM '2024-07-21 12:13:14') as result;
```


```Plain
┌─result─┐
│   1213 │
└────────┘
```


**Example 12:** 

```SQL
SELECT extract(day_second FROM '2024-07-21 12:13:14') as result;
```


```Plain
┌───result─┐
│ 21121314 │
└──────────┘
```


**Example 13:** 

```SQL
sql
Copy code
SELECT extract(day_minute FROM '2024-07-21 12:13:14') as result;
```


```Plain
┌─result─┐
│ 211213 │
└────────┘
```


**Example 14:** 

```SQL
SELECT extract(day_hour FROM '2024-07-21 12:13:14') as result;
```


```Plain
┌─result─┐
│   2112 │
└────────┘
```


**Example 15:** 

```SQL
SELECT extract(year_month FROM '2024-07-21 12:13:14') as result;
```


```Plain
┌─result─┐
│ 202407 │
└────────┘
```


<span id="ea21a22a"></span>
### from_days

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


`from_days` returns the corresponding Date value according to the specified number of days, expr.

**Format**

```SQL
expr
```


**Type**


* `expr`

   * String

   * UInt/Int


**Return type**


* DATE


**Example**

**Example 1:** 

```SQL
SELECT from_days(739453);
```


```Plain
┌─from_days(739453)─┐
│        2024-07-21 │
└───────────────────┘
```


**Example 2:** 

```SQL
SELECT from_days('739453');
```


```Plain
┌─from_days(739453)─┐
│        2024-07-21 │
└───────────────────┘
```


**from_unixtime**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


`from_unixtime` returns a value in the specified format according to the Unix timestamp. The format follows the layout specified in the `date_format` function.

**Syntax**

```SQL
from_unixtime(expr[, format])
```


**Parameter Type**


* `expr`

   * String

   * UInt/Int

   * Float/Double

* `format`

   * String


**Return Type**


* String


**Example**

**Example 1:** 

```SQL
SELECT from_unixtime('1704733565', '%Y %M %h:%i:%s');
```


```Plain
┌─FROM_UNIXTIME('1704733565', '%Y %M %h:%i:%s')─┐
│ 2024 January 01:06:05                         │
└───────────────────────────────────────────────┘
```


**Example 2:** 

```SQL
SELECT from_unixtime(1704733565);
```


```Plain
┌─FROM_UNIXTIME(1704733565)─┐
│       2024-01-09 01:06:05 │
└───────────────────────────┘
```


<span id="289bd7f9"></span>
### formatDateTime

Format time according to the given format string. The format is a constant expression, so a single result column cannot have multiple formats.

**Syntax**

```SQL
formatDateTime(Time, Format\[, Timezone\])
```


**Parameters**


* `Time` Date/DateTime

* `Format` mode


**Field replacement**

By using field replacement, you can define a pattern for the result string. "Example" column displays the formatted result `2018-01-02 22:33:44`.


|**Placeholder** |**Description** |**Example** |
|---|---|---|
|%C |year divided by 100 and truncated to integer (00\-99)<br><br>Year divided by 100 and truncated to integer (00\-99) |20 |
|%d |day of the month, zero\-padded (01\-31)<br><br>Day of the month, zero\-padded (01\-31) |02 |
|%D |Short MM/DD/YY date, equivalent to %m/%d/%y<br><br>Short MM/DD/YY date, equivalent to %m/%d/%y |01/02/18 |
|%e |day of the month, space\-padded ( 1\-31)<br><br>Day of the month, space\-padded (1\-31) |2 |
|%F |short YYYY\-MM\-DD date, equivalent to %Y\-%m\-%d<br><br>Short date YYYY\-MM\-DD, equivalent to %Y\-%m\-%d |2018\-01\-02 |
|%H |hour in 24h format (00\-23)<br><br>Hour in 24\-hour format (00\-23) |22 |
|%I |hour in 12h format (01\-12)<br><br>Hour in 12\-hour format (01\-12) |10 |
|%j |day of the year (001\-366)<br><br>A certain day of the year (001\-366) |002 |
|%m |month as a decimal number (01\-12)<br><br>Month in decimal form (01\-12) |01 |
|%M |minute (00\-59)<br><br>minute(s) (00\-59) |33 |
|%n |new\-line character (‘’)<br><br>line break ||
|%p |AM or PM designation<br><br>AM or PM designation |PM |
|%R |24\-hour HH:MMtime, equivalent to %H:%M<br><br>24\-hour HH:MM time, equivalent to %H:%M |22:33 |
|%S |second (00\-59)<br><br>seconds (00\-59) |44 |
|%t |horizontal\-tab character (’)<br><br>horizontal\-tab character (') ||
|%T |ISO8601 time format (HH:MM:SS), equivalent to %H:%M:%S<br><br>ISO8601 time format (HH:MM:SS), equivalent to %H:%M:%S |22:33:44 |
|%u |ISO8601 weekday as number with Monday as 1 (1\-7)<br><br>ISO8601 weekday as number, monday as 1 (1\-7) |2 |
|%V |ISO8601 week number (01\-53)<br><br>ISO8601 number of weeks (01\-53) |01 |
|%w |weekday as a decimal number with Sunday as 0 (0\-6)<br><br>Weekday as a decimal number, with Sunday as 0 (0\-6) |2 |
|%y |Year, last two digits (00\-99)<br><br>Year, last two digits (00\-99) |18 |
|%Y |Year<br><br>year |2018 |
|%% |a % sign |% |


**Return values**

Return date and time values according to the specified format.

**Example**

```SQL
SELECT formatDateTime(toDate('2010-01-04'), '%d');
```


```SQL
┌─formatDateTime(toDate('2010-01-04'), '%d')─┐
│ 04                                         │
└────────────────────────────────────────────┘

--from_unixtime 
--This function converts a Unix timestamp into a calendar date and the time of day. When there is only one parameter of the Integer type, it has the same effect as toDateTime and returns a value of the DateTime type.

-- Example
SELECT FROM_UNIXTIME(423543535);
```


```Plain
┌─FROM_UNIXTIME(423543535)─┐
│      1983-06-04 10:58:55 │
└──────────────────────────┘
```


When there are two parameters: the first is either an Integer or DateTime, the second is a constant format string — its behavior is the same as formatDateTime and returns a String type.

For example:

```SQL
SELECT FROM_UNIXTIME(1234334543, '%Y-%m-%d %R:%S') AS DateTime;
```


```Plain
┌─DateTime────────────┐
│ 2009-02-11 14:42:23 │
└─────────────────────┘
```


<span id="25c09490"></span>
### hour

Returns the hours in date and time, same as toHour().

<span id="1cf60f05"></span>
### last_day

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


`Last day` returns the last day of the month for the given date or datetime.

**Syntax**

```SQL
last_day(expr)
```


**Parameter type**


* `expr`

   * Datetime/Datetime64

   * Date/Date32

   * String


**Return type**


* Date


**Example**

**Example 1:** 

```SQL
SELECT last_day('2024-07-21');
```


```Plain
┌─toLastDayOfMonth('2024-07-21')─┐
│                     2024-07-31 │
└────────────────────────────────┘
```


**Example 2:** 

```SQL
SELECT last_day(DATETIME '2024-07-21 10:00:00');
```


```Plain
┌─toLastDayOfMonth(toDateTime('2024-07-21 10:00:00'))─┐
│                                          2024-07-31 │
└─────────────────────────────────────────────────────┘
```


**Example 3:** 

```SQL
SELECT last_day('2024-07-21 10:00:00');
```


```Plain
┌─toLastDayOfMonth('2024-07-21 10:00:00')─┐
│                              2024-07-31 │
└─────────────────────────────────────────┘
```


<span id="39ba7f3e"></span>
### localtime/localtimestamp

Returns the current date and time, the same as now().

<span id="8eeab52a"></span>
### makedate

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


`makedate` returns a date according to the parameters `year` and `dayofyear`.

**Syntax**

```SQL
makedate(year, dayofyear)
```


**Type**


* `year`

   * UInt

   * String

* `dayofyear`

   * UInt

   * String


**Return type**


* Date


**Example**

**Example 1:** 

```SQL
SELECT makedate(2024, 202), makedate(2024, 203);
```


```Plain
┌─makeDate(2024, 202)─┬─makeDate(2024, 203)─┐
│          2024-07-20 │          2024-07-21 │
└─────────────────────┴─────────────────────┘
```


**Example 2:** 

```SQL
SELECT makedate('2024', '202'), makedate('2024', '203');
```


```Plain
┌─makeDate('2024', '202')─┬─makeDate('2024', '203')─┐
│              2024-07-20 │              2024-07-21 │
└─────────────────────────┴─────────────────────────┘
```


<span id="1e0ab4ba"></span>
### maketime

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


`maketime` returns a time according to the parameters `hour`, `minute`, and `second`.

**Syntax**

```SQL
maketime(hour, minute, second)
```


**Parameter Type**


* `hour`

   * UInt

   * String

* `minute`

   * UInt

   * String

* `second`

   * UInt

   * String


**Return type**


* Time


**Example**

**Example 1:** 

```SQL
SELECT maketime(07, 21, 10);
```


```Plain
┌─makeTime(7, 21, 10)─┐
│        07:21:10.000 │
└─────────────────────┘
```


**Example 2:** 

```SQL
SELECT maketime('07', '21', '30');
```


```Plain
┌─makeTime('07', '21', '30')─┐
│               07:21:30.000 │
└────────────────────────────┘
```


<span id="2acb0abe"></span>
### minute

Returns the minute from the date and time, same as toMinute().

<span id="44d85e4b"></span>
### month

Returns the month from the date and time, same as toMonth().

<span id="bedff309"></span>
### monthname

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


`MonthName` returns the full English name of the month in the date.

**Syntax**

```SQL
monthname(date)
```


**Type**


* `date`

   * Datetime/Datetime64

   * Date/Date32

   * String


**Return Type**


* String


**Example**

**Example 1:** 

```SQL
SELECT monthname(DATETIME '2024-07-21 00:00:00');
```


```Plain
┌─monthName(toDateTime('2024-07-21 00:00:00'))─┐
│ July                                         │
└──────────────────────────────────────────────┘
```


**Example 2:** 

```SQL
SELECT monthname(DATE'2024-07-21');
```


```Plain
┌─monthName(toDate('2024-07-21'))─┐
│ July                            │
└─────────────────────────────────┘
```


**Example 3:** 

```SQL
SELECT monthname('2024-07-21');
```


```Plain
┌─monthName('2024-07-21')─┐
│ July                    │
└─────────────────────────┘
```


<span id="9a80a41b"></span>
### now

Returns the current date and time.

**Syntax**

```SQL
now()
```


**Return value**


* Current date and time.


Type: Date time.

**Example**

```SQL
SELECT now();
```


```Plain
┌─now()───────────────┐
│ 2021-08-11 14:35:47 │
└─────────────────────┘
```


<span id="46af3b2f"></span>
### period_add

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


`period_add` moves the date format of expr1 forward by expr2 months.

**Syntax**

```SQL
period_add(expr1, expr2)
```


**Type**


* `expr1`

   * UInt

   * String

* `expr2`

   * UInt

   * String


**Return type**


* UInt


**Example**

**Example 1:** 

```SQL
SELECT period_add(202401, 6);
```


```Plain
┌─period_add(202401, 6)─┐
│                202407 │
└───────────────────────┘
```


**Example 2:** 

```SQL
SELECT period_add('202401', '6');
```


```Plain
┌─period_add('202401', '6')─┐
│                    202407 │
└───────────────────────────┘
```


<span id="cb5ecd59"></span>
### period_diff

`Period Difference` calculates the month difference between expr1 and expr2.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


**Syntax**

```SQL
period_diff(expr1, expr2)
```


**Parameter Type**


* `expr1`

   * UInt

   * String

* `expr2`

   * UInt

   * String


**Return Type**


* UInt


**Example**

**Example 1:** 

```SQL
SELECT period_diff(202407, 202301);
```


```Plain
┌─period_diff(202407, 202301)─┐
│                          18 │
└─────────────────────────────┘
```


**Example 2:** 

```SQL
SELECT period_diff('202407', '202301');
```


```Plain
┌─period_diff('202407', '202301')─┐
│                              18 │
└─────────────────────────────────┘
```


<span id="52c0381e"></span>
### quarter

Returns the corresponding quarter in the date and time, same as toQuarter().

<span id="cd623f51"></span>
### sec_to_time

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


`sec_to_time` converts seconds into time format.

**Syntax**

```SQL
sec_to_time(seconds)
```


**Parameter Type**


* `seconds`

   * UInt/Int

   * String


**Return Type**


* Time


**Example**

**Example 1:** 

```SQL
SELECT sec_to_time(7321);
```


```Plain
┌─sec_to_time(7321)─┐
│      02:02:01.000 │
└───────────────────┘
```


**Example 2:** 

```SQL
SELECT sec_to_time('7321');
```


```Plain
┌─sec_to_time('7321')─┐
│        02:02:01.000 │
└─────────────────────┘
```


<span id="f236f5b8"></span>
### second

Returns the seconds in the datetime, similar to toSecond().

<span id="8797cc5c"></span>
### str_to_date

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


`str_to_date` converts a string into a date or datetime type according to the specified format. The format follows the one in the `date_format` function.

**Syntax**

```SQL
str_to_date(str, format)
```


**Parameter type**


* `str`

   * The string to be converted

   * String

* `format`

   * Format

   * String


**Return Type**


* Datetime


**Example**

**Example 1:** 

```SQL
SELECT str_to_date('2024-07-21 12:13:14', '%Y-%m-%d %H:%i:%s') AS result;
```


```Plain
┌─────────────────────result─┐
│ 2024-07-21 12:13:14.000000 │
└────────────────────────────┘
```


<span id="a490d2b4"></span>
### subtractDays

The function subtracts a date/date\-time interval from a date/date\-time, and then returns the date/date\-time.

**Syntax**

```SQL
subtractDays(date, interval)
subtractDays(datetime, interval)
```


**Parameters**


* `date/datetime` date/datetime

* `interval` date/datetime


**Return Value**


* Date/Datetime


**Example**

```SQL
WITH
    toDate('2019-01-01') AS date,
    toDateTime('2019-01-01 00:00:00') AS date_time
SELECT
    subtractDays(date, 1) AS subtract_days_with_date,
    subtractDays(date_time, 1) AS subtract_days_with_date_time
```


```Plain
┌─subtract_days_with_date─┬─subtract_days_with_date_time─┐
│ 2018-12-31              │ 2018-12-31 00:00:00          │
└─────────────────────────┴──────────────────────────────┘
```


<span id="f1bdfd0c"></span>
### subtractHours

The function subtracts a date/datetime interval from a date/datetime, then returns the date/datetime.

**Syntax**

```SQL
subtractHours(date, interval)
subtractHours(datetime, interval)
```


**Parameters**


* `date/datetime` date/datetime

* `interval` date/date time


**Return value**


* Date/date time


**Example**

```SQL
WITH
    toDate('2019-01-01') AS date,
    toDateTime('2019-01-01 00:00:00') AS date_time
SELECT
    subtractHours(date, 1) AS subtract_hours_with_date,
    subtractHours(date_time, 1) AS subtract_hours_with_date_time
```


```Plain
┌─subtract_hours_with_date─┬─subtract_hours_with_date_time─┐
│ 2002-11-25               │ 2018-12-31 23:00:00           │
└──────────────────────────┴───────────────────────────────┘
```


<span id="57d08c79"></span>
### subtractMinutes

The function subtracts a date/date time interval from a date/date time, then returns the result as a date/date time.

**Syntax**

```SQL
subtractMinutes(date, interval)
subtractMinutes(datetime, interval)
```


**Parameters**


* `date/datetime` date/date time

* `interval` date/date time


**Return Value**


* Date/Date\-time


**Example**

```SQL
WITH
    toDate('2019-01-01') AS date,
    toDateTime('2019-01-01 00:00:00') AS date_time
SELECT
    subtractMinutes(date, 1) AS subtract_minutes_with_date,
    subtractMinutes(date_time, 1) AS subtract_minutes_with_date_time
```


```Plain
┌─subtract_minutes_with_date─┬─subtract_minutes_with_date_time─┐
│ 2012-08-04                 │ 2018-12-31 23:59:00             │
└────────────────────────────┴─────────────────────────────────┘
```


<span id="719b3bf6"></span>
### subtractMonths

The function subtracts a date/date\-time interval from a date/date\-time and then returns the date/date\-time.

**Syntax**

```SQL
subtractMonths(date, interval)
subtractMonths(datetime, interval)
```


**Parameters**


* `Date/Date-time` Date/Date\-time

* `Interval` Date/Date\-time


**Return Value**


* Date/Date\-Time


**Example**

```SQL
WITH
    toDate('2019-01-01') AS date,
    toDateTime('2019-01-01 00:00:00') AS date_time
SELECT
    subtractMonths(date, 1) AS subtract_months_with_date,
    subtractMonths(date_time, 1) AS subtract_months_with_date_time
```


```Plain
┌─subtract_months_with_date─┬─subtract_months_with_date_time─┐
│ 2018-12-01                │ 2018-12-01 00:00:00            │
└───────────────────────────┴────────────────────────────────┘
```


<span id="0508780f"></span>
### subtractQuarters

The function subtracts a date/date\-time interval from a date/date\-time, then returns the date/date\-time.

**Syntax**

```SQL
subtractQuarters(date, interval)
subtractQuarters(datetime, interval)
```


**Parameters**


* `date/datetime` Date/Date\-Time

* `interval` Date/Date\-Time


**Return Value**


* Date/Date\-Time


**Example**

```SQL
WITH
    toDate('2019-01-01') AS date,
    toDateTime('2019-01-01 00:00:00') AS date_time
SELECT
    subtractQuarters(date, 1) AS subtract_quarters_with_date,
    subtractQuarters(date_time, 1) AS subtract_quarters_with_date_time
```


```Plain
┌─subtract_quarters_with_date─┬─subtract_quarters_with_date_time─┐
│ 2018-10-01                  │ 2018-10-01 00:00:00              │
└─────────────────────────────┴──────────────────────────────────┘
```


<span id="9b67f6bc"></span>
### subtractSeconds

The function subtracts a date/datetime interval from a date/datetime and then returns the date/datetime.

**Syntax**

```SQL
subtractSeconds(date, interval)
subtractSeconds(datetime, interval)
```


**Parameters**


* `date/datetime` Date/Datetime

* `interval` Date/Datetime


**Return Value**


* Date/Datetime


**Example**

```SQL
WITH
    toDate('2019-01-01') AS date,
    toDateTime('2019-01-01 00:00:00') AS date_time
SELECT
    subtractSeconds(date, 1) AS subtract_seconds_with_date,
    subtractSeconds(date_time, 1) AS subtract_seconds_with_date_time
```


```Plain
┌─subtract_seconds_with_date─┬─subtract_seconds_with_date_time─┐
│ 2012-10-02                 │ 2018-12-31 23:59:59             │
└────────────────────────────┴─────────────────────────────────┘
```


<span id="35d20425"></span>
### subtractWeeks

The function subtracts a date/date\-time interval from a date/date\-time and then returns a date/date\-time.

**Syntax**

```SQL
subtractWeeks(date, interval)
subtractWeeks(datetime, interval)
```


**Parameters**


* `date/datetime` date/date\-time

* `interval` date/date\-time


**Return Value**


* Date/Date\-time


**Example**

```SQL
WITH
    toDate('2019-01-01') AS date,
    toDateTime('2019-01-01 00:00:00') AS date_time
SELECT
    subtractWeeks(date, 1) AS subtract_weeks_with_date,
    subtractWeeks(date_time, 1) AS subtract_weeks_with_date_time
```


```Plain
┌─subtract_weeks_with_date─┬─subtract_weeks_with_date_time─┐
│ 2018-12-25               │ 2018-12-25 00:00:00           │
└──────────────────────────┴───────────────────────────────┘
```


<span id="d383e9d6"></span>
### subtractYears

The function subtracts a date/datetime interval from a date/datetime and then returns the date/datetime.

**Syntax**

```SQL
subtractYears(date, interval)
subtractYears(datetime, interval)
```


**Parameters**


* `Date/datetime` represents a date or datetime.

* `Interval` represents a date or datetime interval.


**Return Value**


* Date/datetime


**Example**

```SQL
WITH
    toDate('2019-01-01') AS date,
    toDateTime('2019-01-01 00:00:00') AS date_time
SELECT
    subtractYears(date, 1) AS subtract_years_with_date,
    subtractYears(date_time, 1) AS subtract_years_with_date_time
```


```Plain
┌─subtract_years_with_date─┬─subtract_years_with_date_time─┐
│ 2018-01-01               │ 2018-01-01 00:00:00           │
└──────────────────────────┴───────────────────────────────┘
```


<span id="cb96b584"></span>
### subtime

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


`subtime` returns the time after subtracting `expr1` from `expr2`.

**Grammar**

```SQL
subtime(expr1, expr2)
```


**Parameter Type**


* `expr1`

   * Expression from which time needs to be subtracted

   * Datetime

* `expr2`

   * Time to be subtracted

   * String


**Return Type**


* Datetime


**Example**

**Example 1:** 

```SQL
SELECT subtime(date '2024-07-21', '0:1:1');
```


```Plain
┌─subtime(toDate('2024-07-21'), '0:1:1')─┐
│                2024-07-20 23:58:59.000 │
└────────────────────────────────────────┘
```


**Example 2:** 

```SQL
SELECT subtime(datetime '2024-07-21 12:13:14', '0:1:1');
```


```Plain
┌─subtime(toDateTime('2024-07-21 12:13:14'), '0:1:1')─┐
│                             2024-07-21 12:12:13.000 │
└─────────────────────────────────────────────────────┘
```


**Example 3:** 

```SQL
SELECT subtime(time '12:13:14', '0:1:1');
```


```Plain
┌─subtime(toTimeType('12:13:14'), '0:1:1')─┐
│                             12:12:13.000 │
└──────────────────────────────────────────┘
```


**Example 4:** 

```SQL
SELECT subtime('2024-07-21 12:13:14', '0:1:1');
```


```Plain
┌─subtime('2024-07-21 12:13:14', '0:1:1')─┐
│                 2024-07-21 12:12:13.000 │
└─────────────────────────────────────────┘
```


<span id="188a3bd7"></span>
### sysdate

Returns the current system time, same as now().

<span id="a9516b90"></span>
### time

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


Returns the time in `expr`.

**Syntax**

```SQL
time(expr[, scale])
```


**Parameter Type**


* `expr`

   * Expression to extract time

   * String

   * Datetime/Datetime64

* `scale`

   * Denotes the decimal precision of the target time

   * UInt8


**Return Type**


* Time


**Example**

**Example 1:** 

```SQL
SELECT time('2024-07-21 12:13:14');
```


```Plain
┌─TIME('2024-07-21 12:13:14')─┐
│                12:13:14.000 │
└─────────────────────────────┘
```


**Example 2:** 

```SQL
SELECT time('2024-07-21 12:13:14', 0);
```


```Plain
┌─TIME('2024-07-21 12:13:14', 0)─┐
│                       12:13:14 │
└────────────────────────────────┘
```


**Example 3:** 

```SQL
SELECT time(Datetime64'2024-07-21 12:13:14.123456', 3);
```


```Plain
┌─TIME(toDateTime64('2024-07-21 12:13:14.123456'), 3)─┐
│                                        12:13:14.123 │
└─────────────────────────────────────────────────────┘
```


<span id="347f2eec"></span>
### timeDiff

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


Returns the time difference between two inputs, same as subtime().

<span id="741d35d7"></span>
### timestamp

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


`Timestamp` returns the date or datetime represented by `expr`.

**Syntax**

```SQL
timestamp(expr)
```


**Parameter Types**


* `expr`

   * Expression to be converted to a timestamp

   * Date/Date32

   * String


**Return type**


* Datetime


**Example**

**Example 1:** 

```SQL
SELECT timestamp(date '2024-07-21');
```


```Plain
┌─timestamp(toDate('2024-07-21'))─┐
│      2024-07-21 00:00:00.000000 │
└─────────────────────────────────┘
```


**Example 2:** 

```SQL
SELECT timestamp('2024-07-21');
```


```Plain
┌────timestamp('2024-07-21')─┐
│ 2024-07-21 00:00:00.000000 │
└────────────────────────────┘
```


<span id="aa9aa506"></span>
### timestampAdd

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


`timestampadd` adds an `interval` to a date or datetime expression `datetime_expr`. The unit of `interval` is specified by `unit`. The possible values for `unit` are: `second`, `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year`.

**Syntax**

```SQL
timestampadd(unit, interval, datetime_expr)
```


**Parameter Types**


* `unit`

   * Time Units

* `interval`

   * Time Interval

   * String

   * UInt64

* `datetime_expr`

   * Date or date\-time expression

   * String

   * Date/Date32/Datetime/Datetime64/Time


**Return type**


* Datetime


**Example**

**Example 1:** 

```SQL
SELECT timestampadd(second, '1', datetime '2024-07-21 12:13:14') AS result;
```


```Plain
┌──────────────result─┐
│ 2024-07-21 12:13:15 │
└─────────────────────┘
```


**Example 2:** 

```SQL
SELECT timestampadd(second, '1', date '2024-07-21') AS result;
```


```SQL
┌──────────────result─┐
│ 2024-07-21 00:00:01 │
└─────────────────────┘
```


<span id="c7de1a9d"></span>
### timestampDiff

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


`timestampdiff` returns the result of subtracting datetime_expr1 from datetime_ex`datetime_expr1 from datetime_expr2`, specified in the units of `unit`. Valid values for `unit` are: second, minute, hour, day, week, month, quarter, or year.

**Syntax**

```SQL
timestampdiff(unit, datetime_expr1, datetime_expr2)
```


**Parameter Type**


* `unit`

   * Time Unit

   * String

* `datetime_expr1`

   * The starting date or datetime expression to calculate

   * Date/Date32/Datetime/Datetime64

* `datetime_expr2`

   * End date or datetime expression to be calculated

   * Date/Date32/Datetime/Datetime64

   * String


**Return type**


* Int64


**Example**

**Example 1:** 

```SQL
SELECT timestampdiff(second, datetime '2024-07-21 10:12:13', datetime '2024-07-21 12:13:14') AS result;
```


```Plain
┌─result─┐
│   7261 │
└────────┘
```


**Example 2:** 

```SQL
SELECT timestampdiff(minute, '2024-07-21 10:12:13', '2024-07-21 12:13:14');
```


```Plain
┌─timestampdiff('minute', '2024-07-21 10:12:13', '2024-07-21 12:13:14')─┐
│                                                                   121 │
└───────────────────────────────────────────────────────────────────────┘
```


<span id="16e9b690"></span>
### timeSlot

Round the time to the nearest half\-hour.

This function is unique to Yandex.Metrica, as it uses the shortest time of half an hour to split the session into two if the tracking tag shows a single user’s consecutive page views are strictly more than half an hour apart. This means it's possible to search the page views contained within the session using the triplet (Tag ID, User ID, and Time Frame).

**Syntax**

```SQL
timeSlot(datetime)
```


**Parameters**


* `datetime`


**Return Value**


* `DateTime`


**Example**

```SQL
SELECT timeSlot(toDateTime('2018-01-01 01:01:01'))
```


```Plain
┌─timeSlot(toDateTime('2018-01-01 01:01:01'))─┐
│ 2018-01-01 01:00:00                         │
└─────────────────────────────────────────────┘
```


<span id="54ce3a31"></span>
### timeSlots

For the time interval starting from "StartTime" and lasting for "Duration" seconds, it returns an array of time points within that interval, rounded to "Size" in seconds. "Size" is an optional parameter: a constant UInt32, default set to 1800.

It is necessary for searching page views in the corresponding session.

**Syntax**

```SQL
timeSlots(StartTime, Duration,[, Size])
```


**Parameters**


* `StartTime` appointment time

* `Duration` duration in seconds, UInt32

* `Size` size of the interval.


**Return value**


* Time frame array.


**Example**

```SQL
SELECT timeSlots(toDateTime('2012-01-01 12:20:00'), toUInt32(600))
```


```Plain
┌─timeSlots(toDateTime('2012-01-01 12:20:00'), toUInt32(600))─┐
│ [2012-01-01 12:00:00, 2012-01-01 12:30:00]                  │
└─────────────────────────────────────────────────────────────┘
```


To which day of this month

Converts a date/datetime to an UInt8 number containing the number of days in the month (1\-31).

**Syntax**

```SQL
toDayOfMonth(date)
toDayOfMonth(datetime)
sql
```


**Parameter**


* `Date/datetime`


**Return value**


* A certain day of the month. UInt8


**Example**

```SQL
SELECT toDayOfMonth(toDate('2021-08-12'))
sql
```


```Plain
┌─toDayOfMonth(toDate('2021-08-12'))─┐
│ 12                                 │
└────────────────────────────────────┘
```


```SQL
SELECT toDayOfMonth(toDateTime('2021-08-12 00:00:00'))
sql
```


```Plain
┌─toDayOfMonth(toDateTime('2021-08-12 00:00:00'))─┐
│ 12                                              │
└─────────────────────────────────────────────────┘
```


<span id="4dd78e8f"></span>
### time_format

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


`time_format` Accoding to the `Format` specified, display the time `Time` as a String. `Format` follows the format in the `date_format` function.

**Syntax**

```SQL
time_format(time, format)
```


**Type**


* `time`

   * The time to be formatted

   * String

   * Date/Date32/Datetime/Datetime64/Time

* `format`

   * Format

   * String


**Return Type**


* String


**Example**

**Example 1:** 

```SQL
SELECT time_format('12:00:00', '%H %k %h %I %l');
```


```Plain
┌─TIME_FORMAT('12:00:00', '%H %k %h %I %l')─┐
│ 12 12 12 12 12                            │
└───────────────────────────────────────────┘
```


**Example 2:** 

```SQL
SELECT time_format(datetime '2024-07-21 23:00:00', '%H %k %h %I %l') AS result;
```


```Plain
┌─result─────────┐
│ 23 23 11 11 11 │
└────────────────┘
```


**Example 3:** 

```SQL
SELECT time_format(time '23:00:00', '%H %k %h %I %l');
```


```Plain
┌─TIME_FORMAT(toTimeType('23:00:00'), '%H %k %h %I %l')─┐
│ 23 23 11 11 11                                        │
└───────────────────────────────────────────────────────┘
```


**Example 4:** 

```SQL
SELECT time_format(date '2024-07-21', '%H %k %h %I %l');
```


```Plain
┌─TIME_FORMAT(toDate('2024-07-21'), '%H %k %h %I %l')─┐
│ 00 00 12 12 12                                      │
└─────────────────────────────────────────────────────┘
```


<span id="2cb248aa"></span>
### time_to_sec

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


`time_to_sec` returns the result of converting `time` to seconds.

**Syntax**

```SQL
time_to_sec(time)
```


**Parameter Type**


* `time`

   * Time to be converted to seconds

   * String

   * Date/Date32/Datetime/Datetime64/Time


**Return Type**


* UInt64


**Example**

**Example 1:** 

```SQL
SELECT time_to_sec(datetime '2024-07-21 22:23:00');
```


```Plain
┌─time_to_sec(toDateTime('2024-07-21 22:23:00'))─┐
│                                          80580 │
└────────────────────────────────────────────────┘
```


**Example 2:** 

```SQL
sql
Copy code
SELECT time_to_sec(date '2024-07-21');
```


```Plain
┌─time_to_sec(toDate('2024-07-21'))─┐
│                                 0 │
└───────────────────────────────────┘
```


**Example 4:** 

```SQL
SELECT time_to_sec(time '12:12:12');
```


```Plain
┌─time_to_sec(toTimeType('12:12:12'))─┐
│                               43932 │
└─────────────────────────────────────┘
```


**Example 5:** 

```SQL
SELECT time_to_sec('22:23:00');
```


```Plain
┌─time_to_sec('22:23:00')─┐
│                   80580 │
└─────────────────────────┘
```


<span id="1da33aed"></span>
### toDayOfWeek

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


Convert a date or datetime to a UInt8 number that includes the day of the week (Monday as 1, Sunday as 7).

**Syntax**

```SQL
toDayOfWeek(date)
toDayOfWeek(datetime)
```


**Param**


* `date/datetime` Date/Datetime


**Return value**


* What day of the week. UInt8


**Example**

```SQL
SELECT toDayOfWeek(toDate('2021-08-12'))
```


```Plain
┌─toDayOfWeek(toDate('2021-08-12'))─┐
│ 4                                 │
└───────────────────────────────────┘
```


```SQL
SELECT toDayOfWeek(toDateTime('2021-08-12 00:00:00'))
```


```Plain
┌─toDayOfWeek(toDateTime('2021-08-12 00:00:00'))─┐
│ 4                                              │
└────────────────────────────────────────────────┘
```


<span id="2c7f568d"></span>
### toDayOfYear

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


Converts a date or datetime to a UInt16 number containing the days of the year (1\-366).

**Syntax**

```SQL
toDayOfYear(date)
toDayOfYear(datetime)
```


**Param**


* `date/datetime` Date/Datetime


**Return value**


* On a certain day of the year. UInt8


**Example**

```SQL
SELECT toDayOfWeek(toDate('2021-08-12'))
```


```Plain
┌─toDayOfWeek(toDate('2021-08-12'))─┐
│ 4                                 │
└───────────────────────────────────┘
```


```SQL
SELECT toDayOfWeek(toDateTime('2021-08-12 00:00:00'))
```


```Plain
┌─toDayOfWeek(toDateTime('2021-08-12 00:00:00'))─┐
│ 4                                              │
└────────────────────────────────────────────────┘
```


<span id="99d4bfa8"></span>
### toHour

Converts a date with time to a UInt8 number containing the hours in the 24\-hour format (0\-23).

This function assumes that if the clock moves forward, it will move by an hour, occurring at 2 AM, and if the clock moves backward, it will move by an hour, occurring at 3 AM (this is not always correct \- even in Moscow, the clock is adjusted at different times twice).

**Syntax**

```SQL
toHour(datetime)
```


**Parameters**


* `datetime` Appointment time


**Return value**


* The number of hours in a 24\-hour format. UInt8


**Example**

```SQL
SELECT toHour(toDateTime('2021-08-12 00:00:00'))
```


```Plain
┌─toHour(toDateTime('2021-08-12 00:00:00'))─┐
│ 0                                         │
└───────────────────────────────────────────┘
```


<span id="7d2524bd"></span>
### toISOWeek

Converts a date or datetime to a UInt8 number containing the ISO week number.

**Syntax**

```SQL
toISOWeek(date)
toISOWeek(datetime)
```


**Parameters**


* `Date/datetime` date or datetime


**Return value**


* ISO week number. UInt8


**Example**

```SQL
SELECT toISOWeek(toDate('2021-08-12'))
```


```Plain
┌─toISOWeek(toDate('2021-08-12'))─┐
│ 32                              │
└─────────────────────────────────┘
```


```SQL
SELECT toISOWeek(toDateTime('2021-08-12 00:00:00'))
```


```Plain
┌─toISOWeek(toDateTime('2021-08-12 00:00:00'))─┐
│ 32                                           │
└──────────────────────────────────────────────┘
```


<span id="a0e90e5a"></span>
### toISOYear

Converts the date or datetime to a UInt16 number containing the ISO year digits.

**Syntax**

```SQL
toISOYear(date)
toISOYear(datetime)
```


**Parameters**


* `Date/datetime` Date/datetime


**Return Value**


* ISO year digits. UInt16


**Example**

```SQL
SELECT toISOYear(toDate('2021-08-12'))
```


```Plain
┌─toISOYear(toDate('2021-08-12'))─┐
│ 2021                            │
└─────────────────────────────────┘
```


```SQL
SELECT toISOYear(toDateTime('2021-08-12 00:00:00'))
```


```Plain
┌─toISOYear(toDateTime('2021-08-12 00:00:00'))─┐
│ 2021                                         │
└──────────────────────────────────────────────┘
```


<span id="685c9259"></span>
### toMinute

Converts a date with time into a UInt8 number representing the minutes (0\-59).

**Syntax**

```SQL
toMinute(datetime)
```


**Parameters**


* `datetime` Appointment time


**Return Value**


* Minutes within an hour. UInt8


**Example**

```SQL
SELECT toMinute(toDateTime('2021-08-12 00:00:00'))
```


```Plain
┌─toMinute(toDateTime('2021-08-12 00:00:00'))─┐
│ 0                                           │
└─────────────────────────────────────────────┘
```


<span id="eed0635b"></span>
### toMonday

Round the date or datetime down to the nearest Monday.

Return the date.

**Syntax**

```SQL
toMonday(date)
toMonday(datetime)
```


**Parameters**


* `date/datetime` Date/Datetime


**Return value**


* Date to the nearest Monday. Date


**Example**

```SQL
SELECT toMonday(toDate('2021-08-12'))
```


```Plain
┌─toMonday(toDate('2021-08-12'))─┐
│ 2021-08-09                     │
└────────────────────────────────┘
```


```SQL
SELECT toMonday(toDateTime('2021-08-12 00:00:00'))
```


```Plain
┌─toMonday(toDateTime('2021-08-12 00:00:00'))─┐
│ 2021-08-09                                  │
└─────────────────────────────────────────────┘
```


<span id="9147b9cd"></span>
### toMonth

Converts a date or date\-time to an UInt8 number representing the month (1\-12).

**Syntax**

```SQL
toMonth(date)
toMonth(datetime)
```


**Parameters**


* `Date/DateTime` \- date/date\-time


**Return Value**


* Converts the date to the nearest Monday. Date


**Example**

```SQL
SELECT toMonday(toDate('2021-08-12'))
```


```Plain
┌─toMonday(toDate('2021-08-12'))─┐
│ 2021-08-09                     │
└────────────────────────────────┘
```


```SQL
SELECT toMonday(toDateTime('2021-08-12 00:00:00'))
```


```Plain
┌─toMonday(toDateTime('2021-08-12 00:00:00'))─┐
│ 2021-08-09                                  │
└─────────────────────────────────────────────┘
```


<span id="5041c03a"></span>
### toQuarter

Convert the date or datetime to a UInt8 number including the quarter.

**Syntax**

```SQL
toQuarter(date)
toQuarter(datetime)
```


**Parameters**


* `Date/datetime` Date/Datetime


**Return Value**


* Quarter number. UInt8


**Example**

```SQL
SELECT toQuarter(toDate('2021-08-12'))
```


```Plain
┌─toQuarter(toDate('2021-08-12'))─┐
│ 3                               │
└─────────────────────────────────┘
```


```SQL
SELECT toQuarter(toDateTime('2021-08-12 00:00:00'))
```


```Plain
┌─toQuarter(toDateTime('2021-08-12 00:00:00'))─┐
│ 3                                            │
└──────────────────────────────────────────────┘
```


<span id="3193a314"></span>
### toRelativeDayNum

Convert dates with time or date to the number of days from a fixed point in the past.

**Syntax**

```SQL
toRelativeDayNum(date)
toRelativeDayNum(datetime)
```


**Parameters**


* `date/datetime` Date/Date Time


**Return Values**


* Number of days from a fixed point in the past. UInt16


**Example**

```SQL
SELECT toRelativeDayNum(toDate('2021-08-12'))
```


```Plain
┌─toRelativeDayNum(toDate('2021-08-12'))─┐
│ 18851                                  │
└────────────────────────────────────────┘
```


```SQL
SELECT toRelativeDayNum(toDateTime('2021-08-12 00:00:00'))
```


```Plain
┌─toRelativeDayNum(toDateTime('2021-08-12 00:00:00'))─┐
│ 18851                                               │
└─────────────────────────────────────────────────────┘
```


<span id="5127cafb"></span>
### toRelativeHourNum

Converts a date with time or date to number of hours from a fixed point in the past.

**Syntax**

```SQL
toRelativeHourNum(date)
toRelativeHourNum(datetime)
```


**Parameter**


* `Date/datetime` date/datetime


**Return value**


* Hours, starting from a fixed point in the past. UInt32


**Example**

```SQL
SELECT toRelativeHourNum(toDate('2021-08-12'))
```


```Plain
┌─toRelativeHourNum(toDate('2021-08-12'))─┐
│ 452416                                  │
└─────────────────────────────────────────┘
```


```SQL
SELECT toRelativeHourNum(toDateTime('2021-08-12 00:00:00'))
```


```Plain
┌─toRelativeHourNum(toDateTime('2021-08-12 00:00:00'))─┐
│ 452416                                               │
└──────────────────────────────────────────────────────┘
```


<span id="c18b668d"></span>
### toRelativeMinuteNum

Converts a date with time or date to minutes, starting from a fixed point in the past.

**Syntax**

```SQL
toRelativeMinuteNum(date)
toRelativeMinuteNum(datetime)
```


**Parameter**


* `Date/DateTime` \- Date/Date and time


**Return value**


* Minutes, starting from a fixed point in the past. UInt32


**Example**

```SQL
SELECT toRelativeMinuteNum(toDate('2021-08-12'))
```


```Plain
┌─toRelativeMinuteNum(toDate('2021-08-12'))─┐
│ 27144960                                  │
└───────────────────────────────────────────┘
```


```SQL
SELECT toRelativeMinuteNum(toDateTime('2021-08-12 00:00:00'))
```


```Plain
┌─toRelativeMinuteNum(toDateTime('2021-08-12 00:00:00'))─┐
│ 27144960                                               │
└────────────────────────────────────────────────────────┘
```


<span id="04f265c3"></span>
### toRelativeMonthNum

Converts a date with time or date to a month number, starting from a fixed point in the past.

**Syntax**

```SQL
toRelativeMonthNum(date)
toRelativeMonthNum(datetime)
```


**Parameters**


* `Date/DateTime` \- Date/Date and time


**Return Value**


* Number of months from a specific point in the past. UInt16


**Example**

```SQL
SELECT toRelativeMonthNum(toDate('2021-08-12'))
```


```Plain
┌─toRelativeMonthNum(toDate('2021-08-12'))─┐
│ 24260                                    │
└──────────────────────────────────────────┘
```


```SQL
SELECT toRelativeMonthNum(toDateTime('2021-08-12 00:00:00'))
```


```Plain
┌─toRelativeMonthNum(toDateTime('2021-08-12 00:00:00'))─┐
│ 24260                                                 │
└───────────────────────────────────────────────────────┘
```


<span id="6f82329a"></span>
### toRelativeQuarterNum

Converts a date with time or just date into a quarter number starting from a fixed point in the past.

**Syntax**

```SQL
toRelativeQuarterNum(date)
toRelativeQuarterNum(datetime)
```


**Parameters**


* `Date/DateTime` Date/DateTime


**Return Value**


* Quarter number starting from a specific fixed point in the past. UInt16


**Example**

```SQL
SELECT toRelativeQuarterNum(toDate('2021-08-12'))
```


```Plain
┌─toRelativeQuarterNum(toDate('2021-08-12'))─┐
│ 8086                                       │
└────────────────────────────────────────────┘
```


```SQL
SELECT toRelativeQuarterNum(toDateTime('2021-08-12 00:00:00'))
```


```Plain
┌─toRelativeQuarterNum(toDateTime('2021-08-12 00:00:00'))─┐
│ 8086                                                    │
└─────────────────────────────────────────────────────────┘
```


<span id="12f48bf3"></span>
### toRelativeSecondNum

Converts a date with time or date into seconds starting from a specific fixed point in the past.

**Syntax**

```SQL
toRelativeSecondNum(date)
toRelativeSecondNum(datetime)
```


**Parameters**


* `Date/datetime` date/date\-time


**Return value**


* Seconds starting from a specific fixed point in the past. UInt32


**Example**

```SQL
SELECT toRelativeSecondNum(toDate('2021-08-12'))
```


```Plain
┌─toRelativeSecondNum(toDate('2021-08-12'))─┐
│ 1628697600                                │
└───────────────────────────────────────────┘
```


```SQL
SELECT toRelativeSecondNum(toDateTime('2021-08-12 00:00:00'))
```


```Plain
┌─toRelativeSecondNum(toDateTime('2021-08-12 00:00:00'))─┐
│ 1628697600                                             │
└────────────────────────────────────────────────────────┘
```


<span id="674bb990"></span>
### toRelativeWeekNum

Converts dates with time or date into week numbers, starting from a fixed point in the past.

**Syntax**

```SQL
toRelativeWeekNum(date)
toRelativeWeekNum(datetime)
```


**Parameters**


* `Date/datetime` date/date\-time


**Return value**


* Week numbers starting from a fixed point in the past. UInt16


**Example**

```SQL
SELECT toRelativeWeekNum(toDate('2021-08-12'))
```


```Plain
┌─toRelativeWeekNum(toDate('2021-08-12'))─┐
│ 2693                                    │
└─────────────────────────────────────────┘
```


```SQL
SELECT toRelativeWeekNum(toDateTime('2021-08-12 00:00:00'))
```


```Plain
┌─toRelativeWeekNum(toDateTime('2021-08-12 00:00:00'))─┐
│ 2693                                                 │
└──────────────────────────────────────────────────────┘
```


<span id="b973d26b"></span>
### toRelativeYearNum

Converts a date with time or just a date to a number of years starting from a certain fixed point in the past.

**Syntax**

```SQL
toRelativeYearNum(date)
toRelativeYearNum(datetime)
```


**Parameters**


* `date/datetime` date/datetime


**Return value**


* The number of years from a certain fixed point in the past. UInt16


**Example**

```SQL
SELECT toRelativeYearNum(toDate('2021-08-12'))
```


```Plain
┌─toRelativeYearNum(toDate('2021-08-12'))─┐
│ 2021                                    │
└─────────────────────────────────────────┘
```


```SQL
SELECT toRelativeYearNum(toDateTime('2021-08-12 00:00:00'))
```


```Plain
┌─toRelativeYearNum(toDateTime('2021-08-12 00:00:00'))─┐
│ 2021                                                 │
└──────────────────────────────────────────────────────┘
```


<span id="ddb5d686"></span>
### toSecond

Convert a date with time to a UInt8 number representing the seconds within the minute (0\-59).

Leap seconds are not considered.

**Syntax**

```SQL
toSecond(datetime)
```


**Parameters**


* `datetime` Appointment time


**Return Value**


* Seconds within the minute. UInt8


**Example**

```SQL
SELECT toSecond(toDateTime('2021-08-12 00:00:00'))
```


```Plain
┌─toSecond(toDateTime('2021-08-12 00:00:00'))─┐
│ 0                                           │
└─────────────────────────────────────────────┘
```


<span id="251c31b2"></span>
### toStartOfDay

Rounds the date\-time down to the start of the day.

**Syntax**

```SQL
toStartOfDay(datetime)
```


**Parameters**


* `datetime` Date\-Time


**Return Value**


* Rounds the date\-time down to the start of the day. Date\-Time


**Example**

```SQL
SELECT toStartOfDay(toDateTime('2021-08-12 08:00:00'))
```


```Plain
┌─toStartOfDay(toDateTime('2021-08-12 08:00:00'))─┐
│ 2021-08-12 00:00:00                             │
└─────────────────────────────────────────────────┘
```


<span id="503b95e9"></span>
### toStartOfFifteenMinutes

Round the date and time down to the start of a fifteen\-minute interval.

**Grammar**

```SQL
toStartOfFifteenMinutes(datetime)
```


**Parameters**


* `datetime` Date and time


**Return value**


* Round the date and time down to the start of a fifteen\-minute interval. DateTime


**Example**

```SQL
SELECT toStartOfFifteenMinutes(toDateTime('2021-08-12 00:10:00'))
```


```Plain
┌─toStartOfFifteenMinutes(toDateTime('2021-08-12 00:10:00'))─┐
│ 2021-08-12 00:00:00                                        │
└────────────────────────────────────────────────────────────┘
```


<span id="8a4839bd"></span>
### toStartOfFiveMinute

Round the date and time down to the start of a five\-minute interval.

**Syntax**

```SQL
toStartOfFiveMinute(datetime)
```


**Parameter**


* `datetime` appointment time


**Return value**


* Round down the datetime to the start of a five\-minute interval. DateTime


**Example**

```SQL
SELECT toStartOfFiveMinute(toDateTime('2021-08-12 00:09:00'))
```


```Plain
┌─toStartOfFiveMinute(toDateTime('2021-08-12 00:09:00'))─┐
│ 2021-08-12 00:05:00                                    │
└────────────────────────────────────────────────────────┘
```


<span id="bd64825a"></span>
### toStartOfHour

Round down the datetime to the start of the hour.

**Syntax**

```SQL
toStartOfHour(datetime)
```


**Parameter**


* `datetime`DateTime


**Return Value**


* Round the datetime down to the start of the hour. DateTime


**Example**

```SQL
SELECT toStartOfHour(toDateTime('2021-08-12 01:09:00'))
```


```Plain
┌─toStartOfHour(toDateTime('2021-08-12 01:09:00'))─┐
│ 2021-08-12 01:00:00                              │
└──────────────────────────────────────────────────┘
```


<span id="bd94208a"></span>
### toStartOfISOYear

Round the date or datetime down to the first day of the ISO year.

Return the date.

**Syntax**

```SQL
toStartOfISOYear(date)
toStartOfISOYear(datetime)
```


**Parameter**


* `Date/datetime` Date/Date and Time


**Return Value**


* Rounds down a date or a date with time to the first day of the ISO year. Date


**Example**

```SQL
SELECT toStartOfISOYear(toDate('2021-08-12'))
```


```Plain
┌─toStartOfISOYear(toDate('2021-08-12'))─┐
│ 2021-01-04                             │
└────────────────────────────────────────┘
```


```SQL
SELECT toStartOfISOYear(toDateTime('2021-08-12 00:00:00'))
```


```Plain
┌─toStartOfISOYear(toDateTime('2021-08-12 00:00:00'))─┐
│ 2021-01-04                                          │
└─────────────────────────────────────────────────────┘
```


<span id="6d45b988"></span>
### toStartOfInterval

This is a generalization of the function named `toStartOf*`. For example,

`toStartOfInterval(t, INTERVAL 1 year)` returns the same value as `toStartOfYear(t)`.

`toStartOfInterval(t, INTERVAL 1 month)` returns the same value as `toStartOfMonth(t)`.

`toStartOfInterval(t, INTERVAL 1 day)` returns the same value as `toStartOfDay(t)`.

`toStartOfInterval(t, INTERVAL 15 minute)` returns the same value as `toStartOfFifteenMinutes(t)` and similar.

**Syntax**

```SQL
toStartOfInterval(time_or_data, INTERVAL x unit [, time_zone])
```


**Parameters**


* `time_or_data` Date/DateTime

* `x unit` x is UInt\*, units can be seconds, minutes, hours, days, months, years, quarters


**Return Values**


* Date/DateTime


**Examples**

```SQL
SELECT toStartOfInterval(toDateTime('2021-08-12 01:09:00'), INTERVAL 2 minute)
```


```Plain
┌─toStartOfInterval(toDateTime('2021-08-12 01:09:00'), toIntervalMinute(2))─┐
│ 2021-08-12 01:08:00                                                       │
└───────────────────────────────────────────────────────────────────────────┘
```


<span id="24dbe255"></span>
### toStartOfMinute

Rounds down the date and time to the start of the minute.

**Syntax**

```SQL
toStartOfMinute(datetime)
```


**Parameters**


* `datetime` Date and time


**Return Value**


* Rounds down the date and time to the start of the minute. DateTime


**Example**

```SQL
SELECT toStartOfMinute(toDateTime('2021-08-12 00:01:30'))
```


```Plain
┌─toStartOfMinute(toDateTime('2021-08-12 00:01:30'))─┐
│ 2021-08-12 00:01:00                                │
└────────────────────────────────────────────────────┘
```


<span id="842e5299"></span>
### toStartOfMonth

Round down the date or datetime to the first day of that month.

Return the date.

**Syntax**

```SQL
toStartOfMonth(date)
toStartOfMonth(datetime)
sql
```


**Param**


* `date/datetime` Date/datetime


**Return value**


* Round down the date or datetime to the first day of that month. Date


**Example**

```SQL
SELECT toStartOfMonth(toDate('2021-08-12'))
```


```Plain
┌─toStartOfMonth(toDate('2021-08-12'))─┐
│ 2021-08-01                           │
└──────────────────────────────────────┘
```


```SQL
SELECT toStartOfMonth(toDateTime('2021-08-12 00:01:30'))
```


```Plain
┌─toStartOfMonth(toDateTime('2021-08-12 00:01:30'))─┐
│ 2021-08-01                                        │
└───────────────────────────────────────────────────┘
```


<span id="ee23cfcd"></span>
### toStartOfQuarter

Round the date or datetime down to the first day of the quarter.

The first day of a quarter can be January 1, April 1, July 1, or October 1.

Return date.

**Syntax**

```SQL
toStartOfQuarter(date)
toStartOfQuarter(datetime)
```


**Param**


* `Date/datetime` Date/datetime


**Return value**


* Round the date or datetime down to the first day of the quarter. Date


**Example**

```SQL
SELECT toStartOfQuarter(toDate('2021-08-12'))
```


```Plain
┌─toStartOfQuarter(toDate('2021-08-12'))─┐
│ 2021-07-01                             │
└────────────────────────────────────────┘
```


```SQL
SELECT toStartOfQuarter(toDateTime('2021-08-12 00:01:30'))
```


```Plain
┌─toStartOfQuarter(toDateTime('2021-08-12 00:01:30'))─┐
│ 2021-07-01                                          │
└─────────────────────────────────────────────────────┘
```


<span id="f4467093"></span>
### toStartOfTenMinutes

Round the date and time down to the start of the ten\-minute interval.

**Param**

```SQL
toStartOfTenMinutes(datetime)
```


**Param**


* `datetime` Date and Time


**Return value**


* Round the date and time down to the start of the ten\-minute interval. DateTime


**Example**

```SQL
SELECT toStartOfTenMinutes(toDateTime('2021-08-12 00:01:30'))
```


```Plain
┌─toStartOfTenMinutes(toDateTime('2021-08-12 00:01:30'))─┐
│ 2021-08-12 00:00:00                                    │
└────────────────────────────────────────────────────────┘
```


<span id="9ccc0ab3"></span>
### toStartOfWeek

According to the mode, round the date or the date with time down to the nearest sunday or monday.

Return the date. mode

The param’s role is exactly the same as the mode param in toWeek(). For single\-param syntax, use mode value 0.

**Syntax**

```SQL
toStartOfWeek(date\[,mode\])
toStartOfWeek(datetime\[,mode\])
```


**Param**


* `Date/datetime` Date/Date time

* `Mode` refers to the week mode.


**Return value**


* According to the mode, round down the Date or datetime to the nearest sunday or monday.


**Example**

```SQL
SELECT toStartOfWeek(toDateTime('2021-08-12 00:01:30'))
```


```Plain
┌─toStartOfWeek(toDateTime('2021-08-12 00:01:30'))─┐
│ 2021-08-08                                       │
└──────────────────────────────────────────────────┘
```


<span id="b821b548"></span>
### toStartOfYear

Round down the Date or datetime to the first day of the year.

Back Date.

**Syntax**

```SQL
toStartOfYear(date)
toStartOfYear(datetime)
```


**Param**


* `Date/datetime` Date/datetime


**Return value**


* Round down the Date or datetime to the first day of the year. Date


**Example**

```SQL
SELECT toStartOfYear(toDateTime('2021-08-12 00:01:30'))
```


```Plain
┌─toStartOfYear(toDateTime('2021-08-12 00:01:30'))─┐
│ 2021-01-01                                       │
└──────────────────────────────────────────────────┘
```


<span id="9bbb859b"></span>
### toTime

Convert a date with time to a fixed date while retaining the time.

**Syntax**

```SQL
toTime(date)
toTime(datetime)
```


**Param**


* `date/datetime` Date/DateTime


**Return value**


* Appointment Time


**Example**

```SQL
SELECT toTime(toDateTime('2021-08-12 00:01:30'))
```


```Plain
┌─toTypeName(toTime(toDateTime('2021-08-12 00:01:30')))─┐
│ DateTime('PRC')                                       │
└───────────────────────────────────────────────────────┘
```


<span id="350578ab"></span>
### toTimezone

Convert time or date and time to the specified timezone. Timezone is a property of the `Date` and `DateTime` data types. The internal value (in seconds) of table fields or result set columns remains unchanged, but the type of the column changes and its string representation changes accordingly.

**Syntax**

```SQL
toTimezone(value, timezone)
```


**Parameters**


* `value`— Time or date and time. Date/DateTime.

* `timezone`— The timezone of the return value. String.


**Return value**


* Date and time. Date time.


**Example**

```SQL
SELECT toDateTime('2019-01-01 00:00:00', 'UTC') AS time_utc,
    toTypeName(time_utc) AS type_utc,
    toInt32(time_utc) AS int32utc,
    toTimeZone(time_utc, 'Asia/Yekaterinburg') AS time_yekat,
    toTypeName(time_yekat) AS type_yekat,
    toInt32(time_yekat) AS int32yekat,
    toTimeZone(time_utc, 'US/Samoa') AS time_samoa,
    toTypeName(time_samoa) AS type_samoa,
    toInt32(time_samoa) AS int32samoa
FORMAT Vertical;
```


```Plain
Row 1:
──────
time_utc:   2019-01-01 00:00:00
type_utc:   DateTime('UTC')
int32utc:   1546300800
time_yekat: 2019-01-01 05:00:00
type_yekat: DateTime('Asia/Yekaterinburg')
int32yekat: 1546300800
time_samoa: 2018-12-31 13:00:00
type_samoa: DateTime('US/Samoa')
int32samoa: 1546300800
```


`toTimeZone(time_utc, 'Asia/Yekaterinburg')` changes the type from `DateTime('UTC')` to `DateTime('Asia/Yekaterinburg')`. The value (Unixtimestamp) 1546300800 remains unchanged, but the string representation (result of toString() function) changes from `time_utc: 2019-01-01 00:00:00` to `time_yekat: 2019-01-01 05:00:00`.

<span id="49372005"></span>
### toWeek

This function returns the number of weeks for a date or datetime. The two\-parameter form of toWeek() allows you to specify whether the week starts on Sunday or Monday and whether the return value should range from 0 to 53 or 1 to 53. If the mode parameter is omitted, the default mode is 0. `toISOWeek()` is a compatible function equivalent to `toWeek(Date, 3)`.

The table below describes how the Mode parameters work.


|**Mode** |**The first day of the week** |**Scope** |**The first week is the first week...**  |
|---|---|---|---|
|0 |sunday |0\-53 |This year |
|1 |Monday |0\-53 |This year there are 4 or more days |
|2 |Sunday |1\-53 |This year has one Sunday |
|3 |monday |1\-53 |This year has 4 days or more |
|4 |sunday |0\-53 |This year has 4 days or more |
|5 |monday |0\-53 |This year contains one Monday |
|6 |Sunday |1\-53 |This year has 4 or more days |
|7 |Monday |1\-53 |This year contains one Monday |
|8 |sunday |1\-53 |contains 1 month 1 day |
|9 |monday |1\-53 |contains 1 month 1 day |


For Mode values meaning "the year contains 4 or more days," the Weeks are numbered according to ISO 8601:1988.


* If the week that contains January 1 has 4 or more days in the New Year, it is considered Week 1.

* Otherwise, it is the last week of the previous year, and the following week is Week 1.


For Mode values meaning "contains January 1," the week that contains January 1 is Week 1. It doesn't matter how many days of the New Year are in that week, even if it's just one day.

**Syntax**

```SQL
toWeek(date, [, mode][, Timezone])
```


**Parameters**


* `Date`– Date or Date\-Time.

* `Mode` – An optional parameter with a value range of [0,9], default is 0.

* `Timezone` – An optional parameter, behaves like any other conversion function.


**Return value**


* Number of weeks. UInt8


**Example**

```SQL
SELECT toDate('2016-12-27') AS date, toWeek(date) AS week0, toWeek(date,1) AS week1, toWeek(date,9) AS week9;
```


```Plain
┌─date───────┬─week0─┬─week1─┬─week9─┐
│ 2016-12-27 │ 52    │ 52    │ 1     │
└────────────┴───────┴───────┴───────┘
```


<span id="8512029b"></span>
### toYYYYMM

Converts a date or datetime to a UInt32 number containing the year and month numbers (YYYY \* 100 + MM).

**Syntax**

```SQL
toYYYYMM(date)
toYYYYMM(datetime)
```


**Param**


* `date/datetime` date/datetime


**Return value**


* Number that includes the year and month. UInt32


**Example**

```SQL
SELECT toYYYYMM(toDate('2021-08-12'))
```


```Plain
┌─toYYYYMM(toDate('2021-08-12'))─┐
│ 202108                         │
└────────────────────────────────┘
```


```SQL
SELECT toYYYYMM(toDateTime('2021-08-12 00:00:00'))
```


```Plain
┌─toYYYYMM(toDateTime('2021-08-12 00:00:00'))─┐
│ 202108                                      │
└─────────────────────────────────────────────┘
```


<span id="301ba0c0"></span>
### toYYYYMMDD

Converts a date or datetime to a UInt32 number containing the year, month, and day (YYYY \* 10000 + MM \* 100 + DD).

**Syntax**

```SQL
toYYYYMMDD(date)
toYYYYMMDD(datetime)
```


**Parameters**


* `date/datetime` date/datetime


**Return Value**


* Numerical date containing year, month, and day. UInt32


**Example**

```SQL
SELECT toYYYYMMDD(toDate('2021-08-12'))
```


```Plain
┌─toYYYYMMDD(toDate('2021-08-12'))─┐
│ 20210812                         │
└──────────────────────────────────┘
```


```SQL
SELECT toYYYYMMDD(toDateTime('2021-08-12 00:00:00'))
```


```Plain
┌─toYYYYMMDD(toDateTime('2021-08-12 00:00:00'))─┐
│ 20210812                                      │
└───────────────────────────────────────────────┘
```


<span id="2262c199"></span>
### toYYYYMMDDhhmmss

Converts a date or date with time into a UInt64 number that contains the year, month, day, hour, minute, and second (YYYY \* 10000000000 + MM \* 100000000 + DD \* 1000000 + hh \* 10000 + mm \* 100 + ss).

**Syntax**

```SQL
toYYYYMMDDhhmmss(date)
toYYYYMMDDhhmmss(datetime)
```


**Parameter**


* `date/datetime` date/date\-time


**Return Value**


* Numerical data including year, month, day, hour, minute, and second. UInt32


**Example**

```SQL
SELECT toYYYYMMDDhhmmss(toDate('2021-08-12'))
```


```Plain
┌─toYYYYMMDDhhmmss(toDate('2021-08-12'))─┐
│ 20210812000000                         │
└────────────────────────────────────────┘
```


```SQL
SELECT toYYYYMMDDhhmmss(toDateTime('2021-08-12 00:00:00'))
```


```Plain
┌─toYYYYMMDDhhmmss(toDateTime('2021-08-12 00:00:00'))─┐
│ 20210812000000                                      │
└─────────────────────────────────────────────────────┘
```


<span id="0a439a77"></span>
### toYear

Convert a date or datetime to a UInt16 number containing the year (AD).

**Syntax**

```SQL
toYear(date)
toYear(datetime)
```


**Parameters**


* `date/datetime` Date/Datetime


**Return Value**


* Convert a date or datetime to a UInt16 number containing the year (AD). UInt16


**Example**

```SQL
SELECT toYear(toDate('2021-08-12'))
```


```Plain
┌─toYear(toDate('2021-08-12'))─┐
│ 2021                         │
└──────────────────────────────┘
```


```SQL
SELECT toYear(toDateTime('2021-08-12 00:00:00'))
```


```Plain
┌─toYear(toDateTime('2021-08-12 00:00:00'))─┐
│ 2021                                      │
└───────────────────────────────────────────┘
```


<span id="06e8099b"></span>
### toYearWeek

Returns the year and week of the date. The year in the results may differ from the year of the first and last weeks of the date parameter.

The mode parameter works exactly like the mode parameter in toWeek(). For the single parameter syntax, use mode value 0.

`toISOYear()` is a compatible function equivalent to `intDiv(toYearWeek(date,3),100)`.

**Syntax**

```SQL
toYearWeek(date[,mode])
toYearWeek(datetime[,mode])
```


**Parameters**


* `Date/datetime` Date/Date and Time

* `Mode` Refer to the weekly mode.


**Return Value**


* The year and week of the date. UInt32


**Example**

```SQL
SELECT toDate('2016-12-27') AS date, toYearWeek(date) AS yearWeek0, toYearWeek(date,1) AS yearWeek1, toYearWeek(date,9) AS yearWeek9;
```


```Plain
┌─date───────┬─yearWeek0─┬─yearWeek1─┬─yearWeek9─┐
│ 2016-12-27 │ 201652    │ 201652    │ 201701    │
└────────────┴───────────┴───────────┴───────────┘
```


<span id="128fc493"></span>
### today

Accepts no parameters and returns the current date at a certain moment when the request is made.

Same as 'toDate(now())'.

**Syntax**

```SQL
today()
```


**Return Value**


* Date.


**Example**

```SQL
SELECT today()
```


<span id="f00c5a05"></span>
### to_days

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


`to_days` returns the number of days since the year 0 based on the specified `date`.

**Syntax**

```SQL
to_days(date)
```


**Parameter Type**


* `date`

   * Date to be converted to days

   * Date/Date32/Datetime/Datetime64

   * String


**Return Type**


* UInt64


**Example**

**Example 1:** 

```SQL
SELECT to_days(date '2024-07-21');
```


```Plain
┌─to_days(toDate('2024-07-21'))─┐
│                        739453 │
└───────────────────────────────┘
```


**Example 2:** 

```SQL
SELECT to_days('2024-07-21');
```


```Plain
┌─to_days('2024-07-21')─┐
│                739453 │
└───────────────────────┘
```


<span id="c7f49621"></span>
### to_seconds

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


`to_seconds` returns the number of seconds since the start of year 0, based on the given `expr`.

**Syntax**

```SQL
to_seconds(expr)
```


**Parameter Type**


* `expr`

   * Expression to be converted into seconds

   * Date/Date32/Datetime/Datetime64

   * String

   * Time


**Return type**


* UInt64


**Example**

**Example 1:** 

```SQL
SELECT to_seconds(date '2024-07-21');
```


```Plain
┌─to_seconds(toDate('2024-07-21'))─┐
│                      63888710400 │
└──────────────────────────────────┘
```


**Example 2:** 

```SQL
SELECT to_seconds(datetime '2024-07-21 12:13:14');
```


```Plain
┌─to_seconds(toDateTime('2024-07-21 12:13:14'))─┐
│                                   63888754394 │
└───────────────────────────────────────────────┘
```


<span id="be89300c"></span>
### unix_timestamp

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


`Unix timestamp` returns the number of seconds from '1970\-01\-01 00:00:00' UTC to the current time. `Unix_timestamp(date)` returns the number of seconds from '1970\-01\-01 00:00:00' UTC to the time specified by `date`.

**Syntax**

```SQL
unix_timestamp()
unix_timestamp(date)
```


**Parameter Types**


* `date`

   * Date or datetime expression to convert to UNIX timestamp

   * String

   * Date/Date32/Datetime/Datetime64


**Return Type**


* Int64


**Example**

**Example 1:** 

```SQL
SELECT unix_timestamp();
```


```Plain
┌─toUnixTimestamp()─┐
│        1721987167 │
└───────────────────┘
```


**Example 2:** 

```SQL
SELECT unix_timestamp(datetime '2024-07-21 12:13:14');
```


```Plain
┌─toUnixTimestamp(toDateTime('2024-07-21 12:13:14'))─┐
│                                         1721535194 │
└────────────────────────────────────────────────────┘
```


**Example 3:** 

```SQL
SELECT unix_timestamp(date '2024-07-21');
```


```Plain
┌─toUnixTimestamp(toDate('2024-07-21'))─┐
│                            1721491200 │
└───────────────────────────────────────┘
```


<span id="dd8e4f3a"></span>
### utc_date

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


`utc_date` returns the UTC date.

**Syntax**

```SQL
utc_date()
```


**Return type**


* Date


**Example**

```SQL
SELECT utc_date();
```


```Plain
┌─utc_date()─┐
│ 2024-07-26 │
└────────────┘
```


<span id="efb24558"></span>
### utc_time

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


`Return value` returns UTC Time.

**Syntax**

```SQL
utc_time()
```


**Return type**


* Time


**Example**

```SQL
SELECT utc_time();
```


```Plain
┌───utc_time()─┐
│ 09:49:58.000 │
└─────────────┘
```


<span id="df5720f8"></span>
### utc_timestamp

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


`utc_timestamp` returns UTC Timestamp.

**Syntax**

```SQL
utc_timestamp()
```


**Return Type**


* Datetime


**Example**

```SQL
SELECT utc_timestamp();
```


```Plain
┌──────UTCTimestamp()─┐
│ 2024-07-26 09:50:19 │
└─────────────────────┘
```


<span id="a2d1d2ce"></span>
### week

Alias for ToWeek

<span id="4f3ccf32"></span>
### weekday

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


`Weekday` returns the `date` as the day number of the week. Return value 0 = Monday, 1 = Tuesday, 2 = Wednesday, 3 = Thursday, 4 = Friday, 5 = Saturday, 6 = Sunday.

**Syntax**

```SQL
weekday(date)
```


**Type**


* `date`

   * Date/Date32/Datetime/Datetime64

   * String


**Return type**


* UInt8


**Example**

**Example 1:** 

```SQL
SELECT weekday(datetime '2024-07-21 00:09:00');
```


```Plain
┌─WEEKDAY(toDateTime('2024-07-21 00:09:00'))─┐
│                                          6 │
└────────────────────────────────────────────┘
```


**Example 2:** 

```SQL
SELECT weekday(date '2024-07-21');
```


```Plain
┌─WEEKDAY(toDate('2024-07-21'))─┐
│                             6 │
└───────────────────────────────┘
```


**Example 3:** 

```SQL
SELECT weekday('2024-07-21');
```


```Plain
┌─WEEKDAY('2024-07-21')─┐
│                     6 │
└───────────────────────┘
```


<span id="b6f20074"></span>
### weekofyear

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax. It is recommended to use in the relevant dialect.</div>


`weekofyear` returns the calendar week corresponding to the `date` with a value range of [1, 53]

**Syntax**

```SQL
weekofyear(date)
```


**Parameter Type**


* `date`

   * Date/Date32/Datetime/Datetime64

   * String


**Return Type**


* UInt64


**Example**

**Example 1:** 

```SQL
SELECT weekofyear(datetime '2024-07-21 09:00:00');
```


```Plain
┌─toWeekOfYear(toDateTime('2024-07-21 09:00:00'))─┐
│                                              29 │
└─────────────────────────────────────────────────┘
```


**Example 2:** 

```SQL
SELECT weekofyear(date '2024-07-21');
```


```Plain
┌─toWeekOfYear(toDate('2024-07-21'))─┐
│                                 29 │
└────────────────────────────────────┘
```


**Example 3:** 

```SQL
SELECT weekofyear('2024-07-21');
```


```Plain
┌─toWeekOfYear('2024-07-21')─┐
│                         29 │
└────────────────────────────┘
```


<span id="27eb0d4b"></span>
### year

alias of toYear

<span id="fcbfaca6"></span>
### yearweek

Returns the year and week of a date. The year in the result may differ from the year of the first and last week of that year in the date parameter.

The effect of the mode parameter is exactly the same as the mode parameter of toWeek(). For single\-parameter syntax, use mode value 0.

`toISOYear()` is a compatible function equivalent to `intDiv(toYearWeek(date,3),100)`.

**Syntax**

```SQL
toYearWeek(date[,mode])
```


**Param**


* `date/datetime` Date/Date and Time


**Return value**


* Rounds a date or date with time down to the first day of the ISO year. Date


**Example**

```SQL
SELECT toDate('2016-12-27') AS date, toYearWeek(date) AS yearWeek0, toYearWeek(date,1) AS yearWeek1, toYearWeek(date,9) AS yearWeek9;
```


```Plain
┌─date───────┬─yearWeek0─┬─yearWeek1─┬─yearWeek9─┐
│ 2016-12-27 │ 201652    │ 201652    │ 201701    │
└────────────┴───────────┴───────────┴───────────┘
```


<span id="3b57c03e"></span>
### yesterday

Accepts zero parameters and returns yesterday's date at some point during the execution of the request.

Same as ‘today() \- 1’.

**Grammar**

```SQL
yesterday()
```


**Return value**


* Date.


**Example**

```SQL
SELECT yesterday()
```
