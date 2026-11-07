---
title: "Recovering to the source instance from a backup set"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/recovering_to_the_source_instance_from_a_backup_set"
---

This topic describes how to restore data to the source instance from a backup set.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* The data information in the restored instance is consistent with the information in the backup file at that time (does not include structures such as stored procedures and functions).

* During restoration, if a user operates on a database or table that has the same name as a previously renamed one, data conflicts may occur or the restoration may fail.

* The restoration process puts some load on the source instance.

* The backup set selection range is determined by the number of days to retain backup. You can adjust the number of days to retain backup by modifying the data backup policy. For more details, refer to [Modifying backup policy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_data_backup_policies).

* When you create a table with foreign key constraints under the same database with the same name, the table build fails due to the foreign key conflict, and MySQL creates the table with a different foreign key constraint name.

* If the selected database to be recovered is empty, the recovery process will not create an empty bak database for this empty database.

* After the restoration task is submitted, if the task encounters issues in the early stage due to insufficient resources or other exceptions, the system will automatically cancel the restoration task and return detailed failure causes. You can view the specific reason for the task failure in the **Task center**. For more information, refer to [View task](https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_a_task?lang=en).

* The time for data recovery from a backup set is directly proportional to the data volume of the instance.


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
## **Procedure**


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance, then click **Instance List** in the left\-side navigation bar.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project to which the instance belongs is not set, this operation should select the project as <strong>All resources</strong>.   </div>
   

3. On the **Instances** page, click the target instance name.

4. At the top of the page, click the **Backups** tab, and on the **Basic backup list** tab, click **Data recovery**.

5. In the pop\-up **Restore To** dialog box, select **the current instance** card and click **OK**.

6. On the **Restore to current instance** page, set the following parameters and click **Next step**.

   * Restore method: Select **By backup set**.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Physical backups can only restore to the original instance.      </div>
      

   * Backup set: Select a backup set to restore from the drop\-down list.

   * Select the recovery mode. You can select **Normal** or **Fast** mode.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">After enabling the fast recovery mode, the system will optimize and accelerate eligible recovery tasks to improve overall recovery efficiency. If the task does not support the fast recovery mode, the system will automatically switch to the normal recovery mode to continue the task.      </div>
      

   * Select databases and tables: Select the databases and tables to restore.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The databases and tables information is based on the current actual database and table records.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Up to 5,000 databases are displayed for each expanded instance, and up to 5,000 tables are displayed for each expanded database.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Search libraries or tables via regular expressions or fuzzy matching. When searching for libraries and tables at the same time, the search results for the libraries and tables will be output based on "and logic".      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Whether the entire database or individual data tables are selected is counted as one selection. The upper limit of selections per instance is 500. The maximum number of tables that can be restored for a single instance is 50,000.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Physical backups can only restore to the original instance.      </div>
      

8. Set up the rollback configuration and set the names for the restored databases and tables. After the settings are completed, click **OK**, and then click **OK** in the pop\-up dialog box.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">By default, it is named with original <strong>name_timestamp</strong>. Batch adjustment is supported to add a prefix, suffix, or both to the original names. The database and table name must <strong>start with a letter, end with a letter or number, and not be the same as the original database and table name</strong>.   </div>
   

<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[RestoreToExistedInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/restoretoexistedinstance) |Call the RestoreToExistedInstance API to restore data to an existing database instance. |
