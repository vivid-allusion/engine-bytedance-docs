---
title: "Modifying data flashback strategy"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/set-data-flashback"
---

Cache for Redis provides data flashback function. After enabling the function, you can restore the Redis instance to a specified point in time, or restore the backup file at a specified point in time to a new instance, so as to avoid data loss caused by misoperations. This article introduces the relevant operation steps for setting up the data flashback function.

## Prerequisite

The instance type is the **Primary\-secondary** instance. Single\-node instances do not support backup and restore functionality. For details about the feature differences between the two instance types, refer to [Feature differences](https://docs.byteplus.com/en/docs/redis/feature-faq#.5Li75aSH5a6e5L6L5ZKM5Y2V6IqC54K557G75Z6L5a6e5L6L5pSv5oyB55qE5Yqf6IO954m55oCn5pyJ5L2V5beu5Yir77yf).

## Precautions

* After enabling the flashback feature, the system requires some time to perform a full backup. The duration of the backup depends on the data volume. After enabling the data flashback feature, it is recommended to wait for a while until the full backup is completed before using the point\-in\-time recovery feature.

* The recoverable time range is between the time when the data flashback feature is enabled and the current time, with the earliest recovery point being 7 days before the current time.

   Examples are as follows:

   * If the current time is `2024-01-18 06:00:00` and the data flashback feature was enabled at `2024-01-10 10:00:00`, then the recoverable time range is `2024-01-11 06:00:00 ~ 2024-01-18 06:00:00`.

   * If the current time is `2024-01-18 06:00:00` and the data flashback feature was enabled at `2024-01-12 10:00:00`, then the recoverable time range is `2024-01-12 10:00:00 ~ 2024-01-18 06:00:00`.

* After enabling data flashback, certain operations may affect the data flashback feature, including:

   * Performing operations such as [Modifying instance configuration](https://docs.byteplus.com/en/docs/redis/solutions-for-spec-modification), [Modifying availability zone](https://docs.byteplus.com/en/docs/redis/modify-az), or system maintenance (for example, upgrading kernel version, hardware/software, network, etc.) will cause the data flashback feature to **automatically disable**. After the data flashback feature is disabled, previous flashback points will no longer be retained.

      > **tip**

      > Cache for Redis provides an event center feature that supports system maintenance operations such as hardware, software, or network upgrades on machines hosting specified instances through planned events, ensuring the stability and sustainability of the cloud database service. For more details, refer to [Event center](https://docs.byteplus.com/en/docs/redis/event-center).

   * Performing [Restore to original instance by backup set](https://docs.byteplus.com/en/docs/redis/recovery-from-backup-set#.5oGi5aSN5Yiw5Y6f5a6e5L6L) or [Restore to original instance by point in time](https://docs.byteplus.com/en/docs/redis/recovery-by-time-point#.5oGi5aSN5Yiw5Y6f5a6e5L6L) operations will cause the Data flashback feature to **first automatically disable and then re\-enable**. After the Data flashback feature is reopened, the recoverable time point will start from the time point when the restore to original instance operation is completed.

* Cache for Redis supports configuring the Append only file persistence feature through the `appendonly-switch` parameter, but there is a constraint relationship between the AOF feature and the [Data flashback](https://docs.byteplus.com/en/docs/redis/set-data-flashback) feature, where:

   * When the `appendonly-switch` parameter is set to `off`, the data flashback feature cannot be enabled.

   * When the data flashback feature is enabled, the `appendonly-switch` parameter cannot be adjusted to `off`.

   For more details about the `appendonly-switch` parameter, refer to [Supported parameters](https://docs.byteplus.com/en/docs/redis/supported-parameter).

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click the **Backups** tab.

5. On **Backupstab,**  click the **Backup strategy** sub\-tab.

6. On the **Backup strategy** sub\-tab, click **Edit** after **Data flashback strategy**.

7. In the pop\-up dialog box, enable or disable **Data flashback**, then click **OK**.

   After enabling data flashback, you can restore instance data by time point. For specific procedures, refer to [Recovery by point in time](https://docs.byteplus.com/en/docs/redis/recovery-by-time-point).

## Relevant APIs

|API |Description |
|---|---|
|[StartContinuousBackup](https://docs.byteplus.com/en/docs/redis/startcontinuousbackup) |Call the StartContinuousBackup API to enable data flashback for a specified instance. |
|[StopContinuousBackup](https://docs.byteplus.com/en/docs/redis/stopcontinuousbackup) |Call the StopContinuousBackup API to disable data flashback for a specified instance. |
