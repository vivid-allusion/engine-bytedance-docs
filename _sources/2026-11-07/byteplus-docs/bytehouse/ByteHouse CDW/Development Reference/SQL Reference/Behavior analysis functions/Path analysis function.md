---
title: "Path analysis function"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/path-analysis-function"
---

This tutorial introduces the basic concepts and usage of path analysis functions.

<span id="575d66e7"></span>
# Function overview

<span id="58093154"></span>
## Business scenarios

The path analysis function applies to a selected time range to analyze user behavior paths within that time. The front\-end display roughly looks like this:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/663159848a034b2f8fed18fb902f6bc1~tplv-goo7wpa0wc-image.image) </span>

Brief introduction to the path analysis calculation logic:


* First, use `pathSplit` to generate an array combining all paths of each user.

* Then use `array join` to expand the two\-dimensional array containing all paths of a single user in one row into multiple rows of single paths.

* Next, use `pathCount` to count the path conversions for all users.


<span id="1e51db52"></span>
## Basic concepts


* Event: an occurrence, also referring to a page visit node displayed in the path analysis chart in this context.

* Prop: acts as a tag attached to the corresponding event.

* Level: can also be understood as the path depth in the chart; paths longer than x nodes are truncated.

* Node: in the context of path analysis, each node represents a page.

* Edge: the visit path from page 1 to page 2.


<span id="cd6794b5"></span>
# Function definition

<span id="b65acd06"></span>
## pathSplit()

Use `pathSplit` to generate an array combining all paths of each user.

```Python
pathSplit(session_time, level)(timestamp, event, prop)
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/54df3ef9b1be4aa69d49b05f0167f149~tplv-goo7wpa0wc-image.image) </span>

**Input parameters**:


* `session_time`: the time window for path analysis, with units consistent with `timestamp`. In the example below, it is 600 seconds, meaning paths formed within 10 minutes after the first event occurrence are calculated.

* `level`: path depth, truncates the path after x nodes.

* `timestamp`: the timestamp column, which needs to be converted to a timestamp first, then to Uint64 format.

* event: event column, only supports numerical type, requires explicit specification through multiIf. As in the example: `multiIf(EventName = 'E0001', 1, EventName = 'E0002', 2, EventName = 'E0003', 3, 0) AS e`.

* `prop`: property column, use `''` as a placeholder if absent.


**Output parameters (intermediate results)** :

Returns a two\-dimensional array: [(e1, p1), (e2, p2), (e1, p2)]


* (ex, px): corresponds to the event stream, that is, the events occurring on this path.

* e: event, corresponds to the event number defined by multiIf in the event colum`multiIf in the event` column.

* p: event property, corresponds to `prop`.


<span id="991a0d2d"></span>
## pathCount()

Use `arrayjoin` to expand a two\-dimensional array that contains all paths for a single user in one row into multiple rows with a single path each, then use `pathCount` to count path conversion for all users. Examples are as follows:

```Python
pathCount(y, x)(path, cnt1, cnt2)
```


```SQL
SELECT pathCount(3, 3)(path, 1, cnt)
FROM
(
 SELECT
 path AS path, count() AS cnt
 FROM
 (
 SELECT arrayJoin(pathSplit(600, 3)(toUInt64(toUnixTimestamp(LOG.EventTime)), multiIf(EventName = 'E0001', 1, EventName = 'E0002', 2, EventName = 'E0004', 3, 0) AS e, '')) AS path
 FROM LOG
 WHERE (EventTime >= '2022-06-01 00:00:00') AND (EventTime < '2022-06-02 00:00:00') AND (EventName IN ('E0001', 'E0002', 'E0004')) AND (Visitor = 964049)
 GROUP BY Visitor
 )
 GROUP BY path
)
```


pathCount returns data needed for display, where x represents the horizontal path depth (4 columns in the diagram below). The frontend needs data showing nodes represented by light blue blocks and edges between these blocks, both output by `pathCount`.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/54df3ef9b1be4aa69d49b05f0167f149~tplv-goo7wpa0wc-image.image) </span>


* `y`: vertical single\-layer display depth, shown as the yellow circled area in the diagram above, where y = 5;

* `x`: horizontal path depth, paths are truncated after x nodes, where x = 4 in the diagram above;

* `path`: `pathSplit` returned path column (needs to be expanded using arrayJoin);

* `cnt1`: path weight 1, usually set to 1, used to count deduplicated occurrences of the path;

* `cnt2`: path weight 2, usually set to the count from the `pathSplit` subquery’s `count()` to calculate the total occurrences without deduplication of the path.


**return format**:


* Return format is a 3\-tuple ([node_index], [nodes], [edges]), which together form a flowchart of page path conversion.

* `node_index`: format is `(event, prop)`, showing event nodes.

   * `event` is the index number of the event. If `pathSplit` previously filled `event` with `multiIf(EventName = 'E0001', 1, EventName = 'E0002', 2, EventName = 'E0004', 3, 0)`, then returning 1 corresponds to 'E0001', 2 to 'E0002', and 3 to 'E0004';

   * `prop` is the prop passed into pathSplit.

* `nodes`: a two\-dimensional array. Indicates the unique count and total count each node appears at each level (index starting at 0), format: (lev (index starting at 0), format: (level, node_index, cnt1, cnt2).

   * `level`: the current level of the node;

   * `node_index`: index of the event, referring to the mapping relation between the node_index array and events;

   * `cnt1`: unique visits to the node;

   * `cnt2`: total visits to the node.

* `edge`: a two\-dimensional array recording the deduplicated count and total count of each edge appearing at each level, in the format: `(level, from_node_index, to_node_index, cnt1, cnt2)`.

   * `level`: level, which is the input x;

   * `from_node_index`: source node, referring to the mapping between events in the `node_index` array;

   * `to_node_index`: target node, referring to the mapping between events in the `node_index` array; `to_node_index` is marked as 65535 when `from_node_index` is the endpoint, meaning the user dropped off after this event;

   * `cnt1`: deduplicated visits to the node;

   * `cnt2`: total visits to the node.


<span id="150d21c5"></span>
# Usage example

<span id="b7d78223"></span>
## Example model

The example table below is a commonly used star schema composed of the user behavior fact table Log and the user dimension table User. The retention analysis function will be demonstrated based on this table.

```SQL
CREATE TABLE -- event log table
  default.LOG (
    `Visitor` UInt32,
    `EventName` String,
    `EventTime` DateTime,
    `Province` String,
    `City` String
  ) ENGINE = CnchMergeTree
  ORDER BY Visitor;
  
  CREATE TABLE -- user table
  default.User (
    `Visitor` UInt32,
    `Fvisit_Time` DateTime,
    `Fvisit_Province` String,
    `Fvisit_City` String
  ) ENGINE = CnchMergeTree
  ORDER BY Visitor;
```


<span id="ff24c08b"></span>
## Page path analysis

This example specifies a user Visitor = 964049 for illustration.

This example covers path data for events 'E0001', 'E0002', and 'E0004' occurring between 2022/6/1 and 2022/6/2, showing page information within 10 minutes after the events and displaying a page path depth of 3 levels.

First, calculate intermediate results using `pathSplit`:

```SQL
SELECT Visitor,pathSplit(600, 3) (toUInt64(toUnixTimestamp(LOG.EventTime)), multiIf(EventName = 'E0001', 1, EventName = 'E0002', 2, EventName = 'E0004', 3, 0) AS e, '') AS path
FROM LOG
WHERE (EventTime >= '2022-06-01 00:00:00')
  AND (EventTime < '2022-06-02 00:00:00')
  AND (EventName IN ('E0001', 'E0002', 'E0004'))
  and Visitor = 964049
GROUP BY Visitor

--返回：
┌─Visitor─┬─path────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┐
│  964049 │ [[(1,''),(2,''),(3,'')],[(1,'')],[(1,''),(2,''),(3,'')],[(1,''),(2,''),(2,'')],[(1,'')],[(1,'')],[(1,'')],[(1,''),(3,''),(3,'')],[(1,''),(2,''),(3,'')],[(1,''),(1,''),(3,'')],[(1,'')],[(1,''),(2,''),(3,'')],[(1,'')],[(1,''),(2,''),(2,'')]] │
└─────────┴─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
```


Then, use arrayJoin to expand the two\-dimensional array of multiple paths returned by the single\-row path into multiple rows with individual paths and count the occurrences of each path.

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
 --返回
┌─path───────────────────┬─cnt─┐
│ [(1,'')]               │   6 │
│ [(1,''),(1,''),(3,'')] │   1 │
│ [(1,''),(2,''),(3,'')] │   4 │
│ [(1,''),(2,''),(2,'')] │   2 │
│ [(1,''),(3,''),(3,'')] │   1 │
└────────────────────────┴─────┘
```


Next, calculate the final 3\*3 result with `pathCount` (path depth of 3, showing up to 3 nodes per level):

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
--返回
┌─pathCount(5, 3)(path, 1, cnt)─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┐
│ ([(1,''),(3,''),(2,'')],
[[0,0,5,14],[1,0,1,1],[1,1,1,1],[1,2,2,6],[2,1,3,6],[2,2,1,2]],
[[0,0,0,1,1],[0,0,1,1,1],[0,0,65535,1,6],[0,0,2,2,6],[1,2,2,1,2],[1,1,1,1,1],[1,0,1,1,1],[1,2,1,1,4]]) │
└───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
```


The result is:


* `node_index`: [(1, ''), (3, ''), (2, '')], mapping event IDs as 0\-\>1 (E0001), 1\-\>3 (E0004), 2\-\>2 (E0002)

* `nodes`：[[0,0,5,14],[1,0,1,1],[1,1,1,1],[1,2,2,6],[2,1,3,6],[2,2,1,2]]

   * Level 1, [0, 0, 5, 14]

      * Only one node "Event 1," which is E0001;

      * The deduplicated visits for this node are 5, with a total of 14 visits.

   * Level 2, [1,0,1,1],[1,1,1,1],[1,2,2,6]

      * Three events occurred: E0001, E0004, E0002

      * The deduplicated visits for the three nodes are 1, 1, 2; total visits are 1, 1, 6

   * ....

* edge：[0,0,0,1,1],[0,0,1,1,1],[0,0,65535,1,6],[0,0,2,2,6],[1,2,2,1,2],[1,1,1,1,1],[1,0,1,1,1],[1,2,1,1,4]

   * Level 1 has the following edges:

      * 0\-\>0: that is, 'E0001' \-\> 'E0001', 1 visit;

      * 0\-\>1: 1 visit;

      * 0\-\>65535 (endpoint), 1 deduplicated visit;

      * 0\-\>2, 2 unique visits.

   * At level two, the following edges exist:

      * 2\-\>2, 1 unique visit;

      * 1\-\>1, 1 unique visit;

      * 0\-\>1, 1 unique visit;

      * 2\-\>1, 1 unique visit.


Results can be supplemented as page path analysis, such as

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/facdbbf039ba464b8c11a0eaaf553cb9~tplv-goo7wpa0wc-image.image) </span>
