---
title: "Kill session"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/kill-session-for-vedb-mysql"
---

DBW provides the `kill` session function, which can be used to terminate specific processes or sessions, maintaining system stability and efficiency. DBW offers methods including KILL selected sessions, KILL all sessions, KILL matching sessions, and persistent KILL sessions to help you effectively control system resources and process behavior.

### Precautions

* A maximum of 5 conditional KILL tasks can run simultaneously.

* The execution cycle of continuous KILL tasks is 1 second. SQL statements that execute in less than 1 second may not be killed. Multiple persistent Kill session tasks are independent of each other (an "or" relationship) and do not interact.

* KILL sessions cannot be recovered and should be performed with caution.

### Procedure

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

3. On the top menu bar, select the region.

4. On the **Observation and diagnosis** page, click **Session management**.

   * In the drop\-down list in the upper\-right corner of the page, select the **NDB for MySQL** database type.

   * In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. Select **Session management** \> **Session information**, and select the **Node ID** of the sessions to kill as needed.

6. In the **Session details** area, click **Real\-time session**.

7. On the **Real\-time session** tab, select the KILL session method as needed.

   **KILL selected session**

1. Check the target session ID and click **KILL selected session**.

   2. In **Confirm KILL?**  dialog box, confirm the session information that needs to be killed, and click **OK**

   **KILL all sessions**

1. Click **KILL all sessions**.

   2. In **Confirm KILL?**  dialog box, confirm the session information that needs to be killed, and click **OK**

   **KILL matching sessions**

1. Click **KILL matching sessions**.

   2. In the **KILL matching sessions** dialog box, configure the following parameters.

      * **IP address**: Enter IP addresses as needed. Up to 10 IP addresses are supported, separated by commas (,).

      * **Username**: Enter username as needed. Up to 10 usernames are supported, separated by commas (,).

      * **Database name**: Enter database name as needed. Up to 10 database names are supported, separated by commas (,).

      * **Additional KILL conditions**: You can select **SQL type**, **SQL template**, and **Null** KILL additional conditions.

         * **SQL type**: When you select **SQL type** in **Additional KILL conditions**, you can select the SQL additional conditions for KILL session as needed, including `SELECT`, `UPDATE`, `DELETE`, `INSERT`, and `REPLACE` options.

         * **SQL template**: When you select **SQL template** in **Additional KILL conditions**, enter the relevant information as needed in the **Enter SQL text as sample** area of the SQL template, and click **Generate SQL templates**.

   3. Click **OK**.

   4. In **Confirm Kill?**  Confirm the session information to be killed in the pop\-up window.

   5. Click **OK**.

   **Persistent Kill**

1. Click **Persistent Kill**.

   2. In the **Persistent Kill session ** dialog box, configure the following parameters:

      * **SQL type**: Check the SQL statement types that need to be continuously killed as required, including **SELECT**, **UPDATE**, **DELETE**, and **INSERT**.

      * **Node Type**: Check the node types to be persistently killed as needed, including **Primary node** and **Read\-only node**.

      * **SQL execution time**: Set the time to execute the Kill session when the SQL statement execution time exceeds the specified time limit as required. The default value is 1, with a valid range of 1~9,999 seconds (s).

      * **Task duration**: Set the duration for which the persistent Kill task will remain active. The task will automatically stop once the specified duration is reached. The default value is 1, with a valid range of 1~99,999,999. You can also manually stop the persistent Kill session task.

   3. Click **OK**.

### View Kill tasks

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

3. On the top menu bar, select the region.

4. On the **Observation and diagnosis** page, click **Session management**.

   * In the drop\-down list in the upper\-right corner of the page, select the **NDB for MySQL** database type.

   * In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **Session management** tab, click **Kill task**.

6. On the **Kill task** sub\-tab, view Kill tasks, including **Task ID**, **Task status**, **SQL type**, **Node type**, **SQL execution time**, **Creator**, **Start time**, and **Remaining effective time (s)** .

   **Task status ** includes **Running**, **Completed ** , **Terminated ** , **Deletion failed ** and **Termination failed**.

## Terminate a Kill task

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

3. On the top menu bar, select the region.

4. On the **Observation and diagnosis** page, click **Session management**.

   * In the drop\-down list in the upper\-right corner of the page, select the **NDB for MySQL** database type.

   * In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **Session management** tab, click **Kill task**.

6. On the **Kill task** sub\-tab, click **Terminate** in the **Actions** column of the target task.

## Delete Kill task

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

3. On the top menu bar, select the region.

4. On the **Observation and diagnosis** page, click **Session management**.

   * In the drop\-down list in the upper\-right corner of the page, select the **NDB for MySQL** database type.

   * In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **Session management** tab, click **Kill task**.

6. On the **Kill task** sub\-tab, click **Delete** in the **Actions** column of the target task.
