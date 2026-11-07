---
title: "Modifying automatic backup strategy"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/automatic-backup"
---

Cache for Redis supports data persistence and automatic data backup. It automatically backs up data according to the default backup strategy. You can modify the automatic backup strategy according to your service requirements. This article describes how to modify automatic backup strategy.

## Prerequisite

* The instance type is the **Primary\-secondary** instance. Single\-node instances do not support backup and restore functionality. For details about the feature differences between the two instance types, refer to [Feature differences](https://docs.byteplus.com/en/docs/redis/feature-faq#.5Li75aSH5a6e5L6L5ZKM5Y2V6IqC54K557G75Z6L5a6e5L6L5pSv5oyB55qE5Yqf6IO954m55oCn5pyJ5L2V5beu5Yir77yf).

* The instance state is **Running**. For more information about instance status, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

## Background information

Cache for Redis uses RDB snapshot storage by default to achieve persistence. It saves the memory data at a certain point in time to files on the hard disk.

After the Redis instance is successfully created, if you do not modify the automatic backup policy, the system will select any hour (such as 02:00~02:59) from 00:00 to 06:59 every day for backup by default, and the backup will be kept for 7 days by default. For more details, refer to [Function introduction](https://docs.byteplus.com/en/docs/redis/backup-recovery-intro).

## Precautions

* After all backups of Cache for Redis are created successfully, the backup retention period is fixed at 7 days and cannot be modified.

* Due to the backup, it will be automatically deleted and cannot be retrieved. It is recommended to download the backup locally in time before the end of the backup retention period, or perform data recovery through backup. For specific procedures, refer to [Downloading backup files](https://docs.byteplus.com/en/docs/redis/download-backup-files) and [Recovery by point in time](https://docs.byteplus.com/en/docs/redis/recovery-from-backup-set).

* When creating a backup, the Cache for Redis will preferentially pull data from the secondary node of the instance for backup. If there is no available secondary node for instance, it will pull data from the primary node for backup. During the backup period, it may cause a short\-term increase in instance access latency. It is recommended to perform backup\-related operations during off\-peak business hours. For more details, refer to [Data backup](https://docs.byteplus.com/en/docs/redis/backup-recovery-intro#.5pWw5o2u5aSH5Lu9).

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click the **Backups** tab.

5. On the **Backups** tab, click the **Backup strategy** sub\-tab.

6. On the **Backup strategy** sub\-tab, click **Edit** after **Automatic backup strategy**, and set the following parameters in the pop\-up dialog box.

   |Parameter |Description |
   |---|---|
   |Automatic backup |Turned on by default, no settings required.<br><br>> **danger**<br><br><br>> When you don't need automatic data backup, you can also turn off the automatic backup function. After turning it off, your data cannot be backed up in time. Please operate with caution.<br> |
   |Backup retention days |The number of days to retain backup files is fixed at seven days and cannot be changed. |
   |Backup cycle |Can be specified as a certain day or days of the week. Backup is performed daily by default. |
   |Backup start time |It can be set to any time range in the unit of hours. Off\-peak hours are recommended. |

7. After the settings are complete, click **OK**.

   > **tip**

   * > After the automatic backup settings are successfully modified, the selected instance will start automatic backup within the backup start time period of the most recent backup cycle according to the latest backup settings. You can also batch modify the automatic backup settings of multiple instances. For specific operation steps, refer to [Modifying automatic backup settings in batches](https://docs.byteplus.com/en/docs/redis/batch-modify-automatic-backup).

   * > After the automatic backup is created successfully, you can go to the **Backups** page to view. For specific procedures, refer to [Viewing backups](https://docs.byteplus.com/en/docs/redis/view-backup).

   * > Backups created with the automatic backup policy use the backup ID as the backup name by default. You can also modify the backup name according to your business needs. For specific procedures, refer to [Modifying backup name](https://docs.byteplus.com/en/docs/redis/modifying_the_backup_name).

## Relevant APIs

|API |Description |
|---|---|
|[DescribeBackupPlan](https://docs.byteplus.com/en/docs/redis/describebackupplan) |Call the DescribeBackupPlan API to query the automatic backup settings of a specified Redis instance, including backup type, backup cycle, expected time of next backup, and other information. |
|[ModifyBackupPlan](https://docs.byteplus.com/en/docs/redis/modifybackupplan) |Call the ModifyBackupPlan API to modify the automatic backup settings of a specified Redis instance, including backup cycle, automatic backup enable or disable, and other settings. |
|[DescribeBackups](https://docs.byteplus.com/en/docs/redis/describebackups) |Call the DescribeBackups API to query the information list of backup sets for a specified Redis instance. |
