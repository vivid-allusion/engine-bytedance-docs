---
title: "Recycle Bin"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Recycle_Bin"
---

This topic describes the Recycle Bin feature for tables in RDS for MySQL.

<span id="wjmOQSxN"></span>
## Supported version


* MySQL 8.0 version, and the kernel minor version is MySQL 8.0.32_20250815 and above.

* MySQL 5.7 version, and the kernel minor version is MySQL 5.7.44_20250815 and above.

* MySQL 8.4, with a kernel minor version of MySQL 8.4.7_20260415 or later.


<span id="8TsFSbWz"></span>
## Background

During daily operations, database developers and administrators may accidentally delete tables by executing `DROP` or `TRUNCATE TABLE` commands. Since Data Definition Language (DDL) operations in MySQL do not support rollbacks, such operations may directly cause data loss. Additionally, in some scenarios, after deleting a table, an administrator may be unsure if the data is still needed and may want the deleted table to be temporarily retained, similar to a "recycle bin" mechanism. To address this, RDS for MySQL has introduced the Recycle Bin feature for tables:


* After the table Recycle Bin feature is enabled, tables deleted by a user are automatically moved to the Recycle Bin for temporary storage to prevent direct data loss from accidental deletion.

* Supports querying table information in the Recycle Bin through a dedicated interface to confirm the data state.

* Allows customizing the retention period for tables in the Recycle Bin. After the period expires, the system automatically clears the tables in the background, balancing security and storage space management.


<span id="aj3HSmHB"></span>
## Feature description

The Recycle Bin function includes the ability to recycle and clear tables.

<span id="PpG04nfM"></span>
### Recycle function

When the Recycle Bin feature is enabled, the processing logic for data and table structures is as follows when a user performs different data deletion operations:


1. For `DROP TABLE` / `DROP DATABASE` operations: The corresponding table/database data is not deleted directly. Instead, it is moved to the dedicated schema of the Recycle Bin for temporary storage.

2. For `TRUNCATE TABLE` operations: The system first moves the original table (including its structure and data) to the dedicated schema of the Recycle Bin. Then, it automatically creates a new table with an identical structure in the original location. The new table contains no historical data.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip    </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Only RDS for MySQL instances running MySQL 8.0 support the Recycle Bin feature for <code>TRUNCATE TABLE</code>.   </div>
   

After a table is moved to the recycle bin, the system renames it using the `__<Storage Engine>_<Table ID>` format. The main reason for this naming convention is that a user may create tables with the same name in different schemas. The table ID is globally unique, which prevents table name conflicts in the recycle bin and ensures that each recycled table can be uniquely identified.

In addition, when a table is moved to the recycle bin, the system automatically records its key metadata, including the original schema, original table name, and the time of recycling. This information helps users quickly and accurately associate tables in the recycle bin with their original tables, and all recorded metadata can be queried through the corresponding interface.

<span id="r4QMbGID"></span>
### Cleanup function

The recycle bin feature supports two cleanup methods to meet user garbage collection needs in different scenarios: manual cleanup and automatic cleanup based on the retention period.


* **Manual cleanup**: The recycle bin feature provides a dedicated `dbms` package, allowing users to call the `dbms` interface to trigger a cleanup operation and precisely delete specified table objects in the recycle bin.

* **Automatic cleanup**: Users can enable the automatic cleanup feature as needed and preset the retention period for table objects in the recycle bin. After this feature is enabled, the system starts an asynchronous background thread to continuously detect and automatically clean up table objects that exceed the set retention period, without requiring manual intervention.


<span id="zKzi15xt"></span>
## Instructions

<span id="d9gYm4M5"></span>
### Parameter description

RDS for MySQL provides the following parameters to manage the Recycle Bin feature. You can enable, disable, and configure the Recycle Bin feature by modifying these parameters. For detailed information on modifying parameters, please refer to [Modifying parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_parameters).


|**Parameter name** |**Description** |**Effective scope** |**Value range** |**Default value** |
|---|---|---|---|---|
|loose_recycle_bin |Whether to enable the recycle bin feature. |GLOBAL/SESSION |ON/OFF |OFF |
|loose_recycle_scheduler<br><br> |Specifies whether to enable the automatic cleanup feature for the recycle bin. |GLOBAL |ON/OFF |OFF |
|loose_recycle_bin_retention<br><br> |The retention period for recycled data.<br><br> |GLOBAL |1 \- 31536000 (in seconds, up to 365 days) |604800 (7 days) |
|loose_recycle_scheduler_interval |The regular check cycle for automatic cleanup of the recycle bin. |GLOBAL |1\-60 (unit: Second) |30 |


<span id="s9sla4cC"></span>
### Interface description

The Recycle Bin feature in RDS for MySQL also provides the `dbms_recycle` package to query and manage recycle bin features.


* `dbms_recycle.show_tables()`: Views the tables temporarily saved in the recycle bin.

   Examples:

   ```SQL
   mysql> call dbms_recycle.show_tables();
   +-----------------+--------------+---------------+--------------+---------------------+------------+
   | SCHEMA          | TABLE        | ORIGIN_SCHEMA | ORIGIN_TABLE | RECYCLED_TIME       | PURGE_TIME |
   +-----------------+--------------+---------------+--------------+---------------------+------------+
   | __recycle_bin__ | __innodb_19  | db_recycle    | t1           | 2025-08-25 21:22:41 | NULL       |
   | __recycle_bin__ | __innodb_158 | test          | l2           | 2025-08-26 11:35:33 | NULL       |
   | __recycle_bin__ | __innodb_116 | test          | t            | 2025-09-06 10:50:50 | NULL       |
   +-----------------+--------------+---------------+--------------+---------------------+------------+
   3 rows in set (0.00 sec)
   ```
   

   The output metrics are described as follows:

   
   |**Parameter** |**Description** |
   |---|---|
   |SCHEMA |The database name of the recycle bin. |
   |TABLE |Name of the table in the recycle bin. |
   |ORIGIN_SCHEMA |Original database name. |
   |ORIGIN_TABLE |Original table name. |
   |RECYCLED_TIME |Recycle time. |
   |PURGE_TIME |The estimated time when the table will be deleted from the Recycle bin. |
   

* `dbms_recycle.purge_table('<TABLE>')`: Manually purges tables from the recycle bin.

   The `<TABLE>` parameter is the value from the `TABLE` column returned by the `dbms_recycle.show_tables()` interface.

   Usage example:

   ```SQL
   call dbms_recycle.purge_table('__innodb_19');
   ```
   

* `dbms_recycle.restore_table('<RECYCLE_TABLE>','<DEST_DB>','<DEST_TABLE>'`: Restores data from the recycle bin to a user SCHEMA.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Running the <code>restore_table</code> command requires the SUPER privilege. Manual execution is not supported.   </div>
   

   ```SQL
   dbms_recycle.restore_table('<RECYCLE_TABLE>','<DEST_DB>','<DEST_TABLE>')
   ```
   

   Parameter description:

   
   |**Parameter** |**Description** |
   |---|---|
   |RECYCLE_TABLE |The name of the table in the Recycle bin to restore.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If only this parameter is provided, the table is restored to the original table.</div><br> |
   |DEST_DB |Target database name. |
   |DEST_TABLE |Target table name. |
   

   Sample:

   ```SQL
   mysql> call dbms_recycle.restore_table('__innodb_19','DB','Table');
   ```
   


<span id="FJQbrudr"></span>
### Examples


* Create a table and insert data:

   ```SQL
   mysql> use test;
   
   mysql> create table t(a int);
   Query OK, 0 rows affected (0.01 sec)
   
   mysql> insert into t values (1), (2), (3);
   Query OK, 3 rows affected (0.00 sec)
   ```
   

* Enable the Recycle Bin feature at the session level and delete the table:

   ```SQL
   mysql> set session loose_recycle_bin = on;
   Query OK, 0 rows affected (0.00 sec)
   
   mysql> drop table t;
   Query OK, 0 rows affected (0.00 sec)
   ```
   

* View the recycle bin by using the API:

   ```SQL
   mysql> call dbms_recycle.show_tables();
   +-----------------+-------------+---------------+--------------+---------------------+------------+
   | SCHEMA          | TABLE       | ORIGIN_SCHEMA | ORIGIN_TABLE | RECYCLED_TIME       | PURGE_TIME |
   +-----------------+-------------+---------------+--------------+---------------------+------------+
   | __recycle_bin__ | __innodb_42 | test          | t            | 2025-09-09 16:18:12 | NULL       |
   +-----------------+-------------+---------------+--------------+---------------------+------------+
   1 row in set (0.00 sec)
   ```
   

* Restore data by using `insert into select`:

   ```SQL
   mysql> create table t(a int);
   Query OK, 0 rows affected (0.00 sec)
   
   mysql> insert into t select * from __recycle_bin__.__innodb_42;
   Query OK, 3 rows affected (0.00 sec)
   Records: 3  Duplicates: 0  Warnings: 0
   
   mysql> select * from t;
   +------+
   | a    |
   +------+
   |    1 |
   |    2 |
   |    3 |
   +------+
   3 rows in set (0.00 sec)
   ```
   

* Manually clear data in the recycle bin through an interface:

   ```SQL
   mysql> call dbms_recycle.purge_table('__innodb_42');
   Query OK, 0 rows affected (0.01 sec)
   
   mysql> call dbms_recycle.show_tables();
   Empty set (0.00 sec)
   ```
   


<span id="pRnB6F5o"></span>
### Precautions

When the RDS for MySQL instance starts, it initializes a database named `__recycle_bin__`**** as a dedicated database for the recycle bin. `__recycle_bin__`**** is a system\-level database that you cannot directly modify or delete.

Although you cannot directly execute the `drop table` statement on tables in the recycle bin, you can use `dbms_recycle.purge_table();` to clear them. The user account is required to have the DROP privilege on both the original table and the recycle bin table.
