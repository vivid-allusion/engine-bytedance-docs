---
title: "Task management"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/task-management"
---

Cache for Redis adds task function, which supports viewing the status, progress, start and end time, and time consumption of tasks related to creating instances, restoring data to new instances, changing instance configurations, and restarting instances in the task center. It is convenient for you to view task details in real time during the above operations and improve operation and maintenance management efficiency.

## Supported tasks

Cache for Redis supports viewing task details listed in the table below in the **Tasks**. When you initiate tasks listed in the table below on the console, the task center will display the details of the corresponding tasks in real\-time, including task status, current task stage, and other information.

|Task name |Task type |Included task stages |
|---|---|---|
|[CreateDBInstance](https://docs.byteplus.com/en/docs/redis/createdbinstance) |[Creating instance](https://docs.byteplus.com/en/docs/redis/create-instance) |1. Task initialization<br><br>2. Resource preparation<br><br>3. Configuration modification<br><br>4. Task success |
|CreateInstanceInner |* [Recovery from backup set](https://docs.byteplus.com/en/docs/redis/recovery-from-backup-set#.5oGi5aSN5Yiw5paw5a6e5L6L77yI5o6o6I2Q77yJ)<br><br>* [Recovery by time point](https://docs.byteplus.com/en/docs/redis/recovery-by-time-point#.5oGi5aSN5Yiw5paw5a6e5L6L77yI5o6o6I2Q77yJ)<br><br>* [Restoring deleted instance](https://docs.byteplus.com/en/docs/redis/restore-deleted-instance) |1. Task initialization<br><br>2. Resource preparation<br><br>3. Backup<br><br>4. Data cleanup<br><br>5. Import backup<br><br>6. Task success |
||[Purchasing instance with same configuration](https://docs.byteplus.com/en/docs/redis/purchase-same-config-instance) |1. Task initialization<br><br>2. Resource preparation<br><br>3. Configuration modification<br><br>4. Task success |
|[IncreaseDBInstanceNodeNumber](https://docs.byteplus.com/en/docs/redis/increasedbinstancenodenumber) |[Adding node](https://docs.byteplus.com/en/docs/redis/modify-node-number#.5aKe5Yqg6IqC54K55pWw) |1. Task initialization<br><br>2. Node addition<br><br>3. Task success |
|[DecreaseDBInstanceNodeNumber](https://docs.byteplus.com/en/docs/redis/decreasedbinstancenodenumber) |[Reducing node](https://docs.byteplus.com/en/docs/redis/modify-node-number#.5YeP5bCR6IqC54K55pWw) |1. Task initialization<br><br>2. Node deletion<br><br>3. Task success |
|[ModifyDBInstanceShardNumber](https://docs.byteplus.com/en/docs/redis/modifydbinstanceshardnumber) |[Adding shard](https://docs.byteplus.com/en/docs/redis/modify-shard--number) |1. Task initialization<br><br>2. Backing up<br><br>3. Shard addition<br><br>4. Data rebalance<br><br>5. Task success |
||[Reducing shard](https://docs.byteplus.com/en/docs/redis/modify-shard--number) |1. Task initialization<br><br>2. Data rebalance<br><br>3. Shard removal<br><br>4. Task success |
|[ModifyDBInstanceShardCapacity](https://docs.byteplus.com/en/docs/redis/modifydbinstanceshardcapacity) |[Modifying node specifications](https://docs.byteplus.com/en/docs/redis/modify-node-spec) |1. Task initialization<br><br>2. Backing up<br><br>3. Node spec change<br><br>4. Configuration modification<br><br>5. Task success |
|[EnableShardedCluster](https://docs.byteplus.com/en/docs/redis/enableshardedcluster) |[Modifying sharding cluster configuration](https://docs.byteplus.com/en/docs/redis/modify-sharding-cluster-config) |1. Task initialization<br><br>2. Instance migration<br><br>3. Configuration modification<br><br>4. Task success |
|[ModifyDBInstanceAZConfigure](https://docs.byteplus.com/en/docs/redis/modifydbinstanceazconfigure) |[Modifying availability zone](https://docs.byteplus.com/en/docs/redis/modify-az) |1. Task initialization<br><br>2. Modifying availability zone<br><br>3. Task success |
|[RestartDBInstance](https://docs.byteplus.com/en/docs/redis/restartdbinstance) |[Restart instance](https://docs.byteplus.com/en/docs/redis/restart-instance) |1. Task initialization<br><br>2. Restarting<br><br>3. Task success |
|[RestoreDBInstance](https://docs.byteplus.com/en/docs/redis/restoredbinstance) |Restore backup to source instance<br><br> |1. Resource preparation<br><br>2. Backup<br><br>3. Data cleanup<br><br>4. Import backup<br><br>5. Task success |

## Precautions

Only supports viewing tasks created within the last 30 days in **Tasks**.

For example, the current time is August 2, 2024, so all tasks created between July 4, 2024 00:00:00 and August 2, 2024 23:59:59 are supported to view.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance involved in the task belongs.

3. In the left navigation pane, select **NoSQL Database \> Redis \> Tasks**.

4. On the **Tasks** list page, you can perform the following operations:

   |Classification of actions |Description |
   |---|---|
   |View tasks |You can view information about the task in the task list, including:<br><br><br>* The **Instance name/ID** of the instances involved in the task, **Task name/ID**, **Task status**, and **Start and end time/time consumption** of the task.<br><br>   Hover over the percentage of a specific status in the **Task status** column to view the task phases included in the current task and the status of each phase.<br><br> <br><br>* You can also click **Details** in the right\-hand panel to enter the **Task information** page for the current task.<br><br>   On the **Task information** page, you can view the following information:<br><br>   * Basic information<br><br>      Includes **Instance ID**, **Instance name**, **Task name**, **Task status**, **Task ID**, **Creation time**, **Start and end time**, and **Task time** information related to task.<br><br>      > **tip**<br>      <br><br>      > If you choose to execute during the maintenance period when initiating tasks such as [Restarting instance](https://docs.byteplus.com/en/docs/redis/restart-instance) or tasks related to instance specification changes (including [Modifying number of nodes](https://docs.byteplus.com/en/docs/redis/modify-node-number), [Modifying number of shards](https://docs.byteplus.com/en/docs/redis/modify-shard--number), [Modifying node specifications](https://docs.byteplus.com/en/docs/redis/modify-node-spec), [Modifying sharding cluster configuration](https://docs.byteplus.com/en/docs/redis/modify-sharding-cluster-config) and [Modifying availability zone](https://docs.byteplus.com/en/docs/redis/modify-az)), then **Creation time** is the time you initiated the task, and the **Start and end time** is the actual start and end time of the task.<br>      <br><br>   * Configuration<br><br>      Includes **Product type**, **Database version**, and instance **Specification** information.<br><br>      > **tip**<br>      <br><br>      > If the current task is related to instance specification changes (including [Modifying number of nodes](https://docs.byteplus.com/en/docs/redis/modify-node-number), [Modifying number of shards](https://docs.byteplus.com/en/docs/redis/modify-shard--number), [Modifying node specifications](https://docs.byteplus.com/en/docs/redis/modify-node-spec), [Modifying sharding cluster configuration](https://docs.byteplus.com/en/docs/redis/modify-sharding-cluster-config) and [Modifying availability zone](https://docs.byteplus.com/en/docs/redis/modify-az)), you can also view the specification comparison information before and after the instance change when the task starts executing.<br>      <br><br>   * Task progress<br><br>      Includes all the **Task phase** of the current task, as well as the current **Status** of each phase. |
   |Filter tasks |Above the task list, you can quickly filter eligible tasks using the following fields:<br><br><br>* Instance name: Fuzzy filter. Only one keyword is supported to filter at a time.<br><br>* Instance ID: Exact filter. Only one instance ID is supported for filtering at a time.<br><br>* Task name: Fuzzy filter. Only one keyword is supported to filter at a time.<br><br>* Creation time: Filter by the task's creation time. By default, tasks created within the last 30 days are displayed.<br><br>   > **tip**<br>   <br><br>   > Only supports viewing tasks created within the last 30 days in **Tasks**.<br>    |
