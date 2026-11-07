---
title: "Modifying specifications temporarily"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/temporary_instance_specification_upgrade"
---

This topic describes the steps to temporarily upgrade a monthly/annual subscription instance.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

RDS for PostgreSQL supports two instance specification modification methods, namely standard modification and temporary modification.


* Regular modification of specification is the standard way to modify instance configuration. It supports adjusting instance specifications, storage space, and adding or deleting read\-only nodes. For more information about regular modification of specification, refer to [Changing specification](https://docs.byteplus.com/en/docs/RDS_for_MySQL/standard_instance_specification_modification), [Adding a node](https://docs.byteplus.com/en/docs/RDS_for_MySQL/adding_nodes), and [Deleting a node](https://docs.byteplus.com/en/docs/RDS_for_MySQL/deleting_nodes).

* Temporary upgrade is a method for modifying instance configuration that is specifically provided by RDS for MySQL for monthly/annual subscription instances to reduce the financial pressure caused by the need to upgrade configurations for short\-term business surges. The configuration upgrade in a temporary upgrade is short\-term. You need to specify a restore date during the upgrade, and it only supports upgrading node specifications.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A monthly/annual subscription instance has been created and its status is **Running**. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The temporary upgrade is currently an allowlisted feature. While there are a few minor areas for experience optimization, they do not affect the normal operation of the instance. If your business has specific needs for this feature, [submit a ticket](https://console.byteplus.com/workorder/create/) to apply for allowlist access.

* The temporary upgrade feature currently has the following limitations:

   * It is only supported for regular instances billed on a monthly/annual subscription. It is not supported for instances with blue\-green deployments.

   * Only node specification upgrades are supported. Adjusting the storage space, changing the storage type, and adding or deleting read\-only nodes are not supported.

   * A single temporary upgrade has a minimum duration of 5 days and a maximum duration of 30 days. A temporary upgrade cannot be initiated for an instance with less than 5 days until its due time. If an instance has less than 30 days until its due time, the maximum upgrade duration is limited to the remaining time.

* For instances during a temporary upgrade period:

   * You can initiate another temporary upgrade, but the upgrade period cannot be shortened. The cumulative temporary upgrade period cannot exceed 30 days.

   * Regular modification of specification is supported, but initiating it will terminate the temporary upgrade. Only upgrades are permitted, not downgrades. An upgrade must meet at least one of the following three conditions: an upgrade of node specifications, an increase in storage space, or an increase in the number of read\-only nodes.

   * Adjusting storage space or changing the storage type is not supported. If an adjustment is required, perform a regular modification of specification. Because only upgrades are allowed for regular modifications on an instance during its temporary upgrade period, fully estimate the storage usage for the period and complete any necessary expansion before starting the temporary upgrade.

   * Unsubscription is not supported.

* After initiating the configuration change for a temporary upgrade, you do not need to manually restart the instance. The change takes minutes, and the duration depends on the number of nodes in the target configuration, the existing data volume, and the write speed of your business data. During the instance configuration modification, the database may have 1 to 3 connection flashes. Operate carefully. It is recommended to perform the operation during off\-peak hours and add a reconnection mechanism to the application to reduce the impact of database connection flashes on the business.

* While the configuration is being modified, the instance page may display abnormally. Refresh the page to try again later.

* When the specification changes, the parameter inherits the current configuration, and the memory parameter that does not fit the target specification will automatically use the default value of the parameter template. For details, see [Parameter modification rules](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Parameter_modification_rules).

* If an instance has read\-write separation enabled and uses a round\-robin scheduling strategy, the system automatically calculates the scheduling weight based on the new instance specifications after the configuration is modified. You can view the weight on the **Connectivity** page. To modify, refer to [Setting the read/write separation policy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_read-write_splitting_policies).

* After the temporary upgrade expires, the instance is automatically restored to its pre\-upgrade configuration.

   * Before the temporary upgrade expires, confirm that the instance workload has decreased to a level that the original configuration can support. This prevents excessive resource consumption by the instance, which can degrade performance and impact your business. Restoring the original configuration is also a configuration modification process, during which the database connection may be interrupted 1 to 3 times. Before the temporary upgrade expires, evaluate the impact on your business and adjust the recovery time as needed. The system will also send you an operation and maintenance event. You can check the restoration progress in the operation and maintenance event. If needed, you can [submit a ticket](https://console.byteplus.com/workorder/create/?step=2&SubProductID=P00000178) to contact technical support.

   * When restoring, the system prioritizes the earliest maintenance window after the temporary upgrade period ends for restoration. If the restoration fails, it will be automatically postponed to the next maintenance window. You will not be charged for the postponement of the restoration time.

* Temporary upgrade is not supported for instances that use the RocksDB engine.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project to which the instance belongs is not set, this operation should select the project as <strong>All resources</strong>.   </div>
   

3. Go to the **Modify configuration** page of the target instance through the following paths.

   * On the **Instances** page, click **Modify Configuration** \> **Temporary upgrade** in the **Actions** column of the target instance.

   * On the **Summary** page, click **Modify configuration** \> **Temporary upgrade** in the upper\-right corner of the page.

4. In the dialog box that appears, read the prompt, select the checkbox, and click **OK**.

5. On the **Temporary upgrade** page that appears, complete the following configurations based on your business requirements and confirm the impacts and risks of changing the instance specification.

   
   |Parameter |Description |
   |---|---|
   |Restore date |Set the restore date for the temporary upgrade to a date between 5 and 30 days from now.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If the instance is already undergoing a temporary upgrade, the new restore time cannot be earlier than the currently set restore time.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The upgrade time does not need to be set; it is the time when the order for the temporary upgrade is submitted. When restoring, the system will give priority to the nearest available maintenance window after the upgrade period. If the restoration fails, it will be automatically postponed to the next maintenance window. You can view the restoration task status in the Operation and maintenance event.</div><br> |
   |Node specification |Temporary upgrade only supports upgrading node specifications. The specifications of the secondary node automatically match those of the primary node.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">However, it should be noted that when the specifications of the read\-only nodes are lower than those of the primary node, there may be a delay in the read\-only nodes or even an OOM (Out of Memory) situation for the read\-only nodes due to the high load on the primary node. It is recommended to select the same or a higher specification for the read\-only nodes as that of the primary node.</div><br> |
   |Estimated impact |Confirm the impact of changing the instance specification.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The estimated impact is based on the resource state when the configuration is completed on the Modify configuration page. The resource status may change when the modification order is submitted or during the actual modification. The estimated impact is not guaranteed to occur, and the actual impact shall prevail.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">In some cases, the impact cannot be estimated due to system reasons. Click the button on the page to retry.</div><br> |
   |Quickly adjust parameters |Select whether to enable quick parameter adjustment. If yes, parameters that require an instance restart to take effect will not be adjusted. You can manually restart the instance later to make the adjustment take effect.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This feature is only available if the storage type is cloud disk and the storage type is not changed during the temporary upgrade.</div><br> |
   |Switch time |Select the switch time of the change. You can select **Execute now**, **Specific time period**, or **Maintenance window**.<br><br><br>* **Execute now**: Execute immediately after submitting the instance specification modification order.<br><br>* **Specific time period**: Perform the specification change within the specified time period.<br><br>* **Maintenance window**: Execute within the maintenance period set for the instance. You can view the maintenance period currently set for the instance on the summary page. For any adjustment, refer to [Configuring maintenance window](https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Multiple node instances currently only support <strong>Execute now</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The temporary upgrade starts from the submission time on the temporary upgrade page, regardless of the execution time you select.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you choose to perform the configuration change in the maintenance window, RDS for MySQL will immediately perform resource scheduling, data synchronization and other prerequisite actions after the change order is submitted, and switch the instance status to <strong>Changing</strong>. When it comes to the maintenance time, switch the route. After the task execution is completed, the instance status changes to <strong>Running</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the required temporary upgrade period is short and the interval until the instance's maintenance window is too long, you may not be able to successfully initiate the temporary upgrade. Plan the maintenance window reasonably when you select to perform a temporary upgrade during the maintenance window.</div><br> |
   |Specific time period |If you select **Specific time period**, you need to set the time period for the specification change.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Time periods cannot be set across days.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The shortest time period is two hours.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Set the time period within the time range indicated in the console.</div><br> |
   |Maintenance window |If you choose to modify the configuration during the **Maintenance window**, you need to confirm the instance's **maintenance window**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can click <strong>Edit</strong> to modify the maintenance window of the instance. For detailed rules on setting maintenance window, see <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period">Configuring maintenance window</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After a task is initiated, you can still modify the instance's maintenance window, but the execution time of the initiated task will not be automatically adjusted with the modification of the maintenance window. If you need to adjust the execution time of a task, you need to manually schedule and adjust it at Task center. For more information about modifying tasks execution time, see <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/changing_the_execution_time_of_a_task">Changing the execution time of a task</a>.</div><br> |
   |Risk Identification |Risks to the database proxy service after modifying the instance specification.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Not all specification change operations require risk identification. If the database proxy is enabled for the instance, and its number of CPU cores is less than half of the total CPU cores of all service nodes after the configuration change, the system prompts you to expand the database proxy resources to handle higher database traffic. Confirm the prompt and select the checkbox to continue the process. After the instance specification change is complete, adjust the resources of the database proxy service. For more information about modifying database proxy service resources, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/changing_agent_configurations">Modify proxy configuration</a>.</div><br> |
   



&nbsp;

5. Click **Confirm order**.

6. on the **Confirm order** page, confirm the order details, read and check the **Database Products and Services Terms** and **Unsubscription rules**, and click ** Submit the order**.

7. On the **Confirm order information** page, reconfirm the order information, and click **Next step**.

8. On the **Submit payment information** page, confirm the payment details and select the **Payment method**, click **Go to payment**, and complete the payment as prompted to complete the temporary upgrade of the instance.


<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Note |
|---|---|
|[ModifyDBNodeTemporarySpec](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbnodetemporaryspec) |Call the ModifyDBNodeTemporarySpec API to temporarily upgrade the configuration of a monthly/annual subscription instance. |
