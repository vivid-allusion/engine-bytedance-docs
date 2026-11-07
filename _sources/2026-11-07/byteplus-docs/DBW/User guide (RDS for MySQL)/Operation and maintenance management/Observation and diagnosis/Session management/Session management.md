---
title: "Session management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/session-information-management-for-mysql"
---

This topic describes how to use the session management feature of Database Workshop (DBW) to view session statistics and real\-time session information of an instance by RDS for MySQL engine or RDS for MySQL proxy.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**


* An instance and account for RDS for MySQL have been created, and the instance status is running. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1) and [Creating an account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_databases_and_accounts#.5Yib5bu66LSm5Y-3).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This feature is not supported when the instance status is creating, recovering, importing, error, deleted, terminated, waiting for payment, billing suspension in progress, billing restoring, billing reclaiming or reconstructing.   </div>
   

* If the target instance has security control enabled, you need to apply for operation and maintenance read\-only or read/write permissions for the current account. For more information, refer to [Enabling instance security control (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql), and [Applying for operation permissions (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/creating-an-operation-permission-ticket).


<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* When the database proxy is enabled for an RDS for MySQL instance, session information for both RDS for MySQL engine and RDS for MySQL proxy is supported. While the proxy feature is disabled, only session information for RDS for MySQL engine is available. The proxy feature is enabled by default. If you do not need to view proxy sessions, you can disable the proxy for RDS for MySQL instances. For specific steps, refer to [Enabling database proxy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enable_database_agent).

* The session statistics refresh interval is set to 5 seconds by default. You can choose to disable auto\-refresh or change the interval to 10 or 15 seconds.

* The **Real\-time session** tab does not display connections from internal accounts of RDS for MySQL (e.g., `root`, `repl`, `byte_rds_agent`, `byte_rds_backup`, `byte_rds_proxy`) and DBW (e.g., `dbw_admin`).

* When you access session management under operation observability, the IP address of the DBW backend service host is automatically added to the allowlist of the corresponding product. The allowlist naming format varies by instance type, The `Allowlist` is named in the format of `DBW_Sole_ *_* _***_RDS` `Or` `byte_rds_ *_* _***-`.

* While using the session management feature, avoid modifying instance configurations, as this may prevent normal display of session information.

* Session snapshot files downloaded by the system are compressed in the `.gz` (Gzip) format. For macOS users, please extract the downloaded file using the steps below:

   * Decompress using the built\-in gzip or gunzip command\-line tools:Open the Terminal and run the gzip or gunzip commands provided by the system to extract the files. The command format is `gzip -d your_filename.gz` or `gunzip your_filename.gz`.

   * To decompress the file using the tar tool: Download and install the tar tool to decompress the file. The command format is `tar -xz --force-local -f file_name.gz`.

* Starting from 2025.12.05, session snapshots for all newly created instances in DBW are disabled by default. If you need to enable session snapshots, you can do so in the instance list or in the session management and transaction and lock sections of the instance. Session snapshots are enabled for existing instances.

   * Enabling the snapshot feature will periodically collect instance\-related information, which introduces additional overhead to the instance.

   * The default collection frequency is 30 seconds.

   * Collection tasks are executed serially; that is, a new collection will not start until the previous one has completed.

   * After enabling or disabling the snapshot feature, the data collection tasks will be adjusted within a few minutes.

   * After the snapshot feature is disabled, historical data is retained for up to 30 days.

   * The aggregation session and hotspot analysis functions in session management both rely on session snapshot data. Therefore, to use the instance's aggregation session or hotspot analysis functions normally, enable session snapshots for the instance.

   * Qwen3.7\-MaxIf the backoff strategy is enabled for the instance, the system may skip certain collection points when high database load causes collection timeouts. In this case, you can refer to the last collection record prior to the skip for diagnosis.


<span id=".5p-l55yL5Lya6K-d5L-h5oGv"></span>
## **View a session**


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis ** page, above the **Session management**tab, switch the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also switch to the target instance by searching for the instance ID.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you access the <strong>Session management </strong>tab through <strong>Operation observability</strong> on the left navigation bar, information about the first instance in the <strong>Instance list </strong>is viewed by default.   </div>
   

5. On the **Session management ** tab, click **RDS for MySQL engine ** or **RDS for MySQL proxy ** to view session statistics and real\-time session information as follows:

   
   <Tabs>
   <Tab zoneid="gqPR11xOKu" title="RDS for MySQL engine">
   <TabTitle>RDS for MySQL engine</TabTitle>
   
   On the **RDS for MySQL engine** pane, you can view the following information:
   
   
   * In the **session statistics** area, view session statistics, such as **total number of sessions**, **active sessions**, **CPU usage**, **Top5 user statistics**, **Top10 IP source statistics**, and **TOP10 database**.
   
   * On the **Aggregation session** pane, perform the following:
   
      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
      
   
      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Aggregation sessions only count session information for active sessions.   </div>
      
   
      * View the details of the aggregation session: You can review all aggregation sessions for the instance within a specified time range, with support for querying sessions up to the last 24 hours. The aggregation session information includes **SQL template**, **Database name**, **Execution time**, **Average execution time(s)** , **Maximum execution time(s)**  and **Total execution time(s)** . You can also click the target SQL template under the **SQL template** column to view session details.
   
      * Filter sessions: Enter session keywords in the **Search keywords, such as SELECT ** text box, to query eligible session information.
   
      * View session hotspot analysis: Hotspot analysis provides in\-depth insights into user interactions and high\-traffic areas, helping optimize system performance and enhance user experience. Click hotspot analysis to access its control panel, where you can view TOP 5 hotspot analysis results, including SQL text, execution time, and execution rate. You can also click Rate limit in the Actions column for a target SQL to control database request volume and SQL concurrency, ensuring service availability. For details on SQL throttling configuration, refer to [SQL throttling management](https://docs.byteplus.com/en/docs/DBW/preview-sql-throttle-task-management-for-mysql).
   
   * On the **Real\-time session information** pane, perform the following:
   
      * View session details: You can view each session's information including **Progress ID**, **User name**, **Host**, **Database name**, **Command type**, **Duration**, **Status**, **Execute statement**, **Blocking process ID**, **Node type** and **Node ID**, where the duration is the duration of the current state.
   
      * View session snapshots: Click **Session snapshot list** to access the **Session snapshot list** control panel. Select the desired instance node and time range (query span must not exceed 24 hours).
   
         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
         
   
         <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Session snapshots are retained for up to 30 days and can be viewed in the list.      </div>
         
   
      * Terminate sessions: You can terminate sessions as needed. For detailed steps, refer to [KILL sessions](https://docs.byteplus.com/en/docs/64/24741#.a2lsbC3kvJror50=).
   
      * Filter sessions: Filter qualified instance sessions as needed based on **Active sessions** or **All sessions** from the **Session type** drop\-down list.
   
      * Create a persistent Kill session task: Click **Persistent Kill ** to create a persistent Kill session task. For more information, refer to [KILL sessions](https://docs.byteplus.com/en/docs/64/24741#.a2lsbC3kvJror50=).
   
   
   </Tab>
   <Tab zoneid="crw12V2y4M" title="RDS for MySQL proxy">
   <TabTitle>RDS for MySQL proxy</TabTitle>
   
   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>
   
   
   <div data-tips="true" data-tips-type="tip">When the database proxy is enabled for an RDS for MySQL instance, session information for the RDS for MySQL proxy becomes accessible. For instructions on enabling the database proxy, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/enable_database_agent">Enabling database proxy</a>.</div>
   
   
   On the **RDS for MySQL proxy** pane, you can view the following information:
   
   
   * On the **Session statistics** pane, view session statistics such as **Total sessions**, **Active sessions**, **CPU usage**, **TOP10 user statistics**, **TOP10 IP source statistics ** and **TOP10 database**.
   
   * On the **Aggregation session** pane, perform the following:
   
      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
      
   
      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Aggregation sessions only count session information for active sessions.   </div>
      
   
      * View the details of the aggregation session: You can review all aggregation sessions for the instance within a specified time range, with support for querying sessions up to the last 24 hours. The aggregation session information includes **SQL template**, **Database name**, **Execution time**, **Average execution time(s)** , **Maximum execution time(s)**  and **Total execution time(s)** . You can also click the target SQL template under the **SQL template** column to view session details.
   
      * Filter sessions: Enter session keywords in the **Search keywords, such as SELECT ** text box, to query eligible session information.
   
      * View session hotspot analysis: Hotspot analysis provides in\-depth insights into user interactions and high\-traffic areas, helping optimize system performance and enhance user experience. Click hotspot analysis to access its control panel, where you can view TOP 5 hotspot analysis results, including SQL text, execution time, and execution rate. You can also click Rate limit in the Actions column for a target SQL to control database request volume and SQL concurrency, ensuring service availability. For details on SQL throttling configuration, refer to [SQL throttling management](https://docs.byteplus.com/en/docs/DBW/preview-sql-throttle-task-management-for-mysql).
   
   * On the **Real\-time session** pane, perform the following:
   
      * View session details: You can view each session's information including **Progress ID**, **User name**, **Host**, **Database name**, **Command type**, and **Duration**, where the duration is the duration of the current state.
   
      * Filter sessions: Filter qualified instance sessions as needed based on **Active sessions** or **All sessions** from the **Session type** drop\-down list.
   
   
   </Tab>
   </Tabs>
   


<span id=".a2lsbC3kvJror50="></span>
## KILL session

DBW provides the `kill` session function, which can be used to terminate specific processes or sessions, maintaining system stability and efficiency. DBW offers methods including KILL selected sessions, KILL all sessions, KILL matching sessions, and persistent KILL sessions to help you effectively control system resources and process behavior.

<span id=".5rOo5oSP5LqL6aG5"></span>
### Precautions


* Multiple persistent Kill session tasks are independent of each other (an "or" relationship) and do not interact.

* When RDS MySQL has the database proxy enabled and uses a transaction pooling connection mode, its connection reuse mechanism may lead to unexpected behavior during KILL sessions. If you attempt to KILL a current session, the connection might have already been reused by another session, causing the KILL operation to not execute as expected. The following two scenarios may occur:

   * Failed to KILL a system connection: After enabling the database proxy, system connections may also reuse user session connections. In some cases, if the user connection you attempt to KILL is being reused by a system connection, you may receive an "insufficient permissions" error. This happens because system connections typically have higher privilege levels and can not be directly terminated by normal users.

   * KILL connections from other users: Due to connection reuse, if user A’s session connection is reused by user B before the KILL operation is executed, attempting to KILL user A’s session may instead terminate user B’s connection.

   Additionally, during batch KILL operations, if an "insufficient permissions" error appears, it typically only indicates the failure to KILL system sessions. Other session KILL operations will continue to be executed normally.


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

3. On the top menu bar, select the project and region.

4. In the upper left corner of the **Session management ** tab, switch the instance.

5. On the **Session information ** sub\-tab of **Session management**, click **Engine**.

6. On the **Session information ** sub\-tab, click **Real\-time session**.

7. On the **Real\-time session** pane, select the KILL session mode as needed.

   
   <Tabs>
   <Tab zoneid="aPMqakPPC6" title="KILL selected session">
   <TabTitle>KILL selected session</TabTitle>
   
   1. Check the target session ID and click **KILL selected session**.
   
   2. In **Confirm KILL?**  dialog box, confirm the session information that needs to be killed, and click **OK**
   
   
   </Tab>
   <Tab zoneid="Nydp5Gydti" title="KILL all sessions">
   <TabTitle>KILL all sessions</TabTitle>
   
   1. Click **KILL all sessions**.
   
   2. In **Confirm KILL?**  dialog box, confirm the session information that needs to be killed, and click **OK**
   
   
   </Tab>
   <Tab zoneid="xmHylxlCdh" title="KILL matching sessions">
   <TabTitle>KILL matching sessions</TabTitle>
   
   1. Click **KILL matching sessions**.
   
   2. In the **KILL matching sessions** dialog box, configure the following parameters.
   
      1. **IP address**: Enter IP addresses as needed. Up to 10 IP addresses are supported, separated by commas (,).
   
      2. **Username**: Enter username as needed. Up to 10 usernames are supported, separated by commas (,).
   
      3. **Database name**: Enter database name as needed. Up to 10 database names are supported, separated by commas (,).
   
      4. **Additional KILL conditions**: You can select **SQL type**, **SQL template**, and **Null** KILL additional conditions.
   
      5. **SQL type**: When you select **SQL type** in **Additional KILL conditions**, you can select the SQL additional conditions for KILL session as needed, including `SELECT`, `UPDATE`, `DELETE`, `INSERT`, and `REPLACE` options.
   
      6. **SQL template**: When you select **SQL template** in **Additional KILL conditions**, enter the relevant information as needed in the **Enter SQL text as sample** area of the SQL template, and click **Generate SQL templates**.
   
   3. Click **OK**.
   
   4. In **Confirm Kill?**  Confirm the session information to be killed in the pop\-up window.
   
   5. Click **OK**.
   
   
   </Tab>
   <Tab zoneid="zLT7ZoCUL3" title="Persistent Kill">
   <TabTitle>Persistent Kill</TabTitle>
   
   1. Click **Persistent Kill**.
   
   2. In the **Persistent Kill session ** dialog box, configure the following parameters:
   
      1. **SQL type**: Check the SQL statement types that need to be continuously killed as required, including **SELECT**, **UPDATE**, **DELETE**, and **INSERT**.
   
      2. **Node Type**: Check the node types to be persistently killed as needed, including **Primary node** and **Read\-only node**.
   
      3. **SQL execution time**: Set the time to execute the Kill session when the SQL statement execution time exceeds the specified time limit as required. The default value is 1, with a valid range of 1~9,999 seconds (s).
   
      4. **Task duration**: Set the duration for which the persistent Kill task will remain active. The task will automatically stop once the specified duration is reached. The default value is 1, with a valid range of 1~99,999,999. You can also manually stop the persistent Kill session task.
   
   3. Click **OK**.
   
   
   </Tab>
   </Tabs>
   


<span id=".55u45YWz5pON5L2c"></span>
### Related operation

After successfully creating a persistent Kill task, you can perform the following operations in the **Kill task list**:


* View Kill tasks: In the **Kill task list** dialog box, view the **Task ID**, **Task status**, **SQL type**, **Node type**, **SQL execution time**, **Creator**, **Start Time**, **remaining effective time (s)** , and other information of the target task.

   **Task status ** includes **Running**, **Completed ** , **Terminated ** , **Deletion failed ** and **Termination failed**.

* Terminate a running task: In the **Kill task list ** dialog box, click **Terminate ** in the **Actions**column of the target task.

* Delete a task:

   * Delete a task that has ** Terminated** or **Completed**: click **Delete** in the **Actions** column of the target task.

   * To delete a task in the running status: Click  **...**  in the ** Actions** column of the target task. \> **Delete**.


<span id="SvVMQUkB"></span>
## Enable/disable session snapshot

Starting from 2025.12.05, session snapshots for all newly created instances in DBW are disabled by default. If you need to enable session snapshots, you can do so in the instance list or in the session management and transaction and lock sections of the instance.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Enabling the snapshot feature will periodically collect instance\-related information, which introduces additional overhead to the instance.</div>


* <div data-tips="true" data-tips-type="default">The default collection frequency is 30 seconds.</div>


* <div data-tips="true" data-tips-type="default">Collection tasks are executed serially; that is, a new collection will not start until the previous one has completed.</div>


* <div data-tips="true" data-tips-type="default">After enabling or disabling the snapshot feature, the data collection tasks will be adjusted within a few minutes.</div>


* <div data-tips="true" data-tips-type="default">After the snapshot feature is disabled, historical data is retained for up to 30 days.</div>


* <div data-tips="true" data-tips-type="default">The aggregation session and hotspot analysis functions in session management both rely on session snapshot data. Therefore, to use the instance's aggregation session or hotspot analysis functions normally, enable session snapshots for the instance.</div>


* <div data-tips="true" data-tips-type="default">Qwen3.7\-MaxIf the backoff strategy is enabled for the instance, the system may skip certain collection points when high database load causes collection timeouts. In this case, you can refer to the last collection record prior to the skip for diagnosis.</div>



The methods to enable or disable session snapshots are as follows.


<Tabs>
<Tab zoneid="Izk4On6omL" title="Set in Session management">
<TabTitle>Set in Session management</TabTitle>

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the top menu bar in the upper\-right corner of the **Observation and diagnosis** page, switch the database type.

   Switch the database type to RDS for MySQL.

5. In the upper\-left corner of the **Observation and diagnosis** page, click the drop\-down icon to select the target instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can also switch to the target instance by searching for the instance ID.   </div>
   

6. On the **Observation and diagnosis** page, click **Session management**.

7. On the **Session management** tab, click **MySQL engine**.

8. In the **Aggregation session** or **Real\-time session information** tab area, click the switch for **Session snapshot**.

9. In the **Snapshot settings** dialog, you can enable or disable session snapshots and transaction and lock snapshots for the current instance.

   
   |**Parameter** |**Set** |
   |---|---|
   |**Session snapshot** |Enable or disable session snapshots as needed.<br><br><br>* Enable: Click **Enable** to enable session snapshot for the current instance.<br><br>* Disable: Click **Disable** to disable session snapshot for the current instance. |
   |**Collection backoff**<br><br> |Collection backoff is a self\-protection mechanism that ensures instance performance and business stability.<br><br>Once enabled, if an instance anomaly causes collection failures or prolonged collections (where a single collection takes over 1 second), this strategy will automatically activate to gradually reduce the collection frequency, and progressively restore it to normal once the instance recovers. While delivering monitoring capabilities, it minimizes the performance impact on database instances. The values are as follows:<br><br><br>* **Yes**: Enables collection backoff. Collection backoff can only be enabled when session snapshot is enabled.<br><br>* **No**: Disables collection backoff. |
   

10. Click **OK**.


</Tab>
<Tab zoneid="ceaP1SrYkN" title="Set in Instance list">
<TabTitle>Set in Instance list</TabTitle>

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, click **Instance list**.

4. On the **Instance list** page, click the pencil icon under the **Snapshot collection** column of the target instance.

5. In the **Snapshot settings** dialog box, you can enable or disable session snapshot and transaction and lock snapshots for the current instance.

   
   |**Parameter** |**Set** |
   |---|---|
   |**Session snapshot** |Enable or disable session snapshot as needed.<br><br><br>* Enable: Click **Enable** to enable session snapshot for the current instance.<br><br>* Disable: Click **Disable** to disable session snapshot for the current instance. |
   |**Collection backoff**<br><br> |Collection backoff is a self\-protection mechanism that ensures instance performance and business stability.<br><br>Once enabled, if an instance anomaly causes collection failures or prolonged collections (where a single collection takes over 1 second), this strategy will automatically activate to gradually reduce the collection frequency, and progressively restore it to normal once the instance recovers. While delivering monitoring capabilities, it minimizes the performance impact on database instances. The values are as follows:<br><br><br>* **Yes**: Enables collection backoff. Collection backoff can only be enabled when session snapshot is enabled.<br><br>* **No**: Disables collection backoff. |
   

6. Click **OK**.


</Tab>
</Tabs>


<span id="SvVMQUkB"></span>
## Download session snapshot

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">In the export history pop\-up window, you can view historical export tasks and download exported files.</div>


* <div data-tips="true" data-tips-type="default">Download files are retained for 1 day. After they are expired, the download link will automatically become invalid. Save the files to your local computer in time.</div>


* <div data-tips="true" data-tips-type="default">When exporting snapshot information, a maximum of 10,000 pieces of data can be exported at a time.</div>


* <div data-tips="true" data-tips-type="default">Session snapshot files downloaded by the system are compressed in the <code>.gz</code> (Gzip) format. For macOS users, please extract the downloaded file using the steps below:</div>


   * <div data-tips="true" data-tips-type="default">Decompress using the built\-in gzip or gunzip command\-line tools:Open the Terminal and run the gzip or gunzip commands provided by the system to extract the files. The command format is <code>gzip -d your_filename.gz</code> or <code>gunzip your_filename.gz</code>.</div>


   * <div data-tips="true" data-tips-type="default">To decompress the file using the tar tool: Download and install the tar tool to decompress the file. The command format is <code>tar -xz --force-local -f file_name.gz</code>.</div>


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the top menu bar in the upper\-right corner of the **Observation and diagnosis** page, switch the database type.

   Switch the database type to RDS for MySQL.

5. In the upper\-left corner of the **Observation and diagnosis** page, click the drop\-down icon to select the target instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can also switch to the target instance by searching for the instance ID.   </div>
   

   6. On the **Observation and diagnosis** page, click **Session management**.

7. On the **Session management** tab, click **MySQL engine**.

8. In the **Real\-time session information** tab area, click **Session snapshot list**.

   
   <Tabs>
   <Tab zoneid="DEz9GgymMT" title="Export Session Details">
   <TabTitle>Export Session Details</TabTitle>
   
   1. On the **Session snapshot list** control panel, click **Download Snapshot** and select **Export session details**.
   
   2. In the **Export Session Details** pop\-up window, set the following parameters.
   
      
      |**Parameter** |**Description** |
      |---|---|
      |**File format** |The supported file formats are **CSV** or **JSON**. |
      |**Export range** |**Select** the **Session snapshot** **Export range** as needed. The current support Customize, Past 2 hours, Past 12 hours and **Past 24 hours**. |
      |**Custom time period** |Select the time frame for exporting the session snapshot.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter can be set when <strong>Export range</strong> is set to <strong>Custom</strong>.</div><br> |
      
   
   
   
   
   
   </Tab>
   <Tab zoneid="W63rFRH8Cg" title="Export the current snapshot point">
   <TabTitle>Export the current snapshot point</TabTitle>
   
   1. In the **Session snapshot list** control panel, select the snapshot time point.
   
   2. In the **Session information** area, click the download icon.
   
      You can filter target session information by session type, Process ID, User name, Host, Database name, Command type, Duration, State, or Execute statement.
   
   3. In the **Export the current snapshot point** pop\-up window, select the file format.
   
      The supported file formats are **csv** or **json**.
   
   
   </Tab>
   </Tabs>
   

9. Click **OK**.

10. In the **Export history** dialog box, select the target task whose **Status** is **Generated**, and click **Download file** in the **Actions** column.
