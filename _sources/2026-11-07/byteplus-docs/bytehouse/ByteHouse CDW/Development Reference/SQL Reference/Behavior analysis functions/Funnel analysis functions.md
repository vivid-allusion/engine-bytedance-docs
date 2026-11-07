---
title: "Funnel analysis functions"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/cdw-funnel-analysis-functions"
---

This tutorial introduces the basic concepts and basic methods of funnel analysis functions.

<span id="214849ec"></span>
# Function overview

The funnel analysis functions are applicable to the following business scenarios: Choose a specific time range to observe the summary of funnel stratification per time unit (day) within that range.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f11d2f7441c4448e89f3eab798c12dd9~tplv-goo7wpa0wc-image.image) </span>

Brief Introduction to Funnel Calculation Logic:


* First, use **finderFunnel** to calculate **each user's** performance within a time window;

* Then, aggregate the results of finderFunnel using **funnelRep** to form a summary of every layer for **all users** in the funnel.


<span id="12210cf4"></span>
# Function description

<span id="2d5777f3"></span>
## finderFunnel()

```Python
finderFunnel(window, start_timestamp, check_granularity, watch_numbers, relatedNum, window_type, time_zone, time_interval)(server_time,client_timestamp, [param1, param2, ..., ]
check_event1, check_event2...)
```


Parameter description


|Parameter |Parameter description |
|---|---|
|window |The total duration of the observation window, in the same units as `client_timestamp`, stated as 86400 \* 7 seconds, which is 7 days. |
|start_timestamp |The starting timestamp for analysis, for example, analysis starts from 2022\-06\-01, hence the start timestamp is `toUInt64(toUnixTimestamp('2022-06-01')) = 1654012800`. |
|check_granularity |The duration of an observation step, the granularity within which to calculate conversion analysis, units consistent with `client_timestamp`, for 1 day it is 86400 (unit: seconds). |
|watch_numbers |How many steps are observed, for example, if `check_granularity` is 86400 (1 day), `watch_numbers = 7` indicates observing the funnel status each day for 7 days starting from `start_timestamp`. |
|relatedNum |When the feature is not in use, set the attribute association\-related parameter to 0. |
|window_type |Relative window type defines whether to calculate conversions for the same day. Setting `window_type=1` indicates the calculation of conversions for that day. |
|time_zone |Specify the time zone, such as 'Asia/Shanghai'. |
|time_interval |Whether to enable the time interval. When the `time_interval` value is 1, the time interval switch is turned on, and the results will additionally include the `client_time` sequence of the corresponding event. **When the time interval is enabled, add** `relatedNum`, `window_type`, `time_zone`**parameters for placeholders.**  |
|server_timestamp |The event occurrence server timestamp column needs to be converted to UInt64 for calculating the time slots/steps during the function run using this value. |
|client_timestamp |The event occurrence client timestamp column needs to be converted to UInt64 to sort the data during the function run. |
|[param1, param2, ..., ] |Attributes related parameters, not set when the feature is not used. |
|check_event |Calculate the converted list of events; those that meet the conditions within the defined analysis duration of `window` will be considered valid event triggers. If there are 3 events, input: EventName = 'E0001', EventName = 'E0002', EventName = 'E0003'. |


<span id="0c764ede"></span>
## funnelRep()

Use funnelRep to aggregate the results of finderFunnel, compiling a summary result of all users at each stage of the funnel.

```Python
funnelRep(number_steps, evnet_count)(funnel_res)
```


**Parameter Description**


|Parameter |Parameter description |
|---|---|
|number_steps |UInt type number, representing the number of time slots included, usually consistent with `finderFunnel` function's `watch_numbers`. |
|evnet_count |UInt type number, indicating the total number of events in the event conversion chain, usually consistent with the number of times in `finderFunnel` function's `check_event`. |
|funnel_res |Conversion step list, produced by the `finderFunnel` subquery, containing the conversion step list for each user. |


**Return Results Explanation**

The funnelRep function returns a 2\-dimensional array, consisting of a total of 1 summarized result and `number_steps` sub\-arrays. The first sub\-array contains the summarized result, and the second sub\-array comprises the funnel calculation for the first time slot within the `window` defined analysis duration, and so forth.

<span id="7599916a"></span>
## funnelRep2()

funnelRep2() function builds on funnelRep() function by adding `targe_step` and `taget_interval_group` parameters, consolidating the results of finderFunnel and processing the detailed data for each step interval.

```C++
funnelRep2(number_steps, evnet_count, targe_step, taget_interval_group)(funnel_res.1, funnel_res.2)
```


**Parameter Description**


|parameter |parameter description ||
|---|---|---|
|number_check<br><br>event_number<br><br>funnel_res.1 |Stay consistent with funnelRep. ||
|targe_step |Set the target step, with values ranging from [0, total number of steps \- 1]. |When passing in i, it represents the time interval between the ith layer (from step i to step i+1).<br><br>When passing in 0, it represents the time interval from the first step to the last step. |
|taget_interval_group |Time interval distribution sequence, type: list, explicit input of the starting threshold is required. |For example, when inputting [0, 1000, 2000, 3000], the desired time interval distribution ranges are [0, 1000), [1000, 2000), and [2000, 3000]. |
|funnel_res.2 |The time interval columns returned by the funnel. ||


**Return Result Description**

```SCSS
(
// The distribution interval of the number of converters at a certain layer, a two-dimensional array, outer(inner)
// outer[0] is the summary value, outer[i] represents the i-th observation unit.
// inner[i] is the number of people for whom the conversion interval of this layer falls into the (i+1) interval.
[ [500, 300, 200], [200, 200, 100], [xxx, xxx, xxx], [xxx, xxx, xxx] ],
// Arithmetic statistical distribution intervals, a two-dimensional array, outer(inner).
// outer[0] is the arithmetic statistics of the summarized conversion intervals, outer[i] is the arithmetic statistics of the i-th interval observation unit.
[ [avg, max, min, mid, 75-quantile, 25-quantile], [...], [...], [...] ]
)
```


<span id="921c6997"></span>
# Funnel Analysis Example

<span id="2ac44b28"></span>
## Sample Model

The following example uses tables, specifically the User Behavior Fact Table (Log) and User Dimension Table (User), which form the commonly used star schema. Subsequent sections will demonstrate the specific usage of the funnel analysis function based on this table.

```SQL
 CREATE TABLE -- Event log table.
  default.LOG (
    `Visitor` UInt32,
    `EventName` String,
    `EventTime` DateTime,
    `Province` String,
    `City` String
  ) ENGINE = CnchMergeTree
  ORDER BY Visitor;
  
  CREATE TABLE -- User table.
  default.User (
    `Visitor` UInt32,
    `Fvisit_Time` DateTime,
    `Fvisit_Province` String,
    `Fvisit_City` String
  ) ENGINE = CnchMergeTree
  ORDER BY Visitor;
```


<span id="5867db2e"></span>
## Basic Conversion Model

The basic conversion model employs finderFunnel() and funnelRep() to analyze conversion rates for each step of the event.

The example below refers to the returned conversion funnel for the 3 events 'E0001', 'E0002', 'E0003' over 7 days from 2022/6/1 to 2022/6/8:

```SQL
SELECT funnelRep(7, 3)(funnel_res)
FROM
(
    SELECT finderFunnel(7 * 86400, 1654012800, 86400, 7)(toUInt64(toUnixTimestamp(LOG.EventTime)), toUInt64(toUnixTimestamp(LOG.EventTime)), LOG.EventName = 'E0001', LOG.EventName = 'E0002', LOG.EventName = 'E0003') AS funnel_res
    FROM LOG
    LEFT JOIN
    (
        SELECT *
        FROM User AS t
    ) AS U ON LOG.Visitor = U.Visitor
    WHERE (EventTime >= '2022-06-01 00:00:00') AND (EventTime <'2022-06-08 00:00:00') AND (EventName IN ('E0001', 'E0002', 'E0003'))
    GROUP BY Visitor
)
SETTINGS distributed_product_mode = 'local', distributed_group_by_no_merge = 1
```


The example SQL above returns:

```SQL
┌─funnelRep(7, 3)(funnel_res)─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┐
│ [[5994501,5944849,56423],[3791527,3780488,39431],[3792876,3767458,33024],[3792031,3733089,26709],[3791519,3656585,20668],[3791859,3480158,14385],[3793389,3077233,8691],[3792344,2143108,3641]] │
```



* This represents the overall funnel (E0001 \-\> E0002 \-\> E0003) as: [5994501,5944849,56423]

* The funnel for day 1 is: [3791527,3780488,39431]

* ...

* The funnel for day 7 is: [3792344,2143108,3641]


<span id="16cd60ac"></span>
## Statistical conversion interval

The following example uses the funnelRep2() function to observe data for 6 days and two conversion events, and measures the interval between each step.

```SQL
SELECT funnelRep2(6, 2, 0, [0, 60000, 120000, 180000, 240000, 300000, 360000, 420000, 480000, 540000, 600000])(funnel_res.1, funnel_res.2) AS col
FROM
(
    SELECT finderFunnel(600000, 1684512000, 86400, 6, 0, 0, 'Asia/Shanghai', 1)(toUInt64(toUnixTimestamp(LOG.EventTime)), toUInt64(toUnixTimestamp(LOG.EventTime)), LOG.EventName = 'E0001', LOG.EventName = 'E0002') AS funnel_res
    FROM LOG
    WHERE (EventTime >= '2023-05-20 00:00:00') AND (EventTime <'2023-05-26 00:00:00') AND (EventName IN ('E0001', 'E0002'))
    GROUP BY Visitor
)
```



* 6: Indicates an observation over 6 days.

* 2: Indicates two conversion events.

* 0: Statistical analysis is required for the interval between each step.

* [0, 60000, 120000, 180000, 240000, 300000, 360000, 420000, 480000, 540000, 600000]: Represents the division of intervals as [0, 60000), [60000, 120000), ..., [540000, 600000], totaling ten intervals.


**Output results**

```SQL
(
 [
 [1845,100,45,24,16,14,17,11,12,32], // Total aggregated value of conversion counts in each interval
 [370,19,12,3,4,4,2,1,5,5], // Aggregated value of conversion counts falling into each interval on Day 1
 [87,6,3,1,1,0,2,0,2,4], // Aggregated value of conversion counts falling into each interval on Day 2
 [99,4,1,2,0,0,2,0,6], // Aggregated value of conversion counts on Day 3... and so on
 [442,25,10,5,2,1,4,1,2,7],
 [437,25,8,6,3,6,3,1,1,6],
 [410,21,11,7,6,3,6,62,4]
 ],
 [
 [38240.619092627596,596767,2,4829.31494140625,20458.8353515625,790.316650390625], // Arithmetic statistics of all conversion time intervals within six days. The six elements correspond to avg (mean), max (maximum value), min (minimum value), mid (median), 75-quantile, and 25-quantile respectively
 [37865.0494117647,588283,28,5586.3125,19187.166015625,816.0833129882812], // Arithmetic statistics of conversion intervals on Day 1, with the six elements corresponding to the same meanings as above
 [59552.33018867925,587526,14,7210.5,25011,1087], // Statistics for Day 2... and so on
 [52667.491228070176,596132,47,3111,19174,781], // Statistics for Day 3... and so on
 [32494.533066132266,596547,23,4434.09375,16213.638671875,731.5277709960938],
 [34384.957661290326,59484,24,4429,23285.33203125,744.5555419921875],
 [40416.285711428572,596767,2,5539,21438.056640625,833.88888549804688]
 ]
)
```
