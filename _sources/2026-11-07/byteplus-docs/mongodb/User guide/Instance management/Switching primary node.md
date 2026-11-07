---
title: "Switching primary node"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/switch-primary-node"
---

MongoDB allows you to manually switch the traffic from a secondary node to the primary node to meet the needs of the business connection in the vicinity based on the business deployment. This topic introduces how to switch to the primary node.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite


* The instance status must be **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).

* The node to be manually switched is a **secondary node** of an instance or a component of any of the following types:

   * Replica set instance

   * Shard within sharding cluster instance

   * ConfigServer components within sharding cluster instance


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* During the process of manually switching primary node role (generally taking 30 to 60 seconds), the instance may experience 1 to 2 transient connection drops. Proceed with caution. It is recommended to perform switching operations during off\-peak hours and ensure that the application has an automatic reconnect mechanism.

* Primary node role switchover only changes the role of the node; it does not alter the node's availability zone or node ID.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. In the **Node information** area under the **Summary** tab, complete the corresponding switching operation based on the instance or component type.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">During the process of manually switching primary node role (generally taking 30 to 60 seconds), the instance may experience 1 to 2 transient connection drops. Proceed with caution. It is recommended to perform switching operations during off\-peak hours and ensure that the application has an automatic reconnect mechanism.   </div>
   

   
   |Instance or component type ||Procedure |
   |---|---|---|
   |Replica set instance ||1. In the **Node information** area, locate the target secondary node.<br><br>2. To the right of the secondary node, in the **Actions** column, click **Switch to primary node**.<br><br>3. In the pop\-up dialog box, confirm the operational impact, and click **OK**. |
   |Sharding cluster instance |Shard |1. In the **Node information** area, click the **Shards** tab.<br><br>2. Locate the target shard under the **Shards** tab.<br><br>3. Click the leftmost icon <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ac21943d108c371a5d4da83f1fc6351d.png) </span> of the target shard, and find the target secondary node in the node list below.<br><br>4. To the right of the secondary node, in the **Actions** column, click **Switch to primary node**.<br><br>5. In the pop\-up dialog box, confirm the operational impact, and click **OK**. |
   ||ConfigServer |1. In the **Node information** area, click the **ConfigServers** tab.<br><br>2. Click the leftmost icon <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ac21943d108c371a5d4da83f1fc6351d.png) </span> in the ConfigServers list, and find the target secondary node in the node list below.<br><br>3. To the right of the secondary node, in the **Actions** column, click **Switch to primary node**.<br><br>4. In the pop\-up dialog box, confirm the operational impact, and click **OK**. |
   


<span id=".55u45YWzLWFwaQ=="></span>
## Relevant APIs


|API |Description |
|---|---|
|[SwitchDBMaster](https://docs.byteplus.com/en/docs/mongodb/switchdbmaster) |Call the SwitchDBMaster API to manually switch the roles of primary and secondary nodes of the specified instance. |
