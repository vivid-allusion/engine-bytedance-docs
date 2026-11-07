---
title: "Command operations"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/command-operation-for-PG"
---

This topic describes how to execute SQL commands for an RDS for PostgreSQL instance in the data interaction platform.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have created an instance and account. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/create_instance) and [Creating an account](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_and_managing_an_account).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Make sure that the account you use has sufficient permissions.</div>


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* SQL execution limits

   * The USE statement is not supported in multiple SQL statements. Otherwise, the USE statement does not take effect. We recommend that you switch databases in the console.

   * A single query can return a maximum of 3,000 rows, with the total data size not exceeding 10 MB (10,485,760 bytes). If either limit is exceeded, the results will be automatically truncated.

   * Online DDL is not supported. Executing DDL may block DML or DQL operations. Proceed with caution during off\-peak hours.

   * It is not recommended to execute latency\-sensitive tasks, as DBW cannot guarantee optimal performance.

   * The current SQL window editor does not support parsing PostgreSQL custom composite types. Visual modifications to composite fields may generate incorrect SQL. It is advised to manually edit the correct SQL via the console.

   * A single execution supports up to 10,000 SQL statements, with a total length not exceeding 100 KB.

* Tab and connection management

   * A maximum of 10 tabs can be opened. Close unused tabs promptly to reduce resource usage.

   * Right\-click a tab to quickly close the current, other, right\-side, or all sessions.

   * The physical connection for each tab is not fixed. When executing transactions, select all statements and execute them at once to avoid connection switches and transaction failures caused by executing statements one by one.

* Data and object browsing

   * Supports switching databases and object types (tables, views, triggers, functions, etc.), with a maximum display of 1000 items per type.

   * Database field values can be NULL (empty), but cannot be set to the string 'null'.

* Quick actions and permissions

   * Use Cmd + Enter (Mac) or Ctrl + Enter (Windows) to quickly execute the selected SQL.

   * After an IAM user logs in, the remaining execution times and query rows are displayed in the upper\-right corner. If adjustments are needed, you can contact the administrator to help set appropriate execution times and query rows. For detailed steps, refer to Editing a user.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. You have logged on to the [Data interaction platform for RDS for PostgreSQL](https://docs.byteplus.com/en/docs/DBW/log-in-database-interaction-platform-for-PG).

2. In the **SQL query** area of the data interaction platform, write an SQL Command, and then click **Execute**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also select the target SQL statement, and then click <strong>Execute</strong> to execute some statements.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The command editor in the SQL window has built\-in quick templates and command completion features. When entering SQL commands, parameters, or functions in the command editor, you can select the target command or template from the recommended command list to enhance your work efficiency.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The command execution area now supports generating standard SQL with natural language. You can enter a piece of natural language and press Enter. The format is \-\- Natural Language. For example, “\-\- generate a create table statement,” and the system will automatically generate a create table statement. Press Enter to formally generate the statement. For more information, please refer to <a href="https://docs.byteplus.com/en/docs/DBW/database-intelligent-assistant-dbcopilot#l1wclKau">DB AI assistant</a>.   </div>
   

   After the execution is successful, you can perform the following operations:

   * View operation logs and execution results in the Execution record area and the execution results in the Execution result area. You can also click **Close all** to close the Execution result tab.

   * Export result set: In the execution result area, for successful results, you can click **Export all** or **Export result set** to save the execution results locally. For more information, please see [Export result set](https://docs.byteplus.com/en/docs/DBW/Exporting_an_SQL_result_set).

   * Copy result set: In the Execution result area, for successfully executed results, select the target information and right\-click, then choose **Copy** in the right\-click menu to copy the current execution result data.

   * Favorite SQL: In the upper right corner of the session window, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1653cb4aef411ee36c305340aa15245a.png) </span>icon. On the **Favorite SQL** control panel, set the following parameter information, and then click **OK**.

      * **SQL name**: Customize the name of the SQL statement (cannot be empty).

      * **Effective scope**: Select the scope in which the favorite SQL statement takes effect. Currently, it is supported to choose whether it applies within **Current database** or **Current instance**.

      * **SQL statement**: You can modify the SQL text to be favorited in the SQL statement area.

   * To view the favorite SQL statement, click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ea80a67c40ff91675b90aaa1b20469ee.png) </span>icon. On the **Favorites** control panel, you can **View**, **Edit**, and **Delete** the favorite SQL statement.

   * To view the SQL execution record, click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0dc8b1b2bb2c62d9d0abc49afeeef830.png) </span>icon. On the execution history control panel, you can filter the SQL statement executed in all windows within the specified time as required. After successful execution, you can view the output on the **Execution result** pane, view the execution history in the **Execution record**, or click **Clear record** to delete the execution history.
