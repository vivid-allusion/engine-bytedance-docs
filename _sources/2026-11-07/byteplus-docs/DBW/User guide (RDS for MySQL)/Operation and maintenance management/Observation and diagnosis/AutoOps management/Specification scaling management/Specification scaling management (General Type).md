---
title: "Specification scaling management (General Type)"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Specification_scaling_management"
---

Database Workshop (DBW) provides the compute scaling function for nodes of RDS for MySQL instances. This function helps you dynamically adjust the number of CPU resources based on your business requirements to adapt to short\-term business changes and ensure the stable operation of your system. This topic describes how to enable, view, modify, and disable compute scaling rules.

<span id="GmnFfbMD"></span>
## Function introduction

DBW supports two compute scaling methods for RDS for MySQL instances. Both of these compute scaling methods can scale exclusive or general\-purpose instance nodes. The differences between them are as follows:


|**Difference** |**Manual scaling** |**Auto scaling** |
|---|---|---|
|Trigger condition<br><br> |* Scale up: After configuring manual scaling, you can trigger scaling up. DBW starts scaling up instance nodes.<br><br>* Scale down: After the **manual effective time** in manual scaling expires, or after manual scaling is disabled, instance node scaling down is triggered. |* Scaling up: Automatically triggered by the average CPU usage.<br><br>* Scaling down: Automatically triggered by the average CPU usage. |
|Expansion duration |There is a time limit, ranging from 12 to 72 times. After the duration expires, the node will automatically revert to the specifications before the expansion.<br><br> |There are no time limits. Node scaling is triggered based on the scaling down conditions. When the conditions are met, the node will automatically revert to the specification before the scaling up. |
|Scaling up the number of CPUs |You can manually configure the number of CPUs to be scaled, ranging from 0 to 8. |The number of CPU cores after scaling up is min(current CPU count \* 2, current CPU count + 8). |


<span id="zuJDaoxV"></span>
## Fee

RDS for MySQL automatically expands the number of node cores in minutes, and is billed according to the number of cores and duration. For more billing information, refer to [Billing items and prices of RDS for MySQL](https://docs.byteplus.com/en/docs/RDS_for_MySQL/charge_items_and_price).

<span id="zuJDaoxV"></span>
## Prerequisites


* An instance for RDS for MySQL has been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* If the target instance has security control enabled, you need to apply for operation and maintenance read\-only or read/write permissions for the current account. For more information, refer to [Enabling instance security control (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql), and [Applying for operation permissions (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/creating-an-operation-permission-ticket).

* The database version of the instance must be no lower than `MySQL 5.7.32_20250615` or `MySQL 8.0.32_20250615`. You can view the kernel minor version of an instance by [Viewing instance information](https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_instance_details). If the kernel minor version of your instance is not within the supported kernel minor version range, you can [Manually upgrade the instance kernel minor version](https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version). For more information on the kernel minor version of RDS for MySQL, refer to [Kernel minor version release notes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/kernal_version_release_notes).


<span id="t2VLseDz"></span>
## Precautions


* If the database version of the instance is lower than `MySQL 5.7.32_20250615` or `MySQL 8.0.32_20250615`, [Upgrade instance kernel minor version manually](https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version) first, and then enable compute scaling for the instance.

* Currently, only in\-place scaling of instance specifications is supported. This operation does not require instance reconstruction or data migration, is typically completed within 3 minutes, and causes no service interruption.

* If the execution conditions for compute scaling are not met after configuring compute scaling (the instance is being changed or local resources are insufficient), the compute scaling may fail. Pay attention to whether the database is scaled successfully in time to avoid business impact caused by scaling failure. You can view the upgrade status of each node in the instance topology. For details, see [View instance topology](https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_instance_topologies).

* If the compute scaling fails, RDS for MySQL reports an "Automatic instance Compute scaling failed" event to Cloud Monitor. You can configure event rules for such events to obtain event information at the earliest opportunity. For more information about viewing events and configuring event rules, see [View events](https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_an_event) and [Create event rules](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Creating_event_policy).

* During compute scaling, you cannot configure both Auto scaling and Manual scaling methods at the same time. You can only select one scaling method.

* After compute scaling is triggered, the RDS for MySQL instance usually completes Compute scaling within a few minutes. During compute scaling, you are not allowed to modify, enable, or close compute scaling rules.

* In manual scaling, the manual effective time ranges from 12 to 72 hours. If the effective time exceeds 72 hours, it is suggested that you use the Modifying specifications temporarily feature. For more information, see [Modifying specifications temporarily](https://docs.byteplus.com/en/docs/RDS_for_MySQL/temporary_instance_specification_upgrade).

* During instance node compute scaling, you are not allowed to modify the compute scaling rule configuration of the current instance.

* Before using the AutoOps function, make sure that there is sufficient balance in the account to support changing the instance configuration. For more billing information about the product, see [Billing overview](https://docs.byteplus.com/en/docs/RDS_for_MySQL/price_overview).

* The additional CPU scaling only supports pay\-as\-you\-go billing, and the CPU costs for general\-purpose and exclusive specifications are different. Fees are charged hourly after successful scaling.

* Scaling of instance specifications is currently supported only for general type instance types.

* If a configuration change occurs in the MySQL instance, an instance scaling rollback will be triggered.


<span id="ISdrFalI"></span>
## Enable compute scaling rules

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">After a manual scaling rule is created successfully, it will take effect immediately and trigger the scaling of the current instance. After compute scaling is triggered, the RDS for MySQL instance usually completes compute scaling within a few minutes. During compute scaling, you are not allowed to modify, enable, or close compute scaling rules.</div>


* <div data-tips="true" data-tips-type="default">After an auto scaling rule is created successfully, scaling of the instance node will only be triggered when the average CPU usage and other conditions meet the scaling conditions.</div>


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **RDS for MySQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, click **Compute scaling** under **Configure AutoOps rules**.

6. In the **Configure AutoOps rules \- Compute scaling** panel, configure the following parameters.

   
   |**Parameter** ||**Description** |
   |---|---|---|
   |**Scaling method** ||Select the scaling method as needed.<br><br><br>* **Auto scaling** automatically triggers scaling up or down of the number of CPU cores of the primary and secondary nodes based on the average CPU usage in the rule configuration.<br><br>* **Manual scaling**, manually configure scaling tasks based on business operations. |
   |**Rule switch** ||After **enabling** this feature, you can configure scaling rules. |
   |**Auto scaling**<br><br> |**Rule configuration** |* **Scaling up rules**: Set the conditions for automatically triggering node CPU scale\-up. The default condition is that when the average CPU usage of the current instance exceeds 90% within 3 minutes, scaling up is automatically triggered, increasing the number of CPU cores to twice the current CPU count or adding 8 cores based on the original rule. You can customize the scale\-up trigger conditions based on your business requirements.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The value range of average CPU usage is 50% to 90%, and the time is selected from the drop\-down box as needed.   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After triggering automatic scaling up, the number of CPUs in the primary and secondary nodes after scaling up is min(current CPU count \* 2, current CPU count + 8).   </div><br>   <br><br>* **Scaling down rules**: Set the conditions for automatically triggering node CPU scale\-down. The default condition is: When the average CPU usage of the current instance is less than 30% within 10 minutes, automatic scaling down is triggered to reduce the number of CPU cores to the specification before scaling up. You can customize the scaling down trigger condition according to your business needs. |
   ||**Read\-only node scaling configuration** |If the current instance is has read\-only nodes, select a scaling policy for the read\-only nodes as needed.<br><br><br>* **Scaling with primary and secondary**: The scaling rules for read\-only nodes are consistent with those for primary and secondary nodes.<br><br>* **No scaling**: No scaling is performed on read\-only nodes.<br><br>* **Custom scaling**: Configure scaling rules separately for read\-only nodes. When the scaling conditions for read\-only nodes are met, scaling is performed separately on the read\-only nodes. If no scaling rules are configured for read\-only nodes, it means that no scaling will be performed on the read\-only nodes. The scaling quantity for read\-only nodes is min(current number of CPUs, 8), and the post\-scaling number of CPUs is min(current number of CPUs \* 2, current number of CPUs + 8). . |
   ||**Expansion configuration** |When the **read\-only node scaling configuration** is **Custom scaling**, you need to configure scaling up rules for the read\-only node.<br><br><br>1. Add read\-only nodes.<br><br>   1. Click **Add read\-only nodes**. In the dialog box that appears, select the read\-only nodes for which you want to configure scaling rules as needed. Multi\-select is supported.<br><br>   2. Click **OK**.<br><br>2. Configure scaling up rules for the node.<br><br>   Configure the trigger condition for scaling up or down for each node.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The value range of the node scale\-up threshold is 50% to 90%, and the duration can be selected from the drop\-down list as needed.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Click <strong>Remove</strong> in the operation column to remove unnecessary read\-only nodes for scaling up or down.</div><br> |
   ||**Scaling preview** |To ensure business availability, the scaling\-up principle is to double the current number of CPU cores, with a maximum increase of 8 cores. The number of CPUs after scaling up is min(current number of CPUs \* 2, current number of CPUs + 8).<br><br>The scaling preview displays the current number of CPUs, the added number of CPUs, and the expected number of CPUs in each node of the instance. |
   |**Manual scaling** |**Expansion configuration** |Manually configure the number of CPUs to be scaled. The scaling range for the number of cores is 0 to 8. For dual\-node or Multi\-node instances, if the number of CPUs to be scaled is the same for each node, click **Batch** to batch configure the number of CPUs to be scaled for each node.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The number of cores for scaling up all nodes cannot be configured to 0 at the same time.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For dual or multi\-node instances, the specification of the Read\-only node and the primary node can be different. However, when the read\-only node specification is lower than the primary node specification, the read\-only node may be delayed or even experience an OOM error due to the high load on the primary node. It is recommended to select the same or a higher specification for the read\-only nodes as that of the primary node. It is recommended to select the same or a higher specification for the read\-only nodes as that of the primary node.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For multiple node instances, the specifications of secondary nodes automatically match those of the primary node.</div><br> |
   ||**Manual effective time** |Configure the duration for which the current scaling up is valid. After the duration expires, the original specifications will be automatically scaled down. The effective time range for the manual effective time is 12 to 72 hours. If the effective time exceeds 72 hours, it is suggested that you use the modifying specifications temporarily feature. For more information, see [Modifying specifications temporarily](https://docs.byteplus.com/en/docs/RDS_for_MySQL/temporary_instance_specification_upgrade). |
   |**Configuration fee** ||RDS for MySQL automatically expands the number of node cores in minutes, and is billed according to the number of cores and duration. Billing will stop once the scaling down rules are triggered. For more billing information, refer to [Billing items and prices of RDS for MySQL](https://docs.byteplus.com/en/docs/RDS_for_MySQL/charge_items_and_price). |
   

7. Click **OK**.


<span id="lU7hc7IN"></span>
## View compute scaling events

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Compute scaling events include automatic scaling up, automatic scaling rollback, manual scaling, manual scaling rollback, and instance changes. If a configuration change occurs in the MySQL instance, an instance scaling rollback will be triggered.</div>



1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **RDS for MySQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, set the time range for the query events as needed. The target events to view include **Event ID**, **Event status**, **Trigger value**, **Trigger condition**, **Rule type**, **Before/After adjustment**, and **Trigger time**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Before/After triggering indicates the number of CPU cores before and after the scaling.   </div>
   

<span id="sY6vnAlM"></span>
## Modify compute scaling rule

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Once the manual scaling rule is successfully modified, it will take effect immediately and trigger the scaling of the current instance.</div>


* <div data-tips="true" data-tips-type="default">After the auto scaling rule is successfully modified, instance node scaling is triggered only when the average CPU usage and other conditions meet the scaling conditions.</div>


* <div data-tips="true" data-tips-type="default">After compute scaling is triggered, the RDS for MySQL instance usually completes compute scaling within a few minutes. During compute scaling, you are not allowed to modify, enable, or close compute scaling rules.</div>


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **RDS for MySQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, click **Compute scaling** under **Configure AutoOps rules**.

6. In the **Configure AutoOps rules \- Compute scaling** panel, configure the following parameters.

   
   |**Scaling method** |**Parameter** |**Description** |
   |---|---|---|
   |**Auto scaling**<br><br> |**Rule configuration**<br><br> |* **Scaling up rules**: Set the conditions for automatically triggering node CPU scale\-up. The default condition is that when the average CPU usage of the current instance exceeds 90% within 3 minutes, scaling up is automatically triggered, increasing the number of CPU cores to twice the current CPU count or adding 8 cores based on the original rule. You can customize the scale\-up trigger conditions based on your business requirements.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The value range of average CPU usage is 50% to 90%, and the time is selected from the drop\-down box as needed.   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After triggering automatic scaling up, the number of CPUs in the primary and secondary nodes after scaling up is min(current CPU count \* 2, current CPU count + 8).   </div><br>   <br><br>* **Scaling down rules**: Set the conditions for automatically triggering node CPU scale\-down. The default condition is that when the average CPU usage of the current instance within 10 minutes is less than 30%, the scaling down is automatically triggered, and the number of CPU cores is reduced to the pre\-scaling specifications. You can customize the scaling down trigger condition according to your business needs. |
   ||**Expansion configuration** |When read\-only nodes exist and the **Read\-only node scaling configuration** is **Custom scaling**, you can modify the scaling up rules for read\-only nodes.<br><br><br>1. Add read\-only nodes.<br><br>   1. Click **Add read\-only nodes**. In the dialog box that appears, select the read\-only nodes for which you want to configure scaling rules as needed. Multi\-select is supported.<br><br>   2. Click **OK**.<br><br>2. Modify the scaling up rules of the node.<br><br>   Modify the conditions for triggering read\-only node scaling as needed.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The value range of the node scale\-up threshold is 50% to 90%, and the duration can be selected from the drop\-down list as needed.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When modifying auto scaling, removing expansion configurations for read\-only nodes is not supported. To remove the expansion configuration of the read\-only node, you need to turn off the Auto scaling rule first, and then configure it when you turn it on again.</div><br> |
   ||**Scaling preview** |To ensure business availability, the scaling\-up principle is to double the current number of CPU cores, with a maximum increase of 8 cores. The number of CPUs after scaling up is min(current number of CPUs \* 2, current number of CPUs + 8).<br><br>The scaling preview displays the current number of CPUs, the added number of CPUs, and the expected number of CPUs in each node of the instance. |
   |**Manual scaling** |**Expansion configuration** |Manually configure the number of CPUs to be scaled. The scaling range for the number of cores is 0 to 8. For dual\-node or Multi\-node instances, if the number of CPUs to be scaled is the same for each node, click **Batch** to batch configure the number of CPUs to be scaled for each node.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The number of cores for scaling up all nodes cannot be configured to 0 at the same time.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For double\-node instances, the read\-only node can have a different specification than the primary node. However, when the read\-only node specification is lower than the primary node specification, the read\-only node may be delayed or even experience an OOM error due to the high load on the primary node. It is recommended to select the same or a higher specification for the read\-only nodes as that of the primary node. It is recommended to select the same or a higher specification for the read\-only nodes as that of the primary node.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For multiple node instances, the specifications of secondary nodes automatically match those of the primary node.</div><br> |
   ||**Manual effective time** |Configure the duration for which the current scaling up is valid. After the duration expires, the original specifications will be automatically scaled down. The effective time range for the manual effective time is 12 to 72 hours. If the effective time exceeds 72 hours, it is suggested that you use the modifying specifications temporarily feature. For more information, see [Modifying specifications temporarily](https://docs.byteplus.com/en/docs/RDS_for_MySQL/temporary_instance_specification_upgrade).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Modifying the manual effective time separately is not supported.</div><br> |
   |**Configuration fee** ||RDS for MySQL automatically expands the number of node cores in minutes, and is billed according to the number of cores and duration. Billing will stop once the scaling down rules are triggered. For more billing information, refer to [Billing items and prices of RDS for MySQL](https://docs.byteplus.com/en/docs/RDS_for_MySQL/charge_items_and_price). |
   

7. Click **OK**.


<span id="yHIBq0C1"></span>
## Disable compute scaling rules

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">After you turn off the <strong>Manual scaling</strong> rule switch, scaling down will be triggered immediately. The specification of the current instance node will be restored to the specification before scaling up within a few minutes.</div>


* <div data-tips="true" data-tips-type="default">DBW will automatically turn off the manual scaling rule <strong>Manual scaling</strong> when the <strong>Manual effective time</strong> expires. The scaling down of the instance node will be triggered immediately.</div>


* <div data-tips="true" data-tips-type="default">If the current instance has been triggered for automatic scaling up, after you turn off the <strong>Auto scaling</strong> rule switch, the scaling down will be triggered immediately. The specification of the current instance node will be restored to the specification before scaling up within a few minutes.</div>


* <div data-tips="true" data-tips-type="default">After compute scaling is triggered, the RDS for MySQL instance usually completes compute scaling within a few minutes. During compute scaling, you are not allowed to modify, enable, or close compute scaling rules.</div>


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **RDS for MySQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, click **Compute scaling** under **Configure AutoOps rules**.

6. On the **Configure AutoOps rules \- Compute scaling** control panel, **close** the rule switch.

7. Click **OK**.

8. If it is a manual scaling rule, you need to confirm it again. In the disable AutoOps rules dialog box that appears, click **OK** again.


<span id="9V5zN559"></span>
## FAQs


|**Error** |**reason** |**Solution** |
|---|---|---|
|Pre\-check failed: The host where the node is located has insufficient resources, so the system cannot complete automatic scaling up normally. |Insufficient resources.<br><br> |We recommend modifying the specifications of the target instance. After the modification is complete, the system will select a host with more available resources. If the error persists, consider readjusting the instance specifications. For details, see [Change configuration](https://docs.byteplus.com/en/docs/RDS_for_MySQL/standard_instance_specification_modification?lang=zh).<br><br>After scaling the instance, you can check for any exceptions on the Auto Scaling page. If there are any exceptions, hover your mouse over the event status to view the specific cause of the error and make corrections based on the prompts. |
|Pre\-check failed: Insufficient account balance. The system will not be able to automatically scale up. |Insufficient account balance |You need to recharge the current account to ensure sufficient account resources. For detailed operations, see [Recharge](https://docs.byteplus.com/en/docs/6269/100434?lang=zh). |
|Pre\-check failed: The expansion conditions are not met, and the system can not complete automatic scaling up normally. |The instance may be in the process of modifying. |If the instance status is not running or changing, the system will automatically record the expansion failure event during the automatic expansion process. If the instance is running, [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical staff for troubleshooting and identifying the specific issue. |



* **Q: Why is there a delay in scaling MySQL databases in auto scaling rules?** 

   A1: In auto scaling implementations, the scanner automatically and periodically scans the scaling conditions. When multiple conditions meet the scaling requirements simultaneously, only one scaling task that meets the conditions can be executed, which may cause scaling delays for some nodes. For example, the scanner scans the average CPU usage of a MySQL instance at 10:29 AM, and the average CPU usage does not meet the scaling condition at this time. At 10:30 AM, the average CPU usage meets the scaling condition, but it is not detected by DBW in time. When the next scan time is 10:32, DBW discovers that the scaling condition is met, and CPU scaling is triggered at this time.

* **Q2: Why does the AutoOps event show a pre\-check event record when the current resource does not meet the trigger condition?** 

   A2: When scaling RDS for MySQL instances, the system performs cyclic pre\-checks in the background to ensure successful scaling when conditions are met. If the pre\-check fails, a corresponding record is generated.
