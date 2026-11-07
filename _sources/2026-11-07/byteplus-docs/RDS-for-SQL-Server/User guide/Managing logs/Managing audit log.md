---
title: "Managing audit log"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/managing-audit-log"
---

RDS for SQL Server provides auditing capabilities that help you log major events at the service, database, and table levels. This article describes how to view and download audit logs for an instance in the SQL Server Edition console of a cloud database.

<span id="prerequisite"></span>
## prerequisite

An instance has been created, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide) for details.

<span id="precautions"></span>
## Precautions


* The maximum size of each file in the audit log is 50 MB, and each instance can retain 50 files. Exceeding this limit will overwrite the earliest collected audit log. Audit logs do not yet provide a clear retention period.

* Instance\-level parameters and objects cannot be audited, such as creating a JOB, modifying parameters, modifying server property parameters, modifying SQL Agent property parameters, database extension properties, and linking services.

* Enabling audit capabilities has no more than a 5% impact on overall instance performance.

* When the master and standby node is created, the default audit is turned on synchronously. When the master and standby switch occurs, you will find the audit record of the current master node.

* Instances after `MSSQL2019CU23 = "15.0.4335"` support viewing and downloading audit logs.


<span id="background-information"></span>
## Background information

The behavior of audit log support records is shown in the following table.


|**action group name** |**explain** |
|---|---|
|APPLICATION_ROLE_CHANGE_PASSWORD_GROUP |Event raised by changing the password of an application role. |
|DATABASE_CHANGE_GROUP |Create, change, and delete databases. |
|DATABASE_OBJECT_CHANGE_GROUP |This event is raised when `create`, `alter`, `drop` statements are executed against database objects, such as schemas. |
|DATABASE_OBJECT_OWNERSHIP_CHANGE_GROUP |This event is triggered when an object owner is changed at the database scope. |
|DATABASE_OBJECT_PERMISSION_CHANGE_GROUP |This event is raised when a `GRANT`, `REVOKE`, or `DENY` statement is issued against database objects, such as assemblies and schemas. |
|DATABASE_OWNERSHIP_CHANGE_GROUP |Raises this event when you use the `alter authorization` statement to change the owner of the database. |
|DATABASE_PERMISSION_CHANGE_GROUP |This event is raised when a `GRANT`, `REVOKE`, or `DENY` statement is issued by any principal in SQL Server for permissions on a statement (only for database events, such as granting permissions on a database) |
|DATABASE_PRINCIPAL_CHANGE_GROUP |This event is raised when a principal, such as a user, is created, changed, or deleted in the database. |
|DATABASE_ROLE_MEMBER_CHANGE_GROUP |This event is raised when a login is added to or removed from a database role. |
|FAILED_LOGIN_GROUP |Indicates that the principal tried to log in to SQL Server, but failed. Events in this class are raised by new connections or by reused connections in the connection pool. |
|LOGIN_CHANGE_PASSWORD_GROUP |This event is raised when the login password is changed through the `alter login` statement or `sp_password` stored procedure. |
|SCHEMA_OBJECT_CHANGE_GROUP |Raises this event when a `create`, `alter`, or `drop` operation is performed on the schema. |
|SCHEMA_OBJECT_OWNERSHIP_CHANGE_GROUP |This event is raised when you check to change the permissions of the owner of a schema object, such as a table, procedure, or function. |
|SCHEMA_OBJECT_PERMISSION_CHANGE_GROUP |This event is raised when a `grant`, `deny`, or `revoke` statement is executed on a schema object. |
|SERVER_OBJECT_CHANGE_GROUP |Raises this event when `create`, `alter`, `drop` operations are performed on server objects. |
|SERVER_OBJECT_OWNERSHIP_CHANGE_GROUP |This event is raised when the owner of an object in the server scope changes. |
|SERVER_OBJECT_PERMISSION_CHANGE_GROUP |This event is raised when any principal in SQL Server issues a `grant`, `revoke`, or `deny` statement for permissions on a server object. |
|SERVER_PERMISSION_CHANGE_GROUP |This event is raised when `grant`, `revoke`, `deny` statements are issued to obtain server\-wide permissions. |
|SERVER_PRINCIPAL_CHANGE_GROUP |This event is raised when a server principal is created, changed, or deleted. |
|SERVER_ROLE_MEMBER_CHANGE_GROUP |This event is raised when a login is added to or removed from a fixed server role. |
|SERVER_STATE_CHANGE_GROUP |This event is raised when you modify the SQL Server service state. |
|USER_CHANGE_PASSWORD_GROUP |This event is raised whenever the password containing the database user is changed using the `alter user` statement. |


<span id="review-the-audit-log"></span>
## Review the audit log


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **instance list** page, click the target instance name to go to the **instance information** tab.

4. At the top of the page, click **Log Management**.

5. On the **Log Management** tab, click **Audit logs**.

6. On the **Audit Log** subtab, you can view a list of all audit logs recorded, including information such as the **file name**, **file size**, and **collection time** of the audit log.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The file name of the audit log starts with <strong>audit_rds_default</strong>, ends with <code>.sqlaudit</code>, and is automatically populated with timestamp as the file name.   </div>
   

<span id="download-the-audit-log"></span>
## Download the audit log


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **instance list** page, click the target instance name to go to the **instance information** tab.

4. At the top of the page, click **Log Management**.

5. On the **Log Management**tab, click **Audit logs**.

6. On the **Audit Log** subtab, click Download in the Destination File Operations column to download the logs locally.
