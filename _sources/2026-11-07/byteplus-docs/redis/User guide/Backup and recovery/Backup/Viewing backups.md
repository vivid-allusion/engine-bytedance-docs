---
title: "Viewing backups"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/view-backup"
---

Cache for Redis supports automatic or manual backup generation. You can view the generated backup information (such as backup name, size, backup start and end time, etc.) on the Redis console. This article describes how to view Redis backups.

## Prerequisites

The instance type is the **Primary\-secondary** instance. Single\-node instances do not support backup and restore functionality. For details about the feature differences between the two instance types, refer to [Feature differences](https://docs.byteplus.com/en/docs/redis/feature-faq#.5Li75aSH5a6e5L6L5ZKM5Y2V6IqC54K557G75Z6L5a6e5L6L5pSv5oyB55qE5Yqf6IO954m55oCn5pyJ5L2V5beu5Yir77yf).

## Backup scenario

Cache for Redis generates backups manually or automatically in the following scenarios:

* Generate backups based on the instance's automatic backup policy. Automatic backup policy settings method, refer to [Setting automatic backup](https://docs.byteplus.com/en/docs/redis/automatic-backup).

* Generating a backup is triggered by the manual backup function. For specific procedures, refer to [Manual backup](https://docs.byteplus.com/en/docs/mongodb/manual-backup).

* When an instance is deleted or unsubscribed, the trigger system creates a final backup for that instance by default. For specific procedures, refer to [Deleting pay-as-you-go instance](https://docs.byteplus.com/en/docs/redis/delete-instance) and [Unsubscribing from yearly or monthly subscription instance](https://docs.byteplus.com/en/docs/redis/unsubscribe-instance).

* When the system forcibly deletes an expired instance, the trigger system creates a final backup for that instance by default. For more information about expired instances, refer to [Expiration](https://docs.byteplus.com/en/docs/redis/arrear-and-expiration).

## Backup status

The following table summarizes all the possible status details of a Cache for Redis backup for your reference.

|Backup status |Triggering operation |Description or impact |
|---|---|---|
|Creating |Create backups. |The backup is being created and no actions can be taken on the backup at this time. |
|Available<br><br>Available |Backup successfully created. |You can save the backup download locally for management, or restore data through backup. For specific procedures, refer to [Downloading backup files](https://docs.byteplus.com/en/docs/redis/download-backup-files) and [Recovery from backup set](https://docs.byteplus.com/en/docs/redis/recovery-from-backup-set). |
|Unavailable |This status occurs when backup create fails or otherwise makes the backup unavailable. |It is recommended that you rebuild the backup through the manual backup function. For specific procedure, refer to [Manual backup](https://docs.byteplus.com/en/docs/mongodb/manual-backup).<br><br>> **tip**<br><br><br>> If a new backup cannot be generated or is not available, please [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support.<br> |
|Deleting |Delete backups. |Backups that exceed the retention period (7 days) are automatically deleted and all resources associated with the backup are reclaimed. |

## Precautions

* All Redis backups have a fixed retention time of 7 days and cannot be modified.

* Backups will be automatically deleted after expiration and cannot be recovered. It is recommended to download the backup locally in time before the end of the backup retention period, or perform data recovery through backup. For specific procedures, refer to [Downloading backup files](https://docs.byteplus.com/en/docs/redis/download-backup-files) and [Recovery](https://docs.byteplus.com/en/docs/redis/recovery).

* [Data backup](https://docs.byteplus.com/en/docs/redis/backup-recovery-intro#.5pWw5o2u5aSH5Lu9).

## View basic backups

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. You can find the backup to view according to your business scenario.

   **View basic backups in single instance**

1. In the top menu bar, select the project and region to which the instance belongs.

   2. On the **Instances** page, click the target instance name.

   3. On the instance details page, click the **Backups** tab.

   4. On the **Backups** tab, under the **Basic backups** sub\-tab, you can perform the following actions.

      |Classification of actions |Description |
      |---|---|
      |Viewing backups |View backup details in the current instance, including backup name/ID, backup status, backup progress, backup size, backup type, backup start and end times, etc. |
      |Filter backups |You can filter out backups that meet the specified criteria by:<br><br><br>* In the upper right corner of the list, first filter the backups in the list based on start and end times.<br><br>* In the backup list, filter again according to the **backup status ** field. |
      |Manage backups |You can also download or restore actions from a backup of the list. For specific procedures, refer to:<br><br><br>* [Downloading backup files](https://docs.byteplus.com/en/docs/redis/download-backup-files)<br><br>* [Recovery from backup set](https://docs.byteplus.com/en/docs/redis/recovery-from-backup-set)<br><br>* [Recovery by point in time](https://docs.byteplus.com/en/docs/redis/recovery-by-time-point) |

   **View basic backups in specified region or project**

1. In the top menu bar, select the project and region to which the backup belongs.

      > **tip**

      > The region and project to which the basic backup belongs in the instance are the same as the region and project to which the backup belongs at the point in time when the backup was generated. E.g., when the backup is generated, the region where the instance is located is Beijing, and the project to which it belongs is the default, then the region where the backup is located is also Beijing, and the project to which it belongs is also the default.

   2. In the left navigation bar, select **NoSQL Database \> Redis \> Backups**.

   3. On the **Backups** tab, under the **Basic backups** tab, you can perform the following actions.

      |Classification of actions |Description |
      |---|---|
      |Viewing backups |You can view backup details in the backup list, including:<br><br><br>* Backup name/ID, backup status, backup size, backup progress, backup method, backup start and end time, and backup retention period.<br><br>* The instance name/ID, instance status, database version, and project to which the backup belongs. |
      |Filter backups |* Supported filters or fields<br><br>   You can filter backups that meet the specified criteria by the following steps:<br><br>   * In the upper right corner of the list, first filter by backup start and end time, backup name, instance name, or instance ID. The backup name, instance name, and instance ID all support fuzzy filtering.<br><br>   * In the backup list, filter again by **Backup status**, **Backup method**, and **Instance status** fields.<br><br>* Example<br><br>   You can filter out all available backups of deleted instances which created between `2024-01-16 00:00:00 ~ 2024-01-16 01:00:00` by the following steps:<br><br>   * Backup starts from `2024-01-16 00:00:00` and ends before `2024-01-16 01:00:00`.<br><br>   * **Backup status** is **Available**.<br><br>   * **Instance status** is **Deleted**. |
      |Manage backups |You can also download or restore actions from a backup of the list. For specific procedures, refer to:<br><br><br>* [Downloading backup files](https://docs.byteplus.com/en/docs/redis/download-backup-files)<br><br>* [Recovery from backup set](https://docs.byteplus.com/en/docs/redis/recovery-from-backup-set)<br><br>* [Recovery by point in time](https://docs.byteplus.com/en/docs/redis/recovery-by-time-point)<br><br>* [Recovery from deleted instance](https://docs.byteplus.com/en/docs/redis/restore-deleted-instance) |

## Relevant APIs

|API |Description |
|---|---|
|[DescribeBackups](https://docs.byteplus.com/en/docs/redis/describebackups) |Call the DescribeBackups API to query the list of backup sets for target Redis instance. |
