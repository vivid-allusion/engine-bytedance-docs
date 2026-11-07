---
title: "Restarting instance, component, or node"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/restart-instance"
---

You can restart MongoDB instances, components, or nodes to release all connections on them, resolving database connection or performance issues. This topic describes how to manually restart MongoDB instances, components, or nodes on the console.

<span id="wHnD1IjJ"></span>
## Prerequisite

The instance status must be **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).

<span id="qRXEBiDz"></span>
## Precautions


* Different instance or component types support different restart operations:

   * Sharding cluster instance

      * Supports restarting instance.

      * Supports restarting Shard and ConfigServer components.

      * Supports restarting Mongos and Mongot nodes (if search functionality is enabled).

   * Replica set instance

      * Supports restarting instance.

      * Supports restarting nodes.

* During instance, component, or node restarts, access to some services may be affected for a short period. Proceed with caution.

* Restart instances during off\-peak hours and ensure your application has an automatic reconnection mechanism. It is highly recommended to use the full high\-availability connection address to access instances in a production environment. For more details on connection addresses, refer to [Viewing connection address](https://docs.byteplus.com/en/docs/mongodb/addresses-introduction).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


<Tabs>
<Tab zoneid="tLYul0djUS" title="Restart instance">
<TabTitle>Restart instance</TabTitle>

1. Log on to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the top menu bar, select the project and region for the instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, locate the target instance, and in the **Actions** column on the right, select  **...**   **\> Restart instance**.

5. In the pop\-up dialog box, confirm the instance information to be restarted and the operational impact, and click **OK**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When the instance status changes from <strong>Restarting</strong> to <strong>Running</strong>, it indicates that the instance is successfully restarted.   </div>
   


</Tab>
<Tab zoneid="bOCd76oxhk" title="Restart component">
<TabTitle>Restart component</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Only Shard and ConfigServer components in sharding cluster instances can be restarted.</div>



1. Log on to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the top menu bar, select the project and region for the instance.

3. In the left navigation bar, select **Sharding instances**.

4. On the **Sharding instances** page, click the target instance name.

5. In the **Node information** area under the **Summary** tab, complete the corresponding restarting operation based on the instance node type.

   
   |Component type |Procedure |
   |---|---|
   |Shard |1. In the **Node information** area, click the **Shards** tab.<br><br>2. Locate the target shard under the **Shards** tab, and in the right **Actions** column, select ... **\> Restart**.<br><br>3. In the pop\-up dialog box, confirm the operational impact, and click **OK**. |
   |ConfigServer<br><br> |1. In the **Node information** area, click the **ConfigServer** tab.<br><br>2. In the node list under the **ConfigServer** tab, click **Restart** in the **Actions** column on the right.<br><br>3. In the pop\-up dialog box, confirm the operational impact, and click **OK**. |
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When the instance status changes from <strong>Restarting</strong> to <strong>Running</strong>, it indicates that the component is successfully restarted.   </div>
   


</Tab>
<Tab zoneid="TL6TWdVLMb" title="Restart node">
<TabTitle>Restart node</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Only supports restarting replica set instances and Mongos and Mongot nodes in sharding cluster instances.</div>



1. Log on to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the top menu bar, select the project and region for the instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. In the **Node Information** area under the **Summary **  tab, complete the corresponding switch operation based on the instance node type.

   
   |Instance node type |Procedure |
   |---|---|
   |Replica set instance node |1. In the **Node information** area, find the node to restart.<br><br>2. In the **Actions** column on the right of the node, click **Restart**.<br><br>3. In the pop\-up dialog box, confirm the operational impact, and click **OK**. |
   |Mongos/Mongot nodes in sharding cluster instance<br><br> |1. In the **Node information** area, under the **Mongos/Mongot** tab, find the target node from the Mongos node list.<br><br>2. In the **Actions** column on the right of the node, click **Restart**.<br><br>3. In the pop\-up dialog box, confirm the operational impact, and click **OK**. |
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When the instance status changes from <strong>Restarting</strong> to <strong>Running</strong>, it indicates that the node is successfully restarted.   </div>
   


</Tab>
</Tabs>


<span id=".55u45YWzLWFwaQ=="></span>
## Relevant APIs


|API |Description |
|---|---|
|[RestartDBInstance](https://docs.byteplus.com/en/docs/mongodb/restartdbinstance) |Call the RestartDBInstance API to restart the target MongoDB instance. |
