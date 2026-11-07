---
title: "Modifying shard configuration"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/modify-shard-config"
---

You can flexibly change the configurations of one or more shards in a MongoDB sharding cluster instance based on business fluctuations, including upgrading or downgrading node specifications, increasing or decreasing shard and storage capacity. This topic describes the relevant procedures.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The change configuration process may last for several minutes or even hours. During this period, the instance will enter the **Scaling** state, and no other operations on the instance are allowed (such as viewing instance details, managing accounts, or backups).

* During the change configuration process, there may be 1 to 2 brief disconnections, each lasting about 30 seconds. Exercise caution during operations. It is recommended to perform change configuration operations during off\-peak business hours and ensure the application supports automatic reconnection.

* After completing the change configuration, some parameter values will vary with the instance specifications. Please assess the impact of these changes on your business. For more information, refer to [Supported parameter](https://docs.byteplus.com/en/docs/mongodb/supported-parameter).

* FlexPL volume instances do not support storage space reduction.


<span id="eRHFZkBB"></span>
## Pre\-check for configuration change

Before performing instance configuration modification operation, the Document Database for MongoDB will pre\-check the health status of the instance to ensure that all health monitoring indicators of the instance meet the requirements for configuration change, reducing the possibility of abnormalities caused by configuration changes. If a relevant error occurs during the instance configuration change pre\-check phase, refer to the suggestions in [What should I do if an error occurs during the pre-check stage of changing the instance configuration](https://docs.byteplus.com/en/docs/mongodb/change-instance-config-faq#knmitzxI) to resolve it.

<span id=".6LS555So6K-05piO"></span>
## Billing information

For details on the billing rules for changing instance configurations, refer to [Pay-as-you-go](https://docs.byteplus.com/en/docs/mongodb/pay-as-you-go#.5Y-Y5pu06YWN572u) and [Subscription](https://docs.byteplus.com/en/docs/mongodb/subscription#.5Y-Y5pu06YWN572u).

<span id=".5Y-Y5pu05oyH5a6aLXNoYXJkLeWIhueJh-mFjee9rg=="></span>
## Modifying configuration of single shard


1. Log on to the [MongoDB console](https://console.byteplus.com/db/region:db+cn-beijing/mongodb).

2. In the top menu bar, select the project and region for the instance.

3. In the left navigation bar, select **Sharding instances**.

4. On the **Sharding instances** page, click the target instance name.

5. In the **Node information** area under the **Summary** tab, click the **Shards** tab.

6. Locate the target shard under the **Shards** tab, and in the **Actions** column on the right, click **Modify configuration**.

7. In the **Modify configuration** area on the **Modify configuration** page, set the following parameters.

   
   |Parameter |Description |
   |---|---|
   |Instance type |Fixed as **Sharding cluster**. No configuration required. |
   |Availability zone |It is fixed to the availability zone currently selected for the instance; no configuration is required.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Changing the number of read\-only nodes is mutually exclusive with other configuration change operations of the shard. That is, when changing the node specification or storage space for the shard, changing the number of read\-only nodes simultaneously is not supported. For more information about read\-only nodes, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/managing_read_only_nodes">MongoDB read\-only nodes</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">To modify the number of read\-only nodes in a sharding cluster instance, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/add-or-remove-read-only-node">Adding or deleting read\-only nodes</a>.</div><br> |
   |Number of node(s) per shard |Each shard contains 3 nodes by default. No configuration is required. |
   |Node specification |You can upgrade or downgrade shard node specifications. Each node in each shard has the same specifications. For more details, refer to [Compute node specifications](https://docs.byteplus.com/en/docs/mongodb/product-specification#.5YiG54mH6ZuG576k5a6e5L6L).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If read\-only nodes exist in the instance, modifying specification of shard node will also modify specifications of read\-only nodes within that shard.</div><br> |
   |Storage space |You can increase or decrease storage space, or keep it unchanged. Unit: GiB. Step: 10.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Node specifications are different, and the supported storage space ranges are also different. For the specific value range of storage space, refer to the console. If you need more storage, <a href="https://console.byteplus.com/workorder/create/">submit a ticket</a> to contact technical support to increase the storage space limit.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When modifying storage space, the modified storage space capacity must be <strong>greater than or equal to 1.2 times</strong> the used space to ensure the instance operates normally.</div><br> |
   

8. Review the updated specification details (such as number of shards, number of nodes and storage space), then click **Confirm order** in the bottom right corner of the page.

9. Complete the subsequent steps according to the billing method you have selected.

   
   |Billing method |Procedure |
   |---|---|
   |Pay\-as\-you\-go |On the **Confirm order** page, confirm the order details, read and check the service terms, and then click **Buy now**. |
   |Subscription |1. On the **Confirm order** page, confirm the order details, read and check the service terms, and then click **Submit order**.<br><br>2. On the **Confirm order information** page, confirm the order details again and then click **Next step**.<br><br>3. On the **Submit payment information** page, confirm the payment details and select the payment method, and then click **Go to pay**. |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The instance status changes to <strong>Configuration modifying</strong>, indicating that modification is in progress. When the instance status displays as <strong>Running</strong>, it indicates that the modification was successful.   </div>
   

<span id=".5om56YeP5Y-Y5pu0LXNoYXJkLeWIhueJh-mFjee9rg=="></span>
## Modifying configuration of multiple shards

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only when there is <strong>no read\-only node</strong> in a sharding cluster instance and the configurations (including node specifications and storage space) of all Shard are the same, is the function of batch modifying Shard configurations supported. For more information about read\-only nodes, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/managing_read_only_nodes">MongoDB read\-only nodes</a>.</div>



1. Log on to the [MongoDB console](https://console.byteplus.com/db/region:db+cn-beijing/mongodb).

2. In the top menu bar, select the project and region for the instance.

3. In the left navigation bar, select **Sharding instances**.

4. On the **Sharding instances** page, locate the target instance, and click **Modify configuration** in the **Actions** column.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the instance contains read\-only node, the <strong>Modify configuration</strong> button is grayed, that is, batch changing shard configurations is not supported.   </div>
   

5. In the **Modify configuration** area on the **Modify configuration** page, set the following parameters.

   
   |Parameter |Description |
   |---|---|
   |Instance type |Fixed as **Sharding cluster**. No configuration required. |
   |Availability zone |It is fixed to the availability zone currently selected for the instance; no configuration is required.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To modify the number of read\-only nodes in a sharding cluster instance, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/add-or-remove-read-only-node">Adding or deleting read\-only nodes</a>.</div><br> |
   |Batch modify Shard |Enable **Batch modify Shard**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When configurations (including node specifications and storage capacity) of different shards in one instance are different, <strong>Batch modify Shard</strong> cannot be enabled, that is, batch changing shard configurations is not supported.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can modify the Mongos node configurations on the <strong>Modify configuration</strong> page. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/modify-mongos-config">Modifying Mongos node configuration</a>.</div><br> |
   |Number of shard(s) |You can increase or keep the number of shards, but decreasing them is not supported. |
   |Number of node(s) per shard |Each shard contains 3 nodes by default. No configuration is required. |
   |Node specification |You can upgrade or downgrade shard node specifications. Each node in each shard has the same specifications. For more details, refer to [Compute node specifications](https://docs.byteplus.com/en/docs/mongodb/product-specification#.5YiG54mH6ZuG576k5a6e5L6L). |
   |Storage space |You can increase storage space, or keep it unchanged. Unit: GiB. Step: 10.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Node specifications are different, and the supported storage space ranges are also different. For the specific value range of storage space, refer to the console. If you need more storage, <a href="https://console.byteplus.com/workorder/create/">submit a ticket</a> to contact technical support to increase the storage space limit.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When modifying storage space, the modified storage space capacity must be <strong>greater than or equal to 1.2 times</strong> the used space to ensure the instance operates normally.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Reducing storage space is not supported when batch modifying shard configuration. To reduce storage space, perform the corresponding operation separately for the specific shard individually. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/modify-shard-config#.5Y-Y5pu05oyH5a6aLXNoYXJkLeWIhueJh-mFjee9rg==">Modifying configuration of single shard</a>.</div><br> |
   

6. Review the updated specification details (such as number of shards, number of nodes and storage space), then click **Confirm order** in the bottom right corner of the page.

7. Complete the subsequent steps according to the billing method you have selected.

   
   |Billing method |Procedure |
   |---|---|
   |Pay\-as\-you\-go |On the **Confirm order** page, confirm the order details, read and check the service terms, and then click **Buy now**. |
   |Subscription |1. On the **Confirm order** page, confirm the order details, read and check the service terms, and then click **Submit order**.<br><br>2. On the **Confirm order information** page, confirm the order details again and then click **Next step**.<br><br>3. On the **Submit payment information** page, confirm the payment details and select the payment method, and then click **Go to pay**. |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The instance status changes to <strong>Configuration modifying</strong>, indicating that modification is in progress. When the instance status displays as <strong>Running</strong>, it indicates that the modification was successful.   </div>
   

<span id=".5re75YqgLXNoYXJkLeWIhueJhw=="></span>
## Adding shard

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Currently, only adding shard is supported; reducing shard is not supported.</div>


* <div data-tips="true" data-tips-type="tip">After adding new shards, the system requires some time to rebalance the data across the new shards. The time required is proportional to the data volume. The full scaling capacity of the added shards will not be available until the rebalancing process has completed. Wait for this process to finish.</div>


1. Log on to the [MongoDB console](https://console.byteplus.com/db/region:db+cn-beijing/mongodb).

2. In the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the target instance name.

4. In the **Node information** area under the **Summary** tab, click the **Shards** tab.

5. On the **Shards** tab, click **Add shard**.

6. In the **Modify configuration** area on the **Modify configuration** page, set the following parameters.

   
   |Parameter |Description |
   |---|---|
   |Instance type |Fixed as **Sharding cluster**. No configuration required. |
   |Availability zone |It is fixed to the availability zone currently selected for the instance; no configuration is required.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When adding a shard, you can set the number of read\-only nodes for the shard. Each Shard can add up to 5 read\-only nodes. For more details on read\-only node feature introduction and limits, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/managing_read_only_nodes">MongoDB read\-only nodes</a>.</div><br> |
   |Number of shard(s) |Set the number of shards to add. A single instance can have up to 32 shards. |
   |Number of node(s) per shard |Each shard contains 3 nodes by default. No configuration is required. |
   |Node specification |Set node specifications for the shards. Each node in each shard has the same specifications. For more details, refer to [Compute node specifications](https://docs.byteplus.com/en/docs/mongodb/product-specification#.5YiG54mH6ZuG576k5a6e5L6L).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the new shard contains read\-only node, the specification of the read\-only is the same as the specification of the primary and secondary nodes of the shard.</div><br> |
   |Storage space |Set the storage capacity for the new shard. Unit: GiB. Step: 10.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Node specifications are different, and the supported storage space ranges are also different. For the specific value range of storage space, refer to the console. If you need more storage, <a href="https://console.byteplus.com/workorder/create/">submit a ticket</a> to contact technical support to increase the storage space limit.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When modifying storage space, the modified storage space capacity must be <strong>greater than or equal to 1.2 times</strong> the used space to ensure the instance operates normally.</div><br> |
   

7. Review the updated specification details (such as number of shards, number of nodes and storage space), then click **Confirm order** in the bottom right corner of the page.

8. Complete the subsequent steps according to the billing method you have selected.

   
   |Billing method |Procedure |
   |---|---|
   |Pay\-as\-you\-go |On the **Confirm order** page, confirm the order details, read and check the service terms, and then click **Buy now**. |
   |Subscription |1. On the **Confirm order** page, confirm the order details, read and check the service terms, and then click **Submit order**.<br><br>2. On the **Confirm order information** page, confirm the order details again and then click **Next step**.<br><br>3. On the **Submit payment information** page, confirm the payment details and select the payment method, and then click **Go to pay**. |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The instance status changes to <strong>Configuration modifying</strong>, indicating that modification is in progress. When the instance status displays as <strong>Running</strong>, it indicates that the modification was successful.   </div>
   

<span id=".55u45YWzLWFwaQ=="></span>
## Relevant APIs


|API |Description |
|---|---|
|[ModifyDBInstanceSpec](https://docs.byteplus.com/en/docs/mongodb/modifydbinstancespec) |Call the ModifyDBInstanceSpec API to modify the configuration of the target MongoDB instance (such as node specification or storage capacity). |
