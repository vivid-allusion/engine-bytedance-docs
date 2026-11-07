---
title: "Command operations"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Command_operations"
---

This article describes how to execute SQL commands on the NDB for MySQL data interaction platform.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A BytePlus account has been registered and completed verification. For the detailed method, refer to [Sign up and verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* As per the regulations in the Chinese mainland, you must have completed real name registration before you can activate and use cloud services in regions in the Chinese mainland through BytePlus. For more details, refer to [Real name registration](https://docs.byteplus.com/en/docs/byteplus-platform/docs-real-name-registration).

* You have [created an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1) and [created an account](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_database_and_account).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The account you create must have the corresponding permissions for querying and modifying the corresponding database.   </div>
   

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The USE statement is not supported: Using USE database in a batch of multiple SQL statements will have no effect. Select the target database using the database switcher at the top of the console.

* Null value convention: Field values can be NULL (null values), but must not be explicitly written as the string "null".

* Result set limits: A single query can return a maximum of 3,000 rows, with the total data size not exceeding 10 MB (10,485,760 bytes). If either limit is exceeded, the results will be automatically truncated.

* Object display limit: In the left\-side object browser, each category, such as tables, views, triggers, stored procedures, functions, and events, displays a maximum of 1,000 items.

* SQL statement limits: A single execution supports up to 10,000 SQL statements, with a total length not exceeding 100 KB.

* Online DDL is not supported: Data Interaction Console does not support lock\-free schema changes. Executing DDL (e.g., ALTER TABLE) may block DML/DQL operations. Use with caution.

* Operation suggestions

   * Avoid latency sensitive tasks: DBW cannot guarantee optimal performance for queries executed in the SQL console, and it is not recommended to run latency critical business SQL statements here.

   * Transaction execution behavior: The underlying physical connection for each tab may change. When executing a transaction, please select and submit all statements at once to avoid connection switching and transaction failure caused by executing statements one by one.

   * Timing for schema change operations: DDL operations such as CREATE and DROP may impact production workloads. It is strongly recommended to perform them during off\-peak business hours.

   * Tab management: The SQL window supports a maximum of 10 open tabs simultaneously. To ensure system stability, please promptly close any tabs that are no longer in use.

* Function description

   * Keyboard shortcut support: Press Cmd + Enter (Mac) or Ctrl + Enter (Windows/Linux) to quickly execute the current SQL statement.

   * Session management: Right\-click on a tab to quickly close the current session, other sessions, all sessions to the right, or all sessions.

   * Object browsing: In the left\-hand interactive panel, you can switch databases and object types (such as tables, views, stored procedures, etc.) as needed to conveniently view metadata information.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [NDB for MySQL Data interaction platform](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql).

2. In the command execution area of the **data interaction platform** page, edit the SQL statement, and then click **Execute**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also select the target SQL statement, and then click <strong>Execute</strong> to execute some statements.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The command execution area now supports generating standard SQL with natural language. You can enter a piece of natural language and press Enter. The format is <code>-- Natural Language</code>. For example, <code>-- Generate a statement to create a table</code>. At this time, the system will automatically generate a statement to create a table, such as <code>CREATE TABLE new_table LIKE test-new</code>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The command editor in SQL window has built\-in shortcut templates and command completion functions. When entering SQL commands, parameters, or functions in the command editor, you can select the target command or template from the recommended command list to enhance your work efficiency.   </div>
   

   After the execution is successful, you can perform the following operations:

   * View operation logs and execution results in the Execution record area and the execution results in the Execution result area. You can also click **Close all** to close the Execution result tab.

   * Export result set: In the execution result area, for successful results, you can click **Export all** or **Export result set** to save the execution results locally. For more information, please see [Export result set](https://docs.byteplus.com/en/docs/DBW/Creating_a_SQL_result_set_export_task#Nq4EYj3M).

   * Copy result set: In the Execution result area, for successfully executed results, select the target information and right\-click, then choose **Copy** in the right\-click menu to copy the current execution result data.

   * Favorite SQL: In the upper right corner of the session window, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1653cb4aef411ee36c305340aa15245a.png) </span>icon. On the **Favorite SQL** control panel, set the following parameter information, and then click **OK**.

      * **SQL name**: Customize the name of the SQL statement (cannot be empty).

      * **Effective scope**: Select the scope in which the favorite SQL statement takes effect. Currently, it is supported to choose whether it applies within **Current database** or **Current instance**.

      * **SQL statement**: You can modify the SQL text to be favorited in the SQL statement area.

   * To view the favorite SQL statement, click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ea80a67c40ff91675b90aaa1b20469ee.png) </span>icon. On the **Favorites** control panel, you can **View**, **Edit**, and **Delete** the favorite SQL statement.

   * To view the SQL execution record, click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0dc8b1b2bb2c62d9d0abc49afeeef830.png) </span>icon. On the execution history control panel, you can filter the SQL statement executed in all windows within the specified time as required. After successful execution, you can view the output on the **Execution result** pane, view the execution history in the **Execution record**, or click **Clear record** to delete the execution history.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[DataExecCommands](https://docs.byteplus.com/en/docs/DBW/dataexeccommands) |Call the DataExecCommands interfaceAPI to execute an SQL command. |
|[DataSessionKeepAlive](https://docs.byteplus.com/en/docs/DBW/datasessionkeepalive) |Call the DataSessionKeepAlive API to keep an SQL session alive. |
|[DataCloseSession](https://docs.byteplus.com/en/docs/DBW/dataclosesession) |Call the DataCloseSession API to close an SQL session. |
|[DataCancelExec](https://docs.byteplus.com/en/docs/DBW/datacancelexec) |Call the DataCancelExec API to cancel SQL execution. |
