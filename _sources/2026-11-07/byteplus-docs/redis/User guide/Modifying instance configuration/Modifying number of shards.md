---
title: "Modifying number of shards"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/modify-shard--number"
---

Cache for Redis supports horizontal scaling (by increasing or reducing the number of shards), allowing you to flexibly adjust the number of shards for Redis instances according to changes in service volume. This topic describes how to add or reduce shards for Redis instance.

## Prerequisite

* The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

* Only instances with **sharding cluster enabled** support changing the number of shards. Instances with sharding cluster disabled contain only one shard, and the number of shards cannot be changed. For more details about configuration change solutions supported by different instance or architecture types, refer to [Solutions for modification of instance specifications](https://docs.byteplus.com/en/docs/redis/solutions-for-spec-modification).

## Precautions

* For sharding cluster enabled instances with an applied direct connection address, the instance's shard count cannot exceed 8 during configuration changes. If you need to increase the number of shards while direct connection is enabled, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support.

* Initiating a configuration change after enabling data flashback will automatically disable the data flashback feature. After the data flashback feature is disabled, previous flashback points will no longer be retained. For more details, refer to [Setting data flashback](https://docs.byteplus.com/en/docs/redis/set-data-flashback).

* If you need to reduce the number of shards, make sure that the **Used memory** of each single shard in the instance after reducing the shards does not exceed 85% of the memory specification of a single shard. Otherwise, the configuration change will fail.

   > **tip**

   > You can view and confirm the **Used memory** metric data of each shard on the **Server** sub\-tab under the **Monitoring** tab. For more information about how to view monitoring data, refer to [Viewing monitoring data](https://docs.byteplus.com/en/docs/redis/view-monitoring-data).

* During the process of adding shards, the instance might prompt error `-TRYAGAIN The specific keys are being migrated.\r\n`.

* During the process of reducing shards, the instance might prompt error `-TRYAGAIN The specific keys are being migrated.\r\n`, or experience one or two temporary disconnections, each less than 30 seconds. Proceed with caution. It is recommended to perform configuration changes during off\-peak hours and ensure that the client is configured with a proper retry mechanism.

## Billing information

For details on the billing rules for changing instance configurations, refer to [Pay-as-you-go](https://docs.byteplus.com/en/docs/redis/pay-as-you-go#.5Y-Y5pu06YWN572u) and [Subscription](https://docs.byteplus.com/en/docs/redis/subscription#.5Y-Y5pu06YWN572u).

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. You can choose any of the following methods to enter the **Modify sharding number** pop\-up window and perform relevant operations.

   * **Method 1**

      On the **Instances** page, find the target instance, and in the **Actions** column on the right side of the instance, click **Modify sharding number**.

   * **Method 2**

      1. On the **Instances** page, click the target instance name.

      2. Find the **Configuration** pane under the **Summary** tab, and select **Modify configuration \> Modify shard number** on the right of **Instance specification**.

4. In the **Modify shard number** pop\-up window, configure the shard count according to your business needs and the instance's availability zone deployment plan.

   |Parameters |Description |
   |---|---|
   |Number of shard(s) |You can set the number of shards according to service volume. The value can be any integer between 2 and 256.<br><br>> **tip**<br><br><br><br>* > This configuration is supported only when the **Sharding cluster** status is **Enabled**.<br><br><br>* > If you need to reduce the number of shards, make sure that the **Used memory** of each single shard in the instance after reducing the shards does not exceed 85% of the memory specification of a single shard. Otherwise, the configuration change will fail. You can view and confirm the **Used memory** metric data of each shard on the **Server** sub\-tab under the **Monitoring** tab. For more information about how to view monitoring data, refer to [Viewing monitoring data](https://docs.byteplus.com/en/docs/redis/view-monitoring-data).<br> |
   |Specifications preview |Review and confirm details of instance specifications and performance after the specification modification, including total RAM capacity, number of shards, node specification, number of nodes per shard, estimated bandwidth and the total number of connections. |
   |Backup |You can choose whether to perform a full backup before the specification modification.<br><br>> **warning**<br><br><br><br>* > Only Redis **primary\-secondary instances** support this configuration. Single node instances do not support backup features and cannot set this parameter.<br><br><br>* > Initiating a configuration change after enabling data flashback will automatically disable the data flashback feature. After the data flashback feature is disabled, previous flashback points will no longer be retained. You can enable data flashback manually after completing the specification modification. For more information on how to use data flashback, refer to [Setting data flashback](https://docs.byteplus.com/en/docs/redis/set-data-flashback).<br> |
   |Backup name |After checking **Make full backup before modifying configuration**, you can set a backup name for the full backup. It is an optional field. If you don't set a backup name, the backup ID will be used as the name by default.<br><br>If you want to set a backup name, the name must meet the following conditions simultaneously:<br><br><br>* It should start with a Chinese character, a letter, or an underscore (_).<br><br>* The length should be between 1 and 128 characters.<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br><br>> **tip**<br><br><br><br>* > After the backup is successfully created, you can view and download the backup on the **Backups** page. For more details, refer to [Viewin backups](https://docs.byteplus.com/en/docs/redis/view-backup).<br><br><br>* > You can also modify the backup name after the backup creates successfully. For specific procedures, refer to [Modifying backup name](https://docs.byteplus.com/en/docs/redis/modifying_the_backup_name).<br> |
   |Execution time |To perform instance configuration changing tasks, you can choose either **Execute now** or **Execution during maintainable window**.<br><br>> **tip**<br><br><br>> If you choose to perform the operation within the maintenance period, the instance status will immediately change (for example, to **Configuration modifying**) and this status will persist until the task is complete, but the actual execution time of the operation task will still be within the maintenance period. For the method to set the maintenance period, refer to [Setting maintenance period](https://docs.byteplus.com/en/docs/redis/set-maintenance-period).<br> |
   |Agreements |Read and check the relevant agreements. |

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
