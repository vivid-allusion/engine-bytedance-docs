---
title: "Database Workshop"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Database_Workshop"
---

Database Workshop (DBW) is a unified cloud management platform for managing the lifecycle of multiple types of databases. DBW is a database SaaS product that integrates a graphical user interface (GUI), troubleshooting, and auditing. It provides web endpoint management capabilities such as comprehensive observation and analysis, intelligent risk checks, and autonomous operations. It provides a stable, secure, and efficient cloud service for database management. RDS for MySQL is integrated with Database Workshop (DBW), embedding DBW features such as slow log analysis, audit log, SQL throttling, tickets, database inspection, and autonomous operation into the RDS for MySQL console.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If your instance does not have the <strong>Database Workshop</strong> menu, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> to contact technical support to upgrade the instance.</div>


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limitation


* Slow log analysis, audit log, and SQL throttling are only available to enterprise users.

* The DBW features embedded in the RDS for MySQL console may have limitations. For full functionality, refer to the [Feature introduction](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Database_Workshop#.5Yqf6IO95LuL57uN) and use the DBW console.

* You need to grant relevant permissions of DBW to your account.


<span id=".5Yqf6IO95LuL57uN"></span>
## Function introduction


* **Logs**

   View details of slow logs and error logs for an instance. You can also diagnose slow logs, view trends, statistics, and details of slow queries, and further analyze slow log information to quickly identify problems. For more information, refer to [Logs](https://docs.byteplus.com/en/docs/DBW/Log_management-?lang=en).

* **Session management**

   Session management capabilities enable viewing session statistics and real\-time session information for instances. For more information, refer to [Session management](https://docs.byteplus.com/en/docs/DBW/session-information-management-for-mysql?lang=en).

* **Database audit**

   Database audit The database audit function records all operation records, making it easy for you to trace back, query and analyze historical operations, helping you to keep track of product security and performance and improve database security. For more information, refer to [Database audit management](https://docs.byteplus.com/en/docs/DBW/database-audit-management-for-mysql?lang=en).

* **SQL throttling**

   SQL throttling controls the volume of database requests and SQL concurrency to ensure service availability. For more information, refer to [SQL throttling](https://docs.byteplus.com/en/docs/DBW/preview-sql-throttle-task-management-for-mysql).

* **Database inspection**

   Database inspection provides regular, automated health checks and risk assessments for database instances, helping you understand their operational status. For more information, refer to [Database inspection management](https://docs.byteplus.com/en/docs/DBW/database-inspection-management-for-mysql).

* **Ticket list**

   DBW uses tickets to provide unified management of database instances. It supports collaborative management through multiple roles, such as system roles and ticket approval roles, to simplify and standardize database management operations and improve data management efficiency. For more information, refer to the [Ticket list](https://docs.byteplus.com/en/docs/DBW/ticket-list-for-mysql).

* **Automatic operation**

   You can configure operation rules to automatically scale the node specification and storage space for a MySQL instance or to automatically create indexes. It helps you dynamically adjust CPU and storage resources based on your business needs and automatically generates index creation suggestions when slow SQL is diagnosed. For more information, refer to [Automatic operation](https://docs.byteplus.com/en/docs/DBW/AutoOps_management?lang=en).

* **Spatial analysis**

   The spatial analysis function allows you to intuitively view the storage space usage of an instance, such as data space, log space, etc. For more information, refer to [Spatial analysis management](https://docs.byteplus.com/en/docs/DBW/spatial-analysis-management-for-mysql?lang=en).

* **Diagnosis**

   Through the diagnostic function, you can more intuitively view the full picture of database performance and quickly confirm whether there are any abnormalities in the instance. For more information, refer to [One-click diagnosis management](https://docs.byteplus.com/en/docs/DBW/one-click-diagnostics-management-for-mysql).

* **Full SQL insight**

   Full SQL insights enable you to capture, review, and analyze all SQL statements to help you improve database performance and stability. For more information, refer to [SQL insight and audit management](https://docs.byteplus.com/en/docs/DBW/full-SQL-explorer?lang=en).

* **Performance monitoring**

   Provides a wealth of performance monitoring metrics. With these metrics, you can view the performance trends of your database instances and identify possible risks in your database instances in a timely manner. For more information, refer to [Performance monitoring](https://docs.byteplus.com/en/docs/6956/1986074?lang=en).

* **Transactions and locks**

   With the transactions and locks feature, you can view and analyze all locks that occur within an instance of RDS for MySQL. For more information, refer to [Transaction and lock management](https://docs.byteplus.com/en/docs/DBW/lock-analysis-management-for-mysql?lang=en).


<span id="gomdSI7S"></span>
## Usage


1. Login the DBW console.

   1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql), click the target instance name on the **Instances List** page to enter the instance details page, and then click **Database Workshop** in the upper‑right corner of the page to enter the DBW console.

   * Login directly to [Database Workshop](https://console.byteplus.com/dbw).

2. Use the corresponding functions in DBW.
