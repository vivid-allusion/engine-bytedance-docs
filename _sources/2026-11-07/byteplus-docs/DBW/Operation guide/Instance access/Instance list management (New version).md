---
title: "Instance list management (New version)"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/instance_list_mangement_new_version"
---

DBW is a unified cloud management platform for lifecycle management of multiple types of databases. The DBW instance list (new version) centrally manages database instances of types including RDS for MySQL, NDB for MySQL,Cache for Redis, Document Database for MongoDB, RDS for PostgreSQL, and RDS for SQL Server.

<span id="57R0qqeD"></span>
## Function introduction

The old version of the instance list displays database instances of a certain type on\-demand according to the database type. The new version of the instance list displays all types of database instances but also supports filtering by database type. There is a slight difference in management concepts between the two, but their functions are completely consistent. You can switch between the new and old versions of the instance list as needed in the upper right corner. The differences between the new and old instance lists are as follows.


| |**New version** |**Old version** |
|---|---|---|
|Database type |Unified management of all types of instances, displaying instance information of all database types in the instance list. |Manage instances according to database type, that is, only one type of database instance can be displayed in the instance list at the same time. Due to differences in database types, the fields in the instance list vary. |
|Synchronize instance information |Scheduled |Real time |
|Supported function |Same |Same |


<span id="CCiQ5hwF"></span>
## **Prerequisites**

Instances of the related database types have been created, as follows.


* To create an RDS for MySQL instance, see [Create MySQL instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* To create an NDB for MySQL instance, see [Create NDB for MySQL instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1).

* To create an RDS for PostgreSQL instance, see [Create PostgreSQL instance](https://docs.byteplus.com/en/docs/RDS_for_PG/create_instance).

* To create an RDS for SQL Server instance, see [Create SQL Server instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide).

* To create a Cache for Redis instance, see [Create Redis instance](https://docs.byteplus.com/en/docs/redis/create-instance).

* To create a Document Database for MongoDB instance, see [Create MongoDB instance](https://docs.byteplus.com/en/docs/mongodb/create-instance).


<span id="2xdgPo5y"></span>
## Precautions


* Automatic synchronization mechanism: DBW automatically synchronizes instance information from various database types at regular intervals.

* Status Indicator Description: A red badge on the Sync Instance Information button indicates that new instances have been added or changes have occurred to existing instance information.

* Manual synchronization: Click the **Synchronize instance information** button to actively trigger synchronization. Synchronization is asynchronous. You must manually refresh the instance list to view the latest data after it completes.

* Handling abnormal instances: An abnormal status indicates that the instance is currently unreachable. If you confirm that the instance has been decommissioned or is no longer in use, you can delete it directly from the DBW instance list.

* Security control: Currently supports enabling security control for the following database instances.

   * Relational databases: RDS for MySQL, NDB for MySQL, RDS for PostgreSQL, and RDS for SQL Server

   * Non\-relational databases: Document Database for MongoDB and Cache for Redis

* Automatic inspection and inspection weight configuration

   * Automatic inspection: supports enabling automatic inspection for instances including RDS for MySQL, NDB for MySQL, RDS for PostgreSQL, and Cache for Redis.

   * Automatic inspection weight: supports setting custom inspection weights for database instances including RDS for MySQL, NDB for MySQL, and RDS for PostgreSQL.

* Session and transaction snapshots

   * Session snapshot: supports enabling session snapshots for instances including RDS for MySQL, NDB for MySQL, RDS for PostgreSQL, and Document Database for MongoDB.

   * Transaction and lock: supports enabling transaction and lock snapshots for database instances including RDS for MySQL, NDB for MySQL, and RDS for PostgreSQL.

* Slow log diagnosis: supports enabling slow log diagnosis for database instances including RDS for MySQL and NDB for MySQL.


<span id="34gWGczn"></span>
## **Procedure**


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, click **Instance list**.

3. On the top menu bar, select the project and region.

4. On the **Instance list** page, click the **Connection normal** tab, where you can perform the following operations.

   You can search for the target instance by instance ID or instance name in the upper right corner of the **Instance list** page, or filter instances that meet the criteria by **Database type**, **Security control**, or **Automatic inspection**.

   
   |**Actions** |**Description** |
   |---|---|
   |View instance information<br><br> |In the instance list, you can view information such as the last update time of the instance list, instance name/ID, database type, security control, automatic inspection, primary node availability zone, instance type, database version, owning project, creation time, and status in DBW.<br><br>The fields in the instance list support customization, so the fields displayed in the list may vary. |
   |Synchronize instance information |Click **Synchronize instance information**, then refresh the instance list later to obtain the latest information for all instances. When a red marker appears in the upper\-right corner of the Connection normal tab, it indicates new instances have been added or existing instance information has changed. It is recommended to update the instance list promptly to obtain the latest instance information. |
   |Customize list fields |In the upper right area of the list, click **Customize list fields** to customize and select the fields to be displayed in the list.<br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_02f58f50db66135c1b4694cf1d2c4314.png) </span><br><br><br>* The default resources in the instance list include **Instance name/ID**, **Database type**, **Security control**, **Automatic inspection**, **Primary node availability zone**, **Instance type**, **Database version**, **Projects**, **Creation time**, and **Status in DBW**.<br><br>* Grayed\-out fields indicate non\-editable fields. |
   |&nbsp;<br><br>Enabling security control |DBW supports unified management of database instances. Enabling security control allows database changes to go through a ticket approval workflow, simplifying and standardizing database management operations and improving data management processes. For specific operations and precautions for enabling security control, please refer to the enable security control features of the respective databases below.<br><br><br>* [Enable security control for RDS for MySQL](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql)<br><br>* [Enable security control for NDB for MySQL](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control)<br><br>* [Enable security control for RDS for PostgreSQL](https://docs.byteplus.com/en/docs/DBW/enabling-security-control)<br><br>* [Enable security control for RDS for SQL Server](https://docs.byteplus.com/en/docs/DBW/enabling-security-control_)<br><br>* [Enable security control for Document Database for MongoDB](https://docs.byteplus.com/en/docs/DBW/MongoDB_Enabling_security_control)<br><br>* [Enable security control for Redis databases](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-redis?lang=zh) |
   |Enable automatic inspection |DBW provides a database inspection feature that performs regular automated health checks and risk assessments on database instances, helping you understand their operational status. For specific steps and considerations on enabling automatic instance inspection, refer to the inspection management function of the respective databases below.<br><br><br>* [Enable automatic inspection for RDS for MySQL](https://docs.byteplus.com/en/docs/DBW/database-inspection-management-for-mysql)<br><br>* [Enable automatic inspection for NDB for MySQL](https://docs.byteplus.com/en/docs/DBW/Database_inspection_management)<br><br>* [Enable automatic inspection for RDS for PostgreSQL](https://docs.byteplus.com/en/docs/DBW/database-inspection-management)<br><br>* [Enable automatic inspection for Cache for Redis](https://docs.byteplus.com/en/docs/DBW/Redis_database_inspectioin_management) |
   |Customize inspection weight |By default, DBW sets the weight of each score deduction item of all instance nodes to Medium. It also supports modifying the weight of each score deduction item based on business requirements.<br><br><br>* [Customize inspection weights for RDS for MySQL](https://docs.byteplus.com/en/docs/DBW/database-inspection-management-for-mysql)<br><br>* [Customize inspection weights for NDB for MySQL](https://docs.byteplus.com/en/docs/DBW/Database_inspection_management)<br><br>* [Customize inspection weights for RDS for PostgreSQL](https://docs.byteplus.com/en/docs/DBW/database-inspection-management) |
   |Enable slow log diagnosis |DBW provides a slow log diagnosis feature, which analyzes the Top 200 slow logs generated on the previous day and offers diagnostic results and optimization suggestions to help improve database performance and stability. For specific operations and precautions on enabling slow log diagnosis, refer to the following Document.<br><br><br>* [Enable slow log diagnosis for RDS for MySQL](https://docs.byteplus.com/en/docs/DBW/Slow_log_diagnosis_management)<br><br>* [Enable slow log diagnosis for NDB for MySQL](https://docs.byteplus.com/en/docs/DBW/Slow_log_diagnosis) |
   |Enable session snapshot |DBW provides session snapshot and transaction and lock snapshots features, which can collect session and transaction and lock related information of the instance at certain frequencies. For detailed operations and precautions for enabling session snapshots or transaction and lock snapshots, refer to the session management or transaction and lock management features of the respective databases below.<br><br><br>* [Enable snapshot for RDS for MySQL](https://docs.byteplus.com/en/docs/DBW/session-information-management-for-mysql#SvVMQUkB)<br><br>* [Enable snapshot for NDB for MySQL](https://docs.byteplus.com/en/docs/DBW/Session_information_management)<br><br>* [Enable snapshot for RDS for PostgreSQL](https://docs.byteplus.com/en/docs/DBW/session-management)<br><br>* [Enable snapshot for Document Database for MongoDB](https://docs.byteplus.com/en/docs/DBW/MongDB_Session_management) |
   |Log on to the data interaction platform |Click **Log in** in the actions column of the target instance to log in to the instance's data interaction platform. On the data interaction platform, i.e., the SQL window, you can execute various SQL statements and manage databases/table structures.<br><br><br>* [Logging in to the data interaction platform (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql)<br><br>* [Logging in to the data interaction platform (NDB for MySQL)](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql)<br><br>* [Logging in to the data interaction platform (RDS for PostgreSQL)](https://docs.byteplus.com/en/docs/DBW/log-in-database-interaction-platform-for-PG)<br><br>* [Logging in to the data interaction platform (Cache for Redis)](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-cache-for-redis)<br><br>* [Logging in to the data interaction platform (RDS for SQL Server)](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-rds-for-sql-server)<br><br>* [Logging in to the data interaction platform (Document Database for MongoDB)](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-documentdb-for-mongodb) |
   |Log in to the Operation observability page |Click **Operations observability** in the Actions column of the target instance, or click the target instance's **Instance name/ID**, to view and manage session statistics, slow log analysis, auditing, and other features for that instance. |
   |View instance details |Click **Instance details** in the actions column of the target instance to navigate to the instance information page of the instance.<br><br><br>* [View RDS for MySQL instance details](https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_instance_details)<br><br>* <br><br>* [View NDB for MySQL instance details](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Viewing_instance_details)<br><br>* [View RDS for PostgreSQL instance details](https://docs.byteplus.com/en/docs/RDS_for_PG/viewing_the_details_of_an_instance)<br><br>* [View Cache for Redis instance details](https://docs.byteplus.com/en/docs/redis/view-instance)<br><br>* [View Document Database for MongoDB instance details](https://docs.byteplus.com/en/docs/mongodb/view-instance)<br><br>* [View RDS for SQL Server instance details](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/viewing-instance-details) |
   

5. On the **Instance list** page, click the **Access exception **  tab, where you can perform the following operations.

   Supports searching for the target instance by instance ID or instance name in the upper right corner of the **Instance list** page.

   
   |**Actions** |**Description** |
   |---|---|
   |View instance information |In the instance list, you can view information such as the last update time of the instance list, instance name/ID, database type, security control, automatic inspection, primary node availability zone, instance type, database version, owning project, creation time, tags, and status in DBW.<br><br>The fields in the instance list support customization, so the fields displayed in the list may vary. |
   |Synchronize instance information |Click **Synchronize instance information**, then refresh the instance list later to obtain the latest information for all instances. If a red marker appears in the upper\-right corner of the Access exception tab, it indicates instances that cannot be connected (e.g., deleted instances or network issues). It is recommended to update the instance list promptly to obtain the latest instance information. |
   |Delete instance |Click **Delete** in the actions column of the target instance, and confirm to delete the instance from the DBW instance list.<br><br>Deleting an instance from the DBW instance list will not remove the instance from its database instance list. |
