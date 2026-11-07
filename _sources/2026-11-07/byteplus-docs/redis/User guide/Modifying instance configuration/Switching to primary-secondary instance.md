---
title: "Switching to primary-secondary instance"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/switch_to_high_availability_instance"
---

Cache for Redis offers single\-node and primary\-secondary instance types. Primary\-secondary instances offer enterprise\-grade high\-availability capabilities such as persistent storage, automatic backup, cross\-availability zone disaster recovery, and read/write splitting, effectively ensuring data persistence, availability, and security. You can switch a single\-node instance to a primary\-secondary instance to meet business growth demands for a high\-availability architecture. This topic describes the procedure for changing to a primary\-secondary instance.

## Prerequisites

* The instance type is **single\-node**. For more details about instance types, refer to [Product architecture](https://docs.byteplus.com/en/docs/redis/product-component-architecture).

* The instance status is **Running**. For more details about instance status, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

## Precautions

* After a single\-node instance is switched to a primary\-secondary instance, the instance type changes, and supported features vary. For details about the feature differences between the two instance types, refer to [Feature differences](https://docs.byteplus.com/en/docs/redis/feature-faq#.5Li75aSH5a6e5L6L5ZKM5Y2V6IqC54K557G75Z6L5a6e5L6L5pSv5oyB55qE5Yqf6IO954m55oCn5pyJ5L2V5beu5Yir77yf).

* During the process of switching to a primary\-secondary instance, if you also reduce the number of shards or downgrade node specifications, ensure that the current **Used memory** of the instance does not exceed the total new memory capacity, where total new memory capacity = modified single shard memory \* shard number. For specific procedures of checking **Used memory**, refer to [Viewing instance information](https://docs.byteplus.com/en/docs/redis/view-instance).

   > **tip**

   > You can view and confirm the **Used memory** metric data of each shard on the **Server** sub\-tab under the **Monitoring** tab. For more information about how to view monitoring data, refer to [Viewing monitoring data](https://docs.byteplus.com/en/docs/redis/view-monitoring-data).

* If the single\-node instance before the change is an instance with sharding cluster enabled and a direct connection address has been applied for, then when switching to a primary\-secondary instance:

      * You cannot select to disable sharding cluster.

      * The instance's number of shards cannot exceed 8. If you need to increase the number of shards while direct connection is enabled, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support.

* During the change process, the instance might prompt the error `-TRYAGAIN The specific keys are being migrated.\r\n`, or experience one or two temporary disconnections, each less than 30 seconds. Proceed with caution. It is recommended to perform configuration changes during off\-peak hours and ensure that the client is configured with a proper retry mechanism.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance name.

4. Find the **Configuration** pane under the **Summary** tab, and select **Modify configuration \> Switch to primary\-secondary instance** on the right of **Instance specification**.

5. In the pop\-up panel, configure the instance specifications based on your business requirements.

   |Parameters |Description |
   |---|---|
   |Sharding cluster |Choose to **Enable** or **Disable** sharding clusters. For more details about sharding cluster enabled, refer to [Product architecture](https://docs.byteplus.com/en/docs/redis/product-component-architecture).<br><br>> **tip**<br><br><br>> If the single\-node instance before the change is an instance with sharding cluster enabled and a direct connection address has been applied for, then when switching to a primary\-secondary instance, it is not allowed to **disable** sharding cluster.<br> |
   |Number of shard(s) |Select the number of shards for instance with sharding cluster enabled. Specify an integer between 2 and 256.<br><br>> **tip**<br><br><br><br>* > This configuration is supported only when the **Sharding cluster** status is **Enable**.<br><br><br>* > If the single\-node instance before the change is an instance with sharding cluster enabled and a direct connection address has been applied for, then when switching to a primary\-secondary instance, the number of shards for the instance cannot exceed 8. If you need to increase the number of shards while direct connection is enabled, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support.<br><br><br>* > To downgrade the node specification or reduce the number of shards, ensure that the current **Used memory** of the instance does not exceed the total new memory capacity, where total new memory capacity = modified single shard memory x shard number. For specific procedures of checking **Used memory**, refer to [Viewing instance information](https://docs.byteplus.com/en/docs/redis/view-instance).<br> |
   |Node(s) per shard |Select the number of nodes in each shard.<br><br>Each shard of a primary\-secondary instance contains at least 2 nodes (1 primary node and 1 secondary node), and up to 6 nodes (1 primary node and 5 secondary nodes).<br><br>> **tip**<br><br><br>> For nodes with a memory capacity of 256 MiB, you can create up to four nodes per account in each region by default. To adjust the purchase quota of 256 MiB nodes (maximum is 10), refer to [Account quota](https://docs.byteplus.com/en/docs/redis/quota-and-limit#.6LSm5Y-36YWN6aKd).<br> |
   |Node specification |Select to upgrade or downgrade the node specification according to business needs. For more information on specifications, refer to [Instance specifications](https://docs.byteplus.com/en/docs/redis/product-specification).<br><br>> **tip**<br><br><br>> To downgrade the node specification or reduce the number of shards, ensure that the current **Used memory** of the instance does not exceed the total new memory capacity, where total new memory capacity = modified single shard memory x shard number. For specific procedures of checking **Used memory**, refer to [Viewing instance information](https://docs.byteplus.com/en/docs/redis/view-instance).<br> |
   |Specifications preview |ModifyDBInstanceShardCapacity |
   |Deployment plan |Complete the following actions based on the desired availability zone deployment scenario:<br><br><br>* Set up single availability zone deployment<br><br>   1. Select the Deployment plan as **Single availability zone deployment**.<br><br>   1. Select the required availability zone from the **Availability zone** drop\-down list.<br><br>* Set up multiple availability zone deployment<br><br>   1. Select the deployment plan as **Multiple availability zone deployment**.<br><br>   1. From the **Availability zone** drop\-down list, set the required availability zones for the primary node and each secondary node respectively.<br><br><br>> **tip**<br><br><br><br>* > Multiple availability zone deployment can improve availability, and at the same time, there may be a network delay of 2ms to 3ms.<br><br><br>* > For more details, refer to [Multi\-availability\-zone disaster recovery solution](https://docs.byteplus.com/en/docs/redis/multi-az-solution).<br> |
   |Execution time |To perform instance configuration changing tasks, you can choose either **Execute now** or **Execution during maintainable window**.<br><br>> **tip**<br><br><br>> If you choose to perform the operation within the maintenance period, the instance status will immediately change (for example, to **Configuration modifying**) and this status will persist until the task is complete, but the actual execution time of the operation task will still be within the maintenance period. For the method to set the maintenance period, refer to [Setting maintenance period](https://docs.byteplus.com/en/docs/redis/set-maintenance-period).<br> |
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
|[EnableDBInstanceHA](https://docs.byteplus.com/en/docs/redis/enabledbinstanceha) |Call the EnableDBInstanceHA API to switch Redis single node instance to primary\-secondary instance. |
