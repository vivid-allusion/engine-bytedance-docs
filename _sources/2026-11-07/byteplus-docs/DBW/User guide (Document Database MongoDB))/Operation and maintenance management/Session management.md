---
title: "Session management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/MongDB_Session_management"
---

This topic describes how to view instance session statistics and real\-time sessions through the session management function of DBW.

## Prerequisite

An instance and account for Document Database for MongoDB have been created, and the instance status is running. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/mongodb/create-instance) and [Creating an account](https://docs.byteplus.com/en/docs/mongodb/create-account).

## Precautions

* The session statistics refresh interval is set to 5 seconds by default. You can choose to disable auto\-refresh or change the interval to 10 or 15 seconds.

* The Real\-time session tab does not display connections from internal accounts of Document Database for MongoDB (e.g., `root`) and DBW (e.g., `dbw_admin`).

* When you access session management under operation observability, the IP address of the DBW backend service host is automatically added to the allowlist of the corresponding product. The naming format of the allowlist is `DBW_Sole_Group_Name_For_Mongo_0`.

* When you access session management via **Operation observability** on the left navigation bar, the session information of the first instance in the instance list is displayed by default. You can also access the **Session management** tab for a specific instance by clicking **Operation observability** in the **Actions** column on the **Instance list** page.

* While using the session management feature, avoid modifying instance configurations, as this may prevent normal display of session information.

* Real\-time sessions are statistically derived based on the `currentOp()` method. Among them, active sessions are filtered and statistically derived by setting the `active` parameter to `true` based on this method.

* The session snapshot of all MongoDB instances is disabled by default. If you need to enable session snapshots, you can do so in the instance list or the instance's session management.

   * Enabling the snapshot function for an instance will regularly collect related instance information. The default collection frequency is 30 seconds and can not be modified.

   * The snapshot function will take effect within a few minutes after being enabled or disabled.

   * After disabling snapshot, historical snapshot data can be retained for up to 30 days.

* When the client automatically sends messages like "hello" to obtain replica set status \- a purely background process without actual business operations \- the username field will be empty. No intervention or termination (Kill) is required in such cases.

* For actual business query operations, username information will be displayed, and such sessions can be terminated (Killed).

## View a session

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, switch the instance type and ID.

   * In the upper right corner of the Observation and diagnosis page, switch the instance type to Document Database for MongoDB.

   * In the upper left corner of the Observation and diagnosis page, switch the target instance based on the instance ID or instance name.

5. On the **Session information** tab of the target instance, click **Engine**.

6. On the **Engine** sub\-tab, depending on the instance type, you can select the node ID of a replica set instance or the component and node ID of a sharding set instance to view the session information as follows:

   > **tip**

   > When viewing a sharding set instance, the session and connection information will be displayed as follows:

   * > Session information: When the Mongos component is selected, the local sessions of that Mongos node as well as all Shard sessions in the cluster will be displayed. You can observe instance sessions through Mongos.

   * > Connection information: If the Mongos component is selected, external connections received by this node and internal connections initiated by Mongos will be displayed. You can distinguish between external and internal connections based on details such as IP addresses and ports.

   * **Viewsession statistics**: On the **Session information** tab, you can view **Maximum session execution time**, **Number of sessions longer than 3 seconds**, **Number of queries without Index**, **Top5 IP source statistics**, **Top5 namespaces**, **Overview** (**Total connections**, **Total number of active connections**), **Connection statistics**, and **Connection display**. Connection statistics and connection display are as follows:

      * Connection statistics: On the **Connection statistics** pane, the **IP**, **Active connections**, and **Total connections** of the current connection instance are displayed.

      * Connection display: on the **Connection display** pane, the **Description**, **Connection ID**, **IP:PORT**, and **Active** status of the current connection are displayed.

   * **Session details**: Session details include real\-time sessions and session snapshots, as follows:

      **Real-time session**

On the **Real\-time session** tab, you can select a **Session type** as needed, with options for **Active session** and **All sessions**. You can perform the following operations:

      * View session details: You can view the **Process ID**, **Client side**, **Username**, **Operation type**, **Execute SQL**, **Duration**, **Namespace**, **Execution plan**, **Description**, and **NodeId** of each session in this area. Where **Duration** is the duration in current status.

         > **tip**

         > If the username is empty, it indicates the session is purely background\-automated without actual business operations.

         * View session snapshots: Click **Session snapshot list** to view session details. The session snapshot list displays session information only for the target node ID.

      * Terminate session: Select the target session, click **KILL selected session**, and click **Are you sure to delete?**  dialog box to confirm terminating the target session. You can also click **KILL all sessions** to terminate all sessions.

         > **tip**

         > When you terminate the target session, sessions with the same session ID in all nodes will be deleted and can not be recovered after deletion. Exercise caution when performing this operation.

      **Session snapshot**

Session snapshots display session information of an instance at specific historical points in time, helping you troubleshoot issues after they occur, capture transient anomalies, identify slow queries, and optimize SQL.

      On the **Session snapshot** tab, you can enable, disable, view, and download sessions.

      **Enable/disable session snapshot**

The session snapshot of all MongoDB instances is disabled by default. If you need to enable session snapshots, you can do so in the instance list or the instance's session management.

      > **tip**

      * > Enabling the snapshot function for an instance will regularly collect related instance information. The default collection frequency is 30 seconds and can not be modified.

      * > The snapshot function will take effect within a few minutes after being enabled or disabled.

      * > After disabling snapshot, historical snapshot data can be retained for up to 30 days.

      The methods to enable or disable session snapshots are as follows.

      * Configure session snapshots on the Session management page.

         1. In the **Session details** area, on the **Session snapshot** tab, click the **Auto collection** switch.

         2. In the **Snapshot settings** dialog box, you can enable or disable the session snapshot for the current instance, Parameters are as follows.

            |**Parameter** |**Set** |
            |---|---|
            |**Session snapshot** |Enable or disable session snapshots as needed.<br><br><br>* Enable: Click **Enable** to enable session snapshot for the current instance.<br><br>* Disable: Click **Disable** to disable session snapshot for the current instance. |
            |**Collection backoff**<br><br> |Collection backoff is a self\-protection mechanism that ensures instance performance and business stability.<br><br>Once enabled, if an instance anomaly causes collection failures or prolonged collections (where a single collection takes over 1 second), this strategy will automatically activate to gradually reduce the collection frequency, and progressively restore it to normal once the instance recovers. While delivering monitoring capabilities, it minimizes the performance impact on database instances. The values are as follows:<br><br><br>* **Yes**: Enables collection backoff. Collection backoff can only be enabled when session snapshot is enabled.<br><br>* **No**: Disables collection backoff. |

         3. Click **OK**.

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

1. In the **Session details** area, on the **Session snapshot** tab, select the node and time range as needed.

      2. Select the target snapshot point from the snapshot history on the left. The corresponding **Session details** and **Snapshot point engine information** are displayed on the right.

         * **View snapshot details**: In the **Session details** area on the right, switch the session type to **All sessions** or **Active sessions** to view process ID, snapshot acquisition time, username, host, database name, command type, duration, state, executed statements, and rate limiting actions. To save the snapshot to your local device, click the download snapshot icon in the upper\-right corner of the page.

         * **Snapshot point engine information**: Displays the database engine running state for the current snapshot point, including engine type, name, state, and Engine Monitor Output. Click the copy icon in the upper\-right corner to copy the engine information of the current snapshot point.

      For the InnoDB engine, this area displays the InnoDB Monitor output, which helps analyze background threads and engine running state.

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

      > To save a snapshot to your local device, click the target snapshot point, then click the download snapshot icon in the upper\-right corner of the page.
