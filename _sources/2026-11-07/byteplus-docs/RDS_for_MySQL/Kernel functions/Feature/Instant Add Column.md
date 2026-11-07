---
title: "Instant Add Column"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Instant_Add_Column"
---

This topic describes the feature for adding columns in seconds provided by RDS for MySQL.

<span id="2q4gWW6H"></span>
## Supported version


* MySQL 5.7 version, and the kernel minor version is MySQL 5.7.44_20251015 and above.

* MySQL 8.0 version, all kernel minor versions are supported.

* MySQL 8.4 version, and the kernel minor version is MySQL 8.4.7_20260415 and above.


<span id="RtOCEClv"></span>
## Background

Each row of data in a database is persistently stored on disk. When you perform an ADD COLUMN operation on a table, the data on the disk is also modified accordingly. The time required is proportional to the size of the table. Therefore, performing an ADD COLUMN operation on a large table can take several hours or even days, which causes significant inconvenience for users.

To optimize this behavior, MySQL Community Edition 8.0.12 introduced the INSTANT algorithm. For some ADD COLUMN operations, this algorithm only modifies the table metadata instead of the original user data. This significantly reduces the time required to add columns to large tables and minimizes the impact on the system.

To provide a better experience, RDS for MySQL ported this feature from the community edition of MySQL 8.0 to the MySQL 5.7 version.

<span id="I6P3wVqh"></span>
## Feature description

The Instant Add Column feature of RDS for MySQL optimizes the `ADD COLUMN` operation by changing metadata in the data dictionary. This avoids the modification or rebuilding of the entire table required by traditional DDL operations, allowing the operation to complete in seconds regardless of the table's data volume.

<span id="biKdbsdl"></span>
## Instructions

<span id="lWuSIv0z"></span>
### Parameter description

RDS for MySQL provides the modifiable parameter `loose_innodb_instant_ddl_enabled` for MySQL 5.7 to enable or disable the Instant Add Column feature. In MySQL 8.0 and MySQL 8.4, the Instant Add Column feature is enabled by default and cannot be modified.


|**Parameter name** |**Type** |**Default value** |**Does it need instance restart to take effect?**  |**Value range** |**Scope** |**Parameter description** |
|---|---|---|---|---|---|---|
|loose_innodb_instant_ddl_enabled |bool |OFF |No |[ON\|OFF] |GLOBAL |Specifies whether to enable the second\-level column adding feature. Values:<br><br><br>* ON: enable.<br><br>* OFF: disable. |


<span id="z39gh0Or"></span>
### Examples

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The following describes how to use the Instant Add Column feature in MySQL 5.7. The method for adding columns in seconds in MySQL 8.0 and MySQL 8.4 is the same as that of the community version. For more information, refer to the <a href="https://dev.mysql.com/doc/refman/8.0/en/innodb-online-ddl-operations.html">official MySQL documentation</a>.</div>



1. Modify the loose_innodb_instant_ddl_enabled parameter to ON. For more information about modifying parameters, see [Modifying parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_parameters).

2. Add columns in seconds.

   * Specify ALGORITHM=INSTANT to force adding columns in seconds.


```SQL
ALTER TABLE <table_name> ADD COLUMN <column_name> <data_type> <constraints>, ALGORITHM = INSTANT;
```



   * If ALGORITHM is not specified, RDS for MySQL selects the optimal mode at runtime based on the conditions.


```SQL
ALTER TABLE <table_name> ADD COLUMN <column_name> <data_type> <constraints>;
```



3. View tables with columns added in seconds.


MySQL 5.7 adds the INSTANT_COLS column to INFORMATION_SCHEMA.INNODB_TABLES. This column indicates the number of original columns in a table before an INSTANT DDL operation is executed.

```SQL
SELECT * FROM INFORMATION_SCHEMA.INNODB_SYS_TABLES WHERE INSTANT_COLS > 0;
```



4. View columns added in seconds.


MySQL 5.7 adds the INNODB_SYS_INSTANT_COLUMNS table to the INFORMATION_SCHEMA database. You can use the following SQL statement to view information about columns added by using the add\-columns\-in\-seconds feature.

```SQL
SELECT * FROM INFORMATION_SCHEMA.INNODB_SYS_INSTANT_COLUMNS WHERE TABLE_ID = 
(SELECT TABLE_ID FROM INFORMATION_SCHEMA.INNODB_SYS_TABLES WHERE NAME = "<database_name>/<table_name>");
```


<span id="FpOjg7wZ"></span>
### Precautions

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The following precautions apply when you use the feature of adding columns in seconds in MySQL 5.7 Version. The method for adding columns in seconds in MySQL 8.0 and MySQL 8.4 is the same as that of the community version. For more information, refer to the <a href="https://dev.mysql.com/doc/refman/8.0/en/innodb-online-ddl-operations.html">official MySQL documentation</a>.</div>



* Combining multiple operations is not supported, such as adding an index while adding a column.

* You can only add columns to the end of a table. The `FIRST` or `AFTER` keyword cannot be specified to define the position of the column.

* Compressed tables, tables with full\-text indexes, temporary tables, and partitioned tables are not supported.

* The added column cannot be an auto\-increment column, a primary key, or a virtual column.

* You cannot execute `flush tables xx for export` on a table to which columns have been added in seconds.

* You cannot execute `alter table xx discard tablespace` on a table to which columns have been added in seconds.


<span id="JgRRUQOT"></span>
## Performance data

In a comparative test on a table with a data volume of 10 GiB, enabling the second\-level column adding feature reduced the operation time for adding a column from 50 seconds to less than one second.
