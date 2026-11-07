---
title: "Logging on to the data interaction platform (Document Database for MongoDB)"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-documentdb-for-mongodb"
---

This topic describes how to log on to the data interaction platform to connect to a Document Database for MongoDB instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A MongoDB instance has been created. For detailed steps, see [Creating an instance](https://docs.byteplus.com/en/docs/mongodb/creating_an_instance).

* A database account has been created. For detailed steps, refer to [Creating an account](https://docs.byteplus.com/en/docs/mongodb/create-account).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Instances with security control enabled support password\-free login on the data interaction platform. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/MongoDB_Enabling_security_control).

* When you select **Authorize Database Workshop to add service IPs to the corresponding database instance allowlist**, the IP address of the DBW backend service host will be added to the allowlist of the database instance. The name format of the allowlist is `DBW_Sole_*_**_*_Mongo_*`.

* Log out and log in again to restore all pages to their state before logging out.

* After 5 consecutive failed login attempts due to an incorrect username or password, DBW will lock the login for one minute. Try again after one minute.

* Do not modify or delete the allowlist during the login process, as this will prevent opening new command windows to execute commands, although the current window can continue to execute commands.

* Logging onto the DBW database interaction platform is temporarily not supported for instances with SSL encryption enabled.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Instances without SSL encryption enabled can successfully log on to the DBW data interaction platform.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If an instance that has successfully logged on to the DBW data interaction platform enables the SSL encryption service, the original connection will not be disconnected and other commands can still be executed, but new windows can no longer be opened.   </div>
   


<span id=".6YCa6L-HLWRidy3mjqfliLblj7DnmbvlvZUtc3FsLeeql-WPow=="></span>
## Procedure


<Tabs>
<Tab zoneid="WsSOoFeOq7" title="Log on to the SQL window through the DBW console">
<TabTitle>Log on to the SQL window through the DBW console</TabTitle>

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, select **Data management** \> **SQL window**.

3. On the top menu bar, select the region.

4. In the **Database Workshop** dialog box, set the relevant parameters as shown in the table below.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Instance type** |From the drop\-down list, select **Document Database for MongoDB**. |
   |**Instance name** |From the drop\-down list, select a target instance from **Recently logged in** or **All**. Fuzzy search is supported. |
   |**Node ID** |From the drop\-down list, select the target node ID. |
   |**Database account** |Enter the database account. Only the `root` account is supported currently. |
   |**Database password** |Enter the database account password. |
   |**Database name** |The `admin` database is connected by default. You can also enter other database names to connect to as needed. |
   

5. Check **Remember password**, **Authorize Database Workshop to add service IPs to the corresponding database instance allowlist**, and then click **Login**.

   After remembering the password, you won’t need to enter it for subsequent logins, helping to improve work efficiency. When you need to clear a remembered password, you can click **Clear record** for the target account in the **Database account** drop\-down list, which will forget the account password.


</Tab>
<Tab zoneid="E7dlXuiBdl" title="Log on to the SQL window through the Document Database for MongoDB console">
<TabTitle>Log on to the SQL window through the Document Database for MongoDB console</TabTitle>

1. Log on to the [Document Database for MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click **Login** in the **Actions** column of the target instance.

5. In the **Database Workshop** dialog box, set the relevant parameters as shown in the table below.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Instance type** |From the drop\-down list, select **Document Database for MongoDB**. |
   |**Instance name** |From the drop\-down list, select a target instance from **Recently logged in** or **All**. Fuzzy search is supported. |
   |**Node ID** |From the drop\-down list, select the target node ID. |
   |**Database account** |Enter the database account. Only the `root` account is supported currently. |
   |**Database password** |Enter the database account password. |
   |**Database name** |The `admin` database is connected by default. You can also enter other database names to connect to as needed. |
   

6. Check **Remember password**, **Authorize Database Workshop to add service IPs to the corresponding database instance allowlist**, and then click **Login**.

   After remembering the password, you won’t need to enter it for subsequent logins, helping to improve work efficiency. When you need to clear a remembered password, you can click **Clear record** for the target account in the **Database account** drop\-down list, which will forget the account password.


</Tab>
</Tabs>


<span id=".5ZCO57ut5pON5L2c"></span>
## Next steps

After logging in, you can perform the following operations in the command window:


* Visually create databases, collections, indexes, etc.

* Execute statement commands. For more information, refer to [Command operations](https://docs.byteplus.com/en/docs/DBW/executing-commands-for-mongodb).

* Click **Observation and diagnosis** to perform operation and maintenance management on the instance. For more information, refer to [Observation and diagnosis](https://docs.byteplus.com/en/docs/DBW/performance-monitoring-management____).

* Click **Instance details** to view the details of the instance. For more information, refer to [Viewing instance information](https://docs.byteplus.com/en/docs/mongodb/view-instance).

* Click **Log out** to exit the instance workbench.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[DataConnectInstance](https://docs.byteplus.com/en/docs/DBW/dataconnectinstance) |Call the DataConnectInstance API to connect to the instance. |
