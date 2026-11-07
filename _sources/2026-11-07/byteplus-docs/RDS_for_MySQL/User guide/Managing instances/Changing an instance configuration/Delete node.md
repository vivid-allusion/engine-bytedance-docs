---
title: "Delete node"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/deleting_nodes"
---

RDS for MySQL supports removing read\-only nodes from double\-node instances and secondary nodes from multiple\-node instances. This topic describes the required steps.

<span id=".6LS555So6K-05piO"></span>
## Billing

For information about fees for removing instance nodes, refer to [Subscription cancellation or instance specification modification](https://docs.byteplus.com/en/docs/RDS_for_MySQL/subscription_cancellation_or_instance_specification_modification).

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An instance is created and in the **Running** state. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* You cannot delete nodes from a single\-node instance.

* Double\-node instances do not support deleting the secondary node; Multi\-node instances must retain at least one secondary node.

* Modifying the configuration may automatically trigger data migration, which can cause a database interruption or transient disconnection. While the instance configuration is being modified, most operations related to databases, accounts, and networks cannot be performed.

* You do not need to manually restart the instance after modifying the configuration. The change takes minutes, and the duration depends on the number of nodes of the target configuration, the amount of existing data, and the write speed of business data. During the instance configuration modification, the database may have 1 to 3 connection flashes. Operate carefully. It is recommended to perform the operation during off\-peak hours and add a reconnection mechanism to the application to reduce the impact of database connection flashes on the business.

* Modifying the configuration will not change the instance ID or connection address.

* High primary\-secondary latency prevents switching between primary and secondary nodes, which can affect configuration modification. It is recommended to estimate the required instance specification and perform an upgrade or expansion before peak business hours.

* Deleting a read\-only node from an instance during a temporary upgrade is not supported.

* If read\-write separation is enabled for the instance, the read\-write separation weights are automatically calculated based on the new instance specifications after modifying the configuration. View them on the **Connectivity** page. To modify, refer to [Setting the read/write separation policy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_read-write_splitting_policies).

* During the process of changing the configuration, the instance page may display an exception, so you can refresh the page later and retry.


<span id="HZZrInNv"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Go to the **Delete node** page of the target instance. RDS for MySQL provides two entry points:

   * On the **Instances** page, click **Modify configuration** \> **Delete node** in the **Actions** column for the target instance.

   * After you go to the target instance page, click **Modify configuration** \> **Delete node** in the upper\-right corner.

4. On the **Delete node** page of the target instance, complete the following configurations based on your business needs and confirm the impact of the instance specification change.

   
   |Parameter |Description |
   |---|---|
   |Node specification |Delete a node from the instance.<br><br><br>* If the instance type is **Double node**:<br><br>   * The instance can have a minimum of 0 read\-only nodes.<br><br>   * You can delete read\-only nodes from up to three availability zones at a time.<br><br>* If the instance type is **Multiple node**:<br><br>   * The instance must have at least 1 secondary node.<br><br>   * You can delete secondary nodes from up to three availability zones at a time. |
   |Estimated impact |Confirm the impact of changing the instance specification.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The estimated impact is based on the resource state when the configuration is completed on the Modify configuration page. The resource status may change when the modification order is submitted or during the actual modification. The estimated impact is not guaranteed to occur, and the actual impact shall prevail.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">In some cases, the impact cannot be estimated due to system reasons. Click the button on the page to retry.</div><br> |
   |Switch time |Select the switch time of the change. You can select **Execute now**, **Specific time period**, or **Maintenance window**.<br><br><br>* **Execute now**: Execute immediately after submitting the modification order.<br><br>* **Specific time period**: Perform the specification change within the specified time period.<br><br>* **Maintenance window**: Execute within the maintenance window set for the instance. You can view the currently set maintenance window for your instance on the Summary page. To adjust, see [Configuring maintenance window](https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Multiple node instances currently only support <strong>Execute now</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you choose to perform the configuration change in the maintenance window, RDS for MySQL will immediately perform resource scheduling, data synchronization and other prerequisite actions after the change order is submitted, and switch the instance status to Changing. When it comes to the maintenance time, switch the route. After the task execution is completed, the instance status changes to Running.</div><br> |
   |Specific time period |If you select **Specific time period**, you need to set the time period for the specification change.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Time periods cannot be set across days.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The minimum time period is two hours.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Set the time period within the time range indicated in the console.</div><br> |
   |Maintenance window |If you choose to modify the configuration during the **Maintenance window**, you need to confirm the instance's **maintenance window**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can click <strong>Edit</strong> to modify the maintenance window of the instance. For detailed rules on setting maintenance window, see <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period">Configuring maintenance window</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After a task is initiated, you can still modify the instance's maintenance window, but the execution time of the initiated task will not be automatically adjusted with the modification of the maintenance window. If you need to adjust the execution time of a task, you need to manually schedule and adjust it at Task center. For more information about modifying tasks execution time, see <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/changing_the_execution_time_of_a_task">Changing the execution time of a task</a>.</div><br> |
   

5. Click **Confirm order**.

6. Complete the subsequent steps based on the billing type selected.

   * If the billing method of the instance is **Pay\-as\-you\-go**: on the **Confirm order** page, confirm the order details, read and check the **Database Products and Services Terms** and **Unsubscription rules**, and then click **Buy now** to complete the instance configuration change.

   * If the billing method of the instance is **Subscription**:

      1. On the **Confirm order** page, confirm the order details, read and check the **Database Products and Services Terms** and **Unsubscription rules**, and click **Submit the order**.

      2. On the **Confirm order information** page, reconfirm the order information, and click **Next step**.

      3. On the **Submit payment information** page, confirm the payment details, select a payment method, click **To pay**, and complete the payment as prompted to finish the instance configuration change.


<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[DeleteDBNodes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/deletedbnodes) |Call the DeleteDBNodes API to remove read\-only nodes from an instance. |
