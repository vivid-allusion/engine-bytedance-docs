---
title: "Instance list management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/instance-list-management_"
---

Database Workshop (DBW) supports the connection to RDS for SQL Server instances. This topic describes how to view the status, primary node availability zone, instance type, instance specification, and read\-only instance details for the target instance on the instance list page of the DBW console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An instance has been created and the instance state is Running. For detailed steps, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide).

<span id=".5pON5L2c5q2l6aqk"></span>
## Precautions

DBW currently supports SQL Server 2019/2022 Standard Edition, SQL Server 2019/2022 Web Edition, and SQL Server 2019/2022 Enterprise Edition instances.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, click **Instance list**.

3. On the **Instance list** page, switch the instance type and ID.

   1. On the **Instance list** page, switch the database type to **RDS for SQL Server**.

   2. In the upper\-right corner the **Instance list** page, search for the target instance by instance ID or instance name.

4. On the **Instance list** page, you can perform the following operations.

   
   |**Actions** |**Description** |
   |---|---|
   |**View instance information** |In this region, you can view information such as the last update time of the instance list, the name and ID of the instance and read\-only instances, instance state, primary node availability zone, instance type, instance specification, database version, owning project, and tags. |
   |**Enabling security control** |DBW enables centralized management of database instances. Enabling security control allows database changes to go through a ticket approval process, simplifying and standardizing database management while improving data management workflows. For specific steps and considerations on enabling security control, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/enabling-security-control_). |
   |**Log on to the data interaction platform** |Click **Log in** to access the data interaction platform for RDS for SQL Server. On the data interaction platform, i.e., the SQL window, you can execute various SQL statements and manage databases/table structures. For more information, refer to[ Logging on to the data interaction platform (RDS for SQL Server)](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-rds-for-sql-server). |
   |**Log in to the Operation observability page** |Click **Operation observability** to log in and access features such as performance monitoring for the corresponding instance. |
   |**View instance details** |Click **Instance details** to navigate to the instance information page of the target instance. For more information on the instance, refer to [Viewing an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/viewing-instance-details). |
