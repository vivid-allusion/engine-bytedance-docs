---
title: "SELECT statement"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/ce-select-statement"
---

The `SELECT` statement can be used to perform data retrieval. By default, the requested data is returned to the client. At the same time, by using `INSERT INTO`, it can be forwarded to different tables.

<span id="b618a15c"></span>
# Overall grammar

All clauses are optional except for the required expression list `expr_list` that immediately follows `SELECT`.

```SQL
[WITH expr_list|(subquery)] 
SELECT [DISTINCT] expr_list
[FROM [db.]table | (subquery) | table_function] [FINAL]
[SAMPLE sample_coeff]
[ARRAY JOIN ...]
[ANY|ALL|ASOF] [INNER|LEFT|RIGHT|FULL|CROSS] [OUTER|SEMI|ANTI] JOIN (subquery)|table (ON <expr_list>)|(USING <column_list>)
[PREWHERE expr]
[WHERE expr]
[GROUP BY expr_list] [WITH TOTALS]
[HAVING expr]
[ORDER BY expr_list] [WITH FILL] [FROM expr] [TO expr] [STEP expr]
[LIMIT [offset_value, ]n BY columns]
[LIMIT [n, ]m] [WITH TIES]
[UNION ALL ...]
[settingsClause]
[INTO OUTFILE filename]
[FORMAT format]
```


<span id="2140be96"></span>
# SELECT clause

<span id="0f1d1649"></span>
## Grammar

```SQL
SELECT [DISTINCT] expr_list
```


<span id="13ad158b"></span>
## **Parameter description**


|Parameters |Description |
|---|---|
|DISTINCT |Optional. It is used to remove duplicate rows from query results. When processing `NULL` values, all `NULL` values are treated as the same value. |
|`*` (asterisk) |The expression can be used at any position in the query as a replacement, and when the query is executed, it will automatically expand to a list of all columns in the table (excluding `MATERIALIZED` and `ALIAS` columns). |
|AS alias |You can assign custom names to columns in query results to improve readability. |


<span id="6850f611"></span>
## **Usage scenarios**


* To include all columns in the results, use the asterisk (`*`) symbol. For example,

   ```SQL
   SELECT * FROM ...
   ```
   

* Columns in the result that contain 'a' can be expressed using `COLUMNS`.

   ```SQL
   SELECT COLUMNS('a') FROM table_name;
   ```
   


<span id="33a4a9a2"></span>
## **Example 1**

Query columns in the table whose names contain 'a'

```SQL
-- 1. Create the required libraries
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create an example table
CREATE TABLE IF NOT EXISTS sample_db.col_names ON CLUSTER sample_cluster (
  aa Int8, 
  ab Int8, 
  bc Int8
) 
ENGINE = MergeTree 
ORDER BY aa;

-- 3. Insert test data
INSERT INTO sample_db.col_names 
VALUES 
  (1, 2, 3),(4, 5, 6);

-- 4. Query operations
SELECT COLUMNS('a') FROM sample_db.col_names
```


Output results:

```Plain
   ┌─aa─┬─ab─┐
   │  1 │  2 │
   │  4 │  5 │
   └────┴────┘
```


<span id="20202150"></span>
## **Example 2**

Use multiple `COLUMNS` expressions and apply functions to columns.

```SQL
-- 1. Create required libraries
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a sample table
CREATE TABLE IF NOT EXISTS sample_db.col_names ON CLUSTER sample_cluster (
  aa Int8,
  ab Int8,
  bc Int8
) 
ENGINE = MergeTree 
ORDER BY aa;

-- 3. Insert test data
INSERT INTO sample_db.col_names 
VALUES 
  (1, 2, 3),(4, 5, 6);

-- 4. Query operations
SELECT COLUMNS('a'), COLUMNS('c'), toTypeName(COLUMNS('c')) FROM sample_db.col_names 
```


Output results:

```Plain
   ┌─aa─┬─ab─┬─bc─┬─toTypeName(bc)─┐
   │  1 │  2 │  3 │ Int8           │
   │  4 │  5 │  6 │ Int8           │
   └────┴────┴────┴────────────────┘
```


Each column returned by the `COLUMNS` expression is passed to the function as a separate parameter. If the function supports additional parameters, you can also pass additional parameters to the function.

<span id="3e859635"></span>
## Cautions


* When using the `COLUMNS` expression, ensure that the number and type of arguments passed to the function are supported by the function; otherwise, ByteHouse will return an error.

   For example, after executing the following command, the system displays the following error message:

   ```SQL
   SELECT COLUMNS('a') + COLUMNS('c') FROM sample.col_names
   ```
   

   ```SQL
   Code: 42, Error: DB::Exception: Number of arguments for function plus doesn't match: passed 3, should be 2 SQLSTATE: 42000
   ```
   

   In this example, `COLUMNS('a')` returns two columns: `aa` and `ab`. `COLUMNS('c')` returns `bc` column(s). The `+` operator cannot be applied to three arguments, so ByteHouse throws an exception with a relevant message.

   Expressions for the matched columns `COLUMNS` can have different data types.

* If `COLUMNS` does not match any columns and is the only expression in `SELECT`, ByteHouse will return an error.

* Usage scenarios for the asterisk symbol (\*):

   You can use an asterisk to replace an expression in any part of a query. During query analysis, the asterisk expands to all columns of all tables except for `MATERIALIZED` and `ALIAS` columns. It is recommended to use asterisks only in the following scenarios:

   * When creating a dump table.

   * When dealing with tables that have a small number of columns, such as operating system tables.

   * Obtain information about the columns in the table. In this case, set `LIMIT 1` **.**  However, it is recommended to use the `DESC TABLE` query.

   * When aggressive filtering is applied to a small number of columns using `PREWHERE`.

   * Use in subqueries, because columns not required by the outer query are excluded from the subquery.

   * Use in other scenarios is not recommended, as it may affect performance.


<span id="ca76013a"></span>
# With clause

Bytehouse supports common table expression (CTE). The result of a WITH clause can be used in subsequent SELECT queries. However, this functionality has certain limitations, including:


* Recursion is not allowed in CTE;

* Subqueries are not allowed in a CTE.


<span id="43ff17e0"></span>
## **Grammar**

```SQL
WITH [columnExpr] AS identifier
```


<span id="68cb04b0"></span>
## Parameter description


|**Parameters** |**Description** |
|---|---|
|columnExpr |Define the expression for the CTE (usually a subquery). Generate a temporary result set. |
|identifier |The name (alias) of the CTE, used to reference this result set in subsequent `SELECT`. |


<span id="bed1df10"></span>
## **Example 1: Use a constant expression as a "variable"** 

```SQL
WITH '2024-07-01 15:23:00' as ts_upper_bound
SELECT *
FROM system.tables
WHERE 
metadata_modification_time <= ts_upper_bound 
LIMIT 5;
```


<span id="30793f3a"></span>
## **Example 2: Remove the result of the sum(bytes) expression from the SELECT clause**

```SQL
WITH sum(total_bytes) as s
SELECT
    formatReadableSize(s),
    database
FROM system.tables
GROUP BY database
ORDER BY s 
LIMIT 3;
```


<span id="41b2ba80"></span>
## **Example 3: Use the result of a scalar subquery**

```SQL
/* The following example will return the 10 largest databases.  */
WITH
    (
        SELECT sum(total_bytes)
        FROM system.tables
    ) AS total_resoure_size
SELECT
    (sum(total_bytes) / total_resoure_size) * 100 AS db_resource_usage,
    database
FROM system.tables
GROUP BY database
ORDER BY db_resource_usage DESC
LIMIT 10 
```


<span id="6e161d6c"></span>
## **Example 4: Reuse expressions in subqueries**

```SQL
WITH ['hello'] AS hello
SELECT
    hello,
    *
FROM
(
    WITH ['hello'] AS hello
    SELECT hello
)

-- Results

┌─hello─────┬─hello_1─────┐
│ ['hello'] │ ['hello'] │
└───────────┴───────────┘
```


<span id="cc63352d"></span>
# FROM clause

The FROM clause specifies the source of the data and can be set to a table, a subquery, or a table function.

<span id="360c8f78"></span>
## **Grammar**


* Read data from the table

   ```SQL
   FROM [tableIdentifier] [FINAL] [sampleClause] 
   ```
   

* Read data from subqueries

   ```SQL
   FROM ([selectUnionStmt]) [FINAL] [sampleClause]
   ```
   

* Read data from table functions

   ```SQL
   FROM tableFunctionExpr [FINAL] [sampleClause]
   ```
   


<span id="3770335c"></span>
## Parameter description


|Parameters |Description |
|---|---|
|tableIdentifier |Specify the name of the table or view. |
|selectUnionStmt |Subquery statements must be enclosed in parentheses. |
|tableFunctionExpr |The table function expression |
|FINAL |When `FINAL` is specified, ByteHouse fully merges the data before returning results; therefore, it performs all data transformations that occur during the merge process. |
|sampleClause |Data sampling expression (for example, `SAMPLE 0.1` means 10% data sampling). |


<span id="6efe1025"></span>
## **Example 1:**  Query from a table

```SQL
-- 1. Create the required libraries
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a sample table
CREATE TABLE sample_db.fromClause ON CLUSTER sample_cluster (
  id UInt32, 
  val UInt32
) 
ENGINE=MergeTree() 
ORDER BY id;

-- 3. Insert data
INSERT INTO sample_db.fromClause 
VALUES 
  (1, 10), 
  (1, 11), 
  (1, 12), 
  (2, 20), 
  (2, 21);

-- 4. Query table data
SELECT * FROM sample_db.fromClause; 

-- Result examples
   ┌─id─┬─val─┐
1. │  1 │  10 │
2. │  1 │  11 │
3. │  1 │  12 │
4. │  2 │  20 │
5. │  2 │  21 │
   └────┴─────┘
```


<span id="d84e8e5e"></span>
## Example 2: Query using a subquery

```SQL
-- 1. Create the required libraries
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create an example table
CREATE TABLE sample_db.fromClause ON CLUSTER sample_cluster (
  id UInt32, 
  val UInt32
) 
ENGINE=MergeTree() 
ORDER BY id;

-- 3. Insert data
INSERT INTO sample_db.fromClause 
VALUES 
  (1, 10), 
  (1, 11), 
  (1, 12), 
  (2, 20), 
  (2, 21);

-- 4. Query the subquery data
SELECT * FROM (SELECT * FROM sample_db.fromClause LIMIT 3); 

-- Result examples
   ┌─id─┬─val─┐
1. │  1 │  10 │
2. │  1 │  11 │
3. │  1 │  12 │
   └────┴─────┘
```


<span id="4ed565c0"></span>
## Example 3: Query from a table function

Here, the table function numbers is used to generate a table containing 10 rows.

```SQL
-- 1. Create required libraries
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a sample table
CREATE TABLE sample_db.fromClause ON CLUSTER sample_cluster (
  id UInt32, 
  val UInt32
) 
ENGINE=MergeTree() 
ORDER BY id;

-- 3. Insert the data
INSERT INTO sample_db.fromClause 
VALUES 
  (1, 10), 
  (1, 11), 
  (1, 12), 
  (2, 20), 
  (2, 21);

-- 4. Query table function data
SELECT * FROM numbers(10); 

-- Result examples
    ┌─number─┐
 1. │      0 │
 2. │      1 │
 3. │      2 │
 4. │      3 │
 5. │      4 │
 6. │      5 │
 7. │      6 │
 8. │      7 │
 9. │      8 │
10. │      9 │
    └────────┘
```


<span id="1a06680e"></span>
# SAMPLE clause

<span id="47ea708b"></span>
## Prerequisites

If you want to use sampling, you must specify a sampling expression when creating a MergeTree table. For details, see [SAMPLE BY statement](https://clickhouse.com/docs/engines/table-engines/mergetree-family/mergetree#sample-by).

<span id="5f2764b0"></span>
## Function overview

The SAMPLE clause allows approximate SELECT query processing. When the sample clause is enabled, the query does not execute on all data, but only on a subset of the data. This is applicable in the following scenarios:


* When there are strict timing requirements (for example, less than 100 milliseconds), but the cost of expanding hardware resources is not feasible.

* The original data is inaccurate, so approximate results will not significantly lower the quality.

* Business requirements may allow accepting approximate results, such as in cost optimization scenarios, or provide precise results only for advanced users.


The following are data sampling features:


* Data sampling is a deterministic mechanism. Same `SELECT ... SAMPLE` query always returns the same result.

* If different tables use the same sampling key (such as user ID), sampling with the same coefficient will select the same subset of data. This also means that you can use IN and JOIN operations in subqueries.

* Sampling allows less data to be read from disk. Note: You must specify the sampling key correctly.


`SAMPLE` clause supports the following syntax:


|SAMPLE clause syntax |Description |
|---|---|
|SAMPLE k |Perform proportional sampling, where k represents the proportion of data to be sampled. Set k as a number from 0 to 1, supporting decimal values. For example, `SAMPLE 0.1` means querying 10% of the data. |
|SAMPLE n |Sample by row count, where n represents the minimum number of sampled rows and should be set to a sufficiently large integer.<br><br>This query is executed on at least one sample for up to n rows. For example, `SAMPLE 10000000` indicates that the query is run on at least 10,000,000 rows. |
|SAMPLE k OFFSET m |Proportional sampling with offset, where k is the sampling ratio and m is the offset ratio. Both are set to values from 0 to 1. For example, `SAMPLE 0.2 OFFSET 0.3` indicates that a 20% data interval is selected starting from the 30% position. |


<span id="b6eb7519"></span>
## SAMPLE K

`k` is set to a number from 0 to 1; both decimals and decimal notation are supported. For example, `SAMPLE 1/2` or `SAMPLE 0.5`.

<span id="fcfe4ec7"></span>
### **Grammar**

```SQL
SAMPLE K
```


<span id="ff409deb"></span>
### **Example**

In this example, an approximate calculation will be performed using 10% of the data.

```SQL
-- 1. Create the required libraries
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a sample table
CREATE TABLE IF NOT EXISTS sample_db.sampleClause ON CLUSTER sample_cluster (
  id UInt32
) 
ENGINE=MergeTree 
ORDER BY id 
SAMPLE BY id;

-- 3. Insert data
INSERT INTO sample_db.sampleClause 
SELECT * FROM numbers(1000);

-- 4. Data sampling
SELECT COUNT() * 10 
FROM sample_db.sampleClause 
SAMPLE 0.1; -- Query 10% of the data
```


<span id="e4a5ce0f"></span>
## SAMPLE N

`n` is set to a sufficiently large integer. , for example, `SAMPLE 10000000`.

In this case, for at least one sample, the query executes `n` rows (but does not exceed that value). For example, `SAMPLE 10000000` indicates that the query is run on at least 10,000,000 rows.

<span id="0c51a48a"></span>
### **Grammar**

```SQL
SAMPLE N
```


<span id="2476dfc7"></span>
### **Example**

In this example, two rows of data will be used for approximate calculation.

```SQL
-- 1. Create the required libraries
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create an example table
CREATE TABLE IF NOT EXISTS sample_db.sampleClause ON CLUSTER sample_cluster (
  id UInt32
) 
ENGINE=MergeTree 
ORDER BY id 
SAMPLE BY id;

-- 3. Insert data
INSERT INTO sample_db.sampleClause 
SELECT * FROM numbers(1000);

-- 4. Data sampling
SELECT COUNT() FROM sample_db.sampleClause SAMPLE 2; 
```


<span id="1d9f5cbe"></span>
## SAMPLE K OFFSET M

`k` is the sampling ratio, `m` is the offset ratio, and both are set to values between 0 and 1. For example, `SAMPLE 0.2 OFFSET 0.3` indicates that a 20% data range is selected starting from the 30% position.

<span id="2f515db6"></span>
### **Grammar**

```SQL
SAMPLE K OFFSET M
```


<span id="4cd9d1b9"></span>
### **Example**

In this example, after skipping 20% of the data, 10% of the data will be used for approximate calculation.

```SQL
-- 1. Create required libraries
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a sample table
CREATE TABLE IF NOT EXISTS sample_db.sampleClause ON CLUSTER sample_cluster (
  id UInt32
) 
ENGINE=MergeTree 
ORDER BY id 
SAMPLE BY id;

-- 3. Insert data
INSERT INTO sample_db.sampleClause 
SELECT * FROM numbers(1000);

-- 4. Data sampling
SELECT COUNT() 
FROM sample_db.sampleClause 
SAMPLE 0.1 OFFSET 0.2;
```


<span id="707d91fb"></span>
# JOIN clause

The JOIN clause combines columns from one or more tables to create a new table by using values that are common to each table.

<span id="bb816325"></span>
## **Grammar**

```SQL
[ANY|ALL|ASOF] [INNER|LEFT|RIGHT|FULL|CROSS] [OUTER] JOIN [tableIdentifier] ON|USING [columnExprList]
```


<span id="22555bee"></span>
## Parameter description


|Parameters |Description |
|---|---|
|ANY |If there are multiple matching rows in the right table, only the first matching row will be joined. If there is only one matching row in the right table, the results of ANY and ALL are the same. |
|ALL |If there are multiple matching rows in the right table, ByteHouse creates a Cartesian product from the matched rows. This is the normal JOIN behavior in standard SQL. |
|ASOF |Used for connecting sequences with uncertain matches. |
|INNER JOIN |Only return matching rows. |
|LEFT OUTER JOIN |In addition to returning matching rows, it also returns non\-matching rows from the left table. |
|RIGHT OUTER JOIN |In addition to returning matching rows, it also returns non\-matching rows from the right table. |
|FULL OUTER JOIN |In addition to returning matching rows, it also returns rows from both tables that do not match. |
|CROSS JOIN |Generate the Cartesian product of the entire table without specifying a "join key". |
|ON |USING<br><br><br>* ON: Define join conditions using expressions.<br><br>* USING: Define join conditions by shared column names. |


<span id="aedd3916"></span>
## **Example**

```SQL
-- 1. Create the required libraries
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a sample table
CREATE TABLE IF NOT EXISTS sample_db.joinClause ON CLUSTER sample_cluster (
  number UInt64
) 
ENGINE=MergeTree 
ORDER BY number;

-- 3. Insert data
INSERT INTO sample_db.joinClause SELECT * 
FROM numbers(10);

-- 4. Use the JOIN clause to query
SELECT 
  number, 
  joined 
FROM sample_db.joinClause 
ANY LEFT JOIN 
(
    SELECT 
        number * 2 AS number, 
        number * 10 + 1 AS joined 
    FROM sample_db.joinClause 
    LIMIT 10
) js2 USING number 
LIMIT 10

-- Result examples
┌─number─┬─joined─┐
│      0 │      1 │
│      1 │   NULL │
│      2 │     21 │
│      3 │   NULL │
│      4 │     41 │
│      5 │   NULL │
│      6 │     61 │
│      7 │   NULL │
│      8 │     81 │
│      9 │   NULL │
└────────┴────────┘
```


<span id="62a39882"></span>
# ARRAY JOIN clause

For tables that contain array columns, an array join generates a new table whose columns contain each individual array element from the original column, while the values of the other columns are duplicated.

<span id="6c29497c"></span>
## **Grammar**

Only one arrayJoin clause can be specified in each `SELECT` query.

```SQL
[LEFT] ARRAY JOIN [columnExprList] 
```


<span id="abdb9c7a"></span>
## Parameter description


|Parameters |Description |
|---|---|
|ARRAY JOIN |Only non\-empty arrays are expanded; rows containing empty arrays are not displayed in the result. |
|LEFT ARRAY JOIN |`JOIN` result contains rows with empty arrays. Expanding an empty array yields the default value for the array element type, which is typically 0, an empty string, or NULL. |


<span id="fb9c1cf2"></span>
## **Example**

```SQL
-- 1. Create required libraries
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a sample table
CREATE TABLE sample_db.arrayJoinClause ON CLUSTER sample_cluster (
  s String, 
  arr Array(UInt8)
) 
ENGINE = MergeTree 
ORDER BY s;

-- 3. Insert data
INSERT INTO sample_db.arrayJoinClause VALUES 
  ('Hello', [1,2]), 
  ('World', [3,4,5]), 
  ('Goodbye', []);
  
-- 4. Query data
SELECT s, arr FROM sample_db.arrayJoinClause ARRAY JOIN arr;

-- Output result examples
   ┌─s─────┬─arr─┐
   │ Hello │   1 │
   │ Hello │   2 │
   │ World │   3 │
   │ World │   4 │
   │ World │   5 │
   └───────┴─────┘
```


<span id="61f11047"></span>
# PREWHERE clause

The Prewhere clause is an optimization mechanism used to apply filtering more efficiently. Even if the PREWHERE clause is not explicitly specified, the system will automatically move part of the WHERE conditions to the prewhere stage for execution. The only purpose of the PREWHERE clause is to control this optimization when you believe you can achieve better results than the default optimization.

When optimizing with prewhere, the specific process is as follows:


1. First, only the columns required for executing the prewhere expression are read.

2. Then, read the additional columns required to execute the rest of the query, but only from those data blocks where the prewhere expression is "true" in some rows.

   If there are a large number of data blocks in which the prewhere expression evaluates to "false" for all rows, and the number of columns required by prewhere is less than that required by other parts of the query, this optimization can significantly reduce disk IO overhead.


<span id="c8039280"></span>
## **Grammar**

```SQL
PREWHERE [columnExpr](http://columnexpr/)
```


<span id="49a10a5b"></span>
## **Example**

```SQL
-- 1. Create a table
CREATE TABLE sample.prewhereClause(id UInt32, val UInt32) ENGINE = MergeTree() ORDER BY id;

-- 2. Insert data
INSERT INTO sample.prewhereClause VALUES (1, 10), (1, 11), (1, 12), (2, 20), (2, 21);

-- 3. Execute prewhere query
SELECT * FROM sample.prewhereClause PREWHERE id=1 WHERE val>10; -- (1, 11), (1, 12) expected
```


<span id="80da296b"></span>
# Where clause

The WHERE clause is used to filter the data obtained from the `FROM` clause in the `SELECT` statement. If the query contains a WHERE clause, the clause must include an expression that returns a `UInt8` value, which is typically an expression involving comparison and logical operators. Rows for which the expression evaluates to 0 will be excluded and will not participate in subsequent data transformation or result set return.

When supported by the underlying table engine, filtering conditions in the WHERE clause will use indexes and partitioning mechanisms to perform data pruning optimization, thereby reducing the amount of data that actually needs to be processed.

<span id="4bb1ffe4"></span>
## **Grammar**

```SQL
WHERE [columnExpr]
```


<span id="2819147a"></span>
## **Example**

```SQL
-- 1. Create the required libraries
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a sample table
CREATE TABLE sample_db.whereClause ON CLUSTER sample_cluster (
  id UInt32, 
  val UInt32
) 
ENGINE = MergeTree() 
ORDER BY id;

-- 3. Insert data
INSERT INTO sample_db.whereClause 
VALUES 
  (1, 10), 
  (1, 11), 
  (1, 12), 
  (2, 20), 
  (2, 21);

-- 4. Execute a where query
SELECT * FROM sample_db.whereClause 
WHERE val>10; -- (1, 11), (1, 12), (2, 20), (2, 21) expected

-- Example output
   ┌─id─┬─val─┐
   │  1 │  11 │
   │  1 │  12 │
   │  2 │  20 │
   │  2 │  21 │
   └────┴─────┘
```


To determine whether a value is NULL, use the `IS NULL` and `IS NOT NULL` operators or the `isNull` and `isNotNull` functions. Because ordinary conditional expressions containing NULL usually do not return the expected result.

**Example**

```SQL
-- 1. Create a test table t_null
CREATE TABLE sample_db.t_null ON CLUSTER sample_cluster (
  x Int8, 
  y Nullable(Int8)
) 
ENGINE=MergeTree() 
ORDER BY x;

-- 2. Insert data
INSERT INTO sample_db.t_null VALUES (1, NULL), (2, 3);

-- 3. Query records where the y field is NULL
SELECT * FROM sample_db.t_null WHERE y IS NULL;
An output result example
   ┌─x─┬────y─┐
   │ 1 │ ᴺᵁᴸᴸ │
   └───┴──────┘

-- 4. Query records where the y field is not 0
SELECT * FROM sample_db.t_null WHERE y != 0;
Example of output result
   ┌─x─┬─y─┐
   │ 2 │ 3 │
   └───┴───┘
```


<span id="44aa2d96"></span>
# GROUP BY clause

The `GROUP BY` clause is used to group and aggregate the results of a `SELECT` query. When `[columnExprList]` is used as the grouping key, the number of rows in the aggregation result matches the number of unique values of the grouping key in the source table, with each unique grouping key corresponding to one row in the aggregation result.

<span id="7e2b3c9a"></span>
## **Grammar**

```SQL
GROUP BY [(][columnExprList][)] [WITH ROLLUP|WITH CUBE] [WITH TOTALS] 
```



* `NULL processing`: ByteHouse treats `NULL` as a valid grouping value. If the grouping key contains NULL values, they will appear in the result.

* `WITH ROLLUP`: Generates subtotals based on the order of key expressions in the `GROUP BY` list.

   * Subtotal rows will be added to the result table afterwards.

   * In subtotal rows, the values of key expressions that have been grouped are set to 0 or to an empty row.

* `WITH CUBE`: Calculates subtotals for every combination of key expressions in the `GROUP BY` list.

* `WITH TOTALS`: Calculates subtotals for all key expression combinations in the `GROUP BY` list.


<span id="a339ac9c"></span>
## **Example 1: Group by key with NULL values**

```SQL
-- 1. Create an example table
CREATE TABLE IF NOT EXISTS sample_db.groupByClause ON CLUSTER sample_cluster (
  x UInt32, 
  y Nullable(UInt32)
) 
ENGINE=MergeTree ORDER BY x;

-- 2. Insert test data
INSERT INTO sample_db.groupByClause 
VALUES 
  (1,2),
  (2,NULL),
  (3,2),
  (3,3),
  (3,NULL);

-- 3. Execute a query
SELECT sum(x), y FROM sample_db.groupByClause GROUP BY y; 

-- Example of output results
   ┌─sum(x)─┬────y─┐
   │      5 │ ᴺᵁᴸᴸ │
   │      3 │    3 │
   │      4 │    2 │
   └────────┴──────┘
```


<span id="47dbe249"></span>
## **Example 2: WITH ROLLUP modifier for grouped aggregation**

```SQL
-- 1. Create an example table
CREATE TABLE IF NOT EXISTS sample_db.groupByClause1 ON CLUSTER sample_cluster (
  year UInt32, 
  month UInt32, 
  day UInt32
) 
ENGINE=MergeTree 
ORDER BY year;

-- 2. Insert test data
INSERT INTO sample_db.groupByClause1 
VALUES 
  (2019,1,5),
  (2019,1,15),
  (2020,1,5),
  (2020,1,15),
  (2021,1,5),
  (2021,1,15);
  
-- 3. Query data
SELECT year, month, day, count() 
FROM sample_db.groupByClause1 
GROUP BY year, month, day WITH ROLLUP;
```


Because the GROUP BY section contains three key expressions, the result includes subtotal tables aggregated from right to left:


* GROUP BY year, month, day；

* GROUP BY year, month (with the day column set to zero);

* GROUP BY year (currently, the month and day columns are filled with zeros);

* Total (all three key expression columns are zero).


Returned results:

```SQL
    ┌─year─┬─month─┬─day─┬─count()─┐
    │ 2020 │     1 │   5 │       1 │
    │ 2019 │     1 │   5 │       1 │
    │ 2021 │     1 │  15 │       1 │
    │ 2019 │     1 │  15 │       1 │
    │ 2020 │     1 │  15 │       1 │
    │ 2021 │     1 │   5 │       1 │
    │ 2020 │     1 │   0 │       2 │
    │ 2019 │     1 │   0 │       2 │
    │ 2021 │     1 │   0 │       2 │
    │ 2019 │     0 │   0 │       2 │
    │ 2021 │     0 │   0 │       2 │
    │ 2020 │     0 │   0 │       2 │
    │    0 │     0 │   0 │       6 │
    └──────┴───────┴─────┴─────────┘
```


<span id="81a95a61"></span>
## **Example 3: The WITH CUBE modifier for grouped aggregation**

```SQL
-- 1. Create an example table
CREATE TABLE IF NOT EXISTS sample_db.groupByClause2 ON CLUSTER sample_cluster (
  year UInt32, 
  month UInt32, 
  day UInt32
) 
ENGINE=MergeTree 
ORDER BY year;

-- 2. Insert test data
INSERT INTO sample_db.groupByClause2 
VALUES 
  (2019,1,5),
  (2019,1,15),
  (2020,1,5),
  (2020,1,15),
  (2021,1,5),
  (2021,1,15);
  
-- 3. Query data
SELECT year, month, day, count() 
FROM sample_db.groupByClause2 
GROUP BY year, month, day WITH CUBE;
```


Because the GROUP BY clause contains three key expressions, the result includes eight subtotal tables, covering the subtotals for all combinations of the key expressions:


* GROUP BY year, month, day

* GROUP BY year, month

* GROUP BY year, day

* GROUP BY year

* GROUP BY month, day

* GROUP BY month

* GROUP BY day

* Total (all three key expression columns are zero)


Results:

```SQL
    ┌─year─┬─month─┬─day─┬─count()─┐
    │ 2020 │     1 │   5 │       1 │
    │ 2019 │     1 │   5 │       1 │
    │ 2021 │     1 │  15 │       1 │
    │ 2019 │     1 │  15 │       1 │
    │ 2020 │     1 │  15 │       1 │
    │ 2021 │     1 │   5 │       1 │
    │ 2020 │     1 │   0 │       2 │
    │ 2019 │     1 │   0 │       2 │
    │ 2021 │     1 │   0 │       2 │
    │ 2020 │     0 │  15 │       1 │
    │ 2019 │     0 │   5 │       1 │
    │ 2019 │     0 │  15 │       1 │
    │ 2020 │     0 │   5 │       1 │
    │ 2021 │     0 │   5 │       1 │
    │ 2021 │     0 │  15 │       1 │
    │ 2019 │     0 │   0 │       2 │
    │ 2021 │     0 │   0 │       2 │
    │ 2020 │     0 │   0 │       2 │
    │    0 │     1 │   5 │       3 │
    │    0 │     1 │  15 │       3 │
    │    0 │     1 │   0 │       6 │
    │    0 │     0 │   5 │       3 │
    │    0 │     0 │  15 │       3 │
    │    0 │     0 │   0 │       6 │
    └──────┴───────┴─────┴─────────┘
```


<span id="b843ada2"></span>
## **Example 4: WITH TOTAL modifier for grouped summary**

```SQL
-- 1. Create a sample table
CREATE TABLE IF NOT EXISTS sample_db.groupByClause3 ON CLUSTER sample_cluster (
  year UInt32, 
  month UInt32, 
  day UInt32
) 
ENGINE=MergeTree 
ORDER BY year;

-- 2. Insert test data
INSERT INTO sample_db.groupByClause3 
VALUES 
  (2019,1,5),
  (2019,1,15),
  (2020,1,5),
  (2020,1,15),
  (2021,1,5),
  (2021,1,15);

-- 3. Query data
SELECT year, month, day, count()
FROM sample_db.groupByClause3
GROUP BY year, month, day WITH TOTALS;
```


If the WITH TOTALS modifier is specified, an additional row will be calculated.


* GROUP BY year, month, day

* Total (all three key expression columns are zero)


Returned results:

```SQL
   ┌─year─┬─month─┬─day─┬─count()─┐
   │ 2020 │     1 │   5 │       1 │
   │ 2019 │     1 │   5 │       1 │
   │ 2021 │     1 │  15 │       1 │
   │ 2019 │     1 │  15 │       1 │
   │ 2020 │     1 │  15 │       1 │
   │ 2021 │     1 │   5 │       1 │
   └──────┴───────┴─────┴─────────┘

Totals:
   ┌─year─┬─month─┬─day─┬─count()─┐
   │    0 │     0 │   0 │       6 │
   └──────┴───────┴─────┴─────────┘
```


<span id="310c7dee"></span>
# LIMIT BY clause

For each distinct value in the list expression, select the first m rows of results.

<span id="c4d2632a"></span>
## **Grammar**

```SQL
LIMIT m BY [columnExprList]
```


<span id="bd5fe831"></span>
## **Example: Limit m rows by list expression**

In this example, for each id, including values 1 and 2, we need to return two rows.

```SQL
-- 1. Create a test table
CREATE TABLE sample_db.limitByClause ON CLUSTER sample_cluster (
  id UInt32, 
  val UInt32
) 
ENGINE = MergeTree() 
ORDER BY id;

-- 2. Insert data
INSERT INTO sample_db.limitByClause 
VALUES 
  (1, 10), 
  (1, 11), 
  (1, 12), 
  (2, 20), 
  (2, 21);

-- 3. Return the first 2 rows for each id
SELECT * FROM sample_db.limitByClause 
ORDER BY id, val LIMIT 2 BY id; 

-- Output results
   ┌─id─┬─val─┐
   │  1 │  10 │
   │  1 │  11 │
   │  2 │  20 │
   │  2 │  21 │
   └────┴─────┘
```


<span id="8c0e0b9e"></span>
# HAVING clause

Filters aggregate results generated by the `groupBy` clause, similar to the `WHERE` clause, but the difference is that the `WHERE` clause is executed before aggregation, while the `HAVING` clause is executed after aggregation.

<span id="f2a67350"></span>
## **Grammar**

```SQL
HAVING [columnExpr](http://columnexpr/) 
```


<span id="dbe426a1"></span>
## **Example**

```SQL
-- 1. Create a test table
CREATE TABLE sample_db.havingClause ON CLUSTER sample_cluster (
  id UInt32, 
  val UInt32
) 
ENGINE = MergeTree() 
ORDER BY id;

-- 2. Insert data
INSERT INTO sample_db.havingClause 
VALUES 
  (1, 10), 
  (1, 11), 
  (1, 12), 
  (2, 20), 
  (2, 21);

-- 3. Filter results
SELECT id FROM sample_db.havingClause 
GROUP BY id HAVING count(id)>2; 

-- Output results
   ┌─id─┐
   │  1 │
   └────┘
```


<span id="1ccac90d"></span>
# DISTINCT clause

`SELECT DISTINCT` is used to filter duplicate rows from query results, ensuring that only one row is retained for rows in which all column values are identical.

**Empty processing**

In `DISTINCT` logic, `NULL` is treated as a specific value, and `NULL == NULL` holds. This means:


* Rows with a `NULL` value in the same position are considered duplicates; only one row is retained;

* This handling method differs from the logic of `NULL` in most SQL scenarios, for example, `NULL = NULL` returns UNKNOWN.


**Alternative solution**

By specifying all `SELECT` columns (without using aggregate functions) in `GROUP BY`, you can achieve the same deduplication effect as the `DISTINCT` clause. The differences between the two are as follows:


* `DISTINCT` can be used together with `GROUP BY`.

* When `ORDER BY` is omitted and `LIMIT` is specified, the system terminates immediately upon retrieving the required number of unique rows.

* Data blocks are output in processing order without waiting for all data to be processed.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If a <code>SELECT</code> statement contains array\-type columns, the <code>DISTINCT</code> clause does not support direct duplicate removal.</div>


<span id="5b1ccccf"></span>
## **Example**

ByteHouse supports using `DISTINCT` and `ORDER BY` to query different columns within the same query. The `DISTINCT` clause is executed before the `ORDER BY` clause, meaning that deduplication occurs prior to sorting.

The example performs two queries based on the following table to demonstrate the execution order logic.

```Plain
┌─a─┬─b─┐
│ 2 │ 1 │
│ 1 │ 2 │
│ 3 │ 3 │
│ 2 │ 4 │
└─┴───┘
```



* Query 1:

   When executing the `SELECT DISTINCT a FROM t1 ORDER BY b ASC` query, the logic is as follows: first, remove duplicates from column a (resulting in {1, 2, 3}), then sort the resulting rows by column b in ascending order.

   ```SQL
   -- 1. Create a test table
   CREATE TABLE IF NOT EXISTS sample_db.distinctClause ON CLUSTER sample_cluster (
       a UInt32,
       b UInt32
   ) 
   ENGINE = MergeTree 
   ORDER BY a;
   
   -- 2. Insert test data
   INSERT INTO sample_db.distinctClause 
   VALUES 
     (2, 1), 
     (1, 2), 
     (3, 3), 
     (2, 4);
     
   -- 3. Query
   SELECT DISTINCT a FROM sample_db.distinctClause ORDER BY b ASC
   ```
   

   The results are as follows:

   ```Plain
      ┌─a─┐
      │ 2 │
      │ 1 │
      │ 3 │
      └───┘
   ```
   

* Query 2:

   Change the sort order `SELECT DISTINCT a FROM t1 ORDER BY b DESC`. When you execute the query again, the logic is: after removing duplicates, sort by b in descending order.

   ```SQL
   -- 1. Create a test table
   CREATE TABLE IF NOT EXISTS sample_db.distinctClause ON CLUSTER sample_cluster (
       a UInt32,
       b UInt32
   ) 
   ENGINE = MergeTree 
   ORDER BY a;
   
   -- 2. Insert test data
   INSERT INTO sample_db.distinctClause 
   VALUES 
     (2, 1), 
     (1, 2), 
     (3, 3), 
     (2, 4);
     
   -- 3. Query data
   SELECT DISTINCT a FROM sample_db.distinctClause ORDER BY b DESC
   ```
   

   The results are as follows:

   ```Plain
      ┌─a─┐
      │ 3 │
      │ 1 │
      │ 2 │
      └───┘
   ```
   

   As shown by the returned results, `DISTINCT` performs deduplication first, followed by sorting with `ORDER BY`. Therefore, sorting does not affect the deduplication result, but it does affect the final output order.


<span id="5965dfaf"></span>
# LIMIT clause

`LIMIT` clause is used to restrict the number of rows returned by a query.

<span id="ee5b0238"></span>
## **Grammar**

```SQL
LIMIT m -- Return the first m rows
LIMIT n, m -- Skip the first n rows, return the following m rows
LIMIT m OFFSET n -- Equivalent to LIMIT n, m
LIMIT ... WITH TIES -- Return all parallel rows
```



* `LIMIT m`: Returns the first `m` rows.

* `LIMIT n, m` or `LIMIT m OFFSET n`: Skip the first n rows and return m rows. `n` and `m` must be non\-negative integers.

* `WITH TIES` description: If the last row shares the same sort value with other rows, all tied rows are returned.

* If there is no ORDER BY clause to explicitly sort the results, the selection of rows in the result may be arbitrary and non\-deterministic.


<span id="43e1106b"></span>
## **Example 1: LIMIT m**

```SQL
-- 1. Create a test table
CREATE TABLE IF NOT EXISTS sample_db.limitClause ON CLUSTER sample_cluster (
  id UInt32
) 
ENGINE=MergeTree()
ORDER BY id;

-- 2. Insert test data
INSERT INTO sample_db.limitClause 
VALUES 
  (1),
  (2),
  (3),
  (4),
  (5);
 
-- 3. Query the first two rows of data
SELECT * FROM sample_db.limitClause LIMIT 2;

-- Output results
   ┌─id─┐
   │  1 │
   │  2 │
   └────┘
```


<span id="2c33d50f"></span>
## **Example 2: LIMIT n, m**

```SQL
-- 1. Create a test table
CREATE TABLE IF NOT EXISTS sample.limitClause ON CLUSTER sample_cluster (
  id UInt32
) 
ENGINE=MergeTree() 
OEDER BY id;

-- 2. Insert test data
INSERT INTO sample.limitClause 
VALUES 
  (1),
  (2),
  (3),
  (4),
  (5);

-- 3. Skip the first n rows and return the following m rows when querying
SELECT * FROM sample_db.limitClause LIMIT 1,2; 
The query methods are different, but the query results are the same
SELECT * FROM sample_db.limitClause LIMIT 2 OFFSET 1; 

-- Output results
   ┌─id─┐
   │  2 │
   │  3 │
   └────┘
```


<span id="5b451841"></span>
## **Example 3: LIMIT WITH TIES**

```SQL
-- 1. Create a test table
CREATE TABLE IF NOT EXISTS sample.limitClause ON CLUSTER sample_cluster (
  id UInt32
) 
ENGINE=MergeTree() 
OEDER BY id;

-- 2. Insert test data
INSERT INTO sample.limitClause 
VALUES 
  (1),
  (2),
  (3),
  (4),
  (5);

-- 3. Return all parallel rows
SELECT * FROM (
    SELECT number%50 AS n FROM numbers(100)
) ORDER BY n LIMIT 0,5 WITH TIES

-- Output results
   ┌─n─┐
   │ 0 │
   │ 0 │
   │ 1 │
   │ 1 │
   │ 2 │
   │ 2 │
   └───┘
```


<span id="d4a2a923"></span>
# UNION ALL clause

`UNION ALL` is used to combine the result sets of multiple `SELECT` statements by appending their rows and returning the combined result set.

<span id="8ae2a309"></span>
## **Grammar**

```SQL
UNION ALL ... 
```


<span id="21bafa6c"></span>
## **Example**

```SQL
-- 1. Create a test table
CREATE TABLE IF NOT EXISTS sample_db.unionClause1 ON CLUSTER sample_cluster (
    CounterID UInt32,
    c UInt64
) 
ENGINE = MergeTree 
ORDER BY CounterID;

CREATE TABLE IF NOT EXISTS sample_db.unionClause2 ON CLUSTER sample_cluster (
    CounterID UInt32,
    c UInt64
) 
ENGINE = MergeTree 
ORDER BY CounterID;

-- 2. Insert test data
INSERT INTO sample_db.unionClause1 VALUES (1, 100), (2, 200);
INSERT INTO sample_db.unionClause2 VALUES (1, 300), (3, 400);

-- 3. Merge query results
SELECT CounterID, 1 AS source, c 
  FROM sample_db.unionClause1
UNION ALL
SELECT CounterID, 2 AS source, c 
  FROM sample_db.unionClause2;
  
-- Output results
   ┌─CounterID─┬─source─┬───c─┐
   │         1 │      2 │ 300 │
   │         3 │      2 │ 400 │
   │         1 │      1 │ 100 │
   │         2 │      1 │ 200 │
   └───────────┴────────┴─────┘
```


Result set handling rules:


1. Column matching mechanism: Result columns from each query are matched in the order of their column indexes, rather than by column name. The column names in the final result are taken from the first query.

2. Handling types:

   * Automatically perform type conversion.

   * If the merged fields contain both `Nullable` and a compatible non\-`Nullable` type, all types are uniformly promoted to `Nullable`.


`ORDER BY`/`LIMIT` only applies to **a single query** (not the final result). When processing the final result, place the entire `UNION ALL` in a subquery, as shown below:

```SQL
SELECT * FROM ( ... UNION ALL ... ) ORDER BY col
```


ByteHouse only supports `UNION ALL` and does not support `UNION DISTINCT`. To use `UNION DISTINCT`, you can use `SELECT DISTINCT` in a subquery that contains `UNION ALL`. For example:

```SQL
SELECT DISTINCT * FROM ( ... UNION ALL ... )
```


<span id="21272f72"></span>
# SETTINGS clause

Use the `SETTINGS` clause to configure database parameters, overriding the default settings.

<span id="da2b8e53"></span>
## **Grammar**

```SQL
SETTINGS [settingExprList] 
```


<span id="2d2e17af"></span>
## Example

```SQL
-- 1. Create the required libraries
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a sample table
CREATE TABLE sample_db.fromClause ON CLUSTER sample_cluster (
  id UInt32, 
  val UInt32
) 
ENGINE=MergeTree() 
ORDER BY id;

-- 3. Insert data
INSERT INTO sample_db.fromClause 
VALUES 
  (1, 10), 
  (1, 11), 
  (1, 12), 
  (2, 20), 
  (2, 21);

-- 4. Query data and adjust parallelism
SELECT * FROM sample_db.fromClause
SETTINGS max_threads = 4;
```


<span id="651f19e9"></span>
# INTO OUTFILE clause

Use the `INTO OUTFILE` clause to output query results directly to a local file on the client.

This feature is only supported in the command\-line client and the clickhouse\-local tool; therefore, queries sent through the HTTP interface will fail. If the target file already exists, the query will fail.

The default output format is `TabSeparated` (consistent with command\-line batch mode).

<span id="ebc5b759"></span>
## **Grammar**

```SQL
INTO OUTFILE filename
```


<span id="a0062b42"></span>
## **Example**

```SQL
-- 1. Create required libraries
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create an example table
CREATE TABLE IF NOT EXISTS sample_db.col_names ON CLUSTER sample_cluster (
  aa Int8, 
  ab Int8, 
  bc Int8
) 
ENGINE = MergeTree 
ORDER BY aa;

-- 3. Insert test data
INSERT INTO sample_db.col_names 
VALUES 
  (1, 2, 3),(4, 5, 6);

-- 4. Export data to a local file; when using, replace the placeholder path with the actual storage path
SELECT * 
FROM sample_db.col_names 
INTO OUTFILE '~/sampel_outfile.txt' 
```


<span id="6c2f3276"></span>
# FORMAT clause

ByteHouse supports serialization formats, which can be used for query results. There are several ways to format the output of `SELECT`. One approach is to specify `FORMAT`[format](https://docs.byteplus.com/en/docs/bytehouse/input-output-formats) at the end of the query to obtain the result set in a specific format.

<span id="ad213846"></span>
## **Grammar**

```SQL
FORMAT format 
```


<span id="c6dfc79f"></span>
## Example

```SQL
-- 1. Create required libraries
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a sample table
CREATE TABLE IF NOT EXISTS sample_db.col_names ON CLUSTER sample_cluster (
  aa Int8, 
  ab Int8, 
  bc Int8
) 
ENGINE = MergeTree 
ORDER BY aa;

-- 3. Insert test data
INSERT INTO sample_db.col_names 
VALUES 
  (1, 2, 3),(4, 5, 6);
  
-- 4. Query data and define output format
SELECT * 
FROM sample_db.col_names 
FORMAT CSVWithNames;

-- Output results
aa        ab        bc
1        2        3
4        5        6
```
