---
title: "Batch rollback"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/batch_rollback"
---

This topic describes the notes, limitations, and operation steps for rolling back instances in the RDS for MySQL console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A BytePlus account has been registered and completed verification. For the detailed method, refer to [Sign Up and Verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* As per the regulations in the Chinese mainland, you must have completed real name registration before you can activate and use cloud services on regions in the Chinese mainland through BytePlus. For more details, refer to [Real name registration](https://docs.byteplus.com/en/docs/byteplus-platform/docs-real-name-registration).

* VPC service access authorization has been completed. For the authorization method, refer to [Cross-service access authorization](https://docs.byteplus.com/en/docs/RDS_for_MySQL/cross-service_access_authorization).

* An instance has been created. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The rollback feature is associated with the backup cycle and the number of days to retain backups in the automatic backup settings. It provides rollbacks based on data backups and log backups (binlog) within the retention period. To ensure data security, the backup cycle for automatic backups must be set to at least twice a week.

* If the database and table that must be rolled back do not exist or are deleted by mistake, you should first log in to the database and create the database and table, and then use the console for rollback.

* If the table is not available in the cold backup before the rollback, disaster recovery will fail.

* When you create a table with foreign key constraints under the same database with the same name, the table build fails due to the foreign key conflict, and MySQL creates the table with a different foreign key constraint name.

* If the selected database to be recovered is empty, the recovery process will not create an empty bak database for this empty database.

* The time for data recovery from a backup set is directly proportional to the data volume of the instance.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limitation


* Currently, rollback is supported only for primary nodes, not for read\-only nodes and standby nodes.

* Currently, only specified databases and tables can be rolled back, and the rolled\-back databases and tables will be written back to the original instance.

* In a batch rollback, up to 10 instances can be selected.

* When using batch rollback for database and table\-level recovery, you can select up to 500 databases or data tables in a single instance. The number of tables cannot exceed 50,000.

* In the following scenarios, the fast recovery mode will fail, and the system will switch to the normal mode for restoration.

   * After a full or incremental physical backup, the fast recovery mode fails if a DDL statement is executed on databases and tables without first running a USE statement.

   * The fast recovery mode fails when restoring a table that was renamed after a full or incremental physical backup.

   * After a full or incremental physical backup, the fast recovery mode will fail if a table is renamed, a DML operation is performed on the table, and the table is then renamed back to its original name.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Click **Instances** in the left\-side navigation bar.

4. On the **Instances** page, select the target instances and click  **...**  in the lower\-left corner \> **Rollback**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the verification of any instance fails at the time of batch rollback, no instances will be submitted.   </div>
   

5. Set the relevant parameters on the **Create rollback task** page, as shown below.

   1. Select the recovery mode. You can select **Normal** or **Fast** mode.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">After enabling the fast recovery mode, the system will optimize and accelerate eligible recovery tasks to improve overall recovery efficiency. If the task does not support the fast recovery mode, the system will automatically switch to the normal recovery mode to continue the task.      </div>
      

   2. Select the databases and tables to roll back. Once you have made your selections, click **Next step**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The source of database table information is the current actual database table record of the database, and missing database table information can be entered manually. The steps for manual entry are as follows:      </div>
      

         1. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">On the <strong>Create rollback task</strong> page, click <strong>Manual entry</strong>.      </div>
      

         2. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">In the drop\-down list in the <strong>Manual entry</strong> window, select instances.      </div>
      

         3. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">In the <strong>Enter databases and tables</strong> text box, enter the databases and tables to roll back. You can enter up to 500 databases and tables separated by line breaks. You can also click <strong>Batch enter database and table names</strong> in the <strong>Manual entry</strong> window, and enter the names in batches in the <strong>Batch enter database and table names</strong> window, separated by commas (,), semicolons (;), or Enter.      </div>
      

         4. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Click <strong>OK</strong>.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Up to 5,000 databases are displayed for each expanded instance, and up to 5,000 tables are displayed for each expanded database.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Search libraries or tables via regular expressions or fuzzy matching. When searching for libraries and tables at the same time, the search results for the libraries and tables will be output based on "and logic".      </div>
      

   3. Set up the rollback configuration, and specify the rollback time and names for the databases and tables. After the settings are completed, click **OK**, and then click **OK** in the pop\-up dialog box to submit the rollback task.

      * **Set backtime for instances in turn**: You can set different backtime for different instances, and the backtime range is automatically calculated based on instance backups and Binlog logs. first.

      * **Batch rollback time**: You can set the rollback time for all instances to be rolled back in batches. Different instances support different rollback times. When setting the batch rollback time, the available time range is the intersection of the rollback time ranges supported by each instance.

      * **Set the restored database and table name**: By default, it is named with "original name_timestamp". Batch adjustment is supported to add a prefix, suffix, or both to the original names. The library table name should meet the principle of "starting with a letter and ending with a letter or number".

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">If the modified name conflicts with the original database, the task will fail.         </div>
         

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can click the <strong>Terminate</strong> button in the <strong>Batch tasks have been initiated</strong> dialog box. After termination, tasks for instances that have not yet started changes will no longer be executed and cannot be recovered. If you want to make changes again, you need to re\-initiate the batch task.</div>


* <div data-tips="true" data-tips-type="tip">If the task execution fails, place the cursor on <strong>Failure</strong> in the <strong>Execution result</strong> column to view the failure reason.</div>
