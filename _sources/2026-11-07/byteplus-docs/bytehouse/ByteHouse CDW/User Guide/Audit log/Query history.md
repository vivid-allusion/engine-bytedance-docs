---
title: "Query history"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/sql-audit"
---

ByteHouse Cloud Data Warehouse provides you with query history capabilities and a graphical interface for viewing SQL execution logs. It supports viewing SQL history and running queries, helping you quickly locate and optimize slow queries, troubleshoot errors, audit user behavior to ensure data security, and is suitable for scenarios such as database performance tuning, security compliance auditing, and post\-incident fault tracing, among many other use cases. Meanwhile, ByteHouse also provides a detailed query log table. After enabling the detailed log toggle, you can view the corresponding detailed SQL log table data and further view more granular log data. This tutorial explains how to use the ByteHouse query history feature.

<span id="8504e385"></span>
# Background

The ByteHouse query history feature supports viewing SQL history and running queries. In SQL history, you can view slow SQL queries and error queries, as well as perform precise searches by ID or SQL statement content.

This feature provides comprehensive audit dimensions, including query ID, status, username/ID, effective role, virtual warehouse, start/end time, duration, SQL type, SQL statement, total CPU time, maximum memory usage (Segment), and more. Additionally, this feature also supports a wide range of filter options, making it easy to efficiently analyze SQL execution.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e113f380852f4e19aa158da254a86dd1~tplv-goo7wpa0wc-image.image) </span>

ByteHouse also supports viewing detailed logs. After enabling this feature, ByteHouse will begin collecting data (requires reconnecting to ByteHouse), and will automatically create a database named `bh_system` and a table named `query_log` within the database to record detailed SQL execution log data. You have full permissions for both the database and the table. The default data lifecycle for this table is 7 days. To retain data for a longer period, you can run SQL commands to remove the TTL or modify the TTL time as needed. For operation details, see [Adjust query_log table life cycle](https://docs.byteplus.com/docs/bytehouse/sql-audit#a49d3610).

<span id="eaca3f11"></span>
# Limitations


* Administrators can view all users' SQL audit information, including SQL history, running queries, and detailed logs, while sub\-users can only view the SQL audit information of the current account. Sub\-users who need to view all users' query history information can contact the administrator to be granted global audit log privileges. For details about the operation, refer to [Resource privilege management](https://docs.byteplus.com/docs/bytehouse/resource-privilege-management).

* The "Total CPU time" and "Maximum memory usage (Segment)" display items in the SQL history list are Beta features and require engine version v2.3 or above. To view the corresponding information, submit a ticket or contact the ByteHouse team to obtain allowlist permission.

* Query log is a non\-public feature. To use it, please submit a ticket or contact the ByteHouse team to obtain allowlist permission.


<span id="f7669eff"></span>
# View SQL history and running queries


1. Log in to the ByteHouse Console, click the top **Audit logs**, then click **Query history**. Under the **History** tab, you can view the History Query List. You can filter SQL history using filter criteria. Querying is supported through **Query ID** or **SQL Statement**, which you can select and switch from the dropdown list.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c50fb5444b5948ec996665af5fef46ba~tplv-goo7wpa0wc-image.image) </span>

   1. The SQL history list contains the following information:

      * **Query ID**: The unique ID number of the SQL query.

      * **Status**: Event completion status, such as "success" or "fail". For failed events, you can view specific details using the button on the right.

      * **Active role**: The role type that executes this event.

      * **Virtual warehouse**: Name of the virtual warehouse (VW) for query execution.

      * **CPU Total Duration**: The sum of CPU time consumed by all segments of the virtual warehouse. Because segments can run in parallel, this value may be greater than the query duration.

      * **Max Memory Usage (Segment)** : The maximum memory usage of all segments executed by the virtual warehouse.

      * **Start time**: The date of the event.

      * **End time**: Specific time when the event ends.

      * **Duration**: Event execution duration.

      * **SQL type**: Type of SQL statement to execute, such as CREATE, DROP, INSERT, DELETE, and more.</a i=1\>

      * **SQL Statement**: Content of the executed SQL statement and its dialect type.

   2. Switch to the **Failed queries** tab to quickly locate failed events and query related statuses as needed.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c51fc1cce004af6abb25522611de634~tplv-goo7wpa0wc-image.image) </span>

   3. Switch to the "**Search by ID or SQL**" tab, where you can query using a query ID or SQL statement.

2. Switch to the "**Running query**" tab to view the list of currently running queries. You can view the query ID, start time, virtual warehouse, and SQL statement. You can also use Query ID, SQL Statement, or Virtual warehouse to view currently running queries.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also view the currently running queries by using the SQL command <code>SHOW PROCESSLIST</code>. For usage instructions, see <a href="https://docs.byteplus.com/docs/bytehouse/show-statement#60fb18df">SHOW PROCESSLIST</a>.   </div>
   

<span id="86549d26"></span>
# View detailed log (query_log)

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Detailed log is a non\-public feature. To use it, please submit a ticket or contact the ByteHouse team to obtain allowlist permissions.</div>


After obtaining allowlist permission, you can open the \*\*Enable detailed logging \*\*switch in the upper right corner of the \*\*Query history \*\*page. Once enabled, ByteHouse will create a `query_log` table in the system for you, which is used to write detailed SQL execution log data.


1. Turn on the **Enable detailed logging** switch.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac323bee7c9546adbbd6003add5fcb21~tplv-goo7wpa0wc-image.image) </span>

   After clicking the detailed log button, ByteHouse will obtain your authorization to create the `bh_system` database under your tenant\-environment, and to create a `query_log` table in that database. You will have all privileges on both the database and the table. If the sub user needs to view the query_log, you can contact the administrator to grant data privileges to the sub user. For details, refer to [Data privilege management](https://docs.byteplus.com/docs/bytehouse/docs-permission).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Since ByteHouse continuously writes the SQL logs of the statements you execute into the <code>bh_system.query_log</code> table, any insert, delete, or update operations on this table will affect logging. Add, delete, and modify operations on this table are prohibited except for modifying TTL.   </div>
   

2. View `query_log` table. At the top of the page, you can click **Database** or **SQL worksheet** to view the `query_log` table.

   For example, to view the `query_log` table using the **SQL worksheet**, you can find this table in the `bh_system` database listed under data objects on the left side of the SQL worksheet.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/177500dcdc9b4f67b7827cf4ed36678e~tplv-goo7wpa0wc-image.image) </span>


<span id="a49d3610"></span>
## Adjust query_log table life cycle

`bh_system.query_log` table has a default data life cycle of only 7 days. To retain data for a longer period, refer to the following commands to delete the TTL or modify the TTL as needed.

```SQL
# View the current retention period of the bh_system.query_log table
SHOW CREATE TABLE bh_system.query_log;

# Remove TTL
ALTER TABLE bh_system.query_log REMOVE TTL;

# Change the default TTL from 7 days to 180 days (you can replace 180 with the number of days you want to retain logs and this operation requires administrator privileges)
ALTER TABLE bh_system.query_log  MODIFY TTL event_time + INTERVAL 180 DAY;
```


<span id="c73fa3b3"></span>
## Query_log table information


|**Column name** |**Data type** |**Field description** |
|---|---|---|
|type |Enum8, enumerated values include:<br><br><br>* 'QueryStart' = 1<br><br>* 'QueryFinish' = 2<br><br>* 'ExceptionBeforeStart' = 3<br><br>* 'ExceptionWhileProcessing' = 4 |Query event type:<br><br><br>1. `QueryStart` (Query launch)<br><br>2. `QueryFinish` (Query ended successfully)<br><br>3. `ExceptionBeforeStart` (Exception before execution)<br><br>4. `ExceptionWhileProcessing` (Execution exception) |
|event_date |Date |Date of event |
|event_time |DateTime |Accurate timestamp of the event's occurrence |
|event_time_microseconds |DateTime64(6) |Event timestamp (microsecond precision) |
|query_start_time |DateTime |Query start time |
|query_start_time_microseconds |DateTime64(6) |Query start time (microsecond precision) |
|query_duration_ms |UInt64 |Query total elapsed time (ms) |
|read_rows |UInt64 |Total number of rows read by all tables and table functions of the query |
|read_bytes |UInt64 |Total number of bytes read by all tables and table functions of the query |
|written_rows |UInt64 |Number of rows written (for INSERT operations only) |
|written_bytes |UInt64 |Number of bytes written (for INSERT operations only) |
|result_rows |UInt64 |Number of rows in the returned result |
|result_bytes |UInt64 |Number of bytes of the returned result |
|memory_usage |UInt64 |Query the highest memory usage on each worker and each segment |
|current_database |String |Current database |
|query |String |Complete query statements |
|normalized_query_hash |UInt64 |Normalize query hash values |
|query_kind |String |Query type (such as `SELECT`, `INSERT`, and more) |
|databases |Array(String) |Databases involved in the query |
|tables |Array(String) |Tables involved in the query |
|columns |Array(String) |Fields of the tables involved in the query |
|partition_ids |Array(String) |Partition |
|projections |Array(String) |Projection names involved in the Query |
|materialized_views |Array(String) |List of names of materialized views involved in the query |
|exception_code |Int32 |Error code (only has a value when `type` is an exception event) |
|exception |String |Exception information (error message) |
|stack_trace |String |Exception stack trace information (requires configuration `log_query_threads=1`) |
|is_initial_query |UInt8 |Whether it is an initial query (0: subquery; 1: query initiated directly by users) |
|user |String |Username |
|query_id |String |Query ID |
|interface |UInt8 |Interface for initiating a query, possible values:<br><br><br>* 1 — TCP<br><br>* 2 — HTTP |
|os_user |String |Operating system user running TCP client |
|client_hostname |String |TCP client hostname |
|client_name |String |TCP client name |
|client_revision |UInt32 |TCP client version |
|client_version_major |UInt32 |Tcp client major version |
|client_version_minor |UInt32 |TCP client minor version number |
|client_version_patch |UInt32 |TCP client patch version |
|http_method |UInt8 |HTTP method for initiating a query, possible values:<br><br>0 — Query of the TCP interface.<br><br>1 — GET<br><br>2 — POST |
|http_user_agent |String |Client's User\-Agent information |
|http_referer |String |HTTP source information |
|forwarded_for |String |Client end IP of the HTTP proxy chain |
|quota_key |String |Quota key |
|revision |UInt32 |ByteHouse revised edition |
|ProfileEvents |Map(String, UInt64) |PrunedPartitions: The number of partitions actually read.<br><br>TotalPartitions: Total number of partitions.<br><br>TotalCPUTimeMs: The total CPU time (ms) summed for each worker and each segment.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The TotalCPUTimeMs column is only supported in ByteHouse CDW engine version v2.3.x and above. Please confirm the engine version before use. You can log in to the ByteHouse Console, click <strong>Tenant management</strong> at the top, and view your engine version on the <strong>Basic information</strong> page.</div><br> |
|Settings |Map(String, String) |Query effective configuration parameters (those that override the default value) |
|log_comment |String |Log comments |
|thread_ids |Array(UInt64) |LIST of thread IDs participating in the Query |
|used_aggregate_functions |Array(String) |Aggregate functions used |
|used_aggregate_function_combinators |Array(String) |Aggregate functions in use |
|used_database_engines |Array(String) |Table engines in use |
|used_data_type_families |Array(String) |Used data type |
|used_dictionaries |Array(String) |Used dictionary table |
|used_formats |Array(String) |Use a data format parameter (such as FORMAT CSV) |
|used_functions |Array(String) |Used functions |
|used_storages |Array(String) |Storage in use |
|used_table_functions |Array(String) |Table functions used |
|virtual_warehouse |String |Virtual warehouse used for queries |
|query_plan |String |Query execution plan |
