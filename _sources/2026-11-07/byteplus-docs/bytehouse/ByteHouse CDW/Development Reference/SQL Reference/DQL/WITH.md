---
title: "WITH"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/with-clause"
---

The WITH clause can be used in queries to create a common table expression (Common Table Expression, abbreviated as CTE). A CTE creates a temporary result set that exists during the execution of a single SQL statement and can be referenced by queries. CTEs can simplify query logic and can also improve query performance by reusing repeated computations.

<span id="edc2fb88"></span>
# How to use the WITH clause

When using the WITH clause, please replace the placeholders in the example with actual fields from the data table.

<span id="db576a7e"></span>
## WITH...SELECT...


* The following queries are equivalent

   ```SQL
   WITH cte AS (
       SELECT a, SUM(b) AS c
       FROM t
       GROUP BY a
       ORDER BY c DESC
   )
   SELECT *
   FROM cte
   LIMIT 10;
   ```
   

   ```SQL
   SELECT *
   FROM (
       SELECT a, SUM(b) AS c
       FROM t
       GROUP BY a
       ORDER BY c DESC
   ) cte
   LIMIT 10;
   ```
   

* Multiple references to the WITH statement

   ```SQL
   WITH cte AS (
       SELECT a, SUM(b) AS c
       FROM t
       GROUP BY a
   )
   SELECT 
       t1.d,
       t1.a,
       t1.b,
       cte1.c AS total,
       CASE WHEN cte2.c > 10000 THEN 'X'
            ELSE 'Y'
       END AS type
   FROM t1
   JOIN cte cte1 ON t1.a = cte1.a
   JOIN cte cte2 ON t1.a = cte2.a
   WHERE t1.b > 100;
   ```
   

* Define multiple subqueries with the WITH statement

   ```SQL
   WITH
       cte1 AS (
           SELECT COUNT(*) AS cnt
           FROM t
           WHERE d = 'val'
       ),
       cte2 AS (
           SELECT COUNT(*) AS cnt
           FROM t
       )
   SELECT 
       c1.cnt AS cnt1,
       c2.cnt AS cnt2,
       (c1.cnt * 100.0 / c2.cnt) AS ratio
   FROM cte1 c1, cte2 c2;
   ```
   

* Mutual references among multiple subqueries in a WITH statement

   ```SQL
   WITH
       cte1 AS (
           SELECT a, SUM(b) AS c
           FROM t
           GROUP BY a
       ),
       cte2 AS (
           SELECT SUM(c) AS total
           FROM cte1
       ),
       cte3 AS (
           SELECT 
               c1.a,
               c1.c,
               (c1.c * 100.0 / c2.total) AS ratio
           FROM cte1 c1
           CROSS JOIN cte2 c2
       )
   SELECT *
   FROM cte3
   ORDER BY ratio DESC;
   ```
   


<span id="4cdc1a52"></span>
## INSERT...WITH...


* Use the WITH statement in INSERT

   ```SQL
   INSERT INTO target (a, c)
   WITH cte AS (
       SELECT a, SUM(b) AS c
       FROM t
       GROUP BY a
   )
   SELECT a, c
   FROM cte
   WHERE c > 10000;
   ```
   

* Use the WITH clause in INSERT OVERWRITE

   ```SQL
   INSERT OVERWRITE summary
   WITH
       cte1 AS (
           SELECT 
               a,
               SUM(b)      AS total,
               COUNT(*)    AS cnt
           FROM t
           WHERE e >= DATE '2025-01-01'
           GROUP BY a
       ),
       cte2 AS (
           SELECT 
               a,
               total * 1.0 / cnt AS avg
           FROM cte1
       )
   SELECT
       s.a,
       s.total,
       s.cnt,
       a.avg
   FROM cte1 s
   JOIN cte2 a 
       ON s.a = a.a;
   ```
   


<span id="25baf5f8"></span>
## Settings parameters

You can use the following settings parameters to optimize CTE. For detailed feature descriptions, see [Auto CTE optimization](https://docs.byteplus.com/docs/bytehouse/69448#97bccda5) and [Implicit CTE optimization](https://docs.byteplus.com/docs/bytehouse/69448#9f40d0fa).


|Parameter items |Optional values |Default value |Recommended value |Explanation |
|---|---|---|---|---|
|cte_mode |SHARED / INLINED / AUTO |AUTO |AUTO |CTE execution mode: When AUTO is enabled, shared or inlined is automatically selected based on cost. |
|enable_shared_common_plan_node |false/true |false |true |Whether to automatically detect identical parts in queries and enable AUTO CTE optimization. |


<span id="97bccda5"></span>
# Auto CTE optimization

CTE supports two execution modes: **Inline all** and **Shared**.

The **Inline all execution method** directly expands the CTE in the main query, executing it separately each time it is used. This execution mode is simpler and can make use of more optimizations, but repeated scanning and computation result in significant waste.

The **Shared execution mode** reuses results to avoid redundant computation. However, this approach prevents the optimizer from performing optimizations. For example, it does not allow the correct predicates from the parent query to be pushed down, which causes the CTE to scan a large number of unnecessary rows. It also prevents join reordering, making it impossible to achieve globally optimal join reordering. In addition, if a CTE is excessively large, the query will require a significant amount of additional memory or temporary storage, resulting in poor execution efficiency.

ByteHouse implements CBO Auto CTE optimization by enumerating Inline and Shared plans for different CTEs within a query, then selecting plans based on cost. It chooses different execution strategies for each CTE, such as **Partial Inline**, to find the globally optimal solution.

ByteHouse can set different execution modes via `settings cte_mode`:


* cte_mode='SHARED': Shared execution mode.

* cte_mode='INLINED': Inline all execution modes.

* cte_mode='AUTO': Partial Inline execution mode.


Auto CTE in ByteHouse can optimize WITH statements in queries, defined views, and CTEs produced by implicit CTEs.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9de532729e26478886042f56c10e6e83~tplv-goo7wpa0wc-image.image) </span>

Usage examples are as follows:

```SQL
WITH v as (SELECT a, b FROM t
WHERE c < 1000)
SELECT v1.* FROM v v1, v v2, v v3
WHERE v1.a = v2.a AND v2.a = v3.a
AND v3.b = 'val'
SETTINGS cte_mode = 'INLINED';
```


<span id="9f40d0fa"></span>
# **Implicit CTE optimization**

ByteHouse can enable `enable_shared_common_plan_node` to automatically detect identical parts in queries and construct CTEs.

```SQL
SELECT * FROM
(SELECT a, b FROM t WHERE c < 1000) v1
WHERE b = 'val1';
UNION ALL
SELECT * FROM
(SELECT a, b FROM t WHERE c < 1000) v2
WHERE b = 'val2'
SETTINGS enable_shared_common_plan_node = true;
```
