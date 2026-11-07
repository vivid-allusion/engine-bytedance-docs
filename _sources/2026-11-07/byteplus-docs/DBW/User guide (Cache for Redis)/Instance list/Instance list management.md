---
title: "Instance list management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/instance-list-management-for-redis"
---

This topic describes how to view detailed information such as the status, primary node availability zone, and instance specification of the target instance on the instance list page.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**

An instance for Cache for Redis has been created, and the instance status is running. For detailed steps, see [Creating an instance](https://docs.byteplus.com/en/docs/redis/create-instance).

<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure**


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, click **Instance list**.

3. On the top menu bar, select the project and region.

4. In the **Instance list** page, switch the **Database type** to **Cache for Redis**. Additionally, you can search for target instances by instance ID or name in the **Instance list** page.

5. On the **Instance list** page, you can perform the following operations.

   
   |**Actions** |**Description** |
   |---|---|
   |View instance information |In this section, you can view information such as the last update time of the instance list, instance name/ID, status, primary node availability zone, instance specification, database version, owning project, and tags. |
   |Enable automatic inspection |DBW provides a database inspection feature that performs regular automated health checks and risk assessments on database instances, helping you understand their operational status. For specific steps and considerations on enabling automatic instance inspection, refer to Database inspection management. |
   |Log on to the data interaction platform |Click **Log in** to access the data interaction platform for Cache for Redis. On the data interaction platform, i.e., the SQL window, you can execute various SQL statements and manage databases/table structures. For more information, refer to [Logging on to the data interaction platform (Cache for Redis)](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-cache-for-redis). |
   |Log in to the Operation observability page |Click **Operation observability** to log in and access features such as bandwidth auto\-scaling for the corresponding instance. |
   |View instance details |Click **Instance details** to navigate to the instance information page of the target instance. For more information on the instance, refer to [Viewing an instance](https://docs.byteplus.com/en/docs/redis/view-instance). |
