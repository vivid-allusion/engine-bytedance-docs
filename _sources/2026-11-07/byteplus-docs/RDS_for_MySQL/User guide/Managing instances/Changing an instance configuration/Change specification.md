---
title: "Change specification"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/standard_instance_specification_modification"
---

RDS for MySQL supports changing the specification and specification type of an instance. This topic describes the steps.

## Billing

For information about fees for changing instance specifications, refer to [Unsubscription or Change Description](https://docs.byteplus.com/en/docs/RDS_for_MySQL/subscription_cancellation_or_instance_specification_modification).

## Prerequisites

An instance is created and in the **Running** state. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

## Precautions

* Modifying the configuration may automatically trigger data migration, which can cause a database interruption or transient disconnection. While the instance configuration is being modified, most operations related to databases, accounts, and networks cannot be performed.

* You do not need to manually restart the instance after modifying the configuration. The change takes minutes, and the duration depends on the number of nodes of the target configuration, the amount of existing data, and the write speed of business data. During the instance configuration modification, the database may have 1 to 3 connection flashes. Operate carefully. It is recommended to perform the operation during off\-peak hours and add a reconnection mechanism to the application to reduce the impact of database connection flashes on the business.

* Modifying the configuration will not change the instance ID or connection address.

* High primary\-secondary latency prevents switching between primary and secondary nodes, which can affect configuration modification. It is recommended to estimate the required instance specification and perform an upgrade or expansion before peak business hours.

* Modifying the configuration of an instance in its temporary upgrade period will end the temporary upgrade. Only upgrades are allowed, and downgrades are not permitted. An upgrade must meet at least one of the following three conditions: an upgrade of node specifications, an increase in storage space, or an increase in the number of read\-only nodes.

* If read\-write separation is enabled for the instance, the read\-write separation weights are automatically calculated based on the new instance specifications after modifying the configuration. View them on the **Connectivity** page. To modify, refer to [Setting the read/write separation policy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_read-write_splitting_policies).

* During the process of changing the configuration, the instance page may display an exception, so you can refresh the page later and retry.

* When the specification changes, the parameter inherits the current configuration, and the memory parameter that does not fit the target specification will automatically use the default value of the parameter template. For details, see [Parameter modification rules](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Parameter_modification_rules).

* Reducing the storage space of a cloud disk instance is not currently supported.

* Storage space is an **instance\-level resource**. When expanding or scaling down in the console, storage space is added to or removed from **The entire instance**, not from a single node (primary node, secondary node, or read\-only node).

## Procedure

1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the top menu bar, select the project and region for the instance.

   > **tip**

   > If the project of the instance has not been set, the project should be selected as **All resources**.

3. Go to the **Change specification** page of the target instance. RDS for MySQL provides two entry points:

   * On the **Instances** page, click **Modify configuration \> Change specification** in the **Actions** column of the target instance.

   * After clicking the target instance name, click **Modify configuration** \> **Change specification** in the upper\-right corner of the page.

4. On the **Change specification** page of the target instance, complete the following configurations based on your business needs and confirm the impact and risks of the instance specification change.

   |Parameter |Description |
   |---|---|
   |Specification type |Supports three specification types: **General type** (formerly "shared type"), **Dedicated type** (formerly "general type"), and **General type (ARM)** .<br><br><br>* **General type**: Exclusive use of allocated memory and storage resources, shares CPU resources with other shared instances in the same physical machine.CPU utilization is maximized through resource reuse, with high cost performance. CPU utilization is maximized through resource reuse, with high cost performance.<br><br>* **Dedicated type**: Fully exclusive use of allocated CPU, memory, and storage resources, with stable performance, not affected by other instances in the physical machine.<br><br>* **General type (ARM)** : General type based on the ARM architecture.<br><br><br>> **tip**<br><br><br><br>* > When an instance's specification type is **General type (ARM)**, it cannot be changed to other specification types.<br><br><br>* > If the instance storage type is Cloud ESSD PL0 or Cloud ESSD FlexPL, the specification type can only be **General type**.<br> |
   |Storage type |Select the storage type for the instance. RDS for MySQL offers four storage types: **Local SSD, High performance cloud disk, Cloud ESSD FlexPL**, and **Cloud ESSD PL0**. The options for changing the storage type depend on the instance's current storage type. The rules are as follows:<br><br><br>* If the instance storage type is Local SSD, you can change the storage type to any cloud disk type.<br><br>* If the instance storage type is Cloud ESSD FlexPL, you can change the storage type to High performance cloud disk.<br><br>* If the instance storage type is Cloud ESSD PL0, you can change the storage type to Cloud ESSD FlexPL and High performance cloud disk.<br><br><br>> **tip**<br><br><br><br>* > The feature to change the storage type from local SSD disks to cloud disks is currently in invite\-only preview. To use it, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support.<br><br><br>* > gh\-performance cloud disks are currently in invite\-only preview. To use it, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support.<br> |
   |Node specification |Modify the specification for each node of the instance.<br><br>> **tip**<br><br><br><br>* > For double\-node instances, the read\-only node can have a different specification than the primary node. However, when the read\-only node specification is lower than the primary node specification, the read\-only node may be delayed or even experience an OOM error due to the high load on the primary node. It is recommended to select the same or a higher specification for the read\-only nodes as that of the primary node. It is recommended to select the same or a higher specification for the read\-only nodes as that of the primary node.<br><br><br>* > For multiple node instances, the specifications of secondary nodes automatically match those of the primary node.<br> |
   |Storage space |Set the storage space for the instance.<br><br>> **tip**<br><br><br><br>* > Storage space includes data space, system file space, Binlog file space, and transaction file space.<br><br><br>* > The storage space can be set from 20 GiB to 32000 GiB in increments of 10 GiB. Different storage types and specifications have different storage space value ranges. For detailed information on storage space value ranges, see [Product specifications](https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications).<br><br><br>* > To reduce the storage space of an instance, the new storage space cannot be less than 120% of the currently used space.<br><br><br>* > Reducing the storage space of a cloud disk instance is not currently supported.<br> |
   |Estimated impact |Confirm the impact of changing the instance specification.<br><br>> **tip**<br><br><br><br>* > The estimated impact is based on the resource state when the configuration is completed on the Modify configuration page. The resource status may change when the modification order is submitted or during the actual modification. The estimated impact is not guaranteed to occur, and the actual impact shall prevail.<br><br><br>* > In some cases, the impact cannot be estimated due to system reasons. Click the button on the page to retry.<br> |
   |Quickly adjust parameters |Select whether to enable quick parameter adjustment. If yes, parameters that require an instance restart to take effect will not be adjusted. You can manually restart the instance later to make the adjustment take effect.<br><br>> **tip**<br><br><br>> This feature is available only when you modify the specification for the following two types of instances:<br><br><br><br>* > Instances whose storage type is cloud disk, and the storage type is not changed when you change the specification.<br><br><br>* > Some instances whose storage type is local SSD.<br> |
   |Switch time |Select the switch time of the change. You can select **Execute now**, **Specific time period**, or **Maintenance window**.<br><br><br>* **Execute now**: Execute immediately after submitting the modification order.<br><br>* **Specific time period**: Perform the specification change within the specified time period.<br><br>* **Maintenance window**: Execute within the maintenance window set for the instance. You can view the currently set maintenance window for your instance on the Summary page. To adjust, see [Configuring maintenance window](https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period).<br><br><br>> **tip**<br><br><br>> If you select to change the specification during the maintenance window, RDS for MySQL will immediately perform prerequisite actions such as resource scheduling and data synchronization after the modification order is submitted, and the instance status will be switched to Modifying. The route will be switched after the maintenance window starts. After the task is completed, the instance status will change to Running.<br> |
   |Specific time period |If you select **Specific time period**, you need to set the time period for the specification change.<br><br>> **tip**<br><br><br><br>* > Time periods cannot be set across days.<br><br><br>* > The minimum time period is two hours.<br><br><br>* > Set the time period within the time range indicated in the console.<br> |
   |Maintenance window |If you choose to modify the configuration during the **Maintenance window**, you need to confirm the instance's **maintenance window**.<br><br>> **tip**<br><br><br><br>* > You can click **Edit** to modify the maintenance window of the instance. For detailed rules on setting maintenance window, see [Configuring maintenance window](https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period).<br><br><br>* > After a task is initiated, you can still modify the instance's maintenance window, but the execution time of the initiated task will not be automatically adjusted with the modification of the maintenance window. If you need to adjust the execution time of a task, you need to manually schedule and adjust it at Task center. For more information about modifying tasks execution time, see [Changing the execution time of a task](https://docs.byteplus.com/en/docs/RDS_for_MySQL/changing_the_execution_time_of_a_task).<br> |
   |Risk Identification |Risks to the database proxy service after modifying the instance specification.<br><br>> **tip**<br><br><br>> Not all specification change operations require risk identification. If the database proxy is enabled for the instance, and its number of CPU cores is less than half of the total CPU cores of all service nodes after the configuration change, the system prompts you to expand the database proxy resources to handle higher database traffic. Confirm the prompt and select the checkbox to continue the process. After the instance specification change is complete, adjust the resources of the database proxy service. For more information about modifying database proxy service resources, refer to [Modify proxy configuration](https://docs.byteplus.com/en/docs/RDS_for_MySQL/changing_agent_configurations).<br> |

5. Click **Confirm order**.

6. Complete the subsequent steps based on the instance's billing method.

   * If the billing method of the instance is **Pay\-as\-you\-go**: on the **Confirm order** page, confirm the order details, read and check the **Database Products and Services Terms** and **Unsubscription rules**, and then click **Buy now** to complete the instance configuration change.

   * If the billing method of the instance is **Subscription**:

      1. On the **Confirm order** page, confirm the order details, read and check the **Database Products and Services Terms** and **Unsubscription rules**, and click **Submit the order**.

      2. On the **Confirm order information** page, reconfirm the order information, and click **Next step**.

      3. On the **Submit payment information** page, confirm the payment details, select a payment method, click **To pay**, and complete the payment as prompted to finish the instance configuration change.

## Related API

|API |Description |
|---|---|
|[ModifyDBNodeSpec](https://docs.byteplus.com/en/docs/RDS_for_MySQL/release_notes) |Call the ModifyDBNodeSpec API to change the instance specification. |
