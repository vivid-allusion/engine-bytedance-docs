---
title: "Modifying automatic backup policy in batches"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/modifying_automatic_backup_policies_in_batches"
---

Document Database for MongoDB replica set instances support batch modification of automatic backup policies. You can simultaneously modify automatic backup policies for replica set instances with consistent backup requirements, thereby improving instance backup management efficiency. This topic describes how to bulk modify automatic backup settings.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite


* The instance type must be **Replica set**. For specific procedures, refer to [Creating instance](https://docs.byteplus.com/en/docs/mongodb/create-instance).

* The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* A maximum of 100 replica set instances can be selected simultaneously to batch modify the backup policy.

* When batch modifying the backup policy, the database versions of the replica set instances can be different. For example, you can simultaneously modify the backup policies of MongoDB 5.0 and MongoDB 6.0 replica set instances.

* By default, MongoDB uses physical backups for automatic backup. For more information on backup methods, refer to [Backup methods](https://docs.byteplus.com/en/docs/mongodb/backup-overview#.5aSH5Lu95pa55byP).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [MongoDB console](https://console.byteplus.com/db/region:db+cn-beijing/mongodb).

2. In the top menu bar, select the project and region for the instance.

3. On the **Replica set instances** page, check the names of the target instances, and then select  **...**  \> **Modify data backup policy**.

4. In the **Modify backup policy** panel, configure the following parameters.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The default configuration of the backup policy is displayed in the batch <strong>Modify backup policy</strong> panel, which is not equal to the current backup policy configuration of the instance. You can view the current backup policy details for each instance under the <strong>Backups \> Full backup</strong> sub\-tab of the target instance. For more details, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/automatic-backup">Modifying automatic backup strategy</a>.   </div>
   

   
   |Parameter |Description |
   |---|---|
   |Backup retention days |Set the retention period for backup files. The value range is 7 to 365 days, with a default of 7 days.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The backup retention period will affect the available time range for point\-in\-time restoration. For example, if you set the retention period to 10 days, the available time range for restoring instance to a specific point in time will be any point within the past 10 days. For specific procedures on point\-in\-time recovery, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/recovery-by-time-point">Recovery by point in time</a>.</div><br> |
   |Backup cycle |You can select the days of the week for backups. By default, backups occur daily.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">For security considerations, a backup cycle of two or more days must be selected.</div><br> |
   |Backup start time |It can be set to any time range in the unit of hours. Off\-peak hours are recommended. |
   |Backup encryption |You can choose to **Enable** or **Disable** the backup encryption feature. Backup encryption encrypts and stores generated backup files, effectively preventing data leakage and meeting high security and compliance requirements.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">ESSD FlexPL volume instances currently do not support the backup encryption feature.</div><br> |
   |Backup log |The system automatically performs streaming backups of oplog logs at a frequency of once per 5 minutes without configuration.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The size of oplog log backup files is small because the logs are sliced by minute. For viewing convenience, the system merges and packages these logs once every two hours and sends the packages to the <a href="https://console.byteplus.com/db/region:db+cn-beijing/mongodb">MongoDB console</a>. You can view the backup files in the backup list on the <strong>Backups \> Full back</strong> sub\-tab.</div><br> |
   

5. When settings are complete, click **OK**.

6. In the pop\-up **Batch tasks have been initiated** dialog box, view **Task progress**, and click **OK** after all tasks are completed.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the <strong>Batch task initiated</strong> dialog box, click the <strong>Terminate</strong> button. After termination, the tasks of the instances that have not started the change will no longer be executed and cannot be restored. If you want to make changes again, you need to re\-initiate the batch task.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the tasks of some instances fail, place the cursor on <strong>Failed</strong> in <strong>Execution result</strong> column of the target instance to view the reason for the failure. You can also click <strong>Retry</strong> in the <strong>Actions</strong> column of the target instance to re\-execute the task; or click <strong>Batch retry</strong> to retry all the failed tasks.   </div>
