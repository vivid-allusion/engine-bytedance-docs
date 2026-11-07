---
title: "Transaction and lock management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Transaction_and_lock_management"
---

The Transactions and Locks feature can capture and analyze in real time the current lock related conditions such as held locks, deadlocks, and lock waits in a NDB for MySQL instance. When lock\-wait issues occur in the database, you can use the Transactions and Locks analysis feature to intuitively examine and visualize relevant locking information such as blocked sessions, holding transactions, and wait chains enabling rapid identification and resolution of the root cause. This helps ensure stable database operation and significantly reduces troubleshooting time. This article explains how to view all transaction and lock information within an instance database on the DBW console.

<span id="tR8ClRs8"></span>
## Prerequisites


* An NDB for MySQL instance and an account have been created, and the Instance state is Running. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1) and [Creating an account](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_and_deleting_accounts).

* If the target instance has security control enabled, you need to apply for operation and maintenance read\-only or read/write permissions for the current account. For more information, see [Enable security control for NDB for MySQL instances](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control) and [Apply for operation permissions related to NDB for MySQL](https://docs.byteplus.com/en/docs/DBW/Creating_an_operation_permission_ticket).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* While using the transaction and lock feature, avoid modifying instance configurations, as this may prevent normal display of transactions and locks.

* Query results can be retained for up to 30 days.

* Considerations for each module are as follows:

   
   <Tabs>
   <Tab zoneid="BZscghTP3g" title="InnoDB Transactions and Locks">
   <TabTitle>InnoDB Transactions and Locks</TabTitle>
   
   * Viewing InnoDB transaction and lock information on secondary nodes is currently unsupported.
   
   * Analysis results are sourced from the following tables
   
      * information_schema.INNODB_TRX: Displays all currently running InnoDB transactions.
   
      * performance_schema.data_locks: Shows all locks (InnoDB row/table locks) held by current transactions.
   
   
   For versions prior to 8.0, transaction and lock analysis sources were from the information_schema.INNODB_LOCKS table.
   
   
      * performance_schema.data_lock_waits: Used to view current lock wait relationships (i.e., who is waiting for whom).
   
   
   Prior to version 8.0, transaction and lock analysis was sourced from the information_schema.INNODB_LOCK_WAITS table.
   
   
   </Tab>
   <Tab zoneid="fZhlfX4oya" title="Deadlock information">
   <TabTitle>Deadlock information</TabTitle>
   
   * The parameter innodb_deadlock_detect for the target instance must be set to ON. Otherwise, deadlock information can not be queried. For parameter configuration steps, refer to [Modifying parameters](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_parameters?lang=en).
   
   * The deadlock tab collects the latest deadlock information with each query.
   
   * Analysis results are sourced from the table innodb status, which provides real\-time monitoring of InnoDB storage engine internals.
   
   * Secondary nodes contain no deadlock information and are not analyzed by default.
   
   * Request types in deadlock information include alter, show, select, update, drop, delete, create, and others.
   
   
   </Tab>
   <Tab zoneid="ffy4Hv8x8Y" title="Lock wait message">
   <TabTitle>Lock wait message</TabTitle>
   
   * For veDB MySQL 8.0, to obtain transaction blocking relationships of the instance, the parameter Performance Schema must be set to ON. However, enabling Performance Schema may significantly impact database performance. Configure with caution. For parameter configuration steps, refer to [Modifying parameters](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_parameters?lang=en).
   
   * Secondary nodes do not have lock wait information and are excluded from analysis by default.
   
   * Analysis results are sourced from the following tables:
   
      * information_schema.INNODB_TRX: Displays all currently running InnoDB transactions.
   
      * performance_schema.data_locks: Shows all locks (InnoDB row/table locks) held by current transactions.
   
   
   For versions prior to 8.0, transaction and lock analysis sources were from the information_schema.INNODB_LOCKS table.
   
   
   </Tab>
   </Tabs>
   


<span id="8k7QefbY"></span>
## Procedure


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **Transaction and lock**.

   1. In the drop\-down list in the upper\-right corner of the page, select the **NDB for MySQL** database type.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **Transactions and lock** tab, select the instance node as needed (primary node displayed by default) to view the instance's transaction and lock information, as detailed in the table below.

   
   <Tabs>
   <Tab zoneid="OhIziRkaK4" title="InnoDB transaction and lock information">
   <TabTitle>InnoDB transaction and lock information</TabTitle>
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   
   * <div data-tips="true" data-tips-type="default">For NDB for MySQL instances on version 5.7, if a lock is held without contention, specific lock details cannot be viewed.</div>
   
   
   * <div data-tips="true" data-tips-type="default">Viewing InnoDB transaction and lock information on secondary nodes is currently unsupported.</div>
   
   
   
   In the **InnoDB transaction and lock information** sub\-tab, you can perform the following actions:
   
   
   * Create analysis task: In the **InnoDB transaction and lock information** sub\-tab, you can either click **Create analysis** to manually create a task (with **Task source** labeled as **Trigger\-based analysis**), or select an automatic interval of **3 seconds**, **5 seconds**, **10 seconds**, or **15 seconds** from the dropdown to generate tasks (with **Task source** labeled as **Auto\-refresh analysis**).
   
   * View analysis results: In the **InnoDB transaction and lock information** sub\-tab, filter analysis tasks by their **generation time** range as needed. By default, tasks from the last 3 hours are displayed, with a maximum history of 30 days.
   
      * No transactions or locks detected: When no transactions or locks are found in the database for your analysis task, the **Detected transactions and locks** column will show **No**. You will only see the **Analysis task creation time**, **Task source**, and **Analysis data**.
   
      * Transactions or locks detected: When transactions or locks are found in the database for your analysis task, the **Detected transactions and locks** column will show **Yes**. Click the ➕ icon before the analysis task creation time to view all session information, including **Session ID**, **Transaction ID**, **Transaction state**, **Lock status**, **Transaction isolation level**, **Transaction execution time(s)** , **Transaction start time**, **Transaction wait since**, **Executing SQL**, **Transaction locked tables**, **Transaction locked rows**, **Number of rows modified by the transaction**, **ID of the blocking transaction**, and **NodeId**.
   
         * When transactions or locks exist, click the target session ID to navigate to the session management tab, where you can terminate the corresponding session as needed. For detailed steps, see [Terminate session](https://docs.byteplus.com/en/docs/DBW/Session_information_management?lang=en#.a2lsbC3kvJror50=).
   
         * When transactions or locks exist, you can copy the SQL statement executed by the corresponding session from the **Executing SQL** column.
   
   
   </Tab>
   <Tab zoneid="gSLKuYarD0" title="Deadlock information">
   <TabTitle>Deadlock information</TabTitle>
   
   On the **Deadlock information** subtab, you can perform the following operations:
   
   
   * Create analysis task: On the **Deadlock information** subtab, you can either click **Create analysis** to manually create an analysis task (with **Task source** as **Trigger\-based analysis**), or select an interval of **3 seconds**, **5 seconds**, **10 seconds**, or **15 seconds** from the dropdown to automatically create analysis tasks (with **Task source** as **Auto\-refresh analysis**).
   
   * View analysis results: On the **Deadlock information** subtab, filter analysis tasks by their creation time range as needed. By default, tasks from the last 3 hours are displayed, with a maximum history of 30 days.
   
      * No deadlock information: When no deadlocks are detected in the database for your created analysis task, the **Detected locks** column will display **No**. Only **Analysis task creation time**, **Task source**, and **Analysis data** are visible.
   
      * Deadlock information exists: When deadlocks are detected in the database for your created analysis task, the **Detected locks** column will display **Yes**. Click the ➕ icon before the analysis task creation time to view deadlock details, including **Deadlock occurrence time**, **Transaction information**, **Session ID**, **Request type**, **Involving table**, **Wait for lock**, **Lock\-wait index name**, **Wait lock type**, **Hold lock**, **Index name of hold lock**, **Hold lock type**, **Involving statement**, and **Transaction processing**.
   
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   
   * <div data-tips="true" data-tips-type="default">Each query collects the most recent deadlock information, and the results are retained for up to 30 days.</div>
   
   
   * <div data-tips="true" data-tips-type="default">The parameter innodb_deadlock_detect for the target instance must be set to ON. Otherwise, deadlock information cannot be queried. For details, refer to <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_parameters?lang=en">Modify parameters</a>.</div>
   
   
   
   </Tab>
   <Tab zoneid="MgNdvo8gDR" title="Lock wait message">
   <TabTitle>Lock wait message</TabTitle>
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   <div data-tips="true" data-tips-type="default">For veDB MySQL 8.0, to obtain transaction blocking relationships of the instance, the parameter Performance Schema must be set to ON. However, enabling Performance Schema may significantly impact database performance. Configure with caution. For parameter configuration steps, refer to <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_parameters?lang=en">Modifying parameters</a>.</div>
   
   
   On the **Lock wait information** subtab, you can perform the following operations:
   
   
   * Create analysis tasks: On the **Lock wait message** subtab, you can either click **Create analysis** to manually create a task (with **Task source** labeled as **Trigger\-based analysis**), or select an **3 seconds**, **5 seconds**, **10 seconds**, or **15 seconds** interval from the dropdown to auto\-create tasks (with **Task source** labeled as **Auto\-refresh analysis**).
   
   * View analysis results: On the **Lock wait information** subtab, filter tasks by their Analysis task creation time as needed. By default, tasks from the last 3 hours are displayed, with a maximum history of 30 days.
   
      * No lock wait detected: If no waiting locks are found in the database for your task, the **Detected locks** column shows **No**. Only **Analysis task creation time**, **Task source**, and **Analysis data** are visible.
   
      * Lock wait information exists: If your analysis task detects lock waits in the database, the **Lock wait detected** column will display **Yes**. Click the ➕ icon next to the task creation time column to view detailed lock wait information for that task, including:
   
         * Transaction ID, transaction state, lock wait SQL, transaction start time, transaction wait since, number of rows modified by the transaction, transaction locked rows, and transaction operation status.
   
         * Blocking wait time(s), blocking transaction ID, blocking transaction status, blocker SQL, blocking transaction start time, blocking transaction wait start time, blocking transaction modified row count, number of locked rows for blocking transactions, blocking transaction operation status, and NodeId.
   
   
   You may also click **View details** to compare session and blocking transaction session information.
   
   
   </Tab>
   </Tabs>
