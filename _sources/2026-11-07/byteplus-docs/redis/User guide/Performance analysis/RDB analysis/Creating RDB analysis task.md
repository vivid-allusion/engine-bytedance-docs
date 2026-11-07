---
title: "Creating RDB analysis task"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/create-rdb-analysis-task"
---

Cache for Redis supports RDB analysis, which helps you understand the memory usage, distribution, expiration time, and other information of keys, providing data reference for you to optimize big Keys. This topic describes how to create RDB analysis task on the Redis console.

## Prerequisites

* No RDB analysis task is in progress under the current instance.

* The instance type is the **Primary\-secondary** instance. Single\-node instances do not support backup and restore functionality. For details about the feature differences between the two instance types, refer to [Feature differences](https://docs.byteplus.com/en/docs/redis/feature-faq#.5Li75aSH5a6e5L6L5ZKM5Y2V6IqC54K557G75Z6L5a6e5L6L5pSv5oyB55qE5Yqf6IO954m55oCn5pyJ5L2V5beu5Yir77yf).

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click the **Performance analysis** tab.

5. Click the **RDB Analysis** sub\-tab.

6. Under the **RDB analysis** sub\-tab, click **Create analysis task**.

7. In the pop\-up dialog box, configure the following parameters.

   |Parameters |Description |
   |---|---|
   |Analysis method |Select the backup file analysis method adopted for the current RDB analysis task. The following analysis methods are supported:<br><br><br>* **Backup now**: A new backup file is created for analysis.<br><br>* **Select history backup**: An existing backup set is used for analysis.<br><br><br>> **tip**<br><br><br>> When creating a backup, the Cache for Redis will preferentially pull data from the secondary node of the instance for backup. If there is no available secondary node for instance, it will pull data from the primary node for backup. During the backup period, it may cause a short\-term increase in instance access latency. It is recommended to perform backup\-related operations during off\-peak business hours. For more details, refer to [Data backup](https://docs.byteplus.com/en/docs/redis/backup-recovery-intro#.5pWw5o2u5aSH5Lu9).<br> |
   |Select history backup |Select the target backup set from the drop\-down list.<br><br>> **tip**<br><br><br>> This parameter is only required when the **Analysis method** is set to **Select history backup**.<br> |
   |Select shard to analysis |In the **All shard(s)**  box on the left, check the shard(s) to be analyzed, and the selected shard(s) will be automatically moved to the **Selected shard(s)**  box on the right.<br><br>> **tip**<br><br><br><br>* > You can select **All shard(s)** to analyze all shards under the current instance.<br><br><br>* > In the **Selected shard(s)** box, click![](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d44ce8503cb70b4cbd298fdc11d3eece.png)icon to the right of the target shard to delete this shard. You can also click![](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_780fa292e1f1e020b9db018da34cb501.jpg)icon on the upper\-right corner of the Selected shard(s) box to delete all selected shards.<br> |
   |Delimiter(s) |Set the delimiter used to identify the key prefix. The following characters are allowed as delimiters:<br><br>```Plain Text```<br>```:;,_-+@=!#```<br><br><br>> **tip**<br><br><br><br>* > You can pass in one or more of the above characters as delimiters. No symbols are needed to separate multiple characters.<br><br><br>* > If this configuration is left blank, all the above characters will be used as delimiters by default.<br> |

8. Click **OK** in the lower\-right corner.

   > **tip**

   > After successfully creating an RDB analysis task, you can view the serial number, status, and progress of the current task in the analysis task list.
