---
title: "Modifying Mongos node configuration"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/modify-mongos-config"
---

You can flexibly change the configurations of Mongos nodes in a MongoDB sharding cluster instance based on business fluctuations, including upgrading or downgrading node specifications, increasing or decreasing node. This topic describes the relevant procedures.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The change configuration process may last for several minutes or even hours. During this period, the instance will enter the **Scaling** state, and no other operations on the instance are allowed (such as viewing instance details, managing accounts, or backups).

* During the change configuration process, there may be 1 to 2 brief disconnections, each lasting about 30 seconds. Exercise caution during operations. It is recommended to perform change configuration operations during off\-peak business hours and ensure the application supports automatic reconnection.

* After completing the change configuration, some parameter values will vary with the instance specifications. Please assess the impact of these changes on your business. For more information, refer to [Supported parameter](https://docs.byteplus.com/en/docs/mongodb/supported-parameter).


<span id=".5Y-Y6YWN6aKE5qOA5p-l"></span>
## Pre\-check for configuration change

Before performing instance configuration modification operation, the Document Database for MongoDB will pre\-check the health status of the instance to ensure that all health monitoring indicators of the instance meet the requirements for configuration change, reducing the possibility of abnormalities caused by configuration changes. If a relevant error occurs during the instance configuration change pre\-check phase, refer to the suggestions in [What should I do if an error occurs during the pre-check stage of changing the instance configuration](https://docs.byteplus.com/en/docs/mongodb/change-instance-config-faq#knmitzxI) to resolve it.

<span id=".6LS555So6K-05piO"></span>
## Billing information

For details on the billing rules for changing instance configurations, refer to [Pay-as-you-go](https://docs.byteplus.com/en/docs/mongodb/pay-as-you-go#.5Y-Y5pu06YWN572u) and [Subscription](https://docs.byteplus.com/en/docs/mongodb/subscription#.5Y-Y5pu06YWN572u).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [MongoDB console](https://console.byteplus.com/db/region:db+cn-beijing/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. In the left navigation bar, select **Sharding instances**.

4. Select any of the following methods to access the instance **Modify configuration** page, and set the relevant Mongos configuration parameters.

   
   <Tabs>
   <Tab zoneid="rG4HkyxXZz" title="Method 1">
   <TabTitle>Method 1</TabTitle>
   
   1. On the **Sharding instances** page, locate the target instance, and click **Modify configuration** in the **Actions** column.
   
      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
      
   
      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the instance contains read\-only node, the <strong>Modify configuration</strong> button is grayed. You can choose method 2 to modify the Mongos configuration.   </div>
      
   
   2. In the **Modify configuration** area on the **Modify configuration** page, set the following parameters.
   
      
      |Parameter |Description |
      |---|---|
      |Instance type |Fixed as **Sharding cluster**. No configuration required. |
      |Availability zone |It is fixed to the availability zone currently selected for the instance; no configuration is required.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To modify the number of read\-only nodes in a sharding cluster instance, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/add-or-remove-read-only-node">Adding or deleting read\-only nodes</a>.</div><br> |
      |Batch modify Mongos |Enable **Batch modify Mongos**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can modify the shard configurations on the <strong>Modify configuration</strong> page. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/modify-shard-config">Modifying Shard configuration</a>.</div><br> |
      |Number of node(s) |You can increase or decrease Mongos node, or keep it unchanged. Valid value range: 2 to 32. |
      |Node specification |You can upgrade or downgrade Mongos node specifications. Each Mongos node in the instance has the same specifications. For more details, refer to [Compute node specifications](https://docs.byteplus.com/en/docs/mongodb/product-specification#.5YiG54mH6ZuG576k5a6e5L6L). |
      
   
   
   
   
   
   </Tab>
   <Tab zoneid="QTUWGDg1wt" title="Method 2">
   <TabTitle>Method 2</TabTitle>
   
   1. On the **Sharding instances** page, click the target instance name.
   
   2. In the **Node information** area under the **Summary** tab, click **Batch modify configuration** under **Mongos** tab.
   
   3. In the **Modify configuration** area on the **Modify configuration** page, set the following parameters.
   
      
      |Parameter |Description |
      |---|---|
      |Instance type |Fixed as **Sharding cluster**. No configuration required. |
      |Availability zone |It is fixed to the availability zone currently selected for the instance; no configuration is required.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To modify the number of read\-only nodes in a sharding cluster instance, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/add-or-remove-read-only-node">Adding or deleting read\-only nodes</a>.</div><br> |
      |Number of node(s) |You can increase or decrease Mongos node, or keep it unchanged. Valid value range: 2 to 32. |
      |Node specification |You can upgrade or downgrade Mongos node specifications. Each Mongos node in the instance has the same specifications. For more details, refer to [Compute node specifications](https://docs.byteplus.com/en/docs/mongodb/product-specification#.5YiG54mH6ZuG576k5a6e5L6L). |
      
   
   
   
   
   
   </Tab>
   </Tabs>
   

5. Review the updated specification details (such as number of nodes), then click **Confirm order** in the bottom right corner of the page.

6. Complete the subsequent steps according to the billing method you have selected.

   
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
