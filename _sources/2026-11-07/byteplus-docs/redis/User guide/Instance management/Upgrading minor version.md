---
title: "Upgrading minor version"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/upgrade-minor-version"
---

Cache for Redis periodically releases minor versions of proxy nodes and server nodes to enrich product features or fix known bugs and improve the user experience. This topic describes the specific procedure for upgrading minor versions.

## Prerequisite

The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

## Upgrade impact

* After initiating a minor version upgrade, the system first prepares node resources for the corresponding version. Then, it triggers a primary\-secondary switch within your selected switch time, promoting the new node to the primary. During switching, the database may experience brief disconnections (1~3 times) or enter read\-only status for seconds. Operate with caution.

* It is recommended to perform the switch operation during off\-peak business hours and ensure the application has an automatic reconnection mechanism to minimize the impact of the operation on your business.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance name.

4. In the **Configuration** area of the **Summary** tab, click **Upgrade** after **Minor version**.

   > **tip**

   > The system automatically detects the instance's minor version. If your server or proxy version is not the latest, a **Recommendation** appears next to the **Upgrade** button. We recommend that you arrange the upgrade as soon as possible during off\-peak business hours.

5. In the pop\-up dialog box, set the following parameters according to your business needs.

   |Parameters |Description |
   |---|---|
   |Server version |Select the target server version to upgrade to from the dropdown list.<br><br>For more details about server versions, refer to [Server version release log](https://docs.byteplus.com/en/docs/redis/db-minor-version-release-log?lang=en#J0CFZO9x). |
   |Proxy version |Select the target proxy version to upgrade to from the dropdown list.<br><br>For more details about proxy versions, refer to [Proxy version release log](https://docs.byteplus.com/en/docs/redis/db-minor-version-release-log?lang=en#.cHJveHkt54mI5pys5Y-R5biD5pel5b-X).<br><br>> **tip**<br><br><br>> This configuration item will not be displayed if the instance only has a direct connection address and no proxy connection address.<br> |
   |Switch time |Select the switch time. You can choose to **Switch now** or **Switch during maintenance window**.<br><br>> **tip**<br><br><br><br>* > After initiating a minor version upgrade, the system first prepares node resources for the corresponding version. Then, it triggers a primary\-secondary switch within your selected switch time, promoting the new node to the primary.<br><br><br>* > If you choose to **Switch during maintenance window**, the instance status will immediately change to **Upgrading minor version**, and this status will persist until the task is complete, but the actual execution time of the operation task will still be within the maintenance period. For more details, refer to [Setting maintenance period](https://docs.byteplus.com/en/docs/redis/set-maintenance-period).<br> |

6. Click **OK**.

> **tip**

> When the instance status returns to **Running**, the upgrade is successful. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

## Relevant APIs

|API |Description |
|---|---|
|[DescribeDBEngineVersions](https://docs.byteplus.com/en/docs/redis/describedbengineversions) |Call the DescribeDBEngineVersions API to query list of minor versions supported by Redis major versions. |
|[ModifyDBInstanceMinorVersion](https://docs.byteplus.com/en/docs/redis/modifydbinstanceminorversion) |Call the ModifyDBInstanceMinorVersion API to upgrade target Redis instance to specified minor version. |
