---
title: "Lock analysis management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/lock-analysis-management"
---

Database Workshop DBW provides the Lock Analysis feature for RDS for SQL Server instances. This feature is designed for database administrators and developers to deeply diagnose and resolve deadlock issues in SQL Server environments. Through intuitive form lists and visual deadlock diagrams, you can quickly identify the context of deadlocks, the involved processes, lock resources, and SQL statements, thereby accurately pinpointing performance bottlenecks and formulating optimization solutions. This article describes how to manage lock analysis for RDS for SQL Server instances in Database Workshop DBW.

<span id="HUUyq71V"></span>
## Prerequisites


* An instance has been created and the instance state is Running. For detailed steps, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide?lang=en).

* If the target instance has security control enabled, you need to apply for operation and maintenance read\-only or read/write permissions for the current account. For more information, refer to [Enabling instance security control ( RDS for SQL Server)](https://docs.byteplus.com/en/docs/DBW/enabling-security-control_), and [Applying for operation permissions ( RDS for SQL Server)](https://docs.byteplus.com/en/docs/DBW/creating-an-operation-permission-ticket_).


<span id="Bhlq6XqW"></span>
## Precautions


* This feature is currently in beta. You can [Submit a ticket](https://console.byteplus.com/workorder/create) to contact technical support for data migration.

* Do not modify the instance configuration while using the lock analysis feature, as this may prevent you from viewing the instance's lock information.

* Data retention period: Query results are retained for up to 30 days.

* Deadlock Diagram Display Rule: The diagram shows the first deadlock by default. To view other deadlocks, click the corresponding item in the deadlock list.


<span id="TTCMtFvn"></span>
## Procedure


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, switch the instance type and ID.

   1. In the upper right corner of the **Observation and diagnosis** page, switch the instance type to RDS for SQL Server.

   2. In the upper left corner of the **Observation and diagnosis** page, switch the target instance based on the instance ID or instance name.

5. On the **Observation and diagnosis** page, click Lock analysis.

6. On the Lock analysis tab, you can view the following information.

   
   <Tabs>
   <Tab zoneid="XC1e7PETki" title="Deadlock details">
   <TabTitle>Deadlock details</TabTitle>
   
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
   
   
   You can also click the + sign on the left of any row in the table to expand the Deadlocked process sub\-table for that row and view detailed information about all related processes in this deadlock event.
   
   
   </Tab>
   <Tab zoneid="N58ApfRYMg" title="Deadlock diagram">
   <TabTitle>Deadlock diagram</TabTitle>
   
   In the **Deadlock diagram** area, the cyclic wait relationship of the deadlock is displayed graphically. In the **Deadlock details** area, click the target row in the table to view the corresponding deadlock diagram. In the deadlock diagram, each node represents a process, and arrows represent request or hold relationships.
   
   
   * Node information interpretation
   
      * Process node (red/green border): Displays the SPID, host address, login account, and log usage. A red border indicates the process selected as the victim, and a green border indicates a surviving process.
   
      * Lock resource node (Key Lock): Displays the lock type (such as Key Lock), associated object ID, object name (such as TestDB.dbo.DeadlockTest), and index name (such as PK_Deadlock__3214EC2727\*\*\*\*\*\*).
   
   * Relationship Arrow Description
   
      * Owner mode: X: Indicates that the process holds an exclusive lock.
   
      * Request mode: X: Indicates that the process is requesting an exclusive lock.
   
      * An arrow pointing from a process to a lock resource indicates a "request"; an arrow pointing from a lock resource to a process indicates "holds."
   
   
   </Tab>
   </Tabs>
