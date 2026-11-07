---
title: "Introduction to SQL window"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Introduction_to_SQL_window"
---

In the Data interaction platform of Database Workshop DBW, executing commands enables full lifecycle management of tables, including creating, viewing, and modifying table data. This article uses MySQL database as an example to introduce the features and usage of the SQL window.

> **tip**

> The functionality of the SQL window varies depending on the database type, subject to actual conditions. This article takes the MySQL database as an example to introduce the related functions of the SQL window.

## Precautions

* Tab Management: The SQL window supports up to 10 tabs. To avoid excessive resource consumption, promptly close unused tabs. Right\-click any tab to quickly close the current, other, right\-side, or all sessions.

* Result Set Limit: A single query returns a maximum of 3,000 rows or 10 MB (10,485,760 bytes) of data. Exceeding either limit triggers automatic truncation.

* SQL execution limits: A single execution supports up to 10,000 SQL statements, with a total length not exceeding 100 KB.

* Transaction execution suggestion: Each tab does not guarantee the use of the same physical connection. Please select and execute complete transaction statements at once to avoid connection switching and transaction failure caused by running them individually.

* Performance and risk notice:

   * DBW cannot guarantee optimal query performance in the SQL window. It is not recommended to execute latency\-sensitive critical tasks here.

   * DDL/DML operations such as creation or deletion may impact online services. Please exercise caution during off\-peak business hours.

## Prerequisite

You have [created an Instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1) and [created an Account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_databases_and_accounts#.5Yib5bu66LSm5Y-3) and have the Query permission for the target database or Table.

## Introduction to SQL window

1. [Log in to the RDS for MySQL console](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql).

2. On the **Data interaction platform** page, you can experience the functions in the SQL window in each function area of the SQL window.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_59c12b201b57abf98d7f67d5a7e350a1.png)

|**No.**  |**Region** |**Description** |
|---|---|---|
|1 |Visual operation area |Visually manage tables, views, triggers, functions, and events.<br><br><br>* **Tables**<br><br>   View all tables in the database, including fields, field types, and indexes. Click the function icon next to a target table or right\-click the table to quickly query, view details, edit structure, rename, import, export, copy structure, create tables, AI\-generated tables, AI\-inserted data, or delete tables. For more information, see [Table management](https://docs.byteplus.com/en/docs/DBW/table-management-for-mysql).<br><br>* **Views**<br><br>   Supports creating, editing, and deleting views. For more information, see [View management](https://docs.byteplus.com/en/docs/DBW/view-management-for-mysql).<br><br>* **Triggers**<br><br>   Supports creating, querying, editing, and deleting triggers. For more information, see [Trigger management](https://docs.byteplus.com/en/docs/DBW/trigger-management-for-mysql).<br><br>* **Stored procedures**<br><br>   Supports creating stored procedures, executing stored procedures, editing stored procedures, and deleting stored procedures. For more information, see [Stored procedure management](https://docs.byteplus.com/en/docs/DBW/stored-procedure-management-for-mysql).<br><br>* **Functions**<br><br>   Supports creating functions, executing functions, editing functions, and deleting functions. For more information, see [Function management](https://docs.byteplus.com/en/docs/DBW/function-management-for-mysql).<br><br>* **Event**<br><br>   Supports creating events, editing events, and deleting events. For more information, see [Event management](https://docs.byteplus.com/en/docs/DBW/event-management-for-mysql). |
|2 |Command execution area |In the command execution area, edit the SQL statement, and then click **Execute**. For more information, see [Command operations](https://docs.byteplus.com/en/docs/DBW/executing-commands-for-mysql).<br><br><br>* **Execute SQL statements**: After entering the SQL statement, click **Execute** to execute the selected SQL statement.<br><br>* **Execution plan**: View how the data interaction platform plans to execute the entered SQL statement.<br><br>* **Format SQL statement**: Select the SQL statement, click **Format**, and the data interaction platform will optimize the format of the selected SQL statement.<br><br>* **View shortcut guide**: Click the **Shortcut guide** icon in the upper\-right corner of the session **window** to view the shortcut keys for each function.<br><br>* **Favorite SQL**: Click the **Favorite SQL** icon in the upper\-right corner of the session window. On the **Favorite SQL** control panel, set the following parameter information, and then click **OK**.<br><br>* **View the favorite SQL statements**: Click the **Favorites** icon in the upper\-right corner of the session window. On the **Favorites** control panel, you can **view**, **edit**, and **delete** the favorite SQL statements.<br><br>* **View SQL execution record**: Click the **Execution history** icon in the upper\-right corner of the session window. On the execution history control panel, you can filter the SQL statements executed in all windows within the specified time as needed. After successful execution, you can view the output on the **Execution result** pane, view the execution history in the **Execution record**, or click **Clear record** to delete the execution history. |
|3 |Execution result area |After executing the SQL command, you can view the execution history and execution results in the execution result area. In the Execution history area, you can view the SQL statement execution history, and in the Execution result area, you can view the command execution results.<br><br>> **tip**<br><br><br>> SQL execution history is retained for 30 days by default.<br><br><br>Additionally, when the SQL execution result is in table format, you can export the SQL result set, copy SQL results, as well as add, delete, or modify rows in the SQL results.<br><br><br>* **Export SQL result set**: Export the execution results of SQL statements. For more information, see [Export SQL result set](https://docs.byteplus.com/en/docs/DBW/creating-a-sql-result-set-export-task-for-mysql).<br><br>* **Copy SQL result set**: Copy the execution results of SQL statements. Select the SQL result set to copy, right\-click, and use the context menu to copy the selected SQL result set.<br><br>* **Add rows to SQL result set**: Click **Add row** below the execution result area to insert a blank row at the bottom of the SQL result set.<br><br>* **Delete rows from SQL result set**: In the SQL result set, select the row to delete, right\-click, and use the context menu to remove it; or click **Delete row** below the execution result area to delete the selected row.<br><br>* **Modify SQL result set**: Double\-click the cell to edit in the SQL result table to directly modify the data. |
|4 |Function extension area |The following are the extended functions in the SQL window.<br><br><br>* **DB intelligent assistant**: the DB intelligent assistant provides comprehensive support when handling SQL\-related tasks. Whether in the SQL console or an assisted AI assistant environment, it plays a crucial role. For more information, see [DB intelligent assistant](https://docs.byteplus.com/en/docs/DBW/database-intelligent-assistant-dbcopilot#l1wclKau).<br><br>* **Import/Export**: Supports exporting data in the database, and also supports importing data into the database. For more information, see [Import and export data](https://docs.byteplus.com/en/docs/DBW/data-import-and-export-for-mysql).<br><br>* **Observation and diagnosis**: Click **Observation and diagnosis** to open the observation and diagnosis page of the current instance. For more information, see [DBCopilot Diagnosis assistant](https://docs.byteplus.com/en/docs/DBW/database-intelligent-assistant-dbcopilot#TQnXzafh) and [Observation and diagnosis](https://docs.byteplus.com/en/docs/DBW/observation-diagnosis-for-mysql).<br><br>* **Instance details**: Click **Instance details** to open the instance information page of the current instance. For more information about the instance, see [View Instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_instance_details).<br><br>* **Log out**: Click **Log out** to exit the login of the current instance workbench. |

## Related APIs

|**API** |**Description** |
|---|---|
|[DataConnectInstance](https://docs.byteplus.com/en/docs/DBW/dataconnectinstance) |Call the DataConnectInstance API to connect to the instance. |
|[DataExecCommands](https://docs.byteplus.com/en/docs/DBW/dataexeccommands) |Call the DataExecCommands interfaceAPI to execute an SQL command. |
|[DataSessionKeepAlive](https://docs.byteplus.com/en/docs/DBW/datasessionkeepalive) |Call the DataSessionKeepAlive API to keep an SQL session alive. |
|[DataCloseSession](https://docs.byteplus.com/en/docs/DBW/dataclosesession) |Call the DataCloseSession API to close an SQL session. |
|[DataCancelExec](https://docs.byteplus.com/en/docs/DBW/datacancelexec) |Call the DataCancelExec API to cancel SQL execution. |
