---
title: "Custom SQL Query"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Custom_SQL_Query"
---

<span id="_1-使用说明"></span>
# 1. Instructions for use

<span id="_1-1-基本用法"></span>
## 1.1 Basic usage


* After viewing the relevant field names of the query table at the bottom of the page, manually enter the query SQL and query. See the Field Description section below for details of supported data tables and fields. Here is an example of the simplest query.

   ```SQL
   select event, event_time 
   from events 
   where event_date >= '2020-08-10' 
   and event_date <= '2020-08-18' 
   and event_time > 1597161600
   limit 20;
   ```
   

   The front end displays 1000 query results by default, and click the "**Download**" button on the result page to download 1000000 query result data.

* Support for manually adding dynamic parameters and then referencing them directly in query SQL. See the Dynamic Parameters section below for details.


<span id="_1-2-字段说明"></span>
## 1.2 Table field description

You can select the table you want to query in the data table page below the SQL custom query page. Currently, events, users, items, and cohorts tables are supported, and it is supported to quickly search through keywords in the search box in the upper right corner to view the field information in the corresponding table.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92ad9fe8e4594d0aadff21b87aa5feeb~tplv-goo7wpa0wc-image.image) </span>

The following describes the key fields in each table, and more other fields can be viewed in the interface.

<span id="_1-2-1-events表"></span>
### 1.2.1 Events table

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Formerly all_data table, now renamed events table.</div>



* **Table data scope: user SSID/UUID, event, event attributes, event public attributes, all_value types of public attributes and business object attributes.** 

* Table key field:

   
   |Field |Explain |
   |---|---|
   |stat_standard_id |* Statistical caliber ID, SSID or UUID, depending on the statistical caliber of the app.<br><br>* Listed as user_unique_id, now abandoned. |
   |user_profiles.user_id |* User ID, filled by device_id/web_id when anonymous; in the real\-name scenario, it is user_unique_id (uuid) value.<br><br>* Listed as user_profiles, now obsolete. |
   |hash_uid |When joining with the users table, it is recommended to use hash_uid to improve join efficiency and speed up queries. |
   |event |event name |
   |event_date |Event date, any SQL recommends specifying the event time, otherwise derive from event_time. |
   |event_time |* Event occurrence timestamp, 10 digits.<br><br>* event_date is automatically derived if and only if event_time is used as a constraint; therefore time and server_time are not recommended. |
   |time |Event occurrence timestamp, history is 10, now 13. |
   |server_time |The server level received the timestamp of the event, 10 bits. |
   |event_params.xxx.yyy |* Event property, the format is **event_params. Event name. Event property name** , at this time SQL will only query the data related to the event.<br><br>* The event name can be omitted and written as **event_params. Event property name** . At this time, SQL will query all events. |
   |user_profiles.xxx |Public property in the format **user_profiles. Public property name** . user_profiles user_id user_unique_id in the corresponding product. |
   |item_profiles.xxx.yyyy |* Business object properties in the format **item_profiles. Business object name. Business object property name** .<br><br>* The values found are of array type, and the FAQ can be seen for the usage method. |
   

* Query example:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fd9c66fb85264bc5810b1bfa9d83718d~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">event_params.xxx .Yyy, user_profiles.xxx , item_profiles.xxx .yyy three fields suggest aliasing, otherwise the query may have problems.   </div>
   

<span id="_1-2-2-users表"></span>
### 1.2.2 Users table


* **Table query range: common properties of user SSID/UUID, all_value/last_value types and business object properties.** 

* Table key field:

   
   |Field |Explain |
   |---|---|
   |ssid |ssid |
   |stat_standard_id |The statistical caliber ID has the same meaning as the events table. |
   |user_id |User ID field, the query result is the reported user_unique_id (uuid) data. |
   |last_active_date |* Represents the last active time of the user, which can be understood as the last refresh time of the record in the users table. Currently supports "YYYY\-MM\-dd" and "YYYMMdd" formats, for example: last_active_date = '2020\-08\-10'.<br><br>* When the events table and the users table are joined, the last_active_date is automatically derived according to the event_date limit of the events table; for example, if the query event is 2021\-08\-01, then the last_active_date will be derived to be greater than or equal to 2021\-08\-01 (because if the last_active_date is less than 2021\-08\-01, then the user must not have any events after 2021\-08\-01).<br><br><br>When querying the user table, use last_active_date for where filtering, otherwise the query may report an error. |
   |user_profiles.xxxx |* Public property in the format **user_profiles. Public property name**.<br><br>* all_value and last_value, but the values stored in the users table are the latest values; to query the historical values of public properties of all_value types, you can query in the events table. |
   

* Query example

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e0ecbea0286148cb824637167dd5e7ec~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">user_profiles.xxx The field suggests an alias, otherwise there may be a problem with the query.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When querying, you need to use the last_active_date field for where filtering, otherwise the query may report an error.   </div>
   


<span id="_1-2-3-items表"></span>
### 1.2.3 Items table


* **Table query range: all_value/last_value type of business object related information** .

* Key field:

   
   |field |explain |
   |---|---|
   |item_name |Business object name. |
   |last_active_date |Represents the last refresh time of the business object property. |
   |item_profiles.xxx.yyyy |Business object properties in the format **item_profiles. Business object name. Business object property name** . |
   

* Query example

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/61b57e09812a4ce7808cdca4096194de~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">user_profiles.xxx The field suggests an alias, otherwise there may be a problem with the query.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When querying, you need to use the last_active_date field for where filtering, otherwise the query may report an error.   </div>
   


<span id="_1-2-4-cohorts表"></span>
### 1.2.4 Cohorts table


* **The query range of the table is: the user statistics contained in the cluster caliber id, hash_uid, sub\-group id, etc** .

* Key field:

   
   |Field |Explain |
   |---|---|
   |stat_standard_id |Statistical caliber id. |
   |hash_uid |The statistical aperture id is hashed, which is usually used for join and in subqueries, and the query speed is faster than stat_standard_id. |
   |cohort_id |Grouping ID. |
   

* Query example

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6422e192ed90412db824fb16a3db38ff~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When querying, it is recommended to specify clusters by cohort_id = x or cohort_id in (x, y,...), otherwise the query may report an error.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When you use the cohort_id field for where filtering to specify a user cluster, you can view the cluster ID of the corresponding cluster in the metadata page.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Currently does not support querying the historical version of the cluster, so the current query through the cluster id is <strong>the latest successful refresh of the cluster, and other advanced analysis scenarios.</strong>   </div>
   


<span id="_1-3-查询范围"></span>
## 1.3 Query data limitations


* Time frame: nearly a year (including today)

* Data scope: events, event properties, public properties, and business object properties.


<span id="_1-4-日期过滤"></span>
## 1.4 Date filtering

**For event_date and last_active_date, the following functions are currently supported. If you need other functions, you can give feedback to customer service.** 

<span id="fe79584a"></span>
### 1.4.1 Date filter

<span id="fe997445"></span>
#### **Method 1: Time dynamic parameter filtering**

After adding the time dynamic parameter below the SQL code box, you can use the dynamic parameter method for time filtering.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fac223032c67486dad63e8ed9e559295~tplv-goo7wpa0wc-image.image) </span>

```SQL
select stat_standard_id from events  where ${event_date:date1} limit 50;
-- where ${event_date: date1} is the added time dynamic parameter
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After using the time dynamic parameter and saving the query results to Kanban, the data of the saved SQL custom query chart will also change after adjusting the Kanban time filter in Kanban.</div>


<span id="3ca517f4"></span>
#### Method 2: Function Filtering


* **Support function:** 

   subtractMonths,subtractWeeks,subtractDays

   addMonths, addWeeks, addDays

   toStartOfQuarter,toStartOfMonth,toStartOfISOYear,toMonday,toStartOfWeek

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">toStartOfWeek function, when mode is even, starts on Monday, otherwise Sunday.   </div>
   

* **Wrong usage:** 

   ```sql
   select event from events where toMonth(event_date) = 9；
   select event from events where subtractDays(event_date, 10) = '2021-09-20'；
   
   ```
   

   In the above way, the custom query will prompt that the event_date cannot be derived.

* **Correct usage:** 

   ```sql
   select event from events where event_date >= subtractDays(today(), 10)；
   
   ```
   


<span id="_1-4-1-events表"></span>
### 1.4.2 Date filtering for the events table

In any case, it is strongly recommended to use event_date as the date filter, and for more precise time intervals, use event_date + event_time to limit.


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

```SQL
select event
from events 
where 
event_time >= 1597010400
and event_time <= 1597212000
and event_date >= '2020-08-10'
and event_date <= '2020-08-12'
```


The international station accesses the application, and the time zone of the application is UTC time: check the events that occurred from 6:00 UTC on August 10, 2020 to 14:00 UTC on August 12, 2020

```SQL
select event
from events 
where 
event_time >= 1597039200
and event_time <= 1597240800
and event_date >= '2020-08-10'
and event_date <= '2020-08-12'
```


The international station accesses the application, and the time zone of the application is UTC + 7 time: Query the events that occurred from 6:00 UTC + 7 time on August 10, 2020 to 14:00 UTC + 7 time on August 12, 2020, which is equivalent to querying the events that occurred from 23:00 UTC time on August 9, 2020 to 7:00 UTC time on August 12, 2020:

```SQL
select event
from events 
where 
event_time >= 1597014000
and event_time <= 1597215600
and event_date >= '2020-08-09'
and event_date <= '2020-08-12'
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Whenever possible, it is recommended that you specify the start and stop times of event_date in SQL to speed up your queries. If you don't add it, the SQL custom query feature automatically assembles time limits, which may produce data that is different from the time period you expected.</div>


<span id="_1-4-2-users、items表"></span>
### 1.4.3 Date filtering for users and items tables

When joining with the events table, last_active_date can be automatically derived from event_date, otherwise it is recommended that the user specify last_active_date range.

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


The SQL does not specify a start event_date for the event, so the default start event_date is 365 days ago today, assumed to be '2019\-10\-11'. At this point, in the join clause, the default query last_active_date \> = '2019\-10\-11' users.

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

<span id="7f326702"></span>
## 1.5 Dynamic parameters

Currently supports dynamic parameter function, supports variable content, numerical expressions, document expressions, and other types of dynamic parameters. You can add dynamic parameters as needed, and then directly reference them in the query SQL.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/94f68f876699466a871f2dab5086e230~tplv-goo7wpa0wc-image.image) </span>

<span id="98f6c1ce"></span>
### Variable content


* **Configuration Instructions** :

   Variable content dynamic parameters allow for the selection of specific times or custom input values, which can be replaced directly during calculations.

* **Example of use** :

   
   |Variable content value is custom |Variable content value is time |
   |---|---|
   |* `${variable1}`value is not customized: `1`<br><br>* SQL query reference code:<br><br>   ```SQL```<br>```   select user_id```<br>```   from events```<br>```   limit ${variable1}```<br>```   ```<br>   <br><br>* The actual query is equivalent to<br><br><br>```SQL```<br>```select user_id```<br>```from events```<br>```limit 1```<br> |* `${variable1}`is the value of time: `'2024-10-01 20:30:30'`<br><br>* SQL query reference code<br><br>   ```SQL```<br>```   select user_id```<br>```   from events```<br>```   where event_time >= ${variable1}```<br>```   ```<br>   <br><br>* The actual query is equivalent to<br><br>   ```SQL```<br>```   select user_id```<br>```   from events```<br>```   where event_time >= '2024-10-01 20:30:30'```<br>```   ```<br>    |
   


<span id="bc94ad7b"></span>
### Event time (event_date)


* **Configuration Instructions** :

   You can analyze event data over a period of time with a quick filter of event time dynamic parameters. Support setting whether the event time dynamic parameter is affected by the time zone, and select the time range of the event time dynamic parameter in the time selector.

* **Example of use** :

   * `${event_date: date1}`is set to: last 7 days

   * SQL query reference code:

      ```SQL
      select user_id 
      from events 
      where ${event_date:date1} 
      ```
      

   * The actual query is equivalent to the representative

      ```SQL
      select user_id 
      from events 
      where event_date >= subtractDays(yesterday(), 7) and event_date <= yesterday() 
      ```
      


<span id="190f396f"></span>
### Numerical/text/time expressions


* **Configuration instructions:** 

   When filtering three types of fields: numeric, text, and time, you can use expression dynamic parameters to configure them flexibly.

   
   |Numeric expression |Text expression |Time expression |
   |---|---|---|
   |* Parameter name: $<br><br>* Operator:<br><br>   * `=`(default)<br><br>   * `<>`<br><br>   * `>`<br><br>   * `<`<br><br>   * `>=`<br><br>   * `<=`<br><br>   * `scope`<br><br>   * `empty`<br><br>   * `Not empty` |* Parameter name: $<br><br>* Operator:<br><br>   * `= (default)`: Support multiple selection, equivalent to `in ( '','' )`<br><br>   * `< >`: Support multiple selection, which is equivalent to `not in ( '','' )`<br><br>   * `Contains`: Does not support multiple selection, equivalent to `lIke '% xx%'`<br><br>   * `Do not contain`: does not support multiple selection, equivalent to `not lIke '% xx%'`<br><br>   * `Is null`: equivalent to `is null`<br><br>   * `Not null`: equivalent to `is not null`<br><br>   * `Range`: Equivalent to `between'xxx 'and'yyy'`<br><br>   * `Custom include`: does not support multiple selection, equivalent to `lIke "'` |* Parameter name: $<br><br>* Operator:<br><br>   * `Date Range`: Equivalent to `between'yyyy-MM-dd 'and'yyyy-MM-dd'`<br><br>   * `Time Range`: Equivalent to `between'yyyy-MM-dd HH: MM: SS 'and'yyyy-MM-dd HH: MM: SS'`<br><br>   * `Greater than or equal to`: equivalent to `> = 'yyyy-MM-dd HH: MM: SS'`<br><br>   * `Less than or equal to`: equivalent to `< = 'yyyy-MM-dd HH: MM: SS'`<br><br>   * `Is null`: equivalent to `is null`<br><br>   * `Not null`: equivalent to `is not null` |
   

* **Example of use:** 

   
   |Numeric expression |Text expression |Time expression |
   |---|---|---|
   |* ${number1} \> 351<br><br>* SQL query reference code:<br><br>   ```SQL```<br>```   select user_id```<br>```   from events join```<br>```   where prop ${number1}```<br>```   ```<br>   <br><br>* The actual query is equivalent to:<br><br>   ```SQL```<br>```   select user_id```<br>```   from events```<br>```   where prop > 351```<br>```   ```<br>    |* ${text1} is not empty<br><br>* SQL query reference code:<br><br>   ```SQL```<br>```   select user_id```<br>```   from events```<br>```   where prop ${text1}```<br>```   ```<br>   <br><br>* The actual query is equivalent to:<br><br>   ```SQL```<br>```   select user_id```<br>```   from events```<br>```   where prop is not null```<br>```   ```<br>    |* ${time1} is less than or equal to 2024\-11\-19<br><br>* SQL query reference code:<br><br>   ```SQL```<br>```   select user_id```<br>```   from events```<br>```   where prop ${time1}```<br>```   ```<br>   <br><br>* The actual query is equivalent to:<br><br>   ```SQL```<br>```   select user_id```<br>```   from events```<br>```   where prop <= '2024-11-19'```<br>```   ```<br>    |
   


<span id="5a0ac371"></span>
### Selector (selector)


* **Configuration instructions:** 

   You can set different option names for the prepared statement fragment by selecting the item dynamic parameter. The viewer only needs to select according to the name, and the corresponding statement fragment will automatically replace the dynamic parameter.

* **Example of use:** 

   * ${selector1} is set to:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d9c018fc2d2c45a5acbcffc76c1234c7~tplv-goo7wpa0wc-image.image) </span>

      Advanced: \> = 1000; Intermediate: between 200 and 1000; Low: < = 200

   * SQL query reference code:

      ```SQL
      select user_id 
      from events 
      where prop ${selector1} 
      ```
      

   * ${selector1} When selecting **advanced** , the actual query is equivalent to:

      ```SQL
      select user_id 
      from events 
      where prop >= 1000
      ```
      


<span id="_1-5-常用函数"></span>
## 1.6 Common functions

<span id="ff0e86d4"></span>
### Approximate percentiles, quantiles, and approximate median

Quantile(level)(expr)

Parameter


* Level \- percentiles. Optional parameter, the recommended value range of level is [0.01, 0.99], and the default value is level = 0.5, which is the calculated median.

* Expr \- expression. Optional numeric, date, or time data types


Median (expr) is equivalent to quantile (0.5) (expr)

Note: This function uses Reservoir_sampling stochastic algorithm, so the results are approximate and non\-deterministic.

For example, in the order event of August 10, 2020, the percentiles are 0.2.

```Plain
select quantile(0.2)(event_params.order.money) from events where event = 'order' and event_date = '2020-08-10' limit 1;
```


<span id="c03d59c1"></span>
### Variance function varSamp

Calculate `sigma ((x - x) ^ 2)/(n - 1)`, where `n`is the sample size and `x`is the average of `x`.

Example: Query the variance of the amount in the order event on August 10, 2020

```Plain
select varSamp(event_params.order.money) from events where event = 'order' and event_date = '2020-08-10' limit 1;
```


<span id="fb257aca"></span>
### Conditional function if

Grammar:

```Plain
SELECT if(cond, then, else)
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the condition cond evaluates to a non\-zero value, the result of the expression then is returned, and the result of the expression else, if present, is skipped. If cond is zero or NULL, the result of the then expression is skipped and the result of the else expression, if present, is returned.</div>


Parameter:


* Cond: conditional expression

* Then: The expression returned when the condition is satisfied

* Else: The expression returned when the condition is not met


Example: Query the person who triggered event A more than event B between October 6 and 12, 2020.

```SQL
select distinct user_unique_id
from (select user_unique_id                      as `user_unique_id`,
           if(event = 'A', count(1), 0) as `event1_cnt`,
           if(event = 'B', count(1), 0) as `event2_cnt`
    from events
    where event in ('A', 'B')
      and event_date >= '2020-10-06'
      and event_date <= '2020-10-12'
    group by user_unique_id, event
    limit 1000)
group by user_unique_id
having sum(event1_cnt) > sum(event2_cnt)

```


<span id="8ff5a6a8"></span>
### Array function arrayEnumerate (arr)

Returns an array of the same size as the source array, where each element represents the number of times the original array element corresponding to its subscript appears in the original array. Common usage is similar to the windowing function in hive row_number ()

Parameter:


* arr array

   Example: Query the previous three times of different events from October 25 to November 1, 2020


```SQL
select *
from (
select event, time_arr, row_number
from (
select event,
groupArray(time) as time_arr,
arrayEnumerate(time_arr) as row_number
from (select distinct event, event_time as time
from events
where event_date >= '2020-10-25'
and event_date <= '2020-11-01'
order by time) a
group by event
)
array join
time_arr
, row_number
)
where row_number <= 3;
```


Result set:

```SQL
| event | time_arr | row_number |
| --- | --- | --- |
| wechat_unsubscribe | 1603967567 | 1 |
| wechat_unsubscribe | 1603968269 | 2 |
| wechat_unsubscribe | 1603968275 | 3 |
| goods_detail_view | 1603469824 | 1 |
| goods_detail_view | 1603473124 | 2 |
| goods_detail_view | 1603479424 | 3 |
```


Supplement: This usage is similar to row_number () for HQL, which is written as:

```SQL
select *
from
(
select event,
row_number() over(partition by event order by event_time) as row_number
from events
) a
where a.row_number <= 3;
```



* Similar functions:

   arrayEnumerateUniq、arrayEnumerateDense


<span id="42b4193e"></span>
### Match、multiMatchAny、multiMatchAnyIndex

match(haystack, pattern)


* Hystack requires matching fields

* Pattern A regular expression that conforms to the RE2 syntax re2: https://github.com/google/re2/wiki/Syntax

* A return value of 0 indicates no match, and 1 indicates a match.


Example:

```sql
select distinct user_profiles.user_id, multiMatchAny(user_profiles.user_id, ['^[0-9]*$', '^d{10}$']) as is_match from events where event_date > '2021-03-01' limit 20;
```


Result set:


|user_profiles.user_id |is_match |
|---|---|
|209041 |1 |
|unknown |0 |


MultiMatchAny(haystack, [pattern1, pattern2, ...])


* [Pattern1, pattern2,...] Any regular expression that conforms to the PCRE syntax.

* A return value of 0 indicates all matches, and 1 indicates at least one pattern match.

* This function matches faster when matching substrings.

* The haystack string needs to be less than 2 ^ 32 bytes.

   multiMatchAnyIndex(haystack, [pattern1, pattern2, ...])

* Similar to multiMatchAny

* The return value is the index that matches haystack, the index starts at 1, and no match returns 0.


Example:

```Plain
select distinct user_profiles.user_id, multiMatchAnyIndex(user_profiles.user_id, ['^[0-9]*$', '^([a-zA-Z0-9_-].)+@[a-zA-Z0-9_-]+(.[a-zA-Z0-9_-]+)+$', '(.[a-zA-Z0-9_-]@)+']) as regex_index from events where event_date > '2021-03-01' limit 2;

```


Result set:


|user_profiles.user_id |regex_index |
|---|---|
|209041 |1 |
|xxxx.xxx@xxx.com |3 |
|aaa@aaa.com |2 |
|unknown |0 |


<span id="_1-6-常见用法举例"></span>
## 1.7 JOIN instructions for use

In SQL custom queries, if you want to use a JOIN statement for an associated query, you need to be aware that the fields of the JOIN table need to be queried for associated fields.


* Correct example

   ```SQL
   SELECT t1.*
   FROM (
       SELECT event_date, ssid, user_id
       FROM events
       WHERE event_params.appId IN ('XXX', 'XXXX')
         AND event_date >= '2025-08-11'
         AND event = 'XXXX'
   ) t1
   LEFT JOIN (
       SELECT DISTINCT user_id
       FROM events
   ) t2 ON t1.user_id = t2.user_id;
   ```
   

* **Error** examples, be sure to avoid wrong use

   ```SQL
   SELECT t1.*
   FROM (
           SELECT event_date, ssid, user_id
           FROM events
           WHERE event_params.appId IN ('XXX', 'XXXX')
             AND event_date >= '2025-08-11'
             AND event = 'XXXX'
   ) t1 
   LEFT JOIN events t2 ON t1.user_id = t2.user_id --When joining t2, the field of join on is not queried in t2 using a query statement, which is incorrect.
   ```
   


<span id="5163928f"></span>
## 1.8 Common usage examples

<span id="a0b64c5f"></span>
### **Query user behavior on a given day based on uuid**

```SQL
select event 
from events 
where user_profiles.user_id = 'datafinder@datarangers.com' 
and event_date = '2020-08-10'
limit 20

```


<span id="25e98b16"></span>
### **Query the total number of occurrences of a certain event for users in a certain time period**

```SQL
select count(event)
from events
where 
event = 'event_name'
and event_time > 1596988800
and event_time < 1597161600
limit 20

```


<span id="264e3f61"></span>
### **Query the number of users who have experienced behavior 1 and behavior 2, but not behavior 3**

```SQL
select count(distinct hash_uid)
from events
where 
(event = 'event_1' or event = 'event_2' and event != 'event_3')
and event_time > 1596988800
and event_time < 1597161600
limit 20

```


<span id="69ed6dd8"></span>
### **Query the user's first\-time behavior attributes**

```SQL
select user_profiles.user_id, event_params.{event_name}.{event_param_name} from events
where event = 'sogo'
and event_date > '2020-01-01'
order by event_time desc
limit 10;
```


<span id="48ca24a7"></span>
### **Query the distribution of user purchases over a period of time**

```SQL
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
    where event = 'buy'
    and event_date > '2020-06-01' and event_date < '2020-08-02'
    limit 200
)
```


Clustering is used as a condition when querying for event\-related information.

```sql
select event from events where hash_uid in (select hash_uid from cohorts where cohort_id = 154) and event_date = yesterday()
```


<span id="512725a2"></span>
### **Query the user_id of users in the cluster**

```sql
select user_id from users where hash_uid in (select hash_uid from cohorts where cohort_id = 154) and last_active_date >= '2021-01-01'
```


<span id="89b8d6d8"></span>
### Complex queries using the WITH clause

```SQL
Refactor the query using the WITH clause
WITH filtered_valid_users AS (
    -- Sub-query: filter out user_id non-empty user base information
    SELECT 
        hash_uid, 
        user_id 
    FROM users 
    WHERE user_id IS NOT NULL
)
Main query: associated transaction table and filtered user table, filtered by date
SELECT 
    `event_params.predefine_pageview_hide.duration` AS pageview_hide_duration,  Alias fields for easy identification
    `event_params.duration` AS event_duration,
    event_time,
    table_a.hash_uid,
    filtered_valid_users.user_id
FROM events AS table_a
INNER JOIN filtered_valid_users 
    ON table_a.hash_uid = filtered_valid_users.hash_uid  SQL standard equality operator
WHERE 
    event_date BETWEEN '2026-03-13' AND '2026-03-15'  -- Simplified date range judgment
LIMIT 500;
```


<span id="32a0f34a"></span>
## 1.9 Visual chart configuration and viewing

The SQL custom query tool supports the configuration and display of visual charts directly on SQL query results.


1. After the query is completed using the SQL command, you can click "Visual Chart" below to enter the visual chart configuration area for configuration.

   1. The far right side of the configuration area shows you a list of all the fields for the current SQL query. You can drag the corresponding fields into the "Dimensions" and "Metrics" configuration areas of the chart.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Dimensions and metrics support up to 20 fields.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Dimensions are commonly used as fields for <strong>categorizing, grouping, or slicing</strong> data, usually descriptive information (such as time, region, device type, etc.); fields of type float are not supported as dimension fields.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Indicators are usually fields used for <strong>quantitative analysis</strong>, usually aggregable numbers (such as times, amounts, duration, etc.) that require statistical calculations.      </div>
      

   2. After selecting the fields for dimensions and metrics, you can configure them according to your analysis needs.

      1. Click the **Settings** button after the **dimension** to rename the dimension field in the pop\-up window, and the rename cannot exceed 20 characters.

      2. Click the **Settings** button after the **indicator** , you can modify the calculation caliber and data display format of the indicator field in the pop\-up window.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">Metric fields of different data types (int, string, etc.) support inconsistent calculation calibers, for example, string only supports counts and deduplicate counts.         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">You can view the data types of each field in the field list on the right, where there are some automatic conversion rules for the field types of the final query results:         </div>
         

            * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">JSON/List types are automatically converted to strings.         </div>
         

            * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">The Boolean type is automatically converted to int.         </div>
         

2. Switch chart types and chart ascending and descending order rules. Once the dimensions and metrics are configured, the chart area shows you a line chart of the query results by default. You can switch the chart type in the chart type drop\-down box and set the ascending and descending order rule for the x\-axis in the chart area.

   * Currently supports line chart, stacked chart, stacked bar chart, parallel bar chart, pie chart.

3. After completing the visual chart configuration, you can directly click "Save to Kanban" in the upper right corner to save the query results to Kanban.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you do not configure a visual chart, the query results are saved as a table to the Kanban board.   </div>
   

<span id="_2-函数列表"></span>
# 2. Function list

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">"Custom Query" currently only supports the following functions. If you need other functions, please contact customer service.</div>



|**Function type** |**Supported functions** |
|---|---|
|aggregate function |'avg', 'count', 'min', 'max', 'sum', 'varSamp', 'quantile', 'median', 'groupArray','any' |
|conditional function |'if', 'multiIf' |
|Other functions |'isNaN', 'isFinite', 'least', 'isInfinite', 'greatest','toTypeName','neighbor', |
|Nullable handler |'coalesce', 'nullIf', 'ifNull', 'isNull', 'assumeNotNull', 'toNullable', 'isNotNull' |
|array function |'indexOf', 'emptyArrayUInt16', 'arrayEnumerate', 'emptyArrayFloat32', 'arrayDifference', 'empty', 'emptyArrayDate', 'notEmpty', 'has', 'arrayResize', 'emptyArrayString', 'emptyArrayInt64', 'arraySlice', 'arrayElement', 'arrayUniq', 'arrayPopFront', 'arrayPushBack', 'hasAny', 'arrayReduce', 'length', 'hasAll', 'array', 'countEqual', 'arrayIntersect', 'emptyArrayDateTime', 'arrayJoin', 'emptyArrayFloat64', 'emptyArrayInt32', 'emptyArrayToSingle', 'emptyArrayInt8', 'range', 'arrayPushFront', 'arraySort', 'emptyArrayUInt64', 'arrayEnumerateDense', 'arrayConcat', 'arrayPopBack', 'emptyArrayUInt32', 'arrayDistinct', 'emptyArrayInt16', 'arrayEnumerateUniq', 'emptyArrayUInt8', 'arrayReverseSort', 'arrayReverse' |
|round function |'floor', 'ceil', 'trunc', 'roundAge', 'roundDuration', 'round', 'roundDown' |
|mathematical function |'cbrt', 'erf', 'pow', 'tan', 'atan', 'pi', 'ln', 'power', 'sin', 'asin', 'erfc', 'lgamma', 'tgamma', 'cos', 'sqrt', 'e', 'acos' |
|arithmetic function |'gcd', 'negate', 'plus', 'intDivOrZero', 'intDiv', 'divide', 'lcm', 'modulo', 'minus' |
|String Search |'position','locate','positionUTF8','multiSearchAllPositions','multiSearchFirstPosition','multiSearchFirstIndex','multiSearchAny','match','multiMatchAny','multiMatchAnyIndex','multiFuzzyMatchAny','multiFuzzyMatchAnyIndex','extract','extractAll','like','notLike','ngramDistance','ngramSearch', |
|type conversion function |'toDateTimeOrNull', 'toFloat64OrNull', 'toIntervalDay', 'reinterpretAsFloat32', 'toIntervalMinute', 'toDateTimeOrZero', 'toDecimal32', 'toDecimal64', 'toDateOrNull', 'parseDateTimeBestEffortOrZero', 'reinterpretAsInt32', 'toUInt32OrNull', 'reinterpretAsUInt64', 'reinterpretAsInt64', 'toUInt16OrZero', 'toDate', 'toUInt64', 'toInt32OrNull', 'toIntervalMonth', 'toUInt32OrZero', 'toIntervalHour', 'CAST', 'toInt64OrNull', 'toUInt32', 'toIntervalWeek', 'toDateOrZero', 'reinterpretAsString', 'toUInt16', 'reinterpretAsUInt32', 'reinterpretAsUInt16', 'toUInt64OrNull', 'toInt8', 'reinterpretAsDate', 'reinterpretAsInt8', 'parseDateTimeBestEffortOrNull', 'toIntervalYear', 'toInt16', 'toUInt16OrNull', 'reinterpretAsFloat64', 'toFloat32OrNull', 'toInt32OrZero', 'toUInt8', 'toString', 'reinterpretAsUInt8', 'parseDateTimeBestEffort', 'toFloat64', 'toInt16OrNull', 'toUInt64OrZero', 'toInt8OrZero', 'toInt8OrNull', 'toIntervalQuarter', 'toInt16OrZero', 'toUInt8OrNull', 'toDecimal128', 'toStringCutToZero', 'toUInt8OrZero', 'toInt64OrZero', 'reinterpretAsDateTime', 'reinterpretAsFixedString', 'toFloat64OrZero', 'toInt32', 'toFixedString', 'toFloat32', 'toInt64', 'reinterpretAsInt16', 'toDateTime', 'toIntervalSecond', 'toFloat32OrZero', 'cast','toInt64OrZero' |
|Event date function |'toYear', 'toStartOfInterval', 'toStartOfFifteenMinutes', 'toYYYYMM', 'subtractSeconds', 'addDays', 'addMinutes', 'toStartOfMinute', 'toStartOfFiveMinute', 'toTimeZone', 'subtractQuarters', 'addSeconds', 'addYears', 'toDayOfMonth', 'toDayOfYear', 'toDayOfWeek', 'addWeeks', 'now', 'toStartOfQuarter', 'toStartOfMonth', 'toMinute', 'toRelativeQuarterNum', 'subtractMonths', 'toStartOfTenMinutes', 'subtractHours', 'timeSlot', 'toTime', 'toSecond', 'formatDateTime', 'toStartOfDay', 'today', 'subtractMinutes', 'toRelativeMinuteNum', 'addMonths', 'toMonday', 'toRelativeHourNum', 'toQuarter', 'toStartOfHour', 'toUnixTimestamp', 'toRelativeMonthNum', 'toRelativeSecondNum', 'addQuarters', 'toRelativeDayNum', 'toHour', 'toStartOfISOYear', 'toISOWeek', 'addHours', 'toStartOfYear', 'timeSlots', 'toYYYYMMDD', 'yesterday', 'toMonth', 'subtractWeeks', 'dateDiff', 'subtractYears', 'toRelativeYearNum', 'toISOYear', 'toRelativeWeekNum', 'subtractDays', 'toYYYYMMDDhhmmss''toStartOfWeek','toWeek','toYearWeek', |
|Split string function |'splitByChar', 'splitByString' |
|String Replacement Function |'replaceOne', 'replaceOne','replaceAll', 'replace','replaceRegexpOne'replaceRegexpAll''regexpQuoteMeta' |
|string function |'empty','notEmpty','length','lengthUTF8','char_length','character_length','lower, 'lcase','upper,'ucase','lowerUTF8','upperUTF8','isValidUTF8','toValidUTF8','reverse','reverseUTF8','format','concat','concatAssumeInjective','substring','mid','substr','substringUTF8','appendTrailingCharIfAbsent','convertCharset','base64Encode','base64Decode','tryBase64Decode','endsWith','startsWith','trimLeft','trimRight','trimBoth', |
|higher order function |'arrayCount','arrayEqual','arrayMap','arraySplit','arrayFirst','arrayFirstIndex','arrayMin','arrayMax','arraySum','arrayAvg','arrayExists','arrayFilter', |
|JSON function |'JSONExtractUInt','JSONExtractInt','JSONExtractFloat','JSONExtractBool','JSONExtractString' |
|URL function |'protocol','domain','topLevelDomain','path','pathFull','queryString','extractURLParameters','extractURLParameterNames' |
|round function |'floor','ceil','trunc','round', |
|IN operator |'tuple', 'tupleElement' |
|IP function |'IPv4NumToString','IPv4StringToNum','IPv4NumToStringClassC','IPv6StringToNum','IPv4ToIPv6','cutIPv6','IPv4CIDRToRange,'IPv6CIDRToRange','toIPv4','toIPv6', |
|random function |'rand', 'rand32'，'rand64'，'randConstant' |
|coding function |'hex','unhex','UUIDStringToNum','UUIDNumToStrin','bitmaskToList','bitmaskToArray', |
|Hash Function |'halfMD5','MD5','sipHash64','sipHash128','cityHash64','intHash32','intHash64','SHA1','SHA224','SHA256','URLHash','farmHash64','javaHash','hiveHash','metroHash64','jumpConsistentHash','murmurHash2_32','murmurHash2_64','murmurHash3_32','murmurHash3_64,'murmurHash3_128','xxHash32','xxHash64', |
|window function |'row_number' |


For details on how to use the function: https://clickhouse.com/docs/zh/sql\-reference/functions

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
|Up to 2 join clauses are supported, please check your SQL. |high |Reduce the number of JOIN clauses |
|Only SELECT statements are supported, please check your SQL. |high |Only the SELECT statement is retained. |
|No query statement, please check your SQL. |high |*  |
|SELECT \* queries are not supported. Please check your SQL. |high |Query only the columns that need to be queried. |
|Subqueries with more than 4 layers are not supported. Please check your SQL. |high |Reduce the number of subquery layers. |
|The column name {column} for the query does not exist, please check your SQL. |high |Checks whether the column name {column} is in the data table. |
|GROUP BY for up to 4 columns is supported, please check your SQL. |high |Reduce the number of columns after GROUP BY. |
|Table function {table_function} is not supported, please check your SQL. |high |Change the table name to events. |
|There is an unsupported function {function_name}, please check your SQL. |high |Check if the {function_name} is in the list of supported functions. If you need to use this function, please contact customer service. |
|SETTINGS is not supported. Please check your SQL. |middle |Delete the SETTINGS statement, otherwise it is ignored by default. |
|Error in query: |high |Modify your SQL statement according to {error_message}. |
|Up to 1 UNION ALL clause is supported, please check your SQL. |high |Reduce the number of UNION ALL clauses |
|INTO OUTFILE is not supported, please check your SQL. |high |Delete the INTO OUTFILE clause. |
|FORMAT is not supported, please check your SQL. |high |Delete the FORMAT clause. |
|Unsupported time condition {time_condition}, please check your SQL. |high |event_time time conditions please use integer 10\-digit timestamp, event_date time conditions please use "YYYY\-MM\-dd", e.g. “2020\-08\-01”。 |
|Query concurrency exceeds the limit. |high |Reduce the concurrency of queries. If you have greater concurrency requirements, please contact customer service. |
|SQL has a syntax error: {syntax_error_msg}. |high |Correct SQL statements based on detailed syntax error information. |
|Use event_time as the event time, not {time_condition}. |high |Use event_time as the event time. |
|Please use {new_column} instead of {old_column}. |middle |high<br><br>New column new_column may be provided in place of old_column due to technical upgrades or other reasons. |
|Invalid time condition (details: {cause}). Example: The time condition is invalid (details: the time limit is derived as empty). |high |Unwritten or problematic time conditions, such as event_date \> = '2020\-08\-05' and event_date = '2020\-08\-01' |
|Could not derive {target_condition}, please add {target_condition} constraint. Example: Unable to derive event_date, please add event_date constraints. |high |1. No event_date and no event_date limit 2. event_date cannot be derived from event_time, such as toDate (event_time) = today (). The derivation of the time function is not currently supported. |
|Please give {column} an alias, otherwise the query may report an error. |middle |For user_profiles.xxx, event_param.xxx .yyy, item_profiles .xxxx.yyy columns, it is recommended to alias, otherwise there may be an error. |


<span id="_4-常见查询错误"></span>
# 4. Common query errors


|**Error code** |**Error message** |**Common Error Causes** | | | | | |
|---|---|---|---|---|---|---|---|
|215 |xxxxxx is not under aggregate function and not in GROUP BY |SQL query columns are not in GROUP BY, for example: select event, user_profiles user_id from events group by event; change it to: select event, user_profiles user_id from events group by event, user_profiles user_id; or: select event, any (user_profiles user_id) from events group by event; | | | | | |
|43 |Illegal types of arguments （xxx, yyy）of function [equals |greater |greaterOrEquals |less |lessOrEquals |notEquals ] |The two sides of the comparison character are not the same type, for example: the price attribute type of the event buy is int, then select event from events where event_param.buy. Price! = '1'; modify it to: select event from events where event_param.buy. Price! = 1; |
|53 |ARRAY JOIN requires array argument |Type mismatch, for example: select *arrayJoin (event_params. Force. $target_uuid_list)*  | | | | | |
|62 |Syntax error: failed at position xxxx |Check the detailed error, for example: select event from events where event as e = 'app_launch' limit 20; The error message is: The query has an error: code: 62, detail_message: DB:: Exc e pt ion DB :: Exc e pt ion: Syntax error: failed at position 239: = 'app_launch') and (tea_app_id = 41514 and event_date \> = '2021\-03\-09' and event_date < = '2021\-03\-15') limit 20;. Expected one of: token, Comma. After observation, it was found that the error occurred around  **= 'app_launch'**  . After investigation, it was found that the event as e syntax was wrong, so it should be changed to: select event from events where event = 'app_launch' limit 20; | | | | | |
|202 |Too many simultaneous queries. |The current database query is busy. Please try again later. | | | | | |
|42 |Number of arguments for function xxxx doesn't match |The number of parameters does not match, for example: select least (user_profiles. user_id) from events limit 20; The error message is: There is an error in the query: code: 42, detail_message: DB:: Exc ep t ion DB :: Exc ep t ion: Number of arguments for function least doesn't match: passed 1, should be 2. After querying the manual, it is found that the least function requires 2 parameters and returns the smaller of the two parameters. \* Specific function usage can be found https://clickhouse.tech/docs/v19.14/zh/ | | | | | |


<span id="_5-faq"></span>
# 5. FAQ

<span id="_5-1-如何查询用户属性或业务对象属性？"></span>
## 5.1 How to query user attributes or business object attributes?

The format of the user attribute column name is user_profiles. {user_profile_name}, and the format of the business object attribute column name is item_profiles. {item_name}. {item_param_name}. The example is as follows:

```Plain
select user_profiles.loc_country_id, item_profiles.jersey.team 
from events 
where event_date > '2020-08-01' 
and event_date < '202-08-10' 
limit 200;
```


<span id="_5-2-如何查询事件属性？"></span>
## 5.2 How to query event properties?

The format of the event property column names is event_params. {event_name}. {event_param_name}. When querying event properties, you need to specify the event name corresponding to the event property in the WHERE condition. An example is as follows:

```Plain
select user_profiles.os_name, event_params.app_launch.session_duration, network_type, device_brand, event_time
from events
where event_date >= '2020-08-12' and event_date <= '2020-08-19'
limit 20;
```


Note: Although the WHERE condition in the sample SQL does not contain event = 'app_launch', according to

event_params app_launch session_duration field semantics will still only query session_duration attribute values under app_launch events.

<span id="_5-3-查询不同事件下的同一个属性名的属性值"></span>
## 5.3 Query the property value of the same property name under different events

Use the event_param event property name so that custom queries do not automatically assemble event limits, requiring you to specify the event in the WHERE condition, such as:

```sql
select event_params.url as url from events where event in ('event_1', 'event_2') and event_date = today();

```


Note: If there are many events containing this property, it may result in an increase in SQL parsing time.

<span id="_5-4-如何查询事件与事件属性的关系？"></span>
## 5.4 How to query the relationship between events and event properties?

It can be viewed in DataRangers' "Data Management" feature.

Search for "event_params" in the data table to see how all events correspond to event properties.

<span id="_5-5-如何将新老用户作为条件"></span>
## 5.5 How to treat new and old users as a condition


4. Query the types of events that occurred to new users that day.

   ```Plain
   select count(distinct event) 
   from events 
   where (toDate(toDateTime(user_register_ts),'Asia/Shanghai') = toDate(toDateTime(event_time),'Asia/Shanghai')) 
   limit 1;
   ```
   

5. Treat users before September 1, 2020 as old users and check the usage of their network types.

   ```Plain
   select network_type, count(network_type) 
   from events 
   where (toDate(toDateTime(user_register_ts),'Asia/Shanghai') < toDate(toDateTime('2020-09-01 00:00:00'))) 
   and event_date >= '2019-10-01' 
   and event_date <= '2020-10-01' 
   group by network_type;
   ```
   


<span id="_5-6-对于user-profiles-user-id这种，如何join？"></span>
## 5.6 For user_profiles user_id, how to join?

If written as follows, it will cause the query to report an error " *query has an error: unknown_identifier* ". This is because the main clause and clause of Join use user_profiles user_id.

```sql
select user_profiles.user_id
from events
         left join (select user_profiles.user_id from events) as tbb on user_profiles.user_id == tbb.user_profiles.user_id
limit 100;

```


It is recommended to rewrite it in the following form:

```sql
select user_profiles.user_id
from events
         left join (select user_profiles.user_id as uuid from events) as tbb on user_profiles.user_id == tbb.uuid
limit 100;

```


<span id="_5-7-如何查询事件公共属性？"></span>
## 5.7 How to query event public properties?

Event public properties usually appear as follows:

```json
event_params.any_event.公共属性名
event_params.any_active_event.公共属性名
event_params.事件名.公共属性名

```


When querying the following SQL, the scope of the query is all events.

```json
select event_params.any_event.common_param_a from events;

```


When querying the following SQL, the scope of the query is all active events.

```json
select event_params.any_active_event.common_param_a from events;

```


When querying the following SQL, the scope of the query is event_1 events.

```json
select event_params.event_1.common_param_a from events;

```


The above SQL is equivalent to \-

```json
select event_params.any_event.common_param_a from events where event = 'event_1';

```


If an SQL contains event_params , event_params. any_active_event.xxx , event_params. Specific event name.xxx, then the event restriction rules for the query are as follows:


|Condition |Rule |
|---|---|
|SQL contains event_params. Event name. Public property name |Automatically derive event names as a limitation, the relationship between multiple specific event names is or |
|SQL contains event_params any_active_event... public attribute name |Limit active events. |
|SQL contains event_params any_event... public attribute name |No restrictions on events. |


The relationship between rules is or, for example:


|Query the event public property fields contained in SQL |Derived **event** query limits |
|---|---|
|* any_event event public attribute a,<br><br>* Public attribute a under any_active_event,<br><br>* Public attributes under event_1 a |Unlimited |
|* Public attribute a under any_active_event,<br><br>* Public attributes under event_1 a<br><br>* Public attributes under event_2 a |event_1 or event_2 or active events |
|* Public attributes under event_1 a<br><br>* Public attributes under event_2 a |event_1 or event_2 |
|* any_event event public attribute a,<br><br>* Public attributes under any_active_event a |Unlimited |
|* any_event event public attribute a,<br><br>* Public attributes under event_1 a<br><br>* Public attributes under event_2 a |Unlimited |


<span id="_5-8-如何将事件和last-value类型的业务对象关联起来"></span>
## 5.8 How to associate events with last_value types of business objects

```json
select item_profiles.phone.id from events et
 any inner join 
(select item_id from items) it
on arrayJoin(if(isNotNull(item_profiles.phone.id), assumeNotNull(item_profiles.phone.id), [NULL])) = it.item_id
where event_date >= '2021-04-07' and event_date <= '2021-04-13' and event = 'phone_event';

```


<span id="_5-9-如何将事件和all-value类型的业务对象关联起来"></span>
## 5.9 How to associate events with all_value types of business objects

```json
select item_profiles.phone.color 
from events 
where 
arrayExists(x->x in ('black'), assumeNotNull(item_profiles.phone.color))
and event = 'phone_event' and event_date >= '2021-04-07' and event_date <= '2021-04-13'

```


<span id="_5-10-为什么有些在事件分析能用的属性，但是自定义查询却不支持？"></span>
## 5.10 Why are some properties available in event analysis, but not in custom queries?

Custom queries currently do not support "old and new users", virtual properties, virtual events, and circled events.

Alternatives are:


* New and existing users: see 5.4 How to condition new and existing users.

* Virtual properties: SQL that can directly use virtual properties.

* Virtual events: using the same conditions as virtual events to query; \- circled events: no alternative;


If you really want to use the above data directly in your custom queries, you can let us know through a ticket or a customer success manager.

<span id="_5-11-如何查询任意主动事件"></span>
## 5.11 How to query for arbitrary active events

The any_active_event in event analysis is essentially a virtual event, and the SQL segments translated into custom queries are as follows:

```c
event not in ('rangers_push_send','rangers_push_workflow') and ifNull(event_params.$inactive, 'null') != 'true'
```


<span id="_5-12-如何查询app-platform这个用户属性"></span>
## 5.12 How to query app_platform this user attribute

app_platform in the actual query, not a single attribute, but a sql fragment, translated into a custom query sql segment as follows:


* app_platfrom = 'app'

   ```Plain
   (bddid not in ('null', '', '-1', '0') and os_name in ('ios','android'))
   ```
   

* app_platform = 'web'

   ```Plain
   (bddid in ('null', '', '-1', '0') and user_profiles.platform in ('wap','web'))
   ```
   

* app_platform = 'web'

   ```sql
   (
   bddid in ('null','','-1','0') 
   and user_profiles.platform not in ('wap','web')
   and user_profiles.custom_mp_platform is not null
   )
   ```
   


<span id="8fd38252"></span>
## 5.13 Whether custom SQL supports dynamic parameters

Current custom SQL queries do not support SQL queries using dynamic parameters, such as:

```SQL
select event, event_time from events where event = ‘app_launch’ and event_date = ${event_date} limit 20;
--Where event = ${event_name} This dynamic parameter is passed in by subsequent dynamic, SQL queries in the form of such dynamic parameters are currently not supported
```
