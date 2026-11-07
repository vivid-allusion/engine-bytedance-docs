---
title: "Rolling back database and table data"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/roll-back-data"
---

Document Database for MongoDB supports rollback of database and table data. When you accidentally delete a collection or document, you can use the rollback function to specify one or more databases or tables that need to be restored, quickly restoring the data to the original instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite


* The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).

* The instance database to be rolled back must contain at least one database or table.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* A maximum of 50 instances can be selected for batch rollback at one time.

* A single instance can select a maximum of 1,000 tables for rollback at a time.

* Rolling back time series collections is not supported, therefore they will not be displayed in the list of selectable database and table objects.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Currently, only the recovery of selected database and table objects is supported. During recovery, the original database and table will not be directly overwritten; instead, a new rollback table will be created under the database where the table needs to be recovered. For example, if the source table is `test`, a new rollback table named `test_bak_backup_timestamp` will be created during rollback.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, select the instances to be rolled back, then click **Rollback** at the bottom of the list.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Multiple instances can be selected for batch rollback, with a maximum of 50 instances selectable simultaneously.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can select instances of different versions for batch rollback, such as MongoDB 5.0 and MongoDB 6.0 instances.   </div>
   

5. Perform the following operations on the **Create rollback task** page.

   
   |Operation |Description |
   |---|---|
   |Select databases and tables |Select the objects to be rolled back. The specific steps are as follows:<br><br><br>1. In the **All instances' databases and tables** area, check the objects to be rolled back, or you can check all databases and tables.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The databases and tables information is based on the current actual database and table records. Up to 5,000 databases are displayed for each expanded instance, and up to 5,000 tables are displayed for each expanded database.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can search by database name or table name in the search bar of the <strong>All instances' databases and tables</strong> area. Fuzzy matching is supported for searching databases or tables. When searching for both databases and tables simultaneously, the relationship between database and table search conditions is <strong>AND</strong>.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Search results display a maximum of 5,000 entries. If the data volume is too large, it is recommended to refine the search conditions.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Instances without any databases or tables are grayed out by default and cannot be selected for rollback.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The total number of selected tables in a single instance cannot exceed 1000.   </div><br>   <br><br>2. In the **Instance database and tables** selected area, confirm the objects to be rolled back.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Whether you select the entire database or a specific table, it is counted as one selection. Up to 1000 tables can be restored for a single instance.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the selected instance does not contain any databases or tables, it will be automatically ignored, and the restoration task will not be executed.   </div><br>   <br><br>3. Click **Next step** at the bottom right corner of the page. |
   |Set rollback configuration |Set the rollback time for the selected databases and tables. You can choose to set the rollback time for all database tables in batches or set the rollback time for each instance separately according to your business needs. Among them:<br><br><br>* Set the rollback time for all instances in batches: In the time selection window after **Batch set rollback time**, select the rollback date and time for all instances in batches.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The default batch rollback time is the current time.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Different instances support different rollback times. When batch setting the rollback time, the selectable time range is the intersection of the rollback time ranges supported by all instances.   </div><br>   <br><br>* Set the rollback time for each instance separately: Find the target instance in the **Instance database & tables selected** list, and in the time selection window of **Set rollback time** on the right, set the rollback time for the specified instance. After setting, the rollback time of all database tables within the same instance will be the same.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The instance's default rollback time is consistent with the batch\-set rollback time.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Each instance's rollback time range is automatically calculated based on instance backups and oplog logs.   </div><br>    |
   

6. Click **OK** in the lower\-right corner of the page.

7. In the pop\-up dialog box, click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After clicking <strong>OK</strong>, the rollback task will be created and executed immediately, and the console will display the <strong>Batch tasks have been initiated</strong> dialog box. It displays information such as the quantity and progress of this rollback task, along with the instance name, ID, and submission result of the instances requiring the rollback task.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the <strong>Batch tasks have been initiated</strong> dialog box, click the <strong>Terminate</strong> button. After termination, the tasks of the instances that have not started the roallback will no longer be executed and cannot be restored. If you want to roll back again, you need to initiate a new batch rollback task.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the tasks of some instances fail, place the cursor on <strong>Failed</strong> in <strong>Execution result</strong> column of the target instance to view the reason for the failure. You can also click <strong>Retry</strong> in the <strong>Actions</strong> column of the target instance to re\-execute the task; or click <strong>Batch retry</strong> to retry all the failed tasks.   </div>
   


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations


* You can also click **Go to task page** in the **Batch tasks have been initiated** dialog box to enter the MongoDB **Batch rollback** page, where you can manage the initiated database and table rollback tasks, such as viewing or modifying the table names of the rollback tables. For more details, refer to [Managing database and table rollback tasks](https://docs.byteplus.com/en/docs/mongodb/manage-rollback-task).

* On the MongoDB **Batch rollback** page, you can view the progress of database and table rollback tasks. When the progress displays as 100%, the instance status will also change to **Running**, and you can then connect to the instance and log in to the database to verify if the data rollback was successful. For specific procedures, refer to [Connecting to instance via Mongo shell](https://docs.byteplus.com/en/docs/mongodb/connect-instance-via-mongo-shell).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the rollback task is in progress, the instance status changes to <strong>Restoring</strong>, indicating that the data is being restored. The time required for rolling back database and table data depends on various factors such as data volume, task queue, and network. Wait patiently.   </div>
