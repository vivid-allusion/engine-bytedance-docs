---
title: "Creating databases and accounts"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_databases_and_accounts"
---

You can create databases and accounts and configure their privileges based on your business needs. This topic describes how to create databases and accounts for a MySQL instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An instance is created and in the **Running** state. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

<span id=".5Yib5bu65pWw5o2u5bqT"></span>
## Create database


&nbsp;

1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.</div>



3. In the left navigation bar, choose **MySQL** \> **Instances**.

4. On the **Instances** page, click the target instance name.

5. On the target instance page, click **Databases**.

6. On the **Databases** tab, click **Create database**, and set the following parameters in the create database panel.



|Parameter |Description |
|---|---|
|Database name |Required. Fill in the database name. Naming rules are as follows:<br><br><br>* The name must be unique.<br><br>* 2 to 64 characters in length.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* It consists of letters, digits, underscores (_), or hyphens (\-).<br><br>* It cannot contain certain reservation words, including root, admin, and prohibited keywords. For all prohibited keywords, refer to the [list of prohibited keywords](https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_forbidden_keywords). |
|Description |Optional. The description of the database. The length does not exceed 256 characters, and can include digits, Chinese, English, underscores (_), and dashes (\-). |
|Character set |Required. Supports selecting `utf8`, `latin1`, `utf8mb4`, or `ascii`. |
|Authorized account |Add a normal account authorized to access the database.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can leave this parameter blank and associate an account after the database is created. For more details, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_account_permissions">Modifying account permissions</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Since Super accounts have all permissions by default, you can only grant permissions to Normal accounts here.</div><br> |
|Account privileges |Required Select the account privilege for the database: **Read/Write**, **Read\-only**, **DDL only**, **DML only**, or **Customize**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The account type is required only when a specific account is selected in <strong>Authorized account</strong>.</div><br> |
|Custom privilege |Required. Customize the privileges for the authorized account in the current database.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can customize account privileges only when you select <strong>Customize</strong> as the <strong>Account type</strong>.</div><br><br><br><br>* `SELECT`<br><br>* `INSERT`<br><br>* `UPDATE`<br><br>* `DELETE`<br><br>* `CREATE`<br><br>* `DROP`<br><br>* `REFERENCES`<br><br>* `INDEX`<br><br>* `ALTER`<br><br>* `CREATE TEMPORARY TABLES`<br><br>* `LOCK TABLES`<br><br>* `EXECUTE`<br><br>* `CREATE VIEW`<br><br>* `SHOW VIEW`<br><br>* `EVENT`<br><br>* `TRIGGER`<br><br>* `CREATE ROUTINE`<br><br>* `ALTER ROUTINE` |



7. Click **OK** to create the database.


&nbsp;

<span id=".5Yib5bu66LSm5Y-3"></span>
## Creating an account

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you created a super account when creating the instance and do not need a normal account, you can skip this step.</div>



1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. On the **Instances** page, click the target instance name.

4. On the target instance page, click **Accounts**.

5. On the **Accounts** tab, click **Create account**. In the displayed **Create account** page, set the following parameters and click **OK** to create the account.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also click <strong>Preview</strong> after completing the settings to view the SQL statements for creating an account with the specified configuration.   </div>
   

   
   |Parameter |Description |
   |---|---|
   |Account type |Required. Select **Super account** or **Normal account**.<br><br><br>* Super account: Can manage all normal accounts and databases.<br><br>* Normal account: You need to manually grant specific database permissions to a normal account.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A MySQL instance supports two types of database accounts: super accounts and normal accounts. After an account is created, its type cannot be changed.</div><br> |
   |Database account |Required Enter the account name. Naming rules are as follows:<br><br><br>* The database account name is globally unique.<br><br>* The account name must be 2 to 32 characters long.<br><br>* The name must start with a letter and ends with a letter or a digit.<br><br>* The name consists of letters, digits, underscores (_), and hyphens (\-).<br><br>* Certain reservation words or prohibited keywords cannot be used. For all disabled keywords and reservation words, refer to the [List of forbidden keywords](https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_forbidden_keywords).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The keywords root and admin can be used in the super account name.</div><br> |
   |Description |Optional. Account description. The length does not exceed 256 characters, and can include digits, Chinese, English, underscores (_), and dashes (\-). |
   |Host IP |Required. Specifies the IP address where the account accesses the database.<br><br><br>* If the host IP is specified as %, allow the account to access the database from any IP address.<br><br>* If the host IP is specified as `192.10.10.%`, the account can access the database from IP addresses between `192.10.10.0` and `192.10.10.255`.<br><br>* The specified host IP needs to be added to the allowlist to which the instance is associated with, otherwise the instance cannot be accessed normally. For information on adding IP addresses to an allowlist, see [Modifying an allowlist](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_an_allowlist).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If the account type created is a super account, the host IP can only be specified as %.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you need to specify the IP address for the account to access the database, you need to enable the database agent service for the instance. For more information, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/enable_database_agent">Enabling the database proxy</a>.</div><br> |
   |Verification method |Required. Specify the verification method for the account, which can be **Password verification** or **IAM verification**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The verification method cannot be modified after the account is created.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Super account does not support the IAM verification method.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If you select <strong>IAM verification</strong>, you do not need to set a password for the account. A temporary token is used for log on verification instead of a password.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The IAM verification feature is currently in a state of invitation\-only testing. To use it, <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000178">submit a ticket</a> to apply.</div><br> |
   |Password |Required. Set the account password. Requirements are as follows:<br><br><br>* The password length is limited to 8~32 characters.<br><br>* It contains at least three of the following: uppercase letters, lowercase letters, digits, and special characters.<br><br>* Special characters are `!@#$%^&*() _ +-=,.&?\|/`.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If you select <strong>IAM verification</strong>, you do not need to set a password for the account.</div><br> |
   |Confirm password |Required. Enter the password again to confirm. |
   |Permission settings |Grant global authorization for the account within the instance scope, authorization for a specified database, or authorization for tables and columns under a specified database.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Only permission setting for normal accounts is supported, and super accounts have all permissions by default.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Only databases that meet <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_a_database#.5pON5L2c5q2l6aqk">the database name naming rules</a> can be deleted through the console.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You cannot revoke your account's <code>PROCESS</code>, <code>REPLICATION SLAVE</code> or <code>REPLICATION CLIENT</code> permissions during account creation.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">In the process of creating an account, except for the global permissions <code>PROCESS</code>, <code>REPLICATION SLAVE</code> and <code>REPLICATION CLIENT</code>, other permissions are optional. After creating an account, you can modify the account permissions according to your business needs. For more information, see <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_account_permissions">Modifying account permissions</a>.</div><br><br><br>* **Global authorization** Set instance\-wide global permissions for the account. The selectable global permissions are shown in the following table, and multiple permissions can be selected. In the **Global authorization** area, check the corresponding permissions.<br><br>   * `PROCESS` Allows viewing information about all currently executing threads and processes.<br><br>   * `REPLICATION SLAVE` Allows replication of data from the primary server.<br><br>   * `REPLICATION CLIENT` Allows viewing and managing the status and parameters of the replication process.<br><br>   * `SELECT` Allows querying data from the specified table.<br><br>   * `INSERT` Allows inserting new data into the table.<br><br>   * `UPDATE` Allows updating data in the specified table.<br><br>   * `DELETE` Allows deletion of data from the specified table.<br><br>   * `CREATE` Allows creation of new databases, tables, views, stored procedures, functions, and other objects.<br><br>   * `DROP` Allows deletion of databases, tables, views, stored procedures, functions, and other objects.<br><br>   * `RELOAD` Allows reloading of system configuration files, restarting or shutting down the database, and other operations.<br><br>   * `REFERENCES` Allows creation or deletion of foreign key constraints in the current database.<br><br>   * `INDEX` Allows creation and deletion of indexes.<br><br>   * `ALTER` Allows modification of the structure of tables in the database, including operations such as changing fields, adding or deleting fields, and adding and deleting indexes.<br><br>   * `LOCK TABLES` Allows locking the specified data table for read and write operations.<br><br>   * `EXECUTE` Allows execution of existing stored procedures and functions, etc.<br><br>   * `CREATE VIEW` Allows creation of view objects.<br><br>   * `SHOW VIEW` Allows displaying the definition of views.<br><br>   * `CREATE ROUTINE` Allows creation of routine objects such as stored procedures and functions.<br><br>   * `ALTER ROUTINE` Allows modification of the definition of routines such as stored procedures and functions.<br><br>   * `CREATE USER` Allows creation of new users.<br><br>   * `EVENT` Allows creation, modification, and deletion of events.<br><br>   * `TRIGGER` Allows creation and management of triggers.<br><br>   * `SHOW DATABASES` Allows displaying all databases in the current database server.<br><br>   * `CREATE TEMPORARY TABLES` Allows creation of temporary tables.<br><br>* **Database\-specific authorization** Grants the account permissions for the specified databases. In the Database list of the **Database\-specific authorization** area, click text box in the **Permissions** column of the database for which permissions need to be set, and click **OK** after checking the corresponding permissions in the drop\-down menu.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you need to set the same permissions for multiple databases, you can check multiple target databases, click <strong>Batch setting of permissions</strong>, and click <strong>OK</strong> after checking permissions in the pop\-up window.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Supports granting the account <strong>Read/Write (DDL+DML)</strong>, <strong>Read\-only</strong>, <strong>DDL only</strong>, <strong>DML only</strong>, or <strong>Custom permissions for the specified database</strong>. Custom permissions can be one or more of <code>SELECT</code>, <code>INSERT</code>, <code>UPDATE</code>, <code>DELETE</code>, <code>CREATE</code>, <code>DROP</code>, <code>REFERENCES</code>, <code>INDEX</code>, <code>ALTER</code>, <code>CREATE TEMPORARY TABLES</code>, <code>LOCK TABLES</code>, <code>EXECUTE</code>, <code>CREATE VIEW</code>, <code>EVENT</code>, <code>SHOW VIEW</code>, <code>TRIGGER</code>, <code>CREATE ROUTINE</code> and <code>ALTER ROUTINE</code>.   </div><br>   <br><br>* **Authorization for tables and columns in a specified database** Grants permissions to some tables or columns in a specified database to an account.<br><br>   1. In the database list of the **Database\-specific authorization** area, click the icon to the right of the name of the database for which table and column permissions need to be set<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0af6ab4bfc8cae59d56a4c22f99cd408.png)<sub> </sub></span>icon.<br><br>   2. In the pop\-up **Set table and column permissions** window, select the target table or column, select the permissions on the right side of the window, and click **OK**.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the account has permissions for tables or columns in the database, the icon to the right of the database name will be displayed as<img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c9594f0b706ea159884b233ef1e531b5.png" />。 Note:   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If a table or column for which the account has permissions is deleted, the icon will be displayed as<img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c9594f0b706ea159884b233ef1e531b5.png" />。   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you retain the permissions of the account associated with the database for a database with the same name when deleting the database, and the account has list permissions for that database. After creating a new database with the same name, the icon will be displayed as<img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c9594f0b706ea159884b233ef1e531b5.png" />。   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Up to 200 data tables can be listed in the <strong>Set table and column permissions</strong> window. If the table or column for which you need to set permissions is not listed, use the <strong>Search table</strong> or <strong>Search column</strong> function to find it.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Supports granting accounts one or more of the following permissions for specified tables: <code>ALTER</code>, <code>CREATE</code>, <code>DELETE</code>, <code>DROP</code>, <code>INDEX</code>, <code>INSERT</code>, <code>SELECT</code>, <code>SHOW VIEW</code>, <code>TRIGGER</code>, <code>UPDATE</code>, <code>CREATE VIEW</code>, <code>REFERENCES</code>.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Supports granting accounts one or more of the following permissions for specified columns: <code>INSERT</code>, <code>REFERENCES</code>, <code>SELECT</code>, <code>UPDATE</code>.   </div><br>    |
   

7. Click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also click <strong>Preview</strong> to preview the SQL statement for creating an account with the specified configuration. Note that if a database name contains an underscore (_), the underscore is escaped as (\_) in the SQL statement when granting permissions to an account.   </div>
   

&nbsp;

<span id=".5bi46KeB6Zeu6aKY"></span>
## FAQ

**What are the differences between a super account and a normal account?** 


* Super account: You can create only one super account for each instance. It can manage all normal accounts and databases.

* Normal account: You can create multiple normal accounts for an instance. You must manually grant specific database privileges to them.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For specific information on account privileges, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_and_managing_an_account">Creating an account</a>.</div>


**Can I modify a specific permission of a super account?** 

The super account can only be reset to the initial status, not modified to specific permissions.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For specific information on account privileges, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_and_managing_an_account">Creating an account</a>.</div>


**Can a database be associated with multiple accounts?** 

No. A database can only be associated with one account.

<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[CreateDBAccount](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdbaccount) |Call the CreateDBAccount API to create an account. |
|[CreateDatabase](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdatabase1) |Call the CreateDatabase API to create a database. |
