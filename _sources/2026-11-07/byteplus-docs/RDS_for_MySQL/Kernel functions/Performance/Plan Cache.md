---
title: "Plan Cache"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Plan_Cache"
---

This topic describes the Plan Cache feature in RDS for MySQL.

<span id="X4vx91lu"></span>
## Background

In high\-concurrency scenarios, applications often execute SQL statements that have the same structure but different parameters, such as SELECT test FROM sbtest1 WHERE id = ?;. These statements typically require parsing, optimization, and execution plan generation. If these statements are frequently executed and have simple logic, the repeated optimization process can cause additional CPU overhead.

Plan Cache caches the execution plans of prepared statements that meet specific conditions. After enabling this feature, for simple parameterized queries executed at high frequency, the database can reuse cached execution plans when no changes affecting plan selection occur in the execution environment or table state. This reduces redundant optimization overhead, improves throughput, and lowers latency.

<span id="pzf6Sc6p"></span>
## Supported version


* MySQL 5.7 version, and the kernel minor version is MySQL 5.7.44_20260615 and above.

* MySQL 8.0 version, and the kernel minor version is MySQL 8.0.43_20260415 and above.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can view the kernel minor version of an instance by <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_instance_details">Viewing instance information</a>. If your instance is a version earlier than MySQL 8.0.43_20260415 and MySQL 5.7.44_20260615, you can <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version">Upgrade instance kernel version</a>.</div>


<span id="coIV2oS5"></span>
## Feature description

After Plan Cache is enabled, the database automatically determines whether prepared statements meet the caching conditions. For statements that meet the conditions, the database tries to reuse the cached plan in subsequent repeated executions; for statements that do not meet the conditions, the database executes them as normal prepared statements.


* Typical applicable scenarios include:

   * Parameterized **single\-table** SELECT prepared statements that are executed frequently.

   * Point queries on primary or unique keys.

   * Apart from the aforementioned scenarios, the following cases also apply to MySQL 8.0 instances:

      * Index range queries.

      * Simple queries with ORDER BY and LIMIT.

* Plan Cache becomes invalid in the following scenarios:


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">An ineffective Plan Cache does not impact normal SQL execution, but only indicates that the execution plan for the SQL statement is not cached or reused.</div>



   * The loose_enable_plan_cache parameter is set to OFF, which means the Plan Cache feature is disabled.

   * Execute SQL statements that are not preprocessed.

   * Execute non\-SELECT statements, such as INSERT, UPDATE, DELETE, or INSERT ... SELECT。

   * The SQL statement is not a single\-table query or contains multi\-table JOIN or SEMI\-JOIN.

   * The table in the SELECT statement is a partitioned table.

   * Non\-simple query block scenarios, such as subqueries, UNION, derived tables, table functions, or queries that contain outer query blocks or inner query expressions.

   * Use of unsupported complex SQL semantics, such as GROUP BY, DISTINCT, ROLLUP, window functions, and full\-text search.

   * Query scenarios that involve stored procedures or custom functions.

   * The query has no WHERE clause, or the WHERE clause does not contain ? parameter.

   * The WHERE clause is a multi\-field composite condition, and the number of condition fields does not match the total number of index columns accessed during the index query.

   * A user\-defined variable is used in the WHERE clause.

   * Accessing temporary tables, schema table, views, and system database tables, such as information_schema, performance_schema, and mysql.

   * The SQL statement uses execution plan binding, optimizer binding strategies, or various index hint syntaxes. For example: FORCE INDEX, USE INDEX, IGNORE INDEX, etc.

   * For MySQL 5.7 instances, apart from the aforementioned scenarios, the Plan Cache will also be invalidated when executing equality queries that do not use indexes.

   * For MySQL 8.0 instances, the Plan Cache also becomes invalid in the following scenarios, in addition to the ones mentioned above:

      * Execute queries with the Hypergraph Optimizer enabled.

      * The secondary engine is enabled for the target data table of the query.

* Cached execution plans will be invalidated in the following scenarios:

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After cached execution plans are invalidated, subsequent statement execution will re\-enter the optimization process. If the statement still meets the caching conditions, the database will rebuild the execution plan cache.   </div>
   

   * The loose_enable_plan_cache parameter is set to OFF, which means the Plan Cache feature is disabled.

   * Deallocate a prepared statement, for example, by executing the DEALLOCATE PREPARE statement.

   * Recreate prepared statements with identical names or exactly consistent SQL content.

   * Perform DDL structural modification operations on the associated data tables of the query.

   * Modify the optimizer configuration parameter (optimizer_switch).

   * Modify the character set and collation of sessions or data tables.

   * Modify the database execution mode parameter (sql_mode).

   * Table statistics change drastically, typically when there is a significant variation in the statistically estimated row count of the table.


<span id="dgqJNiLx"></span>
## Instructions

<span id="W6dWLqZy"></span>
### Enable or disable the Plan Cache feature

Parameter description:


|**Parameter name** |**Type** |**Default value** |**Whether an instance restart is required for the change to take effect** |**Value range** |**Scope** |**Parameter description** |
|---|---|---|---|---|---|---|
|loose_enable_plan_cache |Boolean |OFF |No |ON、OFF |GLOBAL |Specifies whether to enable the Plan Cache feature.<br><br><br>* When set to ON, the database caches the execution plans for prepared statements that meet the conditions.<br><br>* When set to OFF, the database stops using the Plan Cache feature. |


You can view the following commands to enable or close the Plan Cache feature. If your instance does not support the SET command, you can also Modify parameters on the console.


* Enable the Plan Cache feature:

   ```SQL
   SET GLOBAL loose_enable_plan_cache = ON;
   ```
   

* Disable the Plan Cache feature:

   ```SQL
   SET GLOBAL loose_enable_plan_cache = OFF;
   ```
   

* Check whether the Plan Cache feature is enabled.

   ```SQL
   SHOW VARIABLES LIKE 'loose_enable_plan_cache';
   ```
   

* After the Plan Cache feature is enabled, check the Quantity of cached execution plans.

   ```SQL
   SHOW GLOBAL STATUS LIKE 'Cached_prepared_stmt_count';
   ```
   


<span id="U79VG5R8"></span>
### Syntax description

You need to use MySQL prepared statement syntax to execute parameterized SQL statements. The basic syntax is as follows:

```SQL
PREPARE stmt_name FROM 'SELECT ... WHERE col = ?';
SET @param_name = value;
EXECUTE stmt_name USING @param_name;
DEALLOCATE PREPARE stmt_name;
```


<span id="CaOBvaxm"></span>
## Examples

<span id="kQPyyBHC"></span>
### Example 1: Primary key point query

```SQL
CREATE TABLE t_plan_cache_demo (
  id BIGINT PRIMARY KEY,
  c VARCHAR(64),
  KEY idx_c (c)
);

INSERT INTO t_plan_cache_demo VALUES
  (1, 'a'),
  (2, 'b'),
  (3, 'c');

SET GLOBAL loose_enable_plan_cache = ON;

PREPARE stmt_point_select FROM
  'SELECT c FROM t_plan_cache_demo WHERE id = ?';

SET @id = 1;
EXECUTE stmt_point_select USING @id;

SET @id = 2;
EXECUTE stmt_point_select USING @id;

SET @id = 3;
EXECUTE stmt_point_select USING @id;

SHOW GLOBAL STATUS LIKE 'Cached_prepared_stmt_count';

DEALLOCATE PREPARE stmt_point_select;
```


<span id="lAkBPFBM"></span>
### Example 2: Index range query (For MySQL 8.0 instances only)

```SQL
SET GLOBAL loose_enable_plan_cache = ON;

PREPARE stmt_range_select FROM
  'SELECT id, c FROM t_plan_cache_demo WHERE c >= ? ORDER BY c LIMIT 10';

SET @c = 'a';
EXECUTE stmt_range_select USING @c;

SET @c = 'b';
EXECUTE stmt_range_select USING @c;

SET @c = 'c';
EXECUTE stmt_range_select USING @c;

SHOW GLOBAL STATUS LIKE 'Cached_prepared_stmt_count';

DEALLOCATE PREPARE stmt_range_select;
```


<span id="j4ji5vjE"></span>
## Performance test


<Tabs>
<Tab zoneid="FRSSdjChP6" title="MySQL 5.7">
<TabTitle>MySQL 5.7</TabTitle>

The following performance data is from a Sysbench test of typical read\-only scenarios in prepared statement execution mode. The test covers both full CPU load and non\-saturated CPU load states, comparing the changes in TPS/QPS and average latency before and after enabling Plan Cache.

<span id="FzS69ITd"></span>
### Test Environment


* Test method: Execution of typical Sysbench read\-only scenarios in prepared statement execution mode.

* Test scenarios: oltp_point_select, oltp_read_only.

* Data size: 10 tables, each with 500,000 rows of data.

* Comparison metrics: TPS/QPS percentage improvement, Average latency percentage reduction.


<span id="kpxonDSP"></span>
### Test steps


1. Prepare the test table and test data.

2. Close the Plan Cache, execute a benchmark test, and record the TPS/QPS and average latency.

   ```SQL
   SET GLOBAL loose_enable_plan_cache = OFF;
   ```
   

3. Enable the Plan Cache, execute the same test, and record the TPS/QPS and average latency.

   ```SQL
   SET GLOBAL loose_enable_plan_cache = ON;
   ```
   

4. Compare the performance data before and after enabling the feature.

5. Use the status variables to confirm the quantity of cached plans.

   ```SQL
   SHOW GLOBAL STATUS LIKE 'Cached_prepared_stmt_count';
   ```
   


<span id="LSmLfhsK"></span>
### The test results are as follows.


|<div style="text-align: center"><br><strong>Test scenario</strong></div><br> |<div style="text-align: center"><br><strong>TPS/QPS improvement</strong></div><br> |<div style="text-align: center"><br><strong>Average latency reduction</strong></div><br> |
|---|---|---|
|<div style="text-align: center"><br>oltp_point_select</div><br> |<div style="text-align: center"><br>21.4%</div><br> |<div style="text-align: center"><br>17.4%</div><br> |
|<div style="text-align: center"><br>oltp_read_only</div><br> |<div style="text-align: center"><br>12.6%</div><br> |<div style="text-align: center"><br>17.8%</div><br> |



</Tab>
<Tab zoneid="Tkbl6h3q8N" title="MySQL 8.0">
<TabTitle>MySQL 8.0</TabTitle>

The following performance data is from a Sysbench test of typical Read/Write scenarios in prepared statement execution mode. The test covers both full CPU load and non\-saturated CPU load states, comparing the changes in TPS/QPS and average latency before and after enabling Plan Cache.

<span id="nJQl93fE"></span>
### Test Environment


* Test method: Execution of typical Sysbench Read/Write scenarios in prepared statement execution mode.

* Test scenarios: oltp_point_select, select_random_points, oltp_read_only, oltp_read_write.

* Data size: 10 tables, each with 500,000 rows of data.

* Comparison metrics: TPS/QPS percentage improvement, Average latency percentage reduction.


<span id="y4kmWhyy"></span>
### Test steps


1. Prepare the test table and test data.

2. Close the Plan Cache, execute a benchmark test, and record the TPS/QPS and average latency.

   ```SQL
   SET GLOBAL loose_enable_plan_cache = OFF;
   ```
   

3. Enable the Plan Cache, execute the same test, and record the TPS/QPS and average latency.

   ```SQL
   SET GLOBAL loose_enable_plan_cache = ON;
   ```
   

4. Compare the performance data before and after enabling the feature.

5. Use the status variables to confirm the quantity of cached plans.

   ```SQL
   SHOW GLOBAL STATUS LIKE 'Cached_prepared_stmt_count';
   ```
   


<span id="Hy9FLV6r"></span>
### The test results are as follows.


|<div style="text-align: center"><br><strong>Test scenario</strong></div><br> |<div style="text-align: center"><br><strong>TPS/QPS improvement</strong></div><br> |<div style="text-align: center"><br><strong>Average latency reduction</strong></div><br> |
|---|---|---|
|<div style="text-align: center"><br>oltp_point_select</div><br> |<div style="text-align: center"><br>39.7%</div><br> |<div style="text-align: center"><br>27.5%</div><br> |
|<div style="text-align: center"><br>select_random_points</div><br> |<div style="text-align: center"><br>19.6%</div><br> |<div style="text-align: center"><br>16.6%</div><br> |
|<div style="text-align: center"><br>oltp_read_only</div><br> |<div style="text-align: center"><br>21.6%</div><br> |<div style="text-align: center"><br>17.8%</div><br> |
|<div style="text-align: center"><br>oltp_read_write</div><br> |<div style="text-align: center"><br>8.7%</div><br> |<div style="text-align: center"><br>8.0%</div><br> |



</Tab>
</Tabs>


&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;
