---
title: "Flashback query"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/flashback_query"
---

This topic describes information about the flashback query feature of RDS for MySQL.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

In the process of database operation and maintenance, misoperation may occur, which may have a serious impact on the business. When the business is affected due to misoperation, common recovery methods include backtracking, cloning, etc. However, for a small amount of data changes and emergency fault repair, it is prone to errors and takes a long time, and the recovery time is uncontrollable when the amount of data is large.

RDS for MySQL implements the flashback query feature on the InnoDB engine, enabling you to query historical data from before a misoperation by using simple SQL statements.

<span id=".5Y-C5pWw6K-05piO"></span>
### Parameter description

The use of the flashback query function depends on the configuration of the parameters loose_rds_flashback_query and loose_rds_flashback_query_window, which are as follows:


|**Parameter name** |**Default value** |Does it need instance restart to take effect? |Value range |**Scope** |Parameter description |
|---|---|---|---|---|---|
|loose_rds_flashback_query |OFF |No |[ON\|OFF] |Global |Used to enable or disable InnoDB's flashback query feature. |
|loose_rds_flashback_query_window |900 |No |[1\-604800] |Global |Used to set the time period for which flashback queries are supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The end point of the time range that supports flashback queries can only be the current point in time, i.e. now (). The starting point of the supported flashback query time range is determined by the larger values in "Flashback Query Feature On Time" and "Retention Time":</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The activation time of the flashback query function: the time point when the flashback query function is enabled.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Retention time: current time minus the length of time configured in <code>loose_rds_flashback_query_window</code>, i.e., <code>now() - loose_rds_flashback_query_window</code>).</div><br> |


<span id=".54q25oCB6K-05piO"></span>
### Status description

RDS for MySQL provides the following states to display the current state of the flashback query:


|**Parameter name** |**Scope** |**Description** |
|---|---|---|
|Innodb_flashback_state |Global |Flashback query running status<br><br><br>* `DISABLED_AND_PURGED`: The feature is disabled and the purge of the view record is completed.<br><br>* `ENABLED`: The feature is enabled and running normally.<br><br>* `DISABLED`: The feature is disabled but is still purging remaining view records.<br><br>* `MISSING_META_TABLE`: The feature is enabled, but the metadata table has not been created. |
|Innodb_flashback_state_code |Global |Flashback query running status code<br><br><br>* `0`：DISABLED_AND_PURGED<br><br>* `1`：ENABLED<br><br>* `2`：DISABLED<br><br>* `3`：MISSING_META_TABLE |
|Innodb_flashback_query_views_table_open_count_by_purge_thread |Global |The number of times the InnoDB purge thread opened the metadata table. |
|Innodb_flashback_query_views_table_open_count_by_persist_thread |Global |Number of times the Persist thread opened the metadata table. |
|Innodb_flashback_query_views_table_open_count_by_user_thread |Global |The number of times the User thread opened the metadata table. |
|Innodb_flashback_query_start_time |Global |Flashback query support time starting point. |
|Innodb_flashback_query_end_time |Global |Flashback query support time ending point. |


<span id=".5pSv5oyB54mI5pys"></span>
## Supported version


* MySQL 8.0 version, and the kernel minor version is MySQL 8.0.32 _20250215 and above.

* MySQL 5.7 version, and the kernel minor version is MySQL 5.7.32 _20250415 and above.

* MySQL 8.4 version, and the kernel minor version is MySQL 8.4.7_20260415 and above.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can view the kernel minor version of an instance by <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_instance_details">Viewing instance information</a>. If the kernel minor version of your instance is not within the supported kernel minor version range, you can <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version">Manually upgrading the instance kernel minor version</a>.</div>


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* If you perform a flashback query before setting the parameter loose_rds_flashback_query to `ON`, the system returns an error `ERROR 1030 (HY000): Got error 216 - 'Option loose_rds_flashback_query is OFF' from storage engine`.

* If history information outside the flashback query time range is queried, the system returns an error `ERROR 1030 (HY000): Got error 215 - 'Read view not found; Timestamp may be too old' from storage engine`.

* Only InnoDB tables are supported. Views, other engines, and functions without corresponding actual columns, such as 1490059, are not supported.

* Flashback queries are only supported at the REPEATABLE READ, READ COMMITTED isolation levels. For more information on isolation levels, see the official MySQL documentation [17.7.2.1 Transaction Isolation Levels](https://dev.mysql.com/doc/refman/8.0/en/innodb-transaction-isolation-levels.html).

* The use of flashback queries in statements of type for update is not supported, and the execution will report an error `ERROR 1030 (HY000): Got error 217 - 'Current transaction isolation level does not support this kind of flashback queries.' from storage engine`.

* create table select and insert into ... select... Flashback queries are only supported at the READ COMMITTED isolation levels. Executing under other isolation levels will result in the error `ERROR 1030 (HY000): Got error 217 - 'Current transaction isolation level does not support this kind of flashback queries.' from storage engine`.

* The supported flashback query is accurate in seconds and is not guaranteed to be 100% accurate in time. If there are multiple changes within a second, any of them may be found.

* If the same flashback query statement specifies different timestamps before and after a table, only the first timestamp can be used, and the rest are ignored.

* After a DDL operation, previous data cannot be queried for flashback. If the data before the DDL query is flashed back, the results may not meet expectations.

* Due to the time difference between the primary node and the read\-only node, if you specify the same time to perform a flashback query, the results obtained from the primary node and the read\-only node may be different. To resolve this inconsistency, the broker distributes the SQL for the flashback query only to the primary node.

* Flashback queries are recommended for single\-table scenarios. Multi\-table flashback queries can lead to query performance degradation, and it is not recommended to use flashback queries in complex query scenarios. Such as JOIN and subquery.

* It is recommended to use the primary key for flashback query, but the performance is poor if the secondary index is used for flashback query.

* Currently, flashback queries must specify a timestamp string, and functions are not supported.

* Undo log cleaning will be delayed after opening the flashback query. In the configured `loose_rds_flashback_query_window` time window, opening the flashback query function will make the Undo tablespace grow, and the query and write performance of the database will decline. It is not recommended to set the `loose_rds_flashback_query_window` too large, it is recommended to configure according to the business traffic situation.

* The range of supported flashback queries can be viewed in the status variables `Innodb_flashback_query_start_time` and `Innodb_flashback_query_end_time` by executing `show status like '%flashback%`. These timestamps have the same time zone as MySQL system_time_zone.

* If you close `loose_rds_flashback_query` and open it later, you will not be able to query the history information before opening `loose_rds_flashback_query`.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance has been created and the state of the instance is **Running**.

* The running value of parameter loose_rds_flashback_query has been set to `ON`. For more information about modifying parameters, see [Modifying parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_parameters).

* Set the running value of the parameter loose_rds_flashback_query_window as needed.


<span id=".5L2_55So6K-05piO"></span>
## Instructions

Flashback query provides a new AS OF syntax. After completing the [Prerequisites](https://docs.byteplus.com/en/docs/RDS_for_MySQL/flashback_query#.5YmN5o-Q5p2h5Lu2), you can use the AS OF syntax to query the data at a specified time.  The AS OF syntax is as follows:

```sql
SELECT column_name_list FROM table_name AS OF TIMESTAMP time_expr alias WHERE...;
```


The parameters involved in the syntax are described as follows:


|**Parameter name** |**Is it required?**  |**Parameter description** |
|---|---|---|
|column_name_list |Yes |The column name of the query. |
|table_name<br><br>table1_name<br><br>table2_name<br><br>table3_name |Yes |Table name. |
|time_expr |Yes |* Flashback timestamp for a time string, accurate to seconds.<br><br>* Format: `YYYY-MM-DD HH-MM-SS`.<br><br>* The use of functions in this parameter is not supported. |
|alias<br><br>alias1<br><br>alias2<br><br>alias3 |No |Alias for the table. |
|join_cond1<br><br>join_cond2 |Yes |JOIN condition. |


<span id=".5L2_55So56S65L6L"></span>
### Examples


* **Query the specified time reference**

   ```sql
   mysql> SET SESSION TRANSACTION ISOLATION LEVEL READ COMMITTED;
   Query OK, 0 rows affected (0.00 sec)
   
   mysql> create table t1(id int,c1 int) engine=innodb;
   Query OK, 0 rows affected (0.00 sec)
   
   mysql> insert into t1 values(1,1),(2,2),(3,3),(4,4);
   Query OK, 4 rows affected (0.00 sec)
   Records: 4  Duplicates: 0  Warnings: 0
   
   mysql> select now();
   +---------------------+
   | now()               |
   +---------------------+
   | 2025-03-18 11:54:55 |
   +---------------------+
   1 row in set (0.00 sec)
   
   mysql> delete from t1 where id=4;
   Query OK, 1 row affected (0.00 sec)
   
   mysql> select * from t1;
   +------+------+
   | id   | c1   |
   +------+------+
   |    1 |    1 |
   |    2 |    2 |
   |    3 |    3 |
   +------+------+
   3 rows in set (0.00 sec)
   
   mysql> select * from t1 as of timestamp '2025-03-18 11:54:55';
   +------+------+
   | id   | c1   |
   +------+------+
   |    1 |    1 |
   |    2 |    2 |
   |    3 |    3 |
   |    4 |    4 |
   +------+------+
   4 rows in set (0.00 sec)
   ```
   

* **Create tables from historical data**

   ```sql
   mysql> create table t3 select * from t1 as of timestamp '2025-03-18 11:54:55';
   Query OK, 4 rows affected (6.39 sec)
   Records: 4  Duplicates: 0  Warnings: 0
   
   mysql> select * from t3;
   +------+------+
   | id   | c1   |
   +------+------+
   |    1 |    1 |
   |    2 |    2 |
   |    3 |    3 |
   |    4 |    4 |
   +------+------+
   4 rows in set (0.00 sec)
   ```
   

* **Insert historical data into the table**

   ```sql
   mysql> create table t4 like t1;
   Query OK, 0 rows affected (0.00 sec)
   
   mysql> insert into t4 select * from t1 as of timestamp '2025-03-18 11:54:55';
   Query OK, 4 rows affected (0.09 sec)
   Records: 4  Duplicates: 0  Warnings: 0
   
   mysql> select * from t4;
   +------+------+
   | id   | c1   |
   +------+------+
   |    1 |    1 |
   |    2 |    2 |
   |    3 |    3 |
   |    4 |    4 |
   +------+------+
   4 rows in set (0.00 sec)
   ```
