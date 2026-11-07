---
title: "Create and manage accounts"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-and-managing-account"
---

This topic describes how to create and delete accounts for RDS for SQL Server instances.

<span id=".6IOM5pmv5L-h5oGv"></span>
## **Description**

RDS SQL Server instance supports account type as follows:


* Super account: Each instance has a super account that is created with the instance and cannot be deleted.

* Normal account: You can create multiple normal accounts for an instance. You also need to manually grant database permissions to normal accounts.

* System admin account: You can create only one database account with system admin (SA) permissions for each instance. This account can be created, disabled, or enabled through the console. RDS for SQL Server instances with a system admin account enabled **are no longer covered by the Service Level Agreement (SLA)** , **but after\-sales service is not affected**. RDS for SQL Server instances without a System Admin account are still fully covered by the SLA.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The System Admin account feature is available on an allowlist basis. To request access, <a href="https://console.byteplus.com/workorder/create">Submit a ticket</a> to contact the SQL Server technical team.   </div>
   

   For detailed information about account types and permissions, see [Account permissions](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/account-permissions-description).

<span id="LlGhCKTy"></span>
## **Prerequisites**

An instance has been created and the instance state is **Running**. For detailed operations, see [Create an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide).

<span id=".5Yib5bu66LSm5Y-3"></span>
## **Create an account**


1. Log on to the [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper\-left corner of the top menu bar, select the project and region where the instance is located.

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click the **Account management** tab.

5. On the **Account management** tab, configure the following parameters:

   
   |**Parameter** |**Description** |
   |---|---|
   |**Account types** |Support selecting **Normal account** or **System Admin account**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This feature is available on an allowlist basis. To use it, <a href="https://console.byteplus.com/workorder/create?step=1">Submit a ticket</a> to contact the SQL Server technical team.</div><br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">You can create only one database account with System Admin permissions for each instance. After the account is created, you can delete it through the console. Instances are no longer covered by the Service Level Agreement (SLA) after a System Admin  account is created.</div><br> |
   |**Database account** |Enter a custom name for the database account, which must follow the rules below:<br><br><br>* The database account must be globally unique.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* Consists of letters, numbers, and underscores (_), and is case\-insensitive.<br><br>* The length must be between 2 and 128 characters.<br><br>* Do not use reserved words such as `rdsadmin`、`veyun_user`、`rdsbackup`、`rdsmirror`、`dbm_login` |
   |**Password** |Set the password for the database account. The password rules are as follows:<br><br><br>* The length must be between 8 and 32 characters.<br><br>* Contain at least three of the following: uppercase letters, lowercase letters, numbers, or special characters.<br><br>* Special characters include `~!@#$%^&*()-_+=?`. |
   |**Confirm password** |Enter the password again. |
   |**Login SID** |(Optional) Specify the Login SID for the account. To associate database permissions for migrating an on\-premises database to the cloud, this SID must be consistent with the Login SID of the local instance account. The rules for the Login SID are as follows:<br><br><br>* Starts with 0x or 0X and must be unique.<br><br>* The length must be 34 characters.<br><br>* Must contain numbers and uppercase and lowercase letters from A to F.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">For instructions on migrating on\-premises data to BytePlus RDS for SQL Server, refer to <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/upload-full-backup-data-of-local-database-to-rds-for-sql-server-instance-through-tos">Uploading a full backup of a local database to an RDS for SQL Server instance via TOS</a> and <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/upload-incremental-backup-data-of-the-local-database-to-rds-for-sql-server-instance-through-tos">Uploading an incremental backup of a local database to an RDS for SQL Server instance via TOS</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can run the following command on your local instance to get the Login SID of a local account:</div><br><br><br>   <div data-tips="true" data-tips-type="tip">   ```sql```<br>```   SELECT name, sid```<br>```   FROM sys.server_principals```<br>```   WHERE name = 'Loginname' and type = 'S';```<br>```   ```<br>      </div><br>    |
   |**Authorize database** |* If you create a **Normal account:**  you must manually authorize a database for the account and select its permissions: **Owner**, **Read Only**, **Read/Write**. This parameter is optional. You can also modify the databases authorized for the account after creation.<br><br>* If you create a **System Admin** account, manual authorization is not required, as this account type has all permissions for all databases.System admin account<br><br><br> |
   

6. Click **OK**.


<span id=".5Yig6Zmk6LSm5Y-3"></span>
## **Delete account**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Only Normal accounts can be deleted. A deleted account cannot be restored and may interrupt connections that use it. Proceed with caution.</div>



1. Log on to the [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper\-left corner of the top menu bar, select the project and region where the instance is located.

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click the **Account management** tab.

5. On the **Account management** tab, click **Delete** in the **Actions** column for the target account.

6. In **Confirm deletion?**  dialog box, click **Delete**


<span id="8mFzMSNf"></span>
## **Disable** or **Enable a system admin account**

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The System Admin account feature is available on an allowlist basis. To request access, <a href="https://console.byteplus.com/workorder/create">Submit a ticket</a> to contact the SQL Server technical team.</div>


* <div data-tips="true" data-tips-type="default">Once created, system admin accounts can only be disabled or enabled. They cannot be deleted.</div>


1. Log on to the [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper\-left corner of the top menu bar, select the project and region where the instance is located.

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click the **Account management** tab.

5. On the **Account management** tab, do the following:

   * Disable account: Click **Disable account** in the **Actions** column of the target System Admin account. In the **Disable this account?**  dialog box, click **OK**.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">After an account is successfully disabled, the <strong>Disable account</strong> button changes to an <strong>Enable account</strong> button.      </div>
      

   * Activate account: In the **Actions** column for the target system admin account, click **Enable account**.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [Modify account permissions](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/modifying-account-permissions)

* [Reset account password](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/resetting-account-password)


<span id=".5bi46KeB6Zeu6aKY"></span>
## FAQs

<span id=".6auY5p2D6ZmQ6LSm5Y-35ZKM5pmu6YCa6LSm5Y-355qE5Yy65Yir5piv5LuA5LmI77yf"></span>
#### What is the difference between a super account and a normal account?


* Super account: Each instance has a super account that is created with the instance and cannot be deleted.

* Normal account: You can create multiple normal accounts for an instance. You also need to manually grant database permissions to normal accounts.

   For details about account types and super accounts, see [Account permissions](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/account-permissions-description).


<span id=".5pWw5o2u5bqT5Y-v5Lul57uR5a6a5aSa5Liq6LSm5Y-35ZCX77yf"></span>
#### Can a database be associated with multiple accounts?

Yes.

<span id=".5Li65LuA5LmI5Yig6Zmk6LSm5Y-35pe25pi-56S65aSx6LSl77yf"></span>
#### Why did deleting the account fail?


* The account you are trying to delete may be in use, which could affect related data. Ensure that all associated sessions are closed before deleting the account.

* The account was deleted from the primary instance, but it remains on the read\-only instance because its connections were not cleared from the read\-only node during synchronization.


<span id=".5Zyo57uZ6LSm5Y-35o6I5LqI5pWw5o2u5bqT5pON5L2c5p2D6ZmQ5pe25Ye6546wLW1zc3FsLXZlLXJkcy1lcnJvci11c2VyLXRlc3QtdXNlci1zaWQtbm90LXNhbWUtd2l0aC1sb2dpbi10ZXN0LXVzZXItaW4tZGF0YWJhc2UtdGVzdC1kYi3miqXplJnmgI7kuYjlip7vvJ8="></span>
#### An error occurs when granting database permissions to an account: mssql: ve_rds_error: user [test_user] sid not same with login [test_user] in database [test_db]. What should I do?

**Possible cause**: When granting database permissions to an account, the operation will fail if a user with the same name but a different SID already exists in the database.

**Solution**: you can resolve the issue in the following ways.


* Solution **One**: use the following T\-SQL statement to re\-associate the login account (Login) with the user (User) of the current database.

   ```sql
   use [test_db];
   ALTER USER [test_user] with login = [test_user] ;
   ```
   

* Solution Two: run the following statement to delete the user (User) with the same name in the cloud database, and then re\-associate it in the console.

   ```sql
   use [test_db];
   Drop USER [test_user];
   ```
   

* Solution Three: you can create a login account (Login) with a SID that matches the current database User SID. For detailed instructions, see [Create a login account after migrating to the cloud via TOS](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/upload-full-backup-data-of-local-database-to-rds-for-sql-server-instance-through-tos?lang=en#create-login-account).
