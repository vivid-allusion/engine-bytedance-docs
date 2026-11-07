---
title: "Logging on to the data interaction platform (RDS for PostgreSQL)"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/log-in-database-interaction-platform-for-PG"
---

This topic describes how to log on to the RDS for PostgreSQL console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have created an instance and account. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/create_instance) and [Creating an account](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_and_managing_an_account).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The instance must be in the Running state.</div>


* <div data-tips="true" data-tips-type="tip">The account you create must have the corresponding permissions for querying and modifying the corresponding database.</div>



<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Instances with security control enabled support password\-free login on the data interaction platform. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/enabling-security-control).

* Log out and log in again to restore all pages to their state before logging out.

* After 5 consecutive failed login attempts due to an incorrect username or password, DBW will lock the login for one minute. Try again after one minute.

* When you select **Authorize Database Workshop to add service IPs to the corresponding database instance allowlist**, the IP address of the DBW backend service host will be added to the allowlist of the database instance.

   To make allowlist management more efficient and convenient, the new version of the allowlist management function for RDS for PostgreSQL was officially launched on April 25, 2024.

   * Upgrade instance allowlist management function: After logging in to the instance on the DBW console, you can view the allowlist bound to the instance on the instance's data security tab. The naming format of the allowlist is `DBW_Sole``_****_****_For_RDS`.

   * Not upgrade instance allowlist management function: After logging in to the instance on the DBW console, since it is the V1 version of the allowlist, you can not view the associated allowlist in the instance's data security. If you need to view or use the allowlist, you need to upgrade the instance's allowlist management function. For detailed steps to upgrade the instance allowlist, refer to [Upgrading an allowlist](https://docs.byteplus.com/en/docs/6438/1182632).

* Do not modify or delete the allowlist during the login process, as this will prevent opening new command windows to execute commands, although the current window can continue to execute commands.


<span id=".6YCa6L-HLWRidy3mjqfliLblj7DnmbvlvZUtc3FsLeeql-WPow=="></span>
## Procedure


<Tabs>
<Tab zoneid="K6Nzm7tcvZ" title="Log on to the SQL window through the DBW console">
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
   |**Instance type** |From the drop\-down list, select **RDS for PostgreSQL**. |
   |**Instance name** |From the drop\-down list, select a target instance from **Recently logged in** or **All**. Fuzzy search is supported. |
   |**Database account** |Enter the database account name. |
   |**Database password** |Enter the database account password. |
   

5. Check **Remember password**, **Authorize Database Workshop to add service IPs to the corresponding database instance allowlist**, and then click **Login**.

   After remembering the password, you won’t need to enter it for subsequent logins, helping to improve work efficiency. When you need to clear a remembered password, you can click **Clear record** for the target account in the **Database account** drop\-down list, which will forget the account password.


</Tab>
<Tab zoneid="w0NZs220jO" title="Log on to the SQL window through the RDS for PostgreSQL console">
<TabTitle>Log on to the SQL window through the RDS for PostgreSQL console</TabTitle>

1. Log on to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as All resources.   </div>
   

3. On the left navigation bar, click **Instance list**.

4. On the **Instance list** page, click **Login** in the **Actions** column of the target instance.

5. In the **Database Workshop** dialog box, set the relevant parameters as shown in the table below.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Instance type** |From the drop\-down list, select **RDS for PostgreSQL**. |
   |**Instance name** |From the drop\-down list, select a target instance from **Recently logged in** or **All**. Fuzzy search is supported. |
   |**Database account** |Enter the database account name. |
   |**Database password** |Enter the database account password. |
   

6. Check **Remember password**, **Authorize Database Workshop to add service IPs to the corresponding database instance allowlist**, and then click **Login**.

   After remembering the password, you won’t need to enter it for subsequent logins, helping to improve work efficiency. When you need to clear a remembered password, you can click **Clear record** for the target account in the **Database account** drop\-down list, which will forget the account password.


</Tab>
</Tabs>


<span id=".5ZCO57ut5pON5L2c"></span>
## Next steps

After logging in, you can perform the following operations in the command window:


* Visually create databases, schemas, tables, etc.

* Execute statement commands. For more information, refer to [Command operations](https://docs.byteplus.com/en/docs/DBW/command-operation-for-PG).

* Click **Observation and diagnosis** to perform operation and maintenance management on the instance. For more information, refer to [Observation and diagnosis](https://docs.byteplus.com/en/docs/DBW/session-management).

* Click **Instance details** to view the details of the instance. For more information, refer to [Viewing instance information](https://docs.byteplus.com/en/docs/RDS_for_PG/viewing_the_details_of_an_instance).

* Click **Log out** to exit the instance workbench.
