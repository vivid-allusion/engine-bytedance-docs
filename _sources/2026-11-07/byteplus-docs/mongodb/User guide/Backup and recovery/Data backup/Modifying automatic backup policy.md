---
title: "Modifying automatic backup policy"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/automatic-backup"
---

Document Database for MongoDB supports automatic backup, which automatically backs up data according to the default backup policy. You can configure automatic backup policy based on your business needs.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Automatic backup is enabled by default and cannot be disabled.

* By default, MongoDB uses physical backups for automatic backup. For more information on backup methods, refer to [Backup methods](https://docs.byteplus.com/en/docs/mongodb/backup-overview#.5aSH5Lu95pa55byP).

* Document Database for MongoDB replica set instances support batch modification of automatic backup policies. You can simultaneously modify automatic backup policies for replica set instances with consistent backup requirements, thereby improving instance backup management efficiency. For specific procedure, refer to [Modifying automatic backup policies in batches](https://docs.byteplus.com/en/docs/mongodb/modifying_automatic_backup_policies_in_batches).

* During physical backup, disk usage will gradually increase. After the backup is complete, disk usage will automatically return to normal. This behavior is expected during backup. The reason is that the hidden node continuously generates checkpoints to ensure data consistency, and these historical checkpoints cannot be reclaimed at this time. Combined with normal business write operations, disk usage will gradually increase over time.

* To prevent disk exhaustion during backup from impacting business operations, the platform has built\-in capacity safety protection mechanisms. The system reserves a backup retention space equivalent to 6% of the instance's total storage capacity (capped at a minimum of 2 GB and a maximum of 6 GB). In addition, an extra 1 GB of safety space is reserved to prevent write operations once this threshold is reached. Before and during backup, the system continuously monitors remaining disk space. When the sum of used and reserved space reaches the total capacity, the backup task automatically terminates to prioritize service availability.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the top menu bar, select the project and region for the instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click the **Backups** tab.

6. Under the **Full backup** sub\-tab, click **Backup settings**. In the pop\-up dialog box, set the following parameters.

   
   |Parameter |Description |
   |---|---|
   |Backup retention days |Set the retention period for backup files. The value range is 7 to 365 days, with a default of 7 days.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The backup retention period will affect the available time range for point\-in\-time restoration. For example, if you set the retention period to 10 days, the available time range for restoring instance to a specific point in time will be any point within the past 10 days. For specific procedures on point\-in\-time recovery, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/recovery-by-time-point">Recovery by point in time</a>.</div><br> |
   |Backup cycle |You can select the days of the week for backups. By default, backups occur daily.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">For security considerations, a backup cycle of two or more days must be selected.</div><br> |
   |Backup start time |It can be set to any time range in the unit of hours. Off\-peak hours are recommended. |
   |Backup encryption |You can choose to **Enable** or **Disable** the backup encryption feature. Backup encryption encrypts and stores generated backup files, effectively preventing data leakage and meeting high security and compliance requirements.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">FlexPL volume instances currently do not support the backup encryption feature.</div><br> |
   |Backup log |The system automatically performs streaming backups of oplog logs at a frequency of once per 5 minutes without configuration.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The size of oplog log backup files is small because the logs are sliced by minute. For viewing convenience, the system merges and packages these logs once every two hours and sends the packages to the <a href="https://console.byteplus.com/db/region:db+cn-beijing/mongodb">MongoDB console</a>. You can view the backup files in the backup list on the <strong>Backups \> Full back</strong> sub\-tab.</div><br> |
   

7. When settings are complete, click **OK**.


<span id=".55u45YWzLWFwaQ=="></span>
## Relevant APIs


|API |Description |
|---|---|
|[DescribeBackups](https://docs.byteplus.com/en/docs/mongodb/describebackups) |Call the DescribeBackups API to query the backup file list of the target MongoDB instance. |
|[DescribeDBInstanceBackupPolicy](https://docs.byteplus.com/en/docs/mongodb/describedbinstancebackuppolicy) |Call the DescribeDBInstanceBackupPolicy API to query automatic backup policy of target MongoDB instance. |
|[ModifyDBInstanceBackupPolicy](https://docs.byteplus.com/en/docs/mongodb/modifydbinstancebackuppolicy) |Call the ModifyDBInstanceBackupPolicy API to modify the automatic backup policy of the target MongoDB instance. |
