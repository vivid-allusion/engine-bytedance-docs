---
title: "Creating tasks for batch volume operations"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Creating_a_batch_actions_EBS_Volume_tasks"
---

You can use the orchestration service to batch create EBS volume tasks for multiple EBS volumes, including:


* Scale up volumes: Scale up multiple volumes at the same time without losing existing data to increase storage capacity.

* Create snapshots: Back up data of multiple volumes at the same time to prevent volume data loss and improve data migration efficiency.

* Change volume configuration: Change the configuration of multiple volumes at the same time to meet business requirements.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have completed [preparations](https://docs.byteplus.com/en/docs/ecs/Preparation).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure 


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, click "Maintenance & Monitoring \> Orchestration".

3. In the top menu bar, select the region where your business is located.

4. On the "CloudOps Orchestration" page, click the "Common tasks" tab.

5. Click the "Batch operations on EBS volumes" menu.

6. Click the "Create task" button and configure the parameters described in the following table.

   
   <Tabs>
   <Tab zoneid="XuTV8Ds68j" title="Scale up volumes">
   <TabTitle>Scale up volumes</TabTitle>
   
   If the current volume capacity is insufficient to store large amounts of business data, you can scale up multiple volumes at the same time to increase storage capacity without losing existing data.
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   
   * <div data-tips="true" data-tips-type="default">The volumes must be in the <strong>Available</strong> or <strong>Is mounted</strong> status. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Attach-a-volume">Mounting volumes</a>.</div>
   
   
   * <div data-tips="true" data-tips-type="default">To prevent volume data loss, we recommend that you use snapshots to back up your data before you scale up the volumes. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot">Creating snapshots</a>.</div>
   
   
   * <div data-tips="true" data-tips-type="default">After you scale up volumes, scaling down is not supported. We recommend that you plan your storage capacity (volume capacity) appropriately.</div>
   
   
   * <div data-tips="true" data-tips-type="default">For more information about EBS volume scaling up, including Precautions and Before you begin, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Overview-of-extending-volume">EBS volume scaling up overview</a>.</div>
   
   
   
   
   |**Parameter​**  |**Description** |**Sample value** |
   |---|---|---|
   |**Select task type** |||
   |Type |Select the type of O&M command that you want to execute. |Scale up volume |
   |**Select volumes** |||
   |Select volume |Determine volumes that meet batch operation requirements based on information such as volume name or ID, running status, and status. You can select multiple volumes.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can select up to 500 volumes.</div><br> |\- |
   |**Set capacity**<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The maximum capacity of the system volume is 2048 GiB, and the maximum capacity of a data volume is 32,768 GiB.</div><br> |||
   |Batch set target capacity |If the capacity of the selected volumes is the same after scaling\-up, you can specify the capacity for all selected volumes in a batch.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">After you specify the capacity for all selected volumes in a batch, you can also adjust the capacity of individual volumes in the volume list. The target capacity specified for each individual volume in the list takes precedence.</div><br> |61GiB |
   |Specify individual target capacity |In the "Target capacity" column of the target volume, specify the new capacity for the volume after scaling\-up. |\- |
   
   
   
   
   
   </Tab>
   <Tab zoneid="Ng898xHx1Q" title="Create Snapshot">
   <TabTitle>Create Snapshot</TabTitle>
   
   You can create snapshots for existing system volumes and data volumes at the same time to back up data.
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   
   * <div data-tips="true" data-tips-type="default">As of September 18, 2024, the snapshot feature is commercialized, and usage incurs charges. For precautions, prerequisites, and other information about creating snapshots, see <a href="https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot">Creating snapshots</a>.</div>
   
   
   * <div data-tips="true" data-tips-type="default">You can create snapshots for multiple volumes at the same time only when the volumes are in the <strong>Is mounted</strong> or <strong>Available</strong> status. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Attach-a-volume">Mounting volumes</a>.</div>
   
   
   * <div data-tips="true" data-tips-type="default">To ensure the integrity of snapshot data, we recommend that you stop the instance before creating a snapshot, or synchronize the application and file system cache data to the EBS volume before creating a snapshot. For database, the Flush&Lock Table action is recommended; and for file systems, the Sync action is recommended. For specific actions, please  <a href="https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot">view details</a>.</div>
   
   
   
   
   |**Parameters** |**Description** |**Sample value** |
   |---|---|---|
   |**Select task type** |||
   |Type |Select the type of O&M command that you want to execute. |Create snapshots |
   |Snapshot retention time |Specify the retention period for snapshots. The default retention period is one day. You can permanently retain snapshots or specify a custom retention period. You can specify a custom snapshot retention period ranging from 1 to 65,536 days.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The snapshot retention period starts from the moment the snapshot is created.</div><br> |1 day |
   |**Select volume** |||
   |Select volume |Determine target volumes that meet batch operation requirements based on information such as volume name or ID, and status. You can select multiple volumes at the same time.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can select up to 500 volumes.</div><br> |\- |
   
   
   
   
   
   </Tab>
   <Tab zoneid="Ry41Lj30OJ" title="EBS Volume reconfiguration">
   <TabTitle>EBS Volume reconfiguration</TabTitle>
   
   When your business undergoes adjustments and your volume performance requirements change significantly, you can change the volume configuration to meet your business requirements.
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   
   * <div data-tips="true" data-tips-type="default">Several hours may be required to complete a volume configuration change task. We recommend that you initiate such tasks during off\-peak hours.</div>
   
   
   * <div data-tips="true" data-tips-type="default">Only when the EBS volume status is <strong>mounted</strong>, <strong>available</strong>, is modifying the EBS volume specification supported, and the specification of the instance to which the EBS volume is mounted must support the modified EBS volume. Learn more about <a href="https://docs.byteplus.com/en/docs/ecs/Modify-volume-type#.5rOo5oSP5LqL6aG5">Precautions for Modify Instance Spec</a>.</div>
   
   
   
   
   |**Parameter​**  |**Description** |**Sample value** |
   |---|---|---|
   |**Select task type** |||
   |Type |Select the type of task for which you want to execute O&M commands. |Change volume configuration |
   |Configuration change type |Select the type of change you want to perform. Valid values:<br><br><br>* **Upgrade**: If your business data capacity and access requests increase, you can upgrade the volume specifications.<br><br>* **Downgrade**: If your instance type configuration exceeds your actual business requirements, you can downgrade the volume specifications to reduce costs. |Upgrade |
   |Configuration change plan |Select a volume configuration change plan.<br><br><br>* Configuration upgrade plans:<br><br>   * Ultra_Disk changed to ESSD_PL0<br><br>   * Ultra_Disk changed to ESSD_FlexPL<br><br>   * ESSD_PL0 changed to ESSD_FlexPL<br><br>   * ESSD_PL1 changed to ESSD_FlexPL<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Upgrade plans are provided based on the specifications of the original volumes. The actual plans displayed in the console prevail.   </div><br>   <br><br>* Configuration downgrade plans:<br><br>   * ESSD_PL0 changed to Ultra_Disk<br><br>   * ESSD_PL1 changed to Ultra_Disk<br><br>   * ESSD_PL1 changed to ESSD_PL0<br><br>   * ESSD_FlexPL changed to Ultra_Disk<br><br>   * ESSD_FlexPL changed to ESSD_PL0<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Downgrade plans are provided based on the specifications of the original volumes. The actual plans displayed in the console prevail.   </div><br>    |ESSD_PL0 changed to ESSD_FlexPL |
   |**Select volume** |||
   |Select volume |Determine target volumes that meet batch operation requirements based on information such as volume name or ID and status. You can select multiple volumes.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can select up to 500 volumes.</div><br> |\- |
   
   
   
   
   
   </Tab>
   </Tabs>
   

7. Refer to the table below, and set concurrency control and related information.

   
   |**Parameters** |**Description** |**Sample value** |
   |---|---|---|
   |**Concurrency control** |||
   |Concurrency rate |* Specify the number of concurrent executions for a batch instance task, which refers to the maximum number of instances that can undergo operations or receive requests at the same time. For example, if you have 50 instances and set this parameter to 10, the task will be executed in 5 batches, and commands will be sent to 10 instances simultaneously in each batch.<br><br>* Value range: 1\-100. |10 |
   |Maximum error count |Specify the maximum error count or percent allowed when batch EBS volume tasks are performed within a certain operation or scope.<br><br><br>* **Number of errors:**  Generally applicable to scenarios where attention to the number of errors is required; the value range is 0\-100.<br><br>   * If the error count is set to 0, no errors are allowed. That is, if an error occurs even once while performing a task, the entire task will stop (fail).<br><br>   * If the error count is set to 100, a maximum of 100 errors is allowed. That is, as long as the number of errors during the execution of a task does not exceed 100, the task will succeed, but if errors exceed 100 before the task is completed, the entire task will stop (fail).<br><br>      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The next step is allowed to proceed only when the actual number of failures across all batches of the task is less than or equal to the maximum number of errors you specify.      </div><br>      <br><br>* **Percent: ** Applicable to scenarios where the impact of errors on the entire task needs attention. Value range: 0\-100%.<br><br>   * If the maximum error percent is set to 0%, no errors are allowed. That is, if an error occurs even once while performing a task, the entire task will stop (fail).<br><br>   * If the maximum error percent is set to 100%, the task will succeed regardless of the number of errors.<br><br>      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The next step is allowed to proceed only when the actual failure rate (percentage of failed instances) across all batches of the task is less than or equal to the maximum error rate (percentage) you specify.      </div><br>       |Error quantity: 1<br><br> |
   |**Relevant information** |||
   |Project |You can add the cloud assistant to the project and manage it uniformly by project dimension, which helps maintain resource independence and ensure data security. For more information about projects, see [Project management](https://docs.byteplus.com/en/docs/ecs/Managing-projects). |default |
   |Tag |A tag is a key\-value pair used to identify resources. Tags help you categorize resources based on different dimensions, such as purpose, owner, or environment. This allows you to search and aggregate your resources. For more information about tags, see [Tag management](https://docs.byteplus.com/en/docs/ecs/Tag-overview). |Key1:Value1 |
   

8. Click "Create".

9. After you confirm that the information to be configured is correct, click the "Confirm" button to immediately start task execution.

   > The selected task is executed on the selected volumes, which has a wide\-ranging impact. Confirm that all information is correct before you submit the request.   
   

10. (**Only applicable to EBS volume scaling up tasks**) After the EBS volume scaling up is complete, please [log in to the instance](https://docs.byteplus.com/en/docs/ecs/Overview-1) to perform scaling up of the partition and file system. About [Linux partition and file system scaling up](https://docs.byteplus.com/en/docs/ecs/Extend-volume-linux), Windows partition and file system scaling up.


<span id="4tAkUDv4"></span>
## Execution results


|Feature |Description |
|---|---|
|Scale up volume |After the task is **executed successfully**, you can click the names of the target volumes on the "Volumes" page and view the scaled\-up capacity of the volumes on the "Overview" tab. |
|Create snapshots |After the task is **executed successfully**, you can [view the created snapshots](https://docs.byteplus.com/en/docs/ecs/View-a-snapshots) in the snapshot list or by using the snapshot chains of the volumes. |
|Change volume configuration |After the task is **executed successfully**, you can see that the configurations of the volumes are changed on the "Volumes" page. |
