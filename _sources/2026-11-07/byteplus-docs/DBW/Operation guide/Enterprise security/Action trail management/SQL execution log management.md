---
title: "SQL execution log management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/SQL_execution_log_management"
---

The Database Workshop (DBW) provides the SQL execution log function, which can record all SQL operation records, including those in the Database interaction console and tickets.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* DBW Administrators can view all operation behaviors.

* Non\-DBW roles, i.e., normal users or non\-DBW roles, only support viewing their own operation behaviors.

* SQL execution logs are reserved for 30 days by default.


<span id=".5LyY5Yq_"></span>
## Advantages


* **Improve data security**: View all operations on database data in real time, including insert, update, delete, and query, and detect and block anomaly behaviors in time. At the same time, it can also prevent and track all improper data tampering behaviors.

* **Increase operation transparency**: Operation audit records all User operations in the Database in detail, which can provide a complete User activity trail and increase operation transparency. At the same time, you can also analyze the operation logs to identify and understand business operating inertia to optimize database management.


<span id=".5pON5L2c6K6w5b2V"></span>
## Operation record


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the target region.

3. In the left navigation bar, choose **Corporate security** \> **Operation audit**.

4. On the **Operation audit** page, click SQL execution log.

5. On the **SQL execution log** tab, view the following information:

   The **Select search type** input box supports filtering operation records by **Operation time**, **Username**, **User ID**, **Operation type**, **Database type**, **Instance ID**, etc.

   
   <Tabs>
   <Tab zoneid="vaCF4FktKo" title="Data interaction platform">
   <TabTitle>Data interaction platform</TabTitle>
   
   In the **Data interaction platform** subtab, you can view all operation records for all database types in the data interaction platform, including **Operation time**, **Username**, **Operation type**, **Database type**, **Instance ID**, **Database name**, **SQL statement**, **SQL type**, **Execution status**, **Rows affected**, and **Execution time (ms)** .
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   <div data-tips="true" data-tips-type="default">You can click the copy button after the SQL statement to copy the SQL statement executed in the data interaction platform or the SQL result set statement exported in the data interaction platform.</div>
   
   
   <div data-tips="true" data-tips-type="default">Data import/export in the data interaction platform: During data import, you can click the copy button in the <strong>SQL statement</strong> column to download the uploaded table.</div>
   
   
   <div data-tips="true" data-tips-type="default">Database type includes RDS for MySQL, NDB for MySQL, RDS for SQL Server, RDS for PostgreSQL, Cache for Redis and Document Database for MongoDB.</div>
   
   
   
   </Tab>
   <Tab zoneid="GZN9F0Ntha" title="Data change ticket">
   <TabTitle>Data change ticket</TabTitle>
   
   On the **Data change ticket** subtab, you can view all operation records of data change tickets, including **Operation time**, **Username**, **Ticket ID**, **Ticket status**, **Ticket type**, **Instance ID**, and **Database name**.
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   <div data-tips="true" data-tips-type="default">You can click the ID of the target ticket to view the ticket details.</div>
   
   
   <div data-tips="true" data-tips-type="default">You can view the operation records of data change tickets, including RDS for MySQL, NDB for MySQL, and RDS for PostgreSQL.</div>
   
   
   
   </Tab>
   <Tab zoneid="uCAkO6N3ba" title="Clear table ticket">
   <TabTitle>Clear table ticket</TabTitle>
   
   On the **Clear table ticket** sub tab, you can view all operation records of clear table tickets, including **Operation time**, **Username**, **Ticket ID**, **Ticket status**, **Instance ID**, and **Database name**.
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   <div data-tips="true" data-tips-type="default">You can click the ID of the target ticket to view the ticket details.</div>
   
   
   <div data-tips="true" data-tips-type="default">Operation records of clear table tickets for RDS for MySQL and NDB for MySQL database instances can be viewed.</div>
   
   
   
   </Tab>
   <Tab zoneid="ACGPKOfiJ8" title="Data cleanup and archiving ticket">
   <TabTitle>Data cleanup and archiving ticket</TabTitle>
   
   On the **Data cleanup and archiving ticket** sub\-tab, you can **View** all operation records of the data cleanup and archiving ticket, including **Operation time**, **Username**, **Ticket ID**, **Ticket status**, **Instance ID**, and **Database name**.
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   <div data-tips="true" data-tips-type="default">You can click the ID of the target ticket to view the ticket details.</div>
   
   
   <div data-tips="true" data-tips-type="default">You can view the operation records of data cleanup and archiving tickets for database instances of RDS for MySQL and NDB for MySQL.</div>
   
   
   
   </Tab>
   <Tab zoneid="Npu6AnPRam" title="Data import and export ticket">
   <TabTitle>Data import and export ticket</TabTitle>
   
   On the **Data import and export ticket** sub\-tab, you can view all operation records of the data import and export tickets, including **Operation time**, **Username**, **Ticket ID**, **Ticket status**, **Instance ID**, and **Database name**.
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   <div data-tips="true" data-tips-type="default">You can click the ID of the target ticket to view the ticket details.</div>
   
   
   <div data-tips="true" data-tips-type="default">You can view the operation records of data import/export tickets for database instances of RDS for MySQL and NDB for MySQL.</div>
   
   
   
   </Tab>
   </Tabs>
