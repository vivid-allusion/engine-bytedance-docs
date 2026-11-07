---
title: "Adding or deleting read-only nodes"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/add-or-remove-read-only-node"
---

Document Database for MongoDB supports the read\-only node feature. You can flexibly adjust the read\-only node configuration of your MongoDB instance based on changes in instance read request volume. This document describes the specific procedure for adding or deleting read\-only nodes in MongoDB.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Currently, only replica set instances and Shard in sharding cluster instances support using read\-only nodes. For more details on read\-only node feature introduction and limits, refer to [MongoDB read-only nodes](https://docs.byteplus.com/en/docs/mongodb/managing_read_only_nodes).

* The specifications of read\-only nodes are consistent with those of the primary and secondary nodes of the instance (or Shard). Therefore, when upgrading or downgrading the specifications of a replica set instance or the specifications of Shard nodes in a sharding cluster, the specifications of the added read\-only nodes will also be changed synchronously. For methods to change replica set instance specifications and Shard node specifications of sharding cluster instances, refer to [Modifying replica set instance specification](https://docs.byteplus.com/en/docs/mongodb/modify-replica-set-instance-spec) and [Modifying Shard configuration](https://docs.byteplus.com/en/docs/mongodb/modify-shard-config).


<span id=".5Y-Y6YWN6aKE5qOA5p-l"></span>
## Pre\-check for configuration change

Before performing instance configuration modification operation, the Document Database for MongoDB will pre\-check the health status of the instance to ensure that all health monitoring indicators of the instance meet the requirements for configuration change, reducing the possibility of abnormalities caused by configuration changes. If a relevant error occurs during the instance configuration change pre\-check phase, refer to the suggestions in [What should I do if an error occurs during the pre-check stage of changing the instance configuration](https://docs.byteplus.com/en/docs/mongodb/change-instance-config-faq#knmitzxI) to resolve it.

<span id=".6LS555So6K-05piO"></span>
## Billing information

The fee calculation rules for configuration changes of read\-only nodes are consistent with those for other configuration changes of instances sharing the same billing type. For more details, refer to [Pay-as-you-go](https://docs.byteplus.com/en/docs/mongodb/pay-as-you-go#.5Y-Y5pu06YWN572u) and [Subscription](https://docs.byteplus.com/en/docs/mongodb/subscription#.5Y-Y5pu06YWN572u).

<span id=".5re75Yqg5Y-q6K-76IqC54K5"></span>
## Add read\-only node


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. In the **Node information** area under the **Summary** tab, select the corresponding procedure based on the instance or component type, access the **Modify configuration** page to add read\-only node.

   
   <Tabs>
   <Tab zoneid="cpusve6n2p" title="Add read-only node for replica set instance">
   <TabTitle>Add read-only node for replica set instance</TabTitle>
   
   1. In the **Node information** area, click **Add read\-only node**.
   
   2. In the **Modify configuration** area on the **Modify configuration** page, set the following parameters.
   
      
      |Parameter |Description |
      |---|---|
      |Instance type |Fixed as **Replica set**. No configuration required. |
      |Availability zone |At the right of the availability zone, set the number of read\-only nodes after addition.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Each replica set instance can add up to 5 read\-only nodes. For more details on read\-only node feature introduction and limits, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/managing_read_only_nodes">MongoDB read\-only nodes</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You do not need to set the availability zone; it is fixed to the selected availability zone of the instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Changing the number of read\-only nodes is mutually exclusive with other configuration changes for replica set instances. Therefore, you cannot simultaneously change node specifications or storage space when modifying the number of read\-only nodes. To change other configurations of replica set instance, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/modify-replica-set-instance-spec">Modifying replica set instance specification</a>.</div><br> |
      
   
   
   
   
   
   </Tab>
   <Tab zoneid="aB9wa6heP7" title="Add read-only node for specified shard">
   <TabTitle>Add read-only node for specified shard</TabTitle>
   
   1. In the **Node information** area, click the **Shards** tab.
   
   2. Locate the target shard under the **Shards** tab, and in the **Actions** column on the right, click **Add read\-only node**.
   
   3. In the **Modify configuration** area on the **Modify configuration** page, set the following parameters.
   
      
      |Parameter |Description |
      |---|---|
      |Instance type |Fixed as **Sharding cluster**. No configuration required. |
      |Availability zone |At the right of the availability zone, set the number of read\-only nodes after addition.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Each Shard can add up to 5 read\-only nodes. For more details on read\-only node feature introduction and limits, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/managing_read_only_nodes">MongoDB read\-only nodes</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You do not need to set the availability zone; it is fixed to the selected availability zone of the instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Changes to the number of read\-only nodes are mutually exclusive with other configuration changes for Shard. Therefore, you cannot simultaneously change node specifications or storage space for Shard when modifying the number of read\-only nodes. To change other configurations of Shard, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/modify-shard-config">Modifying Shard configuration</a>.</div><br> |
      
   
   
   
   
   
   </Tab>
   </Tabs>
   

6. Review the updated specification details (such as number of shards, number of nodes and storage space), then click **Confirm order** in the bottom right corner of the page.

7. Complete the subsequent steps according to the billing method you have selected.

   
   |Billing method |Procedure |
   |---|---|
   |Pay\-as\-you\-go |On the **Confirm order** page, confirm the order details, read and check the service terms, and then click **Buy now**. |
   |Subscription |1. On the **Confirm order** page, confirm the order details, read and check the service terms, and then click **Submit order**.<br><br>2. On the **Confirm order information** page, confirm the order details again and then click **Next step**.<br><br>3. On the **Submit payment information** page, confirm the payment details and select the payment method, and then click **Go to pay**. |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The instance status changes to <strong>Configuration modifying</strong>, indicating that modification is in progress. When the instance status displays as <strong>Running</strong>, it indicates that the modification was successful.   </div>
   

<span id=".5Yig6Zmk5Y-q6K-76IqC54K5"></span>
## Delete read\-only nodes


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. In the **Node information** area under the **Summary** tab, select the corresponding procedure based on the instance or component type, access the **Modify configuration** page to delete read\-only node.

   
   <Tabs>
   <Tab zoneid="h88cw7MUNV" title="Delete read-only node for replica set instance">
   <TabTitle>Delete read-only node for replica set instance</TabTitle>
   
   1. In the **Node information** area, click **Delete read\-only node**.
   
   2. In the **Modify configuration** area on the **Modify configuration** page, set the following parameters.
   
      
      |Parameter |Description |
      |---|---|
      |Instance type |Fixed as **Replica set**. No configuration required. |
      |Availability zone |At the right of the availability zone, set the number of read\-only nodes after deletion.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can reduce to 0 read\-only nodes, which means deleting all read\-only nodes in the instance. For more details on read\-only node feature introduction and limits, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/managing_read_only_nodes">MongoDB read\-only nodes</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You do not need to set the availability zone; it is fixed to the selected availability zone of the instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Changing the number of read\-only nodes is mutually exclusive with other configuration changes for replica set instances. Therefore, you cannot simultaneously change node specifications or storage space for instance when modifying the number of read\-only nodes. To change other configurations of replica set instance, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/modify-replica-set-instance-spec">Modifying replica set instance specification</a>.</div><br> |
      
   
   
   </Tab>
   <Tab zoneid="tvgZCNfjpq" title="Delete read-only node for specified shard">
   <TabTitle>Delete read-only node for specified shard</TabTitle>
   
   1. In the **Node information** area, click the **Shards** tab.
   
   2. Locate the target shard under the **Shards** tab, and in the **Actions** column on the right, select  **... \> Delete read\-only node**.
   
   3. In the **Modify configuration** area on the **Modify configuration** page, set the following parameters.
   
      
      |Parameter |Description |
      |---|---|
      |Instance type |Fixed as **Sharding cluster**. No configuration required. |
      |Availability zone |At the right of the availability zone, set the number of read\-only nodes after addition.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can reduce to 0 read\-only nodes, which means deleting all read\-only nodes in the current shard. For more details on read\-only node feature introduction and limits, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/managing_read_only_nodes">MongoDB read\-only nodes</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You do not need to set the availability zone; it is fixed to the selected availability zone of the instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Changes to the number of read\-only nodes are mutually exclusive with other configuration changes for Shard. Therefore, you cannot simultaneously change node specifications or storage space for Shard when modifying the number of read\-only nodes. To change other configurations of Shard, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/modify-shard-config">Modifying Shard configuration</a>.</div><br> |
      
   
   
   </Tab>
   </Tabs>
   

6. Review the updated specification details (such as number of shards, number of nodes and storage space), then click **Confirm order** in the bottom right corner of the page.

7. Complete the subsequent steps according to the billing method you have selected.

   
   |Billing method |Procedure |
   |---|---|
   |Pay\-as\-you\-go |On the **Confirm order** page, confirm the order details, read and check the service terms, and then click **Buy now**. |
   |Subscription |1. On the **Confirm order** page, confirm the order details, read and check the service terms, and then click **Submit order**.<br><br>2. On the **Confirm order information** page, confirm the order details again and then click **Next step**.<br><br>3. On the **Submit payment information** page, confirm the payment details and select the payment method, and then click **Go to pay**. |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The instance status changes to <strong>Configuration modifying</strong>, indicating that modification is in progress. When the instance status displays as <strong>Running</strong>, it indicates that the modification was successful.   </div>
