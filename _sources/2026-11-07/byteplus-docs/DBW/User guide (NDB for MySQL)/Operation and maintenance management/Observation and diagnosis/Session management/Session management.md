---
title: "Session management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Session_information_management"
---

Database Workshop (DBW) provides session management to view session statistics and real\-time session information of the primary and read\-only nodes of instances. This topic describes the precautions and steps of session management.

## Prerequisite

* An NDB for MySQL instance and an account have been created, and the Instance state is Running. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1) and [Creating an account](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_and_deleting_accounts#.5Yib5bu66LSm5Y-3).

* If the target instance has security control enabled, you need to apply for operation and maintenance read\-only or read/write permissions for the current account. For more information, see [Enable security control for NDB for MySQL instances](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control) and [Apply for operation permissions related to NDB for MySQL](https://docs.byteplus.com/en/docs/DBW/Creating_an_operation_permission_ticket).

## Precautions

* The **Real\-time session** tab does not display the connections of internal accounts (such as `root`, `repl`, `byte_rds_agent`, `byte_rds_backup`, `byte_rds_proxy`) and DBW internal accounts (such as `dbw_admin`) for NDB for MySQL instances.

* When you access session management under operation observability, the IP address of the DBW backend service host is automatically added to the allowlist of the corresponding product. The allowlist naming format varies by instance type, The naming format of the allowlist is `dbw_unique_****_****` or `byte_ndb_****_***_*dbw`.

* While using the session management feature, avoid modifying instance configurations, as this may prevent normal display of session information.

* Session snapshot files downloaded by the system are compressed in the `.gz` (Gzip) format. For macOS users, please extract the downloaded file using the steps below:

   * Decompress using the built\-in gzip or gunzip command\-line tools:Open the Terminal and run the gzip or gunzip commands provided by the system to extract the files. The command format is `gzip -d your_filename.gz` or `gunzip your_filename.gz`.

   * To decompress the file using the tar tool: Download and install the tar tool to decompress the file. The command format is `tar -xz --force-local -f file_name.gz`.

* Starting from 2025.12.05, session snapshots for all new instances are disabled by default. To enable session snapshots, you can enable them in the instance list or within session management, transaction and lock management of the instance. Session snapshots for existing instances are enabled.

   * Enabling the snapshot feature will periodically collect instance\-related information, which introduces additional overhead to the instance.

   * The default collection frequency is 30 seconds.

   * Collection tasks are executed serially; that is, a new collection will not start until the previous one has completed.

   * After enabling or disabling the snapshot feature, the data collection tasks will be adjusted within a few minutes.

   * After the snapshot feature is disabled, historical data is retained for up to 30 days.

   * The aggregation session and hotspot analysis functions in session management both rely on session snapshot data. Therefore, to use the instance's aggregation session or hotspot analysis functions normally, enable session snapshots for the instance.

   * Qwen3.7\-MaxIf the backoff strategy is enabled for the instance, the system may skip certain collection points when high database load causes collection timeouts. In this case, you can refer to the last collection record prior to the skip for diagnosis.

## View a session

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

3. On the top menu bar, select the region.

4. On the **Observation and diagnosis** page, click **Session management**.

   1. In the drop\-down list in the upper\-right corner of the page, select the **NDB for MySQL** database type.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. Select **Session management** \> **Session information**, and select the required **node ID** to view session information for different nodes, as shown below:

   * Session statistics: In the **Monitoring information** area, you can view session statistics for each node ID in the instance, including **total sessions**, **active sessions**, **CPU usage**, **Top 5 users**, **Top 5 IP sources**, and **Top 5 databases**.

   * Session details: Session details include real\-time sessions, session snapshots, aggregation sessions, and hotspot analysis, as shown below:

      **Real-time session**

On the **Real\-time session** tab, you can view the instance's real\-time sessions, including active sessions and all sessions, as follows:

      * **View session details**: In this tab, you can view each session's **Process ID**, **Username**, **Host**, **Database name**, **Command type**, **Duration**, **State**, **Execute statement**, **Node type**, and **Node ID**, where the duration is the duration in current status.

      * **Terminate sessions**: You can terminate sessions as needed. For detailed operations, see KILL session.

      * **Filter sessions**: Filter qualified instance sessions as needed based on **Active sessions** or **All sessions** from the **Session type** drop\-down list.

      * **SQL throttling**: Controls the volume of database requests and SQL concurrency to ensure service availability. For more information about SQL throttling, see  [SQL throttling management](https://docs.byteplus.com/en/docs/DBW/SQL_throttling_management?lang=en).

      * **SQL optimization**: Click **SQL optimization** in the **Actions** column of the target session, and view **index optimization** suggestions and **SQL rewrite** suggestions in the **SQL optimization suggestions** dialog box.

      **Session snapshot**

Session snapshot displays session information of an instance at a specific historical point in time, helping you troubleshoot issues after they occur, capture fleeting anomalies, and identify slow queries and SQL tuning opportunities.

      On the **Session snapshot** tab, you can enable, disable, view, and download sessions.

      **Enable/disable session snapshot**

Starting from 2025.12.05, session snapshots for all newly created instances in DBW are disabled by default. If you need to enable session snapshots, you can do so in the instance list or in the session management and transaction and lock sections of the instance.

      > **tip**

      * > Enabling the snapshot feature will periodically collect instance\-related information, which introduces additional overhead to the instance.

      * > The default collection frequency is 30 seconds.

      * > Collection tasks are executed serially; that is, a new collection will not start until the previous one has completed.

      * > After the collection backoff feature is enabled, if collection fails due to an instance anomaly, the backoff policy is automatically triggered to gradually reduce the collection frequency until normal operation resumes.

      * > After enabling or disabling the snapshot feature, the data collection tasks will be adjusted within a few minutes.

      * > After the snapshot feature is disabled, historical data is retained for up to 30 days.

      * > The aggregation session and hotspot analysis functions in session management both rely on session snapshot data. Therefore, to use the instance's aggregation session or hotspot analysis functions normally, enable session snapshots for the instance.

      * > Qwen3.7\-MaxIf the backoff strategy is enabled for the instance, the system may skip certain collection points when high database load causes collection timeouts. In this case, you can refer to the last collection record prior to the skip for diagnosis.

      * Configure session snapshots on the Session management page.

         1. In the **Session details** area, on the **Session snapshot** tab, click the **Auto collection** switch.

         2. In the **Snapshot settings** dialog box, you can enable or disable the session snapshot for the current instance, Parameters are as follows.

            |**Parameter** |**Set** |
            |---|---|
            |**Session snapshot** |Enable or disable session snapshots as needed.<br><br><br>* Enable: Click **Enable** to enable session snapshot for the current instance.<br><br>* Disable: Click **Disable** to disable session snapshot for the current instance. |
            |**Collection backoff**<br><br> |Collection backoff is a self\-protection mechanism that ensures instance performance and business stability.<br><br>Once enabled, if an instance anomaly causes collection failures or prolonged collections (where a single collection takes over 1 second), this strategy will automatically activate to gradually reduce the collection frequency, and progressively restore it to normal once the instance recovers. While delivering monitoring capabilities, it minimizes the performance impact on database instances. The values are as follows:<br><br><br>* **Yes**: Enables collection backoff. Collection backoff can only be enabled when session snapshot is enabled.<br><br>* **No**: Disables collection backoff. |

         3. Click **OK**.

      * Set session snapshots on the instance list page

         1. Log on to the [DBW console](https://console.byteplus.com/dbw).

         2. On the top menu bar, select the region.

         3. On the left navigation bar, click **Instance list**.

         4. On the **Instance list** page, click the pencil icon under the **Snapshot collection** column of the target instance.

            |**Parameter** |**Set** |
            |---|---|
            |**Session snapshot** |Enable or disable session snapshots as needed.<br><br><br>* Enable: Click **Enable** to enable session snapshot for the current instance.<br><br>* Disable: Click **Disable** to disable session snapshot for the current instance. |
            |**Collection backoff**<br><br> |Collection backoff is a self\-protection mechanism that ensures instance performance and business stability.<br><br>Once enabled, if an instance anomaly causes collection failures or prolonged collections (where a single collection takes over 1 second), this strategy will automatically activate to gradually reduce the collection frequency, and progressively restore it to normal once the instance recovers. While delivering monitoring capabilities, it minimizes the performance impact on database instances. The values are as follows:<br><br><br>* **Yes**: Enables collection backoff. Collection backoff can only be enabled when session snapshot is enabled.<br><br>* **No**: Disables collection backoff. |

         5. In the **Snapshot settings** dialog box, you can enable or disable the session snapshot for the current instance.

      **View session snapshot information**

1. In the **session snapshot** tab of the **session details** area, select the node and time range as needed.

      2. Select the target snapshot point in the snapshot history on the left. The right side displays the **session details** and **snapshot point engine information** for that snapshot point.

         * **View snapshot details**: In the **session details** area on the right, you can switch the session type to **all sessions** or **active sessions**, and view information including process ID, snapshot acquisition time, username, host, database name, command type, duration, state, execute statement, and rate limiting actions. To save the snapshot of the snapshot point locally, click the download snapshot icon in the upper\-right corner of the page.

         * **Snapshot point engine information**: Displays the database engine running state for the current snapshot point, including engine type, name, state, and Engine Monitor Output. Click the copy icon in the upper\-right corner to copy the engine information of the current snapshot point.

      For the InnoDB engine, this area displays the InnoDB Monitor output, which can be used to assist in analyzing background threads and engine running state.

      **Download session snapshot**

> **tip**

      * > You can view historical export tasks and download exported files in the export history pop\-up window.

      * > Download files are retained for 1 day. After they are expired, the download link will automatically become invalid. Save the files to your local computer in time.

      * > When exporting snapshot information, a maximum of 10,000 pieces of data can be exported at a time.

      * > Session snapshot files downloaded by the system are compressed in the `.gz` (Gzip) format. For macOS users, please extract the downloaded file using the steps below:

         * > Decompress using the built\-in gzip or gunzip command\-line tools:Open the Terminal and run the gzip or gunzip commands provided by the system to extract the files. The command format is `gzip -d your_file_name.gz` or `gunzip your_file_name.gz`.

         * > Use the tar tool: Download and install the tar tool to extract the file. The command format is `tar -xz --force-local -f file_name.gz`.

      In the **Session details** area, on the **Session snapshot** tab, click **Download snapshot** and select the download type as needed.

      * Export Session Details

         1. Click **Export session details**.

         2. In the **Export session details** dialog, configure the following parameters.

            |**Parameter** |**Description** |
            |---|---|
            |**File format** |The supported file formats are **CSV** or **JSON**. |
            |**Export range** |Select the range of session snapshots to download on demand. Currently, **Customize**, **Past 2 hours**, **Past 12 hours**, and **Past 24 hours** are supported. |
            |**Custom time period** |Select the time frame for exporting the session snapshot.<br><br>> **tip**<br><br><br>> This parameter can be set when **Export range** is set to **Custom**.<br> |

         3. Click **OK**.

      * Export history

         1. Click **Export history**.

         2. In the **Export history** dialog, click **Download file** in the **Actions** column of the target task.

         3. Click **Close**.

      > **tip**

      > To save a snapshot to your local computer, click the target snapshot point, and then click the download snapshot icon in the upper\-right corner of the page.

      **Aggregation session**

Aggregation session summarizes current active sessions by SQL template, helping you quickly identify concurrency, execution time, and resource consumption for similar SQL, as well as issues such as concentrated writes, slow queries, or abnormal connections. If unexpected write sessions are found, you can further locate the source and terminate the session.

      On the **Aggregation session** pane, perform the following:

      Aggregation sessions only count session information for active sessions.

      * View the details of the aggregation session: You can review all aggregation sessions for the instance within a specified time range, with support for querying sessions up to the last 24 hours. The aggregation session information includes **SQL template**, **Database name**, **Execution time**, **Average execution time(s)** , **Maximum execution time(s)**  and **Total execution time(s)** . You can also click the target SQL template under the **SQL template** column to view session details.

      * Filter sessions: Enter session keywords in the **Search keywords, such as SELECT ** text box, to query eligible session information.

      * Other operations:

         * Rate limiting: Click **Actions** \> **Rate limiting** for the target SQL template to apply keyword\-based or template\-based rate limiting. Use SQL rate limiting to control database request volume and SQL concurrency, ensuring service availability. For details on SQL throttling configuration, refer to [SQL throttling management](https://docs.byteplus.com/en/docs/DBW/SQL_throttling_management?lang=en).

         * View SQL optimization suggestions: Click **Actions** \> **SQL optimization** for the target SQL template to view suggestions, including **index optimization suggestions** and **SQL rewrite suggestions**.

      **Hotspot analysis**

Hotspot analysis provides in\-depth analysis of your interaction behavior and hotspot areas, helping you optimize system performance and improve user experience.

      In the **Hotspot analysis** tab, select the time frame and SQL type as needed to view information such as **SQL text**, **execution times**, and **execution rate**. Hotspot information for up to 24 hours can be queried. Additionally, click **Rate limiting** in the **Actions** column of the target SQL text to apply keyword\-based rate limiting. For details, see  [SQL Throttling Management](https://docs.byteplus.com/en/docs/DBW/SQL_throttling_management?lang=en).
