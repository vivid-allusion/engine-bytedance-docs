---
title: "Modifying node specifications"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/modify-node-spec"
---

Cache for Redis supports vertical scaling (that is upgrading or downgrading node specifications), allowing you to flexibly change the node specifications of Redis instances based on business volume changes. This topic describes how to upgrade or downgrade the node specifications for Redis instance.

## Prerequisite

The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

## Precautions

* Initiating a configuration change after enabling data flashback will automatically disable the data flashback feature. After the data flashback feature is disabled, previous flashback points will no longer be retained. For more details, refer to [Setting data flashback](https://docs.byteplus.com/en/docs/redis/set-data-flashback).

* When degrading node specifications, you need to ensure that the current **Used memory** of the instance does not exceed 85% of the total new memory capacity, where total new memory capacity = modified single shard memory \* shard number. For specific procedures of checking **Used memory**, refer to [Viewing instance information](https://docs.byteplus.com/en/docs/redis/view-instance).

* During the node specification change, the instance may experience one or two temporary disconnections, each less than 30 seconds. Proceed with caution. It is recommended to perform configuration changes during off\-peak hours and ensure that the client is configured with a proper retry mechanism.

## Billing information

For details on the billing rules for changing instance configurations, refer to [Pay-as-you-go](https://docs.byteplus.com/en/docs/redis/pay-as-you-go#.5Y-Y5pu06YWN572u) and [Subscription](https://docs.byteplus.com/en/docs/redis/subscription#.5Y-Y5pu06YWN572u).

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. Select any of the following methods to access the **Modify node specification** pop\-up window and perform the relevant actions.

   * **Method 1**

      On the **Instances** page, locate the target instance, and in the **Actions** column on the right of the instance, click **Modify node specification** (available only for instances with **sharding cluster disabled**) or select  **...**  \> **Modify node specification** (available only for instances with **sharding cluster enabled**).

   * **Method 2**

      1. On the **Instances** page, click the target instance name.

      2. Find the **Configuration** pane under the **Summary** tab, and select **Modify configuration \> Modify node specification** on the right of **Instance specification**.

4. In the **Modify node specification** dialog box, configure node specifications based on your business requirements and the instance's availability zone deployment plan.

   |Parameters |Description |
   |---|---|
   |Node specification |Select to upgrade or downgrade the node specification according to business needs. For more information on specifications, refer to [Instance specifications](https://docs.byteplus.com/en/docs/redis/product-specification).<br><br>> **tip**<br><br><br>> If you need to downgrade node specifications or reduce the number of shards, you need to ensure that the current **Used memory** of the instance does not exceed 85% of the total new memory capacity, where total new memory capacity = modified single shard memory \* shard number. For specific procedures of checking **Used memory**, refer to [Viewing instance information](https://docs.byteplus.com/en/docs/redis/view-instance).<br> |
   |Additional bandwidth |If you have used additional bandwidth before changing node specifications, you can retain the additional bandwidth by checking **Additional bandwidth**. The following rules apply when retaining additional bandwidth:<br><br><br>* Total bandwidth per shard of instance = Default bandwidth of the changed node specification + Additional bandwidth.<br><br>* Additional bandwidth = min[ Current additional bandwidth per shard, Maximum additional bandwidth allowed by the changed node specification ].<br><br><br>> **tip**<br><br><br>> This parameter can only be set if the instance uses additional bandwidth before changing the node specification. For more details about additional bandwidth, refer to [Modifying bandwidth](https://docs.byteplus.com/en/docs/redis/modify-bandwidth).<br> |
   |Specifications preview |ModifyDBInstanceShardCapacity |
   |Backup |You can choose whether to perform a full backup before the specification modification.<br><br>> **warning**<br><br><br><br>* > Only Redis **primary\-secondary instances** support this configuration. Single node instances do not support backup features and cannot set this parameter.<br><br><br>* > Initiating a configuration change after enabling data flashback will automatically disable the data flashback feature. After the data flashback feature is disabled, previous flashback points will no longer be retained. You can enable data flashback manually after completing the specification modification. For more information on how to use data flashback, refer to [Setting data flashback](https://docs.byteplus.com/en/docs/redis/set-data-flashback).<br> |
   |Backup name |After checking **Make full backup before modifying configuration**, you can set a backup name for the full backup. It is an optional field. If you don't set a backup name, the backup ID will be used as the name by default.<br><br>If you want to set a backup name, the name must meet the following conditions simultaneously:<br><br><br>* It should start with a Chinese character, a letter, or an underscore (_).<br><br>* The length should be between 1 and 128 characters.<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br><br>> **tip**<br><br><br><br>* > After the backup is successfully created, you can view and download the backup on the **Backups** page. For more details, refer to [Viewin backups](https://docs.byteplus.com/en/docs/redis/view-backup).<br><br><br>* > You can also modify the backup name after the backup creates successfully. For specific procedures, refer to [Modifying backup name](https://docs.byteplus.com/en/docs/redis/modifying_the_backup_name).<br> |
   |Execution time |To perform instance configuration changing tasks, you can choose either **Execute now** or **Execution during maintainable window**.<br><br>> **tip**<br><br><br>> If you choose to perform the operation within the maintenance period, the instance status will immediately change (for example, to **Configuration modifying**) and this status will persist until the task is complete, but the actual execution time of the operation task will still be within the maintenance period. For the method to set the maintenance period, refer to [Setting maintenance period](https://docs.byteplus.com/en/docs/redis/set-maintenance-period).<br> |
   |Agreements |Read and check the relevant agreements. |
   |Risk confirmation |If the instance is a single\-node instance, you also need to read and check Risk recognition.<br><br>> **warning**<br><br><br>> Single\-node instances are not guaranteed SLAs, and this change will result in the loss of all data. Proceed with caution.<br> |

5. Complete the subsequent steps according to the billing method you have selected.

   |Billing method |Procedure |
   |---|---|
   |Pay\-as\-you\-go |After confirming the configuration fees in the lower left corner of the pop\-up window, click **OK** in the lower right corner. |
   |Subscription |1. After confirming the configuration fees in the lower left corner of the pop\-up window, click **OK** in the lower right corner.<br><br>2. On the **Confirm order information** page, confirm the order details again and then click **Next step**. |

> tip

* > If the instance status is **Configuration modifying**, it means the configuration is being changed. When the instance status shows **Running**, it means the change is successful. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

* > You can go to the **Tasks** to view the corresponding configuration change task of the instance and understand the current stage and progress details of the task. For the viewing method, refer to [Task management](https://docs.byteplus.com/en/docs/redis/task-management).

## Relevant APIs

|API |Description |
|---|---|
|[ModifyDBInstanceShardCapacity](https://docs.byteplus.com/en/docs/redis/modifydbinstanceshardcapacity) |Call the ModifyDBInstanceShardCapacity API to modify the single shard memory of a specified instance. |
|[ModifyDBInstanceShardNumber](https://docs.byteplus.com/en/docs/redis/modifydbinstanceshardnumber) |Call the ModifyDBInstanceShardNumber interface to modify the number of shards of the target Redis instance. |
