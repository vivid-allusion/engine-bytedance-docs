---
title: "Add nodes for batch instances"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/adding_nodes_in_batches"
---

RDS for MySQL supports adding nodes to instances in batches. This topic describes the corresponding steps.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The instances have been created and are in the **Running** status. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Adding nodes to single\-node instances is not supported.

* Batch changes are only supported for instances with the same instance type, storage type, billing method, specification type, number of nodes, database version, availability zones, and storage space.

* Only adding read\-only nodes to instances is supported, not deleting nodes.

* Up to 50 instances are supported for batch change specifications.

* If read/write separation with a round\-robin scheduling policy is enabled for a double\-node instance, the scheduling weight is automatically recalculated based on the new instance specification after the configuration is modified. You can view the new weight on the **Connectivity** page. To modify, refer to [Setting the read/write separation policy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_read-write_splitting_policies).

* During the process of changing the configuration, the instance page may display an exception, so you can refresh the page later and retry.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the project to which the instance belongs is not set, this operation should select the project as <strong>All resources</strong>.</div>



3. On the **Instances** page, select multiple target instances.

4. In the lower\-left corner of the **Instances** page, choose **Modify configuration \> Add node**.

5. On the **Batch add node** page, complete the following configuration based on your business requirements and confirm the impacts and risks of adding nodes.

   
   |Parameter |Description |
   |---|---|
   |Node specification |Add nodes to the instance and set their specifications and availability zones.<br><br><br>* If the instance type is **Double node**:<br><br>   * An instance can have up to 10 read\-only nodes.<br><br>   * You can set the specifications for new read\-only nodes as needed.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">However, it should be noted that when the specifications of the read\-only nodes are lower than those of the primary node, there may be a delay in the read\-only nodes or even an OOM (Out of Memory) situation for the read\-only nodes due to the high load on the primary node. It is recommended to select the same or a higher specification for the read\-only nodes as that of the primary node.   </div><br>   <br><br>   * Primary, secondary, and read\-only nodes can be deployed in up to three availability zones.<br><br>* If the instance type is **Multiple node**:<br><br>   * The secondary node specifications must be consistent with the primary node specifications.<br><br>   * An instance can have a maximum of 8 secondary nodes.<br><br>   * Nodes can be distributed in at most 3 availability zones. |
   |Switch time |Select the switch time of the change. You can select **Execute now**, **Specific time period**, or **Maintenance window**.<br><br><br>* **Execute now**: Execute immediately after submitting the instance specification modification order.<br><br>* **Specific time period**: Perform the specification change within the specified time period.<br><br>* **Maintenance window**: Execute within the maintenance period set for the instance. You can view the maintenance period currently set for the instance on the summary page. For any adjustment, refer to [Configuring maintenance window](https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you choose to perform the configuration change in the maintenance window, RDS for MySQL will immediately perform resource scheduling, data synchronization and other prerequisite actions after the change order is submitted, and switch the instance status to Changing. When it comes to the maintenance time, switch the route. After the task execution is completed, the instance status changes to Running.</div><br> |
   |Specific time period |If you select **Specific time period**, you need to set the time period for the specification change.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Time periods cannot be set across days.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The shortest time period is two hours.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Set the time period within the time range indicated in the console.</div><br> |
   |Maintenance window |If you choose to modify the configuration during the **Maintenance window**, you need to confirm the instance's **maintenance window**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can click <strong>Edit</strong> to modify the maintenance window of the instance. For detailed rules on setting maintenance window, see <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period">Configuring maintenance window</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After a task is initiated, you can still modify the instance's maintenance window, but the execution time of the initiated task will not be automatically adjusted with the modification of the maintenance window. If you need to adjust the execution time of a task, you need to manually schedule and adjust it at Task center. For more information about modifying tasks execution time, see <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/changing_the_execution_time_of_a_task">Changing the execution time of a task</a>.</div><br> |
   |Risk Identification |Risks to the database proxy service after modifying the instance specification.<br><br>Not all specification change operations require risk identification. If some or all instances in a batch have the database proxy service enabled, and the current number of proxy CPU cores is less than half the total CPU cores of all serviceable nodes after the configuration change, the system will prompt you to expand the database proxy resources to handle higher database traffic. Click **View expansion details** in the prompt. The **Recommended instances for expansion** list will appear in a pop\-up window, showing the instances that require expansion, their current number of proxy cores, and the recommended number of proxy cores. On the Batch specification change page, complete the following configurations based on business requirements and confirm the impact of changing the instance specifications. For more information about modifying database proxy service resources, refer to [Modify proxy configuration](https://docs.byteplus.com/en/docs/RDS_for_MySQL/changing_agent_configurations). |
   

6. Click **Confirm order**.

7. Complete the subsequent steps based on the billing type selected.

   * If **Pay\-as\-you\-go** is selected: on the **Confirm order** page, confirm the order details, read and check the **Database Product and Service terms** and **Unsubscribe rules**, and click **Buy now**.

   * If the instance is a **Subscription** instance: on the **Confirm order** page, confirm the order details, read and check **Database Products and Services Terms** and **Unsubscription rules**, and click **Submit order**.

8. In the pop\-up **Batch cancel** dialog box, view **Task progress**, and click **OK** after all tasks are completed.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can click the <strong>Terminate</strong> button in the <strong>Batch cancel</strong> dialog box, and the task of the instance that has not started changing after termination will no longer proceed and cannot be resumed. If you want to make changes again, you need to re\-initiate the batch task.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the task fails, hover the cursor on <strong>Failed</strong> in the <strong>Execution result</strong> column to view the causes of failure. You can also click the <strong>Retry</strong> button in the <strong>Actions</strong> column for an instance to re\-initiate the modification, or click <strong>Batch retry</strong> to re\-initiate the modification for all failed instances.   </div>
