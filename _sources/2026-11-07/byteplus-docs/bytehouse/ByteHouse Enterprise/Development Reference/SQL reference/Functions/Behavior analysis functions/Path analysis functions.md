---
title: "Path analysis functions"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/path-analysis-functions"
---

This article introduces the usage scenarios and basic methods of path analysis functions.
Path analysis functions business scenario: Select a specific time range to analyze user behavior paths within this period.
<span id="dfc6ac1b"></span>
## pathSplit()
Using **pathSplit** to generate an array consisting of all path combinations for **each user**.
```Python
pathSplit(session_time, level)(timestamp, event, prop)
```

**Input Parameters:**

* Session_time: The time window for path analysis, the unit is consistent with timestamp, in the example below, it is 600 seconds, which means only paths formed within 10 minutes after the first event are calculated.
* `Level`: Path depth, truncating the path beyond x nodes.
* `Timestamp`: The column where **timestamps** are located, needs to be converted into timestamps, then transformed into Uint64 format.
* `Event`: Event column, only supports numerical type, needs to be explicitly specified through **multiIf**.

As in the following example: `multiIf(EventName = 'E0001', 1, EventName = 'E0002', 2, EventName = 'E0003', 3, 0) AS e`

* `Prop`: attribute column, use `''` as a placeholder if not present;

**Output parameter (intermediate result):**
Returns a two-dimensional array: [(e1, p1), (e2, p2), (e1, p2)]

* (ex,px): corresponds to the event stream, i.e., the events that occur on this path
* e: event, corresponds to the event number defined by `event` in the `multiif` column
* p: event attribute, corresponds to `prop`

<span id="8a8b9d0d"></span>
## pathCount()
Use **array join** to unfold a two-dimensional array containing all paths for a single user into multiple rows of individual paths.
Use **pathCount** to tally the path conversion situation for all users.
```Python
pathCount(y, x)(path, cnt1, cnt2)
```

pathCount returns the data needed for the display interface, where x represents the horizontal path depth (as shown in the above diagram, 4).
The data needed for the front-end display are actually each light blue block representing a node, and the edges between the light blue blocks, all output by pathCount.

* `y`: **Vertical single-layer display depth**, as shown in the yellow circled part of the diagram, i.e., y = 5.
* `x`: **Horizontal path depth**, truncate the path after x nodes, as shown in the above diagram where x = 4.
* `path`: `pathSplit`'s return path column (needs to be expanded using arrayJoin).
* `cnt1`: Path weight 1, usually just passing 1 is fine, used to calculate the **deduplicated frequency of paths.**
* `cnt2`: Path weight 2, usually pass the cnt obtained from the `pathSplit` sub-query's `count()` to find the **total frequency of paths without deduplication.**

Return format:

* The return format is a triplet ([node_index], [nodes], [edges]), used to form a flowchart of webpage path conversion through this result set:
* `node_index`: Format: `(event, prop)`, displaying event nodes.
   * `Event` has an index notation for events. If it was specified during pathSplit as multiIf(EventName = 'E0001', 1, EventName = 'E0002', 2, EventName = 'E0004', 3, 0), the results return 1 for 'E0001', 2 for 'E0002', and 3 for 'E0004'.
   * `Prop` is a property passed into pathSplit.
* `Nodes`: a two-dimensional array. Indicates the unique count and total count of each **node** at various levels (starting from level 0, indexed by level), formatted as: `(level, node_index, cnt1, cnt2)`.
   * Level: hierarchy level.
   * Node_index: the index of events, referring to the mapping relation in the node index array.
   * Cnt1: unique visitation count of a node.
   * Cnt2: total visitation count of a node.
* Edge: a two-dimensional array, where each **edge** has unique and total counts at various levels, formatted as:

`(level, from_node_index, to_node_index, cnt1, cnt2)`

* Level: The hierarchy, referring to the input x.
* from_node_index: Source node, refer to the mapping relationship in the node_index array with the event.
* to_node_index: Target node, refer to the mapping relationship in the node_index array with the event; to_node_index is marked with 65535 when from_node_index is the endpoint, which indicates user drop-out after this event.
* cnt1: The number of unique visits to the node.
* cnt2: The number of visits to the node.

<span id="45c4f06d"></span>
## Path analysis SQL examples
Specify a user, Visitor = 964049, for illustration.
This example covers the path data of events 'E0001', 'E0002', 'E0004' between 2022/6/1 and 2022/6/2, showing page information within 10 minutes after the events occurred, with a display path depth of 3 levels.
Firstly, calculate the intermediate results through pathSplit:
```SQL
SELECT Visitor,pathSplit(600, 3) (toUInt64(toUnixTimestamp(LOG.EventTime)), multiIf(EventName = 'E0001', 1, EventName = 'E0002', 2, EventName = 'E0004', 3, 0) AS e, '') AS path
FROM LOG
WHERE (EventTime >= '2022-06-01 00:00:00')
  AND (EventTime < '2022-06-02 00:00:00')
  AND (EventName IN ('E0001', 'E0002', 'E0004'))
  and Visitor = 964049
GROUP BY Visitor

--Return
┌─Visitor─┬─path────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┐
│  964049 │ [[(1,''),(2,''),(3,'')],[(1,'')],[(1,''),(2,''),(3,'')],[(1,''),(2,''),(2,'')],[(1,'')],[(1,'')],[(1,'')],[(1,''),(3,''),(3,'')],[(1,''),(2,''),(3,'')],[(1,''),(1,''),(3,'')],[(1,'')],[(1,''),(2,''),(3,'')],[(1,'')],[(1,''),(2,''),(2,'')]] │
└─────────┴─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
```

Then, by using arrayJoin, expand the single-row path returned in a two-dimensional array into multiple single-path rows and calculate the frequency of each path.
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

Then, calculate the final 3*3 result through pathCount, with path depth as 3 and each layer displaying a maximum of 3 nodes:
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

* `node_index`: [(1,''),(3,''),(2,'')] represents event numbers mapped as 0->1(E0001), 1->3(E0004), 2->2(E0002)
* `nodes`：[[0,0,5,14],[1,0,1,1],[1,1,1,1],[1,2,2,6],[2,1,3,6],[2,2,1,2]]
   * Level 1, [0,0,5,14]
      * Only one node "event 1", namely E0001;
      * The node had 5 unique visits and 14 total visits
   * Level 2, [1,0,1,1],[1,1,1,1],[1,2,2,6]
      * Three events occurred: E0001, E0004, E0002
      * The three nodes had unique visits of 1, 1, 2; total visits of 1, 1, 6
   * ....
* edge：[0,0,0,1,1],[0,0,1,1,1],[0,0,65535,1,6],[0,0,2,2,6],[1,2,2,1,2],[1,1,1,1,1],[1,0,1,1,1],[1,2,1,1,4]
   * The first layer includes the following edges:
      * 0->0: i.e., 'E0001'->'E0001', 1 access
      * 0->1: 1 access
      * 0->65535 (i.e., already the endpoint), 1 deduplicated visit
      * 0->2, 2 deduplicated visits
   * The second layer includes the following edges:
      * 2->2, 1 deduplicated visit
      * 1->1, 1 deduplicated visit
      * 0 to 1, 1 unique visit
      * 2 to 1, 1 unique visit

The result can be supplemented with page path analysis, such as
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/facdbbf039ba464b8c11a0eaaf553cb9~tplv-goo7wpa0wc-image.image =1140x)
