---
title: "Logging on to the data interaction platform (veDB for MySQL)"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql"
---

This topic describes how to log in to the data interaction platform for NDB for MySQL.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have [created an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1) and [created an account](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_database_and_account#.5Yib5bu66LSm5Y-3).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* When you select **Authorize Database Workshop to add service IPs to the corresponding database instance allowlist**, the IP address of the DBW backend service host will be added to the allowlist of the database instance. The allowlist name format is `dbw_unique_***_***` or `byte_ndb_***_***_dbw_`.

* Log out and log in again to restore all pages to their state before logging out.

* After 5 consecutive failed login attempts due to an incorrect username or password, DBW will lock the login for one minute. Try again after one minute.

* Instances with security control enabled support password\-free login on the data interaction platform. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control).

* Do not modify or delete the allowlist during the login process, as this will prevent opening new command windows to execute commands, although the current window can continue to execute commands.


<span id=".6YCa6L-HLWRidy3mjqfliLblj7DnmbvlvZUtc3FsLeeql-WPow=="></span>
## Procedure


<Tabs>
<Tab zoneid="Pf8gL8lXfD" title="Log on to the SQL window through the DBW console">
<TabTitle>Log on to the SQL window through the DBW console</TabTitle>

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. Choose one of the following methods to log on to the **Database interaction platform**:

   * Method 1: On the left navigation bar, select **Data management** \> **SQL window**.

   * Method 2;

      1. On the **Instance list** page, locate the target instance.

      2. In the **Actions** column of the target instance, click **Login**.

4. In the **Database Workshop** dialog box, set the relevant parameters as shown in the table below.



|**Parameter** |**Description** |
|---|---|
|**Instance type** |From the drop\-down list, **select** **NDB** for **MySQL**. |
|**Instance name** |From the drop\-down list, select a target instance from **Recently logged in** or **All**. Fuzzy search is supported. |
|**Database account** |Enter the database account name. |
|**Database password** |Enter the database account password. |



5. Check **Remember password**, **Authorize Database Workshop to add service IPs to the corresponding database instance allowlist**, and then click **Login**.

   After remembering the password, you won’t need to enter it for subsequent logins, helping to improve work efficiency. When you need to clear a remembered password, you can click **Clear record** for the target account in the **Database account** drop\-down list, which will forget the account password.


</Tab>
<Tab zoneid="eMag757RBk" title="Log on to the SQL window through the veDB for MySQL console.">
<TabTitle>Log on to the SQL window through the veDB for MySQL console.</TabTitle>

1. Log on to the [veDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the region where the instance belongs.

3. On the **Instance list** page, click  **...**  in the **Actions** column of the target instance.  **\> Log in**.

4. In the **Database Workshop** dialog box, set the relevant parameters as shown in the table below.



|**Parameter** |**Description** |
|---|---|
|**Instance type** |From the drop\-down list, **select** **NDB** for **MySQL**. |
|**Instance name** |From the drop\-down list, select a target instance from **Recently logged in** or **All**. Fuzzy search is supported. |
|**Database account** |Enter the database account name. |
|**Database password** |Enter the database account password. |



5. Check **Remember password**, **Authorize Database Workshop to add service IPs to the corresponding database instance allowlist**, and then click **Login**.

   After remembering the password, you won’t need to enter it for subsequent logins, helping to improve work efficiency. To clear a remembered password, click **Clear record** for the target account in the **Database account** drop\-down list, and the account password will be forgotten.


</Tab>
</Tabs>


<span id=".5ZCO57ut5pON5L2c"></span>
## Next steps

After logging in, you can perform the following operations in the command window:


* Visually create tables, triggers, functions, views, and stored procedures.

* Execute statement commands. For more information, refer to [Command operations](https://docs.byteplus.com/en/docs/DBW/Command_operations).

* Click **Observation and diagnosis** to perform operation and maintenance management on the instance. For more information, refer to [Observation and diagnosis](https://docs.byteplus.com/en/docs/DBW/Observation_and_diagnosis).

* Click **Instance details** to view the details of the instance. For more information, refer to [Viewing instance information](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Viewing_instance_details).

* Click **Log out** to exit the instance workbench.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[DataConnectInstance](https://docs.byteplus.com/en/docs/DBW/dataconnectinstance) |Call the DataConnectInstance API to connect to the instance. |
