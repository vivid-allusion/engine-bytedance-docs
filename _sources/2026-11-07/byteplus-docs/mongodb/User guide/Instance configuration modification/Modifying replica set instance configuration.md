---
title: "Modifying replica set instance configuration"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/modify-replica-set-instance-spec"
---

You can flexibly change the configurations of MongoDB replica set instance based on business fluctuations, including upgrading or downgrading node specifications, increasing or decreasing storage space. This topic describes the relevant procedures.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The change configuration process may last for several minutes or even hours. During this period, the instance will enter the **Scaling** state, and no other operations on the instance are allowed (such as viewing instance details, managing accounts, or backups).

* During the change configuration process, there may be 1 to 2 brief disconnections, each lasting about 30 seconds. Exercise caution during operations. It is recommended to perform change configuration operations during off\-peak business hours and ensure the application supports automatic reconnection.

* After completing the change configuration, some parameter values will vary with the instance specifications. Please assess the impact of these changes on your business. For more information, refer to [Supported parameter](https://docs.byteplus.com/en/docs/mongodb/supported-parameter).

* FlexPL volume instances do not support storage space reduction.


<span id=".5Y-Y6YWN6aKE5qOA5p-l"></span>
## Pre\-check for configuration change

Before performing instance configuration modification operation, the Document Database for MongoDB will pre\-check the health status of the instance to ensure that all health monitoring indicators of the instance meet the requirements for configuration change, reducing the possibility of abnormalities caused by configuration changes. If a relevant error occurs during the instance configuration change pre\-check phase, refer to the suggestions in [What should I do if an error occurs during the pre-check stage of changing the instance configuration](https://docs.byteplus.com/en/docs/mongodb/change-instance-config-faq#knmitzxI) to resolve it.

<span id=".6LS555So6K-05piO"></span>
## Billing information

For details on the billing rules for changing instance configurations, refer to [Pay-as-you-go](https://docs.byteplus.com/en/docs/mongodb/pay-as-you-go#.5Y-Y5pu06YWN572u) and [Subscription](https://docs.byteplus.com/en/docs/mongodb/subscription#.5Y-Y5pu06YWN572u).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [MongoDB console](https://console.byteplus.com/db/region:db+cn-beijing/mongodb).

2. In the top menu bar, select the project and region for the instance.

3. Select any of the following methods to access the instance **Modify configuration** page.

   * Method 1

      On the **Replica set instances** page, locate the target instance, and click **Modify configuration** in the **Actions** column.

   * Method 2

      1. On the **Replica set instances** page, click the name of the target instance.

      2. In the **Node information** area under the **Summary** tab, click **Modify configuration**.

4. In the **Modify configuration** area on the **Modify configuration** page, set the following parameters.

   
   |Parameter |Description |
   |---|---|
   |Instance type |Fixed as **Replica set**; no configuration is required. |
   |Availability zone |It is fixed to the availability zone currently selected for the instance; no configuration is required.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For replica set instances, changing the number of read\-only nodes is mutually exclusive with other configuration change operations of the instance. That is, when changing the node specification or storage space, changing the number of read\-only nodes simultaneously is not supported. To modify the number of read\-only nodes in the instance, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/add-or-remove-read-only-node">Adding or deleting read\-only nodes</a>.</div><br> |
   |Number of nodes |Replica set instances adopt a 3\-node high availability architecture by default; no configuration is required. |
   |Node specification |You can upgrade or downgrade the node specification. For more details on node specifications, refer to [Compute node specifications](https://docs.byteplus.com/en/docs/mongodb/product-specification#.5Ymv5pys6ZuG5a6e5L6L).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If read\-only nodes exist in the instance, modifying specification of replica set instance node will also modify specifications of read\-only nodes within the instance.</div><br> |
   |Storage space |You can increase or decrease storage space, or keep it unchanged. Unit: GiB. Step: 10.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Node specifications are different, and the supported storage space ranges are also different. For the specific value range of storage space, refer to the console. If you need more storage, <a href="https://console.byteplus.com/workorder/create/">submit a ticket</a> to contact technical support to increase the storage space limit.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When modifying storage space, the modified storage space capacity must be <strong>greater than or equal to 1.2 times</strong> the used space to ensure the instance operates normally.</div><br> |
   

5. Review the updated specification details (such as number of shards, node specification and storage space), then click **Confirm order** in the bottom right corner of the page.

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
