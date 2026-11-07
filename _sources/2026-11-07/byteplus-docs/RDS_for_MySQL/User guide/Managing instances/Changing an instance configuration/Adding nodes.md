---
title: "Adding nodes"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/adding_nodes"
---

This topic describes how to add nodes to an RDS for MySQL instance.

<span id=".6LS555So6K-05piO"></span>
## Billing

For information about fees for adding nodes to an instance, refer to [Subscription cancellation or instance specification modification.](https://docs.byteplus.com/en/docs/RDS_for_MySQL/subscription_cancellation_or_instance_specification_modification).

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* You cannot add nodes to a single\-node instance.

* Modifying the configuration may automatically trigger data migration, which can cause a database interruption or transient disconnection. While the instance configuration is being modified, most operations related to databases, accounts, and networks cannot be performed.

* You do not need to manually restart the instance after modifying the configuration. The change takes minutes, and the duration depends on the number of nodes of the target configuration, the amount of existing data, and the write speed of business data. During the instance configuration modification, the database may have 1 to 3 connection flashes. Operate carefully. It is recommended to perform the operation during off\-peak hours and add a reconnection mechanism to the application to reduce the impact of database connection flashes on the business.

* Modifying the configuration will not change the instance ID or connection address.

* High primary\-secondary latency prevents switching between primary and secondary nodes, which can affect configuration modification. It is recommended to estimate the required instance specification and perform an upgrade or expansion before peak business hours.

* Modifying the configuration of an instance in its temporary upgrade period will end the temporary upgrade. Only upgrades are allowed, and downgrades are not permitted. An upgrade must meet at least one of the following three conditions: an upgrade of node specifications, an increase in storage space, or an increase in the number of read\-only nodes.

* If read/write separation is enabled for a double\-node instance, the read/write separation weight is automatically calculated based on the new instance specification after the instance configuration is modified. You can view it on the **Connectivity** page. To modify, refer to [Setting the read/write separation policy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_read-write_splitting_policies).

* During the process of changing the configuration, the instance page may display an exception, so you can refresh the page later and retry.

* When the specification changes, the parameter inherits the current configuration, and the memory parameter that does not fit the target specification will automatically use the default value of the parameter template. For details, see [Parameter modification rules](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Parameter_modification_rules).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project to which the instance belongs is not set, this operation should select the project as <strong>All resources</strong>.   </div>
   

3. Go to the **Add node** page of the target instance. RDS for MySQL provides two entry points:

   * On the **Instances** page, click **Modify configuration** in the **Actions** column of the target instance\>**Add node**.

   * After entering the target instance, click **Modify configuration** in the upper right corner of the page\>**Add node**.

4. On the **Add node** page of the target instance, complete the following configurations based on your business needs and confirm the impact and risks of the instance specification change.

   
   |Parameter |Description |
   |---|---|
   |Node specification |Add nodes to the instance and set their specifications and availability zones.<br><br><br>* If the instance type is **Double node**:<br><br>   * An instance can have up to 10 read\-only nodes.<br><br>   * You can set the specifications for new read\-only nodes as needed.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">However, it should be noted that when the specifications of the read\-only nodes are lower than those of the primary node, there may be a delay in the read\-only nodes or even an OOM (Out of Memory) situation for the read\-only nodes due to the high load on the primary node. It is recommended to select the same or a higher specification for the read\-only nodes as that of the primary node.   </div><br>   <br><br>   * Primary, secondary, and read\-only nodes can be deployed in up to three availability zones.<br><br>* If the instance type is **Multiple node**:<br><br>   * The secondary node specifications must be consistent with the primary node specifications.<br><br>   * An instance can have a maximum of 8 secondary nodes.<br><br>   * Nodes can be distributed in at most 3 availability zones. |
   |Switch time |Select the switch time of the change. You can select **Execute now**, **Specific time period**, or **Maintenance window**.<br><br><br>* **Execute now**: Execute immediately after submitting the instance specification modification order.<br><br>* **Specific time period**: Perform the specification change within the specified time period.<br><br>* **Maintenance window**: Execute within the maintenance period set for the instance. You can view the maintenance period currently set for the instance on the summary page. For any adjustment, refer to [Configuring maintenance window](https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Multiple node instances currently only support <strong>Execute now</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you choose to perform the configuration change in the maintenance window, RDS for MySQL will immediately perform resource scheduling, data synchronization and other prerequisite actions after the change order is submitted, and switch the instance status to Changing. When it comes to the maintenance time, switch the route. After the task execution is completed, the instance status changes to Running.</div><br> |
   |Specific time period |If you select **Specific time period**, you need to set the time period for the specification change.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Time periods cannot be set across days.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The shortest time period is two hours.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Set the time period within the time range indicated in the console.</div><br> |
   |Maintenance window |If you choose to modify the configuration during the **Maintenance window**, you need to confirm the instance's **maintenance window**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can click <strong>Edit</strong> to modify the maintenance window of the instance. For detailed rules on setting maintenance window, see <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period">Configuring maintenance window</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After a task is initiated, you can still modify the instance's maintenance window, but the execution time of the initiated task will not be automatically adjusted with the modification of the maintenance window. If you need to adjust the execution time of a task, you need to manually schedule and adjust it at Task center. For more information about modifying tasks execution time, see <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/changing_the_execution_time_of_a_task">Changing the execution time of a task</a>.</div><br> |
   |Risk Identification |Risks to the database proxy service after modifying the instance specification.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Not all specification change operations require risk identification. If the database proxy is enabled for the instance, and its number of CPU cores is less than half of the total CPU cores of all service nodes after the configuration change, the system prompts you to expand the database proxy resources to handle higher database traffic. Confirm the prompt and select the checkbox to continue the process. After the instance specification change is complete, adjust the resources of the database proxy service. For more information about modifying database proxy service resources, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/changing_agent_configurations">Modify proxy configuration</a>.</div><br> |
   

5. Click **Confirm order**.

6. Complete the subsequent steps based on the billing type selected.

   * If the billing method of the instance is **Pay\-as\-you\-go**: on the **Confirm order** page, confirm the order details, read and check the **Database Products and Services Terms** and **Unsubscription rules**, and then click **Buy now** to complete the instance configuration change.

   * If the billing method of the instance is **Subscription**:

      1. on the **Confirm order** page, confirm the order details, read and check the **Database Products and Services Terms** and **Unsubscription rules**, and click ** Submit the order**.

      2. On the **Confirm order information** page, reconfirm the order information, and click **Next step**.

      3. On the **Submit payment information** page, confirm the payment details, select a payment method, click **To pay**, and complete the payment as prompted to finish the instance configuration change.


<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[CreateDBNodes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdbnodes) |Call the CreateDBNodes API to add read\-only nodes to an instance. |
