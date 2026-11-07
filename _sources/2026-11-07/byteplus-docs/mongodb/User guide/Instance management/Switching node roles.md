---
title: "Switching node roles"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/switching_node_roles"
---

Document Database for MongoDB supports the node role switching feature. You can switch the roles of primary, secondary, and hidden nodes based on business needs to achieve proximity access.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite


* Only the following instance or component types support switching node roles:

   * Replica set instance

   * Shard within sharding cluster instance

   * ConfigServer components within sharding cluster instance

   For more details about instance types, refer to [Product architecture](https://docs.byteplus.com/en/docs/mongodb/about-mongodb#.5Lqn5ZOB5p625p6E).

* The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).


<span id=".6IqC54K56KeS6Imy5YiH5o2i5Zy65pmv"></span>
## Node role switching scenarios

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Document Database for MongoDB supports four types of nodes: primary nodes, secondary nodes, hidden nodes, and read\-only nodes. For more details on different node types, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/managing_read_only_nodes#.5LiN5ZCM57G75Z6L55qE6IqC54K55a-55q-U">Comparison of different types of nodes</a>.</div>


* <div data-tips="true" data-tips-type="tip">Regarding the identification in the table, the instructions are as follows:</div>


   * <div data-tips="true" data-tips-type="tip">✔️ : Indicates that switching from the original node role to the target node role is supported.</div>


   * <div data-tips="true" data-tips-type="tip">❌ : Indicates that switching from the original node role to the target node role is not supported.</div>




|Original node or target node role |Primary node |Secondary node |Hidden node |Read\-only node |
|---|---|---|---|---|
|Primary node |Not involved |✔️ |✔️ |❌ |
|Secondary node |✔️ |Not involved |✔️ |❌ |
|Hidden node |✔️ |✔️ |Not involved |❌ |
|Read\-only node |❌ |❌ |❌ |Not involved |


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* During the process of manually switching the node role (generally taking 30 to 60 seconds), the instance may experience 1 to 2 transient connection drops. Proceed with caution.

* If public access is enabled for instance, the public connection address may be temporarily unavailable or disconnected during the switchover. It is strongly recommended to avoid performing read/write operations via the public connection address during the switchover.

* It is recommended to perform switching operations during off\-peak hours and ensure that the application has an automatic reconnect mechanism.

* A node role switchover only changes the role of the node; it does not alter the node's availability zone or node ID.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the name of the target instance.

5. In the **Node information** area under the **Summary** tab, complete the corresponding switching operation based on the instance or component type.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When switching node roles, the node's <strong>Original role</strong> and <strong>Target role</strong> must be different.   </div>
   

   
   |Instance or component type ||Procedure |
   |---|---|---|
   |Replica set instance ||1. In the **Node information** area, click **Role switching**.<br><br>2. In the pop\-up panel, select the corresponding node from the **Original role** and **Target role** drop\-down lists respectively.<br><br>3. Click **OK** in the lower right corner of the page. |
   |Sharding cluster instance |Shard |1. In the **Node information** area, click the **Shards** tab.<br><br>2. Under the **Shards** tab, click **Role switching**.<br><br>3. In the pop\-up panel, first select the target shard from the **Select shard** drop\-down list, then select the corresponding node from the **Original role** and **Target role** drop\-down lists respectively.<br><br>4. Click **OK** in the lower right corner of the page. |
   ||ConfigServer |1. In the **Node information** area, click the **ConfigServers** tab.<br><br>2. On the **ConfigServers** tab, click **Role switching**.<br><br>3. In the pop\-up panel, select the corresponding node from the **Original role** and **Target role** drop\-down lists respectively.<br><br>4. Click **OK** in the lower right corner of the page. |
