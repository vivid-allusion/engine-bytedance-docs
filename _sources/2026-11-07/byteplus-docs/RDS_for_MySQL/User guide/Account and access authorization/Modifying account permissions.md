---
title: "Modifying account permissions"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_account_permissions"
---

You can modify the permissions of a normal account as needed. This topic explains how to modify account privileges for a normal account and the procedure.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance is created and in the **Running** state. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* An account has been created. For more information on specific operations, refer to [Creating an account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_and_managing_an_account#.5Yib5bu66LSm5Y-3).

* The instance account permission is **Normal account**.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* A super account can only be reset to the initial status. Its permissions cannot be modified.

* Modifying account permissions may cause impact on business, proceed with caution.

* Only databases that meet [the database name naming rules](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_a_database#.5pON5L2c5q2l6aqk) can be deleted through the console.

* If the account obtains permissions that are not supported by RDS for MySQL through non\-console methods, it cannot modify the permissions through the console. It is recommended to use the command\-line tool to adjust the permissions. For the permissions supported by RDS for MySQL, see [Account permissions](https://docs.byteplus.com/en/docs/RDS_for_MySQL/account_permissions1).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.</div>



3. Click on **Instances** in the left navigation bar.

4. On the **Instances** page, click on the target instance name.

5. Click **Accounts** at the top of the page.

6. On the **Accounts** tab, click **Modify permission** in the **Actions** column of the target account.

7. Set the following parameters in the **Modify permission** pop\-up dialog box.

   
   |Parameter |Description |
   |---|---|
   |Host IP |Required. Specifies the IP address where the account accesses the database.<br><br><br>* If the host IP is specified as %, allow the account to access the database from any IP address.<br><br>* If the host IP is specified as `192.10.10.%`, the account can access the database from IP addresses between `192.10.10.0` and `192.10.10.255`.<br><br>* The specified host IP needs to be added to the allowlist to which the instance is associated with, otherwise the instance cannot be accessed normally. For information on adding IP addresses to an allowlist, see [Modifying an allowlist](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_an_allowlist).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If the account type created is a super account, the host IP can only be specified as %.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you need to specify the IP address for the account to access the database, you need to enable the database agent service for the instance. For more information, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/enable_database_agent">Enabling the database proxy</a>.</div><br> |
   |Permission settings |Grant global authorization for the account within the instance scope, authorization for a specified database, or authorization for tables and columns under a specified database.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Only permission setting for normal accounts is supported, and super accounts have all permissions by default.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Only databases that meet <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_a_database#.5pON5L2c5q2l6aqk">the database name naming rules</a> can be deleted through the console.</div><br><br><br>* **Global authorization** Set instance\-wide global permissions for the account. The available global permissions are shown in the table below. You can select multiple permissions. In the **Global authorization** area, check the corresponding permissions.<br><br>   * `PROCESS` Allows viewing information about all currently executing threads and processes.<br><br>   * `REPLICATION SLAVE` Allows replication of data from the primary server.<br><br>   * `REPLICATION CLIENT` Allows viewing and managing the status and parameters of the replication process.<br><br>   * `SELECT` Allows querying data from the specified table.<br><br>   * `INSERT` Allows inserting new data into the table.<br><br>   * `UPDATE` Allows updating data in the specified table.<br><br>   * `DELETE` Allows deletion of data from the specified table.<br><br>   * `CREATE` Allows creation of new databases, tables, views, stored procedures, functions, and other objects.<br><br>   * `DROP` Allows deletion of databases, tables, views, stored procedures, functions, and other objects.<br><br>   * `RELOAD` Allows reloading of system configuration files, restarting or shutting down the database, and other operations.<br><br>   * `REFERENCES` Allows creation or deletion of foreign key constraints in the current database.<br><br>   * `INDEX` Allows creation and deletion of indexes.<br><br>   * `ALTER` Allows modification of the structure of tables in the database, including operations such as changing fields, adding or deleting fields, and adding and deleting indexes.<br><br>   * `LOCK TABLES` Allows locking the specified data table for read and write operations.<br><br>   * `EXECUTE` Allows execution of existing stored procedures and functions, etc.<br><br>   * `CREATE VIEW` Allows creation of view objects.<br><br>   * `SHOW VIEW` Allows displaying the definition of views.<br><br>   * `CREATE ROUTINE` Allows creation of routine objects such as stored procedures and functions.<br><br>   * `ALTER ROUTINE` Allows modification of the definition of routines such as stored procedures and functions.<br><br>   * `CREATE USER` Allows creation of new users.<br><br>   * `EVENT` Allows creation, modification, and deletion of events.<br><br>   * `TRIGGER` Allows creation and management of triggers.<br><br>   * `SHOW DATABASES` Allows displaying all databases in the current database server.<br><br>   * `CREATE TEMPORARY TABLES` Allows creation of temporary tables.<br><br>* **Database\-specific authorization** Grants the account permissions for the specified databases. In the Database list of the **Database\-specific authorization** area, click text box in the **Permissions** column of the database for which permissions need to be set, and click **OK** after checking the corresponding permissions in the drop\-down menu.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you need to set the same permissions for multiple databases, you can check multiple target databases, click <strong>Batch setting of permissions</strong>, and click <strong>OK</strong> after checking permissions in the pop\-up window.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Supports granting the account <strong>Read/Write (DDL+DML)</strong>, <strong>Read\-only</strong>, <strong>DDL only</strong>, <strong>DML only</strong>, or <strong>Custom permissions for the specified database</strong>. Custom permissions can be one or more of <code>SELECT</code>, <code>INSERT</code>, <code>UPDATE</code>, <code>DELETE</code>, <code>CREATE</code>, <code>DROP</code>, <code>REFERENCES</code>, <code>INDEX</code>, <code>ALTER</code>, <code>CREATE TEMPORARY TABLES</code>, <code>LOCK TABLES</code>, <code>EXECUTE</code>, <code>CREATE VIEW</code>, <code>EVENT</code>, <code>SHOW VIEW</code>, <code>TRIGGER</code>, <code>CREATE ROUTINE</code> and <code>ALTER ROUTINE</code>.   </div><br>   <br><br>* **Authorization for tables and columns in a specified database** Grants permissions to some tables or columns in a specified database to an account.<br><br>   1. In the database list of the **Database\-specific authorization** area, click the icon to the right of the name of the database for which table and column permissions need to be set<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0af6ab4bfc8cae59d56a4c22f99cd408.png)<sub> </sub></span>icon.<br><br>   2. In the pop\-up **Set table and column permissions** window, select the target table or column, select the permissions on the right side of the window, and click **OK**.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the account has permissions for tables or columns in the database, the icon to the right of the database name will be displayed as<img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c9594f0b706ea159884b233ef1e531b5.png" />。 Note:   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If a table or column for which the account has permissions is deleted, the icon will be displayed as<img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c9594f0b706ea159884b233ef1e531b5.png" />。   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you retain the permissions of the account associated with the database for a database with the same name when deleting the database, and the account has list permissions for that database. After creating a new database with the same name, the icon will be displayed as<img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c9594f0b706ea159884b233ef1e531b5.png" />。   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Up to 200 data tables can be listed in the <strong>Set table and column permissions</strong> window. If the table or column for which you need to set permissions is not listed, use the <strong>Search table</strong> or <strong>Search column</strong> function to find it.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Supports granting accounts one or more of the following permissions for specified tables: <code>ALTER</code>, <code>CREATE</code>, <code>DELETE</code>, <code>DROP</code>, <code>INDEX</code>, <code>INSERT</code>, <code>SELECT</code>, <code>SHOW VIEW</code>, <code>TRIGGER</code>, <code>UPDATE</code>, <code>CREATE VIEW</code>, <code>REFERENCES</code>.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Supports granting accounts one or more of the following permissions for specified columns: <code>INSERT</code>, <code>REFERENCES</code>, <code>SELECT</code>, <code>UPDATE</code>.   </div><br>    |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also click <strong>Preview</strong> to preview the SQL statement for modifying the account's permission configuration. Note that if a database name contains an underscore (_), the underscore is escaped as (\_) in the SQL statement when granting permissions to an account.   </div>
   

3. Click **OK** to complete the permission modification of the account.


<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[GrantDBAccountPrivilege](https://docs.byteplus.com/en/docs/RDS_for_MySQL/grantdbaccountprivilege) |Call GrantDBAccountPrivilege API to grant database account permissions. |
