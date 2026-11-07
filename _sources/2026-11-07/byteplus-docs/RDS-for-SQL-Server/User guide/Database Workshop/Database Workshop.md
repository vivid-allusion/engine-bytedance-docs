---
title: "Database Workshop"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/Database_Workshop"
---

Database Workshop (DBW) is a unified cloud management platform for managing the lifecycle of various types of databases. DBW is a database SaaS product that integrates a graphical user interface (GUI), troubleshooting, and auditing, providing web terminal management capabilities such as comprehensive observation and analysis, intelligent risk checks, and autonomous O&M. It provides a stable, secure, and efficient cloud service for database management. RDS for SQL Server is integrated with Database Workshop (DBW), embedding its lock analysis and slow query log analysis features into the RDS for SQL Server console.

This chapter describes the lock analysis and slow query log analysis features.

## Lock Analysis

The lock analysis feature allows you to view and analyze all locks that occur in your RDS for SQL Server database instances.

### Prerequisites

You have [created an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide?lang=en), and its status is **Running**.

### Precautions

* Do not change the instance configurations while using the transaction and lock feature. Otherwise, you will be unable to view the instance's lock information.

* Data retention period: Query results are retained for up to 30 days.

* Deadlock Diagram Display Rule: The diagram shows the first deadlock by default. To view other deadlocks, click the corresponding item in the deadlock list.

### Procedure

1. Go to the Lock analysis tab. There are two ways to open this tab:

   **View directly in the SQL Server console**

1. Log on to the [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

   2. In the top menu bar, select the project and region of the instance.

   3. On the **Instances** page, click the name of the target instance.

   4. On the **Summary** page, click the **Database Workshop** tab.

   5. Click the **Transactions and Locks** sub\-tab.

   **Go to the DBW console to view**

1. Log on to the [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

   2. In the top menu bar, select the project and region of the instance.

   3. On the **Instances** page, click **Log in workshop** in the **Action** column of the target instance.

   4. Go to the data workshop and log in with your account and password.

   5. In the left\-side navigation pane of the data workbench, choose **Operation and Maintenance** \> **Monitoring and diagnosis**.

   6. In the upper right corner of the **Observation and diagnosis** page, switch the instance type to **RDS for SQL Server**.

   7. Click the **Lock analysis** tab.

2. View lock information. In the Transactions and Locks tab of the SQL Server console or the Lock Analysis tab of the DBW console, you can view **deadlock details** and **deadlock diagrams**:

   **Deadlock details**

In the **Deadlock details** area, customize the time for querying deadlock information as needed. The default view shows deadlock information from the last 7 days. Specific deadlock information is shown below:

   * **LastTranStarted**: The transaction start time, accurate to the millisecond, used to pinpoint the exact moment the deadlock occurred.

   * **SPID**: The session process ID, which uniquely identifies a database connection and is a key identifier for tracking deadlock processes.

   * **IsVictim**: Indicates whether the process is the deadlock victim. Marked as × means the process was selected by the system as the victim and rolled back; marked as √ means the process was terminated in the deadlock.

   * **Database**: The name of the database where the deadlock occurred.

   * **LogUsed**: The amount of log space used by this transaction (in bytes), reflecting the transaction's scale.

   * **LockMode**: The lock mode, such as X for exclusive lock, indicating the process is holding or requesting an exclusive lock.

   * **WaitResourceDesc**: The details of the resource the current transaction is waiting for, typically including the table name, index name, and key value, used to precisely identify the lock conflict object.

   * **ObjectOwned**: The ID of the lock object currently held by the process.

   * **ObjectRequested**: The ID of the lock object currently being requested by the process.

   * **WaitResource**: The resource the current transaction is waiting for.

   * **HostName**: The host name of the current transaction.

   * **LoginName**: The account name of the current transaction.

   * **Status**: The state of the current transaction; "suspended" indicates the process is suspended while waiting for a resource.

   * **ClientApp**: The name of the client application currently used by the firm, such as SQLCMD, to identify the source of the call.

   * **SQLText**: The text of the SQL statement that caused the deadlock. Click to copy for subsequent analysis and optimization.

   You can also click the  **+**  sign on the left of any row in the table to expand the Deadlocked process sub\-table for that row and view detailed information about all related processes in this deadlock event.

   **Deadlock diagram**

In the **Deadlock diagram** area, the cyclic wait relationship of the deadlock is displayed graphically. In the **Deadlock details** area, click the target row in the table to view the corresponding deadlock diagram. In the deadlock diagram, each node represents a process, and arrows represent request or hold relationships.

   * Node information interpretation

      * Process node (red/green border): Displays the SPID, host address, login account, and log usage. A red border indicates the process selected as the victim, and a green border indicates a surviving process.

      * Lock resource node (Key Lock): Displays the lock type (such as Key Lock), associated object ID, object name (such as TestDB.dbo.DeadlockTest), and index name (such as PK_Deadlock__3214EC2727\*\*\*\*\*\*).

   * Relationship Arrow Description

      * Owner mode: X: Indicates that the process holds an exclusive lock.

      * Request mode: X: Indicates that the process is requesting an exclusive lock.

      * An arrow pointing from a process to a lock resource indicates a "request"; an arrow pointing from a lock resource to a process indicates "holds."

## Slow log analysis

The slow query log analysis feature allows you to view slow query trends, statistics, and details for an instance, and analyze logs from primary and standby nodes to quickly identify issues.

### Prerequisites

* You have [created an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide?lang=en), and its status is **Running**.

* The slow query log has been enabled for the instance. If the slow query log is not enabled, refer to [Enable slow query log](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/enabling-slow-log?lang=en) for instructions.

### Precautions

* Currently, only slow logs from the primary node are supported, and the query results show up to the first 100 records from a maximum of 2 log files.

* By default, slow log information from the past 10 minutes is displayed.

* You can view slow log data for up to the past 30 days, with a maximum query time span of 7 days.

* When filtering to view slow SQL queries within a certain period, the query end time must be later than the start time.

* A single download supports up to 100 log entries.

### Procedure

1. Go to the Slow query log analysis page. You can access this page using one of the following two methods:

   **View directly in the SQL Server console**

1. Log on to the [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

   2. In the top menu bar, select the project and region of the instance.

   3. On the **Instances** page, click the name of the target instance.

   4. On the **Summary** page, click the **Database Workshop** tab.

   5. Click the **Slow query log analysis** subtab.

   **Go to the DBW console to view**

1. Log on to the [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

   2. In the top menu bar, select the project and region of the instance.

   3. On the **Instances** page, click Log in workshop in the **ActionLog in workshop** in the Action column of the target instance.

   4. Go to the data workshop and log in with your account and password.

   5. In the left\-side navigation pane of the data workbench, choose **Operation and maintenance** \> **Monitoring and diagnosis**.

   6. In the upper right corner of the **Observation and diagnosis** page, switch the instance type to **RDS for SQL Server**.

   7. Click **Log management**.

2. On the **Slow query log analysis** tab in the SQL Server console or the **Log management** tab in the DBW console, you can filter, view, and download slow query log details. The details are as follows:

   **Filter slow logs**

You can filter by a target time period. When selecting a query time frame, the query end time must be later than the query start time.

   You can also click **Advanced filter**. In the expanded filter area, configure the parameters as needed and click **Query**.

   * **Database name**: Enter the target database in the input box, then press Enter. Multiple databases can be entered at once.

   * **Executing user**: Enter the target user in the input box, then press Enter. Multiple executing users can be entered at once.

   * **IP source**: Enter multiple target IPs in the input box, then press Enter. Multiple IP addresses can be entered at once.

   **View slow SQL list**

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

   **Download a slow log**

1. Click![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6911ec2462a02cad5c95ff61813dfb56.png)the download icon to export the slow query log.

   2. In the **Export** dialog box, select the information to include in the slow log download as needed.

      The slow query log download can include **Execution completion time**, **SQL**, **Database**, **IP source**, **Application name**, **Executing user**, **Execution time (s)** , **Affected rows**, **CPU time**, **Total logical reads**, and **Total I/O writes**.

   3. Click **OK**.
