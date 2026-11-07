---
title: "Connecting to MongoDB via DBW"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/connect-mongodb-through-dbw"
---

Database Workshop (DBW) is a unified cloud management platform for managing the lifecycle of multiple types of databases. You can use DBW to quickly remotely connect to and manage MongoDB databases online. This topic describes how to connect to MongoDB instance via DBW.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

DBW is a database SaaS product that integrates database graphical user interface (GUI), fault troubleshooting, and auditing. It provides web\-terminal management capabilities such as comprehensive observation and analysis, intelligent risk checking, and autonomous operation and maintenance, offering you stable, safe, and efficient database management cloud services. For more details, refer to [What is Database Workshop](https://docs.byteplus.com/en/docs/DBW/what-is-database-workbench).

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite


* MongoDB instance has been created. For specific procedures, refer to [Creating instance](https://docs.byteplus.com/en/docs/mongodb/creating_an_instance).

* The database login account and password have been set for MongoDB instance. For specific procedures, refer to [Creating account](https://docs.byteplus.com/en/docs/mongodb/create-account).

* The instance status must be **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* When you select **Authorize Database Workshop to add service IPs to the corresponding database instance allowlist**, the IP address of the DBW backend service host will be added to the allowlist of the database instance. The name format of this allowlist is `DBW_Sole_***_***_***_Mongo`.

* During the process of connecting to MongoDB using DBW, do not modify, disassociate, or delete the above allowlist; otherwise, you will not be able to open a new command window to execute commands, but the current window can still continue to execute command operations.

* Logging in to MongoDB instances with SSL encryption enabled via DBW is not supported. If you want to log in, please first disable the SSL encryption service of the instance. For specific procedures, refer to [Setting SSL encryption](https://docs.byteplus.com/en/docs/mongodb/setup-ssl).

   If you successfully connect to MongoDB instance through DBW and then enable the SSL encryption service for the instance, the original connection will not be disconnected and you can still continue to execute other commands, but you cannot open a new command window.


<span id=".6YCa6L-HLW1vbmdvZGIt5o6n5Yi25Y-w55m75b2VLWRidw=="></span>
## Log on to DBW via MongoDB console


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, locate the target instance, and click **Login DBW** in the **Actions** column on the right.

5. In the pop\-up dialog box, set the following instance connection parameters.

   
   |Parameter |Description |
   |---|---|
   |Instance type |**Document Database for MongoDB** is selected by default. No modification is required. |
   |Instance name |The target MongoDB instance from step 4 is selected by default.<br><br>To log in to a different MongoDB instance, select the corresponding MongoDB instance from the drop\-down list. |
   |Node ID |From the drop\-down list, select the target node ID.<br><br>MongoDB instance architectures vary, and the target nodes that can be selected also vary. Among them:<br><br><br>* **MongoDB replica set instance**<br><br>   You can specify the node type to connect to from the dropdown list, including the primary node and secondary node of the replica set instance.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you choose to connect to the instance using secondary node, since this node does not accept read requests by default, you must execute <code>rs.slaveOK()</code> on it beforehand to view databases, collections, and indexes. However, add, delete, or modify operations are not supported.   </div><br>   <br><br>* **MongoDB sharding cluster instance**<br><br>   You can specify the Mongos node to connect to from the dropdown list. |
   |Database account |Enter the database account. Currently, only the `root` account is supported for connecting to instances. |
   |Database password |Enter the password corresponding to the database account. If you forget the password, you can modify it through the MongoDB console. For specific procedures, refer to [Resetting password](https://docs.byteplus.com/en/docs/mongodb/reset-password). |
   

6. Select **Authorize Database Workshop to add service IPs to the corresponding database instance allowlist**, and click **Log in**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also check <strong>Remember password</strong> at the same time. After checking, you don't need to enter the password when logging in to this MongoDB instance with the same account in the future.   </div>
   

<span id=".6YCa6L-HLWRidy3mjqfliLblj7Dov57mjqUtbW9uZ29kYi3lrp7kvos="></span>
## Connecting to MongoDB via DBW console


1. Log in to the [DBW console](https://console.byteplus.com/dbw).

2. In the top menu bar, select the project and region to which the target MongoDB instance belongs.

3. In the left navigation pane, select **Data Management \> SQL Window**.

4. In the pop\-up dialog box, set the following instance connection parameters.

   
   |Parameter |Description |
   |---|---|
   |Instance type |From the drop\-down list, select **Document Database for MongoDB**. |
   |Instance name |Select the target MongoDB instance from the dropdown list. |
   |Node ID |From the drop\-down list, select the target node ID. MongoDB instance architectures vary, and the target nodes that can be selected also vary. Among them:<br><br><br>* **MongoDB replica set instance**<br><br>   You can specify the node type to connect to from the dropdown list, including the primary node and secondary node of the replica set instance.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you choose to connect to the instance using secondary node, since this node does not accept read requests by default, you must execute <code>rs.slaveOK()</code> on it beforehand to view databases, collections, and indexes. However, add, delete, or modify operations are not supported.   </div><br>   <br><br>* **MongoDB sharding cluster instance**<br><br>   You can specify the Mongos node to connect to from the dropdown list. |
   |Database account |Enter the database account. Currently, only the `root` account is supported for connecting to instances. |
   |Database password |Enter the password corresponding to the database account. If you forget the password, you can modify it through the MongoDB console. For specific procedures, refer to [Resetting password](https://docs.byteplus.com/en/docs/mongodb/reset-password). |
   

5. Select **Authorize Database Workshop to add service IPs to the corresponding database instance allowlist**, and click **Log in**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also check <strong>Remember password</strong> at the same time. After checking, you don't need to enter the password when logging in to this MongoDB instance with the same account in the future.   </div>
   

<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

After successfully connecting to a MongoDB instance via DBW, you can execute various command statements in the DBW SQL window. Meanwhile, you can also visually manage databases, collections, and indexes (such as create, query, delete). For specific procedures, refer to:


* [Executing commands](https://docs.byteplus.com/en/docs/DBW/executing-commands-for-mongodb)

* [Database management](https://docs.byteplus.com/en/docs/DBW/database-management-for-mongodb)

* [Collection management](https://docs.byteplus.com/en/docs/DBW/collection-management-for-mongodb)

* [Index management](https://docs.byteplus.com/en/docs/DBW/index-management-for-mongodb)
