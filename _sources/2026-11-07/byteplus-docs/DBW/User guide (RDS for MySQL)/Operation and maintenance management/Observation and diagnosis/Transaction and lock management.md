---
title: "Transaction and lock management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/lock-analysis-management-for-mysql"
---

The Transactions and Locks feature can capture and analyze in real time the current lock related conditions such as held locks, deadlocks, and lock waits in a RDS for MySQL instance. When lock\-wait issues occur in the database, you can use the Transactions and Locks analysis feature to intuitively examine and visualize relevant locking information such as blocked sessions, holding transactions, and wait chains enabling rapid identification and resolution of the root cause. This helps ensure stable database operation and significantly reduces troubleshooting time. This article describes how to view all transaction and lock information occurring within an instance database in the DBW console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance and account have been created, and the instance status is running. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1) and [Creating an account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_databases_and_accounts#.5Yib5bu66LSm5Y-3).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This feature is not supported when the instance status is creating, recovering, importing, error, deleted, terminated, waiting for payment, billing suspension in progress, billing restoring, billing reclaiming or reconstructing.   </div>
   

* If the target instance has security control enabled, you need to apply for operation and maintenance read\-only or read/write permissions for the current account. For more information, refer to [Enabling instance security control (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql), and [Applying for operation permissions (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/creating-an-operation-permission-ticket).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

The Transactions and Locks feature can capture and analyze in real time the current lock related conditions such as held locks, deadlocks, and lock waits in a RDS for MySQL instance. When lock\-wait issues occur in the database, you can use the Transactions and Locks analysis feature to intuitively examine and visualize relevant locking information such as blocked sessions, holding transactions, and wait chains enabling rapid identification and resolution of the root cause. This helps ensure stable database operation and significantly reduces troubleshooting time. This article describes how to view all transaction and lock information occurring within an instance database in the DBW console.

<span id="3GTT5xwP"></span>
## Prerequisites


* An instance and account have been created, and the instance status is running. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1?lang=en) and [Creating an account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_databases_and_accounts?lang=en#.5Yib5bu66LSm5Y-3).

   This feature is not supported when the instance status is creating, recovering, importing, error, deleted, terminated, waiting for payment, billing suspension in progress, billing restoring, billing reclaiming or reconstructing.

* If the target instance has security control enabled, you need to apply for operation and maintenance read\-only or read/write permissions for the current account. For more information, refer to [Enabling instance security control (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql?lang=en), and [Applying for operation permissions (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/creating-an-operation-permission-ticket?lang=en).


<span id="Jd6LAsQ1"></span>
## Precautions


* While using the transaction and lock feature, avoid modifying instance configurations, as this may prevent normal display of transactions and locks.

* Query results can be retained for up to 30 days.

* Considerations for each module are as follows:

   
   <Tabs>
   <Tab zoneid="FZwhvoJkEn" title="InnoDB Transactions and Locks">
   <TabTitle>InnoDB Transactions and Locks</TabTitle>
   
   * For RDS for MySQL instances of version 8.0, analysis results are sourced from the following tables:
   
      * `information_schema.INNODB_TRX`: Displays all currently running InnoDB transactions.
   
      * `performance_schema.data_locks`: Shows all locks (InnoDB row/table locks) held by current transactions.
   
      * `performance_schema.data_lock_waits`: Used to view current lock wait relationships (i.e., who is waiting for whom).
   
   * For RDS for MySQL instances of version 5.7:
   
      * When there is no lock contention between transactions, specific lock details, such as transaction IDs, cannot be detected.
   
      * Analysis results are sourced from the following tables:
   
         * `information_schema.INNODB_TRX`: Displays all currently running InnoDB transactions.
   
         * `information_schema.INNODB_LOCKS`: Used to view all locks (InnoDB row/table locks) currently held by transactions.
   
         * `information_schema.INNODB_LOCK_WAITS`: Displays current lock wait relationships (i.e., who is waiting for whom).
   
   
   </Tab>
   <Tab zoneid="dvkeZr86BE" title="Deadlock information">
   <TabTitle>Deadlock information</TabTitle>
   
   * The parameter innodb_deadlock_detect for the target instance must be set to ON. Otherwise, deadlock information can not be queried. For parameter configuration steps, refer to [Modifying parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_parameters?lang=en).
   
   * The Deadlocks tab collects the most recent deadlock information each time a query is performed.
   
   * Request types in deadlock information include `alter`, `show`, `select`, `update`, `drop`, `delete`, `create`, and others.
   
   * The analysis results are sourced from the table `innodb status`: Used to view the internal operational status of the InnoDB storage engine in real time.
   
   * For RDS for MySQL 5.7 or earlier versions, note the following:
   
      * When a circular deadlock occurs and involves three or more transactions, only details of two transactions in the deadlock are displayed.
   
      * When a deadlock occurs, detailed information about the transactions involved in the deadlock can be displayed, but only one of the transactions will show its held lock information.
   
   
   </Tab>
   <Tab zoneid="yCVdFL8M0u" title="Lock wait message">
   <TabTitle>Lock wait message</TabTitle>
   
   * Prerequisites and performance impact
   
      * MySQL 8.0 instances: The `Performance Schema` parameter must be configured to `ON`; otherwise, transaction blocking relationships cannot be obtained. For specific configuration, refer to [Modify parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_parameters?_vtm_=a106466.b106468.0_0.0_0.0.1727_7610615829733918244&lang=en).
   
      * Performance evaluation: Enabling `Performance Schema` incurs some performance overhead on the database. Additionally, querying related monitoring tables on heavily loaded instances may cause performance fluctuations. Carefully evaluate and perform actions based on your actual business conditions.
   
   * Analysis data sources: The system obtains detailed information about lock waits and transaction blocking from the following core tables.
   
      * `information_schema.INNODB_TRX`: Displays the state of all currently running InnoDB transactions.
   
      * `performance_schema.data_locks / data_lock_waits` (for MySQL 8.0): Used to view all locks (InnoDB row/table locks) currently held by transactions and specific lock wait relationships.
   
      * `information_schema.INNODB_LOCKS / INNODB_LOCK_WAITS`: Before MySQL version 8.0, these two tables were the primary sources for analyzing transaction and lock relationships.
   
   * Security operation warning: Exercise extreme caution when performing lock wait analysis:
   
      * MySQL 8.0 instance: Querying the `performance_schema.data_lock_waits` table may trigger a global lock, affecting online business operations.
   
      * MySQL 5.7 instance: Querying the `information_schema.INNODB_LOCK_WAITS` table also carries the risk of triggering a global lock, which may disrupt business operations.
   
   
   </Tab>
   </Tabs>
   


<span id="yoDx6y8k"></span>
## Procedure


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **Transaction and lock**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **RDS for MySQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **Transaction and lock** tab, select the instance node as needed (the primary node is displayed by default) to view the transaction and lock information for that instance, as detailed in the table below.

   
   <Tabs>
   <Tab zoneid="cA6BCUITjf" title="InnoDB transaction and lock information">
   <TabTitle>InnoDB transaction and lock information</TabTitle>
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   <div data-tips="true" data-tips-type="default">If a lock is held but no contention occurs, the specific lock details cannot be viewed.</div>
   
   
   In the **InnoDB transaction and lock information** subtab, you can perform the following actions:
   
   
   * Create analysis task: In the **InnoDB transaction and lock information** sub\-tab, you can either click **Create analysis** to manually create a task (with **Task source** labeled as **Trigger\-based analysis**), or select an automatic interval of **3 seconds**, **5 seconds**, **10 seconds**, or **15 seconds** from the dropdown to generate tasks (with **Task source** labeled as **Auto\-refresh analysis**).
   
   * View analysis results: In the **InnoDB transaction and lock information** sub\-tab, filter analysis tasks by their **generation time** range as needed. By default, tasks from the last 3 hours are displayed, with a maximum history of 30 days.
   
      * No transactions or locks detected: When no transactions or locks are found in the database for your analysis task, the **Detected transactions and locks** column will show **No**. You will only see the **Analysis task creation time**, **Task source**, and **Analysis data**.
   
      * Transactions or locks detected: When transactions or locks are found in the database for your analysis task, the **Detected transactions and locks** column will show **Yes**. Click the ➕ icon before the analysis task creation time to view all session information, including **Session ID**, **Transaction ID**, **Transaction state**, **Lock status**, **Transaction isolation level**, **Transaction execution time(s)** , **Transaction start time**, **Transaction wait since**, **Executing SQL**, **Transaction locked tables**, **Transaction locked rows**, **Number of rows modified by the transaction**, **ID of the blocking transaction**, and **NodeId**.
   
         * When transactions or locks exist, click the target session ID to navigate to the session management tab, where you can terminate the corresponding session as needed. For detailed steps, see [Terminate session](https://docs.byteplus.com/en/docs/DBW/session-information-management-for-mysql?lang=en#.a2lsbC3kvJror50=).
   
         * When transactions or locks exist, you can copy the SQL statement executed by the corresponding session from the **Executing SQL** column.
   
   
   </Tab>
   <Tab zoneid="D0Uke6lROD" title="Deadlock information">
   <TabTitle>Deadlock information</TabTitle>
   
   On the **Deadlock information** subtab, you can perform the following operations:
   
   
   * Create analysis task: On the **Deadlock information** subtab, you can either click **Create analysis** to manually create an analysis task (with **Task source** as **Trigger\-based analysis**), or select an interval of **3 seconds**, **5 seconds**, **10 seconds**, or **15 seconds** from the dropdown to automatically create analysis tasks (with **Task source** as **Auto\-refresh analysis**).
   
   * View analysis results: On the **Deadlock information** subtab, filter analysis tasks by their creation time range as needed. By default, tasks from the last 3 hours are displayed, with a maximum history of 30 days.
   
      * No deadlock information: When no deadlocks are detected in the database for your created analysis task, the **Detected locks** column will display **No**. Only **Analysis task creation time**, **Task source**, and **Analysis data** are visible.
   
      * Deadlock information exists: When deadlocks are detected in the database for your created analysis task, the **Detected locks** column will display **Yes**. Click the ➕ icon before the analysis task creation time to view deadlock details, including **Deadlock occurrence time**, **Transaction information**, **Session ID**, **Request type**, **Involving table**, **Wait for lock**, **Lock\-wait index name**, **Wait lock type**, **Hold lock**, **Index name of hold lock**, **Hold lock type**, **Involving statement**, and **Transaction processing**.
   
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   
   * <div data-tips="true" data-tips-type="default">Each query collects the most recent deadlock information, and the results are retained for up to 30 days.</div>
   
   
   * <div data-tips="true" data-tips-type="default">The parameter <code>innodb_deadlock_detect</code> for the target instance must be set to <code>ON</code>. Otherwise, deadlock information cannot be queried. For details, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_parameters">Modify parameters</a>.</div>
   
   
   
   </Tab>
   <Tab zoneid="BukuMbBEp4" title="Lock wait message">
   <TabTitle>Lock wait message</TabTitle>
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   
   * <div data-tips="true" data-tips-type="default">For RDS for MySQL 8.0, to obtain transaction blocking relationships of the instance, the parameter <code>Performance Schema</code> must be set to <code>ON</code>. However, the parameter <code>Performance Schema</code> setting to <code>ON</code> may significantly impact database performance. Enable it with caution. For parameter configuration steps, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_parameters?lang=en">Modifying parameters</a>.</div>
   
   
   * <div data-tips="true" data-tips-type="default">MySQL 8.0 instance: Querying the <code>performance_schema.data_lock_waits</code> table may trigger a global lock, affecting online business operations.</div>
   
   
   * <div data-tips="true" data-tips-type="default">MySQL 5.7 instance: Querying the <code>information_schema.INNODB_LOCK_WAITS</code> table also carries the risk of triggering a global lock, which may disrupt business operations.</div>
   
   
   
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
