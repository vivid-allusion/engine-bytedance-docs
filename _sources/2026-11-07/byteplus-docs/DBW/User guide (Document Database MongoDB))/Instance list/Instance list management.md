---
title: "Instance list management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/instance-list-management"
---

Database Workshop (DBW) supports the connection to Document Database for MongoDB instances. This topic describes how to view the status, primary node availability zone, instance type, instance specification for the target instance on the instance list page of the DBW console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An instance for Document Database for MongoDB has been created. For detailed steps, see [Creating an instance](https://docs.byteplus.com/en/docs/mongodb/create-instance).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, click **Instance list**.

3. On the top menu bar, select the project and region.

4. On the **Instance list** page, switch the instance type and ID.

   1. In the **Instance list** page, switch the database type to **Document Database for MongoDB**.

   2. On the **Instance list** page, search for the target instance by Instance ID or Instance name.

5. On the **Instance list** page, you can perform the following operations.

   
   |**Actions** |**Description** |
   |---|---|
   |**View instance information** |In this area, you can View information such as the instance list's last updated at, instance name/ID, instance state, primary node availability zone, instance type, instance specification, database version, owning project, and tags. |
   |**Enabling security control** |DBW enables centralized management of database instances. Enabling security control allows database changes to go through a ticket approval process, simplifying and standardizing database management while improving data management workflows. For specific steps and considerations on enabling security control, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/MongoDB_Enabling_security_control). |
   |**Enable session snapshot** |DBW provides the session snapshot feature, which can collect session information of instances at a certain frequency. For detailed operations and notes on enabling session snapshot, refer to [Enable or disable session snapshot](https://docs.byteplus.com/en/docs/DBW/MongDB_Session_management#bOXdLDIz). |
   |**Log on to the data interaction platform** |Click **Log in** to access the data interaction platform for Document Database for MongoDB. On the data interaction platform, i.e., the SQL window, you can execute various SQL statements and manage databases/table structures. For more information, refer to Logging on to the data interaction platform (Document Database for MongoDB). |
   |**Log in to the Operation observability page** |Click **Operation observability** to log in and access features such as session information, performance monitoring and database audit logs for the corresponding instance. |
   |**View instance details** |Click **Instance details** to navigate to the instance information page of the target instance. For more information on the instance, refer to [Viewing an instance](https://docs.byteplus.com/en/docs/mongodb/view-instance). |
