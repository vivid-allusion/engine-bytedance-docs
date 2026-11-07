---
title: "Changing node specifications"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Changing_node_specifications"
---

You can change the instance configuration based on business requirements, and this article describes how to change the node specification of an instance.

## Prerequisites

* The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1).

* The instance currently has no **pending** configuration change events. You can search and view them by instance ID in the **Planned event** list. For steps, see [Viewing event list](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Viewing_event_list).

## Precautions

* During the node specification change process, the instance will be restarted and the primary node will be switched.

   * Change order: First make configuration changes to the read\-only nodes, then make configuration changes to the primary node.

   * Impact: During the configuration change, the database may experience a 20\-30 second disconnection. Therefore, it is recommended to perform configuration changes during off\-peak hours and ensure that the application has an automatic reconnection mechanism.

* The time required to change node specifications mainly depends on the number of nodes in the instance. Under normal circumstances, the time required for each computing node to change is approximately 5 minutes. For example, when an instance with 2 nodes is upgraded from 4C to 8C, the total time taken is about 10 minutes.

* Expanding or scaling down the storage space has no impact on the instance. When scaling down, if the input storage space capacity is less than the storage space capacity used by the instance, the excess storage capacity will be charged on a usage\-based basis.

* Before changing the configuration, check whether there is an Online DDL task in progress on the instance. Changing the configuration will interrupt the task, so proceed with caution. For more information, see [Viewing ticket](https://docs.byteplus.com/en/docs/DBW/Managing_data_change_tickets#.5p-l55yL5bel5Y2V)s.

* Before changing the instance configuration, confirm if any scheduled auto\-scaling rules exist. If so, manually changing the instance configuration may invalidate these rules. For details about scheduled scaling, refer to [Scheduled scaling management](https://docs.byteplus.com/en/docs/DBW/scheduled-scaling-management?lang=en).

* You can upgrade or downgrade the specifications of General type instances without a restart under certain conditions. Instances of earlier versions do not support this feature directly. You must first enable fast specification change on the instance details page. Once it is enabled, you can change the node specification. For specific steps, refer to [Enabling fast specification change](https://bytedance.larkoffice.com/docx/XZXIdafphoaMVCxyHajcDwI9n9b#share-LKoYd4XMDo3EUvxjkyNcHoiNnvL).

   > **tip**

   > This is an allowlist feature. To use it, [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical support and apply.

## Procedure

1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the top menu bar, select the project and region for the instance.

3. On the **Instances** page, select **Modify configuration** \> **Change specification** for the Target Instance **Actions** column.

4. Reset the following parameters according to business requirements.

   |Name |Description |
   |---|---|
   |Specification type |Please select the specification type. For more information on node specifications, see [Product specifications](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Product_specifications).<br><br><br>* **Exclusive type**: Completely exclusive CPU and memory, long\-term stable performance, will not be affected by the behavior of other instances on the physical machine. The top of the exclusive specification is exclusive TCE\-metal, completely monopolizing all the resources of a TCE\-metal.<br><br>* **General type**: Exclusive access to allocated memory, sharing CPU resources with other generic instances on the same physical machine. Enjoy scale dividends through resource reuse, with high cost performance. |
   |Node specification |Select node specifications for primary nodes, read\-only nodes. Each specification has a corresponding number of cores and memory, and you can choose according to your business requirements. For more information on node specifications, see[ Product specifications](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Product_specifications).<br><br>> **tip**<br><br><br>> The node specifications of the primary and read\-only nodes are consistent by default.<br> |
   |Storage space |* If the storage billing type is pay\-as\-you\-go, you do not need to select storage capacity. The storage capacity will automatically scale up and down as the amount of data increases or decreases, and will be billed on an hourly basis based on actual usage.<br><br>* If the storage billing type is yearly or monthly subscription, you need to enter the changed storage space size in steps of 10 GiB.<br><br>   > **warning**<br>   <br><br>   > When scaling down, if the input storage space capacity is less than the storage space capacity used by the instance, the excess storage capacity will be charged on a usage\-based basis.<br>    |
   |Storage type |Displays the storage type of the instance. For more information about storage types, refer to [Product specifications](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Product_specifications). |
   |Estimated impact |Displays the impact of changing the instance specification.<br><br>> **tip**<br><br><br><br>* > The estimated impact is based on the resource state when the configuration is completed on the Modify configuration page. The resource state may change when the configuration change order is submitted or when the change is applied. Therefore, the estimated impact may not occur, and the actual impact prevails.<br><br><br>* > In some cases, the impact cannot be estimated due to system reasons. Click **Re\-evaluate** on the page.<br> |
   |Restart after changes |You can upgrade or downgrade the specifications of General type instances without a restart under certain conditions.<br><br>If you select the restart option, the instance will restart after you confirm the order. The read/write connection will be momentarily interrupted during the restart. Ensure your application has a reconnection mechanism.<br><br>> **tip**<br><br><br>> This parameter can be selected when the **Specification type** is **General type**.<br> |
   |Execution method |Select the execution method and choose the value:<br><br><br>* **Execute now** (default): Deduct or refund the fee immediately and perform the configuration change operation. The instance enters the **Configuration modifying** state. At this time, other operations are not allowed on the instance.<br><br>* **Execute during maintainable window**: Deductions or refunds are made during the maintenance time period, and configuration changes are performed. For details about the maintenance time window, see [Configuring maintenance window](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Configuring_maintenance_window).<br><br>   > **tip**<br>   <br><br>   > You can also click **Edit** next to the **Current maintainable window** to modify the current maintenance time period. Modifying the maintenance time period takes effect on all scheduled events in the **pending** state for the instance. Please proceed with caution.<br>    |

5. Click **Confirm order**.

6. On the **Confirm order** page, after confirming that the instance configuration is correct, read and check the **Database Products and Services Terms**.  If you choose to **Execute during maintainable window**, you also need to check the fee description.

7. Then click ** Buy now** to change the configuration of the instance.

## Related APIs

|API |Description |Version |
|---|---|---|
|[ModifyDBInstanceName](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceName) |Call ModifyDBInstanceName to modify the instance name. |2022\-01\-01 |
|[ModifyDBInstanceSpec](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceSpec_v2) |Call the ModifyDBInstanceSpec to modify the node configuration of the instance. |2024\-01\-01 |
|[ModifyDBInstanceSpecDryRun](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceSpecDryRun) |Call the ModifyDBInstanceSpecDryRun API to view the estimated impact of modifying the instance specification. |2024\-01\-01 |
