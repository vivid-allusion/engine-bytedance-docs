---
title: "Modifying basic backup policy in batches"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_data_backup_policies_in_batches"
---

RDS for MySQL supports batch modification of data backup policies, allowing you to set data backup policies simultaneously for instances with consistent business needs. This topic describes the steps to set up a data backup policy in a batch.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance is created and in the **Running** state. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* When batch modifying the data backup policy in batches, make sure that all instances have the same requirements for the data backup policy.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Recovery of read\-only nodes is not currently supported.

* Do not perform DDL operations during the backup period to avoid table locks that may cause a backup failure.

* We recommend you avoid peak business hours when performing backup.

* You can batch modify the data backup policy for up to 50 instances at the same time.

* You can set a backup policy only for a batch of instances that have the same storage type and engine type.

* Since the multiple node is a one\-primary\-multiple\-secondary architecture, there may be multiple secondary nodes, resulting in more binlogs than double node instances. It is recommended that you set up a reasonable backup strategy to avoid taking up too much storage space and incurring unexpected expenses. Each instance has a free basic backup storage space of the same size as the instance primary node storage space. The portion of the basic backup file that exceeds the free space will be billed according to the billing standard of the basic backup storage space. For more information on billing for backup storage space, see [Billing items and prices](https://docs.byteplus.com/en/docs/RDS_for_MySQL/charge_items_and_price).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, select multiple target instances.

4. In the lower\-left corner of the **Instances** page, choose  **...**  \> **Modify data backup policy**.

5. Set the following parameters on the pop\-up **Modify basic backup policy in batches** page, and then click **OK** after the parameters are set.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When you batch modify the data backup policy in batches, the backup policy parameters are set to null by default, and the original backup policy of the instances is not displayed.</div>



<Tabs>
<Tab zoneid="kl3WD2Nrmi" title="Storage type is Local SSD">
<TabTitle>Storage type is Local SSD</TabTitle>


|Policy category |Configuration item |Is it required? |Description |
|---|---|---|---|
|<div style="text-align: center"><br>Data backup settings</div><br> |Retain the backups until the instance is released |No |Whether to retain backup files for a long time before releasing the instance. After enabling this function, there is no need to set the backup retention days. |
||Full backup retention period |Yes |The retention duration of backup files after instance release. The value range is 7 to 3650 days, with a default of 7 days. |
||Time window for starting backup |Yes |The time window for starting full backup or incremental backup. The time window cannot span across days. |
||Full backup cycle<br><br> |Yes |The days of the week when full backups are executed. Select at least 2 days and at most 7 days per week. RDS for MySQL provides three non\-consecutive days as the default value based on the current system status. |
||DDL maximum wait time |Yes |Data backups will block DDL commands. When the DDL command exceeds the wait time, the backup will be stopped and the DDL command will be released. The default DDL maximum wait time is 1800 seconds. The minimum can be set to 1 second, the maximum can be set to 86400 seconds, and the increment is 1 second. |
||Incremental backup frequency |No |You can set incremental backups to High frequency or Normal frequency. Default is normal.<br><br><br>* **High**: When selecting high\-frequency incremental, you need to set **High frequency incremental backup frequency**. After setting, incremental backups can be performed according to the set frequency.<br><br>* **Normal**: When selecting normal incremental, you need to set **Incremental backup cycle**. |
||High frequency incremental backup frequency<br><br> |No |When selecting high\-frequency incremental, you need to set High frequency incremental backup frequency. Can be set to perform an incremental backup every 1 hour, every 2 hours, every 4 hours, every 6 hours, or every 12 hours. The default value is backup every 2 hours.<br><br>Description<br><br><br>* No incremental backup will be initiated during full backup.<br><br>* The next incremental backup is not performed until the end of the incremental backup. If the data volume of a local disk instance exceeds 8 TB, a single incremental backup will take more than one hour, and the "Every 1 hour" high\-frequency incremental backup will not be strictly performed.<br><br>* Full backup has a higher priority than incremental backup. If an incremental backup is still in progress when the start time window for full backup arrives, the incremental task will be terminated and full backup will start. |
||Incremental backup cycle |No |When normal incremental backup is selected, the frequency of performing incremental backups. The frequency of normal incremental backup is selected weekly and cannot conflict with the full backup cycle. According to the setting of the full backup cycle, up to 5 days per week can be selected for incremental backup. If not selected, the instance will not perform incremental backups. |
|Binlog backup settings |Binlog backup |No |Enable or disable the backup function for binlog.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Enabling the binlog backup function may incur additional costs.</div><br><br><br>* <div data-tips="true" data-tips-type="default">After disabling the Binlog backup function, existing backups will be immediately emptied and time point recovery will no longer be supported.</div><br> |
||Consistent with the full backup retention period |No |Set whether the retention days of Binlog backups are the same as those of data backups.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If this switch is turned on, there is no need to set <strong>Binlog backup retention period</strong>.</div><br> |
||Binlog backup retention period |No |The retention period of backup files in the backup space. The value range is 7 to 3650 days, with a default of 7 days. |
|Backup file retention rule after releasing instance |Retention policy |Yes |Set the retention policy for backup files after instance release. You can choose:<br><br><br>* **Do not retain backups**: that is, do not keep any backups of the instance after the instance is deleted.<br><br>* **Create a final backup and retain only this backup**: that is, the instance will be backed up and retained before the instance is deleted, and other backups of the instance will be deleted. Default.<br><br>* **Create a final backup and retain all backups**: that is, all backups of the instance are retained after the instance is deleted. |
||Retention period |Yes |The retention duration of backup files after instance release. The value range is 7 to 3650 days, with a default of 7 days. |





</Tab>
<Tab zoneid="bebAUV8BKH" title="Storage type is Cloud ESSD PL0 or Cloud ESSD FlexPL">
<TabTitle>Storage type is Cloud ESSD PL0 or Cloud ESSD FlexPL</TabTitle>


|Policy category |Configuration item |Is it required? |Description |
|---|---|---|---|
|<div style="text-align: center"><br>Data backup settings</div><br> |Snapshot backup retention period |Yes |The length of time for retaining backup files after instance release. The value range is 7 to 730 days, with a default of 7 days. |
||High frequency snapshot backup |No |Enable or disable high frequency snapshot backup function. Off by default. |
||High frequency snapshot backup frequency<br><br> |No |If the high frequency snapshot backup is enable, the frequency of high frequency snapshot backup needs to be set. Support settings for snapshot backups every 15 minutes **, ** every 30 minutes, every 1 hour, every 2 hours, every 3 hours, every 4 hours, every 6 hours, every 8 hours, or every 12 hours.<br><br><br>* Backup frequency is minute: All snapshots created within one hour are retained. After one hour, only the first snapshot of each hour is retained. After 24 hours, only the first snapshot after 00:00 each day is retained.<br><br><br>Example: If you set the snapshot backup frequency to every 30 minutes, the 2 snapshots created within 1 hour will all be retained; after 1 hour but within 24 hours, only the 23 snapshots created on the hour are retained; after 24 hours (for example, within a week), only the 6 snapshots created after 00:00 each day are retained. In summary, if you set the snapshot frequency to every 30 minutes, 31 snapshots will be retained within a week.<br><br><br>* Backup frequency is hourly: all snapshots generated within 24 hours are retained. After 24 hours, only the first snapshot after 00:00 each day is retained.<br><br><br>Example: if you set the snapshot backup frequency to every 4 hours, all 6 snapshots generated within 24 hours will be retained. After 24 hours (for example, within a week), only the 6 snapshots created after 00:00 each day are retained. In summary, if you set the snapshot frequency to every 4 hours, 12 snapshots will be retained within a week. |
||Time window for starting backup |Yes |The time window for starting snapshot backup. The time window cannot span across days. |
||Snapshot backup cycle<br><br> |Yes |The days of the week when snapshot backups are executed. Select at least 2 days and at most 7 days per week. RDS for MySQL provides three non\-consecutive days as the default value based on the current system status. |
||DDL maximum wait time<br><br> |Yes |Data backups will block DDL commands. When the DDL command exceeds the wait time, the backup will be stopped and the DDL command will be released. The default DDL maximum wait time is 1800 seconds. The minimum can be set to 1 second, the maximum can be set to 86400 seconds, and the increment is 1 second. |
|Binlog backup settings |Binlog backup |No |Enable or disable the backup function for binlog. Enabled by default.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Enabling the binlog backup function may incur additional costs.</div><br><br><br>* <div data-tips="true" data-tips-type="default">After disabling the Binlog backup function, existing backups will be immediately emptied and time point recovery will no longer be supported.</div><br> |
||Consistent with the full backup retention period |No |Set whether the retention days of Binlog backups are the same as those of fulll backups. Off by default.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If this switch is turned on, there is no need to set <strong>Binlog backup retention period</strong>.</div><br> |
||Binlog backup retention period |No |The retention period of backup files in the backup space. The value range is 7 to 730 days, with a default of 7 days. |
|Backup file retention rule after releasing instance |Retention policy |Yes |Set the retention policy for backup files after instance release. You can choose:<br><br><br>* **Do not retain backups**: that is, do not keep any backups of the instance after the instance is deleted.<br><br>* **Create a final backup and retain only this backup**: that is, the instance will be backed up and retained before the instance is deleted, and other backups of the instance will be deleted. Default.<br><br>* **Create a final backup and retain all backups**: that is, all backups of the instance are retained after the instance is deleted. |
||Retention period |Yes |The retention duration of backup files after instance release. The value range is 7 to 3650 days, with a default of 7 days. |





</Tab>
</Tabs>



6. In the pop\-up **Batch tasks have been initiated** dialog box, view **Task progress**, and click **OK** after a task is completed.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can click the <strong>Terminate</strong> button in the <strong>Batch tasks have been initiated</strong> dialog box. After termination, tasks for instances that have not yet started changes will no longer be executed and cannot be recovered. If you want to make changes again, you need to re\-initiate the batch task.</div>


* <div data-tips="true" data-tips-type="tip">If the task execution fails, place the cursor on <strong>Failure</strong> in the <strong>Execution result</strong> column to view the failure reason.</div>
