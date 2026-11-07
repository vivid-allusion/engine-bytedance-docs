---
title: "Modifying sharding cluster configuration"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/modify-sharding-cluster-config"
---

Cache for Redis offers two architectures: sharding cluster enabled and sharding cluster disabled. It supports converting a sharding cluster disabled instance to a sharding cluster enabled instance to meet business horizontal scaling requirements. This topic describes the procedure for enabling sharding cluster architecture for instance.

## Prerequisites

* The instance architecture is **sharding cluster disabled**. For more details on instance architecture, refer to [Product architecture](https://docs.byteplus.com/en/docs/redis/product-component-architecture).

* The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

## Precautions

* If you need to change the instance to a sharding cluster, you must wait for all multi\-key commands to complete. Executing commands during the change period may cause the change operation to fail. For more information on multi\-key commands, refer to [Limits on multiple key commands](https://docs.byteplus.com/en/docs/redis/command-limit?lang=zh#.5aSaLWtleS3lkb3ku6TpmZDliLY=).

* Once instance is changed from sharding cluster disabled to sharding cluster enabled, it cannot be reversed.

* Changing the sharding cluster status from disabled to enabled only alters the architecture of the instance, with the instance type, availability zone, connection address, and other attributes remaining unchanged.

* After changing instance with sharding cluster disabled to sharding cluster enabled, the instance architecture changes, and there will be differences in limits concerning Lua script usage, multi\-key commands, transaction commands, and other commands. For more information about command limits, refer to [Command limits](https://docs.byteplus.com/en/docs/redis/command-limit).

* During the change process, the instance might prompt the error `-TRYAGAIN The specific keys are being migrated.\r\n`, or experience one or two temporary disconnections, each less than 30 seconds. Proceed with caution. It is recommended to perform configuration changes during off\-peak hours and ensure that the client is configured with a proper retry mechanism.

* Initiating a configuration change after enabling data flashback will automatically disable the data flashback feature. After the data flashback feature is disabled, previous flashback points will no longer be retained. For more details, refer to [Setting data flashback](https://docs.byteplus.com/en/docs/redis/set-data-flashback).

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. In the **Configuration** pane under the **Summary** tab, click **Enable** next to the instance whose sharding cluster has disabled.

5. In the **Sharding cluster enabled** pop\-up window, configure the following parameters according to service requirements.

   |Parameters |Description |
   |---|---|
   |Target number of shards |You can set the number of shards according to service volume. The value can be any integer between 2 and 256. |
   |Node specification |Select the node specifications of the instance with sharding cluster enabled. You can choose to upgrade or downgrade the node specifications. For more information on specifications, refer to [Instance specifications](https://docs.byteplus.com/en/docs/redis/product-specification).<br><br>> **tip**<br><br><br>> If you want to downgrade the node specification, you need to ensure that the current **Used memory** of the instance does not exceed 85% of the total new memory capacity, where total new memory capacity = modified single shard memory \* shard number. For specific procedures of checking **Used memory**, refer to [Viewing instance information](https://docs.byteplus.com/en/docs/redis/view-instance).<br> |
   |Specifications preview |Review and confirm details of instance specifications and performance after the specification modification, including total RAM capacity, number of shards, node specification, number of nodes per shard, total bandwidth and the total number of connections. |
   |Backup |You can choose whether to perform a full backup before the specification modification.<br><br>> **warning**<br><br><br><br>* > Only Redis primary\-secondary instances support this configuration. Single node instances do not support backup features and cannot set this parameter.<br><br><br>* > Initiating a configuration change after enabling data flashback will automatically disable the data flashback feature. After the data flashback feature is disabled, previous flashback points will no longer be retained. You can enable data flashback manually after completing the specification modification. For more information on how to use data flashback, refer to [Setting data flashback](https://docs.byteplus.com/en/docs/redis/set-data-flashback).<br> |
   |Backup name |After checking **Make full backup before modifying configuration**, you can set a backup name for the full backup. It is an optional field. If you don't set a backup name, the backup ID will be used as the name by default.<br><br>If you want to set a backup name, the name must meet the following conditions simultaneously:<br><br><br>* It should start with a Chinese character, a letter, or an underscore (_).<br><br>* The length should be between 1 and 128 characters.<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br><br>> **tip**<br><br><br><br>* > After the backup is successfully created, you can view and download the backup on the **Backups** page. For more details, refer to [Viewin backups](https://docs.byteplus.com/en/docs/redis/view-backup).<br><br><br>* > You can also modify the backup name after the backup creates successfully. For specific procedures, refer to [Modifying backup name](https://docs.byteplus.com/en/docs/redis/modifying_the_backup_name).<br> |
   |Execution time |To perform instance configuration changing tasks, you can choose either Execute now or Execution during maintainable window.<br><br>> **tip**<br><br><br>> If you choose to perform the operation within the maintenance period, the instance status will immediately change (for example, to **Configuration modifying**) and this status will persist until the task is complete, but the actual execution time of the operation task will still be within the maintenance period. For the method to set the maintenance period, refer to [Setting maintenance period](https://docs.byteplus.com/en/docs/redis/set-maintenance-period).<br> |
   |Agreements |Read and check the relevant agreements. |

6. Complete the subsequent steps according to the billing method you have selected.

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
|[EnableShardedCluster](https://docs.byteplus.com/en/docs/redis/enableshardedcluster) |Call the EnableShardedCluster API to change an instance with sharding cluster disabled to an instance with sharding cluster enabled. |
