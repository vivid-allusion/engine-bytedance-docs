---
title: "Enabling or disabling read/write separation"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/enabling_read-write_splitting"
---

After you enable read/write separation for an instance, you can configure it to forward read requests to read\-only nodes to reduce the read workload on the primary node. This topic describes how to enable read/write separation for a database.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

After you enable read/write separation, requests are forwarded as follows:


* **Sent only to the primary node**

   * INSERT、UPDATE、DELETE、SELECT FOR UPDATE、SELECT LOCK IN SHARE MODE。

   * All user operations (such as CREATE/DROP/GRANT USER).

   * All DDL operations (such as creating or deleting tables and databases, or altering table structures).

   * All requests within transactions (including SET autocommit=0).

   * LOCK\-related statements.

   * User\-customized functions.

   * Stored procedures.

   * EXECUTE statements.

   * [Multi Statements](https://dev.mysql.com/doc/internals/en/multi-statement.html)。

   * Requests that use temporary tables.

   * SELECT last_insert_id()。

   * All queries and changes to user variables.

   * KILL (KILL in SQL statements, not the KILL command).

   * Locking functions in query statements.

* **Sent to the read\-only node or primary node**

   * SELECT statements outside of a transaction.

   * SHOW VARIABLES statements outside of a transaction.

   * COM_STMT_EXECUTE commands.

* **Always sent to all nodes**

   * Changes to all system variables.

   * USE commands.

   * SHOW PROCESSLIST (The proxy returns aggregated PROCESSLIST information for all nodes).

   * COM_STMT_PREPARE commands.

   * Commands such as COM_CHANGE_USER, COM_QUIT, and COM_SET_OPTION.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Only the Read/Write mode proxy connection endpoints of double\-node and multiple\-node instances support this feature.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* The database proxy for the instance is **Enabled**. To enable it, refer to [Enable database proxy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enable_database_agent).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the project to which the instance belongs is not set, this operation should select the project as <strong>All resources</strong>.</div>



3. On the left navigation bar, click **Instances** to go to the **Instances** page.

4. On the **Instances** page, click the name of the target instance to enter the instance.Instances

5. On the target instance page, click **Connectivity**.

6. On the **Connectivity** tab, in the **Endpoints** list, click **Edit** in the **Actions** column of the target connection endpoint to go to the **Modify endpoint** page.

7. On the **Modify endpoint** page, in the **Read/Write separation configuration** section, turn on the **Read/Write separation** switch.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To disable the read/write separation feature, turn off the <strong>Read/Write separation</strong> switch and click <strong>OK</strong>. No other actions are needed.   </div>
   

8. Set the read\-only latency threshold. The value range for this setting is 1 to 3600s. After the threshold is set, read\-only requests are not assigned to read\-only nodes whose latency exceeds the specified threshold.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Only the Default_endpoint and customized Read/Write Endpoints support setting the read\-only latency threshold.Default_endpointDefault_endpoint   </div>
   

9. Select the assignment mode for the Read/Write splitting strategy. The automatic assignment mode is used by default. For more details, refer to [Setting the read/write separation policy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_read-write_splitting_policies).

10. Click **OK**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[ModifyDBEndpoint](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbendpoint) |Call the ModifyDBEndpoint API to modify an Endpoint. |
