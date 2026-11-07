---
title: "Command operations"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/executing-commands-for-mongodb"
---

This topic explains how to execute commands in the Document Database for MongoDB data interaction platform.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A MongoDB instance has been created and is in the running state. For detailed steps, see [Creating an instance](https://docs.byteplus.com/en/docs/mongodb/creating_an_instance).

* A database account has been created with permissions to execute the corresponding commands. For detailed steps, refer to [Creating an account](https://docs.byteplus.com/en/docs/mongodb/create-account).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The query results can display up to 3,000 rows, with a single\-row data limit of 3 MB and a result set limit of 10 MB.

* Up to 10 tabs can be opened in the SQL window. To avoid affecting the running of the database, close some tabs in time.

* In the SQL window, right\-click the tab page to close the current session, close another session, close right session, or close all sessions.

* DBW cannot guarantee optimal performance for SQL executed in the data interaction console.  Therefore, it is not recommended to execute SQL tasks that are sensitive to response latency in the data interaction console.

* In the SQL window, each Tab page does not correspond to a unique physical connection. Therefore, when executing transactions, it is recommended to select all transaction statements and execute them at once; avoid executing them one by one as this may cause physical connection changes and invalidate subsequent execution statements.

* The creation, deletion, and other operations you perform may affect the online business operation. It is recommended to perform them during off\-peak hours.

* You can switch databases and collections as needed in the operable area of the data interaction console. A maximum of 100 databases or collections are supported.

* When executing multiple commands, all commands will be executed, but only the last executed command result is displayed. If you need to view the execution result of a specific command, you must execute that command individually.

* You can execute the specified SQL statement through the `CMD + Enter` shortcut.

* Commands such as the `use`, `set`, `it`, and `show` series cannot be executed together with other commands. To execute, run them individually.

* When executing database commands, if the command fails and prompts insufficient permissions, refer to [permissions](https://docs.byteplus.com/en/docs/mongodb/modifying_account_privileges) [permissions](https://docs.byteplus.com/en/docs/mongodb/modifying_account_privileges) [permissions](https://docs.byteplus.com/en/docs/mongodb/modifying_account_privileges) to adjust the database permissions of the login account.

* Currently, the following commands are not supported for execution in the Document Database for MongoDB data interaction platform. If you require support for these commands, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support, or use open\-source tools such as [Compass](https://github.com/mongodb-js/compass/releases?page=5), [DataGrip](https://www.jetbrains.com/datagrip/download/?section=mac), or [Studio 3T](https://robomongo.org/download.php) to connect to the BytePlus Document Database for MongoDB.

   
   |**Command form** |**Subcommands** |
   |---|---|
   |db.runCommand({$command}) |`shutdownServer`, `applyOps`, `replSetAbortPrimaryCatchUp`, `replSetFreeze`, `replSetGetConfig`, `replSetInitiate`, `replSetMaintenance`, `replSetReconfig`, `replSetStepDown`, `replSetSyncFrom`, `replSetAbortPrimaryCatchUp`, a`ddShard`, `balancerStart`, b`alancerStop`, `checkShardingIndex`, `moveChunk`, `movePrimary`, `mergeChunks`, `removeShard`, `setShardVersion`, `split`, `splitVector`, `unsetSharding`, `print` |
   |db.adminCommand({$command}) |`clone`, `cloneDatabase`, `cloneCollection`, `cloneCollectionAsCapped`, `compact`, `logRotate`, `reIndex`, `shutdown` |
   |db.$command |`db.shutdownServer()`, `db.cloneDatabase("hostname")`, `db.cloneCollection("test")` |
   |rs.$command |`rs.freeze`, `rs.initiate`, `rs.reconfig`, `rs.stepDown`, `rs.add`, `rs.addArb`, `rs.syncFrom` |
   |sh.$command |`addShard`, `moveChunk`, `movePrimary`, `mergeChunks`, `removeShard`, `setShardVersion`, `split`, `splitVector`, `unsetSharding` |
   


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to [the data interaction console of Document Database for MongoDB](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-documentdb-for-mongodb).

2. In the command execution area of the **Data interaction platform** page, edit the SQL statement, and then click **Execute**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also select the target SQL statement, and then click <strong>Execute</strong> to execute some statements.   </div>
   

   After the execution is successful, you can perform the following operations:

   * **View execution records and execution results**: View execution records in the execution record area and view the command's execution results in the execution results area. You can also click **Close all** to close the Execution result tab.

   * **Download execution results**: In the execution results area, for successfully executed results, you can click **Download** to save the execution results locally as a result.json file.

   * **Copy execution results**: In the execution results area, for successfully executed results, you can click **Copy** to copy the current execution result data.

   * **Favorite SQL**: In the upper right corner of the session window, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1653cb4aef411ee36c305340aa15245a.png) </span>icon. On the **Favorite SQL** control panel, set the following parameter information, and then click **OK**.

      * **SQL name**: Customize the name of the SQL statement (cannot be empty).

      * **Effective scope**: Select the scope in which the favorite SQL statement takes effect. Currently, it is supported to choose whether it applies within **Current database** or **Current instance**.

      * **SQL statement**: You can modify the SQL text to be favorited in the SQL statement area.

   * **To view the favorite SQL statement**, click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ea80a67c40ff91675b90aaa1b20469ee.png) </span>icon. On the **Favorites** control panel, you can **View**, **Edit**, and **Delete** the favorite SQL statement.

   * **To view the SQL execution record**, click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0dc8b1b2bb2c62d9d0abc49afeeef830.png) </span>icon. On the execution history control panel, you can filter the SQL statement executed in all windows within the specified time as required. After successful execution, you can view the output on the **Execution result** pane, view the execution history in the **Execution record**, or click **Clear record** to delete the execution history.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[DataExecCommands](https://docs.byteplus.com/en/docs/DBW/dataexeccommands) |Call the DataExecCommands interfaceAPI to execute an SQL command. |
|[DataSessionKeepAlive](https://docs.byteplus.com/en/docs/DBW/datasessionkeepalive) |Call the DataSessionKeepAlive API to keep an SQL session alive. |
|[DataCloseSession](https://docs.byteplus.com/en/docs/DBW/dataclosesession) |Call the DataCloseSession API to close an SQL session. |
|[DataCancelExec](https://docs.byteplus.com/en/docs/DBW/datacancelexec) |Call the DataCancelExec interface to cancel SQL execution. |
