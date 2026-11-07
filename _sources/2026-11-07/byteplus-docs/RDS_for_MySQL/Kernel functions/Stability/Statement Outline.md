---
title: "Statement Outline"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Statement_Outline"
---

## Supported version

* MySQL 5.7 version, and the kernel minor version is MySQL 5.7.32 _20250415 and above.

* MySQL 8.0 version, and the kernel minor version is MySQL 8.0.32 _20250215 and above.

* MySQL 8.4, with a kernel minor version of MySQL 8.4.7_20260415 or later.

> **tip**

> You can view the kernel minor version of an instance by [Viewing instance information](https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_instance_details). If the kernel minor version of your instance is not within the supported kernel minor version range, you can [Manually upgrading the instance kernel minor version](https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version).

## Background

### Statement outline

While an instance is running, the execution plans for some SQL statements might change unexpectedly, posing stability risks.

For example:

1. When online services use the `order by limit n` syntax, frequent changes in the execution plan affect performance, especially when the n value is small.

2. When the data volume changes, the statistical data also changes. These changes may cause the optimizer to make incorrect cost\-based decisions, leading to the selection of a non\-optimal index.

Temporary workarounds, such as adjusting the `optimizer_switch` parameter for the instance or modifying the business SQL by adding hints to associate the execution plan, are not business\-friendly. However, the Statement outline feature can associate the SQL execution plan with a SQL query template, allowing users to solidify the query plan without modifying the SQL and thus avoiding the risks mentioned above.

### Terminology

|Abbreviation |English full name |Chinese explanation |
|---|---|---|
|Outline |Statement outline |Execution plan binding resolves the database instability problem caused by frequent changes to SQL execution plans in production environments. |
|Package |Native package procedure framework |A native toolkit is a logical collection of predefined stored procedures for using related stored procedures in a specific domain. |
|Digest |SQL Digest |An SQL fingerprint uses a SHA256 value by default in MySQL 8.0, and each template has a unique value. |
|Digest Text |SQL Digest Text |The SQL template is an SQL statement with its parameters removed. |

### Related parameters

|Parameter name |Scope |Value range |Default value |Description |
|---|---|---|---|---|
|loose_outline_enabled |GLOBAL |[ON\|OFF] |ON |Enables or disables the Statement outline feature. |

> **tip**

> This parameter is not open for modification. To modify it, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support.

## Prerequisites

An instance has been created and its instance status is **Running**.

## Hint

MySQL provides statement\-level optimizer control through hints. By adding hints to SQL statements, you can influence the decisions of the query optimizer:

```sql
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

## SQL syntax interface

RDS for MySQL has a built\-in native stored procedure (Native Package) toolkit for Outline. Users can perform Outline operations by calling the relevant `dbms_outline` interfaces.

### insert_optimizer_outline

* Description: Adds Optimizer Hints.

* Syntax:

   ```sql
   CALL dbms_outline.insert_optimizer_outline('<Schema_name>','<Digest>','<Query_block>','<Hint>','<Query>');
   ```

* Parameter description:

   |**Parameter** |**Description** |
   |---|---|
   |**Schema_name** |Database name.<br><br>> **tip**<br><br><br>> You can apply the Outline to all matching schemas by adding an empty <Schema_name\>: `''`.<br> |
   |**Digest** |Query the corresponding SQL fingerprint.<br><br>> **tip**<br><br><br><br>* > Either Digest or Query (original SQL statement) can be used. If a Query is provided, dbms_outline calculates the Digest and the SQL Template (Digest_text).<br><br><br>* > Digest generation follows the same logic as MySQL. Take note that MySQL statement_digest is **case\-sensitive** for identifiers, including database names, table names, column names and aliases. Distinct digests may be generated even if these identifiers are case\-insensitive in SQL semantics. It is recommended to use the same SQL statements as production when adding outlines. For more information, refer to [STATEMENT_DIGEST](https://dev.mysql.com/doc/refman/8.0/en/encryption-functions.html#function_statement-digest).<br> |
   |**Query_Block** |Number of the query block to which the optimizer hint is applied, starting from 1. Query blocks are numbered sequentially from left to right based on the occurrence order of keywords ([SELECT](https://dev.mysql.com/doc/refman/9.7/en/select.html), [UPDATE](https://dev.mysql.com/doc/refman/9.7/en/update.html), [INSERT](https://dev.mysql.com/doc/refman/9.7/en/insert.html), [REPLACE](https://dev.mysql.com/doc/refman/9.7/en/replace.html), [DELETE](https://dev.mysql.com/doc/refman/9.7/en/delete.html)) in the SQL statement. Query_Block corresponds to the ordinal number of the query block to which the hint applies. |
   |**Hint** |**Hint** represents the complete hint string, for example, `/*+ NO_ICP(t1, t2) */`. |
   |**Query** |The original SQL statement for which to add a statement outline.<br><br>> **tip**<br><br><br>> When using quotation marks within a Query statement, enclose the part requiring quotes in single quotation marks, and enclose the entire Query statement in double quotation marks.<br> |

* Sample:

   ```sql
   CALL dbms_outline.insert_optimizer_outline('outline_db', '', 1, '/*+ MAX_EXECUTION_TIME(1000) */', 'SELECT * FROM t1 WHERE id = 1');
   ```

### insert_index_outline

* Description: Add Index Hints.

* Syntax:

   ```sql
   CALL dbms_outline.insert_index_outline('<Schema_name>','<Digest>','<Position>','<Type>','<Hint>','<Scope>','<Query>');
   ```

* Parameter description

   |**Parameter** |**Description** |
   |---|---|
   |**Schema_name** |Database name.<br><br>> **tip**<br><br><br>> You can apply the Outline to all matching schemas by adding an empty <Schema_name\>: `''`.<br> |
   |**Digest** |The corresponding SQL fingerprint.<br><br>> **tip**<br><br><br><br>* > Either Digest or Query (original SQL statement) can be used. If a Query is provided, dbms_outline calculates the Digest and the SQL Template (Digest_text).<br><br><br>* > Digest generation follows the same logic as MySQL. Take note that MySQL statement_digest is **case\-sensitive** for identifiers, including database names, table names, column names and aliases. Distinct digests may be generated even if these identifiers are case\-insensitive in SQL semantics. It is recommended to use the same SQL statements as production when adding outlines. For more information, refer to [STATEMENT_DIGEST](https://dev.mysql.com/doc/refman/8.0/en/encryption-functions.html#function_statement-digest).<br> |
   |**Position** |The position number of the target table starts from 1 Tables are numbered sequentially from left to right according to their occurrence order in the SQL statement. Position corresponds to the ordinal number of the table to which the hint applies. |
   |**Type** |Index hint type. The value can be `USE INDEX`, `FORCE INDEX`, or `IGNORE INDEX`. |
   |**Hint** |A list of index names, for example, `idx_1,idx_2`. |
   |**Scope** |Are classified into the following three types:<br><br><br>* `FOR GROUP BY`<br><br>* `FOR ORDER BY`<br><br>* `FOR JOIN`<br><br>> An empty string represents all types of Index Hints. |
   |**Query** |The original SQL statement for which to add a statement outline.<br><br>> **tip**<br><br><br>> When using quotation marks within a Query statement, enclose the part requiring quotes in single quotation marks, and enclose the entire Query statement in double quotation marks.<br> |

* Sample:

   ```sql
   -- Use the original SQL statement
   CALL dbms_outline.insert_index_outline('outline_db', '', 1, 'FORCE INDEX', 'idx_1', '',"SELECT * FROM t1 WHERE t1.col1 = 1 AND t1.col2 = 'mytest'");
   
   -- Use the SQL fingerprint
   CALL dbms_outline.insert_index_outline('outline_db', 'b4369611be7ab2d27c85897632576a04bc08f50b928a1d735b62d0a140628c4c', 1, 'USE INDEX', 'idx_1', '', "");
   ```

### check_outline

* Description: Verifies if the Statement outline for an SQL statement is effective. If a match is found, the SQL template applies the specified hint.

* Syntax:

   ```sql
   CALL dbms_outline.check_outline('<Schema_name>', '<Query>');
   ```

* Parameter description:

   |**Parameter** |**Description** |
   |---|---|
   |**Schema_name** |Database name.<br><br>> **tip**<br><br><br>> Adding an empty <Schema_name\>: `''` applies the Outline to all matching schemas.<br> |
   |**Query** |The original SQL statement for which to add a statement outline. |

* Sample:

   ```sql
   CALL dbms_outline.check_outline('outline_db', "SELECT * FROM t1 WHERE t1.col1 =1 AND t1.col2 ='mytest'");
   +------------+------------------------------------------------------------------+------------+------------+-------+---------------------+
   | SCHEMA     | DIGEST                                                          | BLOCK_TYPE | BLOCK_NAME | BLOCK | HINT                |
   +------------+------------------------------------------------------------------+------------+------------+-------+---------------------+
   | outline_db | b4369611be7ab2d27c85897632576a04bc08f50b928a1d735b62d0a140628c4c | TABLE      | t1         |     1 | USE INDEX (`idx_1`) |
   +------------+------------------------------------------------------------------+------------+------------+-------+---------------------+
   ```

* Explain：

You can also use the `EXPLAIN` statement to check if the Outline is effective.

```sql
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

   ```sql
   mysql> explain analyze SELECT * FROM t1 WHERE t1.col1 =1 AND t1.col2 ='mytest';
   +-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | EXPLAIN                                                                                                                                                                                                     |
   +-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | -> Filter: (t1.col2 = 'mytest')  (cost=1.10 rows=1) (actual time=0.100..0.100 rows=0 loops=1)                                                                                                               |
   |   -> Index lookup on t1 using idx_1 (col1=1)  (cost=1.10 rows=1) (actual time=0.099..0.099 rows=0 loops=1)                                                                                                  |
   +-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   1 row in set (0.00 sec)
   ```

### display_outline

* Description: View the saved Statement outlines and their effective status in the system.

* Syntax:

   ```sql
   CALL dbms_outline.display_outline();
   ```

* Sample:

   ```sql
   CALL dbms_outline.display_outline();
   +------+------------+------------------------------------------------------------------+-----------+-------+------+--------------------+------+----------+-----------------------------------------------------------------------------------------------------------------+
   | ID   | SCHEMA     | DIGEST                                                           | TYPE      | SCOPE | POS  | HINT               | HIT  | OVERFLOW | DIGEST_TEXT                                                                                                     |
   +------+------------+------------------------------------------------------------------+-----------+-------+------+--------------------+------+----------+-----------------------------------------------------------------------------------------------------------------+
   |    1 | outline_db | ab234071d1d3af13a775f45b532639203e1aa8c3ec63b289a75b9fb862c61c4c | USE INDEX |       |    1 | idx_1              |    0 |        0 | SELECT * FROM `t1` WHERE `t1` . `id` = ? UNION SELECT * FROM `t1` WHERE `t1` . `col1` = ? AND `t1` . `col2` = ? |
   |    2 | outline_db | ab234071d1d3af13a775f45b532639203e1aa8c3ec63b289a75b9fb862c61c4c | OPTIMIZER |       |    2 | /*+ QB_NAME(q2) */ |    0 |        0 | SELECT * FROM `t1` WHERE `t1` . `id` = ? UNION SELECT * FROM `t1` WHERE `t1` . `col1` = ? AND `t1` . `col2` = ? |
   +------+------------+------------------------------------------------------------------+-----------+-------+------+--------------------+------+----------+-----------------------------------------------------------------------------------------------------------------+
   ```

> **tip**

* > `HIT` indicates the number of times this Statement outline has been hit,

* > `OVERFLOW` indicates the number of times this Statement outline matched only the schema and digest, but did not find the Query Block or the corresponding table.

### delete_outline

* Description: Deletes a Statement outline from memory and tables.

* Syntax:

   ```sql
   CALL dbms_outline.delete_outline(<Id>);
   ```

* Parameter description:

   |**Parameter** |**Description** |
   |---|---|
   |**Id** |Outline ID。 |

* Sample:

   ```sql
   CALL dbms_outline.delete_outline(2);
   ```

   If the Outline to be deleted does not exist, a warning is returned. Use `SHOW WARNINGS` to view the warning.

   ```sql
   --Delete non-existent outline
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

## Common scenarios

### Index Hint

#### Specify using the idx_1 index of the t1 table

```sql
CALL dbms_outline.insert_index_outline('outline_db', '', 1, 'USE INDEX', 'idx_1', '',
    "select * from t1 where t1.col1 =1 and t1.col2 ='mytest'");
```

### Optimizer Hint

#### Using the hotspot high\-concurrency update feature

#### For hot\-row update operations (flash sale scenarios), the kernel of RDS for MySQL supports marking flash sale statements by adding HINTs to the relevant SQL statements, significantly improving the performance of hotspot high\-concurrency updates.

> **tip**

> For more information about the hotspot high\-concurrency update feature, refer to [Hotspot high\-concurrency updates](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Hotspot_high_concurrent_updates).

By adding an optimizer hint through Statement Outline, you can enable flash sales for SQL statements without modifying the code:

* Enable flash sales for a single statement:

   ```sql
   CALL dbms_outline.insert_optimizer_outline('stock_db', '', 1, '/*+ LOGIC_UPDATE */',
         "update t_stock set num = num - 1 where id = 2 and num > 0");
   ```

   This is equivalent to adding the HINT:

   > **tip**

   > Add `/*+ LOGIC_UPDATE */` to mark the statement for flash sales.

```sql
update /*+ LOGIC_UPDATE */ t_stock set num = num - 1 where id = X and num > 0;
```

* Enable flash sales for statements within a transaction block

   ```sql
   CALL dbms_outline.insert_optimizer_outline('stock_db', '', 1, '/*+ LOGIC_UPDATE AUTO_LOGIC_COMMIT_ROLLBACK */',
         "update t_stock set num = num - 1 where id = 2 and num > 0");
   ```

   This is equivalent to adding the HINT.

   > **tip**

   > Add `/*+ LOGIC_UPDATE AUTO_LOGIC_COMMIT_ROLLBACK */` to the last statement of the transaction block to mark the transaction for flash sales.

   ```sql
   begin; 
   insert into t_order(userid, stockid, num) values(1, 2, 3); 
   update /*+ LOGIC_UPDATE AUTO_LOGIC_COMMIT_ROLLBACK */ t_stock set num = num - 1 where id = X and num > 0;
   commit;
   ```

* You can use the `Explain` statement to verify that the flash sales feature is enabled:

   > **tip**

   > If the Extra column contains `Using logical`, the statement uses the flash sales feature.

   ```sql
   mysql> EXPLAIN update t_stock set num = num - 1 where id = 1 and num > 0;
   +----+-------------+---------+------------+-------+---------------+---------+---------+-------+------+----------+----------------------------+
   | id | select_type | table   | partitions | type  | possible_keys | key     | key_len | ref   | rows | filtered | Extra                      |
   +----+-------------+---------+------------+-------+---------------+---------+---------+-------+------+----------+----------------------------+
   |  1 | UPDATE      | t_stock | NULL       | range | PRIMARY       | PRIMARY | 4       | const |    1 |   100.00 | Using where; Using logical |
   +----+-------------+---------+------------+-------+---------------+---------+---------+-------+------+----------+----------------------------+
   1 row in set, 1 warning (0.00 sec)
   ```

#### Using Nested\-Loop join

* Sample

   ```sql
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

      * Loads data from the driving table (such as `t1`) into memory in blocks

      * Matches data from the driven table (such as `t2`) row by row in the memory block

      * Suitable for scenarios where the driving table is small and the driven table has no efficient index.

   * `BNL(t1, t2)` forces the optimizer to use the block nested loop join algorithm for the join operation between tables `t1` and `t2`.

#### Related to subqueries

* Set the query block identifier for the subquery

   ```sql
   CALL dbms_outline.insert_optimizer_outline('outline_db', '', 2, ' /*+ QB_NAME(subq1) */', 
         "SELECT * FROM t1 WHERE t1.col1 IN (SELECT col1 FROM t2)");
   ```

* Use SEMIJOIN\-related hints

   ```sql
   CALL dbms_outline.insert_optimizer_outline('outline_db', '', 1, '/*+ SEMIJOIN(@subq1 MATERIALIZATION, DUPSWEEDOUT) */ ',
         "SELECT * FROM t1 WHERE t1.col1 IN (SELECT col1 FROM t2)");
   ```

* Example:

   * `SEMIJOIN` indicates that this hint is for a semi\-join operation, where a subquery (like `IN` or `EXISTS`) filters the primary table's data and only matches rows that have at least one corresponding record in the subquery.

   * `@subq1` identifies the name or alias of the subquery to be optimized. Here, it is the subquery name specified in the previous Outline.

   * `MATERIALIZATION` **Materialization strategy**: forces the subquery results to be temporarily stored in memory or on disk to avoid repeated computation. Suitable for scenarios where a small subquery result set is accessed multiple times.

   * `DUPSWEEDOUT` **Deduplication strategy**: eliminates duplicate values in the subquery results, ensuring that the primary query only matches unique values. Often used to optimize performance when a subquery may return duplicate data

* Verifying the effect

   ```sql
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

#### Set runtime variables for a single statement

* You can use SET_VAR to set variables for a single statement

   ```sql
   /*+ SET_VAR(<var_name>=<var_value>) */
   ```

Outline example:

* Set the maximum query time `MAX_EXECUTION_TIME`

   ```sql
   CALL dbms_outline.insert_optimizer_outline("outline_db", '', 1, '/*+ MAX_EXECUTION_TIME(1000) */',
         "select * from t1 where id = 1");
   ```

* Set the foreign key constraint `foreign_key_checks`

   ```sql
   CALL dbms_outline.insert_optimizer_outline("outline_db", '', 1, '/*+ SET_VAR(foreign_key_checks=OFF) */',
       "select * from t1 where id = 1");
   ```

* Verifying the effect

   ```sql
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

## FAQ

### How does RDS for MySQL handle conflicting Outlines?

If a user inserts two conflicting Outlines, MySQL's hint resolve logic determines which hint takes effect. For details, refer to the [MySQL document](https://dev.mysql.com/doc/refman/8.4/en/optimizer-hints.html).

* Sample

   ```sql
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

### On which nodes are Outlines added and effective?

* The SQL interfaces for managing Outlines can only be executed on the **primary node**. After you call the following SQL interfaces, Outline modifications are automatically synchronized to and take effect on **all** read\-only nodes and Standby nodes:

   * insert_optimizer_outline

   * insert_index_outline

   * delete_outline

* The Outline verification and display interfaces can be executed on **any node**:

   * display_outline

   * check_outline

### Does enabling Statement outline impact database performance?

After enabling Statement outline, an SQL fingerprint is calculated during SQL execution.

The impact on performance is negligible. In CPU\-bound performance tests, which are most affected by SQL fingerprint calculation, the performance impact of Outline is < 3%.

### Do Backups restore the Outline in the system?

* If you select **Recovery to new instance**, the instance data is fully restored to the new instance as of the specified time point, and the Outline table stored in the system is also restored to its state at the specified time point.

* If you select **Restore to original instance**, you will restore specified user databases and tables. In this case, the outlines will remain unchanged.

### How does upgrading the MySQL version impact outlines?

MySQL 5.7 and MySQL 8.0 calculate SQL fingerprints differently. Therefore, outlines from the two versions are incompatible.

If you have added outlines on MySQL 5.7, RDS for MySQL will automatically migrate the outlines when the major version of the MySQL instance is upgraded from 5.7 to 8.0. After the migration is complete, the SQL fingerprints of the effective outlines will change.

Major versions of MySQL support different HINT types and have different optimizer decisions. As a result, outlines from MySQL 5.7 may not be optimal and might become invalid in MySQL 8.0. Confirm and verify all outlines after the upgrade to prevent your SQL queries from using unexpected execution plans.
