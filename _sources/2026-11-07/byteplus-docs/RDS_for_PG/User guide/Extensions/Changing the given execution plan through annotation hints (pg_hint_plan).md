---
title: "Changing the given execution plan through annotation hints (pg_hint_plan)"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/pg_hint_plan"
---

Hints PostgreSQL to change its intended execution plan via special comment statements using pg_hint_plan extension.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Unlike adjusting GUC variables to affect execution plans, which impacts all SQL in the current session, pg_hint_plan only modifies the specified single SQL execution plan to optimize a specific SQL execution plan.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Before using this extension, include pg_stat_statements and pg_hint_plan in the shared_preload_libraries parameter. For more information about how to modify parameters, refer to [Modifying parameters](https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_parameters).

<span id=".5Yib5bu65LiO5Yig6Zmk5o-S5Lu2"></span>
## Create and delete extension


* Create extension

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">A super account is required to create the extension.   </div>
   

   ```sql
   CREATE EXTENSION pg_hint_plan;
   ```
   

* Delete extension

   ```sql
   DROP EXTENSION pg_hint_plan;
   ```
   


<span id=".5L2_55So"></span>
## Usage

<span id=".5L2_55So5o-Q56S655-t6K-t"></span>
### Usage prompt phrases

pg_hint_plan reads special format prompt phrases in the target sql statement. Prompt phrases start with characters `/*+` and end with `*/`. Prompt phrases consist of prompt names and parameters, enclosed in parentheses, with space separating two parameters. To improve readability, each prompt phrase occupies one line.

The default plan in the following example is:

```sql
postgres=# create table  a(id int, name text);
CREATE TABLE
postgres=# create table  b(id int, name text);
CREATE TABLE
postgres=# explain select * from a join b on a.id=b.id;
                            QUERY PLAN                            
------------------------------------------------------------------
 Merge Join  (cost=176.34..303.67 rows=8064 width=72)
   Merge Cond: (a.id = b.id)
   ->  Sort  (cost=88.17..91.35 rows=1270 width=36)
         Sort Key: a.id
         ->  Seq Scan on a  (cost=0.00..22.70 rows=1270 width=36)
   ->  Sort  (cost=88.17..91.35 rows=1270 width=36)
         Sort Key: b.id
         ->  Seq Scan on b  (cost=0.00..22.70 rows=1270 width=36)
(8 rows)
```


Specifying `HashJoin` as the chosen join method starts with `/*+` and ends with `*/`, plan is:

```sql
postgres=# /*+
postgres*#    HashJoin(a b)
postgres*#  */
postgres-# explain select * from a join b on a.id=b.id;
                            QUERY PLAN                            
------------------------------------------------------------------
 Hash Join  (cost=38.58..346.71 rows=8064 width=72)
   Hash Cond: (a.id = b.id)
   ->  Seq Scan on a  (cost=0.00..22.70 rows=1270 width=36)
   ->  Hash  (cost=22.70..22.70 rows=1270 width=36)
         ->  Seq Scan on b  (cost=0.00..22.70 rows=1270 width=36)
(5 rows)
```


<span id=".5L2_55So5o-Q56S66KGo"></span>
### **Usage prompt table**

Using prompt phrases causes many inconveniences when the query statement cannot be edited. At this time, the prompt can be placed in the special table `hint_plan.hints`, with the table structure as follows:


|Column name |Description |
|---|---|
|id |Prompt row unique identifier. This column is auto\-filled in order. |
|norm_query_string |The pattern matching the query to prompt. Constants in the query must be replaced with `?`. Spaces also require special attention. |
|application_name |Name the session applying this prompt. An empty string indicates any session with application_name. |
|hints |Prompt phrase. Exclude comment tags. |


**Example**

```sql
--hint_plan.hints table defines prompts to use SeqScan(a) when executing EXPLAIN (COSTS false) SELECT * FROM a WHERE a.id = xxx
postgres=# INSERT INTO hint_plan.hints(norm_query_string, application_name, hints) VALUES('EXPLAIN (COSTS false) SELECT * FROM a WHERE a.id = ?;', '', 'SeqScan(a)');
INSERT 0 1
postgres=# update hint_plan.hints set hints='IndexScan(a)' where id=1;
UPDATE 1
```


<span id=".5o-Q56S657G75Z6L"></span>
### Prompt type

According to how the prompt phrases affect the execution plan, they can be divided into the following six categories: scan method, join method, join order, row number correction, parallel query, and GUC settings. The list of prompt phrases for each type can be viewed in the [prompt list](https://docs.byteplus.com/en/docs/RDS_for_PG/pg_hint_plan#.5o-Q56S65YiX6KGo).

<span id=".5omr5o-P5pa55rOV5o-Q56S6"></span>
#### Scan method prompt


* The scan method prompt forces the target table to use a specific scan method. pg_hint_plan identifies the target table by its table alias (if any). Scan methods include `SeqScan`, `IndexScan`, etc.

* Scan prompts are effective for ordinary tables, inherited tables, UNLOGGED tables, temporary tables, and system tables, but ineffective for external tables, table functions, VALUES clauses, common expressions, views, and subqueries.

* Example is as follows.

   ```sql
   postgres=# /*+
   postgres*#    IndexScan(a a_pk)
   postgres*#    SeqScan(b)
   postgres*#  */
   postgres-# explain select * from a join b on a.id=b.id;
                                    QUERY PLAN                                  
   -----------------------------------------------------------------------------
    Hash Join  (cost=14.89..48.70 rows=635 width=45)
      Hash Cond: (b.id = a.id)
      ->  Seq Scan on b  (cost=0.00..22.70 rows=1270 width=36)
      ->  Hash  (cost=13.64..13.64 rows=100 width=9)
            ->  Index Scan using a_pk on a  (cost=0.14..13.64 rows=100 width=9)
   (5 rows)
   ```
   


<span id=".6L-e5o6l5pa55rOV5o-Q56S6"></span>
#### Connection method prompt


* Connection method prompt forces specifying related tables to aggregate together.

* Connection method prompt is valid for ordinary tables, inherited tables, UNLOGGED tables, temporary tables, external tables, system tables, table functions, VALUES clauses, and common expressions, but invalid for views and subqueries.

   ```sql
   postgres=# /*+
   postgres*#    MergeJoin(a b)
   postgres*#    IndexScan(a a_pk)
   postgres*#    SeqScan(b)
   postgres*#  */
   postgres-# explain select * from a join b on a.id=b.id;
                                 QUERY PLAN                               
   -----------------------------------------------------------------------
    Merge Join  (cost=88.31..114.76 rows=635 width=45)
      Merge Cond: (a.id = b.id)
      ->  Index Scan using a_pk on a  (cost=0.14..13.64 rows=100 width=9)
      ->  Sort  (cost=88.17..91.35 rows=1270 width=36)
            Sort Key: b.id
            ->  Seq Scan on b  (cost=0.00..22.70 rows=1270 width=36)
   (6 rows)
   ```
   


<span id=".6L-e5o6l6aG65bqP5o-Q56S6"></span>
#### Join order prompt


* This prompt "Leading" indicates the join order of two or more tables. There are two methods to force specify here:

   * Force a specific join order without restricting the direction at each join level.

   * Force join direction.

* Example is as follows:

   ```sql
   postgres=# /*+
   postgres*#     NestLoop(a b)
   postgres*#     MergeJoin(a b c)
   postgres*#     Leading(a b c)
   postgres*#  */
   postgres-# EXPLAIN SELECT * FROM a
   postgres-#      JOIN b ON (a.id = b.id)
   postgres-#      JOIN c ON (b.id = c.id);
                                      QUERY PLAN                                   
   --------------------------------------------------------------------------------
    Merge Join  (cost=368.33..431.99 rows=4032 width=81)
      Merge Cond: (a.id = c.id)
      ->  Sort  (cost=280.16..281.75 rows=635 width=45)
            Sort Key: a.id
            ->  Nested Loop  (cost=0.14..250.60 rows=635 width=45)
                  ->  Seq Scan on b  (cost=0.00..22.70 rows=1270 width=36)
                  ->  Index Scan using a_pk on a  (cost=0.14..0.17 rows=1 width=9)
                        Index Cond: (id = b.id)
      ->  Sort  (cost=88.17..91.35 rows=1270 width=36)
            Sort Key: c.id
            ->  Seq Scan on c  (cost=0.00..22.70 rows=1270 width=36)
   (11 rows)
   ```
   


<span id=".6KGM5Y-357qg5q2j5o-Q56S6"></span>
#### Line number correction prompt


* Line number correction prompt corrects line number errors caused by scheduler limitations.

* Example is as follows:

   ```sql
   /*+ Rows(a b #10) */ SELECT... ;     //设置连接结果的行数量为 10。
   /*+ Rows(a b +10) */ SELECT... ;     //行数量增加 10。
   /*+ Rows(a b -10) */ SELECT... ;     //行数量减去 10。
   /*+ Rows(a b *10) */ SELECT... ;     //将行数量扩大至原来的 10 倍。
   ```
   


<span id=".5bm26KGM5omn6KGM5o-Q56S6"></span>
#### Parallel execution prompt


* Parallel query prompt forces parallel execution configuration during scanning.

* The third parameter represents intensity. soft means pg_hint_plan only changes max_parallel_worker_per_gather; hard changes all parameters to make prompt numbers effective.

* Parallel query prompts apply to ordinary tables, inheritance tables, UNLOGGED tables, and system tables; they do not apply to external tables, table functions, VALUES clauses, common table expressions (CTEs), views, or subqueries. The target object can be specified by the real name or alias of the internal table.

* The following two examples illustrate different ways to execute queries on each table:

   ```sql
   postgres=# explain /*+ Parallel(a 2 hard) Parallel(b 3 hard) */
   postgres-# select * from a join b on a.id=b.id;
                                    QUERY PLAN                                  
   -----------------------------------------------------------------------------
    Hash Join  (cost=1.25..12.36 rows=635 width=45)
      Hash Cond: (b.id = a.id)
      ->  Gather  (cost=0.00..0.00 rows=1270 width=36)
            Workers Planned: 3
            ->  Parallel Seq Scan on b  (cost=0.00..0.00 rows=410 width=36)
      ->  Hash  (cost=0.00..0.00 rows=100 width=9)
            ->  Gather  (cost=0.00..0.00 rows=100 width=9)
                  Workers Planned: 2
                  ->  Parallel Seq Scan on a  (cost=0.00..0.00 rows=59 width=9)
   (9 rows)
   
   postgres=# EXPLAIN /*+ Parallel(a 5 hard) */ SELECT sum(id) FROM a;
                                       QUERY PLAN                                    
   ----------------------------------------------------------------------------------
    Finalize Aggregate  (cost=3703.27..3703.28 rows=1 width=8)
      ->  Gather  (cost=3702.75..3703.26 rows=5 width=8)
            Workers Planned: 5
            ->  Partial Aggregate  (cost=2702.75..2702.76 rows=1 width=8)
                  ->  Parallel Seq Scan on a  (cost=0.00..0.00 rows=1081100 width=4)
   (5 rows)
   ```
   


<span id=".6K6-572u5Li05pe2IEdVQyDlj4LmlbA="></span>
#### Setting temporary GUC Parameter


* Temporarily modify the GUC Parameter during planning. The set GUC is effective if the planner's configuration Parameter does not conflict with any other Prompt. The same GUC Parameter setting is subject to the latest one.

* Example is as follows:

   ```sql
   postgres=# /*+ Set(random_page_cost 1.2) */
   SELECT * FROM a ta WHERE name = '10abc';
    id | name  
   ----+-------
    10 | 10abc
   (1 row)
   ```
   


<span id=".5o-Q56S65YiX6KGo"></span>
### **Prompt list**

All supported formats for Prompt are shown in the following table:


|Scope |File format |Note |
|---|---|---|
|Scan method prompt |SeqScan(table) |Force sequential scan. |
||TidScan(table) |Force TID scan. |
||IndexScan(table[ index...]) |Force index scan, a specific index can be specified. |
||IndexOnlyScan(table[ index...]) |Force using only index scan, a specific index can be specified. |
||BitmapScan(table[ index...]) |Force use bitmap scan. |
||NoSeqScan(table) |Force not to use sequential scanning. |
||NoTidScan(table) |Force no TID scan. |
||NoIndexScan(table) |Force not to use index scan. |
||NoIndexOnlyScan(table) |Force not to use index scan, only scan the table. |
||NoBitmapScan(table) |Force no Bitmap scan. |
|Join method prompt |NestLoop(table table[ table...]) |Force nested loop join. |
||HashJoin(table table[ table...]) |Force hash join. |
||MergeJoin(table table[ table...]) |Force using merge join. |
||NoNestLoop(table table[ table...]) |Force disable using nested loop join. |
||NoHashJoin(table table[ table...]) |Force not to use hash join. |
||NoMergeJoin(table table[ table...]) |Force not to use merge join. |
|Join order prompt |Leading(table table[ table...]) |Enforce join order. |
||Leading() |Force the order and direction of join. |
|line number correction prompt |Rows(table table[ table...] correction) |Correct the row number of the join result composed of the specified tables. Available correction methods are absolute value #<n\>, addition +<n\>, subtraction \-<n\>, and multiplication \*<n\>. <n\> is a number that the strtod function can read. |
|Parallel execution prompt |Parallel(table <# of workers\> [soft\|hard]) |Force or prohibit parallel execution for the specified table. <worker#\> is the required quantity of parallel worker process, 0 means disabling parallel execution. The third parameter, if soft (default), changes only max_parallel_workers_per_gather and leaves all other settings to the planner; if hard, all related parameters will be forced to be set. |
|Set temporary GUC parameter |Set(GUC\-param value) |set the GUC parameter to this value during planner runtime. |


<span id=".5YW25LuW"></span>
## Others

For more information, refer to [PostgreSQL official documentation](https://postgrespro.com/docs/enterprise/10/pg-hint-plan.html).
