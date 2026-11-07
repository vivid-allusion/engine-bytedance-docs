---
title: "Instance list management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/instance-list-management-for-mysql"
---

This topic explains how to view the status, CPU and memory usage of target instances, as well as detailed information about read\-only nodes within instances on the instance list page.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**

An instance for RDS for MySQL has been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure**


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, click **Instance list**.

3. On the top menu bar, select the project and region.

4. On the **Instance list** page, filter by **Database type** as **RDS for MySQL**. You can also query the target instance by **Instance ID** Or **Instance name** in the upper\-left corner of the **Instance list** page.

5. On the **Instance list** page, you can perform the following operations.

   
   |**Actions** |**Description** |
   |---|---|
   |View instance information |In this area, you can view the latest update time of the instance list, instance name/ID, state, primary node availability zone, instance specification, database version, owning project, tags, and information such as read\-only node ID, node specification, and availability zone. |
   |Enabling security control |DBW enables centralized management of database instances. Enabling security control allows database changes to go through a ticket approval process, simplifying and standardizing database management while improving data management workflows. For specific steps and considerations on enabling security control, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql). |
   |Enable automatic inspection |DBW provides a database inspection feature that performs regular automated health checks and risk assessments on database instances, helping you understand their operational status. For specific steps and considerations on enabling automatic instance inspection, refer to [Database inspection management](https://docs.byteplus.com/en/docs/DBW/database-inspection-management-for-mysql). |
   |Enable slow log diagnosis |DBW provides a slow log diagnosis feature, which analyzes the Top 200 slow logs generated on the previous day and offers diagnostic results and optimization suggestions to help improve database performance and stability. For specific steps and considerations on enabling slow log diagnosis for instances, refer to [Slow log diagnosis.](https://docs.byteplus.com/en/docs/DBW/Slow_log_diagnosis_management) |
   |Enable session snapshot |DBW provides session snapshot and transaction and lock snapshot features. These features can collect session and transaction and lock related information of instances at certain frequencies. For specific steps and considerations on enabling session snapshot or transaction and lock snapshots, refer to [snapshot](https://docs.byteplus.com/en/docs/DBW/session-information-management-for-mysql#SvVMQUkB) [snapshot](https://docs.byteplus.com/en/docs/DBW/session-information-management-for-mysql#SvVMQUkB) [snapshot](https://docs.byteplus.com/en/docs/DBW/session-information-management-for-mysql#SvVMQUkB) or [snapshots](https://docs.byteplus.com/en/docs/DBW/lock-analysis-management-for-mysql) [snapshots](https://docs.byteplus.com/en/docs/DBW/lock-analysis-management-for-mysql) [snapshots](https://docs.byteplus.com/en/docs/DBW/lock-analysis-management-for-mysql). |
   |Log on to the data interaction platform |Click **Log in** to access the data interaction platform for RDS for MySQL. On the data interaction platform, i.e., the SQL window, you can execute various SQL statements and manage databases/table structures. For more information, refer to [Logging on to the data interaction platform (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql). |
   |Log in to the Operation observability page |Click **Operation observability** to log in and access features such as session statistics, slow log analysis, and auditing for the corresponding instance. |
   |View instance details |Click **Instance details** to navigate to the instance information page of the target instance. For more information on the instance, refer to [Viewing an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_instance_details). |
   |Set inspection weight |Click **Set inspection weight** to assign weights to each deduction item for individual instance nodes. For specific steps and considerations on setting inspection weights, refer to [Database inspection management](https://docs.byteplus.com/en/docs/DBW/database-inspection-management-for-mysql). |
