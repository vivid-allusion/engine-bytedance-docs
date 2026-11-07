---
title: "Modifying backup policy"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_data_backup_policies"
---

This topic introduces the operation steps for modifying the backup policy.

## Background

RDS for MySQL supports customizing the backup policy for instances. The backup policy is divided into several categories: basic backup policy, local binlog retention policy, backup retention policy after instance release and backup download policy.

* Basic backup policy

   * Storage type is local SSD disk: includes settings such as the retention days of full backups, retaining backup files after instance release, binlog backup, incremental backup, backup start time, retention days of binlog backups, full backup cycle, retaining backup files after instance release, encryption of binlog backups, incremental backup cycle, and encryption of physical backups.

   * For the Cloud ESSD FlexPL and Cloud ESSD PL0 storage types: including snapshot backup retention period, binlog backup, backup start time, high\-frequency snapshot backup, snapshot backup cycle, binlog backup retention period, binlog backup encryption, and DDL maximum wait time.

   > **tip**

   * > Cloud disk\-based instances and instances that use the RocksDB engine do not currently support physical backup encryption.

   * > Instances that use the RocksDB engine do not support incremental backup.

* Local binlog retention policy

   The local binlog retention policy includes settings such as local binlog retention duration, maximum storage space usage rate, file retention upper limit, and available storage space.

* Backup retention policy after instance release

   The backup retention policy after instance release includes the retention policy and the retention duration settings.

* Backup download policy

   The backup download policy includes settings on whether to generate a backup of the public network download address.

## Prerequisites

The instance has been created and is in the **Running** or **Stopped** status. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

## Precautions

* Backup settings for read\-only nodes are not supported.

* Do not perform DDL operations during the backup period to avoid table locks that may cause a backup failure.

* It is recommended to set the backup start time window to avoid business peak periods.

* Notes on backup encryption

   * Encryption of log backups and data backups of physical backup type is supported.

   * Enable or disable the encryption function for binlog backup files.

   * After enabling backup encryption, the backup time is expected to increase by 20% to 30%.

   * Enabling backup encryption does not affect the use of backup files in the RDS for MySQL console, and manual decryption is not required. If the encrypted backup file is downloaded for local use, the backup file needs to be decrypted after downloading the key of the backup file. For more information about downloading backup file keys and decrypting backup files, see [Downloading backup file keys](https://docs.byteplus.com/en/docs/RDS_for_MySQL/downloading_backup_file_keys) and [Decrypting backup files](https://docs.byteplus.com/en/docs/RDS_for_MySQL/decrypting_backup_files).

   * When backup encryption is disabled, the encryption of backup files during backup encryption is still in effect. If you want to download the backup file for local use, you still need the key to download the backup file to decrypt the backup file.

   * The backup encryption function is currently available for free. Please pay attention to the follow\-up notice for the official charging time.

* Billing applies to the storage space used by basic backups, cross\-regional backups, and backups of deleted instances in RDS for MySQL. Set your backup policy reasonably to avoid unexpected fees from excessive storage usage. Especially, the multi\-node instance with one primary and multiple secondary architecture will generate more binlogs than the dual\-node instance because it has multiple secondary nodes. RDS for MySQL provides each instance with a certain amount of free storage space for basic backups. Storage space for basic backup files that exceed free space, cross\-region backups, and deleted instance backups is billed according to the appropriate billing standard. For more billing information on backup storage space, see [Billing items and prices](https://docs.byteplus.com/en/docs/RDS_for_MySQL/charge_items_and_price).

## Procedure

1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   > **tip**

   > If the project of the instance has not been set, the project should be selected as **All resources**.

3. Click on **Instances** in the left navigation bar.

4. On the **Instances** page, click on the target instance name to enter the instance details page.

5. At the top of the page, click the **Backups** tab.

6. Click the **Backup policy** sub\-tab, click **Edit** on the right side of **Basic backup policy**, **Local binlog retention policy**, **Backup retention policy after instance release**, or **Backup download policy**. The specific configuration items are shown in the following table.

**Basic backup policy**

|Storage type |Configuration item |Is it required? |Description |
|---|---|---|---|
|Local SSD |Retain the backups until the instance is released |No |Whether to retain backup files for a long time before releasing the instance. After enabling this function, there is no need to set the backup retention days. Off by default. |
||Full backup retention period |Yes |The length of time for retaining backup files after instance release. The range of backup retention days for different storage type instances is different:<br><br><br>* For local disk instances: the optional range is 7 to 3650 days, and the default is 7 days.<br><br>* For cloud disk instances: currently only supports retention for 7 days. |
||Time window for starting backup |Yes |The time window for starting full backup or incremental backup. The time window cannot span across days. |
||Full backup cycle |Yes |The days of the week when full backups are executed. Select at least 2 days and at most 7 days per week. RDS for MySQL provides three non\-consecutive days as the default value based on the current system status. |
||DDL maximum wait time |Yes |Data backups will block DDL commands. When the DDL command exceeds the wait time, the backup will be stopped and the DDL command will be released. The default DDL maximum wait time is 1800 seconds. The minimum can be set to 1 second, the maximum can be set to 86400 seconds, and the increment is 1 second. |
||Incremental backup (Local disk instance) |No |You can set incremental backups to High frequency or Normal frequency. Default is normal.<br><br><br>* **High**: When selecting high\-frequency incremental, you need to set **High frequency incremental backup frequency**. After setting, incremental backups can be performed according to the set frequency.<br><br>* **Normal**: When selecting normal incremental, you need to set **Incremental backup cycle**. |
||High frequency incremental backup frequency (Local disk instance) |No |When selecting high\-frequency incremental, you need to set High frequency incremental backup frequency. Can be set to perform an incremental backup every 1 hour, every 2 hours, every 4 hours, every 6 hours, or every 12 hours. The default value is backup every 2 hours.<br><br>> **tip**<br><br><br><br>* > No incremental backup will be initiated during full backup.<br><br><br>* > The next incremental backup is not performed until the end of the incremental backup. If the data volume of a local disk instance exceeds 8 TB, a single incremental backup will take more than one hour, and the "Every 1 hour" high\-frequency incremental backup will not be strictly performed.<br><br><br>* > Full backup has a higher priority than incremental backup. If an incremental backup is still in progress when the start time window for full backup arrives, the incremental task will be terminated and full backup will start.<br> |
||Incremental backup cycle (Local disk instance) |No |When normal incremental backup is selected, the frequency of performing incremental backups. The frequency of normal incremental backup is selected weekly and cannot conflict with the full backup cycle. According to the setting of the full backup cycle, up to 5 days per week can be selected for incremental backup. If not selected, the instance will not perform incremental backups. |
||Physical backup encryption (Local disk instance) |No |Enable or disable the encryption function for physical backup files. Off by default. |
||High frequency incremental backup（Cloud disk instance） |No |Set whether to enable high frequency incremental backup. Off by default. |
||High frequency incremental backup frequency (Cloud disk instance) |No |If the high frequency incremental backup is enabled, the frequency of high frequency incremental backup needs to be set. Support settings for incremental backups every 1 hour, every 2 hours, every 3 hours, every 4 hours, every 6 hours, every 8 hours, and every 12 hours. |
||Binlog backup |No |Enable or disable the backup function for binlog. Enabled by default.<br><br>> **tip**<br><br><br><br>* > Enabling the binlog backup function may incur additional costs.<br><br><br>* > After disabling the Binlog backup function, existing backups will be immediately emptied and time point recovery will no longer be supported.<br> |
||Consistent with the full backup retention period |No |Set whether the retention days of Binlog backups are the same as those of fulll backups. Off by default.<br><br>> **tip**<br><br><br>> If this switch is turned on, there is no need to set **Binlog backup retention period**.<br> |
||Binlog backup retention period |No |The retention period of backup files in the backup space. The range of backup retention days for different storage type instances is different:<br><br><br>* For local disk instances: the optional range is 7 to 3650 days, and the default is 7 days.<br><br>* For cloud disk instances: the optional range is 7 to 720 days, and the default is 7 days. |
||Binlog backup encryption |No |Enable or disable the encryption function for binlog backup files. Off by default. |
|Cloud ESSD PL0 or Cloud ESSD FlexPL |Snapshot backup retention period |Yes |The length of time for retaining backup files after instance release. The value range is 7 to 730 days, with a default of 7 days. |
||High frequency snapshot backup |No |Enable or disable the high frequency snapshot backup function. Off by default. |
||High frequency snapshot backup frequency<br><br> |No |To enable the high frequency snapshot backup feature, you need to set its frequency. Support settings for snapshot backups 15 minutes, every 30 minutes, every 1 hour, every 2 hours, every 3 hours, every 4 hours, every 6 hours, every 8 hours, and every 12 hours.****<br><br><br>* Backup frequency is minute: All snapshots created within one hour are retained. After one hour, only the first snapshot of each hour is retained. After 24 hours, only the first snapshot after 00:00 each day is retained.<br><br>   Example: If you set the snapshot backup frequency to every 30 minutes, the 2 snapshots created within 1 hour will all be retained; after 1 hour but within 24 hours, only the 23 snapshots created on the hour are retained; after 24 hours (for example, within a week), only the 6 snapshots created after 00:00 each day are retained. In summary, if you set the snapshot frequency to every 30 minutes, 31 snapshots will be retained within a week.<br><br>* Backup frequency is hourly: all snapshots generated within 24 hours are retained. After 24 hours, only the first snapshot after 00:00 each day is retained.<br><br>   Example: if you set the snapshot backup frequency to every 4 hours, all 6 snapshots generated within 24 hours will be retained. After 24 hours (for example, within a week), only the 6 snapshots created after 00:00 each day are retained. In summary, if you set the snapshot frequency to every 4 hours, 12 snapshots will be retained within a week. |
||Time window for starting backup |Yes |The time window for starting snapshot backup. The time window cannot span across days. |
||Snapshot backup cycle |Yes |The days of the week when snapshot backup are executed. Select at least 2 days and at most 7 days per week. RDS for MySQL provides three non\-consecutive days as the default value based on the current system status. |
||DDL maximum wait time<br><br> |Yes |Data backups will block DDL commands. When the DDL command exceeds the wait time, the backup will be stopped and the DDL command will be released. The default DDL maximum wait time is 1800 seconds. The minimum can be set to 1 second, the maximum can be set to 86400 seconds, and the increment is 1 second. |
||Binlog backup<br><br> |No<br><br> |Enable or disable the backup function for binlog. Enabled by default.<br><br>> **tip**<br><br><br><br>* > Enabling the binlog backup function may incur additional costs.<br><br><br>* > After disabling the Binlog backup function, existing backups will be immediately emptied and time point recovery will no longer be supported.<br> |
||Consistent with the full backup retention period<br><br> |No |Set whether the retention days of Binlog backups are the same as those of fulll backups. Off by default.<br><br>> **tip**<br><br><br>> If this switch is turned on, there is no need to set **Binlog backup retention period**.<br> |
||Binlog backup retention period |No |The retention period of backup files in the backup space. The value range is 7 to 3650 days, with a default of 7 days. |
||Binlog backup encryption |No |Enable or disable the encryption function for binlog backup files. Off by default. |

**Cross-regional backup policy**

|Configuration item |Is it required? |Description |
|---|---|---|

**Local binlog retention policy**

|Configuration item |Is it required? |Description |
|---|---|---|
|Local binlog retention period |Yes |Local logs that exceed the retention period will be automatically deleted. It can be set from 0 to 168 hours, and the default value is 24 hours. When set to 0, local logs will not be automatically deleted. |
|Maximum storage usage ratio |Yes |The oldest Binlog files will be deleted automatically when the space utilization rate above is exceeded until the space utilization rate is lower than this rate. Space usage rate = Local binlog size / Total available (purchased) space size of the instance. It can be set to 20% to 50%, and the default value is 30%. |
|Maximum number of files to be retained |Yes |Enable or disable the function of restricting the number of local binlog retained. When you turn it on, you need to set **Local binlog reservations**. Maximum number of files to be retained is enabled by default. |
|Local binlog reservation number |No |The number of local binlog files to be retained. Local binlogs exceeding the retention number will be automatically deleted. It can be set from 6 to 1000, and the default value is 60.<br><br>> **tip**<br><br><br>> The frequency of binlog file switching depends on the log size and log duration, when the binlog file exceeds 500MB or exceeds 1 hour, it will be switched to a new binlog file to continue writing.<br> |
|Available storage space |Yes |Enable or disable the protection of locally available storage space. Off by default. When this feature is turned on, the system will automatically start to clean up the earliest local binlogs when the total storage space occupancy of the instance exceeds 80% or the remaining space is less than 5 GiB, until the total space occupancy is less than 80% and the remaining space is more than 5 GiB. |

**Backup retention policy after instance release**

|Configuration item |Is it required? |Description |
|---|---|---|
|Retention policy |Yes |Set the retention policy for backup files after instance release. You can choose:<br><br><br>* **Do not retain backups**: that is, do not keep any backups of the instance after the instance is deleted.<br><br>* **Create a final backup and retain only this backup**: that is, the instance will be backed up and retained before the instance is deleted, and other backups of the instance will be deleted. Default.<br><br>* **Create a final backup and retain all backups**: that is, all backups of the instance are retained after the instance is deleted. |
|Retention period |Yes |The retention duration of backup files after instance release. The value range is 7 to 3650 days, with a default of 7 days.<br><br>> **tip**<br><br><br>> Storage for backups of deleted instances is free for 30 days. After 30 days, charges are based on backup space usage. For details on billing rules, refer to [Billing items and Price](https://docs.byteplus.com/en/docs/RDS_for_MySQL/charge_items_and_price). The retention duration of backup files after instance release. Currently only supports setting to 7 days.<br> |

**Backup download policy**

|Configuration item |Is it required? |Description |
|---|---|---|
|Generate public network download address |Yes |Sets whether to generate a public download address for the backup when downloading backup files for the instance. |
