---
title: "Transaction and lock management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/transaction-and-lock-management"
---

The Transactions and Locks feature can capture and analyze in real time the current lock holdings, lock waits, and related conditions in your RDS for PostgreSQL database. When lock\-wait issues occur in the database, the Transactions and Locks analysis feature enables intuitive inspection of relevant locking information, such as blocking transactions and waiting sessions, allowing you to quickly pinpoint and resolve problems, ensure database stability, and significantly reduce troubleshooting time. This article describes how to view all transaction and lock information occurring within an instance database in the DBW console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance for RDS for PostgreSQL has been created, and the instance status is running. For detailed steps, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/create_instance).

* If the target instance has security control enabled, you need to apply for operation and maintenance read\-only or read/write permissions for the current account. For more information, refer to [Enabling instance security control (RDS for PostgreSQL)](https://docs.byteplus.com/en/docs/DBW/enabling-security-control), and [Applying for operation permissions (RDS for PostgreSQL)](https://docs.byteplus.com/en/docs/DBW/Create_operation_permission_ticket).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


|**Type** |**Precautions** |
|---|---|
|Transactions and locks |The analysis results are sourced from the pg_stat_activity view, which provides information about all currently active sessions connected to the database, including the SQL statements they are executing (or most recently executed). |
|Lock wait message |Analysis data is sourced from the following views:<br><br><br>* pg_stat_activity: View all current database connections (sessions) and their executing (or recently executed) SQL statements, transaction states, and waiting status.<br><br>* pg_locks: View all locks currently held by sessions (table locks, row locks, transaction locks, etc.) and their status (granted/waiting). |
|Other considerations |* While using the transaction and lock feature, avoid modifying instance configurations, as this may prevent normal display of transactions and locks.<br><br>* Query results can be retained for up to 30 days. |


<span id="NQnVmPZ4"></span>
## Procedure


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **Transaction and lock**.

5. On the **Transaction and lock** tab, switch to the target instance type and the target instance.

   1. In the upper right corner of the tab, switch the instance type to RDS for PostgreSQL.

   2. In the upper\-left corner of the tab, switch the target instance. You can also switch to the target instance by searching for the instance ID.

6. On the **Transaction and lock** tab, select the instance node as needed (the primary node is displayed by default) to view the transaction and lock information for that instance, as detailed in the table below.



|**Type** |**Description** |
|---|---|
|**Transaction and lock information**<br><br> |<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If a lock is held but no contention occurs, the specific lock details cannot be viewed.</div><br><br><br>In the **Transaction and lock information** subtab, you can perform the following operations:<br><br><br>* Create an analysis task: In the **Transaction and lock information** subtab, you can either click **Create analysis** to manually create an analysis task, where the generated **Task source** is **Trigger\-based analysis**; or select an interval of **3 seconds**, **5 seconds**, **10 seconds**, or **15 seconds** from the dropdown list to automatically create analysis tasks, where the generated **Task source** is **Auto\-refresh analysis**.<br><br>* View analysis results: In the **Transaction and lock information** subtab, you can filter and view analysis tasks based on your desired time range for task creation. By default, analysis tasks from the last 3 hours are displayed, and you can view tasks created within the past 30 days at most.<br><br>   * No transactions or locks detected: If your analysis task does not find any active transactions or locks in the database, the **Detected transactions and locks** column will display **No**, and you can only see **Analysis task creation time**, **Task source**, and **Analysis data**.<br><br>   * Transactions and locks detected: If your analysis task identifies active transactions or locks in the database, the **Detected transactions and locks** column will display **Yes**. Click the ➕ icon in front of the analysis task creation time column to view all session information included in the transaction, such as **Session ID**, **Transaction ID**, **Transaction state**, **Transaction execution time(s)** , **Transaction start time**, **Executing SQL**, **ID of the blocking transaction**, and **NodeId**.<br><br>      * When transactions and locks are present, you can click the target Session ID in the Transactions and Locks section to navigate to the Session Management tab, where you can optionally terminate the corresponding session as needed. For detailed steps, refer to [Terminate session](https://docs.byteplus.com/en/docs/DBW/session-management?lang=zh&TagIDs=2#g9LUJw4G).<br><br>      * When transactions and locks exist, you can **Copy the SQL statement** executed by the corresponding session in the Executing SQL column. |
|**Lock wait message** |In the **Lock wait information** subtab, the following operations are available:<br><br><br>* Create an analysis task: In the **Lock wait information** subtab, you can either click **Create aAnalysis** to manually create an analysis task (with **Task source** labeled as **Trigger\-based analysis**), or select an interval of **3 seconds**, **5 seconds**, **10 seconds**, or **15 seconds** from the dropdown to automatically create analysis tasks (with **Task source** labeled as **Auto\-refresh analysis**).<br><br>* View analysis results: In the **Lock wait information** subtab, you can filter and view analysis tasks based on the desired time range. The default display shows analysis tasks from the last 3 hours, with a maximum historical range of 30 days.<br><br>   * No lock wait information found: If your analysis task does not detect any lock waits in the database, the **Detected locks** column will display **No**. You will only see **Analysis task creation time**, **Task source**, and **Analysis data**.<br><br>   * Lock wait information exists: If your analysis task detects lock waits in the database, the **Lock wait detected** column will display **Yes**. Click the ➕ icon next to the task creation time column to view detailed lock wait information for that task, including:<br><br>      * Transaction ID, Transaction state, Lock wait SQL, Transaction start time, Transaction wait since.<br><br>      * Blocking wait time(s), Blocking transaction ID, Blocking transaction status, Blocker SQL, Blocking transaction start time, NodeId.<br><br><br>You can also **View details** to compare session and blocking transaction session information. |
