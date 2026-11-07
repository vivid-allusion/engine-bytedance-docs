---
title: "Logging on to the RDS for MySQL console"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql"
---

This topic describes how to log in to the data interaction platform of RDS for MySQL to connect to an instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have [created an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1) and [created an account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_databases_and_accounts#.5Yib5bu66LSm5Y-3).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* When selecting **Authorize Database Workshop to add service IPs to the corresponding database instance allowlist** during login to the DBW data interaction platform, the IP addresses of the DBW backend service hosts will be added to the allowlist of the database instance. The allowlist name format is `DBW_Sole_***_***_***_RDS` or `byte_rds_***_***_***-`.

* Log out and log in again to restore all pages to their state before logging out.

* After 5 consecutive failed login attempts due to an incorrect username or password, DBW will lock the login for one minute. Try again after one minute.

* Do not modify or delete the allowlist during the login process, as this will prevent opening new command windows to execute commands, although the current window can continue to execute commands.

* Instances with security control enabled support password\-free login on the data interaction platform. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql).

* Logging onto the DBW database interaction platform is temporarily not supported for instances with SSL encryption enabled.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Instances without SSL encryption enabled can successfully log on to the DBW data interaction platform.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the instance that successfully logs in to the Data interaction platform function of DBW, when the SSL encryption service is enabled, the DBW connection will be disconnected and cannot be logged in again because the instance will restart by default after the SSL encryption service is enabled.   </div>
   


<span id=".6YCa6L-HLWRidy3mjqfliLblj7DnmbvlvZUtc3FsLeeql-WPow=="></span>
## Procedure


<Tabs>
<Tab zoneid="PM1wxIjlG8" title="At the DBW console entry">
<TabTitle>At the DBW console entry</TabTitle>

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. Select one of the following methods to log in to the **SQL Window** as needed:

   * Method 1: On the left navigation bar, select **Data management** \> **SQL window**.

   * Method 2;

      1. On the **Instance list** page, locate the target instance.

      2. In the **Actions** column of the target instance, click **Login**.

4. In the **Database Workshop** dialog box, set the relevant parameters as shown in the table below.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Instance type** |Select **RDS for MySQL** from the drop\-down list. |
   |**Instance name** |From the drop\-down list, select a target instance from **Recently logged in** or **All**. Fuzzy search is supported. |
   |**Database node** |Select the node you want to log in to from the drop\-down list as needed. The primary node of the instance is logged in by default. |
   |**Database account** |Enter the database account name. |
   |**Database password** |Enter the database account password. |
   

5. Check **Remember password**, **Authorize Database Workshop to add service IPs to the corresponding database instance allowlist**, and then click **Login**.

   If you select Remember password, you do not need to enter the password for subsequent logins, which helps you improve work efficiency. You can also choose not to remember the password.


</Tab>
<Tab zoneid="gXttA0tIRR" title="At the RDS for MySQL console entry">
<TabTitle>At the RDS for MySQL console entry</TabTitle>

1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the region where the instance belongs.

3. On the **Instance list** page, click **Login** in the **Actions** column of the target instance.

4. In the **Database Workshop** dialog box, set the relevant parameters as shown in the table below.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Instance type** |Select **RDS for MySQL** from the drop\-down list. |
   |**Instance name** |From the drop\-down list, select a target instance from **Recently logged in** or **All**. Fuzzy search is supported. |
   |**Database node** |Select the node you want to log in to from the drop\-down list as needed. The primary node of the instance is logged in by default. |
   |**Database account** |Enter the database account name. |
   |**Database password** |Enter the database account password. |
   

5. Check **Remember password**, **Authorize Database Workshop to add service IPs to the corresponding database instance allowlist**, and then click **Login**.

   After remembering the password, you won’t need to enter it for subsequent logins, helping to improve work efficiency. When you need to clear a remembered password, you can click **Clear record** for the target account in the **Database account** drop\-down list, which will forget the account password.


</Tab>
</Tabs>


<span id="0ILU4Ii4"></span>
## Next steps

After logging in, you can perform the following operations in the command window:


* Visually create tables, triggers, functions, views, and stored procedures.

* Execute statement commands. For more information, refer to [Command operations](https://docs.byteplus.com/en/docs/DBW/executing-commands-for-mysql).

* Click **Observation and diagnosis** to perform operation and maintenance management on the instance. For more information, refer to [Observation and diagnosis](https://docs.byteplus.com/en/docs/DBW/observation-diagnosis-for-mysql).

* Click **Instance details** to view the details of the instance. For more information, refer to [Viewing instance information](https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_instance_details).

* Click **Log out** to exit the instance workbench.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[DataConnectInstance](https://docs.byteplus.com/en/docs/DBW/dataconnectinstance) |Call the DataConnectInstance API to connect to the instance. |
