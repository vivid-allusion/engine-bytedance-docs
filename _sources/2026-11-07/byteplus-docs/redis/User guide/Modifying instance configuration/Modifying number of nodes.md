---
title: "Modifying number of nodes"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/modify-node-number"
---

Each shard in the Redis primary\-secondary instances contains one primary node and at least one secondary node. There is a replication relationship between the primary and secondary nodes. You can flexibly change the number of secondary nodes in primary\-secondary instances according to changes in service volume. This topic describes how to add or reduce nodes in a single shard.

## Prerequisite

* The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

* The instance type is the **primary\-secondary** instance. A single node instance contains one node and cannot be modified. For more details about configuration change solutions supported by different instance or architecture types, refer to [Solutions for modification of instance specifications](https://docs.byteplus.com/en/docs/redis/solutions-for-spec-modification).

## Precautions

* Initiating a configuration change after enabling data flashback will automatically disable the data flashback feature. After the data flashback feature is disabled, previous flashback points will no longer be retained. For more details, refer to [Setting data flashback](https://docs.byteplus.com/en/docs/redis/set-data-flashback).

* Adding nodes has no impact on the instance or services. When reducing nodes, the instance might experience up to 1 connection interruption, lasting within 30 seconds. Proceed with caution. It is recommended to perform configuration changes during off\-peak hours and ensure that the client is configured with a proper retry mechanism.

## Billing information

For details on the billing rules for changing instance configurations, refer to [Pay-as-you-go](https://docs.byteplus.com/en/docs/redis/pay-as-you-go#.5Y-Y5pu06YWN572u) and [Subscription](https://docs.byteplus.com/en/docs/redis/subscription#.5Y-Y5pu06YWN572u).

## Adding node

> **tip**

> Each shard of the Redis primary\-secondary instances can contain two to six nodes. When the number of nodes in a single shard of an instance reaches its upper limit, adding more nodes is not supported, and the **Add node** button will be grayed out.

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. You can choose any of the following methods to enter the **Add node** pop\-up window and perform relevant operations.

   * **Method 1**

      On the **Instances** page, find the target instance, and in the **Actions** column on the right side of the instance, select  **... \> Add node**.

   * **Method 2**

      1. On the **Instances** page, click the target instance name.

      2. Find the **Configuration** pane under the **Summary** tab, and select **Modify configuration \> Add node** on the right of **Instance specification**.

4. In the **Add node** dialog box, configure the number of nodes based on business requirements and the instance's availability zone deployment scheme.

   |Parameters |Description |
   |---|---|
   |Instance ID/Name |Confirm the ID and name of the instance for which nodes need to be added. |
   |Node configuration |Due to varying availability zone deployment plans for instance, the node configuration items that need to be configured when adding node will also differ. Among them:<br><br><br>* If the instance uses **Single availability zone deployment** plan, the following parameters must be set when adding node:<br><br>   * **Availability zone**: Confirm the instance's current availability zone.<br><br>   * **Current number of node(s)** : Confirm the number of nodes already included in each shard of the current instance.<br><br>   * **Add node**: Set the number of nodes to add.<br><br>      > **tip**<br>      <br><br>      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Each shard supports 2 to 6 nodes, meaning 2 <= (current number of nodes + number of nodes to add) <= 6.      </div><br>      <br><br>* If the instance uses **Multiple availability zone deployment** plan, set the following parameters when adding nodes:<br><br>   * **Current number of node(s)** : Confirm the number of nodes already included in each shard of the current instance.<br><br>   * **Add node**: Set the number of nodes to add.<br><br>      > **tip**<br>      <br><br>      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Each shard supports 2 to 6 nodes, meaning 2 <= (current number of nodes + number of nodes to add) <= 6.      </div><br>      <br><br>   * **Operation node**: From the **Availability zone** drop\-down list to the right of the newly added nodes, select the target availability zone for each new secondary node. |
   |Specifications preview |Review and confirm details of instance specifications and performance after the specification modification, including total RAM capacity, number of shards, node specification, number of nodes per shard, total bandwidth and the total number of connections. |
   |Backup |You can choose whether to perform a full backup before the specification modification.<br><br>> **warning**<br><br><br>> Initiating a configuration change after enabling data flashback will automatically disable the data flashback feature. After the data flashback feature is disabled, previous flashback points will no longer be retained. You may enable data flashback manually after completing the availability zone modification. For more information on how to use data flashback, refer to [Setting data flashback](https://docs.byteplus.com/en/docs/redis/set-data-flashback).<br> |
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

## Reducing node

> **tip**

> Each shard of the Redis primary\-secondary instances can contain two to six nodes. When the number of nodes in a single shard of an instance reaches the lower limit, decreasing nodes is no longer supported. On the console, the **Reduce node** button will be grayed out.

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. You can choose any of the following methods to enter the **Reduce node** pop\-up window and perform relevant operations.

   * **Method 1**

      On the **Instances** page, find the target instance, and in the **Actions** column on the right side of the instance, select  **... \> Reduce node**.

   * **Method 2**

      1. On the **Instances** page, click the target instance name.

      2. Find the **Configuration** pane under the **Summary** tab, and select **Modify configuration \> Reduce node** on the right of **Instance specification**.

4. In the **Reduce node** dialog box, configure the number of nodes based on business requirements and the instance's availability zone deployment scheme.

   |Parameters |Description |
   |---|---|
   |Instance ID/Name |Confirm the ID and name of the instance for which nodes need to be reduced. |
   |Node configuration |Due to varying availability zone deployment plans for instance, the node configuration items that need to be configured when reducing node will also differ. Among them:<br><br><br>* If the instance uses **Single availability zone deployment** plan, the following parameters must be set when reducing node:<br><br>   * **Availability zone**: Confirm the instance's current availability zone.<br><br>   * **Current number of node(s)** : Confirm the number of nodes already included in each shard of the current instance.<br><br>   * **Reduce node**: Set the number of nodes to reduce.<br><br>      > **tip**<br>      <br><br>      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Each shard supports 2 to 6 nodes, meaning 2 <= (current number of nodes + number of nodes to reduce) <= 6.      </div><br>      <br><br>* If the instance uses **Multiple availability zone deploymen**t plan, set the following parameters when reducing nodes:<br><br>   * **Current number of node(s)** : Confirm the number of nodes already included in each shard of the current instance.<br><br>   * **Select node**: Check the nodes to reduce from the node list.<br><br>      > **tip**<br>      <br><br>      > Each instance must retain at least 2 nodes, and the remaining nodes must be deployed in at least 2 different availability zones.<br>      <br><br>   * **Number of remaining node(s)** : Confirm the instance's remaining number of nodes. |
   |Specifications preview |Review and confirm details of instance specifications and performance after the specification modification, including total RAM capacity, number of shards, node specification, number of nodes per shard, total bandwidth and the total number of connections. |
   |Backup |You can choose whether to perform a full backup before the specification modification.<br><br>> **warning**<br><br><br>> Initiating a configuration change after enabling data flashback will automatically disable the data flashback feature. After the data flashback feature is disabled, previous flashback points will no longer be retained. You may enable data flashback manually after completing the availability zone modification. For more information on how to use data flashback, refer to [Setting data flashback](https://docs.byteplus.com/en/docs/redis/set-data-flashback).<br> |
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
|[IncreaseDBInstanceNodeNumber](https://docs.byteplus.com/en/docs/redis/increasedbinstancenodenumber) |Call the IncreaseDBInstanceNodeNumber API to increase the number of single shard nodes for a specified instance. |
|[DecreaseDBInstanceNodeNumber](https://docs.byteplus.com/en/docs/redis/decreasedbinstancenodenumber) |Call the DecreaseDBInstanceNodeNumber API to decrease the number of single shard nodes for target Redis instance. |
