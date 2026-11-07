---
title: "Modifying availability zone"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/modify-az"
---

Cache for Redis provides the function to modify availability zones. Multi\-availability zone migration schemes are supported to meet the requirements of availability zone deployments in different scenarios. This topic contains instructions on how to modify availability zone.

## Prerequisite

* The instance type is the **primary\-secondary** instance. Single node instances do not support multi\-availability deployment or modification of availability zones. For details about the feature differences between the two instance types, refer to [Feature differences](https://docs.byteplus.com/en/docs/redis/feature-faq#.5Li75aSH5a6e5L6L5ZKM5Y2V6IqC54K557G75Z6L5a6e5L6L5pSv5oyB55qE5Yqf6IO954m55oCn5pyJ5L2V5beu5Yir77yf).

* The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

## Comparison of availability zone migration solutions

Cache for Redis supports various availability zone migration schemes. The table below summarizes the applicable scenarios, the outcomes of related operations, and limits concerning different availability zone migration schemes for your reference.

|Migration plan |Migrate from multiple availability zones to multiple availability zones |Migrate from a single availability zone to a single availability zone |Migrate from a single availability zone to a single availability zone |Migrate from multiple availability zones to a single availability zone |
|---|---|---|---|---|
|Applicable scenarios |Migrating a Redis instance to the availability zone to which the ECS instance belongs, and connecting ECS instance and Redis instances within the same availability zone through a private network to reduce network latency and optimally ensure security and performance. ||Migrating a Redis instance from a single availability zone to multiple availability zones can improve the disaster recovery capabilities of the instance and achieve cross\-room disaster recovery. |Meet specific functional requirements. |
|Operation impact |* When modifying the availability zone, the instance cannot be read or written for about 10 seconds. Please proceed with caution.<br><br>* The time required to modify the availability zone is affected by various factors, such as the network environment, task queue, and data size. We recommend that you perform the operation during off\-peak hours. |* When modifying the availability zone, the instance may have one to two temporary disconnections (each disconnection lasts up to 30 seconds). Please proceed with caution, and ensure that the client has the correct retry mechanism.<br><br>* The time required to modify the availability zone is affected by various factors, such as the network environment, task queue, and data size. We recommend that you perform the operation during off\-peak hours. |||
|Limits |Single\-node instances do not support modifying availability zones, and all of the above availability zone migration scenarios are not applicable to single\-node instances. For more details about single\-node instances, refer to [Product architecture](https://docs.byteplus.com/en/docs/redis/product-component-architecture). ||||

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance name.

4. In the **Basic information** pane under the **Summary** tab, click **Modifying availability zone** behind the availability zone.

5. In the **Modify availability zone** dialog box, set the availability zone deployment solution for the instance according to service requirements.

   |Parameter |Description |
   |---|---|
   |Deployment plan |Complete the following actions based on the desired availability zone deployment scenario:<br><br><br>* Set up single availability zone deployment<br><br>   1. Select the **Deployment plan** as **Single availability zone deployment**.<br><br>   2. Select the required availability zone from the **Availability zone** drop\-down list.<br><br>* Set up multiple availability zone deployment<br><br>   1. Select the **Deployment plan** as **Multiple availability zone deployment**.<br><br>   2. From the **Availability zone** drop\-down list, set the required availability zones for the primary node and each secondary node respectively.<br><br>   > **tip**<br>   <br><br>   * > If you select the same availability zone for all nodes, the instance will automatically adopt single availability zone deployment after the swap is completed.<br>   <br><br>   * > Multiple availability zone deployment can improve availability, and at the same time, there may be a network delay of 2ms to 3ms.<br>   <br><br><br>For more details, refer to [Multi-availability-zone disaster recovery solution](https://docs.byteplus.com/en/docs/redis/multi-az-solution). |
   |Backup |You can choose whether to perform a full backup before the specification modification.<br><br>> **warning**<br><br><br>> Data flashback is automatically disabled when initiating availability zone modification. After the data flashback feature is disabled, previous flashback points will no longer be retained. You may enable data flashback manually after completing the availability zone modification. For more information on how to use data flashback, refer to [Setting data flashback](https://docs.byteplus.com/en/docs/redis/set-data-flashback).<br> |
   |Backup name |After checking **Make full backup before modifying configuration**, you can set a backup name for the full backup. It is an optional field. If you don't set a backup name, the backup ID will be used as the name by default.<br><br>If you want to set a backup name, the name must meet the following conditions simultaneously:<br><br><br>* It should start with a Chinese character, a letter, or an underscore (_).<br><br>* The length should be between 1 and 128 characters.<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br><br>> **tip**<br><br><br><br>* > After the backup is successfully created, you can view and download the backup on the **Backups** page. For more details, refer to [Viewin backups](https://docs.byteplus.com/en/docs/redis/view-backup).<br><br><br>* > You can also modify the backup name after the backup creates successfully. For specific procedures, refer to [Modifying backup name](https://docs.byteplus.com/en/docs/redis/modifying_the_backup_name).<br> |
   |Execution time |To perform instance configuration changing tasks, you can choose either **Execute now** or **Execution during maintainable window**.<br><br>> **tip**<br><br><br>> If you choose to execute during a maintenance period, the instance status will change immediately, for example, change to **Scaling**, and the new status will persist until the task is completed. However, the actual execution time of the task will still be within the maintenance period.For more information on the maintenance periods, refer to . For the method to set the maintenance period, refer to [Setting maintenance period](https://docs.byteplus.com/en/docs/redis/set-maintenance-period).<br> |

6. Click **OK** on the lower\-right corner of the pop\-up window.

   > **tip**

   * > The instance status **AZ Changing** indicates that the availability zone is being modified. When the instance status changes to **Running**, it means the modification has been successfully completed. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

   * > You can go to the **Tasks** to view the corresponding configuration change task of the instance and understand the current stage and progress details of the task. For the specific procedures, refer to [Task management](https://docs.byteplus.com/en/docs/redis/task-management).

## Relevant APIs

|API |Description |
|---|---|
|[ModifyDBInstanceAZConfigure](https://docs.byteplus.com/en/docs/redis/modifydbinstanceazconfigure) |Call the ModifyDBInstanceAZConfigure to modify the availability zone of a specified instance. |
|[TestFailoverDBInstanceZone](https://docs.byteplus.com/en/docs/redis/testfailoverdbinstancezone) |Call the TestShutDownDBInstanceNodes API to simulate a specified Server or Proxy node failover for the target Redis instance. |
