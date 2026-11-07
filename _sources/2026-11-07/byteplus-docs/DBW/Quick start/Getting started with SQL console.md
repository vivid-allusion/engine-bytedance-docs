---
title: "Getting started with SQL console"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/implementing-the-whole-table-lifecycle-via-the-data-interaction-platform"
---

This topic uses RDS for MySQL as an example to demonstrate how to implement ** ** the full lifecycle of a table \- including creating, viewing, and modifying table data \- through command execution on the DBW's data interaction platform.

<span id="prerequisites"></span>
## Prerequisites

An RDS for MySQL instance is created, and a database account is created. For more information, refer to [Creating RDS for MySQL instances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1) and [Creating an account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_databases_and_accounts).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip</div>


<div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The account you create must be granted the required permissions, for example, for querying and modifying the specified database.</div>


<span id="procedure"></span>
## **Procedure**

The following procedure describes how to implement the full lifecycle of a table, for example, Table ** ** **`table`** ** ** in Database ** ** **`test`**, by executing commands on the data interaction platform.


1. Log on to the [data interaction platform for RDS for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql).

2. On the **SQL query_0** tab, type the following commands and click **Execution** to switch to the target database:

   ```sql
   use test;
   ```
   

3. On the **SQL query_0** tab, type the following commands and click **Execution ** to create a table:

   ```sql
   CREATE TABLE `table` (
     `opid` INT(11) NOT NULL AUTO_INCREMENT COMMENT 'Primary key',
     `opcode` VARCHAR(20) NOT NULL COMMENT 'Permission value',
     `opname` VARCHAR(50) NOT NULL COMMENT 'Permission name',
     `ophref` VARCHAR(200) DEFAULT NULL COMMENT 'Permission operation link',
     `opseq` INT(11) NOT NULL DEFAULT '1' COMMENT 'Display order',
     PRIMARY KEY (`opid`),
     KEY `op_code_index` (`opcode`) USING BTREE,
     KEY `op_name_index` (`opname`) USING BTREE
   ) ENGINE=INNODB AUTO_INCREMENT=139 DEFAULT CHARSET=utf8 COMMENT='Permission information table';
   ```
   

4. On the **SQL query_0** tab, type the following commands and click **Execution ** to add table data:

   ```sql
   INSERT INTO `table` VALUES ('87', '01', 'Permission management', '/admin/auth', '1');
   INSERT INTO `table` VALUES ('88', '02', 'Technological integration', '/admin/tech', '1');
   INSERT INTO `table` VALUES ('89', '03', 'Log management', '/admin/log', '1');
   INSERT INTO `table` VALUES ('90', '0101', 'Querying user lists', '/admin/user/queryPage', '1');
   INSERT INTO `table` VALUES ('91', '010102', 'Updating the user page', '/admin/user/updatePage/{id}', '1');
   INSERT INTO `table` VALUES ('92', '010206', 'Permissions granted to roles', '/admin/role/hasOpers/{roleid}', '1');
   INSERT INTO `table` VALUES ('93', '010102', 'Modifying a user', '/admin/user/update', '1');
   INSERT INTO `table` VALUES ('94', '0103', 'Querying permission lists', '/admin/oper/queryPage', '1');
   ```
   

5. On the **SQL query_0** tab, type the following commands and click **Execution ** to add data:

   * Add an index.

      ```sql
      ALTER TABLE
        `test`.`table` ADD INDEX `op_href_index` (`ophref`) USING BTREE;
      ```
      

   * Add a foreign key.

      ```sql
      ALTER TABLE
        `test`.`table` ADD CONSTRAINT `op_code` FOREIGN KEY (`opcode`) REFERENCES `test`.`table1` (`opcode`) ON DELETE RESTRICT ON UPDATE RESTRICT;
      ```
      

   * Add a column.

      ```sql
      ALTER TABLE
        `test`.`table`
      ADD COLUMN
        `oplong` varchar(30) NULL;
      ```
      

6. On the **SQL query_0** tab, type the following commands and click **Execution ** to modify data:

   * Change the table name from `table` to `table2`.

      ```sql
      ALTER TABLE
        `test`.`table` RENAME `table2`;
      ```
      

   * Change the type of Column `opname` to `VARCHAR(20)`.

      ```sql
      ALTER TABLE
        `test`.`table` MODIFY COLUMN `opname` VARCHAR(20) NOT NULL COMMENT 'Permission name';
      ```
      

   * Change the index name from `eee` to `ddd`.

      ```sql
      ALTER TABLE
        `test`.`table`
      DROP
        INDEX `eee`,
        ADD UNIQUE INDEX `ddd` (`opid`) USING BTREE;
      ```
      

7. On the **SQL query_0** tab, type the following commands and click **Execution ** to query a table:

   ```sql
   select * from `table`;
   ```
   

8. On the **SQL query_0** tab, type the following commands and click **Execution ** to delete table data:

   * Delete Column `opseq`.

      ```sql
      ALTER TABLE
        `test`.`table`
      DROP COLUMN
        `opseq`;
      ```
      

   * Delete Index `op_code_index`.

      ```sql
      ALTER TABLE
        `test`.`table`
      DROP
        INDEX `op_code_index`;
      ```
      

   * Delete Table `table`.

      ```sql
      DROP TABLE `table`;
      ```
      


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can visually manage the full lifecycle of a table on the data interaction platform of DBW. For more information, refer to <a href="https://docs.byteplus.com/en/docs/DBW/table-management-for-mysql">Table management</a>.</div>


<span id="relevant-apis"></span>
## Relevant APIs


|**API** |**Description** |
|---|---|
|[DataConnectInstance](https://docs.byteplus.com/en/docs/DBW/dataconnectinstance) |Call the DataConnectInstance to connect to an instance. |
|[DataExecCommands](https://docs.byteplus.com/en/docs/DBW/dataexeccommands) |Call the DataExecCommands to execute command statements. |
|[DataSessionKeepAlive](https://docs.byteplus.com/en/docs/DBW/datasessionkeepalive) |Call the DataSessionKeepAlive to keep an SQL session alive. |
|[DataCloseSession](https://docs.byteplus.com/en/docs/DBW/dataclosesession) |Call the DataCloseSession to close an SQL session. |
|[DataCancelExec](https://docs.byteplus.com/en/docs/DBW/datacancelexec) |Call the DataCancelExec to cancel the execution of an SQL command.. |
