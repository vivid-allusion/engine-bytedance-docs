---
title: "Modifying basic backup policies"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_basic_backup_policies"
---

NDB for MySQL instances support automatic backup. The system will perform data backup regularly according to the preset backup strategy. You can customize the backup strategy based on your business needs. This article describes the steps for customizing a backup policy.

<span id="前提条件"></span>
## Prerequisites

The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://www.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance).

<span id="注意事项"></span>
## Precautions


* We recommend you avoid peak business hours when performing backup.

* When batch modifying the data backup policy in batches, make sure that all instances have the same requirements for the data backup policy.

* A single support for selecting up to 100 instances to modify the backup policy in batches.


<span id="为单个实例设置备份策略"></span>
## Set a backup policy for a single instance


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click the **Backups** tab.

5. In the **Backup policy** subtab, click **Editor** after the **Basic backup policy** and set the following parameters in the dialog box that pops up.

   
   |Parameter |Description |
   |---|---|
   |Snapshot backup retention period |The retention duration of backup files after instance release. The value range is 7 days to 365 days, and the default is 7 days. |
   |Snapshot backup window |The time window for performing **full backup** is 2 hours. The backup task is executed at a random time period within this window.<br><br>By default, three days (At least one day apart) are randomly selected in each week, and the backup task is executed in the same time period of these three days, such as Monday, Wednesday, and Friday from 02:00 to 04:00 every week. |
   |Snapshot backup cycle |The frequency of performing full backup is set by default to randomly select three days (At least one day apart) every week to perform backup, such as Tuesday, Thursday, and Saturday. You can customize other times, but at least two days a week must be selected for full backup. |
   

6. Click **OK**.


<span id="批量设置备份策略"></span>
## Set backup policies in batches


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instance list** page, select multiple target instances.

4. Select **Instance list** at the bottom of the page  **...**  \> **Modify backup policy**.

5. In the pop\-up **Batch backup settings** control panel, confirm the original backup policy information for all instances and reset the following parameters.

   
   |Parameter |Description |
   |---|---|
   |Snapshot backup retention period |The retention duration of backup files after instance release. The value range is 7 days to 365 days, and the default is 7 days. |
   |Snapshot backup window |The time window for performing **full backup** is 2 hours. The backup task is executed at a random time period within this window.<br><br>By default, three days (At least one day apart) are randomly selected in each week, and the backup task is executed in the same time period of these three days, such as Monday, Wednesday, and Friday from 02:00 to 04:00 every week. |
   |Snapshot backup cycle |The frequency of performing full backup is set by default to randomly select three days (At least one day apart) every week to perform backup, such as Tuesday, Thursday, and Saturday. You can customize other times, but at least two days a week must be selected for full backup. |
   

6. Click **OK**.

7. In the pop\-up **Batch tasks have been initiated** dialog box, view **Task progress**, and click **OK** after a task is completed.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can click the <strong>Terminate</strong> button in the <strong>Batch tasks have been initiated</strong> dialog box. After termination, tasks for instances that have not started changes will no longer be performed and cannot be resumed. If you want to make changes again, you need to re\-initiate the batch task.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the task execution fails, place the cursor on <strong>Failure</strong> in the <strong>Execution result</strong> column to view the failure reason. You can also click the target instance <strong>Actions</strong> column to <strong>Retry</strong> the task, or click <strong>Batch retry</strong> to retry all failed tasks.   </div>
   


<span id="相关-api"></span>
## Related APIs


|API |Description |
|---|---|
|[DescribeBackupPolicy](https://www.byteplus.com/en/docs/NDB_for_MySQL/DescribeBackupPolicy) |Call the DescribeBackupPolicy to query the instance data backup policy. |
|[ModifyBackupPolicy](https://www.byteplus.com/en/docs/NDB_for_MySQL/ModifyBackupPolicy) |Call the ModifyBackupPolicy to modify the data backup policy of the instance. |
