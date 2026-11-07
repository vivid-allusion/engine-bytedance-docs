---
title: "Recovering database and table by time point"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Recovering_database_and_table_by_time_point"
---

The database and table recovery function allows you to restore an existing backup set or a database and table at any recoverable time point to the original instance without affecting the existing database and table in the original instance. Instead, you can recreate the database and table in the original instance. This article describes how to restore databases and tables by time point.

<span id="前提条件"></span>
## Prerequisites


* The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://www.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance).

* There is a point in time for recovery.


<span id="原理介绍"></span>
## Principle introduction

According to the product architecture design principles, after the database and table recovery operation is completed, the instance may have an unrecoverable period. This is because in order to improve recovery performance, NDB for MySQL writes the final data directly to the storage pool when recovering the database and table, and does not generate redo_log. If the initial version of the newly restored database table is modified before it is backed up, it will be impossible to restore it to the state before the modification, resulting in a permanent unrecoverable period. The specific principle is as follows:


|Write process |Normal write process |Restore database and table writing process |
|---|---|---|
|Example diagram |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_17abddd1e4f637cacb3ed453a751cf65.png) </span> |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_07497d792ab30956285f4c01f1abc5e6.png) </span> |
|Description |VeDB the total data of the database into a plurality of logical files, each modification operation of a logical file is a redo_log, the background from time to time redo_log applied to the logical file, thereby modifying the contents of the logical file, get a checkpoint. The backup process guarantees that all redo_log generated after starting the backup will be backed up, but only certain checkpoints of the logical file can be backed up. When restoring a logical file, select the latest checkpoint before the target time and the full redo_log after the checkpoint and before target\-ts to restore the logical file to the state of the target point.<br><br>As shown in the example diagram, if C1 to C3 are all checkpoints that have been successfully backed up, when you want to restore to target\-ts, you only need to read C2, L4, L5, and then apply L4 and L5 to C2 in turn to get the status of the logical file target\-ts, and then write this version of the logical file directly to the storage cluster. |After the database table is restored, the newly restored table can be written to redo_log. Since the content of the logical file may change at any time due to the application of redo_log, and it takes time to back up the logical file, it is impossible to guarantee the initial state of the logical file. If the initial state of a logical file is modified without being backed up, there will be an unrecoverable interval.<br><br>As shown in the example figure, C1 is the initial data written when the database table is restored, C2, C3 are the checkpoints after applying some redo_log, and L0~ L5 are the redo_log newly written in the foreground after the database table recovery is completed. If C1 is not backed up, only C2 and C3 are backed up, even if both L0 and L1 are backed up, it will never be restored to the state before C2. |


<span id="注意事项"></span>
## Precautions


* When restoring database and table, if the specified database name already exists in the original instance, the database and table recovery will fail.

* Database and table recovery is not allowed during the instance specification changes, restart, delete and other operations.

* During the database and table recovery process, DML operations can always proceed normally.

* If the original instance uses hot and cold separate storage, when restoring data, the hot and cold states of the original table are different, and the state of the target table will also be different after the restoration is complete. For details, see [Backup and recovery](https://www.byteplus.com/en/docs/6357/1231210#%E5%A4%87%E4%BB%BD%E6%81%A2%E5%A4%8D).


<span id="使用限制"></span>
## Limitation


* The total number of entire databases and single tables that can be restored at a time cannot exceed 100. When you choose to restore the entire database, you can restore all tables in the database.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If there are too many tables to restore at one time, it will take a long time for database and table recovery, so it is not recommended to restore too many tables at one time. In this case, it is recommended to restore the entire instance. For specific operation methods, please refer to <a href="https://www.byteplus.com/en/docs/NDB_for_MySQL/Recovering_to_the_new_instance_from_a_backup_set">Recovering to the new instance from a backup set</a> and <a href="https://www.byteplus.com/en/docs/NDB_for_MySQL/Recovering_to_the_new_instance_by_time_point">Recovering to the new instance by time point</a>.   </div>
   

* Only historical database tables can be restored at a point in time after the function is launched.

* When restoring database tables, the total number of data tables at the target time cannot exceed 50,000.

* The database table recovery function does not support the recovery of triggers and foreign keys. If the original table has a Trigger or Foreign Key set, the Trigger or Foreign Key will not be recovered.

* The database and table recovery function is designed for full\-text index scenarios. It supports the recovery of the most common single\-column and compound full\-text indexes, and supports ascending and descending order of multiple columns. Restoring full\-text indexes with index comments, Functional Key Parts, invisible indexes, or other advanced features is not supported. If you restore a special full\-text index, it will degenerate into a full\-text index with only basic features or the restored table will have no index.


<span id="操作步骤"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click the **Backups** tab.

5. On the **Basic backup list** subtab, click **Databases and tables recovery**.

6. On the **Databases and tables recovery** page, set the following parameter items.

   
   |Parameter |Description |
   |---|---|
   |Restore method |Select **By point in time**. |
   |Recovery time point |Select the point in time that needs to be restored. |
   |Restore to |Default to ** Original instance**. |
   |Select databases and tables |1. Select the database and table that needs to be restored in the **All instances' databases and tables** area. There are two scenarios for database table selection:<br><br>   * **All databases and tables**: directly check the target database name, indicating that the data of all tables under the library is restored. The name of the restored table cannot be set and defaults to the original table name. Only the name of the restored database can be set and it cannot be the same as the original database name.<br><br>   * **Partially selected**: Partially selected supports setting the restored database name and table name separately. The restored table name can be the same as the original table name, but the restored database name cannot be the same as the original database name. The following two operation conditions exist for partial selection:<br><br>      * Expand the target database and select some tables.<br><br>      * Expand the target database and manually select all the tables under the database.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can enter the database name or table name in the search bar to search, and fuzzy matching is supported. When searching for a table, you need to first enter the full database name to which the table belongs.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The total number of entire databases and single tables that can be restored at a time cannot exceed 100. When you choose to restore the entire database, you can restore all tables in the database.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The maximum number of databases displayed for each instance is 5,000, and the maximum number of tables displayed after each database is expanded is 5,000.   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the number of databases or tables in the instance exceeds 5,000, select the databases or tables that are not displayed through the search function.   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Checking <strong>All databases and tables</strong> means selecting all displayed databases, with an upper limit of 5,000.   </div><br>   <br><br>2. In the **Selected** area, you can view the selected databases and tables to be restored.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can remove a database or table by clicking the <strong>×</strong> after the database or table has been selected. Or click <strong>Clear with one click</strong> to clear all selected databases & tables.   </div><br>    |
   

7. Click **Next step** to configure the selected database and tables.

   
   |Parameter |Description |
   |---|---|
   |Unrecoverable database table information |Shows whether the selected database and table contains unrecoverable database table information without configuration.<br><br><br>* If the selected database contains irrecoverable tables, these tables will be automatically removed.<br><br>* If there are no recoverable tables in the database, the entire database will be removed for you. |
   |Selected database & table settings |In the **Selected database & table settings** area, set the restored name for the database and table to be restored.<br><br><br>* Single rename<br><br>   In the **Rename** column, set the restored name for the target database or target table respectively. The rules are as follows:<br><br>   * Begin with a lowercase letter and end with a lowercase letter or number.<br><br>   * The length is 2~64 characters.<br><br>   * It must consist of letters, numbers, underscores (_) and hyphens (\-).<br><br>* Batch rename<br><br>   Click **Batch rename** after **Rename** to set prefixes and suffixes for all **database names** or **table names**. The prefix and suffix settings must meet the database and table name rules. For example, if the original database name is `testdb`, the prefix is set to `p_`, and the suffix is set to `_bak`, then the restored library name is `p_testdb_bak`.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When setting the restored database name and table name, please note that the new database name cannot be the same as the original database name, otherwise the database and table recovery operation will fail.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you do not set the name of the restored database and table, <code>_bak</code> is added after the original database and table name by default. For example, if the original table is <code>table</code>, the restored table name is <code>table_bak</code> by default.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can remove a database or table by clicking the <strong>×</strong> after the database or table has been selected.</div><br> |
   

8. Click **OK**.


<span id="相关-api"></span>
## Related APIs


|API |Description |
|---|---|
|[DescribeRecoverableTables](https://www.byteplus.com/en/docs/NDB_for_MySQL/DescribeRecoverableTables) |Call the DescribeRecoverableTables to query the recoverable libraries and tables of the instance. |
|[RestoreTable](https://www.byteplus.com/en/docs/NDB_for_MySQL/RestoreTable) |Call the RestoreTable to restore the historical database and table of the instance to the original instance. |
