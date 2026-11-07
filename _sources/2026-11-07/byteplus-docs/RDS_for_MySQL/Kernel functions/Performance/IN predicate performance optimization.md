---
title: "IN predicate performance optimization"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/IN_predicate_performance_optimization"
---

This topic describes the IN predicate performance optimization feature of RDS for MySQL.

<span id="KOh6ffmI"></span>
## Supported version


* MySQL 5.7 version, and the kernel minor version is MySQL 5.7.44_20250815 and above.

* MySQL 8.0 version, and the kernel minor version is MySQL 8.0.32_20250815 and above.

* MySQL 8.4, with a kernel minor version of MySQL 8.4.7_20260415 or later.


<span id="R6oCZOYR"></span>
## Background

When an equality check is used in a query condition (WHERE or JOIN clause), an index can quickly locate data, which avoids a full table scan and reduces overhead. The performance improvement from an index scan is especially significant for tables with many rows.

When an IN predicate appears in a query condition (WHERE or JOIN clause), an index can also be used for quick lookups to avoid a full table scan and reduce overhead. This is because an IN predicate can be broken down into multiple equality conditions connected by logical ORs.

In the implementation of MySQL Community Edition, a longer IN predicate list requires the optimizer to record more information when generating an index scan plan, which in turn consumes more memory. To control memory usage, MySQL sets a threshold controlled by the `range_optimizer_max_mem_size` parameter. If creating an index scan plan requires more memory than this threshold, the optimizer will stop and use a full table scan plan instead. When the IN predicate list is long, the optimizer's memory usage may exceed the threshold, causing it to select a less performant full table scan.

<span id="jdFdEaK2"></span>
## Feature description

The IN predicate performance optimization feature rewrites queries with IN predicates during the optimization phase, eliminating the predicate and replacing it with a JOIN on a temporary table. For example, consider the following query with an IN predicate:

```SQL
SELECT * FROM sbtest1 WHERE k IN (0, 1, 2);
```


It can be rewritten as:

```SQL
SELECT sbtest1.* FROM sbtest1 SEMI JOIN tmp_table ON (sbtest1.k = tmp_table.column_0);
```


The table `tmp_table` contains three rows and one column of data, (0), (1), and (2), which correspond to the data in the IN predicate list before the rewrite.

The advantages of this rewrite are:


* If the IN predicate before the rewrite can use an index on the `sbtest1` table to quickly find the required data, the rewritten SEMI JOIN can also use the same index on the `sbtest1` table to do so.

* Before the rewrite, if the IN predicate list is too long, the optimizer may choose a less performant full table scan for `sbtest1` to avoid using too much memory. The rewritten SEMI JOIN eliminates concerns about excessive memory usage because all data from the IN predicate list is placed in a temporary table. This table is initially stored in memory and automatically switches to disk storage if memory usage becomes too high. Therefore, regardless of the original length of the IN predicate list, the rewritten SEMI JOIN can always use the index on the `sbtest1` table to quickly locate the required data.


<span id="doMy8v9P"></span>
## Instructions

<span id="3MultCG1"></span>
### Parameter description

This feature adds two new parameters, `loose_enable_in_list_optimization` and `loose_in_list_optimization_threshold`, to control when to rewrite. The descriptions of these two parameters are as follows:


|Parameter name |Default value |Does it need instance restart to take effect? |Value range |Scope |Parameter description |
|---|---|---|---|---|---|
|loose_enable_in_list_optimization |OFF |No |OFF \| ON \| AUTO |Global, Session |Controls the behavior of the IN predicate optimization feature:<br><br><br>* When set to `OFF`, IN predicate rewriting is never performed.<br><br>* When set to `ON`, the IN predicate is rewritten when its list length reaches the threshold defined by the `loose_in_list_optimization_threshold` parameter.<br><br>* When set to `AUTO`, MySQL determines whether to perform the rewrite based on a comprehensive performance comparison. |
|loose_in_list_optimization_threshold |32768 |No |[1, 4294967295] |Global, Session |When `loose_enable_in_list_optimization` is set to `ON`, this parameter controls the rewrite threshold. The rewrite occurs when the length of the IN predicate list reaches the value of this parameter. |


To enable this feature, we recommend setting `loose_enable_in_list_optimization` to `AUTO`. When a query contains an IN predicate, the feature automatically determines whether to rewrite based on a comprehensive performance evaluation before and after the rewrite. For detailed information on modifying parameters, please refer to [Modifying parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_parameters).

<span id="KZ0sy5O0"></span>
### Examples


* Set parameters to enable this feature.

   * Set `loose_enable_in_list_optimization` to `AUTO` to let MySQL automatically decide when to rewrite:

      ```SQL
      mysql> SET loose_enable_in_list_optimization = AUTO;
      Query OK, 0 rows affected (0.00 sec)
      ```
      

   * Or, set `loose_enable_in_list_optimization` to `ON` and also set `loose_in_list_optimization_threshold`, which rewrites all IN predicates with a length that reaches the ` loose_in_list_optimization_threshold` value:

      ```SQL
      -- Rewrite all IN predicates with a length of 10 or greater.
      mysql> SET loose_enable_in_list_optimization = ON;
      Query OK, 0 rows affected (0.00 sec)
      
      mysql> SET loose_in_list_optimization_threshold = 10;
      Query OK, 0 rows affected (0.00 sec)
      ```
      

* Use the EXPLAIN statement to check whether the query is rewritten:

   ```SQL
   -- Rewrite all IN predicates with a length of 10 or greater.
   mysql> SET loose_enable_in_list_optimization = ON;
   Query OK, 0 rows affected (0.00 sec)
   
   mysql> SET loose_in_list_optimization_threshold = 10;
   Query OK, 0 rows affected (0.00 sec)
   
   -- The length of the IN predicate list is 9. It is not rewritten.
   mysql> EXPLAIN SELECT * FROM sbtest1 WHERE k IN (0, 1, 2, 3, 4, 5, 6, 7, 8);
   +----+-------------+---------+------------+------+---------------+------+---------+------+------+----------+-------------+
   | id | select_type | table   | partitions | type | possible_keys | key  | key_len | ref  | rows | filtered | Extra       |
   +----+-------------+---------+------------+------+---------------+------+---------+------+------+----------+-------------+
   |  1 | SIMPLE      | sbtest1 | NULL       | ALL  | k_1           | NULL | NULL    | NULL |    1 |   100.00 | Using where |
   +----+-------------+---------+------------+------+---------------+------+---------+------+------+----------+-------------+
   1 row in set, 1 warning (0.00 sec)
   
   -- The length of the IN predicate list is 10. It is rewritten.
   mysql> EXPLAIN SELECT * FROM sbtest1 WHERE k IN (0, 1, 2, 3, 4, 5, 6, 7, 8, 9);
   +----+-------------+------------+------------+------+---------------+-------------+---------+-----------------+------+----------+---------------------------------------------------------------------+
   | id | select_type | table      | partitions | type | possible_keys | key         | key_len | ref             | rows | filtered | Extra                                                               |
   +----+-------------+------------+------------+------+---------------+-------------+---------+-----------------+------+----------+---------------------------------------------------------------------+
   |  1 | PRIMARY     | sbtest1    | NULL       | ALL  | k_1           | NULL        | NULL    | NULL            |    1 |   100.00 | NULL                                                                |
   |  1 | PRIMARY     | <derived2> | NULL       | ref  | <auto_key0>   | <auto_key0> | 8       | mysql.sbtest1.k |    2 |   100.00 | Using where; IN-list optimization; Using index; FirstMatch(sbtest1) |
   |  2 | SUBQUERY    | NULL       | NULL       | NULL | NULL          | NULL        | NULL    | NULL            | NULL |     NULL | No tables used                                                      |
   +----+-------------+------------+------------+------+---------------+-------------+---------+-----------------+------+----------+---------------------------------------------------------------------+
   3 rows in set, 1 warning (0.00 sec)
   ```
   


When the IN predicate is rewritten, the Extra column in the EXPLAIN output displays `IN-list optimization`.

<span id="9ZUuiBm9"></span>
## Precautions

The rewrite for this feature must meet the following conditions:


* The WHERE or JOIN clause of the query contains an IN predicate.

* The IN predicate list contains only constants, and all constants have the same type.

* The IN predicate must be able to use an index.

* If `loose_enable_in_list_optimization` is `ON`, the length of the IN predicate list must be greater than or equal to the value of `loose_in_list_optimization_threshold`. If `loose_enable_in_list_optimization` is `AUTO`, MySQL determines whether to perform the rewrite based on the performance before and after the rewrite.


<span id="uIWSaZNm"></span>
## Performance data

Create a sysbench table `sbtest1` with 20,000,000 rows and run the following query to verify its performance:

```SQL
SELECT * FROM sbtest1 WHERE k IN (...);
```


For MySQL 5.7, the execution times before and after rewriting with different IN predicate lengths are as follows:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dbd751c379beb39e04bfcca1d115950f.png) </span>

For MySQL 8.0, the execution times before and after rewriting with different IN predicate lengths are as follows:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0c0f09e680c3e58a0b278cec5c56bd7b.png) </span>

Based on the preceding performance data, the following conclusions can be drawn:


* When the IN predicate list has 10,000 or fewer items, the original query uses an index scan and performs slightly better than the rewritten SEMI JOIN query. This is because the rewriting itself has some overhead, and it introduces an additional temporary table after rewriting, making the execution plan slightly more complex.

* When the IN predicate list length is 50,000 or more, the original query with the IN predicate performs a full table scan due to memory limitations. In this case, its performance is much worse than the rewritten SEMI JOIN query because the rewritten SEMI JOIN query can use an index to quickly locate the required data in `sbtest1`.


Therefore, when using this feature, we recommend setting `loose_enable_in_list_optimization` to `AUTO`. The feature then automatically decides whether to rewrite queries containing IN predicates based on a comprehensive performance comparison.
