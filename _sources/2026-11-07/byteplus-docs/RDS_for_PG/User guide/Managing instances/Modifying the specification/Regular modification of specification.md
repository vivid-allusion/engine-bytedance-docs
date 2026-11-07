---
title: "Regular modification of specification"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/standard_instance_specification_modification"
---

This topic describes how to modify the configuration of your instance, including changing the instance specification, expanding or reducing storage space, and adding or deleting read\-only nodes.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have [created an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/create_instance), and the instance is in the **Running** status.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* While the instance configuration is being modified, most operations related to databases, accounts, and networks cannot be performed.

* During the process of modifying the instance configuration, the database may experience 3 to 4 connection interruptions. Operate with caution. It is recommended that you add a reconnection mechanism to the application, which can greatly reduce the impact of database disconnection on the business.

* After modifying the configuration, there is no need for you to manually restart the instance. The modification time is at the minute level and related to the data size, generally not exceeding 10 minutes.

* Modifying the configuration will not change the instance ID or connection address.

* Supports adjusting the read\-only node specification to be lower than the primary node specifications during configuration modification. When the read\-only node specification is lower than the primary node specifications, there is a risk of memory exhaustion leading to downtime.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Login to the [RDS for PostgreSQL](https://console.byteplus.com/db/rds-pg) console.

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. On the **Instances** page, click **Modify configuration** in the **Actions** column of the target instance.

4. Re\-select the **Node specification** and **Storage space** according to business requirements, and set the following parameters.

   
   |Parameter |Note |
   |---|---|
   |Node specification |Node specification includes cores, memory, max connections, and availability zone. You can choose according to your business requirements.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When modifying configuration, you can reselect the specifications of the primary node, secondary node, and read\-only node, and the quantity of read\-only nodes. The availability zones of each node do not support change. When selecting node specifications and the number of read\-only nodes, the following requirements must be met:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The specifications of the secondary and primary nodes must be consistent.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The read\-only node specification cannot be lower than half of the primary node specification. Both CPU cores and memory must not be less than half of the primary node specifications. For example, if the primary node specification is 8C16G, the number of cores for the read\-only node cannot be less than 4, and the memory cannot be less than 8.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can add up to 10 read\-only nodes.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The primary, secondary, and read\-only nodes of multi\-availability zone instances can belong to different availability zones under the same region. For single\-availability zone instances, new read\-only nodes can only be selected within the same availability zone as the primary node. To choose a different availability zone, please first complete a multi\-availability zone deployment using <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/availability_zone_migration">Migrating availability zone</a>.</div><br> |
   |Storage space |Storage space includes data space, log space, WAL log space, and transaction file space. Please enter storage space in the range of 20GB to 12,000GB, with a step size of 10GB, and it cannot be less than 120% of the currently used space. Please scale up or down according to business needs.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Different specifications have different storage space value ranges. For detailed information on storage space value ranges, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/product_specifications">Product specifications</a>.</div><br> |
   |Estimated impact |Confirm the impact of changing the instance specification.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The estimated impact is based on the resource state when the configuration is completed on the Modify configuration page. The resource status may change when the modification order is submitted or during the actual modification. The estimated impact is not guaranteed to occur, and the actual impact shall prevail.</div><br><br><br>* <div data-tips="true" data-tips-type="default">In some cases, the impact cannot be estimated due to system reasons. Click the button on the page to retry.</div><br> |
   |Switch time |Select the switch time of the change. You can select **Execute now**, **Specific time period**, or **Maintenance window**.<br><br><br>* **Execute now**: Execute immediately after submitting the modification order.<br><br>* **Specific time period**: Perform the specification change within the specified time period.<br><br>* **Maintenance window**: Execute within the maintenance window set for the instance. You can view the currently set maintenance window for your instance on the Summary page. To adjust, see [Configuring maintenance window](https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period).<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The switch time for the following tasks can only be <strong>Execute now</strong>.</div><br><br><br>   * <div data-tips="true" data-tips-type="default">Temporary upgrade for local disk instances</div><br><br><br>   * <div data-tips="true" data-tips-type="default">Regular modification of specification and temporary upgrade for cloud disk instances</div><br><br><br>* <div data-tips="true" data-tips-type="default">If you choose to perform the configuration change in the maintenance window, RDS for PostgreSQL will immediately perform resource scheduling, data synchronization and other prerequisite actions after the change order is submitted, and switch the instance status to <strong>Changing</strong>. When it comes to the maintenance time, switch the route. After the task execution is completed, the instance status changes to <strong>Running</strong>.</div><br> |
   |Specific time period |If you select **Specific time period**, you need to set the time period for the specification change.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Time periods cannot be set across days.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The minimum time period is two hours.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Set the time period within the time range prompted by the console.</div><br> |
   |Maintenance window |If you choose to modify the configuration during the **Maintenance window**, you need to confirm the instance's **maintenance window**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can click <strong>Edit</strong> to modify the maintenance window of the instance. For detailed rules on setting maintenance window, see <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/Configuring_maintenance_window">Configuring maintenance window</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">After a task is initiated, you can still modify the instance's maintenance window, but the execution time of the initiated task will not be automatically adjusted with the modification of the maintenance window. If you need to adjust the execution time of a task, you need to manually schedule and adjust it at Task center. For more information about modifying tasks execution time, see <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/Modifying_the_task_execution_time">Changing the execution time of a task</a>.</div><br> |
   

5. Click **Confirm order**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For details on modification fees, please refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/fees_for_modification_of_instance_specification">Unsubscription or modification fee description</a>.   </div>
   

6. Complete the subsequent steps based on the instance's billing method.

   * If **Pay\-as\-you\-go** is selected: On the **Confirm order** page, confirm the order details, read and check the **Database Product and Services Terms**, then click **Buy now**.

   * If you select **Subscription**:

      * On the **Confirm order** page, confirm the order details. Read and check the **Database Product and Services Terms**, and click **Submit the order**.

      * On the **Confirm order information** page, confirm the order information again and click **Next step**.

      * On the **Submit payment information** page, confirm the payment details, select a payment method, click **To pay**, and complete the payment as prompted to finish the instance configuration change.
