---
title: "SQL Custom Query"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/SQL-Custom-Query"
---

<span id="_1-使用说明"></span>
# 1. Instructions for use

<span id="_1-1-基本用法"></span>
## 1.1 Basic Usage

```Plain
select event, event_time
from events
where event_date >= '2020-08-10'
and event_date <= '2020-08-18'
and event_time > 1597161600
limit 20;
The front-end displays 1000 items, and users can download 1000000 items.
```


<span id="_1-2-字段说明"></span>
## 1.2 Field Description

<span id="_1-2-1-events表"></span>
### 1.2.1 Events table

**The query range of this table is: user SSID/UUID, event, event properties, event user properties, all_value type of user properties and business object properties.** 


* stat_standard_id

   * Statistical caliber ID, SSID or UUID, depending on the statistical caliber of the app

* user_id

   * User ID, empty string when anonymous

* hash_uid

   * When joining with the users table, it is recommended to use hash_uid to improve join efficiency and speed up queries

* device_id

   * Device ID

* web_id

* event

   * event name

* event_date

   * Event date, any SQL is recommended to specify the event time, otherwise derive according to event_time

* event_time

   * Event occurrence timestamp, 10 digits

   * event_date is automatically derived if and only if event_time is used as a constraint; therefore time and server_time are not recommended

* time

   * Event timstamp, 10 digits in history, 13 digits now

* server_time

   * Server level received the timestamp of the event, 10 bits

* content

   * An overview of the behavior log, including basic information about events, event properties, and more

* [event_params.xxx](https://docs.byteplus.com/en/docs/490/event_params.xxx).yyy

   * Event property, the format is **event_params. Event name. Event property name** , at this time SQL will only query the data related to the event.

   * The event name can be omitted and written as **event_params. Event property name** . At this time, SQL will query all events.

* [user_profiles.xxx](https://docs.byteplus.com/en/docs/490/user_profiles.xxx)

   * User property in the format **user_profiles. User property name**

* [item_profiles.xxx](https://docs.byteplus.com/en/docs/490/item_profiles.xxx).yyyy

   * Business object properties in the format **item_profiles. Business object name. Business object property name**

* Map column

   * Contains string_params, int_params, float_params, string_array_params, etc., which correspond to the location after the event attributes of string (version), int (datetime), float, and list are dropped into the library. For example, the event attribute a of the list type can be obtained by mapElemet (string_array_params, 'a'), and the result is consistent with event_params.

   * Typical scenario of using map column: reported some event attributes that do not conform to the SQL specification, such as'wechat.uid ', there are points in this attribute, if event_params.' wechat.uid ' (for attribute names that do not conform to the SQL specification, custom queries will automatically add single quotes as identification), may cause query errors, but use mapElemet (string_params,' wechat.uid ') to query normally.

   * The drawbacks of using map columns: 1. The SQL editor needs to perceive the type of the event attribute; 2. If the attribute type changes, it is difficult for the SQL editor to grasp which map column should be queried in. At this point, you can check the content column first to determine what map column the corresponding attribute is in.

* Other fields


**Tip** : [event_params.xxx](https://docs.byteplus.com/en/docs/490/event_params.xxx).yyy, user_profiles.xxx, item_profiles.xxx.yyy three fields suggest aliasing, otherwise the query may have problems.

<span id="_1-2-2-users表"></span>
### 1.2.2 Users table

**The query range of this table is: user SSID/UUID, all_value/last_value type of user properties.** 


* stat_standard_id

   * Statistical caliber ID, with the same meaning as the events table

* user_id

   * user ID

* ssid

   * ssid

* device_id

* web_id

* last_active_date

   * Represents the last active time of the user, which can be understood as the last refresh time of the record in the users table. Currently supports "YYYY\-MM\-dd" and "YYYMMdd" formats, for example: last_active_date = '2020\-08\-10'.

   * When the events table and the users table are joined, the last_active_date is automatically derived according to the event_date limit of the events table; for example, if the query event is 2021\-08\-01, then the last_active_date will be derived to be greater than or equal to 2021\-08\-01 (because if the last_active_date is less than 2021\-08\-01, then the user must not have any events after 2021\-08\-01).

* user_profiles.xxxx

   * User property in the format **user_profiles. User property name**

   * all_value and last_value, but the values stored in the users table are the latest values; to query the historical values of user properties of all_value types, you can query in the events table.

* string_profiles，int_profiles，float_profiles， string_array_profiles。

   * Map columns, similar to the transaction table.

* Other fields


<span id="_1-2-3-items表"></span>
### 1.2.3 Items table

**The query range of this table is: all_value/last_value type of business object related information**


* item_name

   * business object name

* last_active_date

   * Represents the last refresh time of the business object property.

* hash_item_id

   * For joining transaction tables

* item_profiles.xxx.yyyy

   * Business object properties in the format **item_profiles. Business object name. Business object property name**

* string_profiles，int_profiles， float_profiles，string_array_profiles。

   * Map columns, similar to the transaction table.

* Other fields


<span id="_1-2-4-cohorts表"></span>
### 1.2.4 Cohorts table

**The query range of this table is: the user statistics contained in the sub\-group caliber id, hash_uid, sub\-group id, etc.** 


* stat_standard_id

   * Statistical caliber id

* hash_uid

   * The statistical aperture id is hashed, which is usually used for join and in subqueries, and the query speed is faster than stat_standard_id.

* cohort_id

   * grouping id

* Under the "metadata" tab, you can view all subgroup names, subgroup IDs, and subgroup numbers.

* Currently does not support querying the historical version of the cluster, so the current query through the cluster id is **the most recent successfully refreshed cluster, consistent with other advanced analysis scenarios.** 

    &nbsp;


<span id="_1-3-query-range"></span>
## 1.3 Query range


* Time frame: nearly a year (including today)

* Data scope: events, event properties, user properties, and business object properties.


<span id="_1-4-日期过滤"></span>
## 1.4 Date Filtering


* **For event_date and last_active_date, the following functions are currently supported. If you need other functions, you can give feedback to customer service.** 

   **Support function:** 

   subtractMonths,subtractWeeks,subtractDays

   addMonths, addWeeks, addDays

   toStartOfQuarter,toStartOfMonth,toStartOfISOYear,toMonday,toStartOfWeek

   Note: The toStartOfWeek function, when the mode is even, starts on Monday, otherwise it is Sunday.

   **Wrong usage:** 


```sql
select event from events where toMonth(event_date) = 9；

select event from events where subtractDays(event_date, 10) = '2021-09-20'；
```


In the above way, the custom query will prompt that the event_date cannot be derived.

**Correct usage:** 

```sql
select event from events where event_date >= subtractDays(today(), 10)；
```


<span id="_1-4-1-events表"></span>
### 1.4.1 Events table

In any case, it is strongly recommended to use event_date as a date filter, and for more precise time intervals, use event_date + event_time to limit.


* event_date


event_date indicates the date of the event, accurate to the day, can be used to speed up the query, the default default is the last 7 days (including today).

Currently only the format "YYYY\-MM\-dd" is supported, for example: event_date = '2020\-08\-10'.


* event_time


event_time represents the time of the event, a 10\-digit timestamp, accurate to the second, and can be used to provide a more accurate time interval.


* Time Zone


The event_date of the domestic station access application is UTC + 8 (East Eighth District) time, and the event_date of the international station access application is UTC (Zero Time Zone) time.

For example:

event_time = 1597273200, domestic station event_date '2020\-08\-13'

event_time = 1597273200, international station event_date '2020\-08\-12'

Domestic station access application: Check the events that occurred from 6:00 on August 10, 2020 to 14:00 on August 12, 2020 Beijing time

```Plain
select event
from events
where
event_time >= 1597010400
and event_time <= 1597212000
and event_date >= '2020-08-10'
and event_date <= '2020-08-12'
```


The international station accesses the application, and the time zone of the application is UTC time: check the events that occurred from 6:00 UTC on August 10, 2020 to 14:00 UTC on August 12, 2020

```Plain
select event
from events
where
event_time >= 1597039200
and event_time <= 1597240800
and event_date >= '2020-08-10'
and event_date <= '2020-08-12'
```


The international station accesses the application, and the time zone of the application is UTC + 7 time: Query the events that occurred from 6:00 UTC + 7 time on August 10, 2020 to 14:00 UTC + 7 time on August 12, 2020, which is equivalent to querying the events that occurred from 23:00 UTC time on August 9, 2020 to 7:00 UTC time on August 12, 2020:

```Plain
select event
from events
where
event_time >= 1597014000
and event_time <= 1597215600
and event_date >= '2020-08-09'
and event_date <= '2020-08-12'
```


**Note** : Whenever possible, it is recommended that you specify a start and stop time for event_date in SQL to speed up queries. If you don't add it, the SQL custom query feature automatically assembles time limits, which may produce data that is different from the time period you expected.

<span id="_1-4-2-users、items表"></span>
### 1.4.2 Users, items table

When joining the events table, last_active_date can be automatically derived from event_date, otherwise it is recommended that the user specify last_active_date range.

**Semantic example:** 


1. Check the gender of active users **after** August 10, 2020.


```sql
select user_profiles.gender from users where last_active_date >= '2020-08-10'
```



2. Check the gender of users who have done A events **before** August 10, 2020


```sql
select gender, hash_uid, user_id
    from events as table_a
            left join
            (   
                select hash_uid, user_profiles.gender as gender from users
                where user_profiles.gender is not null
            ) as table_b 
    on table_a.hash_uid == table_b.hash_uid
   where event_date <= '2020-08-10' and event = 'A'
    limit 500;
```


SQL does not specify a start event_date for the event, so the default start event_date is 365 days ago today, assumed to be '2019\-10\-11'. At this point, in the join clause, the default query last_active_date \> = '2019\-10\-11' users.

It is worth noting that the **typical misspelling** of this case is:

```sql
select gender, hash_uid, user_id
    from events as table_a
            left join
            (   
                select hash_uid, user_profiles.gender as gender from users
                where user_profiles.gender is not null where last_active_date <= '2020-08-10'
            ) as table_b 
    on table_a.hash_uid == table_b.hash_uid
   where event_date <= '2020-08-10'
    limit 500;
```


If a user enters last_active_date < = '2020\-08\-10', the semantics of the join clause becomes \- querying for users who had no events after August 10, 2020, rather than querying for users who had events before August 10, 2020.

<span id="_1-5-常用函数"></span>
## 1.5 Common functions


1. Approximate percentiles, quantiles, and approximate median


quantile(level)(expr)

parameter


* Level \- percentiles. Optional parameter, the recommended value range of level is [0.01, 0.99], and the default value is level = 0.5, which is the calculated median.

* Expr \- expression. Optional numeric, date, or time data types


Median (expr) is equivalent to quantile (0.5) (expr)

Note: This function uses Reservoir_sampling stochastic algorithm, so the results are approximate and non\-deterministic.

For example, in the order event of August 10, 2020, the percentiles are 0.2.

select quantile(0.2)(event_params.order.money) from events where event = 'order' and event_date = '2020\-08\-10' limit 1;


2. Variance function varSamp


Calculate `sigma ((x - x) ^ 2)/(n - 1)`, where `n`is the sample size and `x`is the average of `x`.

Example: Query the variance of the amount in the order event on August 10, 2020

select varSamp(event_params.order.money) from events where event = 'order' and event_date = '2020\-08\-10' limit 1;


3. conditional function if


Grammar:

SELECT if(cond, then, else)

If the condition cond evaluates to a non\-zero value, the result of the expression then is returned, and the result of the expression else, if present, is skipped. If cond is zero or NULL, the result of the then expression is skipped and the result of the else expression, if present, is returned. 、

Parameter:


* Cond: conditional expression

* Then: The expression returned when the condition is satisfied

* Else: The expression returned when the condition is not met


Example: Query the person who triggered event A more than event B between October 6 and 12, 2020.

```sql
select distinct user_unique_id
from (select user_unique_id as `user_unique_id`,
*if*(event = 'A', *count*(1), 0) as `event1_cnt`,
*if*(event = 'B', *count*(1), 0) as `event2_cnt`
from events
where event in ('A', 'B')
and event_date >= '2020-10-06'
and event_date <= '2020-10-12'
group by user_unique_id, event
limit 1000)
group by user_unique_id
having *sum*(event1_cnt) > *sum*(event2_cnt)
```



4. Array function arrayEnumerate (arr)


Returns an array of the same size as the source array, where each element represents the number of times the original array element corresponding to its subscript appears in the original array. Common usage is similar to the windowing function in hive row_number ()

Parameter:


* arr array


Example: Query the previous three times of different events from October 25 to November 1, 2020

```sql
select \*
from (
select event, time\_arr, row\_number
from (
select event,
*groupArray*(time) as time\_arr,
*arrayEnumerate*(time\_arr) as row\_number
from (select distinct event, event\_time as time
from events
where event\_date >= '2020-10-25'
and event\_date <= '2020-11-01'
order by time) a
group by event
)
array join
time\_arr
, row\_number
)
where row\_number <= 3;
```


Result set:


|Event |Time_arr |Row_number |
|---|---|---|
|wechat_unsubscribe |1603967567 |1 |
|wechat_unsubscribe |1603968269 |2 |
|wechat_unsubscribe |1603968275 |3 |
|goods_detail_view |1603469824 |1 |
|goods_detail_view |1603473124 |2 |
|goods_detail_view |1603479424 |3 |


Supplement:

This usage is similar to row_number () for HQL, which is written as:

select \*

from

(

select event,

row_number() over(partition by event order by event_time) as row_number

from events

) a

where a.row_number <= 3;

Similar functions:

arrayEnumerateUniq、arrayEnumerateDense


5. match、multiMatchAny、multiMatchAnyIndex


match(haystack, pattern)


* Hystack requires matching fields

* Pattern A regular expression that conforms to the RE2 syntax re2: https://github.com/google/re2/wiki/Syntax

* A return value of 0 indicates no match, and 1 indicates a match.


Example:

```Plain
select distinct user_profiles.user_id, multiMatchAny(user_profiles.user_id, ['^[0-9]*$', '^\d{10}$']) as is_match from events where event_date > '2021-03-01' limit 20;
```


Result set:


|user_profiles.user_id |is_match |
|---|---|
|209041 |1 |
|unknown |0 |


multiMatchAny(haystack, [pattern1, pattern2, ...])


* [Pattern1, pattern2,...] Any regular expression that conforms to the PCRE syntax.

* A return value of 0 indicates all matches, and 1 indicates at least one pattern match.

* This function matches faster when matching substrings.

* The haystack string needs to be less than 2 ^ 32 bytes.


multiMatchAnyIndex(haystack, [pattern1, pattern2, ...])


* Similar to multiMatchAny

* The return value is the index that matches haystack, the index starts at 1, and no match returns 0.


Example:

```Plain
select distinct user_profiles.user_id, multiMatchAnyIndex(user_profiles.user_id, ['^[0-9]*$', '^([a-zA-Z0-9_-]\.)+@[a-zA-Z0-9_-]+(\.[a-zA-Z0-9_-]+)+$', '(\.[a-zA-Z0-9_-]@)+']) as regex_index from events where event_date > '2021-03-01' limit 2;
```


Result set:


|user_profiles.user_id |regex_index |
|---|---|
|209041 |1 |
|[xxxx.xxx@xxx.com](http://xxxx.xxx@xxx.com/) |3 |
|[aaa@aaa.com](http://aaa@aaa.com/) |2 |
|unknown |0 |


<span id="_1-6-常见用法举例"></span>
## 1.6 Common usage examples

<span id="根据uuid查询用户在某一天的行为"></span>
### Query user behavior on a given day based on uuid

```Plain
select event
from events
where user_profiles.user_id = 'datafinder@datarangers.com'
and event_date = '2020-08-10'
limit 20
```


<span id="查询在某一时间段内的用户的某个事件的发生总量"></span>
### Query the total number of occurrences of a certain event for users in a certain time period

```Plain
select count(event)
from events
where
event = 'event_name'
and event_time > 1596988800
and event_time < 1597161600
limit 20
```


<span id="查询发生过行为1和行为2，但是没有发生过行为3的用户数"></span>
### Query the number of users who have experienced behavior 1 and behavior 2, but not behavior 3

```Plain
select count(distinct hash_uid)
from events
where
(event = 'event_1' or event = 'event_2' and event != 'event_3')
and event_time > 1596988800
and event_time < 1597161600
limit 20
```


<span id="查询用户的首次行为属性"></span>
### Query the user's first\-time behavior attributes

```Plain
select user_profiles.user_id, event_params.{event_name}.{event_param_name} from events
where event = 'sogo'
and event_date > '2020-01-01'
order by event_time desc
limit 10;
```


<span id="查询一段时间内用户购买数量分布情况"></span>
### Query the distribution of user purchases over a period of time

```Plain
select
case
when amount > 10 then 'x>10'
when amount >5 and amount <= 10 then '5<x<=10'
else 'x<=5'
end
from
(
select event_params.buy.amount as amount
from events
where event = '`buy`'
and event_date > '2020-06-01' and event_date < '2020-08-02'
limit 200
)
```


<span id="查询事件相关信息时，把分群作为条件"></span>
### When querying for event\-related information, use grouping as a condition

```sql
select event from events where hash_uid in (select hash_uid from cohorts where cohort_id = 154) and event_date = yesterday()
```


<span id="查询分群中用户的user-id"></span>
### Query the user_id of users in the cluster

```sql
select user_id from users where hash_uid in (select hash_uid from cohorts where cohort_id = 154) and last_active_date >= '2021-01-01'
```


<span id="_2-函数列表"></span>
# 2. Function List

See the function details: [Functions Overview](https://clickhouse.com/docs/reference/functions).

<span id="_3-错误类型"></span>
# 3. Type of error


|**Error** |**Severity** |**Modification proposal** |
|---|---|---|
|Please add a WHERE clause, otherwise the query may time out. |middle |Add a WHERE clause, otherwise the data from the past 7 days will be queried by default. |
|Lack of event_time or event_date time limit, default query data for the past 7 days. |middle |Add a event_date or event_time condition to the WHERE clause, otherwise the last 7 days are queried by default. |
|Multiple SQL entries were found, but only the first one was executed. |middle |Put the SQL statement that needs to be executed first, or comment out other SQL. (Supports/\*\*/multi\-line comments and \-\- single\-line comments.) |
|A character not supported by SQL has been ignored. |middle |Delete unsupported characters in the SQL query. |
|LIMIT clause is missing, up to 1000 items are returned. |middle |Add the LIMIT clause. |
|The maximum number of query results returned is 1000. |middle |The LIMIT clause is limited to 1000. |
|Table name {table_name} is incorrect, please check your SQL. |high |Change the table name to events. |
|Only data from the past 365 days can be queried. Data beyond this range will not be queried. |middle |Limit the query time to nearly 365 days. |
|The data you inquired about is not available in the past 365 days. |high |Limit the query time to nearly 365 days. |
|Up to 20 join clauses are supported, please check your SQL. |high |Reduce the number of JOIN clauses |
|Only SELECT statements are supported, please check your SQL. |high |Only the SELECT statement is retained. |
|No query statement, please check your SQL. |high |*  |
|SELECT \* queries are not supported. Please check your SQL. |high |Query only the columns that need to be queried. |
|Subqueries with more than 10 layers are not supported. Please check your SQL. |high |Reduce the number of subquery layers. |
|The column name {column} for the query does not exist, please check your SQL. |high |Checks whether the column name {column} is in the data table. |
|GROUP BY for up to 30 columns is supported, please check your SQL. |high |Reduce the number of columns after GROUP BY. |
|Table function {table_function} is not supported, please check your SQL. |high |Change the table name to events. |
|There is an unsupported function {function_name}, please check your SQL. |high |Check if the {function_name} is in the list of supported functions. If you need to use this function, please contact customer service. |
|SETTINGS is not supported. Please check your SQL. |middle |Delete the SETTINGS statement, otherwise it is ignored by default. |
|Error in query: |high |Modify your SQL statement according to {error_message}. |
|Up to 3 UNION ALL clauses are supported, please check your SQL. |high |Reduce the number of UNION ALL clauses |
|INTO OUTFILE is not supported, please check your SQL. |high |Delete the INTO OUTFILE clause. |
|FORMAT is not supported, please check your SQL. |high |Delete the FORMAT clause. |
|Unsupported time condition {time_condition}, please check your SQL. |high |event_time time conditions please use integer 10\-digit timestamp, event_date time conditions please use "YYYY\-MM\-dd", e.g. “2020\-08\-01”。 |
|Query concurrency exceeds the limit. |high |Reduce the concurrency of queries. If you have greater concurrency requirements, please contact customer service. |
|SQL has a syntax error: {syntax_error_msg}. |high |Correct SQL statements based on detailed syntax error information. |
|Use event_time as the event time, not {time_condition}. |high |Use event_time as the event time. |
|Please use {new_column} instead of {old_column}. |middle |high |
|Invalid time condition (details: {cause}). |high |Unwritten or problematic time conditions, such as event_date \> = '2020\-08\-05' and event_date = '2020\-08\-01' |
|Example: The time condition is invalid (details: The time limit is derived as empty). | | |
|Could not derive {target_condition}, please add {target_condition} constraint. |high |1. No event_date and no event_date restrictions |
|Example: Unable to derive event_date, please add event_date constraints. ||2. According to event_time, event_date cannot be derived, such as toDate (event_time) = today (). The derivation of the time function is not currently supported. |
|Please give {column} an alias, otherwise the query may report an error. |middle |For columns user_profiles.xxx, event_param.xxx.yyy, item_profiles .xxxx.yyy, it is recommended to alias, otherwise there may be an error. |


<span id="_4-常见查询错误"></span>
# 4. Common query errors


|**Error code** |**Error message** |**Common Error Causes** | |
|---|---|---|---|
|215 |xxxxxx is not under aggregate function and not in GROUP BY |SQL query columns are not in GROUP BY, for example: | |
|select event, user_profiles.user_id from events group by event; | | | |
| |Modify it to: | | |
|select event, user_profiles.user_id from events group by event, user_profiles.user_id; | | | |
| |Or: | | |
|select event, any(user_profiles.user_id) from events group by event; | | | |
| |43 |Illegal types of arguments （xxx, yyy）of function [equals |greater |
|The price attribute of the event buy is of type int, which should be | | | |
| |select event from events where event_param.buy.price != '1'; | | |
|Modify it to: | | | |
| |select event from events where event_param.buy.price != 1; | | |
|53 |ARRAY JOIN requires array argument |Type mismatch, for example: | |
|select *arrayJoin(event_params.force.$target_uuid_list)*  | | | |
| |62 |Syntax error: failed at position xxxx |Check for detailed errors, such as: |
|select event from events where event as e = 'app_launch' limit 20; | | | |
| |The error message is: | | |
|Query error: code: 62, detail_message: DB:: Exception DB :: Exception: Syntax error: failed at position 239: = 'app_launch') and (tea_app_id = 41514 and event_date \> = '2021\-03\-09' and event_date < = '2021\-03\-15') limit 20;. Expected one of: token, Comma. | | | |
| |After observation, it was found that the error occurred around \*\*= 'app_launch' \*\*. After investigation, it was found that the event as e syntax was wrong and should be changed to: | | |
|select event from events where event = 'app_launch' limit 20; | | | |
| |202 |Too many simultaneous queries. |The current database query is busy. Please try again later. |
|42 |Number of arguments for function xxxx doesn't match |The number of parameters does not match, for example: | |
|select least(user_profiles.user_id) from events limit 20; | | | |
| |The error message is: | | |
|Query error: code: 42, detail_message: DB:: Exc ep t ion DB :: Exc ep t ion: Number of arguments for function least doesn't match: passed 1, should be 2. | | | |
| |After querying the manual, it was found that the least function requires 2 parameters and returns the smaller of the two parameters. | | |
|* Specific function usage can be found https://clickhouse.com/docs/reference/functions | | | |
