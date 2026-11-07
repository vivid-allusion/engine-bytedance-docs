---
title: "Overview"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/behavior-analysis-function-overview"
---

ByteHouse customizes certain functions according to user behavior analysis use scenarios, including:

* Retention analysis function
* Funnel analysis function
* Path analysis function

Compared to assembling SQL or using ClickHouse's native functions, using ByteHouse's proprietary functions is more efficient. This document details the usage methods of these functions.
<span id="7706e53c"></span>
### Example model
Below is an example table composed of the user behavior fact table Log and the user dimension table User in a commonly used star model.
The following text will demonstrate the specific application of these functions based on this table.
```SQL
 CREATE TABLE -- Event log table
  default.LOG (
    `Visitor` UInt32,
    `EventName` String,
    `EventTime` DateTime,
    `Province` String,
    `City` String
  ) ENGINE = Distributed('your_cluster', 'default', 'LOG_Example_local')
  
  CREATE TABLE -- User table
  default.User (
    `Visitor` UInt32,
    `Fvisit_Time` DateTime,
    `Fvisit_Province` String,
    `Fvisit_City` String
  ) ENGINE = Distributed('your_cluster', 'default', 'User_Example_local')
  
  -- Only the Schema of the Distributed table is displayed. The Schema of the local table is omitted. 
```

<span id="771257be"></span>
### Retention analysis function
<span id="959ee68e"></span>
#### Business dcenarios
Select a time limit, observe the retention of users who meet a certain dimension in each time unit within this time limit after a period.
Introduction to Retention Calculation Logic:

* First, use **`genArrayIf`** function to pre-aggregate **first visit** (`first_events`) and **return** (`return_events`) behavioral data into specified time slots, obtaining a bitset of visit situations in `Array(UInt8)` format `bitset`. This step divides the time limit into discrete time slots and uses a bitset to represent whether an event occurs in each slot.
* Then use **`retention2`** to aggregate the bitsets of users' first visits (`first_events`) and returns (`return_events`) to get the retention data for each time slot.

<span id="1994a6b7"></span>
#### Basic concepts

* Time slots (Step): i.e., the step length. For example, observing the retention data of each day in 7 days, the Time slots quantity (*number_step*) is 7, the duration of each time slot (*step_time*) is 86400 seconds, which equals one day.
* Event Position Set: Computes intermediate data for retention, returning as [0,1,0,1.....] representing whether an event occurred in each time slot.
* First visit events (first_events), that is, whether a first visit event occurred in each time slot for the user. Example: User registers.
* Return events (return_events), that is, whether a return event occurred in each time slot for the user. Example: User logs in.
   * In the example below, first events are [13,2], where the first decimal Number 13 corresponds to the 8-bit binary number 0000 1101, and the second decimal Number 2 corresponds to the 8-bit binary number 0000 0010. This array's 16-bit binary representation is 0000 0010 0000 1101, covering 16 days, and shows whether the target event occurred on No. 1, 3, 4, 9 days with the lowest bit representing day 1 and the highest bit representing day 16. Similarly, the return_events array signifies that the target event occurred on days 1, 3, 9, and 10.

```SQL
first_events array: [13, 2]
Corresponding binary represents: 0000 0010     0000 1101
Corresponding decimal numbers: 2              13
Meaning: The target event occurred on the 1st, 3rd, 4th, and 10th days.

return_events array: [5, 3]
Corresponding binary represents: 0000 0011     0000 0101
Corresponding decimal numbers: 3              5
Meaning: The target event occurred on the 1st, 3rd, 9th, and 10th days.
```


* Retention array: Retention refers to observing from the perspective of user starting events if return events occurred in future time slots.

```SQL
--Example
SELECT retention2(10)([13, 2], [5, 3])

┌─retention2(10)([13, 2], [5, 3])───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┐
│ [1,0,1,0,0,0,0,0,1,1,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,0,1,1,0,0,0,1,0,0,0,0,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1] │
└───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
```

In the above example, considering a time slot duration of 1 day and a total of 10 days, with first_event and return_event as [13,2], [5,3], the retention array under this condition. The returned retention array is a Number_steps*Number_steps array; in the example given, it's a 10*10 array. Thus, this array should be divided into 10 rows to observe the results, where each row of the retention array represents the outcome of performing a bitwise "and" operation between the events in return_events and the day i event in first_events is considered as the start time.
```SQL
1,0,1,0,0,0,0,0,1,1, -- Taking the 1st day as the starting observation point, the user made a return visit on the 1st, 3rd, 9th, and 10th days. So the columns corresponding to the 1st, 3rd, 9th, and 10th days are 1.
0,0,0,0,0,0,0,0,0,0, -- Taking the 2nd day as the starting observation point, no event occurred on the second day, so all values in the second row are 0.
0,0,1,0,0,0,0,0,1,1, -- Taking the 3rd day as the starting observation point, the user made a return visit on the 3rd, 9th, and 10th days. So the columns corresponding to the 3rd, 9th, and 10th days are 1.
0,0,0,1,0,0,0,0,1,1, -- Taking the 4th day as the starting observation point, the user made a return visit on the 9th and 10th days. So the columns corresponding to the 9th and 10th days are 1. For the 4th day itself, although there was no return visit event, it is also output as 1 in the corresponding column by default.
0,0,0,0,0,0,0,0,0,0, 
0,0,0,0,0,0,0,0,0,0,
0,0,0,0,0,0,0,0,0,0,
0,0,0,0,0,0,0,0,0,0,
0,0,0,0,0,0,0,0,0,0,
0,0,0,0,0,0,0,0,0,1
```

Aggregate these retention arrays by city, media source, etc., to obtain retention data. Example:
```SQL
select city, retention2(3)(..., ...) from ... group by city
--The retention array for a certain city is:
22,11,1
0,5,3
0,0,1
```

<span id="6be3407f"></span>
#### Function definition
<span id="81701ac3"></span>
##### genArrayIf()
```SQL
genArrayIf(number_steps, begin_timestamp, step_time)(timestamp, if_expr)
```

**Input parameters:**

* `number_steps`: The quantity of time slots.
* `begin_timestamp`: The starting timestamp for analysis, e.g., the data filtering range starts from 2022-06-01, so the start timestamp is toUInt64(toUnixTimestamp('2022-06-01')) = 1654012800.
* `step_time`: Duration of one time slot.
* `timestamp`: Column containing the event timestamp. First, convert to a timestamp, then to Uint64 format.
* `if_expr`: Definition of retention conditions, those verifying the hypothesis will be considered as behavior occurring.

**Output parameters:**

* Output in `Array(UInt8)` format the visits overview `bitset`.

**Example:**
In the example below, the result shows whether the event `EventName = 'E0002'` occurred every day over 7 days.
```SQL
SELECT
    Visitor,
    genArrayIf(7, 1654012800, 86400)(toUInt64(toUnixTimestamp(LOG.EventTime)), EventName = 'E0002') AS return_events
FROM LOG
WHERE (EventTime >= '2022-06-01') AND (EventTime < '2022-06-08') AND (EventName = 'E0002')
GROUP BY Visitor
```

<span id="bbabac12"></span>
##### retention2()
```SQL
retention2(number_steps)(first_events, return_events)
```

**Input parameters:**

* `number_steps`: The number of time slots. `number_steps` should be consistent with `genArrayIf` in `number_steps`.
   :::warning
   `number_steps` is restricted by the size of **bit sets** of initial visits (first_events) and return visits (return_events), following the rule `(events_array.size()-1)*8< number_steps <= events_array.size()*8`. For example, if the count of UInt8 type elements in first_events in the example below is 2, the window size to be entered should be a value between `(8, 16]`.
   The sizes of the initial visit array and return visit array need to be consistent; if inconsistent, the final calculation will be incorrect, resulting in many zeros.
   :::
* `first_events`: The bitset for the initial visits, required from `genArrayIf`.
* `return_events`: The bitset for the return visits, required from `genArrayIf`.

**Output parameters:**

* Output `Array(UInt64)` format of the retention array.

<span id="bba4502b"></span>
#### Example SQL
Observe the retention from the first visit ('E0001') to the return visit ('E0002') within a 7 day window, grouped by city.
```SQL
SELECT
    City,
    retention2(7)(first_events, return_events)
FROM
(
    SELECT
        City,
        Visitor,
        genArrayIf(7, 1654012800, 86400)(toUInt64(toUnixTimestamp(LOG.EventTime)), EventName = 'E0001') AS first_events
    FROM LOG
    WHERE (EventTime >= '2022-06-01') AND (EventTime < '2022-06-08') AND (EventName = 'E0001')
    GROUP BY
        Visitor,
        City
) AS t1
ANY LEFT JOIN
(
    SELECT
        Visitor,
        genArrayIf(7, 1654012800, 86400)(toUInt64(toUnixTimestamp(LOG.EventTime)), EventName = 'E0002') AS return_events
    FROM LOG
    WHERE (EventTime >= '2022-06-01') AND (EventTime < '2022-06-08') AND (EventName = 'E0002')
    GROUP BY Visitor
) AS t2 ON t1.Visitor = t2.Visitor
GROUP BY City
ORDER BY City ASC
SETTINGS distributed_product_mode = 'local', distributed_group_by_no_merge = 0
```

Return:
<div style="text-align: center"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d53c1eef73e043f486b83a545509dfc8~tplv-goo7wpa0wc-image.image" width="2392px" /></div>

Obtain a 7*7 array, as illustrated above where city1 is analyzed as:
```SQL
109777,61903,62185,62116,62064,62066,61952,
0,109978,61922,62500,61817,62671,62417,
0,0,110033,62193,62177,62230,62287,
0,0,0,109715,61833,62142,62119,
0,0,0,0,110598,62493,62515,
0,0,0,0,0,109508,61909,
0,0,0,0,0,0,110746
```

Calculate the 1-day conversion rate from Day1->Day6 as needed.
According to actual needs, the time slot can be modified to weeks, months, etc.
<span id="4d7bac41"></span>
### Funnel analysis function
Use scenario: Select a certain time range and observe the funnel layer summary for each day within this time range according to a definite time interval.
Overview of Funnel Computation Logic:

* First, use **finderFunnel** A to calculate **each User** 's performance within a time window;
* Then, use **funnelRep Aggregate** A to finderFunnel's result to form the funnel **all Users** ' aggregated result at every level.

<span id="5415079c"></span>
#### Function diagram
<span id="2d5777f3"></span>
##### finderFunnel()
```Python
finderFunnel(window, start_timestamp, check_granularity, watch_numbers)(server_timestamp, client_timestamp, check_event1, check_event2...)
```


* `window`: The total observation window duration, in the same unit as `client_timestamp`, in the example below, it is 86400 * 7 seconds, which is 7 days.
* `start_timestamp`: The start timestamp of the analysis, e.g., the analysis starts from June 1, 2022, so the start timestamp is `toUInt64(toUnixTimestamp('2022-06-01')) = 1654012800`
* `check_granularity`: Observation step duration, the granularity within which to calculate conversion analysis, in the same unit as `client_timestamp`, e.g., 1 day corresponds to 86400 seconds.
* `watch_numbers`: The number of steps to observe, if`check_granularity` is 86400 (1 day), `watch_numbners = 7`, refers to observing funnel conditions each day for 7 days starting from `start_timestamp`
* `server_timestamp`: Event occurrence server timestamp column, to be converted into UInt64 type for function runtime to calculate the time slot/step the event belongs to.
* `Client_timestamp`: The column for the event occurrence client timestamp, needs to be converted to UInt64 type for data sorting during function execution.
* `Check_event`: List of conversion events, valid event triggers are determined within the duration defined by `window`. If there are 3 events, then input: EventName = 'E0001', EventName = 'E0002', EventName = 'E0003'

<span id="0c764ede"></span>
##### funnelRep()
```Python
funnelRep(number_steps, evnet_count)(funnel_res)
```


* `Number_steps`: A UInt type number that includes the quantity of time slots, usually consistent with watch_numbers in the finderFunne`watch_numbers in the finderFunnel` function.
* `Event_count`: A UInt type number representing the total number of events in the conversion chain, typically consistent with the quantity of events in the `finderFunnel` function's `check_event`.
* `Funnel_res` : List of conversion steps generated by the subquery of `finderFunnel`, containing all conversion steps produced by each user.

Return Results:

* Returns a two-dimensional array, with a total of 1 aggregated result + `number_steps` subarrays. The first subarray is the aggregated result and the second subarray is the funnel calculation result for the first time slot within the duration defined by `window`, and so on.

<span id="3dae1f97"></span>
#### Funnel Analysis Example SQL
The following example refers to the return from the conversion funnel of 3 events 'E0001', 'E0002', 'E0003' over 7 days from 2022/6/1-2022/6/8:
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

The example SQL above returns as follows:
```SQL
┌─funnelRep(7, 3)(funnel_res)─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┐
│ [[5994501,5944849,56423],[3791527,3780488,39431],[3792876,3767458,33024],[3792031,3733089,26709],[3791519,3656585,20668],[3791859,3480158,14385],[3793389,3077233,8691],[3792344,2143108,3641]] │
```


* The overall funnel (E0001->E0002->E0003) is: [5994501,5944849,56423]
* The funnel for day 1 is: [3791527,3780488,39431]
* ...
* The funnel for day 7: [3792344,2143108,3641]

<span id="23833faa"></span>
### Path analysis function

* pathSplit
* pathCount

<span id="9772d64a"></span>
#### Business scenarios
Select a time range, analyze the user behavior paths within this range, and display the effect as follows.
Overview of path analysis computational logic:

* First **generate** an array containing all the path combinations of **each user**.
* Then **array join** expands each user's two-dimensional array containing all paths into multiple rows of individual paths.
* Then use **pathCount** to tally the path conversion situations of all users.

<span id="afd1a98d"></span>
#### Basic concepts

* Event: The occurrence of an event, also refers to the page visit nodes displayed in the path analysis chart in this context.
* Attribute (Name): Equivalent to tagging the corresponding event.
* Level: Also can be understood as the path depth in the chart, cutting off the path after exceeding x nodes.
* Node: In the context of path analysis, each node represents a page.
* Edge: URL path from Page 1 to Page 2.

<span id="f466cd0a"></span>
#### Function diagram
<span id="7bc3c3af"></span>
##### pathSplit()
```Python
pathSplit(session_time, level)(timestamp, event, prop)
```

Input Parameters:

* session_time: The time window for path analysis, consistent with the timestamp unit, is 600 seconds in the example below, which means only the paths formed within 10 minutes after the first event are calculated;
* `level`: Path depth, the path is truncated after x nodes;
* `timestamp`: **Timestamp** column, needs to be converted into a timestamp, then converted into Uint64 format;
* `event`: Event column, only supports numerical value type, needs to be explicitly specified through **multiIf;**

As in the following example: multiIf(EventName = 'E0001', 1, EventName = 'E0002', 2, EventName = 'E0003', 3, 0) AS e

* `prop`: Attribute column, when absent use `''` as a placeholder;

Output Parameters (Intermediate Results):
Returns a two-dimensional array: [(e1, p1), (e2, p2), (e1, p2)]

* (ex,px): Corresponds to the event stream, i.e., the events that occur on this path
* e: Events, corresponding to the `event` number defined in the `multiif` column
* p: Event corresponding attribute, corresponding to `prop`

<span id="0c65508d"></span>
##### pathCount()
```Python
pathCount(y, x)(path, cnt1, cnt2)
```

pathCount returns the data needed for display, where x represents the horizontal path depth (as depicted, it is 4),
The data required for frontend display essentially represents each light blue block as a node, and the edges between light blue blocks are all output by pathCount

* `y`: **Vertical single-layer display depth**, as shown in the yellow circled part of the diagram, that is y = 5.
* `x`: **Horizontal path depth**, any paths exceeding x nodes will truncate the path, as shown in the diagram where x = 4.
* `Path`: Returns the path column (expanded through arrayJoin) from `pathSplit`.
* `cnt1`: Path weight 1, usually just passing 1 is fine, used to calculate the number of unique path occurrences **after removal of duplicates;**
* `cnt2`: Path weight 2, usually pass the count obtained in the `pathSplit` subquery as `count()` to find the total number of path occurrences **without duplicates.**

Return format:

* The return format is a 3-tuple ([node_index],[nodes], [edges]), which forms a flow graph of page path conversion through this result set:
* `node_index`: Format: `(event, prop)`, shows event nodes.
   * `event` is the index number of the event; if previous 'pathSplit' used fill in multiIf(EventName = 'E0001', 1, EventName = 'E0002', 2, EventName = 'E0004', 3, 0), then now return 1 corresponds to 'E0001', 2 to 'E0002', and 3 to 'E0004';
   * `prop` is the prop passed into 'pathSplit'.
* `nodes`: Two-dimensional array. Show the unique occurrences and total occurrences of each **node** at various levels (level, index starts from 0), format: `(level, node_index, cnt1, cnt2)`.
   * Level: Level
   * Node index: The index of the event, refer to the mapping relation in the node_index array
   * Cnt1: The unique count of node visits
   * Cnt2: The count of node visits
* Edge: Two-dimension array, each **edge** shows the unique count and count of occurrences at each level, the format is:

`(level, from_node_index, to_node_index, cnt1, cnt2)`

* Level: Level, the input x
* From_node_index: Source node, refer to the mapping relation in the node_index array
* To_node_index: Target node, refer to the mapping relation in the node_index array; to_node_index is marked with 65535 if from_node_index is already the endpoint, indicating that the user has experienced loss after reaching this event
* Cnt1: The unique count of node visits
* cnt2: Frequency of node access;

<span id="c9c7b2ff"></span>
#### Path analysis example SQL
Specify a user Visitor = 964049 for illustration.
This example represents data from events 'E0001', 'E0002', 'E0004' that occurred within 10 minutes after the events on 2022/6/1-2022/6/2, showing the page information at a Page Path depth of 3 levels.
Firstly, calculate the intermediate results through pathSplit:
```SQL
SELECT Visitor,pathSplit(600, 3) (toUInt64(toUnixTimestamp(LOG.EventTime)), multiIf(EventName = 'E0001', 1, EventName = 'E0002', 2, EventName = 'E0004', 3, 0) AS e, '') AS path
FROM LOG
WHERE (EventTime >= '2022-06-01 00:00:00')
  AND (EventTime < '2022-06-02 00:00:00')
  AND (EventName IN ('E0001', 'E0002', 'E0004'))
  and Visitor = 964049
GROUP BY Visitor

--Return：
┌─Visitor─┬─path────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┐
│  964049 │ [[(1,''),(2,''),(3,'')],[(1,'')],[(1,''),(2,''),(3,'')],[(1,''),(2,''),(2,'')],[(1,'')],[(1,'')],[(1,'')],[(1,''),(3,''),(3,'')],[(1,''),(2,''),(3,'')],[(1,''),(1,''),(3,'')],[(1,'')],[(1,''),(2,''),(3,'')],[(1,'')],[(1,''),(2,''),(2,'')]] │
└─────────┴─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
```

Then expand the two-dimensional array representation of a single row path returned by arrayJoin into multiple single row paths, and calculate the number of times each Path appears.
```SQL
SELECT path    AS path,
             count() AS cnt
      FROM (SELECT arrayJoin(pathSplit(600, 3)(toUInt64(toUnixTimestamp(LOG.EventTime)), multiIf(EventName = 'E0001', 1, EventName = 'E0002', 2, EventName = 'E0004', 3, 0) AS e, '')) AS path
            FROM LOG
            WHERE (EventTime >= '2022-06-01 00:00:00')
              AND (EventTime < '2022-06-02 00:00:00')
              AND (EventName IN ('E0001', 'E0002', 'E0004'))
              and Visitor = 964049
            GROUP BY Visitor)
      GROUP BY path
 --Return
┌─path───────────────────┬─cnt─┐
│ [(1,'')]               │   6 │
│ [(1,''),(1,''),(3,'')] │   1 │
│ [(1,''),(2,''),(3,'')] │   4 │
│ [(1,''),(2,''),(2,'')] │   2 │
│ [(1,''),(3,''),(3,'')] │   1 │
└────────────────────────┴─────┘
```

Finally, calculate the final 3*3 result (Path depth of 3, with up to three nodes shown at each level) through pathCount:
```SQL
SELECT pathCount(3, 3) (path, 1, cnt)
FROM (SELECT path    AS path,
             count() AS cnt
      FROM (SELECT arrayJoin(pathSplit(600, 3)(toUInt64(toUnixTimestamp(LOG.EventTime)), multiIf(EventName = 'E0001', 1, EventName = 'E0002', 2, EventName = 'E0004', 3, 0) AS e, '')) AS path
            FROM LOG
            WHERE (EventTime >= '2022-06-01 00:00:00')
              AND (EventTime < '2022-06-02 00:00:00')
              AND (EventName IN ('E0001', 'E0002', 'E0004'))
              and Visitor = 964049
            GROUP BY Visitor)
      GROUP BY path )
--Return
┌─pathCount(5, 3)(path, 1, cnt)─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┐
│ ([(1,''),(3,''),(2,'')],
[[0,0,5,14],[1,0,1,1],[1,1,1,1],[1,2,2,6],[2,1,3,6],[2,2,1,2]],
[[0,0,0,1,1],[0,0,1,1,1],[0,0,65535,1,6],[0,0,2,2,6],[1,2,2,1,2],[1,1,1,1,1],[1,0,1,1,1],[1,2,1,1,4]]) │
└───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
```

The result is:

* `Node index`: [(1,''),(3,''),(2,'')], showing event numbers mapped as 0->1(E0001), 1->3(E0004), 2->2(E0002)
* `nodes`：[[0,0,5,14],[1,0,1,1],[1,1,1,1],[1,2,2,6],[2,1,3,6],[2,2,1,2]]
   * No 1 Level, [0,0,5,14]
      * Only one node "Event 1", i.e., E0001;
      * The node's unique visit count is 5, total visit count is 14
   * No 2 Level, [1,0,1,1],[1,1,1,1],[1,2,2,6]
      * Three events occurred: E0001, E0004, E0002
      * The unique visit counts for the 3 nodes are 1, 1, 2; total visit counts are 1, 1, 6
   * ....
* edge：[0,0,0,1,1],[0,0,1,1,1],[0,0,65535,1,6],[0,0,2,2,6],[1,2,2,1,2],[1,1,1,1,1],[1,0,1,1,1],[1,2,1,1,4]
   * On the first level, there are the following edges:
      * 0->0: that is 'E0001'->'E0001', 1 visit
      * From 0 to 1: 1 visit
      * From 0 to 65535 (i.e., the endpoint), 1 deduplicated visit
      * From 0 to 2, 2 deduplicated visits
   * At the second level, the following edges exist:
      * From 2 to 2, 1 deduplicated visit
      * From 1 to 1, 1 deduplicated visit
      * From 0 to 1, 1 deduplicated visit
      * From 2 to 1, 1 deduplicated visit

The results can be supplemented as Page Path analysis, such as
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/facdbbf039ba464b8c11a0eaaf553cb9~tplv-goo7wpa0wc-image.image =1140x)
