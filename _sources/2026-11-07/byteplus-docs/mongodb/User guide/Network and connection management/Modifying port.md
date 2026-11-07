---
title: "Modifying port"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/modifying_ports"
---

The Document Database for MongoDB supports modifying the port number of the connection address of replica set instances and Mongos nodes in the sharding cluster instances. This topic describes how to modify the port number of the connection address.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite

The instance status must be **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

Currently, only the port number of the connection address of **replica set instances** and the **Mongos** nodes in sharding cluster instances can be modified. The port numbers of Shard or ConfigServer nodes in sharding cluster instances cannot be modified. For more information on the connection addresses supported by each instance or component type, refer to [Connection addresses supported by different instances](https://docs.byteplus.com/en/docs/mongodb/addresses-introduction#.5LiN5ZCM5a6e5L6L5pSv5oyB55qE6L-e5o6l5Zyw5Z2A).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Modifying the port number will cause access to some services to be affected in a short time. Please operate with caution.

* After modifying the port number, the original connection will be disconnected. Please modify the connection information of the client in a timely manner. For specific procedures, refer to [Connecting to instance via Mongo shell](https://docs.byteplus.com/en/docs/mongodb/connect-instance-via-mongo-shell).

* The effective scopes of new ports vary depending on the instance or component type. The specific effective scopes are shown in the following table. The specific effective scopes are shown in the following table.

   
   |Instance or component type |Effective scope of new ports |
   |---|---|
   |Replica set instance |* After the port number is modified, it will take effect on the private network address ports of all existing primary, secondary, hidden, and read\-only nodes on the instance.<br><br>* At the same time, it will also take effect on the public network address ports of all existing primary, secondary, and read\-only nodes on the instance.<br><br>* After the port number is modified, when a new read\-only node is added to the instance, the port of the new read\-only node will also inherit the modified port number. For more information about read\-only nodes, refer to [Managing read-only nodes](https://docs.byteplus.com/en/docs/mongodb/managing_read_only_nodes). |
   |Mongos node in sharding cluster instance |* After the port number is modified, it will take effect on the public and private network address ports of all existing Mongos nodes on this instance.<br><br>* After modifying the port number, when a new Mongos node is added to the instance, the port of the newly added Mongos node will also inherit the modified port number. |
   


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click on the **Connectivity** tab.

6. In the **Network information** area under the **Connectivity** tab, after **Database port** click <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png) </span> icon.

7. In the pop\-up dialog box, enter a new port number. The modifiable range of port numbers is 1000 to 65535.

   <div data-tips="true" data-tips-type="danger" data-tips-is-title="true" data-wrapper-indent="1">danger   </div>
   

   * <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1">Modifying the port number will cause access to some services to be affected in a short time. Please operate with caution.   </div>
   

   * <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1">After modifying the port number, the original connection will be disconnected. Please modify the connection information of the client in a timely manner. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/connect-instance-via-mongo-shell">Connecting to instance via Mongo shell</a>.   </div>
   

8. Click **OK**.


<span id=".55u45YWzLWFwaQ=="></span>
## Relevant APIs


|API |Description |
|---|---|
|[ModifyDBEndpointPort](https://docs.byteplus.com/en/docs/mongodb/modifydbendpointport) |Call the ModifyDBEndpointPort interface to modify port number of connection address corresponding to target MongoDB instance. |
