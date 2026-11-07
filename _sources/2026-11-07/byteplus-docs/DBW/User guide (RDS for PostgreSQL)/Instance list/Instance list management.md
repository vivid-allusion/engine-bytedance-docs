---
title: "Instance list management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/instance-list-management-for-postgresql"
---

This topic describes how to view information about the status, availability zone, instance specifications, version, tags, and the ID, node specifications, and availability zone of read\-only nodes for an RDS for PostgreSQL instance on the instance list page of the DBW console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An instance for RDS for PostgreSQL has been created, and the instance status is running. For detailed steps, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/create_instance).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, click **Instance list**.

3. On the top menu bar, select the project and region.

4. On the **Instance list** page, set the **Database type** filter to **RDS for PostgreSQL**. Alternatively, you can query for the target instance by its **Instance list** page, using the instance ID or instance name.

5. On the **Instance list** page, you can perform the following operations.

   
   |**Actions** |**Description** |
   |---|---|
   |View instance information |In this area, you can view information such as the last update time of the instance list, instance name/ID, state, primary node availability zone, instance specification, database version, owning project, and tags.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the instance has created read\-only nodes, you can also view the read\-only node ID, node specifications, availability zone, tags, and other information.</div><br> |
   |Enable automatic inspection |DBW provides a database inspection feature that performs regular automated health checks and risk assessments on database instances, helping you understand their operational status. For specific steps and considerations on enabling automatic instance inspection, refer to [Enabling automatic inspection](https://docs.byteplus.com/en/docs/DBW/database-inspection-management). |
   |Enabling security control |DBW enables centralized management of database instances. Enabling security control allows database changes to go through a ticket approval process, simplifying and standardizing database management while improving data management workflows. For specific steps and considerations on enabling security control, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/enabling-security-control). |
   |Enable session snapshot |DBW provides session snapshot and transaction and lock snapshot features. These features can collect session and transaction and lock related information of instances at certain frequencies. For specific steps and considerations on enabling session snapshot or transaction and lock snapshots, refer to [snapshot](https://docs.byteplus.com/en/docs/DBW/session-management#g9LUJw4G) [snapshot](https://docs.byteplus.com/en/docs/DBW/session-management#g9LUJw4G) [snapshot](https://docs.byteplus.com/en/docs/DBW/session-management#g9LUJw4G) or [enable or disable transaction and lock snapshots](https://docs.byteplus.com/en/docs/DBW/transaction-and-lock-management). |
   |Log on to the data interaction platform |Click **Log in** to log in to the data interaction platform of RDS for PostgreSQL. On the data interaction platform, i.e., the SQL window, you can execute various SQL statements and manage databases/table structures. For more information, refer to [Logging on to the data interaction platform (RDS for PostgreSQL)](https://docs.byteplus.com/en/docs/DBW/log-in-database-interaction-platform-for-PG). |
   |Log in to the Operation observability page |* Click **Operations observability** in the **Actions** column of the target instance to log in to the operations observability page, and view and analyze slow logs and other functions of the corresponding instance.<br><br>* Click **Slow log analysis** in the **Actions** column of the read\-only node to log in and view the slow log analysis function of the corresponding read\-only node. |
   |View instance details |Click **Instance details** to navigate to the instance information page of the target instance. For more information on the instance, refer to [Viewing an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/viewing_the_details_of_an_instance). |
   |Set inspection weight |Click **Set inspection weight** to assign weights to each deduction item for individual instance nodes. For specific steps and considerations on setting inspection weights, refer to [Database inspection management](https://docs.byteplus.com/en/docs/DBW/database-inspection-management).<br><br> |
