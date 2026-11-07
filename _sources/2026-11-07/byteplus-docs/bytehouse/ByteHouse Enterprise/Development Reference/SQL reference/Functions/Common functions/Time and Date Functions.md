---
title: "Time and Date Functions"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/time-and-date-functions"
---

Supports time zones.
All time and date functions can accept a timezone parameter as the second optional argument. Example: Asia/Yekaterinburg. In this case, they use the specified time zone instead of the local (default) time zone.
SELECT toDateTime('2016-06-15 23:00:00') AS time, toDate(time) AS date_local, toDate(time, 'Asia/Yekaterinburg') AS date_yekat, toString(time, 'US/Samoa') AS time_samoa
```plaintext
┌────────────────time─┬─date_local─┬─date_yekat─┬─time_samoa──────────┐
│ 2016-06-15 23:00:00 │ 2016-06-15 │ 2016-06-16 │ 2016-06-15 09:00:00 │
└─────────────────────┴────────────┴────────────┴─────────────────────┘
```

Only supports time zones that are whole hours different from UTC.
<span id="totimezone"></span>
## toTimeZone
Converts a Date or DateTime to the specified time zone. Time zone is a property of the Date/DateTime type. The internal value (seconds) of table fields or result set columns does not change, but the type of the column changes, and its string representation also changes accordingly.
SELECT toDateTime('2019-01-01 00:00:00', 'UTC') AS time_utc, toTypeName(time_utc) AS type_utc, toInt32(time_utc) AS int32utc, toTimeZone(time_utc, 'Asia/Yekaterinburg') AS time_yekat, toTypeName(time_yekat) AS type_yekat, toInt32(time_yekat) AS int32yekat, toTimeZone(time_utc, 'US/Samoa') AS time_samoa, toTypeName(time_samoa) AS type_samoa, toInt32(time_samoa) AS int32samoa FORMAT Vertical;
```plaintext
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

`toTimeZone(time_utc, 'Asia/Yekaterinburg')` converts `DateTime('UTC')` type to `DateTime('Asia/Yekaterinburg')`. The internal value (Unix timestamp) 1546300800 remains unchanged, but the string representation (result of toString() function) is converted from `time_utc: 2019-01-01 00:00:00` to `time_yekat: 2019-01-01 05:00:00`.
<span id="toyear"></span>
## toYear
Converts Date or DateTime to a UInt16 type number containing the year number (AD).
<span id="toquarter"></span>
## toQuarter
Converts Date or DateTime to a UInt8 type number containing the quarter number.
<span id="tomonth"></span>
## toMonth
Convert Date or DateTime to a UInt8 number containing the month number (1-12).
<span id="todayofyear"></span>
## toDayOfYear
Convert Date or DateTime to a UInt16 number containing the day number of the year (1-366).
<span id="todayofmonth"></span>
## toDayOfMonth
Convert Date or DateTime to a UInt8 number containing the day number of the month (1-31).
<span id="todayofweek"></span>
## toDayOfWeek
Convert Date or DateTime to a UInt8 number indicating which day of the week it is, with Monday as 1 and Sunday as 7.
<span id="tohour"></span>
## toHour
Convert DateTime to a UInt8 containing the hour number in a 24-hour format (0-23). This function assumes that if the clock moves forward, it occurs at 2 AM for one hour, and if the clock is set back, it happens at 3 AM for one hour, although the changes do not always occur at these times - even in Moscow, the clock changes at different times twice.
<span id="tominute"></span>
## toMinute
Converts DateTime to a UInt8 number representing the minutes (0-59) within an hour.
<span id="tosecond"></span>
## toSecond
Converts DateTime to a UInt8 number representing the seconds (0-59) within a minute. Leap seconds are not included.
<span id="tounixtimestamp"></span>
## toUnixTimestamp
For DateTime argument: Converts the value to a UInt32 number—[Unix timestamp](https://en.wikipedia.org/wiki/Unix_time). For String argument: Converts the input string to date and time according to the time zone (second parameter optional, default is server's time zone), and returns the corresponding Unix timestamp.
Syntax
toUnixTimestamp(datetime) toUnixTimestamp(str, [timezone])
Return Value

* Returns UNIX timestamp.

Type: `UInt32`.
Example
Query:
```SQL
SELECT toUnixTimestamp('2017-11-05 08:07:47', 'Asia/Tokyo') AS unix_timestamp
```

Result:
<span id="tostartofyear"></span>
## ```plaintext
┌─unix_timestamp─┐
│     1509836867 │
└────────────────┘
```

<span id="tostartofyear"></span>
## toStartOfYear
Rounds a Date or DateTime to the first day of the year. Returns Date type.
<span id="tostartofisoyear"></span>
## toStartOfISOYear
Round Date or DateTime down to the first day of the ISO year. Returns Date type.
<span id="tostartofquarter"></span>
## toStartOfQuarter
Round Date or DateTime down to the first day of the current quarter. Returns Date type.
<span id="tostartofmonth"></span>
## toStartOfMonth
Round Date or DateTime down to the first day of the current month. Returns Date type.
:::warning
The behavior of incorrectly parsing dates is implementation-specific. ClickHouse may return a zero date, throw an exception, or perform a "natural" overflow.
:::
<span id="tomonday"></span>
## toMonday
Round Date or DateTime down to the Monday of this week. Returns a Date type.
<span id="tostartofweek-t-mode"></span>
## toStartOfWeek(t[,mode])
Round Date or DateTime down to the nearest Sunday or Monday depending on the mode. Returns a Date type. The mode parameter works the same way as the mode parameter in toWeek(). For the single-parameter syntax, the mode uses a default value of 0.
<span id="tostartofday"></span>
## toStartOfDay
Round DateTime down to the start of today.
<span id="tostartofhour"></span>
## toStartOfHour
Round DateTime to the start of the current hour.
<span id="tostartofminute"></span>
## toStartOfMinute
Round DateTime to the start of the current minute.
<span id="tostartofsecond"></span>
## toStartOfSecond
Round DateTime to the start of the current second.
Syntax
toStartOfSecond(value[, timezone])
Parameters

* `value` — Date and time [DateTime64](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/en/sql-reference/data-types/datetime64.md).
* `timezone` — The [Timezone](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/en/operations/server-configuration-parameters/settings.md#server_configuration_parameters-timezone) of the return value (optional parameter). If the time zone is not specified, the `value` parameter's time zone will be used. [String](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/en/sql-reference/data-types/string.md).

Return Value

* The millisecond part of the input value is zero.

Type: [DateTime64](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/en/sql-reference/data-types/datetime64.md).
Example
Query without specifying time zone:
WITH toDateTime64('2020-01-01 10:20:30.999', 3) AS dt64 SELECT toStartOfSecond(dt64);
Result:
```plaintext
┌───toStartOfSecond(dt64)─┐
│ 2020-01-01 10:20:30.000 │
└─────────────────────────┘
```

Query specifying time zone:
WITH toDateTime64('2020-01-01 10:20:30.999', 3) AS dt64 SELECT toStartOfSecond(dt64, 'Europe/Moscow');
Result:
```plaintext
┌─toStartOfSecond(dt64, 'Europe/Moscow')─┐
│                2020-01-01 13:20:30.000 │
└────────────────────────────────────────┘
```

Reference

* [Timezone](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/en/operations/server-configuration-parameters/settings.md#server_configuration_parameters-timezone) server configuration options.

<span id="tostartoffiveminute"></span>
## toStartOfFiveMinute
Rounds DateTime to the nearest time point in five-minute increments.
<span id="tostartoftenminutes"></span>
## toStartOfTenMinutes
Rounds DateTime to the nearest time point in ten-minute increments.
<span id="tostartoffifteenminutes"></span>
## toStartOfFifteenMinutes
Rounds DateTime to the nearest time point in fifteen-minute increments.
<span id="tostartofinterval-time-or-data-间隔x单位-time-zone"></span>
## toStartOfInterval(time_or_data, interval x unit[,time_zone])
This is a common function for all functions named `toStartOf*`. For example:

* `toStartOfInterval(t, INTERVAL 1 year)` returns the same result as `toStartOfYear(t)`.
* `toStartOfInterval(t, INTERVAL 1 month)` returns the same result as `toStartOfMonth(t)`.
* `toStartOfInterval(t, INTERVAL 1 day)` returns the same result as `toStartOfDay(t)`.
* `toStartOfInterval(t, INTERVAL 15 minutes)` returns the same result as `toStartOfFifteenMinutes(t)`.

<span id="totime"></span>
## toTime
Converts the date in DateTime to a fixed date, while retaining the time portion.
<span id="torelativeyearnum"></span>
## toRelativeYearNum
Convert Date or DateTime to a year number, starting from a fixed point in the past.
<span id="torelativequarternum"></span>
## toRelativeQuarterNum
Convert Date or DateTime to a quarter number, starting from a fixed point in the past.
<span id="torelativemonthnum"></span>
## toRelativeMonthNum
Convert Date or DateTime to a month number, starting from a fixed point in the past.
<span id="torelativeweeknum"></span>
## toRelativeWeekNum
Convert Date or DateTime to a week number, starting from a fixed point in the past.
<span id="torelativedaynum"></span>
## toRelativeDayNum
Convert Date or DateTime to the number of the current day, starting from a fixed point in the past.
<span id="torelativehournum"></span>
## toRelativeHourNum
Convert DateTime to hour count, starting from a fixed point in the past.
<span id="torelativeminutenum"></span>
## toRelativeMinuteNum
Convert DateTime to minute count, starting from a fixed point in the past.
<span id="torelativesecondnum"></span>
## toRelativeSecondNum
Convert DateTime to second count, starting from a fixed point in the past.
<span id="toisoyear"></span>
## toISOYear
Convert Date or DateTime to a UInt16 type number containing the ISO year.
<span id="toisoweek"></span>
## toISOWeek
Convert Date or DateTime to a UInt8 type number containing the ISO week number.
<span id="toweek-date-mode"></span>
## toWeek(date[,mode])
Returns the week number of a Date or DateTime. The two parameter forms can specify whether the week starts on Sunday or Monday, and whether the returned value ranges between 0 to 53 or from 1 to 53. If the mode parameter is omitted, the default mode is 0. `toISOWeek()` is a compatibility function, equivalent to `toWeek(date,3)`. The table below describes how the mode parameter works.

| | | | | \
|Mode |First day of week |Range |Week 1 is the first week … |
|---|---|---|---|
| | | | | \
|0 |Sunday |0-53 |with a Sunday in this year |
| | | | | \
|1 |Monday |0-53 |with 4 or more days this year |
| | | | | \
|2 |Sunday |Jan-53 |with a Sunday in this year |
| | | | | \
|3 |Monday |Jan-53 |with 4 or more days this year |
| | | | | \
|4 |Sunday |0-53 |with 4 or more days this year |
| | | | | \
|5 |Monday |0-53 |with a Monday in this year |
| | | | | \
|6 |Sunday |Jan-53 |with 4 or more days this year |
| | | | | \
|7 |Monday |Jan-53 |with a Monday in this year |
| | | | | \
|8 |Sunday |Jan-53 |contains January 1 |
| | | | | \
|9 |Monday |Jan-53 |contains January 1 |

For mode values like "with 4 or more days this year," weeks are numbered according to ISO 8601: 1988:

* If the week containing January 1 has four or more days in the subsequent year, it is considered week 1.
* Otherwise, it is the last week of the previous year, and the following week is week 1.

For mode values like "contains January 1," the week that includes January 1 is the first week of the year.
toWeek(date, [, mode][, Timezone])
Parameter

* `Date` – Date or DateTime.
* `Mode` – Optional parameter, range [0,9], default 0.
* `Timezone` – Optional parameter, consistent with other date and time conversion parameters.

Example
SELECT toDate('2016-12-27') AS date, toWeek(date) AS week0, toWeek(date,1) AS week1, toWeek(date,9) AS week9;
<span id="toyearweek-date-mode"></span>
## ```plaintext
┌───────date─┬─week0─┬─week1─┬─week9─┐
│ 2016-12-27 │    52 │    52 │     1 │
└────────────┴───────┴───────┴───────┘
```

<span id="toyearweek-date-mode"></span>
## toYearWeek(date[,mode])
Returns the year and week of the Date. The year in the results may differ from the Date's year due to the Date being in the first or last week of the year.
The working mode of the mode parameter is exactly the same as the mode parameter in toWeek(). For single-parameter syntax, the mode uses the default value 0.
`toISOYear()` is a compatibility function equivalent to `intDiv(toYearWeek(date,3),100)`.
Example
SELECT toDate('2016-12-27') AS date, toYearWeek(date) AS yearWeek0, toYearWeek(date,1) AS yearWeek1, toYearWeek(date,9) AS yearWeek9;
<span id="date-trunc"></span>
## ```plaintext
┌───────date─┬─yearWeek0─┬─yearWeek1─┬─yearWeek9─┐
│ 2016-12-27 │    201652 │    201652 │    201701 │
└────────────┴───────────┴───────────┴───────────┘
```

<span id="date-trunc"></span>
## date_trunc
Rounds a Date or DateTime to the nearest time point by the specified unit.
Syntax
date_trunc(unit, value[, timezone])
Alias: `dateTrunc`.
Parameters

* `Unit` — Unit. [String](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/en/sql-reference/syntax.md#syntax-string-literal). Possible values:
   * `second`
   * `minute`
   * `hour`
   * `day`
   * `week`
   * `month`
   * `quarter`
   * `year`
* `Value` — [DateTime](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/en/sql-reference/data-types/datetime.md) or [DateTime64](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/en/sql-reference/data-types/datetime64.md).
* `Timezone` — [Timezone name](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/en/operations/server-configuration-parameters/settings.md#server_configuration_parameters-timezone) Return value's timezone (optional). If not specified, the timezone of the `value` will be used. [String](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/en/sql-reference/data-types/string.md).

Return value

* DateTime rounded to the specified unit.

Type: [Datetime](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/en/sql-reference/data-types/datetime.md).
Example
Query without specifying a timezone:
SELECT now(), date_trunc('hour', now());
Result:
```plaintext
┌───────────────now()─┬─date_trunc('hour', now())─┐
│ 2020-09-28 10:40:45 │       2020-09-28 10:00:00 │
└─────────────────────┴───────────────────────────┘
```

Query with specified time zone:
SELECT now(), date_trunc('hour', now(), 'Europe/Moscow');
Result:
```plaintext
┌───────────────now()─┬─date_trunc('hour', now(), 'Europe/Moscow')─┐
│ 2020-09-28 10:46:26 │                        2020-09-28 13:00:00 │
└─────────────────────┴────────────────────────────────────────────┘
```

Reference: 

* [toStartOfInterval](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/en/sql-reference/data-types/datetime.md)

<span id="2f7db4ad"></span>
## now
Returns the current date and time.
Syntax
now([timezone])
Parameter

* `timezone` — [Timezone name](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/zh/operations/server-configuration-parameters/settings.md#server_configuration_parameters-timezone) specifies the timezone for the result (optional parameter). [String](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/en/sql-reference/data-types/string.md).

Return Value

* Current date and time.

Type: [Datetime](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/en/sql-reference/data-types/datetime.md).
Example
Query without specifying timezone:
SELECT now();
Result:
```plaintext
┌───────────────now()─┐
│ 2020-10-17 07:42:09 │
└─────────────────────┘
```

Specified Time Zone Query:
SELECT now('Europe/Moscow');
Result:
<span id="today"></span>
## ```plaintext
┌─now('Europe/Moscow')─┐
│  2020-10-17 10:42:23 │
└──────────────────────┘
```

<span id="today"></span>
## today
It does not accept any parameters and returns the current date (Date) at the moment the request is executed. Its function is the same as 'toDate(now())'.
<span id="yesterday"></span>
## yesterday
It does not accept any parameters and returns yesterday’s date (Date) at the moment the request is executed. Its function is the same as 'today() - 1'.
<span id="timeslot"></span>
## timeSlot
Round the time to the nearest half hour. This feature is used in Yandex.Metrica because if the tracking tag shows that a single user's continuous comprehensive page views strictly exceed this number in time, half an hour is the shortest time to split the session into two sessions. This means that (tag id, user id, time slot) can be used to search for the comprehensive page views contained in the corresponding session.
<span id="toyyyymm"></span>
## toYYYYMM
Convert Date or DateTime into a UInt32 type number containing the year and month numbers (YYYY * 100 + MM).
<span id="toyyyymmdd"></span>
## toYYYYMMDD
Convert Date or DateTime into a UInt32 type number containing the year, month, and day numbers (YYYY * 10000 + MM * 100 + DD).
<span id="toyyyymmddhhmmss"></span>
## toYYYYMMDDhhmmss
Convert Date or DateTime into a UInt64 type number containing the year, month, day, hour, minute, and second numbers (YYYY * 10000000000 + MM * 100000000 + DD * 1000000 + hh * 10000 + mm * 100 + ss).
<span id="addyears-addmonths-addweeks-adddays-addhours-addminutes-addseconds-addquarters"></span>
## addYears, addMonths, addWeeks, addDays, addHours, addMinutes, addSeconds, addQuarters
The function adds a time interval to a Date/DateTime and then returns the Date/DateTime. For example:
WITH toDate('2018-01-01') AS date, toDateTime('2018-01-01 00:00:00') AS date_time SELECT addYears(date, 1) AS add_years_with_date, addYears(date_time, 1) AS add_years_with_date_time
<span id="subtractyears-subtractmonths-subtractweeks-subtractdays-subtractours-subtractminutes-subtractseconds-subtractquarters"></span>
## ```plaintext
┌─add_years_with_date─┬─add_years_with_date_time─┐
│          2019-01-01 │      2019-01-01 00:00:00 │
└─────────────────────┴──────────────────────────┘
```

<span id="subtractyears-subtractmonths-subtractweeks-subtractdays-subtractours-subtractminutes-subtractseconds-subtractquarters"></span>
## subtractYears,subtractMonths,subtractWeeks,subtractDays,subtractours,subtractMinutes,subtractSeconds,subtractQuarters
The function subtracts a time interval from a Date/DateTime and then returns the Date/DateTime. For example:
WITH toDate('2019-01-01') AS date, toDateTime('2019-01-01 00:00:00') AS date_time SELECT subtractYears(date, 1) AS subtract_years_with_date, subtractYears(date_time, 1) AS subtract_years_with_date_time
<span id="datediff"></span>
## ```plaintext
┌─subtract_years_with_date─┬─subtract_years_with_date_time─┐
│               2018-01-01 │           2018-01-01 00:00:00 │
└──────────────────────────┴───────────────────────────────┘
```

<span id="datediff"></span>
## dateDiff
Returns the time difference between two Dates or DateTimes.
Syntax
dateDiff('unit', startdate, enddate, [timezone])
Parameters

* `unit` — The time unit of the returned result. [String](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/en/sql-reference/syntax.md#syntax-string-literal).

```plaintext
Supported time units: second, minute, hour, day, week, month, quarter, year.
```


* `startdate` — The first value for comparison. [Date](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/en/sql-reference/data-types/date.md) or [DateTime](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/en/sql-reference/data-types/datetime.md).
* `enddate` — The second value for comparison. [Date](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/en/sql-reference/data-types/date.md) or [DateTime](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/en/sql-reference/data-types/datetime.md).
* `timezone` — Optional parameter. If specified, it applies to both `startdate` and `enddate`. If not specified, the time zones of `startdate` and `enddate` are used. If the two time zones are inconsistent, the result is unpredictable.

Return Value
The difference between `unit`, `startdate`, and `enddate`.
Type: `int`.
Example
Query:
SELECT dateDiff('hour', toDateTime('2018-01-01 22:00:00'), toDateTime('2018-01-02 23:00:00'));
Result:
<span id="timeslots-starttime-duration-size"></span>
## ```plaintext
┌─dateDiff('hour', toDateTime('2018-01-01 22:00:00'), toDateTime('2018-01-02 23:00:00'))─┐
│                                                                                     25 │
└────────────────────────────────────────────────────────────────────────────────────────┘
```

<span id="timeslots-starttime-duration-size"></span>
## timeSlots(StartTime, Duration,[, Size])
It returns a time array, which covers all the times in steps of «size» seconds from «StartTime» to «StartTime + Duration seconds». «size» is an optional parameter, with the default being 1800. For example, `timeSlots(toDateTime('2012-01-01 12:20:00'), 600) = [toDateTime('2012-01-01 12:00:00'), toDateTime('2012-01-01 12:30:00')]`. This is very useful for analyzing aggregate views in corresponding sessions.
<span id="formatdatetime"></span>
## formatDateTime
The function formats time according to a given format string. Please note: the format string must be a constant expression, for example, a single result column cannot have multiple format strings.
Syntax
formatDateTime(Time, Format\[, Timezone\])
Return Value
The date and time formatted according to the specified format.
Supported Format Modifiers
Use format modifiers to specify the style of the result string. The "Example" column shows the formatting result for `2018-01-02 22:33:44`.

| | | | \
|Modifier |Description |Example |
|---|---|---|
| | | | \
|%C |Year divided by 100 and truncated to integer (00-99) |20 |
| | | | \
|%d |Day of the month, zero-padded (01-31) |2 |
| | | | \
|%D |Short date MM/DD/YY, equivalent to %m/%d/%y |1/2/2018 |
| | | | \
|%e |Day of the month with space padding (1-31). |2 |
| | | | \
|%F |Short YYYY-MM-DD date format, equivalent to %Y-%m-%d. |2018-01-02 |
| | | | \
|%G |The four-digit year format for ISO week numbers, defined by [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601#Week_dates), is calculated based on the week-based year and is usually only useful for %V. |2018 |
| | | | \
|%g |The two-digit year format, consistent with ISO 8601, is an abbreviation for the four-digit representation. |18 |
| | | | \
|%H |24-hour format (00-23) |22 |
| | | | \
|%I |12-hour format (01-12) |10 |
| | | | \
|%j |One day of the year (001-366) |2 |
| | | | \
|%m |Month as a decimal number (01-12) |1 |
| | | | \
|%M |Minutes (00-59) |33 |
| | | | \
|%n |Line break (") | |
| | | | \
|%p |AM or PM designation |PM |
| | | | \
|%Q |Quarter (1-4) |1 |
| | | | \
|%R |24-hour HH:MM time, equivalent to %H:%M |22:33 |
| | | | \
|%S |Second (00-59) |44 |
| | | | \
|%t |Horizontal Tab (') | |
| | | | \
|%T |ISO8601 Time Format (HH:MM:SS), equivalent to %H:%M:%S |22:33:44 |
| | | | \
|%u |ISO8601 Weekday as a Number, with Monday as 1 (1-7) |2 |
| | | | \
|%V |ISO8601 Week Number (01-53) |1 |
| | | | \
|%w |Weekday as a decimal number, Sunday as 0 (0-6) |2 |
| | | | \
|%y |Year, last two digits (00-99) |18 |
| | | | \
|%Y |year |2018 |
| | | | \
|%% |% symbol |% |

Example
Query:
```SQL
SELECT formatDateTime(toDate('2010-01-04'), '%g')
```

Result:
```plaintext
┌─formatDateTime(toDate('2010-01-04'), '%g')─┐
│ 10                                         │
└────────────────────────────────────────────┘
```

[Original article](https://clickhouse.tech/docs/en/query_language/functions/date_time_functions/)
<span id="c1355381"></span>
## FROM_UNIXTIME
When there is only a single integer parameter, it functions the same as `toDateTime` and returns a [DateTime](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/en/sql-reference/data-types/datetime.md) type.
For example:
```SQL
SELECT FROM_UNIXTIME(423543535)
```

```SQL
┌─FROM_UNIXTIME(423543535)─┐
│      1983-06-04 10:58:55 │
└──────────────────────────┘
```

When there are two parameters, the first is either an integer or DateTime, and the second is a constant format string, it functions the same as `formatDateTime` and returns a `String` type.
For example:
SELECT FROM_UNIXTIME(1234334543, '%Y-%m-%d %R:%S') AS DateTime
```SQL
┌─DateTime────────────┐
│ 2009-02-11 14:42:23 │
└─────────────────────┘
```
