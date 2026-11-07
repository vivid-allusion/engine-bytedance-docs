---
title: "Creating an account"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_and_managing_an_account"
---

This topic describes how to create a database account for a MySQL instance.

## Prerequisites

* An instance has been created and the instance state is **Running**. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* If you need to authorize an account by host IP, enable database proxy for the instance first. For more information about enabling the database proxy, refer to [Enabling database proxy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enable_database_agent).

## Precautions

* The console **Accounts** page does not support creating normal accounts with the same name as super accounts but a different host IP. If your business requires this, use SQL statements to create the account. Such normal accounts created via SQL are not displayed on the console **Account** page. Account‑management operations for these accounts cannot be performed through the console. In addition, do not perform any operations on these accounts using API interfaces.

* Creating accounts, modifying accounts, granting and revoking permissions can be completed via the console, Account‑management API interfaces, or SQL commands (CREATE USER, ALTER USER, GRANT, and REVOKE).

* Instances of different versions support different password authentication plugins. The specific differences are as follows:

   * MySQL 5.7 instances only support the **mysql_native_password** password authentication plugin.

   * MySQL 8.0 and MySQL 8.4 instances support two password authentication plugins: **mysql_native_password** and **caching_sha2_password ** . By Default, MySQL 8.0 uses **mysql_native_password**; MySQL 8.4 uses **caching_sha2_password**.

* Do not directly modify authentication fields such as plugin and authentication_string via UPDATE mysql.user. Such operations bypass the consistency processing for authentication plugins and authentication data performed by MySQL account‑management statements, and do not immediately refresh privilege information stored in memory. If authentication plugins do not match authentication data, account records may be deemed invalid and ignored when privilege tables reload (for example, after you run FLUSH PRIVILEGES, restart the instance, or perform a version upgrade with a subsequent restart). Consequently, the account cannot log in, or related account management operations fail. For more information, refer to the [official documentation](https://dev.mysql.com/doc/refman/5.7/en/privilege-changes.html).

* If you need to specify the password authentication plugin for a new account during account creation, or modify the password authentication plugin used by an existing account, use the CREATE USER and ALTER USER commands. Example as follows:

   ```SQL
   -- Specify the password authentication plugin when creating a new account
   CREATE USER 'app_user'@'%' IDENTIFIED WITH mysql_native_password BY 'psssword1';
   -- Modify the password authentication plugin for an existing account
   ALTER USER 'app_user'@'%' IDENTIFIED WITH caching_sha2_password BY 'password2';
   ```

## Procedure

1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   > **tip**

   > If the project of the instance has not been set, the project should be selected as **All resources**.

3. On the **Instances** page, click the target instance name.

4. On the target instance page, click **Accounts**.

5. On the **Accounts** tab, click **Create account**. In the displayed **Create account** page, set the following parameters and click **OK** to create the account.

   > **tip**

   > You can also click **Preview** after completing the settings to view the SQL statements for creating an account with the specified configuration.

   |Parameter |Description |
   |---|---|
   |Account type |Required. Select **Super account** or **Normal account**.<br><br><br>* Super account: Can manage all normal accounts and databases.<br><br>* Normal account: You need to manually grant specific database permissions to a normal account.<br><br><br>> **tip**<br><br><br>> A MySQL instance supports two types of database accounts: super accounts and normal accounts. After an account is created, its type cannot be changed.<br> |
   |Database account |Required Enter the account name. Naming rules are as follows:<br><br><br>* The database account name is globally unique.<br><br>* The account name must be 2 to 32 characters long.<br><br>* The name must start with a letter and ends with a letter or a digit.<br><br>* The name consists of letters, digits, underscores (_), and hyphens (\-).<br><br>* Certain reservation words or prohibited keywords cannot be used. For all disabled keywords and reservation words, refer to the [List of forbidden keywords](https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_forbidden_keywords).<br><br><br>> **tip**<br><br><br>> The keywords root and admin can be used in the super account name.<br> |
   |Description |Optional. Account description. The length does not exceed 256 characters, and can include digits, Chinese, English, underscores (_), and dashes (\-). |
   |Host IP |Required. Specifies the IP address where the account accesses the database.<br><br><br>* If the host IP is specified as %, allow the account to access the database from any IP address.<br><br>* If the host IP is specified as `192.10.10.%`, the account can access the database from IP addresses between `192.10.10.0` and `192.10.10.255`.<br><br>* The specified host IP needs to be added to the allowlist to which the instance is associated with, otherwise the instance cannot be accessed normally. For information on adding IP addresses to an allowlist, see [Modifying an allowlist](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_an_allowlist).<br><br><br>> **tip**<br><br><br><br>* > If the account type created is a super account, the host IP can only be specified as %.<br><br><br>* > If you need to specify the IP address for the account to access the database, you need to enable the database agent service for the instance. For more information, refer to [Enabling the database proxy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enable_database_agent).<br> |
   |Verification method |Required. Specify the verification method for the account, which can be **Password verification** or **IAM verification**.<br><br>> **tip**<br><br><br><br>* > The verification method cannot be modified after the account is created.<br><br><br>* > Super account does not support the IAM verification method.<br><br><br>* > It is recommended to select the IAM verification method only when the number of new IAM authenticated database connections created by the application per second is less than 200.<br><br><br>* > The total number of new IAM\-authenticated database connections created per second across all instances under the primary account must not exceed 20,000. Exceeding this limit will trigger traffic throttling and prevent new connections.<br><br><br>* > After you select the IAM verification method, the application uses a generated temporary token for verification when connecting to the database. Frequent creation of IAM\-authenticated database connections may exceed the connection limit. It is recommended to use a connection pool for centralized connection management. This allows applications to reuse existing connections and lowers the IAM authentication overhead from repeated connection creation.<br> |
   |Password |Required. Set the account password. Requirements are as follows:<br><br><br>* The password length is limited to 8~32 characters.<br><br>* It contains at least three of the following: uppercase letters, lowercase letters, digits, and special characters.<br><br>* Special characters are `!@#$%^&*() _ +-=,.&?\|/`.<br><br><br>> **tip**<br><br><br>> If you select **IAM verification**, you do not need to set a password for the account. When connecting, the system uses the obtained temporary token instead of a password for verification and login.<br> |
   |Confirm password |Required. Enter the password again to confirm. |
   |Permission settings |Grant global authorization for the account within the instance scope, authorization for a specified database, or authorization for tables and columns under a specified database.<br><br>> **tip**<br><br><br><br>* > Only permission setting for normal accounts is supported, and super accounts have all permissions by default.<br><br><br>* > Only databases that meet [the database name naming rules](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_a_database#.5pON5L2c5q2l6aqk) can be deleted through the console.<br><br><br>* > You cannot revoke your account's `PROCESS`, `REPLICATION SLAVE` or `REPLICATION CLIENT` permissions during account creation.<br><br><br>* > In the process of creating an account, except for the global permissions `PROCESS`, `REPLICATION SLAVE` and `REPLICATION CLIENT`, other permissions are optional. After creating an account, you can modify the account permissions according to your business needs. For more information, see [Modifying account permissions](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_account_permissions).<br><br><br>* **Global authorization** Set instance\-wide global permissions for the account. The selectable global permissions are shown in the following table, and multiple permissions can be selected. In the **Global authorization** area, check the corresponding permissions.<br><br>   * `PROCESS` Allows viewing information about all currently executing threads and processes.<br><br>   * `REPLICATION SLAVE` Allows replication of data from the primary server.<br><br>   * `REPLICATION CLIENT` Allows viewing and managing the status and parameters of the replication process.<br><br>   * `SELECT` Allows querying data from the specified table.<br><br>   * `INSERT` Allows inserting new data into the table.<br><br>   * `UPDATE` Allows updating data in the specified table.<br><br>   * `DELETE` Allows deletion of data from the specified table.<br><br>   * `CREATE` Allows creation of new databases, tables, views, stored procedures, functions, and other objects.<br><br>   * `DROP` Allows deletion of databases, tables, views, stored procedures, functions, and other objects.<br><br>   * `RELOAD` Allows reloading of system configuration files, restarting or shutting down the database, and other operations.<br><br>   * `REFERENCES` Allows creation or deletion of foreign key constraints in the current database.<br><br>   * `INDEX` Allows creation and deletion of indexes.<br><br>   * `ALTER` Allows modification of the structure of tables in the database, including operations such as changing fields, adding or deleting fields, and adding and deleting indexes.<br><br>   * `LOCK TABLES` Allows locking the specified data table for read and write operations.<br><br>   * `EXECUTE` Allows execution of existing stored procedures and functions, etc.<br><br>   * `CREATE VIEW` Allows creation of view objects.<br><br>   * `SHOW VIEW` Allows displaying the definition of views.<br><br>   * `CREATE ROUTINE` Allows creation of routine objects such as stored procedures and functions.<br><br>   * `ALTER ROUTINE` Allows modification of the definition of routines such as stored procedures and functions.<br><br>   * `CREATE USER` Allows creation of new users.<br><br>   * `EVENT` Allows creation, modification, and deletion of events.<br><br>   * `TRIGGER` Allows creation and management of triggers.<br><br>   * `SHOW DATABASES` Allows displaying all databases in the current database server.<br><br>   * `CREATE TEMPORARY TABLES` Allows creation of temporary tables.<br><br>* **Database\-specific authorization** Grants the account permissions for the specified databases. In the Database list of the **Database\-specific authorization** area, click text box in the **Permissions** column of the database for which permissions need to be set, and click **OK** after checking the corresponding permissions in the drop\-down menu.<br><br>   > **tip**<br>   <br><br>   * > If you need to set the same permissions for multiple databases, you can check multiple target databases, click **Batch setting of permissions**, and click **OK** after checking permissions in the pop\-up window.<br>   <br><br>   * > Supports granting the account **Read/Write (DDL+DML)**, **Read\-only**, **DDL only**, **DML only**, or **Custom permissions for the specified database**. Custom permissions can be one or more of `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `CREATE`, `DROP`, `REFERENCES`, `INDEX`, `ALTER`, `CREATE TEMPORARY TABLES`, `LOCK TABLES`, `EXECUTE`, `CREATE VIEW`, `EVENT`, `SHOW VIEW`, `TRIGGER`, `CREATE ROUTINE` and `ALTER ROUTINE`.<br>   <br><br>* **Authorization for tables and columns in a specified database** Grants permissions to some tables or columns in a specified database to an account.<br><br>   1. In the database list of the **Database\-specific authorization** area, click the icon to the right of the name of the database for which table and column permissions need to be set![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0af6ab4bfc8cae59d56a4c22f99cd408.png)icon.<br><br>   2. In the pop\-up **Set table and column permissions** window, select the target table or column, select the permissions on the right side of the window, and click **OK**.<br><br>   > **tip**<br>   <br><br>   * > When the account has permissions for tables or columns in the database, the icon to the right of the database name will be displayed as![](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c9594f0b706ea159884b233ef1e531b5.png)。 Note:<br>   <br><br>      * > If a table or column for which the account has permissions is deleted, the icon will be displayed as![](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c9594f0b706ea159884b233ef1e531b5.png)。<br>   <br><br>      * > If you retain the permissions of the account associated with the database for a database with the same name when deleting the database, and the account has list permissions for that database. After creating a new database with the same name, the icon will be displayed as![](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c9594f0b706ea159884b233ef1e531b5.png)。<br>   <br><br>   * > Up to 200 data tables can be listed in the **Set table and column permissions** window. If the table or column for which you need to set permissions is not listed, use the **Search table** or **Search column** function to find it.<br>   <br><br>   * > Supports granting accounts one or more of the following permissions for specified tables: `ALTER`, `CREATE`, `DELETE`, `DROP`, `INDEX`, `INSERT`, `SELECT`, `SHOW VIEW`, `TRIGGER`, `UPDATE`, `CREATE VIEW`, `REFERENCES`.<br>   <br><br>   * > Supports granting accounts one or more of the following permissions for specified columns: `INSERT`, `REFERENCES`, `SELECT`, `UPDATE`.<br>    |

7. Click **OK**.

   > **tip**

   > You can also click **Preview** to preview the SQL statement for creating an account with the specified configuration. Note that if a database name contains an underscore (_), the underscore is escaped as (\_) in the SQL statement when granting permissions to an account.

## FAQ

**What are the differences between a super account and a normal account?**

* Super account: Can manage all normal accounts and databases.

* Normal account: You must manually grant specific database privileges.

> **tip**

> For detailed information about account permissions, refer to [Account permission description](https://docs.byteplus.com/en/docs/RDS_for_MySQL/account_permissions1).

**Can I modify a specific permission of a super account?**

The super account can only be reset to the initial status, not modified to specific permissions.

> **tip**

> For detailed information about account permissions, refer to [Account permission description](https://docs.byteplus.com/en/docs/RDS_for_MySQL/account_permissions1).

**Can a database be associated with multiple accounts?**

Yes.

**Why is the account state 'Unavailable'?**

Reason: If a database account is deleted from the command line after it has been created, its state is displayed as **Unavailable** in the account list on the console.

Solution: Reset the password for the account in the console to restore it to an available state. For details about resetting the password, refer to [Resetting account password](https://docs.byteplus.com/en/docs/RDS_for_MySQL/resetting_an_account_password). We recommend performing account management operations in the console to prevent the account from becoming **Unavailable**.

## Related API

|API |Description |
|---|---|
|[CreateDBAccount](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdbaccount) |Call the CreateDBAccount API to create an account. |
|[DescribeDBAccounts](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbaccounts) |Call the DescribeDBAccounts API to view the account list. |
