---
title: "Query Statement (SELECT)"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/select-statement"
---

`SELECT` retrieves data upon execution. By default, the requested data is returned to the client, and can also be forwarded to different tables using `INSERT INTO`.

<span id="dd6dd36a"></span>
### Overall syntax

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


All clauses are optional, except for the required expression list immediately following **`SELECT`**.

<span id="911be613"></span>
### SELECT clause

```SQL
SELECT [DISTINCT] expr_list
```


DISTINCT, retains only unique rows in the query results. It treats NULL as a specific value, and considers NULL == NULL.

The asterisk symbol (\*), an asterisk can be placed anywhere in the query to replace expressions. When analyzing the query, the asterisk expands to a list of all table columns (excluding MATERIALIZED and ALIAS columns).

You can use synonyms in any part of the query as an `AS` alias.

<span id="dcbc91c5"></span>
#### **Use cases**


* To include all columns in the result, use the asterisk (`*`) symbol. For example, `SELECT * FROM ...`.

* To include columns containing 'a' in the results, you can use the `COLUMNS` expression.


**Example:** 

```SQL
CREATE TABLE sample.col_names (aa Int8, ab Int8, bc Int8) ENGINE = CnchMergeTree order by aa;
```


The following queries for all column names containing **`a`**.

```SQL
SELECT COLUMNS('a') FROM sample.col_names
```


```Plain
┌─aa─┬─ab─┐
│  1 │  1 │
└────┴────┘
```



* Use multiple **`COLUMNS`** expressions and apply functions to them.


**Example**

```SQL
SELECT COLUMNS('a'), COLUMNS('c'), toTypeName(COLUMNS('c')) FROM sample.col_names
```


```Plain
┌─aa─┬─ab─┬─bc─┬─toTypeName(bc)─┐
│  1 │  1 │  1 │ Int8           │
└────┴────┴────┴────────────────┘
```


Each returned column's **`COLUMNS`** expression is passed as a separate argument to the function. If the function supports additional arguments, you can also pass other arguments to the function.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Be cautious when using functions, as ByteHouse will throw an exception if the function does not support the parameters passed to it.</div>


For example:

```SQL
SELECT COLUMNS('a') + COLUMNS('c') FROM sample.col_names
```


```SQL
Code: 42, Error: DB::Exception: Number of arguments for function plus doesn't match: passed 3, should be 2 SQLSTATE: 42000
```


In this example, **`COLUMNS('a')`**  returns two columns: **`aa`** and **`ab`**. **`COLUMNS('c')`**  returns the **`bc`** column. The  **`+`**  operator cannot be applied to three arguments, thus ByteHouse throws an exception with a related message.

The matching column expressions for **`COLUMNS`** can have different data types. If **`COLUMNS`** doesn't match any columns and is the only expression in **`SELECT`**, ClickHouse will throw an exception.

<span id="11dbfc6f"></span>
#### Asterisk

You can use an asterisk as a replacement expression in any part of the query. During query analysis, the asterisk will expand to include all table columns (excluding **`MATERIALIZED`** and **`ALIAS`** columns). Using asterisks is only justifiable in a few cases:


* When creating dump tables.

* For tables that contain only a few columns, such as system tables.

* When retrieving information about columns in a table. In such cases, set **`LIMIT 1`**. However, it is better to use **`DESC TABLE`** query.

* When using **`PREWHERE`** for strong filtering on a small number of columns.

* In subqueries (because columns not needed by the outer query are excluded from the subquery).


In all other cases, using asterisks is not recommended, as it only highlights the shortcomings of a columnar DBMS, not its advantages. In other words, **using asterisks is not recommended**.

<span id="adeba35f"></span>
#### Implementation details

If the query omits `DISTINCT`, `GROUP BY`, `ORDER BY`, `IN`, `JOIN` subqueries, the query will be fully stream\-processed using O(1) amount of RAM. If appropriate limitations are not specified, the query may consume a large amount of RAM:


* `max_memory_usage`

* `max_rows_to_group_by`

* `max_rows_to_sort`

* `max_rows_in_distinct`

* `max_bytes_in_distinct`

* `max_rows_in_set`

* `max_bytes_in_set`

* `max_rows_in_join`

* `max_bytes_in_join`

* `max_bytes_before_external_sort`

* `max_bytes_before_external_group_by`


<span id="3a15f208"></span>
### WITH clause

This section provides support for Common Table Expressions (CTE), so the result `WITH` clause can be used in the rest of the `SELECT` query.

Bytehouse supports Common Table Expressions (CTE). The result of the WITH clause can be used in subsequent SELECT queries. There are certain limitations to the support, including:


* Recursion is not allowed in CTE

* Subqueries are not allowed in CTE


**Grammar**

```SQL
WITH [columnExpr] AS identifier
```


**Example 1: Use constant expressions as "variable"** 

```SQL
WITH '2024-07-01 15:23:00' as ts_upper_bound
SELECT *
FROM system.tables
WHERE 
metadata_modification_time <= ts_upper_bound
```


**Example 2: Evict the result of sum(bytes) expression from the SELECT clause list**

```SQL
WITH sum(total_bytes) as s
SELECT
    formatReadableSize(s),
    database
FROM system.tables
GROUP BY database
ORDER BY s
```


**Example 3: Use the result of a scalar subquery**

```SQL
/* this example would return TOP 10 of most huge database */
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


**Example 4: Reuse expressions in subqueries**

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

--result

┌─hello─────┬─hello_1─────┐
│ ['hello'] │ ['hello'] │
└───────────┴───────────┘
```


<span id="ad52d7ef"></span>
### FROM clause

The fromClause specifies the source of the data read:


* Table

* Subquery

* Table function


**Grammar**

Read data from the table

```SQL
FROM [tableIdentifier] [FINAL] [sampleClause] 
```


Read data from the subquery

```SQL
FROM ([selectUnionStmt]) [FINAL] [sampleClause]
```


Read data from the table function

```SQL
FROM tableFunctionExpr [FINAL] [sampleClause]
```



* `FINAL`: When `FINAL` is specified, ByteHouse fully merges the data before returning the results, thus performing all data transformations that occur during the merge process.


**Example**


1. Query from the table

   ```SQL
   CREATE TABLE test.fromClause (id UInt32, val UInt32) ENGINE=CnchMergeTree() ORDER BY id;
   INSERT INTO test.fromClause VALUES (1, 10), (1, 11), (1, 12), (2, 20), (2, 21);
   SELECT * FROM test.fromClause; -- expect 5 rows 
   ```
   

2. Query from the subquery

   ```SQL
   CREATE TABLE test.fromClause (id UInt32, val UInt32) ENGINE=CnchMergeTree() ORDER BY id;
   INSERT INTO test.fromClause VALUES (1, 10), (1, 11), (1, 12), (2, 20), (2, 21);
   SELECT * FROM (SELECT * FROM test.fromClause LIMIT 3); -- expect 3 rows 
   ```
   

3. Query from the table function

   ```SQL
   SELECT * FROM numbers(10); -- expect 10 rows 
   ```
   


We use the table function numbers here to generate a table containing 10 rows.

<span id="7efdcc16"></span>
### SAMPLE clause

The sampleClause allows for approximate SELECT query processing. When enabled, sampleClause executes queries on a segment of data instead of all data. This is extremely useful in the following scenarios:


* There are strict time requirements (such as less than 100 milliseconds), but it is not justifiable to increase hardware resources to meet these requirements.

* The original data is not accurate, so approximation does not significantly reduce quality.

* The business requirement targets approximate results (for cost\-effectiveness, or to provide precise results to premium users).

   Note: To use sampling, a sampling expression must be declared when creating the CnchMergeTree table, see [sampleByClause].


The features of data sampling are listed below:


* Data sampling is a deterministic mechanism. The same result **`SELECT ..`**  **`SAMPLE`** queries are always the same.

* For different tables, sampling works consistently. For tables with a single sampling key, sampling with the same coefficient always selects the same likely data subset. For example, a sample of userIds uses rows from the same subset of all possible userIds from different tables. This means you can use sampling in subqueries as well as JOIN.

* Sampling allows for reading less data from the disk. Note that you must correctly specify the sampling key.


Support for the following syntax is provided for the **`SAMPLE`** clause:


|SAMPLE Clause Syntax |Product Description |
|---|---|
|**SAMPLE k** |Here k is a number from 0 to 1.<br><br>Query is executed on k fraction of the data. For example, SAMPLE 0.1 runs the query on 10% of the data. |
|**SAMPLE n** |Here n is a sufficiently large integer.<br><br>The query is executed on at least n rows (but not exceeding this). For example, SAMPLE 10000000 runs the query on at least 10,000,000 rows. |
|**SAMPLE k OFFSET m** |Here k and m are numbers from 0 to 1.<br><br>Query the score of data k in the following examples. The data used for sampling has an offset m fraction. |


<span id="7972abf9"></span>
#### SAMPLE K

Here `k` ranges from 0 to 1, supporting decimals and scientific notation. For example, `SAMPLE 1/2` or `SAMPLE 0.5`.

**Syntax**

```SQL
SAMPLE K
```


**Example**

In this example, data is approximated using 10%.

```SQL
CREATE TABLE IF NOT EXISTS test.sampleClause (id UInt32) ENGINE=CnchMergeTree ORDER BY id SAMPLE BY id;
INSERT INTO test.sampleClause SELECT * FROM numbers(1000);
SELECT COUNT() FROM test.sampleClause SAMPLE 0.1; -- 1000 is expected
```


<span id="ea431a1b"></span>
#### SAMPLE N

Here `n` is a sufficiently large integer. For example, `SAMPLE 10000000`.

In this case, the query runs on at least one sample of `n` lines (but not more than that). For example, `SAMPLE 10000000` runs queries on at least 10,000,000 lines.

**Grammar**

```SQL
SAMPLE N
```


**Example**

In this example, an approximation calculation will be performed using 2 rows of data.

```SQL
CREATE TABLE IF NOT EXISTS test.sampleClause (id UInt32) ENGINE=CnchMergeTree ORDER BY id SAMPLE BY id;
INSERT INTO test.sampleClause SELECT * FROM numbers(1000);
SELECT COUNT() FROM test.sampleClause SAMPLE 2; -- 1000 is expected
```


<span id="f8897f16"></span>
#### SAMPLE K OFFSET M

Here `k` is a number ranging from 0 to 1 (supports decimal and decimal notation). For instance, `SAMPLE 1/2` or `SAMPLE 0.5`.

**Grammar**

```SQL
SAMPLE K OFFSET M
```


**Example**

In this example, after skipping 20% of the data, an approximation calculation will be performed using 10% of the data.

```SQL
CREATE TABLE IF NOT EXISTS test.sampleClause (id UInt32) ENGINE=CnchMergeTree ORDER BY id SAMPLE BY id;
INSERT INTO test.sampleClause SELECT * FROM numbers(1000);
SELECT COUNT() FROM test.sampleClause SAMPLE 0.1 OFFSET 0.2;
```


<span id="ad1c0430"></span>
### JOIN Clause

Join combines columns from one or more tables into a new table by using the common values available in each table.

**Syntax**

```SQL
[ANY|ALL|ASOF] [INNER|LEFT|RIGHT|FULL|CROSS] [OUTER] JOIN [tableIdentifier] ON|USING [columnExprList]
```


 **[ANY|ALL|ASOF]：** 


* ANY: If multiple rows in the right table match, only the first found row is joined. If only one row in the right table matches, the result is the same for ANY and ALL.

* ALL: If multiple rows in the right table match, ClickHouse creates a Cartesian product from the matching rows. This is the standard JOIN behavior in SQL.

* ASOF: Used to join sequences with uncertain matching.


 **[INNER|LEFT|RIGHT|FULL|CROSS]** : All standard SQL JOIN types.


* INNER JOIN: Only returns matching rows.

* LEFT OUTER JOIN: In addition to returning matching rows, it also returns unmatched rows from the left table.

* RIGHT OUTER JOIN: In addition to returning matching rows, it also returns unmatched rows from the right table.

* FULL OUTER JOIN: In addition to returning matching rows, it also returns unmatched rows from both tables.

* CROSS JOIN: Generates the Cartesian product of the entire table without specifying a "join key."


**ON|USING**：


* The expressions in the ON clause and the columns in the USING clause are referred to as "join keys."


**Example**

```SQL
CREATE TABLE IF NOT EXISTS test.joinClause (number UInt64) ENGINE=CnchMergeTree ORDER BY number;
INSERT INTO test.joinClause SELECT * FROM numbers(10);

SELECT number, joined FROM test.joinClause ANY LEFT JOIN (SELECT number * 2 AS number, number * 10 + 1 AS joined FROM test.joinClause LIMIT 10) js2 USING number LIMIT 10
```



|**number** |**joined** |
|---|---|
|0 |1 |
|1 |NULL |
|2 |21 |
|3 |NULL |


<span id="3e938464"></span>
### ARRAY JOIN clause

For tables containing array columns, an array join can generate a new table where the columns contain each individual array element from the initial columns, while other column values are repeated.

**Syntax**

```SQL
[LEFT] ARRAY JOIN [columnExprList]
```


Only one arrayJoinClause can be specified in a `SELECT` query.

`[LEFT] ARRAY JOIN`: Types of ARRAY JOIN


* `ARRAY JOIN` \- In basic cases, empty arrays are not included in the results of `JOIN`.

* `LEFT ARRAY JOIN` \- The results of `JOIN` include rows with empty arrays. The values of empty arrays are set to the default value of the array element type (usually 0, empty string, or NULL).


**Example**

```SQL
CREATE TABLE test.arrayJoinClause(s String, arr Array(UInt8)) ENGINE = CnchMergeTree ORDER BY s;
INSERT INTO test.arrayJoinClause VALUES ('Hello', [1,2]), ('World', [3,4,5]), ('Goodbye', []);
SELECT s, arr FROM test.arrayJoinClause ARRAY JOIN arr;
```


<span id="911f635a"></span>
### PREWHERE Clause

Prewhere is an optimization used to apply filtering more efficiently. Even if not explicitly specified, the PREWHERE clause is enabled by default. It works by automatically moving some of the WHERE conditions to the prewhere stage. The PREWHERE clause's function is solely to control this optimization when you believe you can perform better than the default optimization.

When using prewhere optimization, it first reads only the columns necessary for executing the prewhere expression. It then reads other columns necessary for executing the rest of the query, but only for data blocks where the prewhere expression evaluates to “true” in some rows. If there are many data blocks where the prewhere expression is “false” in all rows, and the columns needed for prewhere are fewer than those needed for the rest of the query, this can often significantly reduce the data read from disk during query execution.

**Syntax**

```SQL
PREWHERE [columnExpr](http://columnexpr/)
```


**Example**

```SQL
CREATE TABLE test.prewhereClause(id UInt32, val UInt32) ENGINE = CnchMergeTree() ORDER BY id;
INSERT INTO test.prewhereClause VALUES (1, 10), (1, 11), (1, 12), (2, 20), (2, 21);
SELECT * FROM test.prewhereClause PREWHERE id=1 WHERE val>10; -- (1, 11), (1, 12) expected
```


<span id="156062d4"></span>
### WHERE Clause

`WHERE` clause allows filtering data from the `SELECT` subclause FROM.

If there is a `WHERE` clause, it must contain an expression with the `UInt8` type. This is usually an expression with comparison and logical operators. Rows where the expression evaluates to 0 will be excluded from further transformations or results.

If the underlying table engine supports it, the `WHERE` expression will utilize indexes and partitions for pruning.

**Syntax**

```SQL
WHERE [columnExpr]
```


**Example**

```SQL
CREATE TABLE test.whereClause(id UInt32, val UInt32) ENGINE = CnchMergeTree() ORDER BY id;
INSERT INTO test.whereClause VALUES (1, 10), (1, 11), (1, 12), (2, 20), (2, 21);
SELECT * FROM test.whereClause WHERE val>10; -- (1, 11), (1, 12), (2, 20), (2, 21) expected
```


If you need to test for a NULL value, use IS NULL and IS NOT NULL operators or the isNull and isNotNull functions. Otherwise, expressions containing NULL will never pass.

**Example**

```SQL
CREATE TABLE t_null(x Int8, y Nullable(Int8)) ENGINE=CnchMergeTree() ORDER BY x;
INSERT INTO t_null VALUES (1, NULL), (2, 3);

SELECT * FROM t_null WHERE y IS NULL;
SELECT * FROM t_null WHERE y != 0;
```


**Result**

```SQL
┌─x─┬────y─┐
│ 1 │ ᴺᵁᴸᴸ │
└───┴──────┘
┌─x─┬─y─┐
│ 2 │ 3 │
└───┴───┘
```


<span id="f71e9371"></span>
### GROUP BY clause

The `GROUP BY` clause converts `SELECT` query results into an aggregated mode. `GROUP BY` clause uses [columnExprList] as grouping keys; the aggregated `SELECT` query results will contain the same number of rows as the unique values of the grouping keys in the source table.

**Syntax**

```SQL
GROUP BY [(][columnExprList][)] [WITH ROLLUP|WITH CUBE] [WITH TOTALS]
```



* `NULL processing`: ByteHouse interprets NULL as a value. If the grouping keys contain NULL values, they will appear in the results.

* `[WITH ROLLUP]`: Calculates subtotals based on the order of key expressions in the `GROUP BY` list.

   \* Subtotal rows are added after the result table.

   \* In subtotal rows, values of the "grouped" key expressions are set to 0 or blank rows.

* `[WITH CUBE]`: Calculates subtotals for every combination of key expressions in the `GROUP BY` list.

* `[WITH TOTALS]`: Calculates subtotals for all combinations of key expressions in the `GROUP BY` list.


**Example 1: Group by keys contain NULL values.** 

```SQL
CREATE TABLE IF NOT EXISTS test.groupByClause (x UInt32, y Nullable(UInt32)) ENGINE=CnchMergeTree ORDER BY x;
INSERT INTO test.groupByClause VALUES (1,2),(2,NULL),(3,2),(3,3),(3,NULL);
SELECT sum(x), y FROM test.groupByClause GROUP BY y; 
```


**Example 2: The WITH ROLLUP Modifier Grouped by Set**

```SQL
CREATE TABLE IF NOT EXISTS test.groupByClause (year UInt32, month UInt32, day UInt32) ENGINE=CnchMergeTree ORDER BY year;
INSERT INTO test.groupByClause VALUES (2019,1,5),(2019,1,15),(2020,1,5),(2020,1,15),(2021,1,5),(2021,1,15);
SELECT year, month, day, count() FROM test.groupByClause GROUP BY year, month, day WITH ROLLUP;
```


Since the GROUP BY section includes three key expressions, the result features subtotals tables which aggregate from right to left:


* GROUP BY year, month, day；

* GROUP BY year, month (and the day column is populated with zeros);

* GROUP BY year (now both month and day columns are filled with zeros);

* Total (all three key expression columns are zero).


**Example 3: The WITH CUBE Modifier Grouped by Set**

```SQL
CREATE TABLE IF NOT EXISTS test.groupByClause (year UInt32, month UInt32, day UInt32) ENGINE=CnchMergeTree ORDER BY year;
INSERT INTO test.groupByClause VALUES (2019,1,5),(2019,1,15),(2020,1,5),(2020,1,15),(2021,1,5),(2021,1,15);
SELECT year, month, day, count() FROM test.groupByClause GROUP BY year, month, day WITH CUBE;
```


Since the GROUP BY part includes three key expressions, the result features eight subtotals tables covering all combinations of key expressions:


* GROUP BY year, month, day

* GROUP BY year, month

* GROUP BY year, day

* GROUP BY year

* GROUP BY month, day

* GROUP BY month

* GROUP BY day

* Total (all three key expression columns are zero)


**Example 4: GROUP BY with the WITH TOTALS modifier**

```SQL
CREATE TABLE IF NOT EXISTS test.groupByClause (year UInt32, month UInt32, day UInt32) ENGINE=CnchMergeTree ORDER BY year;
INSERT INTO test.groupByClause VALUES (2019,1,5),(2019,1,15),(2020,1,5),(2020,1,15),(2021,1,5),(2021,1,15);
SELECT year, month, day, count() FROM test.groupByClause GROUP BY year, month, day WITH TOTALS;
```


If the WITH TOTALS modifier is specified, another row will be calculated.


* GROUP BY year, month, day

* Total (all three key expression columns are zero)


<span id="416392c4"></span>
### LIMIT BY clause

Select the top m rows for each distinct value of the expression

**Syntax**

Select the top m rows from the results for each distinct value of the expression list.

```SQL
LIMIT m BY [columnExprList]
```


**Example: Limit m rows by expression**

```SQL
CREATE TABLE test.limitByClause(id UInt32, val UInt32) ENGINE = CnchMergeTree() order by id;
INSERT INTO test.limitByClause VALUES (1, 10), (1, 11), (1, 12), (2, 20), (2, 21);
SELECT * FROM test.limitByClause ORDER BY id, val LIMIT 2 BY id; -- expect 4 rows. (1, 10), (1, 11), (2, 20), (2, 21) 
```


In this example, for each id (including values 1 and 2), we need to return 2 rows.

<span id="b023760f"></span>
### HAVING clause

Filter aggregate results produced by the groupByClause. It’s similar to the whereClause, but the difference is WHERE is executed before aggregation while HAVING is conducted post\-aggregation.

**Syntax**

```SQL
HAVING [columnExpr](http://columnexpr/)
```


**Example**

```SQL
CREATE TABLE test.havingClause(id UInt32, val UInt32) ENGINE = CnchMergeTree() ORDER BY id;
INSERT INTO test.havingClause VALUES (1, 10), (1, 11), (1, 12), (2, 20), (2, 21);
SELECT id FROM test.havingClause GROUP BY id HAVING count(id)>2; -- only 1 is expected. 
```


<span id="c1f032ad"></span>
### DISTINCT clause

If `SELECT DISTINCT` is declared, only unique rows are retained in the query results. Therefore, among all sets of completely matching rows in the results, only one row is retained.

**Null handling**

`DISTINCT` treats NULL as though `NULL` is a specific value, and `NULL==NULL`. In other words, in `DISTINCT` results, different combinations of `NULL` occur only once. It differs from the treatment of `NULL` in most other cases.

**Alternative methods**

By applying a GROUP BY to the same set of values specified in the `SELECT` clause, the same results can be obtained without using any aggregate functions. But there are several differences from `GROUP BY`:


* `DISTINCT` can be used with `GROUP BY`.

* When ORDER BY is omitted and LIMIT is defined, it stops running immediately after reading the required number of distinct rows.

* Data blocks are output during processing, without waiting for the entire query to finish running.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong><code>DISTINCT</code></strong> is not supported when <strong><code>SELECT</code></strong> includes a column with arrays.</div>


**Example**

ByteHouse supports the use of `DISTINCT` and `ORDER BY` for different columns in the same query. The `DISTINCT` clause is executed before the `ORDER BY` clause.

Example table:

```Plain
┌─a─┬─b─┐
│ 2 │ 1 │
│ 1 │ 2 │
│ 3 │ 3 │
│ 2 │ 4 │
└───┴───┘
```


When executing `SELECT DISTINCT a FROM t1 ORDER BY b ASC`, we obtain the following results:

```Plain
┌─a─┐
│ 2 │
│ 1 │
│ 3 │
└───┘
```


If we change the sorting direction to `SELECT DISTINCT a FROM t1 ORDER BY b DESC`, we achieve the following results:

```Plain
┌─a─┐
│ 3 │
│ 1 │
│ 2 │
└───┘
```


Rows `2, 4` are cut off before sorting.

<span id="196b9beb"></span>
### LIMIT clause

`LIMIT m` allows selecting the first `m` rows from the result.

`LIMIT n, m` enables selecting `m` rows after skipping the first result `n` rows. The syntax is equivalent to `LIMIT m OFFSET n`.

`n` and `m` must be non\-negative integers.

If there is no explicit ORDER BY clause to sort the results, the selection of rows in the result might be arbitrary and non\-deterministic.

**Syntax**

```SQL
LIMIT m
LIMIT n, m
LIMIT m OFFSET n
LIMIT ... WITH TIES
```


**Example 1: LIMIT m**

```SQL
CREATE TABLE IF NOT EXISTS test.limitClause (id UInt32) engine=CnchMergeTree() order by id;
INSERT INTO test.limitClause VALUES (1),(2),(3),(4),(5);
SELECT * FROM test.limitClause LIMIT 2; -- first 2 values will be return
```


**Example 2: LIMIT n, m**

```SQL
CREATE TABLE IF NOT EXISTS test.limitClause (id UInt32) engine=CnchMergeTree() order by id;
INSERT INTO test.limitClause VALUES (1),(2),(3),(4),(5);
SELECT * FROM test.limitClause LIMIT 1,2; -- skip first value，next 2 values will be return
SELECT * FROM test.limitClause LIMIT 2 OFFSET 1; -- skip first value，next 2 values will be return
```


**Example 3: LIMIT ...**  **WITH TIES**

```SQL
SELECT * FROM (
    SELECT number%50 AS n FROM numbers(100)
) ORDER BY n LIMIT 0,5 WITH TIES

┌─n─┐
│ 0 │
│ 0 │
│ 1 │
│ 1 │
│ 2 │
│ 2 │
└───┘
```


<span id="062869b6"></span>
### UNION ALL clause

You can use `UNION ALL` to combine any number of `SELECT` to expand its results.

**Syntax**

```SQL
UNION ALL ...
```


**Example**

```SQL
SELECT CounterID, 1 AS table, toInt64(count()) AS c
    FROM test.hits
    GROUP BY CounterID

UNION ALL

SELECT CounterID, 2 AS table, sum(Sign) AS c
    FROM test.visits
    GROUP BY CounterID
    HAVING c > 0
```


Result columns are matched by their index (in the internal order of `SELECT`). If column names do not match, the final result's name is taken from the first query. Perform type conversion jointly.

For example, if two merged queries have the same fields with non\-`Nullable` and `Nullable` from compatible types, the resulting `UNION ALL` will have a `Nullable` type field.

The queries that are part of the `UNION ALL` cannot be enclosed in parentheses. ORDER BY and LIMIT are applied to individual queries, not to the final result. If you need to apply transformations to the final result, you can include all queries in a FROM clause subquery using `UNION ALL`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only <code>UNION ALL</code> is supported. <code>UNION</code> (<code>UNION DISTINCT</code>) is not supported. If you need <code>UNION DISTINCT</code>, you can write a <code>SELECT DISTINCT</code> subquery that includes <code>UNION ALL</code>.</div>


<span id="046f089b"></span>
### SETTINGS clause

**Syntax**

```SQL
SETTINGS [settingExprList]
```


<span id="85e78d76"></span>
### INTO OUTFILE clause

Add an `INTO OUTFILE filename` clause (where filename is a string) to a `SELECT query` to redirect its output to a specified file on the client.

**Syntax**

```SQL
[INTO OUTFILE filename]
```


**Example**

```SQL
select * from ttt into outfile '~/abc.txt'
```



> * This feature is available through the command\-line client and clickhouse\-local. Therefore, sending queries via the HTTP interface will fail.

> * If a file with the same filename already exists, the query will fail.

> * The default output format is **`TabSeparated`** (just like in batch mode in the command\-line client).


<span id="bdf04b0e"></span>
### FORMAT clause

ByteHouse supports serialization formats available for query results. There are various methods to choose the formatting of `SELECT` output, one of which is to specify `FORMAT format` at the end of the query to obtain the result set in any specific format.

**Syntax**

```SQL
FORMAT format
```
