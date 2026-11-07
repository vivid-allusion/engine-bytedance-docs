---
title: "Command operations"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/executing-commands-for-redis"
---

This topic describes how to execute statement commands on the data interaction platform for Cache for Redis.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have[ created an instance](https://docs.byteplus.com/en/docs/redis/create-instance) and [set the Default account password](https://docs.byteplus.com/en/docs/redis/create-manage-account).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Query statements can display a maximum of 3,000 rows.

* You can open up to 10 tabs in the SQL window. To avoid affecting the database operation, close some tabs in time.

* In the SQL window, right\-click the tab page to close the current session, close another session, close right session, or close all sessions.

* Currently, the execution of `SUBSCRIBE`, `PUBLISH`, `HyperLogLog`, and `MULTI` commands is not supported. Otherwise, an error will occur in execution.

* You can execute the specified SQL statement through the `CMD + Enter` shortcut.

* DBW cannot guarantee optimal performance for SQL executed in the data interaction console.  Therefore, it is not recommended to execute SQL tasks that are sensitive to response latency in the data interaction console.

* In the SQL window, each Tab page does not correspond to a unique physical connection. Therefore, when executing transactions, it is recommended to select all transaction statements and execute them at once; avoid executing them one by one as this may cause physical connection changes and invalidate subsequent execution statements.

* The current Console only supports the Resp2 protocol, with Resp3 protocol not yet available.

* The creation, deletion, and other operations you perform may affect the online business operation. It is recommended to perform them during off\-peak hours.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [data interaction platform for Cache for Redis](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-cache-for-redis).

2. On the **Data interaction platform** page, click the plus icon to open a new command line tab.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9901be69184accfd4b33a1df0bf62633.png) </span>

3. In the command execution area (No. 1) of the **Command window_{number}**  tab, edit the statement to create a key value, and then click **Execute(F8)**  or press **F8**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also select the target SQL statement, and then click <strong>Execute</strong> to execute some statements.   </div>
   

   After the execution is successful, you can perform the following operations:

   * To view the execution result, check the running result of the command in the execution result area.

   * Clear execution record: In the execution record area, click **Clear** to clear all Execution records.

   * Favorite SQL: In the upper right corner of the session window, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1653cb4aef411ee36c305340aa15245a.png) </span>icon. On the **Favorite SQL** control panel, set the following parameter information, and then click **OK**.

      * **SQL name**: Customize the name of the SQL statement (cannot be empty).

      * **Effective scope**: Select the scope in which the favorite SQL statement takes effect. Currently, it is supported to choose whether it applies within **Current database** or **Current instance**.

      * **SQL statement**: You can modify the SQL text to be favorited in the SQL statement area.

   * To view the favorite SQL statement, click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ea80a67c40ff91675b90aaa1b20469ee.png) </span>icon. On the **Favorites** control panel, you can **View**, **Edit**, and **Delete** the favorite SQL statement.

   * To view the SQL execution record, click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0dc8b1b2bb2c62d9d0abc49afeeef830.png) </span>icon. On the execution history control panel, you can filter the SQL statement executed in all windows within the specified time as required.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[DataExecCommands](https://docs.byteplus.com/en/docs/DBW/dataexeccommands) |Call the DataExecCommands interfaceAPI to execute an SQL command. |
|[DataSessionKeepAlive](https://docs.byteplus.com/en/docs/DBW/datasessionkeepalive) |Call the DataSessionKeepAlive API to keep an SQL session alive. |
|[DataCloseSession](https://docs.byteplus.com/en/docs/DBW/dataclosesession) |Call the DataCloseSession API to close an SQL session. |
|[DataCancelExec](https://docs.byteplus.com/en/docs/DBW/datacancelexec) |Call the DataCancelExec interface to cancel SQL execution. |
