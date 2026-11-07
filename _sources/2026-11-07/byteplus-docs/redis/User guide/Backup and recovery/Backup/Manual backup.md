---
title: "Manual backup"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/manual-backup"
---

You can use manual backup to temporarily back up the data of a Redis instance.

## Prerequisite

The instance type is the **Primary\-secondary** instance. Single\-node instances do not support backup and restore functionality. For details about the feature differences between the two instance types, refer to [Feature differences](https://docs.byteplus.com/en/docs/redis/feature-faq#.5Li75aSH5a6e5L6L5ZKM5Y2V6IqC54K557G75Z6L5a6e5L6L5pSv5oyB55qE5Yqf6IO954m55oCn5pyJ5L2V5beu5Yir77yf).

## Background information

Similar to automatic backup, Cache for Redis uses RDB snapshot storage by default to achieve persistence. It saves the memory data at a certain point in time to files on the hard disk. For more details, refer to [Function introduction](https://docs.byteplus.com/en/docs/redis/backup-recovery-intro).

## Precautions

* All Redis backups have a fixed retention time of 7 days and cannot be modified.

* Backups will be automatically deleted after expiration and cannot be recovered. It is recommended to download the backup locally in time before the end of the backup retention period, or perform data recovery through backup. For specific procedures, refer to [Downloading backup files](https://docs.byteplus.com/en/docs/redis/download-backup-files) and [Recovery by point in time](https://docs.byteplus.com/en/docs/redis/recovery-from-backup-set).

* When creating a backup, the Cache for Redis will preferentially pull data from the secondary node of the instance for backup. If there is no available secondary node for instance, it will pull data from the primary node for backup. During the backup period, it may cause a short\-term increase in instance access latency. It is recommended to perform backup\-related operations during off\-peak business hours. For more details, refer to [Data backup](https://docs.byteplus.com/en/docs/redis/backup-recovery-intro#.5pWw5o2u5aSH5Lu9).

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the **Summary** page, click the **Backups** tab.

5. On the **Backups ** tab, under the **Basic backups ** sub\-tab, click **Create backup manually**.

6. In the dialog box that pops up, after settings backup name click **OK**.

   > **tip**

   * > The backup name is an optional configuration. If the backup name is not set, the backup ID is used as the name by default. You can also modify the backup name after the backup creates successfully. For specific procedures, refer to [Modifying backup name](https://docs.byteplus.com/en/docs/redis/modifying_the_backup_name).

   * > If you want toseta backup name, the name must meet the following conditions simultaneously:

      * > It should start with a Chinese character, a letter, or an underscore (_).

      * > The length should be 1 to 128 characters.

      * > It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).

   * > Instance backup takes some time. Data update records that occur during the backup period will not be saved in the backup data.

   * > After the backup is completed, you can refresh the **Backups** to view the backup data. For the specific procedures, refer to [Viewing backups](https://docs.byteplus.com/en/docs/redis/view-backup).

## Relevant APIs

|API |Description |
|---|---|
|[CreateBackup](https://docs.byteplus.com/en/docs/redis/createbackup) |Call the CreateBackup interface to manually create backups for the specified Redis instance. |
|[DescribeBackups](https://docs.byteplus.com/en/docs/redis/describebackups) |Call the DescribeBackups interface to query the list of backup set information for the specified Redis instance. |
