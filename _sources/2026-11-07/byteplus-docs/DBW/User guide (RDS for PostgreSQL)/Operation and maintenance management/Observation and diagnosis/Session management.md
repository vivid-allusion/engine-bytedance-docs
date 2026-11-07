---
title: "Session management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/session-management"
---

This topic describes how to view instance session statistics and real\-time sessions through the session management function of DBW.

## Prerequisite

* An instance and account for RDS for PostgreSQL have been created, and the instance status is running. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance) and [Creating an account](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_and_managing_an_account).

* If the target instance has security control enabled, you need to apply for operation and maintenance read\-only or read/write permissions for the current account. For more information, refer to [Enabling instance security control (RDS for PostgreSQL)](https://docs.byteplus.com/en/docs/DBW/enabling-security-control), and [Applying for operation permissions (RDS for PostgreSQL)](https://docs.byteplus.com/en/docs/DBW/Create_operation_permission_ticket).

## Precautions

* When you access session management under operation observability, the IP address of the DBW backend service host is automatically added to the allowlist of the corresponding product.

* When you access session management via **Operation observability** on the left navigation bar, the session information of the first instance in the instance list is displayed by default. You can also access the **Session management** tab for a specific instance by clicking **Operation observability** in the **Actions** column on the **Instance list** page.

* While using the session management feature, avoid modifying instance configurations, as this may prevent normal display of session information.

* Starting from 2025.12.05, the session snapshot for all newly created instances in Database Workshop DBW is disabled by default. If you need to enable session snapshots, you can enable them in the instance list or within the instance's session management or transaction and lock sections. The session snapshot for existing instances is enabled.

   * Enabling the snapshot function for an instance will periodically collect related instance information. The default collection frequency is 30 seconds and cannot be modified.

   * The aggregation session and hotspot analysis functions in session management both rely on session snapshot data. Therefore, to use the instance's aggregation session or hotspot analysis functions normally, enable session snapshots for the instance.

   * After enabling/disabling the snapshot function, it will take effect within a few minutes.

   * After disabling the snapshot function, historical snapshot data can be retained for up to 30 days.

## View a session

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the Observation and diagnosis page, select the instance type and target instance on the **Session management** tab.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **RDS for PostgreSQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **Session management** tab, click Engine.

6. On the engine tab, you can view the following information in different areas.

   * Session statistics: In the **Monitoring information** area, you can view session statistics of the instance, including **Total sessions**, **Active sessions**, **CPU usage**, **Top 5 users**, **Top 5 IP sources**, and **Top 5 databases**.

   * Session details: Session details include real\-time sessions, session snapshots, aggregated sessions, and hotspot analysis, as described below.

      **Real-time session**

In the **Real\-time session** tab, you can view the instance's real\-time sessions, including active sessions and all sessions, as follows:

      * **View session details**: In this tab, you can view each session's **Process ID**, **Username**, **Host**, **Database name**, **Command type**, **Duration**, **State**, **Execute statement**, **Node type**, and **Node ID** for active or real\-time sessions, where the duration is the duration in current status.

      * **Terminate sessions**: You can terminate sessions as needed. For detailed operations, see  [KILL session](https://docs.byteplus.com/en/docs/DBW/session-management?TagIDs=2&lang=en#hSSyQyvU).

      * **Filter sessions**: Filter qualified instance sessions as needed based on **Active sessions** or **All sessions** from the **Session type** drop\-down list.

      **Session snapshot**

Session snapshots display session information for an instance at specific historical points in time, helping you troubleshoot issues after the fact, capture fleeting anomalies, and identify slow queries and SQL tuning opportunities.

      On the **Session snapshot** tab, you can enable, disable, view, and download sessions.

      **Enable/disable session snapshot**

Starting from 2025.12.05, session snapshots for all newly created instances in DBW are disabled by default. If you need to enable session snapshots, you can do so in the instance list or in the session management and transaction and lock sections of the instance.

      > **tip**

      * > Enabling the snapshot function for the instance will periodically collect instance\-related information, with the default collection frequency set to 30 seconds and cannot be modified.

      * > The aggregation session and hotspot analysis functions in session management both rely on session snapshot data. Therefore, to use the instance's aggregation session or hotspot analysis functions normally, enable session snapshots for the instance.

      * > After enabling/disabling the snapshot function, it will take effect within a few minutes.

      * > After disabling snapshot, historical snapshot data can be retained for up to 30 days.

      The methods to enable or disable session snapshots are as follows.

      * Set session snapshots on the session management page

         1. On the **Session details** tab in the **Session snapshot** area, enable the **Automatic collection** switch.

         2. In the **Snapshot settings** dialog box, you can enable or disable session snapshots for the current instance. The parameters are as follows.

            |**Parameter** |**Set** |
            |---|---|
            |**Session snapshot** |Enable or disable session snapshots as needed.<br><br><br>* Enable: Click **Enable** to enable session snapshot for the current instance.<br><br>* Disable: Click **Disable** to disable session snapshot for the current instance. |
            |**Collection backoff**<br><br> |Collection backoff is a self\-protection mechanism that ensures instance performance and business stability.<br><br>Once enabled, if an instance anomaly causes collection failures or prolonged collections (where a single collection takes over 1 second), this strategy will automatically activate to gradually reduce the collection frequency, and progressively restore it to normal once the instance recovers. While delivering monitoring capabilities, it minimizes the performance impact on database instances. The values are as follows:<br><br><br>* **Yes**: Enables collection backoff. Collection backoff can only be enabled when session snapshot is enabled.<br><br>* **No**: Disables collection backoff. |

         3. Click **OK**

      * Set session snapshots on the Instance list page

         1. Log on to the [DBW console](https://console.byteplus.com/dbw).

         2. On the top menu bar, select the region.

         3. On the left navigation bar, click **Instance list**.

         4. On the **Instance list** page, click the pencil icon under the **Snapshot collection** column of the target instance.

         5. In the **Snapshot settings** dialog box, you can enable or disable the session snapshot for the current instance.

            |**Parameter** |**Set** |
            |---|---|
            |**Session snapshot** |Enable or disable session snapshots as needed.<br><br><br>* Enable: Click **Enable** to enable session snapshot for the current instance.<br><br>* Disable: Click **Disable** to disable session snapshot for the current instance. |
            |**Collection backoff**<br><br> |Collection backoff is a self\-protection mechanism that ensures instance performance and business stability.<br><br>Once enabled, if an instance anomaly causes collection failures or prolonged collections (where a single collection takes over 1 second), this strategy will automatically activate to gradually reduce the collection frequency, and progressively restore it to normal once the instance recovers. While delivering monitoring capabilities, it minimizes the performance impact on database instances. The values are as follows:<br><br><br>* **Yes**: Enables collection backoff. Collection backoff can only be enabled when session snapshot is enabled.<br><br>* **No**: Disables collection backoff. |

         6. Click **OK**.

      **View session snapshot information**

1. In the **Session details** area's **Session snapshot** tab, select the node and time frame as needed.

      2. Select a target snapshot point from the snapshot history on the left, and the corresponding **Session details** and **Snapshot point engine information** will be displayed on the right.

         * **View snapshot details**: In the **Session details** area on the right, switch the session type to **All sessions** or **Active session** to view Process ID, Snapshot acquisition time, Username, Host, Database name, Command type, Duration, State, Execute statement, and Rate limiting operations. To save the snapshot to your local device, click the download snapshot icon in the upper\-right corner of the page.

         * **Snapshot point engine information**: Displays the database engine running status at the current snapshot point, including engine type, name, state, and Engine Monitor Output. Click the copy icon in the upper\-right corner to copy the engine information of the current snapshot point.

      For the InnoDB engine, this area displays the InnoDB Monitor output, which can be used to analyze background threads and engine running status.

      **Download session snapshot**

> **tip**

      * > You can view historical export tasks and download exported files in the export history pop\-up window.

      * > Download files are retained for 1 day. After they are expired, the download link will automatically become invalid. Save the files to your local computer in time.

      * > When exporting snapshot information, a maximum of 10,000 pieces of data can be exported at a time.

      In the **Session details** area, on the **Session snapshot** tab, click **Download snapshot** and select the download type as needed.

      * Export Session Details

         1. Click **Export session details**.

         2. In the **Export session details** dialog box, configure the following parameters.

            |**Parameter** |**Description** |
            |---|---|
            |**File format** |The supported file formats are **CSV** or **JSON**. |
            |**Export range** |**Select** the **Session snapshot** **Export range** as needed. The current support Customize, Past 2 hours, Past 12 hours and **Past 24 hours**. |
            |**Custom time period** |Select the time frame for exporting the session snapshot.<br><br>> **tip**<br><br><br>> This parameter can be set when **Export range** is set to **Custom**.<br> |

         3. Click **OK**.

      * Export history

         1. Click **Export history**.

         2. In the **Export history** dialog box, click **Download file** in the **Actions** column of the target task.

         3. Click **Close**.

      > **tip**

      > To save a snapshot to your local computer, click the target snapshot point, and then click the download snapshot icon in the upper\-right corner of the page.

      **Aggregation session**

Aggregation sessions summarize current active sessions by SQL template, helping you quickly identify concurrency, execution time, and resource consumption of similar SQL statements, as well as issues such as concentrated writes, slow queries, or abnormal connections. If unexpected write sessions are found, you can further locate the source and terminate the session.

      On the **Aggregation session** pane, perform the following:

      > **tip**

      > Aggregation sessions only count session information for active sessions.

      * View the details of the aggregation session: You can review all aggregation sessions for the instance within a specified time range, with support for querying sessions up to the last 24 hours. The aggregation session information includes **SQL template**, **Database name**, **Execution time**, **Average execution time(s)** , **Maximum execution time(s)**  and **Total execution time(s)** . You can also click the target SQL template under the **SQL template** column to view session details.

      * Filter sessions: Enter session keywords in the **Search keywords, such as SELECT ** text box, to query eligible session information.

## Kill session

DBW provides the `kill` session function, which can be used to terminate specific processes or sessions, maintaining system stability and efficiency. DBW provides methods including KILL selected sessions and KILL all sessions to help you effectively control system resources and process behavior.

### Precautions

* Multiple persistent Kill session tasks are independent of each other (an "or" relationship) and do not interact.

* Terminated sessions cannot be recovered. Proceed with caution.

### Procedure

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

3. On the top menu bar, select the region.

4. On the Observation and diagnosis page, select the instance type and target instance on the **Session management** tab.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **RDS for PostgreSQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **Session information ** sub\-tab, click **Real\-time session**.

6. On the **Real\-time session** pane, select the KILL session mode as needed.

   |**KILL session mode** |**Procedure** |
   |---|---|
   |**KILL selected session** |1. Check the target session ID and click **KILL selected session**.<br><br>2. In **Confirm KILL?**  dialog box, confirm the session information that needs to be killed, and click **OK** |
   |**KILL all sessions** |1. Click **KILL all sessions**.<br><br>2. In **Confirm KILL?**  dialog box, confirm the session information that needs to be killed, and click **OK** |

##
