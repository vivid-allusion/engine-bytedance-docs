---
title: "Modifying connection address"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/modify-connection-address"
---

Document Database for MongoDB supports modifying the domain name prefix of the connection address in replica set instances and Mongos nodes of sharding cluster instances. You can modify the connection address of the new instance to that of the original instance, eliminating the need to modify the code of the client connection address. This topic describes how to modify the domain name prefix of the connection address.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite

The instance status must be **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

Currently, only the private network or public network connection address domain names of the **replica set instances** and the **Mongos** node in sharding cluster instances and can be modified, but the connection address domain names of Shard or ConfigServer nodes in sharding cluster instances cannot be modified. For more information about the connection addresses supported by each instance or component type, refer to [Address types supported by different instance types](https://docs.byteplus.com/en/docs/mongodb/addresses-introduction#.5LiN5ZCM5a6e5L6L5pSv5oyB55qE6L-e5o6l5Zyw5Z2A).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Modifying the domain name of the connection address may cause access to some services to be affected within a short period of time. Please operate with caution.

* After modifying the domain name of the connection address, the original connection will be disconnected. Please modify the connection information of the client in time. For specific procedures, refer to [Connecting to instance via Mongo shell](https://docs.byteplus.com/en/docs/mongodb/connect-instance-via-mongo-shell).

* If you need to modify the domain name prefix of the public network address, you need to apply for a public network address for the replica set instances or Mongos nodes of sharding cluster instances first. For specific procedures, refer to [Applying for public address](https://docs.byteplus.com/en/docs/mongodb/ug-apply-public-address).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click on the **Connectivity** tab.

6. On the **Connectivity** tab, perform the corresponding operations according to the instance or node type and the connection address type.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Currently, you can only modify the prefix of the connection address, specifically the part before <code>.mongodb.ibytepluses.com</code> or <code>.mongodb.bytepluses.com</code>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The new domain name needs to meet the following requirements simultaneously:   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The length of the connection address prefix must be 8~63 characters.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The connection address prefix should start with a lowercase letter and end with a lowercase letter or a number.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The connection address prefix can contain lowercase letters, numbers, and hyphens (\-).   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The modified connection address needs to be globally unique and cannot have the same name as any connection address in any region of BytePlus.   </div>
   

   
   <Tabs>
   <Tab zoneid="WfjJliYnzG" title="Replica set instance">
   <TabTitle>Replica set instance</TabTitle>
   
   
   |**Connection address type** |**Specific procedure** |
   |---|---|
   |Private network address |1. In the **Private network access** area under the **Connectivity** tab, on the right of the **Private network address**, click the<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png) </span>icon.<br><br>2. In the **Modify connection address** pop\-up window, first select the node whose connection address domain name needs to be modified from the **Node** drop\-down list, and then enter the new connection address domain name prefix in the **New connection address** text box.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can modify the domain prefix of the private network connection addresses of the primary nodes, secondary nodes, hidden nodes, and read\-only nodes of a replica set instance.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Only when the read\-only nodes are added to the instance will the read\-only node option be displayed in the <strong>Node</strong> drop\-down list. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/add-or-remove-read-only-node#.5re75Yqg5Y-q6K-76IqC54K5">Adding read\-only nodes</a>.</div><br> |
   |Public network address |You can modify the public network connection address domain prefix of the primary, secondary, or read\-only node of a replica set instance. The specific procedure is as follows:<br><br><br>* Modify the public network connection address of primary and secondary nodes<br><br>   1. In the **Public network access** area under the **Connectivity** tab, on the right of the **Public network address for primary and secondary nodes**, click <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png) </span> icon.<br><br>   2. In the **Modify connection address** pop\-up window, first select the node whose connection address domain name needs to be modified from the **Node** drop\-down list, and then enter the new connection address domain name prefix in the **New connection address** text box.Secondary node<br><br>* Modify the public network connection address of the read\-only node<br><br>   1. In the **Public network access** area under the **Connectivity** tab, locate the target read\-only node in the single\-node address table, and click the<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png) </span>icon.<br><br>   2. In the **Modify connection address** pop\-up window, first confirm the read\-node information, and then enter the new connection address domain name prefix in the **New connection address** text box.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You need to apply for a public network address for the replica set instance before you can view and modify the public network address domain name. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/ug-apply-public-address">Applying for public address</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Only when there are read\-only nodes in the instance will the connection address information of the read\-only nodes be displayed. For more information about read\-only nodes, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/managing_read_only_nodes">Managing read\-only nodes</a>.</div><br> |
   
   
   
   
   
   </Tab>
   <Tab zoneid="fld3T5lxPM" title="Mongos nodes of sharding cluster instance">
   <TabTitle>Mongos nodes of sharding cluster instance</TabTitle>
   
   
   |**Connection address type** |**Specific procedure** |
   |---|---|
   |Private network address |1. In the **Connect to Mongos** area under the **Connectivity** tab, on the right of the **Private network address**, click <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png) </span> icon.<br><br>2. In the **Modify connection address** pop\-up window, first select the node whose connection address domain name needs to be modified from the **Node** drop\-down list, and then enter the new connection address domain name prefix in the **New connection address** text box.Secondary node<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Only the connection address domain name of the Mongos node in the sharding cluster can be modified. Modifying the connection address domain names of Shard or ConfigServer nodes is not supported.</div><br> |
   |Public network address |1. In the **Connect to Mongos** area under the **Connectivity** tab, on the right of the **Public network address**, click <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png) </span> icon.<br><br>2. In the **Modify connection address** pop\-up window, first select the node whose connection address domain name needs to be modified from the **Node** drop\-down list, and then enter the new connection address domain name prefix in the **New connection address** text box.Secondary node<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You need to apply for a public network connection address for the Mongos node before you can view and modify the public network connection address domain name. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/ug-apply-public-address">Applying for public address</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Only the connection address domain name of the Mongos node in the sharding cluster can be modified. Modifying the connection address domain names of Shard or ConfigServer nodes is not supported.</div><br> |
   
   
   
   
   
   </Tab>
   </Tabs>
   

7. Click **OK** in the lower right corner of the **Modify connection address** pop\-up window.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Modifying the domain name of the connection address may cause access to some services to be affected within a short period of time. Please operate with caution.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After modifying the domain name of the connection address, the original connection will be disconnected. Please modify the connection information of the client in time. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/connect-instance-via-mongo-shell">Connecting to instance via Mongo shell</a>.   </div>
