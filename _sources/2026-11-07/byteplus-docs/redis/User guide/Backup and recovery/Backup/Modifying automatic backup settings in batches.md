---
title: "Modifying automatic backup settings in batches"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/batch-modify-automatic-backup"
---

Cache for Redis supports batch modification of automatic backup settings for instance. You can batch settings the same backup policy for instance with consistent backup requirements, improving the efficiency of instance backup management. This article describes how to bulk modify automatic backup settings.

## Prerequisite

* The instance type is the **Primary\-secondary** instance. Single\-node instances do not support backup and restore functionality. For details about the feature differences between the two instance types, refer to [Feature differences](https://docs.byteplus.com/en/docs/redis/feature-faq#.5Li75aSH5a6e5L6L5ZKM5Y2V6IqC54K557G75Z6L5a6e5L6L5pSv5oyB55qE5Yqf6IO954m55oCn5pyJ5L2V5beu5Yir77yf).

* The instance status that needs to modify the automatic backup settings in batches is **Running**. For more information about instance status, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

## Precautions

* You can select up to 100 instances simultaneously when modifying auto\-backup settings in batches.

* When creating a backup, the Cache for Redis will preferentially pull data from the secondary node of the instance for backup. If there is no available secondary node for instance, it will pull data from the primary node for backup. During the backup period, it may cause a short\-term increase in instance access latency. It is recommended to perform backup\-related operations during off\-peak business hours. For more details, refer to [Data backup](https://docs.byteplus.com/en/docs/redis/backup-recovery-intro#.5pWw5o2u5aSH5Lu9).

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, check the instance that requires automatic backup settings.

   > **tip**

   > You can select up to 100 instances simultaneously when modifying auto\-backup settings in batches.

4. Below the instance list, select  **...**   **\> Automatic backup settings**.

5. In the **Batch modify automatic backup settings** pop\-up window, the settings are as follows.

   |Parameter |Description |
   |---|---|
   |Automatic backup |Enabled by default, no settings required.<br><br>> **danger**<br><br><br>> When you don't need automatic data backup, you can also turn off the automatic backup function. The data cannot be backed up in time after disabled automatic data backup. Please operate with caution.<br> |
   |Backup retention days |The number of days to retain backup files is fixed at seven days and cannot be changed. |
   |Backup cycle |Can be specified as a certain day or days of the week. Backup is performed daily by default. |
   |Backup start time |Default is 04:00 ~ 04:59, it can be set to any time range in the unit of hours. Off\-peak hours are recommended. |

6. When settings are complete, click **OK**.

   > **tip**

   * > After the automatic backup settings are successfully modified, the selected instance will start automatic backup within the backup start time period of the most recent backup cycle according to the latest backup settings. You can also batch modify the automatic backup settings of single instance. For specific procedures, refer to [Modifying automatic backup strategy](https://docs.byteplus.com/en/docs/redis/automatic-backup).

   * > After the automatic backup is created successfully, you can go to **Backups** page to view. For specific procedures, refer to [Viewing backups](https://docs.byteplus.com/en/docs/redis/view-backup).

   * > Backups created with the automatic backup policy use the backup ID as the backup name by default. You can also modify the backup name according to your business needs. For specific procedures, refer to [Modifying backup name](https://docs.byteplus.com/en/docs/redis/modifying_the_backup_name).
