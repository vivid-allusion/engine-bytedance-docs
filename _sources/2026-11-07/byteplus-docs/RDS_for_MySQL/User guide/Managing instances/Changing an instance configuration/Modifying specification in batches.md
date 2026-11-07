---
title: "Modifying specification in batches"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_instance_specification_in_batches"
---

This topic describes how to batch modify instance specifications.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An instance is created and in the **Running** state. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Batch modification is only supported for instances that have the same instance type, storage type, billing method, specification type, number of nodes, database version, availability zones, and storage space range.

* Batch modifying the instance specification only supports the specification upgrade, specification downgrade, and storage expansion.

* Up to 50 instances are supported for batch change specifications.

* If read/write separation with a round\-robin scheduling policy is enabled for a double\-node instance, the scheduling weight is automatically recalculated based on the new instance specification after the configuration is modified. You can view the new weight on the **Connectivity** page. To modify, refer to [Setting the read/write separation policy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_read-write_splitting_policies).

* During the process of changing the configuration, the instance page may display an exception, so you can refresh the page later and retry.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.</div>



3. On the **Instances** page, select multiple target instances.

4. In the lower\-left corner of the **Instances**, choose **Modify configuration** \> **Change specification**.

5. On the **Batch specification change** page, complete the following configurations based on business requirements and confirm the impact of changing the instance specifications.

   
   |Parameter |Description |
   |---|---|
   |Storage type |Select the storage type for the instance. RDS for MySQL provides four storage types: **local SSD, Cloud ESSD FlexPL, Cloud ESSD PL0**, and **High performance cloud disk**. The options for changing the storage type depend on the instance's current storage type. The rules are as follows:<br><br><br>* If the instance storage type is Local SSD, you can change the storage type to any cloud disk type.<br><br>* If the instance storage type is Cloud ESSD FlexPL, you can change the storage type to High performance cloud disk.<br><br>* If the instance storage type is Cloud ESSD PL0, you can change the storage type to Cloud ESSD FlexPL and High performance cloud disk.<br><br>* If the instance specification type is General type (ARM), the storage type can only be local SSD. |
   |Node specification |Set the specification for each node.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The initial value of the node specification displayed on the <strong>Batch specification change</strong> page is the specification information for the first instance you selected.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the read\-only node specification is lower than the primary node specification, the read\-only node may be delayed or even OOM due to high load on the primary node. it is recommended that the read\-only node be selected with the same or higher specification as the primary node.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For multiple node instances, the specifications of secondary nodes automatically match those of the primary node.</div><br> |
   |Storage space |Set the storage space for the instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The lower limit of storage space displayed on the <strong>Batch specification change</strong> page is the maximum value of storage space for the selected instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The storage space can be set from 20 GiB to 32000 GiB in increments of 10 GiB. For more information on the value range of storage space corresponding to each specification, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications">Product specifications</a>.</div><br> |
   |Switch time |Select the switch time of the change. You can select **Execute now**, **Specific time period**, or **Maintenance window**.<br><br><br>* **Execute now**: Execute immediately after submitting the modification order.<br><br>* **Specific time period**: Perform the specification change within the specified time period.<br><br>* **Maintenance window**: Execute within the maintenance window set for the instance. You can view the currently set maintenance window for your instance on the Summary page. To adjust, see [Configuring maintenance window](https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Multiple node instances currently only support <strong>Execute now</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you choose to perform the configuration change in the maintenance window, RDS for MySQL will immediately perform resource scheduling, data synchronization and other prerequisite actions after the change order is submitted, and switch the instance status to Changing. When it comes to the maintenance time, switch the route. After the task execution is completed, the instance status changes to Running.</div><br> |
   |Specific time period |If you select **Specific time period**, you need to set the time period for the specification change.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Time periods cannot be set across days.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The minimum time period is two hours.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Set the time period within the time range indicated in the console.</div><br> |
   |Maintenance window |If you choose to modify the configuration during the **Maintenance window**, you need to confirm the instance's **maintenance window**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can click <strong>Edit</strong> to modify the maintenance window of the instance. For detailed rules on setting maintenance window, see <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period">Configuring maintenance window</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After a task is initiated, you can still modify the instance's maintenance window, but the execution time of the initiated task will not be automatically adjusted with the modification of the maintenance window. If you need to adjust the execution time of a task, you need to manually schedule and adjust it at Task center. For more information about modifying tasks execution time, see <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/changing_the_execution_time_of_a_task">Changing the execution time of a task</a>.</div><br> |
   |Risk Identification |Risks to the database proxy service after modifying the instance specification.<br><br>Not all specification change operations require risk identification. If some or all instances in a batch have the database proxy service enabled, and the current number of proxy CPU cores is less than half the total CPU cores of all serviceable nodes after the configuration change, the system will prompt you to expand the database proxy resources to handle higher database traffic. Click **View expansion details** in the prompt. The **Recommended instances for expansion** list will appear in a pop\-up window, showing the instances that require expansion, their current number of proxy cores, and the recommended number of proxy cores. On the Batch specification change page, complete the following configurations based on business requirements and confirm the impact of changing the instance specifications. For more information about modifying database proxy service resources, refer to [Modify proxy configuration](https://docs.byteplus.com/en/docs/RDS_for_MySQL/changing_agent_configurations). |
   

6. Click **Confirm order**.

7. Complete the subsequent steps based on the billing type selected.

   * If **Pay\-as\-you\-go** is selected: on the **Confirm order** page, confirm the order details, read and check the **Database Product and Service terms** and **Unsubscribe rules**, and click **Buy now**.

   * If the instance is a **Subscription** instance: on the **Confirm order** page, confirm the order details, read and check **Database Products and Services Terms** and **Unsubscription rules**, and click **Submit order**.

8. In the pop\-up **Batch cancel** dialog box, view **Task progress**, and click **OK** after all tasks are completed.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can click the <strong>Terminate</strong> button in the <strong>Batch cancel</strong> dialog box, and the task of the instance that has not started changing after termination will no longer proceed and cannot be resumed. If you want to make changes again, you need to re\-initiate the batch task.</div>


* <div data-tips="true" data-tips-type="tip">If the task fails, hover the cursor on <strong>Failed</strong> in the <strong>Execution result</strong> column to view the causes of failure. You can also click the <strong>Retry</strong> button in the <strong>Actions</strong> column for an instance to re\-initiate the modification, or click <strong>Batch retry</strong> to re\-initiate the modification for all failed instances.</div>
