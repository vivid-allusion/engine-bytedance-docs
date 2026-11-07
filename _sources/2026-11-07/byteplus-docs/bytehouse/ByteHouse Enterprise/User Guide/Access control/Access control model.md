---
title: "Access control model"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/privilege-model"
---

ByteHouse follows the RBAC model and has designed a privilege model that supports both single\-cluster and multi\-cluster privilege management. ByteHouse's privilege management supports granting privileges through roles and behavior for users, allowing flexible access control over databases, tables, columns, indexes, and views within the cluster data resources. This document introduces the basic concepts and architectural design of ByteHouse's privilege model.

<span id="66bd0f8a"></span>
# Basic concepts

Within a ByteHouse cluster, the privilege model involves the following five concepts:


* Data Object: An entity within a database. For ByteHouse, data objects include the following entities: Database (Datebase), Tables (Table), Columns (Column), Indexes (Index), Views (View), Projections (Projection), etc.

* User: A user corresponds to a set of username and password, used for establishing a database connection.

* Role: A role constitutes a collection of privileges. Role management enables batch authorization for users in a specific role within a project, reducing repetitive and complex authorization operations. A role can be assigned to multiple users.

* Privilege: An abstract strategy expressing whether a user is allowed operations like Insert, Drop, Alter, and Select on data objects.

* Row Policy: A security strategy used to control data access. Allows conditions to be applied to the rows of a table to control which data rows different users can access. This row\-level security policy can be used to protect sensitive data, ensuring that only users meeting specific conditions can access certain data rows.


<span id="4b16e672"></span>
# Privilege model

ByteHouse has built its own privilege model based on the default privilege system of the ClickHouse community, which includes both single\-cluster and multi\-cluster models. The default privilege system of the ClickHouse community is the RBAC model, supporting the interrelation of the quartet: [User](https://clickhouse.com/docs/sql-reference/statements/create/user), [Role](https://clickhouse.com/docs/sql-reference/statements/create/role), Privilege, and Data Object, with operations interlinked through [Revoke](https://clickhouse.com/docs/sql-reference/statements/revoke) and [Grant](https://clickhouse.com/docs/sql-reference/statements/grant) syntax to achieve distribution and adjustment of privileges. On the basis of the ClickHouse privilege model, ByteHouse has developed a multi\-cluster model that enables cross\-cluster data unified control by assigning cross\-cluster roles and privileges to users, enhancing the efficiency of privilege control while refining the granularity of privilege management and meeting the needs of different scenarios.


|Single Cluster Model |Multi\-cluster Model |
|---|---|
|In a single cluster, the ByteHouse Enterprise version's privilege model is as follows: it supports granting privileges directly to users and also via roles.<br><br>When managing multiple users and roles is needed,<br><br><br>* System administrators can grant the same privileges to multiple users at once through a role, reducing redundant authorization tasks.<br><br>* System administrators can also grant multiple role privileges to a single user; in this case, the user's privileges will be the union of the privileges from multiple roles.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ecc120189c05467da7aea001ae2d68a3~tplv-goo7wpa0wc-image.image) </span> |The multi\-cluster model facilitates cross\-cluster user privileges management. System administrators can create roles based on data\-object\-related privileges within each cluster, granting them to different users within the same cluster. The same user can be part of different clusters.<br><br>As a cross\-cluster entity, the user supports being granted different roles in different clusters to obtain corresponding privileges, thus enabling cross\-cluster privileges management. Administrators need to configure at least one usable cluster range for the user, then base privileges directly to users or through roles based on the cluster. After directly granting privileges, a user will automatically join the current cluster.<br><br>Roles are entities under the cluster dimension. ByteHouse offers roles, with the System Admin acting as a super admin who has cross\-cluster privileges and can manage all clusters within a tenant. Other roles (Cluster Admin, Data Engineer, Query User, custom roles) are cluster\-specific roles without cross\-cluster privileges.<br><br>privileges refer to the rights to data objects within a specific cluster and cannot be applied across clusters.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/797c50133c424056bfb6439a10ae146f~tplv-goo7wpa0wc-image.image) </span><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Modifying the password of a user through the console will affect all clusters that the user belongs to.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Do not modify the current cluster's user password at the cluster level, otherwise, users will not be able to perform create, delete, modify, or query operations on tables under that cluster via the console.</div><br> |


<span id="f9f33e4c"></span>
# Default roles and custom roles

ByteHouse offers you default roles and custom roles; there are four default roles, namely System Admin, Cluster Admin, Data Engineer, Query User, each with different privileges. Additionally, you can create custom roles with unique names and privileges, ensuring these names do not duplicate those of default roles.


| |**Custom role** |**Query User** |**Data Engineer** |**Cluster Admin** |**System Admin** |
|---|---|---|---|---|---|
|Role Overview |User\-defined roles |Read\-only role with data query access |Role with data manipulation privileges |Role with privileges to manage the entire cluster |Role with privileges to manage the entire ByteHouse GUI |
|Role level |Role within the cluster |Role within the cluster |Role within the cluster |Role within the cluster |Cross\-Cluster Roles |
|Database Table privileges |None by default, supports custom database table privilege scopes |By default, only read privileges for the Default database |By default, has read and write privileges for the Default database |By default, has read and write privileges for all database tables within the cluster |By default, has read and write privileges for all database tables across all clusters under the tenant |
|Resource privileges/Console Features ||||||
|Data Management |None |None |None |Role Management, Role Authorization |User Management, User Authorization, Role Management, Role Authorization |
|Data Import |View |View |View, Edit |View, Edit |View, Edit |
|Data Query |View, inquire |View, inquire |View, inquire |View, inquire |View, inquire |
|Cluster Management |View |View |View |View, Cluster Management |View, Cluster Management |


<span id="b7c2623a"></span>
# **User types**

ByteHouse users can be categorized as main users, sub\-users, system administrators, non\-administrator users, and system users.


|User Types |Definition |User Default privileges and Authorization Operation Instructions |
|---|---|---|
|User |Primary and secondary users are collectively referred to as users. A user corresponds to a username and password. |General description, please refer to the primary and secondary user privileges and authorization description for distinction. |
|Primary User |The primary user associated with a BytePlus account, each BytePlus account has only one primary user. |This user has access to all services of ByteHouse and can create sub\-users and assign specific privileges under the affiliated tenant.<br><br>For primary user privilege configuration, see [User Management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user). |
|IAM sub\-user |The main user of the BytePlus account creates users in ByteHouse. |When this user is created by default, they do not have any access privileges to the ByteHouse clusters. The primary user must assign specific privilege strategies before ordinary users can log in with the sub\-user password assigned by the primary user and use ByteHouse's service.<br><br>To configure privileges for sub\-users, see [IAM sub-user management](https://docs.byteplus.com/docs/bytehouse/sub-user-management). |
|Database user |Database\-level user. |By default, this database user is not granted any privileges on ByteHouse databases upon creation. An administrator must assign specific roles or grant data privileges to the user. Database users can log in and access ByteHouse services using the database username and password configured by the administrator.<br><br>For instructions on creating database users and configuring their privileges, refer to [Database user management](https://docs.byteplus.com/docs/bytehouse/database-user-management). |
|System Admin |User with the “system_admin” role. |This user is the super admin and can control all functions of ByteHouse, created by the system by default.<br><br>You can view the users marked as "Yes" in the Admin column of the user list via the **ByteHouse Console** \> **Access control** \> **User** Path. |
|Non\-admin user |Users not granted the "system_admin" role. |The user's privileges must be granted by the system administrator, and different users have different privileges. You can contact the system administrator for configuration, for details see [IAM sub-user management](https://docs.byteplus.com/docs/bytehouse/sub-user-management).<br><br>You can view users marked as "No" in the Admin column of the user list via **ByteHouse Console\>Access control\>User** path.<br><br>After creation, the system administrator can configure some console functionalities for non\-administrators collectively. For details, see [Non-admin user management](https://docs.byteplus.com/docs/bytehouse/non-admin-user-management). |
|System user |DBA users, ByteHouse engine configuration users. |This user is only used for internal communication within the system, displayed only in the user list and requires no actions. There is only one DBA user per BytePlus account, but the password for each cluster varies.<br><br>You can access the **ByteHouse Console**\>**privilege Management**\>**User** path and search for **dba** in the User List to view the details. |


<span id="e75a2c67"></span>
# Description of grantable database and table privileges

ByteHouse Enterprise supports granting data privileges directly to users or roles. The details of these privileges are explained as follows:


|Privileges |Description |
|---|---|
|TRUNCATE |Grant users privileges to clear all data from specified databases, tables, external tables, views, or materialized views (delete data only, retain table structure). |
|ALTER |Modify data privileges.<br><br><br>* ALTER: This privilege can only be granted at the database level, allowing modification of all tables, foreign tables, views, and materialized views within the specified database. The ALTER privilege also includes the following privileges: ALTER TABLE, ALTER VIEW, ALTER DELETE, and ALTER UPDATE.<br><br>* ALTER TABLE: Grants users the privilege to modify a specified table or external table.<br><br>* ALTER VIEW: Grant users the privilege to modify specified views or materialized views.<br><br>* ALTER DELETE: Grants users the privilege to delete data from specified databases, tables, external tables, views, or materialized views.<br><br>* ALTER UPDATE: Grant users the privilege to update data in a specified database, table, external table, view, or materialized view. |
|CREATE |Create data resources.<br><br><br>* CREATE: This privilege can only be granted at the database level and allows users to create databases, tables, foreign tables, views, and materialized views. The CREATE privilege also supports the following privileges: CREATE DATABASE, CREATE TABLE, CREATE VIEW, and CREATE TEMPORARY TABLE.<br><br>* CREATE DATABASE: Grants users the privilege to create a database.<br><br>* CREATE TABLE: Grants users the privilege to create tables or external tables in the specified database.<br><br>* CREATE VIEW: Grants users the privilege to create views or materialized views in the specified database.<br><br>* CREATE TEMPORARY TABLE: This privilege can only be set at the database level and grants users the ability to create temporary tables in the specified database. When granting, select ALL for the database.<br><br>* CREATE DICTIONARY：Grants users the privilege to create dictionaries in the specified database. |
|DROP |Delete data.<br><br><br>* DROP: Grants users the privilege to create databases, tables, external tables, views, and materialized views. The DROP privilege also includes the following privileges: DROP DATABASE, DROP TABLE, and DROP VIEW.<br><br>* DROP DATABASE: Grants users the privilege to delete a specified database.<br><br>* DROP TABLE: Grants users the privilege to delete tables or external tables in the specified database.<br><br>* DROP VIEW: Grants users the privilege to delete views or materialized views in the specified database.<br><br>* DROP DICTIONARY：Grants users the privilege to delete dictionaries in the specified database. |
|SHOW |View the data.<br><br><br>* SHOW: Grants users the privilege to view databases, tables, external tables, views, and materialized views.<br><br>* SHOW TABLES: This privilege can only be set at the database level. It grants users privilege to view tables, external tables, views, and materialized views in the specified database, and grants users privilege to execute `SHOW TABLES`, `EXISTS <table>`, and `CHECK <table>` queries.<br><br>* SHOW COLUMNS: Grants users the privilege to view the column structure of a specified database, table, external table, view, or materialized view, and grants privilege to execute `SHOW CREATE TABLE` and `DESCRIBE` queries.<br><br>* SHOW DICTIONARIES：Grants the privilege to view dictionaries in the specified database, and also grants users the permission to execute the SHOW CREATE DICTIONARY query.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When a user has any other privilege on a database table, SHOW privilege is automatically granted.</div><br> |
|SYSTEM |* SYSTEM: This privilege can only be set for databases and grants users the ability to perform system\-level operations. For more information, see [ClickHouse community documentation](https://clickhouse.com/docs/zh/sql-reference/statements/system).<br><br>* SYSTEM CONSUME: Grants users the privilege to consume Kafka tables. |
|SELECT |Grant users query privileges on databases, tables, external tables, views, materialized views, and columns. |
|INSERT |Grant users insert privileges on the specified database, table, external table, view, materialized view, or column. |
|Customize |You can add custom privileges as needed. Each privilege must correspond to SQL statements supported by ByteHouse. |
|MYSQL |Grant users the privilege to create MySQL external tables in the specified database. When granting privileges, the database must be set to ALL, and both the MYSQL and CREATE privileges must be granted. |
|MANAGE |Grant users the privileges to manage user\-defined function (UDF) privileges, including privileges to create, edit, and delete UDF privileges. |
|dictGet |Grants users the privilege to query dictionary data using the dictGet function. |


<span id="e9a7528a"></span>
# Authorization operation guide

No matter who the user is, the principle of "least privilege" should always be applied: only the necessary privileges needed for user activities are assigned.


* Operation guides: [Role management](https://docs.byteplus.com/docs/bytehouse/role-management), [IAM sub-user management](https://docs.byteplus.com/docs/bytehouse/sub-user-management),[Database user management](https://docs.byteplus.com/docs/bytehouse/database-user-management), [Row privilege](https://docs.byteplus.com/docs/bytehouse/row-privilege),[Non-admin user management](https://docs.byteplus.com/docs/bytehouse/non-admin-user-management)
