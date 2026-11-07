---
title: "Incremental view maintenance (pg_ivm)"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/pg_ivm"
---

Support pg_ivm extension, which provides the incremental view maintenance (IVM) function for RDS for PostgreSQL.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Incremental view maintenance (IVM) is a method to keep materialized views up to date by computing and applying only incremental changes to the views, rather than recalculating the entire content from scratch like REFRESH MATERIALIZED VIEW. IVM can update materialized views more efficiently than recalculation when only a small part of the view is changed.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

The pg_ivm extension is only supported on instances with PostgreSQL version 13 or above. To use this extension, make sure to select the appropriate instance version when creating an instance.

<span id=".5Yib5bu65LiO5Yig6Zmk5o-S5Lu2"></span>
## Create and delete extension


* Create extension

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">A super account is required to create the extension.   </div>
   

   ```sql
   CREATE EXTENSION pg_ivm;
   ```
   

* Delete extension

   ```sql
   DROP EXTENSION pg_ivm;
   ```
   


<span id=".5L2_55So"></span>
## Usage

We support the incremental maintainable materialized view (immv) for ivm materialized views. To create immv, call the create_immv function with the table name and view definition statement. For example:

```sql
testdb=> CREATE TABLE mv_base_a (i int, j int);
CREATE TABLE
testdb=> INSERT INTO mv_base_a VALUES
testdb->   (1,10),
testdb->   (2,20),
testdb->   (3,30),
testdb->   (4,40),
testdb->   (5,50);
INSERT 0 5
testdb=> CREATE TABLE mv_base_b (i int, k int);
CREATE TABLE
testdb=> INSERT INTO mv_base_b VALUES
testdb->   (1,101),
testdb->   (2,102),
testdb->   (3,103),
testdb->   (4,104);
INSERT 0 4
-- create immv
testdb=> SELECT create_immv('mv_ivm_1', 'SELECT i,j,k FROM mv_base_a a INNER JOIN mv_base_b b USING(i)');
NOTICE:  could not create an index on immv "mv_ivm_1" automatically
DETAIL:  This target list does not have all the primary key columns, or this view does not contain GROUP BY or DISTINCT clause.
HINT:  Create an index on the immv for efficient incremental maintenance.
 create_immv
-------------
           4
(1 row)

testdb=> SELECT * FROM mv_ivm_1 ORDER BY 1,2,3;
 i | j  |  k
---+----+-----
 1 | 10 | 101
 2 | 20 | 102
 3 | 30 | 103
 4 | 40 | 104
(4 rows)

testdb=> BEGIN;
BEGIN
testdb=*> INSERT INTO mv_base_b VALUES(5,105);
INSERT 0 1
testdb=*> SELECT * FROM mv_ivm_1 ORDER BY 1,2,3; -- insert data automatically updates immv
 i | j  |  k
---+----+-----
 1 | 10 | 101
 2 | 20 | 102
 3 | 30 | 103
 4 | 40 | 104
 5 | 50 | 105
(5 rows)

testdb=*> UPDATE mv_base_a SET j = 0 WHERE i = 1;
UPDATE 1
testdb=*> SELECT * FROM mv_ivm_1 ORDER BY 1,2,3; -- update data automatically updates immv
 i | j  |  k
---+----+-----
 1 |  0 | 101
 2 | 20 | 102
 3 | 30 | 103
 4 | 40 | 104
 5 | 50 | 105
(5 rows)

testdb=*> DELETE FROM mv_base_b WHERE (i,k) = (5,105);
DELETE 1
testdb=*> SELECT * FROM mv_ivm_1 ORDER BY 1,2,3; -- delete data automatically updates immv
 i | j  |  k
---+----+-----
 1 |  0 | 101
 2 | 20 | 102
 3 | 30 | 103
 4 | 40 | 104
(4 rows)

testdb=> ROLLBACK;
ROLLBACK
```


<span id=".5o-S5Lu25YWD5pWw5o2u"></span>
## Extension metadata

pg_ivm_immv stores immv information.


|Parameter |Type |Description |
|---|---|---|
|immvrelid |regclass |OID of IMMV. |
|viewdef |text |The parse tree of view definition (this is a decompiled reconstruction, not the command's original text, use get_immv_def to retrieve the original text). |
|ispopulated |bool |true if IMMV is currently populated. |


```sql
testdb=> SELECT immvrelid,get_immv_def(immvrelid),ispopulated FROM pg_ivm_immv ORDER BY 1;
 immvrelid |           get_immv_def           | ispopulated 
-----------+----------------------------------+-------------
 mv_ivm_1  |  SELECT a.i,                    +| t
           |     a.j,                        +| 
           |     b.k                         +| 
           |    FROM (mv_base_a a            +| 
           |      JOIN mv_base_b b USING (i)) | 
 mv        |  SELECT i                       +| t
           |    FROM t                        | 
(2 rows)
```


<span id=".5o-S5Lu25Ye95pWw"></span>
## Extension functions

<span id="create_immv"></span>
### **create_immv**

Use the create_immv function to create immv. Usage example of create_immv function:

```sql
create_immv(immv_name text, view_definition text) RETURNS bigint
```


create_immv defines a new IMMV for querying. Create a table named immv_name, execute the query specified by view_definition, and use it to populate the IMMV. The query is stored in pg_ivm_immv for later refresh during incremental view maintenance. create_immv returns the number of rows in the created IMMV.

```sql
testdb=> CREATE TABLE t (i int PRIMARY KEY);
CREATE TABLE
testdb=> INSERT INTO t SELECT generate_series(1, 100);
INSERT 0 100
testdb=> SELECT create_immv('mv', 'SELECT * FROM t');
NOTICE:  created index "mv_index" on immv "mv"
 create_immv
-------------
         100
(1 row)
```


<span id="refresh_imm"></span>
### **refresh_imm**

Use the refresh_immv function to refresh the IMMV. Usage example of refresh_immv function:

```sql
refresh_immv(immv_name text, with_data bool) RETURNS bigint
```


The refresh_immv function can completely replace the content of the IMMV, similar to what the REFRESH MATERIALIZED VIEW command does for materialized views. To execute this function, you must be the owner of the IMMV (using PostgreSQL 16 or earlier) or have MAINTAIN privileges on the IMMV (using PostgreSQL 17 or later). After executing the refresh_immv function, the old content in IMMV will be discarded. The with_data flag corresponds to the WITH [NO] DATA option of the REFRESH MATERIALIZED VIEW command.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If you use PostgreSQL 17 or later, search_path temporarily changes to pg_catalog, pg_temp when running refresh_immv.</div>


```sql
testdb=> SELECT immvrelid, ispopulated FROM pg_ivm_immv where immvrelid='mv'::regclass;
 immvrelid | ispopulated 
-----------+-------------
 mv        | t
(1 row)

testdb=> SELECT refresh_immv('mv', true);  -- Refresh IMMV with data
 refresh_immv
--------------
          100
(1 row)

testdb=> SELECT immvrelid, ispopulated FROM pg_ivm_immv where immvrelid='mv'::regclass;
 immvrelid | ispopulated
-----------+-------------
 mv        | t
(1 row)

testdb=> INSERT INTO t VALUES(101);
INSERT 0 1
testdb=> SELECT i FROM mv ORDER BY 1 desc limit 1; -- insert original table data automatically updated to immv
  i
-----
 101
(1 row)

testdb=> SELECT refresh_immv('mv', false);  -- Make IMMV unpopulated
 refresh_immv
--------------
            0
(1 row)

testdb=> SELECT immvrelid, ispopulated FROM pg_ivm_immv where immvrelid='mv'::regclass;
 immvrelid | ispopulated
-----------+-------------
 mv        | f
(1 row)

testdb=> SELECT i FROM mv ORDER BY 1 desc limit 1; -- no data because immv is unpopulated
 i
---
(0 rows)

testdb=> INSERT INTO t VALUES(102);
INSERT 0 1
testdb=> SELECT i FROM mv ORDER BY 1 desc limit 1; -- because immv is unpopulated, insert will not update
 i
---
(0 rows)

testdb=> SELECT refresh_immv('mv', true); -- Refresh the IMMV and make it populated.
 refresh_immv
--------------
          102
(1 row)

testdb=> SELECT i FROM mv ORDER BY 1 desc limit 1; -- data recovery in immv is normal
  i
-----
 102
(1 row)

testdb=> INSERT INTO t VALUES(103);
INSERT 0 1
testdb=> SELECT i FROM mv ORDER BY 1 desc limit 1; -- insert original table data automatically updated to immv
  i
-----
 103
(1 row)

testdb=>
```


<span id="get_immv_def"></span>
### **get_immv_def**

the get_immv_def function is used to reconstruct the underlying SELECT command of IMMV. An example of using the get_immv_def function is as follows:

```sql
get_immv_def(immv regclass) RETURNS text
```


```sql
testdb=> SELECT immvrelid, get_immv_def(immvrelid) FROM pg_ivm_immv ORDER BY 1;
 immvrelid |           get_immv_def           
-----------+----------------------------------
 mv_ivm_1  |  SELECT a.i,                    +
           |     a.j,                        +
           |     b.k                         +
           |    FROM (mv_base_a a            +
           |      JOIN mv_base_b b USING (i))
 mv        |  SELECT i                       +
           |    FROM t
(2 rows)
```


&nbsp;

<span id=".57qm5p2f"></span>
## Constraints

<span id=".6IGa5ZCI"></span>
### Aggregate

Supported aggregate functions include count, sum, avg, min, and max. Currently only built\-in aggregate functions are supported; user\-defined aggregates are not available.

Precautions:


* For min or max, when tuples containing the current minimum or maximum are deleted from the base table, new values may be recalculated from the base table based on the affected groups. Therefore, updating an IMMV containing these functions may take a long time.

* Using sum or avg on real (float4) or double precision (float8) types in an IMMV is unsafe because the aggregate values in the IMMV may differ from those computed from the base table due to the limited precision of these types. To avoid this issue, use the numeric type instead.


If there is a GROUP BY clause, the expressions specified in the GROUP BY must appear in the target list. This is how tuples to update in the IMMV are identified. These attributes are used as scan keys to search tuples in the IMMV and therefore must be indexed for efficient IVM.

<span id=".5a2Q5p-l6K-i"></span>
### Subquery

Subqueries with EXISTS in the FROM clause and simple subqueries are supported. EXISTS subqueries that are not combined with AND and those in the target list are not supported. EXISTS subqueries are only supported in WHERE clauses and not in target lists.

If EXISTS references columns from tables in the outer query, these columns must be included in the target list. Subqueries containing aggregate functions or DISTINCT are not supported.

<span id="CTE"></span>
### CTE

Simple CTEs (WITH queries) are supported; WITH queries containing aggregate functions or DISTINCT are not supported.

Recursive queries (WITH RECURSIVE) are not allowed. Unreferenced CTEs are also not allowed; in view definition queries, CTEs must be referenced at least once.

<span id="DISTINCT"></span>
### DISTINCT

DISTINCT is allowed in the definition query of IMMV. Assuming IMMV is defined using DISTINCT on base tables containing duplicate tuples. When tuples are deleted from the base table, tuples in the view are deleted if and only if the tuple count becomes zero. Additionally, when tuples are inserted into the base table, tuples are inserted into the view only if the same tuples do not exist in the view.

<span id="TRUNCATE"></span>
### TRUNCATE

When the base table is truncated, if the view definition query does not include aggregation without a GROUP BY clause, the IMMV is also truncated, and its contents become empty. Aggregated views without a GROUP BY clause always have only one row. Therefore, in this case, if the base table is truncated, the IMMV is only refreshed and not truncated.

<span id=".5YW25LuW"></span>
## Others

For more information, refer to [official documentation](https://github.com/sraoss/pg_ivm/blob/v1.9/README.md).
