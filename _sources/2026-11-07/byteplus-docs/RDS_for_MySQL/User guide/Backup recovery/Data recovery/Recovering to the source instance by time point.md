---
title: "Recovering to the source instance by time point"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/recovering_to_the_source_instance_by_time_point"
---

This topic describes how to recover data to the source instance by time point.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The data information in the restored instance is consistent with the information in the backup file at that time (does not include structures such as stored procedures and functions).

* Point\-in\-Time Recovery supports second\-level precision for restore time points. During point\-in\-time recovery, the system restores data generated prior to the specified restore time by one second.

   Example: Three records (Data A, Data B, Data C) are inserted at timestamps 2026\-06\-26 15:12:02.999999, 2026\-06\-26 15:12:03.000000 and 2026\-06\-26 15:12:03.000001 respectively. If you set the restore time point to 2026\-06\-26 15:12:03, only Data A will be restored, while Data B and Data C will not be restored.

* During restoration, if a user operates on a database or table that has the same name as a previously renamed one, data conflicts may occur or the restoration may fail.

* The restoration process increases the load on the source instance.

* When you create a table with foreign key constraints under the same database with the same name, the table build fails due to the foreign key conflict, and MySQL creates the table with a different foreign key constraint name.

* If the selected database to be recovered is empty, the recovery process will not create an empty bak database for this empty database.

* After the restoration task is submitted, if the task encounters issues in the early stage due to insufficient resources or other exceptions, the system will automatically cancel the restoration task and return detailed failure causes. You can view the specific reason for the task failure in the **Task center**. For more information, refer to [View task](https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_a_task?lang=en).

* The instance is restored to a point in time through a **Backup set + Binlog logs**. If there is a long interval between the full backup set and the target recovery point‑in‑time, a large number of Binlog logs need to be replayed, resulting in increased recovery duration. Recovery duration cannot be estimated. The actual time is directly proportional to the real‑world data volume.


<span id=".6ZmQ5Yi25LqL6aG5"></span>
## Limits

In the following scenarios, the fast recovery mode will fail and switch to the normal mode to restore.


* After a full or incremental physical backup, the fast recovery mode fails if a DDL statement is executed on databases and tables without first running a USE statement.

* The fast recovery mode fails when restoring a table that was renamed after a full or incremental physical backup.

* After a full or incremental physical backup, the fast recovery mode will fail if a table is renamed, a DML operation is performed on the table, and the table is then renamed back to its original name.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**


* An instance is created and in the **Running** state. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* The source instance must have at least one physical backup.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance, then click **Instance List** in the left\-side navigation bar.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project to which the instance belongs is not set, this operation should select the project as <strong>All resources</strong>.   </div>
   

3. On the **Instances** page, click the target instance name.

4. At the top of the page, click the **Backups** tab, and on the **Basic backup list** tab, click **Data recovery**.

5. In the pop\-up **Restore To** dialog box, select **the current instance card** and click **OK**.

6. On the **Restore to current instance** page, set the following parameters and click **Next step**.

   * Restore method: Select **By point in time**.

   * Select a recovery mode. You can select **Normal** or **Fast** mode.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">After enabling the fast recovery mode, the system will optimize and accelerate eligible recovery tasks to improve overall recovery efficiency. If the task does not support the fast recovery mode, the system will automatically switch to the normal recovery mode to continue the task.      </div>
      

   * Select databases and tables: Select the databases and tables to restore.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The source of database table information is the current actual database table record of the database, and missing database table information can be entered manually.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Up to 5,000 databases are displayed for each expanded instance, and up to 5,000 tables are displayed for each expanded database.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Search libraries or tables via regular expressions or fuzzy matching. When searching for libraries and tables at the same time, the search results for the libraries and tables will be output based on "and logic".      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Whether the entire database or individual data tables are selected is counted as one selection. The upper limit of selections per instance is 500. The maximum number of tables that can be restored for a single instance is 50,000.      </div>
      

   * Manually enter databases and tables (optional): If an instance has no more than 500 selected databases and tables, you can manually enter specific ones for rollback. Ensure the names are correct (case\-sensitive) and exist at the specified time point. Non\-existent entries will be ignored on submission.

      1. In the **Selected** tab, click **Manual entry**.

      2. In the **Manual entry** window, select instances.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">Only the original instance can be selected for restoration.         </div>
         

      3. In the **Enter databases and tables** text box, enter the database and table names. The format for database and table names is `databasename.tablename`. You can enter up to 500 database and table names, separated by line breaks.

      4. (Optional) Click  **+Batch enter database and table names**. In the **Batch input of database names and table names** window, enter the database and table names in batches.

         1. Select the delimiter to use for batch entry.

         2. In the **Database and table names** text box, enter the names for batch entry, and then click **OK**. Separate database and table names with the selected delimiter.

            <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="4">tip            </div>
            

            <div data-tips="true" data-tips-type="tip" data-wrapper-indent="4">Click <strong>Input example</strong> to view examples of batch entry with different separators.            </div>
            

      5. Click **OK**.

7. Specify the **rollback time** and names for the selected **databases and tables**. After the settings are completed, click **OK**, and then click **OK** in the pop\-up dialog box.

   1. **Set rollback time**: the rollback time range is automatically calculated based on instance backup and Binlog logs.

   2. **Set the restored database and table name**: By default, it is named with **original name_timestamp**. Batch adjustment is supported to add a prefix, suffix, or both to the original names. The database and table name must **start with a letter, end with a letter or number, and not be the same as the original database and table name**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[RestoreToExistedInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/restoretoexistedinstance) |Call the RestoreToExistedInstance API to restore data to an existing database instance. |
