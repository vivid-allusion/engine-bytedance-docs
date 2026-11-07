---
title: "Command operations"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Command_operations"
---

In the AI Native BaaS for Supabase, executing commands can achieve the full lifecycle management of modes and tables, including creating mode, editing mode, query mode, as well as creating tables, viewing tables, and changing table data. It also supports the SQL (Text\-to\-SQL) function, which helps you generate standard SQL from natural language and lowers the barrier to SQL writing and learning. This topic introduces how to execute SQL commands in the Data interaction platform.

<span id="qpwDsACy"></span>
## Prerequisites

Workspace and account have been created. For detailed operations, please refer to [Creating a workspace ](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Creating_a_workspace) and [Createing  an account](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Creating_an_account).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Make sure that the account you use has sufficient permissions.</div>


<span id="cgphkxgD"></span>
## Precautions


* When using SQL (Text\-to\-SQL), a small number of conversions of natural language may be inaccurate, and high concurrency may cause performance issues.

* The USE statement is not supported for executing multiple SQL statements. Otherwise, the USE statement will not take effect. You are advised to perform the database switching on the console.

* A maximum of 3,000 lines of query statements are supported.

* The specific values of database records can be empty, but cannot be set to string null.

* In the operable area of the data interaction platform, you can switch the database and object type as needed. For example, details of tables, views, triggers, and functions. Each type supports displaying a maximum of 1,000 items.

* OnlineDDL operations are not supported in the data interaction platform. Executing DDL operations in the data interaction platform may cause DML, DQL, and other operations to be blocked. Use with caution.

* DBW cannot guarantee optimal performance for SQL executed in the data interaction console.  Therefore, it is not recommended to execute SQL tasks that are sensitive to response latency in the data interaction console.

* The creation, deletion, and other operations you perform may affect the online business operation. It is recommended to perform them during off\-peak hours.


<span id="4tutJR9h"></span>
## Procedure


1. Log in to the [AI Native BaaS for Supabase](https://console.byteplus.com/aidap).

2. In the top navigation bar, select the target project and target region.

3. Go to the **SQL query** page of the target database. Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_906ef41b4eb1b26873ff9c3cc9ddbc6d.png)<sub> </sub></span> **SQL query** in the center navigation bar on the page, then click the icon <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span> to the right of the workspace name, branch name, and database name on the top left of the page in turn to select the target workspace, target branch, and target database from the drop\-down list respectively to enter the **SQL query** page of the target database.

4. On the **SQL query** page, you can click **Create SQL query** (when there is no operation window) or<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3b88dd0370b6f86070a41b069df07e03.png) </span>(when there is an operation window) to create a new SQL query window.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can also select the target SQL statement, and then click <strong>Execute</strong> to execute some statements.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The command execution area now supports generating standard SQL with natural language. You can enter a piece of natural language and press Enter. The format is <code>-- Natural Language</code>. For example, “\-\- please create a table,” and the system will automatically generate a create table statement.   </div>
   


After the execution is successful, you can perform the following operations:


* View operation logs and execution results in the Execution record area and the execution results in the Execution result area.

* Favorite SQL: Click the **Favorite SQL** icon in the upper right corner of the session window, set the following parameter information in the **Favorite SQL** control panel, then click **OK**.

   * **SQL name**: Customize the name of the SQL statement (cannot be empty).

   * **Effective scope**: select the scope in which the favorite SQL statement takes effect. Currently, it is supported to choose to take effect in **Current database** and **Current workspace**.

   * **SQL statement**: You can modify the SQL text to be favorited in the SQL statement area.

* View the favorite SQL statements: Click the **Favorites** icon in the upper\-right corner of the session window. On the **Favorites** control panel, you can **view**, **edit**, and **delete** the favorite SQL statements.

* View SQL execution records: in the execution result area, click **Execution history**. In the execution history control panel, you can filter SQL statements executed across all windows within the specified time as needed. After successful execution, you can view the output on the **Execution result** pane, view the execution history in the **Execution record**, or click **Clear record** to delete the execution history.

* Time travel: click the **Time travel** icon in the upper right corner of the session window to enable or disable the Time shuttle function in the popup. After enabling the Time shuttle function, you can set the time frame for time travel (the time frame cannot exceed 24 hours).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After enabling the Time shuttle function, executed SQL statements are based on historical data from execution records, rather than current data.   </div>
