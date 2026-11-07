---
title: "Retention analysis functions"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/retention-analysis-functions"
---

This article introduces the use scenarios for retention analysis functions and their basic usage.
Business scenario of retention analysis functions: Select a time range, observe the retention of users meeting a certain dimension in each time unit within this time range after a specified period.
<span id="65905d8c"></span>
## genArrayIf()
Using **`genArrayIf`** function to pre-aggregate**first visit**(`first_events`) and **return visit**(`return_events`) behavioral data into specified time slots, obtaining a `Array(UInt8)` formatted visits overview bitset `bitset`. This step divides the time range into discrete time slots, and uses a bitset to represent the occurrence of events in each slot.
```SQL
genArrayIf(number_steps, begin_timestamp, step_time)(timestamp, if_expr)
```

**Input Parameters:**

* `number_steps`: The number of time slots.
* `begin_timestamp`: Analysis start timestamp, as data filtering range starts from 2022-06-01, so the start timestamp is toUInt64(toUnixTimestamp('2022-06-01')) = 1654012800.
* `step_time`: Duration of one time slot.
* `timestamp`: Column where the event timestamp is located. Firstly, convert it into a timestamp, then into Uint64 Format.
* `if_expr`: Defines the retention conditions; behaviors meeting these conditions are considered to have occurred.

**Output parameters:**

* Outputs a bitset in the format of `Array(UInt8)` showing visit occurrences `bitset`.

**Example:**
In the example below, the result expresses whether the event `EventName = 'E0002'` occurred in each unit time (1 day) over 7 days.
```SQL
SELECT
    Visitor,
    genArrayIf(7, 1654012800, 86400)(toUInt64(toUnixTimestamp(LOG.EventTime)), EventName = 'E0002') AS return_events
FROM LOG
WHERE (EventTime >= '2022-06-01') AND (EventTime < '2022-06-08') AND (EventName = 'E0002')
GROUP BY Visitor
```

<span id="7491f0e9"></span>
## retention2()
Use **`retention2`** to aggregate user first visits (`first_events`) and return visits (`return_events`) bitsets to obtain retention data for each time slot.
```SQL
retention2(number_steps)(first_events, return_events)
```

**Input parameters:**

* `number_steps`: Number of time slots. `number_steps` values should be consistent with `genArrayIf` in `number_steps`.

:::tip
Advisory:

* `number_steps` value range is limited by the Size of the initial visit (first_events) and return visit (return_events) **bit set**, the Rules are `(events_array.size()-1)*8< number_steps <= events_array.size()*8`. For instance, if the UInt8 Type Element Quantity in first_events is 2 in this example, the entered window size should be a value in the `(8, 16]` range.
* The sizes of the initial visit array and return visit array need to be consistent. If they are inconsistent, the final calculation Result will be incorrect, resulting in many zeros.
:::

* `first_events`: Bitset for initial visit events, requires a return from `genArrayIf`.
* `return_events`: Bitset for return visit events, requires a return from `genArrayIf`.

**Output Parameters:**

* Output an array in `Array(UInt64)` format for retention.

**Example SQL:**
Observe a 7-day window, group by city, and analyze retention from initial visit ("E0001") to return visit ("E0002").
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

Get a 7x7 array, as interpreted for city1 in the diagram above.
```SQL
109777,61903,62185,62116,62064,62066,61952,
0,109978,61922,62500,61817,62671,62417,
0,0,110033,62193,62177,62230,62287,
0,0,0,109715,61833,62142,62119,
0,0,0,0,110598,62493,62515,
0,0,0,0,0,109508,61909,
0,0,0,0,0,0,110746
```

Calculate the daily conversion rate from Day1 to Day6 as needed.
According to actual needs, the time slots can be amended to weeks, months, etc.
