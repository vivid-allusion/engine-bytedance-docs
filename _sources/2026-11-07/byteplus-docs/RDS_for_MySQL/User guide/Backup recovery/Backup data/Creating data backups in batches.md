---
title: "Creating data backups in batches"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_backups_in_batches"
---

RDS for MySQL supports creating manual backups for batch instances. This topic introduces the operation steps for creating manual backups in batches.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Only full physical backups and full database logical backups are supported for batch instances. To create a logical backup of specified databases and tables, you can only do it instance by instance. For more information about creating a logical backup of specified databases and tables, see [Creating a data backup manually](https://docs.byteplus.com/en/docs/RDS_for_MySQL/manually_creating_a_data_backup).

* A maximum of 10 instances can be supported to create data backups at a time.

* Creating data backups for cloud disk instances and local disk instances at the same time is not supported.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The instances have been created and are in the **Running** status. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project to which the instance belongs is not set, this operation should select the project as <strong>All resources</strong>.   </div>
   

3. On the **Instances** page, select multiple target instances.

4. In the lower\-left corner of the **Instances** page, choose  **...**  \> **Manual backup**.

5. On the popped\-up **Manul backup** page, after completing the configuration of **Backup type** and **Backup method**, click **OK**.

   
   |Configuration items |Description |
   |---|---|
   |Backup type |The supported backup types vary depending on the instances' storage type:<br><br><br>* If the instance's storage type is local disk, you can choose **Physical backup** or **Logical Backup**.<br><br>* If the instance's storage type is cloud disk, you can choose **Snapshot backup**. |
   |Backup method |If the backup type is **Physical backup** or **Snapshot backup**, the backup method can only be **Full backup**.<br><br>If the backup type is selected as **Logical backup**, the backup method can only be **Full database backup**. |
   

6. You can view the **Task progress** in the popped\-up **Batch tasks have been initiated** dialog box. After the task is completed, click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can click the <strong>Terminate</strong> button in the <strong>Batch tasks have been initiated</strong> dialog box to terminate tasks that have not started. After termination, tasks that have not started will no longer be performed and cannot be resumed. If you need to execute the task again, you need to initiate it again.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the task execution fails, move the cursor to <strong>Failure</strong> in the <strong>Execution result</strong> column to view the failure reason. You can click the <strong>Retry</strong> button in the <strong>Operation</strong> column of the corresponding task to try to re\-execute the task.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If multiple tasks fail, you can click the <strong>Batch retry</strong> button in the <strong>Batch tasks have been initiated</strong> dialog box to try to retry all failed tasks.   </div>
