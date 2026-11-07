---
title: "Command operations"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/command-opeartions_"
---

This topic describes how to execute commands for RDS for SQL Server in the data interaction platform of the DBW console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance has been created and the instance state is Running. For detailed steps, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide).

* A database account has been created. For detailed steps, refer to [Creating and managing an account](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-and-managing-account).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Limitations

   * The USE statement is not supported: when executing multiple SQL statements in batch, USE database will not take effect. Select the target database using the database switcher at the top of the console.

   * Result set limit: A single query returns a maximum of 3,000 rows of data, with a total size not exceeding 10 MB (10,485,760 bytes). If either limit is exceeded, the results will be automatically truncated.

   * Object display limit: In the left\-side object browser, each category, such as tables, views, triggers, stored procedures, and functions, displays a maximum of 1,000 items.

   * Null value convention: Field values can be NULL (null values), but must not be explicitly written as the string "null".

   * SQL statement limits: A single execution supports up to 10,000 SQL statements, with a total length not exceeding 100 KB.

* Operation suggestions

   * Avoid latency sensitive tasks: DBW cannot guarantee optimal performance for queries executed in the SQL console, and it is not recommended to run latency critical business SQL statements here.

   * Transaction execution behavior: The underlying physical connection for each tab may change. When executing a transaction, please select and submit all statements at once to avoid connection switching and transaction failure caused by executing statements individually.

   * Timing of schema changes: DDL operations such as CREATE and DROP may impact production workloads. It is strongly recommended to perform them during off\-peak business hours.

   * Tab management: The SQL window supports a maximum of 10 open tabs simultaneously. To ensure system stability, please promptly close any tabs that are no longer in use.

* Function description

   * Keyboard shortcut support: Press Cmd + Enter (Mac) or Ctrl + Enter (Windows/Linux) to quickly execute the current SQL statement.

   * Session management: Right\-click on a tab to quickly close the current session, other sessions, all sessions to the right, or all sessions.

   * Object browsing: In the left\-hand interactive panel, you can switch databases and object types (such as tables, views, stored procedures, etc.) as needed to conveniently view metadata information.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [data interaction platform for RDS for SQL Server](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-rds-for-sql-server).

2. In the command execution area of the data interaction platform page, edit the SQL statement, and then click **Execute**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also select the target SQL statement, and then click <strong>Execute</strong> to execute some statements.   </div>
   

   After the execution is successful, you can perform the following operations:

   * View operation logs and execution results in the Execution record area and the execution results in the Execution result area. You can also click **Close all** to close the Execution result tab.

   * Favorite SQL: In the upper right corner of the session window, click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1653cb4aef411ee36c305340aa15245a.png) </span>icon. On the **Favorite SQL** control panel, set the following parameter information, and then click **OK**.

      * **SQL name**: Customize the name of the SQL statement (cannot be empty).

      * **Effective scope**: Select the scope in which the favorite SQL statement takes effect. Currently, it is supported to choose whether it applies within **Current database** or **Current instance**.

      * **SQL statement**: You can modify the SQL text to be favorited in the SQL statement area.

   * To view the favorite SQL statement, click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ea80a67c40ff91675b90aaa1b20469ee.png) </span>icon. On the **Favorites** control panel, you can **View**, **Edit**, and **Delete** the favorite SQL statement.

   * To view the SQL execution record, click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0dc8b1b2bb2c62d9d0abc49afeeef830.png) </span>icon. On the execution history control panel, you can filter the SQL statement executed in all windows within the specified time as required. After successful execution, you can view the output on the **Execution result** pane, view the execution history in the **Execution record**, or click **Clear record** to delete the execution history.
