---
title: "Logging on to the data interaction platform (RDS for SQL Server)"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-rds-for-sql-server"
---

This topic describes how to connect to an instance via logging on to the data interaction platform for RDS for SQL Server to on the Database Workshop (DBW) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance has been created and the instance state is Running. For detailed steps, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide).

* A database account has been created. For detailed steps, refer to [Creating and managing an account](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-and-managing-account).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Instances with security control enabled support password\-free login on the data interaction platform. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/enabling-security-control_).

* When you select **Authorize Database Workshop to add service IPs to the corresponding database instance allowlist**, the IP address of the DBW backend service host will be added to the allowlist of the database instance. The name of the allowlist is in the `DBW_Sole_****_****_For_mssql` format.

* Log out and log in again to restore all pages to their state before logging out.

* After 5 consecutive failed login attempts due to an incorrect username or password, DBW will lock the login for one minute. Try again after one minute.

* Do not modify or delete the allowlist during the login process, as this will prevent opening new command windows to execute commands, although the current window can continue to execute commands.

* It supports logging into both the primary instance and read\-only instances.


<span id=".6YCa6L-HLWRidy3mjqfliLblj7DnmbvlvZUtc3FsLeeql-WPow=="></span>
## Procedure


<Tabs>
<Tab zoneid="WfqX36CJ4z" title="Log on to the SQL window through the DBW console">
<TabTitle>Log on to the SQL window through the DBW console</TabTitle>

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. Choose one of the following methods to log on to the **Database interaction platform**:

   * Method 1: On the left navigation bar, select **Data management** \> **SQL window**.

   * Method 2;

      1. On the left navigation bar, click **Instance list**.

      2. In the upper\-left corner of the **Instance list** page, set the database type to ** RDS for SQL Server** and find the target instance.

      3. In the **Actions** column of the target instance, click **Login**.

4. In the **Database Workshop** dialog box, set the relevant parameters as shown in the table below.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Instance type** |From the drop\-down list, select **RDS for SQL Server**. |
   |**Instance name** |From the drop\-down list, select a target instance from **Recently logged in** or **All**. Fuzzy search is supported. |
   |**Database account** |Enter the database account name. |
   |**Database password** |Enter the database account password. |
   |**Database name** |Optional. Enter the database name as needed. The `master` database is used by default. |
   

5. Check **Remember password**, **Authorize Database Workshop to add service IPs to the corresponding database instance allowlist**, and then click **Login**.

   After remembering the password, you won’t need to enter it for subsequent logins, helping to improve work efficiency. When you need to clear a remembered password, you can click **Clear record** for the target account in the **Database account** drop\-down list, which will forget the account password.


</Tab>
<Tab zoneid="MzjooqKsdr" title="Log on to the SQL window through the RDS for SQL Server console">
<TabTitle>Log on to the SQL window through the RDS for SQL Server console</TabTitle>

1. Log on to the [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper\-left corner of the top menu bar, select the region where the instance belongs.

3. On the **Instance list** page, click **Login** in the **Actions** column of the target instance.

4. In the **Database Workshop** dialog box, set the relevant parameters as shown in the table below.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Instance type** |From the drop\-down list, select **RDS for SQL Server**. |
   |**Instance name** |From the drop\-down list, select a target instance from **Recently logged in** or **All**. Fuzzy search is supported. |
   |**Database account** |Enter the database account name. |
   |**Database password** |Enter the database account password. |
   |**Database name** |Optional. Enter the database name as needed. The `master` database is used by default. |
   

5. Check **Remember password**, **Authorize Database Workshop to add service IPs to the corresponding database instance allowlist**, and then click **Login**.

   After remembering the password, you won’t need to enter it for subsequent logins, helping to improve work efficiency. When you need to clear a remembered password, you can click **Clear record** for the target account in the **Database account** drop\-down list, which will forget the account password.


</Tab>
</Tabs>


<span id=".5ZCO57ut5pON5L2c"></span>
## Next steps

After logging in, you can perform the following operations in the command window:


* Execute statement commands. For more information, refer to [Command operations](https://docs.byteplus.com/en/docs/DBW/command-opeartions_).

* Click **Observation and diagnosis** to perform operation and maintenance management on the instance. For more information, refer to [Observation and diagnosis](https://docs.byteplus.com/en/docs/DBW/Operation_and_maintenance_management_).

* Click **Instance details** to view the details of the instance. For more information, refer to [Viewing instance information](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/viewing-instance-details).

* Click **Log out** to exit the instance workbench.
