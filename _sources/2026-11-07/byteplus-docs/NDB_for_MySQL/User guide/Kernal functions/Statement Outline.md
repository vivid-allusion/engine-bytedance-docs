---
title: "Statement Outline"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Statement_Outline"
---

This article describes how to use the Statement outline feature.

<span id="oJjjdOvA"></span>
## Supported version


* MySQL version 8.0 with kernel version 3.0.6.1 or later.

* MySQL version 5.7 with kernel version 2.0.6.2 or later.


<span id="6wbdrtlS"></span>
## Background

<span id="pFrjRMqZ"></span>
### Statement outline

While an instance is running, the execution plans for some SQL statements might change unexpectedly, posing stability risks.

For example:


1. When online services use the `order by limit n` syntax, frequent changes in the execution plan affect performance, especially when the `n` value is small.

2. When the data volume changes, the statistical data also changes. These changes may cause the optimizer to make incorrect cost\-based decisions, leading to the selection of a non\-optimal index.


Temporary workarounds, such as adjusting the `optimizer_switch` parameter for the instance or modifying the business SQL by adding hints to associate the execution plan, are not business\-friendly. However, the Statement outline feature can associate the SQL execution plan with a SQL query template, allowing users to solidify the query plan without modifying the SQL and thus avoiding the risks mentioned above.

<span id="uOaCfCqg"></span>
### Terminology


|**Abbreviation** |**English full name** |**Chinese explanation** |
|---|---|---|
|Outline |Statement outline |Execution plan binding resolves the database instability problem caused by frequent changes to SQL execution plans in production environments. |
|Package |Native package procedure framework |A native toolkit is a logical collection of predefined stored procedures for using related stored procedures in a specific domain. |
|Digest |SQL Digest |An SQL fingerprint uses a SHA256 value by default in MySQL 8.0, and each template has a unique value. |
|Digest Text |SQL Digest Text |The SQL template is an SQL statement with its parameters removed. |


<span id="FDRlywEB"></span>
### Related parameters


|**Parameter name** |**Scope** |**Value range** |**Default value** |**Description** |
|---|---|---|---|---|
|opt_outline_enabled |GLOBAL |[ON\|OFF] |ON |Enables or disables the Statement outline feature. |


<span id="gBKqVY3L"></span>
## Prerequisites

[An instance has been created](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1) and its instance status is **Running**.

<span id="mPPYhDh5"></span>
## Hint

MySQL provides statement\-level optimizer control through hints. By adding hints to SQL statements, you can influence the decisions of the query optimizer:

```SQL
SELECT /*+ NO_RANGE_OPTIMIZATION(t3 PRIMARY, f2_idx) */ f1 FROM t3 WHERE f1 > 30 AND f1 < 33;
SELECT /*+ BKA(t1) NO_BKA(t2) */ * FROM t1 INNER JOIN t2 WHERE ...;
SELECT /*+ NO_ICP(t1, t2) */ * FROM t1 INNER JOIN t2 WHERE ...;
SELECT /*+ SEMIJOIN(FIRSTMATCH, LOOSESCAN) */ * FROM t1 ...;
EXPLAIN SELECT /*+ NO_ICP(t1) */ * FROM t1 WHERE ...;
SELECT /*+ MERGE(dt) */ * FROM (SELECT * FROM t1) AS dt;
INSERT /*+ SET_VAR(foreign_key_checks=OFF) */ INTO t2 VALUES(2);
```


The Statement outline feature supports associating two types of Hint with SQL templates to fix query plans. The supported Hint types are consistent with MySQL:


* [Index Hint](https://dev.mysql.com/doc/refman/8.0/en/index-hints.html)

* [Optimizer Hint](https://dev.mysql.com/doc/refman/8.0/en/optimizer-hints.html)


<span id="Wrcqu72f"></span>
## SQL syntax interface

NDB for MySQL has a built\-in native stored procedure (Native Package) toolkit for Outline. Users can perform Outline operations by calling the relevant `dbms_outline` interfaces.

<span id="Ko8dejYZ"></span>
### insert_optimizer_outline


* Description: Adds Optimizer Hints.

* Syntax:

   ```SQL
   CALL dbms_outline.insert_optimizer_outline('<Schema_name>','<Digest>','<Query_block>','<Hint>','<Query>');
   ```
   

* Parameter descriptions:

   
   |**Name** |**Description** |
   |---|---|
   |**Schema_name** |Database name.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can apply the Outline to all matching schemas by adding an empty <Schema_name\>: <code>''</code>.</div><br> |
   |**Digest** |Query the corresponding SQL fingerprint. |
   |**Query_Block** |The ID of the keyword (such as `SELECT` or `UPDATE`) to which the hint applies, starting from 1. |
   |**Hint** |**Hint** represents the complete hint string, for example, `/*+ NO_ICP(t1, t2) */`. |
   |**Query** |The original SQL statement for which to add a statement outline. |
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Either Digest or Query (original SQL statement) can be used. If a Query is provided, <code>dbms_outline</code> calculates the Digest and the SQL Template (Digest_text).   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When using quotation marks within a Query statement, enclose the part requiring quotes in single quotation marks, and enclose the entire Query statement in double quotation marks.   </div>
   

* Examples:

   ```SQL
   CALL dbms_outline.insert_optimizer_outline('outline_db', '', 1, '/*+ MAX_EXECUTION_TIME(1000) */', 'SELECT * FROM t1 WHERE id = 1');
   ```
   


<span id="cCXkuZxg"></span>
### insert_index_outline


* Description: Add Index Hints.

* Syntax:


```SQL
CALL dbms_outline.insert_index_outline('<Schema_name>','<Digest>','<Position>','<Type>','<Hint>','<Scope>','<Query>');
```



* Parameter description

   
   |**Name** |**Description** |
   |---|---|
   |**Schema_name** |Database name.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can apply the Outline to all matching schemas by adding an empty <Schema_name\>: <code>''</code>.</div><br> |
   |**Digest** |The corresponding SQL fingerprint. |
   |**Position** |The position of the table to apply the hint to, starting from 1. |
   |**Type** |Index hint type. The value can be `USE INDEX`, `FORCE INDEX`, or `IGNORE INDEX`. |
   |**Hint** |A list of index names, for example, `idx_1,idx_2`. |
   |**Scope**<br><br> |Are classified into the following three types:<br><br><br>* `FOR GROUP BY`<br><br>* `FOR ORDER BY`<br><br>* `FOR JOIN`<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">An empty string represents all types of Index Hints.</div><br> |
   |**Query** |The original SQL statement for which to add a statement outline. |
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Either Digest or Query (original SQL statement) can be used. If a Query is provided, <code>dbms_outline</code> calculates the Digest and the SQL Template (Digest_text).   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When using quotation marks within a Query statement, enclose the part requiring quotes in single quotation marks, and enclose the entire Query statement in double quotation marks.   </div>
   

* Examples:

   ```SQL
   -- Use the original SQL statement
   CALL dbms_outline.insert_index_outline('outline_db', '', 1, 'FORCE INDEX', 'idx_1', '',"SELECT * FROM t1 WHERE t1.col1 = 1 AND t1.col2 = 'mytest'");
   -- Use the SQL fingerprint
   CALL dbms_outline.insert_index_outline('outline_db', 'b4369611be7ab2d27c85897632576a04bc08f50b928a1d735b62d0a140628c4c', 1, 'USE INDEX', 'idx_1', '', "");
   ```
   


<span id="lFZdITlD"></span>
### check_outline


* Description: Verifies if the Statement outline for an SQL statement is effective. If a match is found, the SQL template applies the specified hint.

* Syntax:

   ```SQL
   CALL dbms_outline.check_outline('<Schema_name>', '<Query>');
   ```
   

* Parameter descriptions:

   
   |**Name** |**Description** |
   |---|---|
   |**Schema_name** |Database name.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Adding an empty <Schema_name\>: <code>''</code> applies the Outline to all matching schemas.</div><br> |
   |**Query** |The original SQL statement for which to add a statement outline. |
   

* Examples:

   ```SQL
   CALL dbms_outline.check_outline('outline_db', "SELECT * FROM t1 WHERE t1.col1 =1 AND t1.col2 ='mytest'");
   +------------+------------------------------------------------------------------+------------+------------+-------+---------------------+
   | SCHEMA     | DIGEST                                                          | BLOCK_TYPE | BLOCK_NAME | BLOCK | HINT                |
   +------------+------------------------------------------------------------------+------------+------------+-------+---------------------+
   | outline_db | b4369611be7ab2d27c85897632576a04bc08f50b928a1d735b62d0a140628c4c | TABLE      | t1         |     1 | USE INDEX (`idx_1`) |
   +------------+------------------------------------------------------------------+------------+------------+-------+---------------------+
   ```
   

* Explain：

   You can also use the `EXPLAIN` statement to check if the Outline is effective.

   ```SQL
   explain select * from t1 where t1.col1 =1 and t1.col2 ='mytest';
   +----+-------------+-------+------------+------+---------------+-------+---------+-------+------+----------+-------------+
   | id | select_type | table | partitions | type | possible_keys | key   | key_len | ref   | rows | filtered | Extra       |
   +----+-------------+-------+------------+------+---------------+-------+---------+-------+------+----------+-------------+
   |  1 | SIMPLE      | t1    | NULL       | ref  | idx_1         | idx_1 | 5       | const |    1 |   100.00 | Using where |
   +----+-------------+-------+------------+------+---------------+-------+---------+-------+------+----------+-------------+
   1 row in set, 1 warning (0.00 sec)
   mysql> show warnings;
   +-------+------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Level | Code | Message                                                                                                                                                                                                                                                 |
   +-------+------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Note  | 1003 | /* select#1 */ select `outline_db`.`t1`.`id` AS `id`,`outline_db`.`t1`.`col1` AS `col1`,`outline_db`.`t1`.`col2` AS `col2` from `outline_db`.`t1` USE INDEX (`idx_1`) where ((`outline_db`.`t1`.`col1` = 1) and (`outline_db`.`t1`.`col2` = 'mytest')) |
   +-------+------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   1 row in set (0.00 sec)
   ```
   

* Explain Analyze：

   [MySQL 8.0](https://dev.mysql.com/blog-archive/mysql-explain-analyze/) supports the `EXPLAIN ANALYZE` syntax, allowing users to execute a query and providing detailed execution information. Applies to scenarios that require a detailed analysis of query performance. After you enable Statement Outline, you can verify the outline's performance in Explain Analyze.

   ```SQL
   mysql> explain analyze SELECT * FROM t1 WHERE t1.col1 =1 AND t1.col2 ='mytest';
   +-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | EXPLAIN                                                                                                                                                                                                     |
   +-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | -> Filter: (t1.col2 = 'mytest')  (cost=1.10 rows=1) (actual time=0.100..0.100 rows=0 loops=1)                                                                                                               |
   |   -> Index lookup on t1 using idx_1 (col1=1)  (cost=1.10 rows=1) (actual time=0.099..0.099 rows=0 loops=1)                                                                                                  |
   +-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   1 row in set (0.00 sec)
   ```
   


<span id="5tbjC7Z4"></span>
### display_outline


* Description: View the saved Statement outlines and their effective status in the system.

* Syntax:

   ```Plain Text
   CALL dbms_outline.display_outline();
   ```
   

* Examples:

   ```SQL
   CALL dbms_outline.display_outline();
   +------+------------+------------------------------------------------------------------+-----------+-------+------+--------------------+------+----------+-----------------------------------------------------------------------------------------------------------------+
   | ID   | SCHEMA     | DIGEST                                                           | TYPE      | SCOPE | POS  | HINT               | HIT  | OVERFLOW | DIGEST_TEXT                                                                                                     |
   +------+------------+------------------------------------------------------------------+-----------+-------+------+--------------------+------+----------+-----------------------------------------------------------------------------------------------------------------+
   |    1 | outline_db | ab234071d1d3af13a775f45b532639203e1aa8c3ec63b289a75b9fb862c61c4c | USE INDEX |       |    1 | idx_1              |    0 |        0 | SELECT * FROM `t1` WHERE `t1` . `id` = ? UNION SELECT * FROM `t1` WHERE `t1` . `col1` = ? AND `t1` . `col2` = ? |
   |    2 | outline_db | ab234071d1d3af13a775f45b532639203e1aa8c3ec63b289a75b9fb862c61c4c | OPTIMIZER |       |    2 | /*+ QB_NAME(q2) */ |    0 |        0 | SELECT * FROM `t1` WHERE `t1` . `id` = ? UNION SELECT * FROM `t1` WHERE `t1` . `col1` = ? AND `t1` . `col2` = ? |
   +------+------------+------------------------------------------------------------------+-----------+-------+------+--------------------+------+----------+-----------------------------------------------------------------------------------------------------------------+
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><code>HIT</code> indicates the number of times this Statement outline has been hit,   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><code>OVERFLOW</code> indicates the number of times this Statement outline matched only the schema and digest, but did not find the Query Block or the corresponding table.   </div>
   


<span id="XJ5196uW"></span>
### delete_outline


* Description: Deletes a Statement outline from memory and tables.

* Syntax:

   ```Plain Text
   CALL dbms_outline.delete_outline(<Id>);
   ```
   

* Parameter descriptions:

   
   |**Name** |**Description** |
   |---|---|
   |**Id** |Outline ID。 |
   

* Examples:

   ```Plain Text
   CALL dbms_outline.delete_outline(2);
   ```
   

   If the Outline to be deleted does not exist, a warning is returned. Use `SHOW WARNINGS` to view the warning.

   ```SQL
   -- Delete non-existent outline
   CALL dbms_outline.delete_outline(999999);
   Query OK, 0 rows affected, 2 warnings (0.00 sec)
   SHOW WARNINGS;
   +---------+------+------------------------------------------------+
   | Level   | Code | Message                                        |
   +---------+------+------------------------------------------------+
   | Warning | 7521 | Statement outline 999999 is not found in table |
   | Warning | 7521 | Statement outline 999999 is not found in cache |
   +---------+------+------------------------------------------------+
   2 rows in set (0.00 sec)
   ```
   


<span id="xgeYdlB6"></span>
## Common scenarios

<span id="oxxrYM8L"></span>
### Index Hint

Specify using the idx_1 index of the t1 table.

```SQL
CALL dbms_outline.insert_index_outline('outline_db', '', 1, 'USE INDEX', 'idx_1', '',
    "select * from t1 where t1.col1 =1 and t1.col2 ='mytest'");
```


<span id="JuplIhz1"></span>
### Optimizer Hint

<span id="kYOfbglK"></span>
#### Using Nested\-Loop join


* Example

   ```SQL
   CALL dbms_outline.insert_optimizer_outline('outline_db', '', 1, '/*+ BNL(t1,t2) */',
         "select t1.id, t2.id from t1,t2");
   mysql> explain select t1.id, t2.id from t1,t2;
   +----+-------------+-------+------------+-------+---------------+-------+---------+------+------+----------+----------------------------------------------------+
   | id | select_type | table | partitions | type  | possible_keys | key   | key_len | ref  | rows | filtered | Extra                                              |
   +----+-------------+-------+------------+-------+---------------+-------+---------+------+------+----------+----------------------------------------------------+
   |  1 | SIMPLE      | t1    | NULL       | index | NULL          | ind_1 | 5       | NULL |    1 |   100.00 | Using index                                        |
   |  1 | SIMPLE      | t2    | NULL       | index | NULL          | ind_1 | 5       | NULL |    1 |   100.00 | Using index; Using join buffer (Block Nested Loop) |
   +----+-------------+-------+------------+-------+---------------+-------+---------+------+------+----------+----------------------------------------------------+
   2 rows in set, 1 warning (0.01 sec)
   mysql> show warnings;
   +-------+------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Level | Code | Message                                                                                                                                                                            |
   +-------+------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Note  | 1003 | /* select#1 */ select /*+ BNL(`t1`@`select#1`) BNL(`t2`@`select#1`) */ `outline_db`.`t1`.`id` AS `id`,`outline_db`.`t2`.`id` AS `id` from `outline_db`.`t1` join `outline_db`.`t2` |
   +-------+------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   1 row in set (0.00 sec)
   ```
   

* Sample:

   * BNL stands for Block Nested Loop, which is a table join algorithm. Its core logic is:

      * Loads data from the driving table (such as `t1`) into memory in blocks.

      * Matches data from the driven table (such as `t2`) row by row in the memory block.

      * Suitable for scenarios where the driving table is small and the driven table has no efficient index.

   * `BNL(t1, t2)` forces the optimizer to use the block nested loop join algorithm for the join operation between tables `t1` and `t2`.


<span id="f5DwiglZ"></span>
#### Related to subqueries


* Set the query block identifier for the subquery

   ```Plain Text
   CALL dbms_outline.insert_optimizer_outline('outline_db', '', 2, ' /*+ QB_NAME(subq1) */', 
         "SELECT * FROM t1 WHERE t1.col1 IN (SELECT col1 FROM t2)");
   ```
   

* Use SEMIJOIN\-related hints

   ```Plain Text
   CALL dbms_outline.insert_optimizer_outline('outline_db', '', 1, '/*+ SEMIJOIN(@subq1 MATERIALIZATION, DUPSWEEDOUT) */ ',
         "SELECT * FROM t1 WHERE t1.col1 IN (SELECT col1 FROM t2)");
   ```
   

* Example:

   * `SEMIJOIN` indicates that this hint is for a semi\-join operation, where a subquery (like `IN` or `EXISTS`) filters the primary table's data and only matches rows that have at least one corresponding record in the subquery.

   * @`subq1` identifies the name or alias of the subquery to be optimized, which in this case is the subquery name specified in the previous Outline.

   * `MATERIALIZATION` **Materialization strategy**: forces the subquery results to be temporarily stored in memory or on disk to avoid repeated computation. Suitable for scenarios where a small subquery result set is accessed multiple times.

   * `DUPSWEEDOUT` **Deduplication strategy**: eliminates duplicate values in the subquery results, ensuring that the primary query only matches unique values. Often used to optimize performance when a subquery may return duplicate data.

* Verifying the effect

   ```SQL
   mysql> explain SELECT * FROM t1 WHERE t1.col1 IN (SELECT col1 FROM t2);
   +----+--------------+-------------+------------+--------+---------------------+---------------------+---------+--------------------+------+----------+-------------+
   | id | select_type  | table       | partitions | type   | possible_keys       | key                 | key_len | ref                | rows | filtered | Extra       |
   +----+--------------+-------------+------------+--------+---------------------+---------------------+---------+--------------------+------+----------+-------------+
   |  1 | SIMPLE       | t1          | NULL       | ALL    | ind_1               | NULL                | NULL    | NULL               |    1 |   100.00 | Using where |
   |  1 | SIMPLE       | <subquery2> | NULL       | eq_ref | <auto_distinct_key> | <auto_distinct_key> | 5       | outline_db.t1.col1 |    1 |   100.00 | NULL        |
   |  2 | MATERIALIZED | t2          | NULL       | index  | ind_1               | ind_1               | 5       | NULL               |    1 |   100.00 | Using index |
   +----+--------------+-------------+------------+--------+---------------------+---------------------+---------+--------------------+------+----------+-------------+
   3 rows in set, 1 warning (0.00 sec)
   mysql> show warnings;
   +-------+------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Level | Code | Message                                                                                                                                                                                                                                                                                        |
   +-------+------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Note  | 1003 | /* select#1 */ select /*+ SEMIJOIN(@`subq1` MATERIALIZATION, DUPSWEEDOUT) */ `outline_db`.`t1`.`id` AS `id`,`outline_db`.`t1`.`col1` AS `col1`,`outline_db`.`t1`.`col2` AS `col2` from `outline_db`.`t1` semi join (`outline_db`.`t2`) where (`<subquery2>`.`col1` = `outline_db`.`t1`.`col1`) |
   +-------+------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   1 row in set (0.00 sec)
   ```
   


<span id="QPRroSuK"></span>
#### Set runtime variables for a single statement


* You can use SET_VAR to set variables for a single statement.

   ```Plain Text
   /*+ SET_VAR(<var_name>=<var_value>) */
   ```
   

   Outline example:

   * Set the maximum query time `MAX_EXECUTION_TIME`.

      ```SQL
      CALL dbms_outline.insert_optimizer_outline("outline_db", '', 1, '/*+ MAX_EXECUTION_TIME(1000) */',
            "select * from t1 where id = 1");
      ```
      

   * Set the foreign key constraint `foreign_key_checks`.

      ```SQL
      CALL dbms_outline.insert_optimizer_outline("outline_db", '', 1, '/*+ SET_VAR(foreign_key_checks=OFF) */',
          "select * from t1 where id = 1");
      ```
      

   * Verifying the effect

      ```SQL
      mysql> explain select * from t1 where id = 1;
      +----+-------------+-------+------------+------+---------------+------+---------+------+------+----------+--------------------------------+
      | id | select_type | table | partitions | type | possible_keys | key  | key_len | ref  | rows | filtered | Extra                          |
      +----+-------------+-------+------------+------+---------------+------+---------+------+------+----------+--------------------------------+
      |  1 | SIMPLE      | NULL  | NULL       | NULL | NULL          | NULL | NULL    | NULL | NULL |     NULL | no matching row in const table |
      +----+-------------+-------+------------+------+---------------+------+---------+------+------+----------+--------------------------------+
      1 row in set, 1 warning (0.01 sec)
      mysql> show warnings;
      +-------+------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Level | Code | Message                                                                                                                                                                                 |
      +-------+------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Note  | 1003 | /* select#1 */ select /*+ MAX_EXECUTION_TIME(1000) SET_VAR(foreign_key_checks='OFF') */ NULL AS `id`,NULL AS `col1`,NULL AS `col2` from `outline_db`.`t1` where multiple equal(1, NULL) |
      +-------+------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      1 row in set (0.00 sec)
      ```
      


<span id="6x0t1oMN"></span>
## FAQ

<span id="YX52HpWQ"></span>
### How does NDB for MySQL handle conflicting Outlines?

If a user inserts two conflicting Outlines, MySQL's hint resolve logic determines which hint takes effect. For details, refer to the [MySQL document](https://dev.mysql.com/doc/refman/8.4/en/optimizer-hints.html).


* Example

   ```SQL
   mysql> CALL dbms_outline.display_outline();
   +------+------------+------------------------------------------------------------------+-----------+-------+------+-------------------------------------------------------+------+----------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ID   | SCHEMA     | DIGEST                                                           | TYPE      | SCOPE | POS  | HINT                                                  | HIT  | OVERFLOW | DIGEST_TEXT                                                                                                                                                                                                                            |
   +------+------------+------------------------------------------------------------------+-----------+-------+------+-------------------------------------------------------+------+----------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |   14 |            | d9bc7ca4b466e3eff5c35133b62328b340e7996a20c0a3278f44e81908516796 | OPTIMIZER |       |    2 |  /*+ QB_NAME(subq2) */                                |    6 |        0 | SELECT * FROM `db1` . `t1` WHERE `t1` . `col1` IN ( SELECT `col1` FROM `db1` . `t2` )                                                                                                                                                  |
   |   15 |            | d9bc7ca4b466e3eff5c35133b62328b340e7996a20c0a3278f44e81908516796 | OPTIMIZER |       |    2 |  /*+ NO_INDEX(t1) */                                  |    2 |        0 | SELECT * FROM `db1` . `t1` WHERE `t1` . `col1` IN ( SELECT `col1` FROM `db1` . `t2` )                                                                                                                                                  |
   |   16 |            | d9bc7ca4b466e3eff5c35133b62328b340e7996a20c0a3278f44e81908516796 | OPTIMIZER |       |    2 |  /*+ INDEX(t1) */                                     |    2 |        0 | SELECT * FROM `db1` . `t1` WHERE `t1` . `col1` IN ( SELECT `col1` FROM `db1` . `t2` )                                                                                                                                                  |
   |   17 |            | d9bc7ca4b466e3eff5c35133b62328b340e7996a20c0a3278f44e81908516796 | OPTIMIZER |       |    2 |  /*+ INDEX(t2) */                                     |    0 |        0 | SELECT * FROM `db1` . `t1` WHERE `t1` . `col1` IN ( SELECT `col1` FROM `db1` . `t2` )                                                                                                                                                  |
   |   18 |            | d9bc7ca4b466e3eff5c35133b62328b340e7996a20c0a3278f44e81908516796 | OPTIMIZER |       |    2 |  /*+ NO_INDEX(t2) */                                  |    0 |        0 | SELECT * FROM `db1` . `t1` WHERE `t1` . `col1` IN ( SELECT `col1` FROM `db1` . `t2` )                                                                                                                                                  |
   +------+------------+------------------------------------------------------------------+-----------+-------+------+-------------------------------------------------------+------+----------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   mysql> CALL dbms_outline.check_outline('', 'SELECT * FROM db1.t1 WHERE t1.col1 IN (SELECT col1 FROM db1.t2)');
   +--------+------------------------------------------------------------------+------------+------------+-------+----------------------------------------------------+
   | SCHEMA | DIGEST                                                           | BLOCK_TYPE | BLOCK_NAME | BLOCK | HINT                                               |
   +--------+------------------------------------------------------------------+------------+------------+-------+----------------------------------------------------+
   |        | d9bc7ca4b466e3eff5c35133b62328b340e7996a20c0a3278f44e81908516796 | QUERY      |            |     1 | /*+ NO_INDEX(`t1`@`subq2`) INDEX(`t2`@`subq2`) */  |
   |        | d9bc7ca4b466e3eff5c35133b62328b340e7996a20c0a3278f44e81908516796 | QUERY      |            |     2 | /*+ QB_NAME(`subq2`) */                            |
   +--------+------------------------------------------------------------------+------------+------------+-------+----------------------------------------------------+
   2 rows in set, 2 warnings (0.00 sec)
   mysql> show warnings;
   +---------+------+-----------------------------------------------------------+
   | Level   | Code | Message                                                   |
   +---------+------+-----------------------------------------------------------+
   | Warning | 3126 | Hint INDEX(`t1` ) is ignored as conflicting/duplicated    |
   | Warning | 3126 | Hint NO_INDEX(`t2` ) is ignored as conflicting/duplicated |
   +---------+------+-----------------------------------------------------------+
   2 rows in set (0.00 sec)
   ```
   

* Example description

   * Query block 2 only contains t2, but the Outline specifies an index for t1. Additionally, it specifies both NO_INDEX and INDEX for t2. In this case, although all hints match, the first inserted Outline takes effect: `NO_INDEX(t1)` and `INDEX(t2)`.

   * A warning is returned for conflicting Outlines. Use `SHOW WARNINGS` to check the warning content.


<span id="FxMz0FTE"></span>
### On which nodes are Outlines added and effective?


* The SQL interfaces for managing Outlines can only be executed on the **primary node**. After you call the following SQL interfaces, Outline modifications are automatically synchronized to and take effect on **all** read\-only nodes:

   * insert_optimizer_outline

   * insert_index_outline

   * delete_outline

* The Outline verification and display interfaces can be executed on **any node**:

   * display_outline

   * check_outline


<span id="KAN71IMZ"></span>
### Does enabling Statement outline impact database performance?

After enabling Statement outline, an SQL fingerprint is calculated during SQL execution.

The impact on performance is negligible. In CPU\-bound performance tests, which are most affected by SQL fingerprint calculation, the performance impact of Outline is < 3%.

<span id="WcY9wJAt"></span>
### Do Backups restore the Outline in the system?


* If you select "Recovery to new instance", the instance data is fully restored to the new instance as of the specified time point, and the Outline table stored in the system is also restored to its state at the specified time point.

* If you select 'Restore to original instance', you will restore specified user databases and tables. In this case, the outlines will remain unchanged.


<span id="YEbHdpQm"></span>
### How does upgrading the MySQL version impact outlines?

MySQL 5.7 and MySQL 8.0 calculate SQL fingerprints differently. Therefore, outlines from the two versions are incompatible.

If you have added outlines on MySQL 5.7, NDB for MySQL will automatically migrate the outlines when the major version of the MySQL instance is upgraded from 5.7 to 8.0. After the migration is complete, the SQL fingerprints of the effective outlines will change.

Major versions of MySQL support different HINT types and have different optimizer decisions. As a result, outlines from MySQL 5.7 may not be optimal and might become invalid in MySQL 8.0. Confirm and verify all outlines after the upgrade to prevent your SQL queries from using unexpected execution plans.
