---
title: "Retention analysis function"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/retention-analysis-function"
---

This tutorial introduces the basic concepts and usage of the retention analysis function.

<span id="0918642f"></span>
# Function overview

<span id="8acc14a5"></span>
## Business scenarios

The retention analysis function can be used to select a time range to observe user retention within a specific time unit who meet certain dimensions after that time range.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/170890570e584614be02932ff6e42a4c~tplv-goo7wpa0wc-image.image) </span>

Retention calculation logic overview:


* First, use the `genArrayIf` function to pre\-aggregate first\-time visits (`first_events`) and return visits (`return_events`) behavior data into specified time slots, generating an `Array(UInt8)`\-format visit bitset `bitset`. This step divides the time range into discrete time slots, using bitsets to indicate whether events occurred in each slot.

* Then, use `retention2` to aggregate user first visits (`first_events`) and return visits (`return_events`) bitsets to obtain retention data for each time slot.


<span id="0a37eec6"></span>
## Basic concepts


* Time slot (Step): also called step length. For example, to observe retention data for 7 days, with each day as one time slot, the number of time slots (number_step) is 7, and the duration of each time slot (step_time) is 86400 (unit: seconds; 86400 seconds equals one day).

* Event bit set: intermediate data for calculating retention, returned as [0,1,0,1.....], indicating whether the event occurred in each time slot.

* First\-time events (first_events): whether the user triggered a first\-time event in each time slot. For example, user registration.

* Return events (return_events): whether the user triggered a return event in each time slot. For example, user log in.

   * In the example below, first_events is [13,2]. The first decimal number 13 corresponds to the 8\-bit binary 00001101, and the second decimal number 2 corresponds to the 8\-bit binary 00000010. Combined, this 16\-bit binary 0000001000001101 represents 16 days of event occurrence status. The least significant bit represents day 1, and the most significant bit represents day 16. Thus, the target event occurred on days 1, 3, 4, and 9. Similarly, the return_events array indicates the target event occurred on days 1, 3, 9, and 10.

      ```SQL
      First_events Array: [13, 2]  
      Corresponding Bit Representation: 0000 0010 (binary) → 2 (decimal), 0000 1101 (binary) → 13 (decimal)  
      Meaning: The target event occurred on days 1, 3, 4, and 10.  
      
      Return_events Array: [5, 3]  
      Corresponding Bit Representation: 0000 0011 (binary) → 3 (decimal), 0000 0101 (binary) → 5 (decimal)  
      Meaning: The target event occurred on days 1, 3, 9, and 10.  
      ```
      

* Retention array: Retention refers to whether return events occur in some slots in the future from the perspective of users who have triggered first\-visit events.

   ```SQL
   --Example:
   SELECT retention2(10)([13, 2], [5, 3])
   
   ┌─retention2(10)([13, 2], [5, 3])───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┐
   │ [1,0,1,0,0,0,0,0,1,1,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,0,1,1,0,0,0,1,0,0,0,0,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1] │
   └───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
   ```
   

   In the example above, the time slot count is 10 days, the slot duration is 1 day, and the first_event and return_event arrays are [13,2] and [5,3], respectively, under these conditions, the retention array is formed. The returned retention array is a number_steps*number_steps array. In this example, it is a 10*10 array. Therefore, this array should be divided into 10 rows to observe the results. Each row in the retention array represents the result of a bitwise "and" operation between the first_event of day i and return_events.

   ```SQL
   1,0,1,0,0,0,0,0,1,1, --Using day 1 as the starting observation point, the user returned on days 1, 3, 9, and 10, so columns 1, 3, 9, and 10 are marked as 1.
   0,0,0,0,0,0,0,0,0,0, --Using day 2 as the starting observation point, no events occurred on the second day, so the entire second row is 0.
   0,0,1,0,0,0,0,0,1,1, --Using day 3 as the starting observation point, the user returned on days 3, 9, and 10, so columns 3, 9, and 10 are marked as 1.
   0,0,0,1,0,0,0,0,1,1, --Using day 4 as the starting observation point, the user returned on days 9 and 10, so columns 9 and 10 are marked as 1. For day 4 itself, although there is no return event, a 1 is output by default in the corresponding column
   0,0,0,0,0,0,0,0,0,0, 
   0,0,0,0,0,0,0,0,0,0,
   0,0,0,0,0,0,0,0,0,0,
   0,0,0,0,0,0,0,0,0,0,
   0,0,0,0,0,0,0,0,0,0,
   0,0,0,0,0,0,0,0,0,1
   ```
   

   Aggregating these retention arrays by city, media source, and other dimensions produces retention data, such as:

   ```SQL
   select city, retention2(3)(..., ...) from ... group by city
   -- The retention array for a city is:
   22,11,1
   0,5,3
   0,0,1
   ```
   


<span id="25942118"></span>
# Function description

<span id="1abd451f"></span>
## genArrayIf()

Use the **`genArrayIf`** function to pre\-aggregate **first\-visit** (`first_events`) and **return** (`return_events`) user behavior data into specified time slots, resulting in a `Array(UInt8)` format visit overview bitset `bitset`. This step divides the time range into discrete time slots and uses bitsets to indicate whether events occurred in each slot.

```SQL
genArrayIf(number_steps, begin_timestamp, step_time)(timestamp, if_expr)
```


**Input parameters:** 


* `number_steps`: the number of time slots.

* `begin_timestamp`: analysis start timestamp. For example, if the data filter range starts from 2022\-06\-01, the start timestamp is toUInt64(toUnixTimestamp('2022\-06\-01')) = 1654012800.

* `step_time`: duration of one time slot.

* `timestamp`: column for event timestamp. Convert to timestamp first, then convert to Uint64 format.

* `if_expr`: definition of retention condition; actions that satisfy the condition are considered to have occurred.


**Output parameters:** 


* Output the `Array(UInt8)` format visit overview bitset `bitset`.


<span id="681d7135"></span>
## retention2()

Use **`retention2`** to aggregate user first visit (`first_events`) and return visit (`return_events`) bitsets to obtain retention data for each time slot.

```SQL
retention2(number_steps)(first_events, return_events)
```


**Input parameters:** 


* `number_steps`: The number of time slots. The value of `number_steps` must be consistent with the number_steps in genArrayIf.`number_steps in genArrayIf`.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><code>number_steps</code> value range is limited by the bitset size of first_events and return_events, with the rule <code>(events_array.size()-1)*8 < number_steps <= events_array.size()*8</code>. For example, in the example below, the number of UInt8 elements in first_events is 2, so the passed window size should be a value within <code>(8, 16]</code>.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The first_events array and return_events array sizes must be consistent; if not, the final calculation results will be incorrect and show many zeros.   </div>
   

* `first_events`: The bit set of first visit events, which needs to be returned by `genArrayIf`.

* `return_events`: The bit set of return events, which needs to be returned by `genArrayIf`.


**Output parameters:** 


* Output retention array in `Array(UInt64)` format.


<span id="f5a0048e"></span>
# Example usage

<span id="c80a8af3"></span>
## Example model

The example table below consists of the user behavior fact table Log and the user dimension table User, forming a commonly used star model. The following will demonstrate the specific usage of the retention analysis function based on this table.

```SQL
CREATE TABLE -- Event log table
  default.LOG (
    `Visitor` UInt32,
    `EventName` String,
    `EventTime` DateTime,
    `Province` String,
    `City` String
  ) ENGINE = CnchMergeTree
  ORDER BY Visitor;
  
  CREATE TABLE -- User table
  default.User (
    `Visitor` UInt32,
    `Fvisit_Time` DateTime,
    `Fvisit_Province` String,
    `Fvisit_City` String
  ) ENGINE = CnchMergeTree
  ORDER BY Visitor;
```


<span id="b8bc3d1e"></span>
## Event analysis

The returned result in the following example shows whether the `EventName = 'E0002'` event occurred during each unit time (1 day) within 7 days.

```SQL
SELECT
    Visitor,
    genArrayIf(7, 1654012800, 86400)(toUInt64(toUnixTimestamp(LOG.EventTime)), EventName = 'E0002') AS return_events
FROM LOG
WHERE (EventTime >= '2022-06-01') AND (EventTime < '2022-06-08') AND (EventName = 'E0002')
GROUP BY Visitor
```


<span id="35c996a8"></span>
## Retention analysis

Observe the retention from first visit ('E0001') to return visit ('E0002') within a 7\-day window grouped by city.

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

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d53c1eef73e043f486b83a545509dfc8~tplv-goo7wpa0wc-image.image" width="2392px" /></div>


Obtain a 7 by 7 array. For example, city1 is parsed as shown in the above figure:

```SQL
109777,61903,62185,62116,62064,62066,61952,
0,109978,61922,62500,61817,62671,62417,
0,0,110033,62193,62177,62230,62287,
0,0,0,109715,61833,62142,62119,
0,0,0,0,110598,62493,62515,
0,0,0,0,0,109508,61909,
0,0,0,0,0,0,110746
```


The following explains the parsing results:


* The row dimension (i) represents the user's first visit on day i, (`i=1` is day 1, and so on).

* The column dimension (j) represents the return visit on day j after the first visit.

* When i = j, the value indicates the total number of users who first visited on day i.


In the above parsing results,


* The 109,777 in the first row, first column (1,1) represents the total number of first\-time visits on day one.

* The 61,903 in the first row, second column (1,2) represents the number of people who returned on the second day after their first visit on day one.

* The 62,500 in the second row, fourth column (2,4) represents the number of people who returned on the fourth day after their first visit on day two.


You can calculate the one\-day conversion rate from day 1 to day 6 as needed. You can also adjust the time slots to week or month based on actual requirements.
