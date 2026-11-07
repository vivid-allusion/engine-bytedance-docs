---
title: "Account permissions"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/account_permissions1"
---

This topic introduces the account types and account permission description of a MySQL instance.

<span id=".6LSm5Y-357G75Z6L"></span>
## Account type

A MySQL instance supports two types of database accounts: super accounts and normal accounts. After an account is created, its type cannot be changed.


|Account type |Description |
|---|---|
|Super account |* Can be created and managed through the console or API.<br><br>* Manages all normal accounts and databases.<br><br>* It provides more privileges for personalized and fine\-grained privilege management. For example, you can grant query privileges for different tables to different users.<br><br>* Has privileges for all databases in the instance.<br><br>* Can disconnect any account. |
|Normal account |* Can be created and managed via the console, API, or SQL statements.<br><br>* You can create multiple normal accounts in an instance. The specific quantity depends on the instance kernel.<br><br>* You need to manually grant specific database permissions to a normal account.<br><br>* A normal account cannot disconnect the connections of other accounts. |


<span id=".6LSm5Y-35p2D6ZmQ"></span>
## Account privileges

RDS for MySQL provides six types of permissions for accounts: basic data operation, database and table structure management, stored procedure and event, basic operation session, advanced system management, and primary\-secondary replication, as detailed in the table below.


|**Type** |**Privilege** |
|---|---|
|Basic data operation privileges |`SELECT`, `INSERT`, `UPDATE`, `DELETE` |
|Database and table structure management privileges |`ALTER`, `CREATE`, `DROP`, `INDEX`, `CREATE TEMPORARY TABLES`, `CREATE VIEW`, `SHOW VIEW`, `TRIGGER`, `REFERENCES` |
|Stored procedure and event privileges |`ALTER ROUTINE`, `CREATE ROUTINE`, `EXECUTE`, `EVENT` |
|Basic operation session privileges |`LOCK TABLES`, `PROCESS` |
|Advanced system management privileges |`CREATE USER`, `GRANT`, `RELOAD`, `SHOW DATABASES`<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">In RDS for MySQL, the <code>GRANT</code> privilege cannot be granted to a normal account.</div><br> |
|Primary\-secondary replication privileges |`REPLICATION CLIENT`, `REPLICATION SLAVE` |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In some older versions of instances, the account privileges may be inconsistent with those described in the table above. If this occurs, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> to contact technical support to upgrade the instance.</div>


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permission description

The following table details the permissions that RDS for MySQL provides for accounts.


|Privilege |Description |
|---|---|
|ALTER |Allows modification of the structure of tables in the database, including operations such as changing fields, adding or deleting fields, and adding and deleting indexes. |
|ALTER ROUTINE |Allows modification of the definition of routines such as stored procedures and functions. |
|CREATE |Allows creation of new databases, tables, views, stored procedures, functions, and other objects. |
|CREATE ROUTINE |Allows creation of routine objects such as stored procedures and functions. |
|CREATE TEMPORARY TABLES |Allows creation of temporary tables. |
|CREATE USER |Allows creation of new users. |
|CREATE VIEW |Allows creation of view objects. |
|DELETE |Allows deletion of data from the specified table. |
|DROP |Allows deletion of databases, tables, views, stored procedures, functions, and other objects. |
|EVENT |Allows creation, modification, and deletion of events. |
|EXECUTE |Allows execution of existing stored procedures and functions, etc. |
|GRANT |Allows users to assign access rights to other users. |
|INDEX |Allows creation and deletion of indexes. |
|INSERT |Allows inserting new data into the table. |
|LOCK TABLES |Allows locking the specified data table for read and write operations. |
|PROCESS |Allows viewing information about all currently executing threads and processes. |
|REFERENCES |Allows creation or deletion of foreign key constraints in the current database. |
|RELOAD |Allows reloading of system configuration files, restarting or shutting down the database, and other operations. |
|REPLICATION CLIENT |Allows viewing and managing the status and parameters of the replication process. |
|REPLICATION SLAVE |Allows replication of data from the primary server. |
|SELECT |Allows querying data from the specified table. |
|SHOW DATABASES |Allows displaying all databases in the current database server. |
|SHOW VIEW |Allows displaying the definition of views. |
|TRIGGER |Allows creation and management of triggers. |
|UPDATE |Allows updating data in the specified table. |


&nbsp;

&nbsp;
