---
title: "Log management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/log-management"
---

Database Workshop DBW provides the slow log management feature for RDS for SQL Server instances. This feature helps you quickly identify inefficient SQL statements, detect performance bottlenecks, optimize database query performance, and ensure stable system operation. This topic describes how to manage the slow logs of an RDS for SQL Server instance in the Database Workshop DBW console.

<span id="dWcw5oYe"></span>
## Prerequisites


* An instance has been created and the instance state is Running. For detailed steps, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide?lang=en).

* If the target instance has security control enabled, you need to apply for operation and maintenance read\-only or read/write permissions for the current account. For more information, refer to [Enabling instance security control ( RDS for SQL Server)](https://docs.byteplus.com/en/docs/DBW/enabling-security-control_), and [Applying for operation permissions ( RDS for SQL Server)](https://docs.byteplus.com/en/docs/DBW/creating-an-operation-permission-ticket_).


<span id="IX0u6kLq"></span>
## Precautions


* Currently, you cannot directly enable the slow log for an SQL Server instance in the DBW console. Go to the instance management page and manually enable slow logs to use this feature. For detailed steps, see [Enable slow logs](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/enabling-slow-log?lang=en).

* Currently, only slow logs from the primary node are supported, and the query results show up to the first 100 records from a maximum of 2 log files.

* By default, slow log information from the past 10 minutes is displayed.

* You can view slow log data for up to the past 30 days, with a maximum query time span of 7 days.

* When filtering to view slow SQL queries within a certain period, the query end time must be later than the start time.

* A single download supports up to 100 log entries.


<span id="9upmnyYz"></span>
## Query a slow log


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, switch the instance type and ID.

   1. In the upper right corner of the **Observation and diagnosis** page, switch the instance type to RDS for SQL Server.

   2. In the upper left corner of the **Observation and diagnosis** page, switch the target instance based on the instance ID or instance name.

5. On the **Observation and diagnosis** page, click **Log management**.

6. On the **Log management** page, filter by the required time frame, then view the slow log details.

   When selecting a query time frame, the query end time must be later than the query start time.

   
   <Tabs>
   <Tab zoneid="Am8B2KCcvZ" title="Filter slow logs">
   <TabTitle>Filter slow logs</TabTitle>
   
   Click **Advanced filtering**. In the expanded filter area, configure the following parameters as needed, and then click **Query**.
   
   
   * **Database name**: Enter the target database in the input box, then press Enter. Multiple databases can be entered at once.
   
   * **Executing user**: Enter the target user in the input box, then press Enter. Multiple executing users can be entered at once.
   
   * **IP source**: Enter multiple target IPs in the input box, then press Enter. Multiple IP addresses can be entered at once.
   
   
   </Tab>
   <Tab zoneid="WOOhIcEqST" title="View slow SQL list">
   <TabTitle>View slow SQL list</TabTitle>
   
   In the **Slow SQL list** area, you can view information for each SQL, as detailed below:
   
   
   * **Execution completion time**: The specific time when this SQL statement finished executing on the database server. Combined with the **Execution time**, you can calculate its start time to accurately pinpoint performance issues during peak business hours or at specific times.
   
   * **SQL**: The content of the actual SQL statement executed, which can be copied.
   
   * **Database**: The specific database (Schema) where this SQL statement was executed, helping to quickly identify the affected business database.
   
   * **IP source**: The IP address of the client machine that initiated the SQL request. This field quickly identifies which application server, developer's computer, or even which non\-compliant script is frequently calling slow SQL.
   
   * **Application name**: The name of the application that initiated the request (typically specified in the database connection configuration). It directly indicates which business system (such as "Order Service" or "Backend Reporting System") generated the slow query.
   
   * **Executing user**: The database account that executed the SQL. Used to determine which business account or operation personnel is performing the operation, helping to troubleshoot permission misuse or specific business logic issues.
   
   * **Execution time (s)** : The total duration from the start to the completion of SQL execution, measured in seconds. The most direct criterion for determining whether an SQL is slow. It includes the total time for all steps such as CPU computation, disk I/O, lock waits, and network transmission.
   
   * **Rows affected**: The number of data rows actually affected after executing the SQL (e.g., the number of rows actually modified by UPDATE or DELETE, or the number of rows ultimately returned by SELECT). A large number of affected rows may lead to significant log writing or network transmission pressure.
   
   * **CPU time**: The time the CPU actually spent on computation (such as parsing, condition evaluation, function operations, etc.) while the database was executing the SQL. If **CPU time** is close to **Execution time**, it indicates that the executed SQL is compute\-intensive (with complex logic). If there is a significant difference, it suggests that the time is mainly spent waiting for I/O or locks.
   
   * **Total logical reads**: The total number of data blocks read by the database from the memory buffer pool to execute the SQL. It is a key metric for measuring the amount of data scanned by SQL and the memory/CPU consumption.
   
   * **Total I/O writes**: The total number of data blocks written to the disk during SQL execution. Operations that modify data, such as INSERT, UPDATE, and DELETE, or processes that generate a large number of disk temporary tables or sorting files, can result in high I/O writes.
   
   
   </Tab>
   </Tabs>
   


<span id="CRW4vj8c"></span>
## Download a slow log

A single download supports up to 100 log entries.


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, switch the instance type and ID.

   1. In the upper right corner of the **Observation and diagnosis** page, switch the instance type to RDS for SQL Server.

   2. In the upper left corner of the **Observation and diagnosis** page, switch the target instance based on the instance ID or instance name.

5. On the **Observation and diagnosis** page, click **Log management**.

6. On the **Log management** tab, click the download icon.

7. In the **Export** dialog box, select the information to include in the slow log download as needed.


The current slow log download can include **Execution completion time**, **SQL**, **Database**, **IP source**, **Application name**, **Executing user**, **Execution time (s)** , **Rows affected**, **CPU time**, **Total logical reads**, and **Total I/O writes**.


8. Click **OK**.
