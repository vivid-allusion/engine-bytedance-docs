---
title: "Slow log"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Slow_log_details"
---

This topic describes how to view the analysis results of slow logs and download target slow logs on the Database Workshop (DBW) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**


* A  NDB for MySQL instance and account have been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance) and [Creating an account](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_and_deleting_accounts).

* If the target instance has security control enabled, you need to apply for operation and maintenance read\-only or read/write permissions for the current account. For more information, see [ for MySQL instance security control](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control)[ for MySQL instance security control](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control)[ for MySQL instance security control](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control) and [ for MySQL instance related operation permissions](https://docs.byteplus.com/en/docs/DBW/Creating_an_operation_permission_ticket) [ for MySQL instance related operation permissions](https://docs.byteplus.com/en/docs/DBW/Creating_an_operation_permission_ticket)[ for MySQL instance related operation permissions](https://docs.byteplus.com/en/docs/DBW/Creating_an_operation_permission_ticket).


<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* When you access the Slow log analysis tab through Operation observability on the left navigation bar, slow log information about the first instance in the Instance list is viewed by default.

* Default displays slow log information from the past 10 minutes, such as the number of slow SQL, CPU usage, and Slow SQL list.

* You can view slow log data for up to the past 30 days, with a maximum query time span of 7 days.

* When filtering to view slow SQL queries within a certain period, the query end time must be later than the start time.

* When you filter by time to view the number of slow SQL queries and CPU usage of primary node or read\-only node within a specified time, the slow SQL list pane displays the database, executing user, IP source, average execution time (s), maximum lock wait time (s), average rows returned, and first wait time for eachSQL template within the specified time.

* Slow log files downloaded from the system are compressed in `.gz` (Gzip) format. For macOS users, please extract the downloaded file using the steps below:

   * Decompress using the built\-in gzip or gunzip command\-line tools:Open the Terminal and run the gzip or gunzip commands provided by the system to extract the files. The command format is `gzip -d your_filename.gz` or `gunzip your_filename.gz`.

   * To decompress the file using the tar tool: Download and install the tar tool to decompress the file. The command format is `tar -xz --force-local -f file_name.gz`.

* When downloading slow logs, note the following:

   * Up to 1 million slow log entries can be downloaded in a single request.

   * Slow log download tasks are retained for 1 day by default. Expired tasks will be automatically deleted.

   * When you select to download slow log details, you will get the slow SQL that can be executed directly.

   * You can view and export slow log download files in Export history.


<span id=".5p-l6K-i5oWi5pel5b-X"></span>
## Query a slow log


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. In the upper\-right corner of the **Observation and diagnosis** page, switch the database **Database ** **NDBfor MySQL **  instance type.

   By default, the information about the first instance in the **Instance list** page is displayed. Click the drop\-down icon in the upper\-left corner of the page to select the target instance.

5. On the **Observation and diagnosis** page, click **Log management**.

6. On the **Slow log** tab, filter the time frame as needed. Select the target node (such as the primary node or a read\-only node) from the Node ID drop\-down list to view the slow log trends, statistics summary, and details of that node, as shown below.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you do not select a node ID, the slow log information of all nodes is displayed by default.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the Node ID dropdown, each node shows the number of slow logs within the selected time frame:   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">0 article: Indicates no slow logs during this period, with normal system response, and performance bottlenecks can be ruled out.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Greater than 0 article: Indicates potential performance issues. It is recommended to further analyze the specific slow SQL.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When selecting a time range, the query end time must be later than the start time.   </div>
   

   * View slow log trends: In the left area of the **Slow log details** tab, you can view the slow log trends within a certain period. You can also click a specific time point to view the **Slow SQL number** and **CPU usage** at that moment.

   * View slow log statistics: On the right side of the **Slow log** tab, you can view the **Top 1\-day slow SQL locations** and **Top 7\-day slow SQL locations** for a certain period.

   * View slow log details: In the **Slow SQL List** section, filter slow SQL templates as needed and view detailed information of slow SQL within the templates. Specific parameters are shown in the table below.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Before viewing slow SQL details on the slow SQL list pane, you need to click the bar graph of a certain point in time in the slow log development trend graph.      </div>
      

      
      <Tabs>
      <Tab zoneid="QljKbzoVdK" title="Enable/Disable shard compatibility">
      <TabTitle>Enable/Disable shard compatibility</TabTitle>
      
      * After enabling **Shard compatible**, in the sharding scenario, SQL templates with the same logical database and table names will be aggregated together, and the aggregated SQL template will be displayed.
      
      * After disabling **Shard compatible**, all SQL templates are displayed in the sharding scenario.
      
      
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
      
      
      <div data-tips="true" data-tips-type="default">In general, the number of SQL templates after shard compatibility is enabled is less than the number of SQL templates after shard compatibility is disabled.</div>
      
      
      
      </Tab>
      <Tab zoneid="VOvrdvJZkB" title="Filter slow SQL">
      <TabTitle>Filter slow SQL</TabTitle>
      
      Click **Advanced filtering**. In the expanded filter area, configure the following parameters as needed, and then click **Query**.
      
      
      * **Aggregation method**: Select whether to **Aggregate ignore execution User**, **Aggregate ignore IP source**, or **Aggregate ignore DB** as needed. Multiple options can be selected simultaneously.
      
      
      By default, aggregation ignores the execution User and IP source. To view by User and IP dimensions, deselect the corresponding aggregation method options here.
      
      
      * **Database**: Select the target database from the drop\-down list. Multiple selections are supported.
      
      * **User**: Select the target user from the drop\-down list. Multiple selections are supported.
      
      * **IP**: Check the target IPs in the drop\-down list. Multiple selections are supported.
      
      * **Keywords**: Enter the keywords to be queried in the input box, such as `select`, `from`, and `drop`.
      
      * **Execution time range**: Set the execution time range in the input box. The minimum time range must be less than or equal to the maximum time range.
      
      
      </Tab>
      <Tab zoneid="AqjmguT6d0" title="View slow SQL list">
      <TabTitle>View slow SQL list</TabTitle>
      
      On the **Slow SQL list** pane, you can perform the following operations:
      
      
      * View information for each SQL template, including the **database name**, **executing user**, **IP source**, **execution times**, **total time (s)** , **maximum execution time (s)** , **average execution time (s)** , **maximum lock wait time (s)** , **average lock wait time (s)** , **maximum rows returned, average rows returned, maximum rows scaned, average rows scanned, maximum number of affected rows, average rows affected, first appearance time, last appearance time**, and **table name** of each **SQL template**. You can also click **Advanced filtering** to view the SQL template that meets the target.
      
         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
         
      
         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The SQL template column can display up to 3 lines of SQL text.   </div>
         
      
         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The <strong>Slow SQL list</strong> area displays slow logs from the past 10 minutes by default.   </div>
         
      
         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">All SQL commands that meet the template are aggregated within each SQL template.   </div>
         
      
         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Total time (s)</strong> refers to the total time of all execution times of the SQL statement in the SQL template, in seconds.   </div>
         
      
         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Maximum execution time (s)</strong> and <strong>average execution time (s)</strong> refer to the maximum execution time and average execution time of a single execution of the SQL statement in the SQL template, in seconds.   </div>
         
      
      * View SQL index optimization suggestions:
      
         1. Click **SQL optimization** in the **Actions** column of the target SQL template. In the **Allow authorization** dialog box, click **Authorize**.
      
            * The SQL optimization suggestion function needs to sample and analyze the content of the database and table. Therefore, when you view the index optimization suggestion of SQL for the first time, you need to authorize DBW to read the database and table. If it is enabled, you do not need to perform this operation again.
      
            * It takes approximately 10 to 20 seconds to view SQL optimization suggestions.
      
         2. In the **SQL optimization suggestions** dialog box, view SQL optimization suggestions, including the executed SQL statement, **Execution plan**, and **Optimization suggestions**, including **Index optimization** and **SQL rewrite**.
      
         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
         
      
         <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the <strong>Automatic index creation</strong> function has been enabled in AutoOps, DBW automatically creates indexes for the current slow SQL based on the SQL optimization suggestions. For more information, refer to <a href="https://docs.byteplus.com/en/docs/DBW/Automatic_index_creation_management">Automatic index creation management</a>.   </div>
         
      
      
      </Tab>
      <Tab zoneid="Rne47R0wDr" title="View slow SQL details">
      <TabTitle>View slow SQL details</TabTitle>
      
      Click the target **SQL template** under the SQL template column. In the **SQL details** panel, you can view relevant parameter information under different tabs:
      
      
      * **Execution details**: On the **Execution details** tab, you can view the **Start Time**, **SQL text**, **Database**, **Executing user**, **IP source**, **Execution time (s)** , **Lock wait time (s)** , **Rows scanned**, and **Rows returned** of each SQL statement. At the same time, you can click the copy icon to copy the SQL text, and click the filter icon after **Execution user** or **IP source** to filter User or IP.
      
      * View SQL optimization suggestions:
      
         1. Click **SQL optimization** in the **Actions** column of the target SQL text. In the **Allow authorization** dialog box, click **Authorize**.
      
            * The index optimization suggestion function needs to sample and analyze the content of the database and table. Therefore, when you view the index optimization suggestion of SQL for the first time, you need to authorize DBW to read the database and table. If it is already enabled, you do not need to perform this operation again.
      
            * It takes about 10 to 20 seconds to view SQL index optimization suggestions.
      
         2. In the **SQL optimization suggestions** dialog box, view SQL optimization suggestions, including the executed SQL statement, **Execution plan**, and **Optimization suggestions**, including **Index optimization** and **SQL rewrite**.
      
         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
         
      
         <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the <strong>Automatic index creation</strong> function has been enabled in AutoOps, DBW automatically creates indexes for the current slow SQL based on the SQL optimization suggestions. For more information, refer to <a href="https://docs.byteplus.com/en/docs/DBW/Automatic_index_creation_management">Automatic index creation management</a>.   </div>
         
      
      * **Execution statistics**: On the **Execution statistics** tab, you can view all SQL text information that meets the filtering criteria in the SQL template.
      
         * **Total time consumption ratio**: The proportion of the total time consumption of the current SQL template to the total time consumption of all SQL lists within a certain period of time.
      
         * **Total lock wait time ratio**: The ratio of the total lock wait time of the current SQL template to the total lock wait time of all SQL lists within a certain period of time.
      
         * **Percentage of total rows scanned**: The ratio of the total number of scanned rows in the current SQL template to the total time consumption of all SQL lists within a certain period of time.
      
         * **Percentage of total rows returned**: The ratio of the total number of returned rows in the current SQL template to the total number of returned rows in all SQL lists.
      
         * **SQL execution times**: view the trend of slow SQL within the filtered time period.
      
         * **Execution profiling**: Displays the execution status of SQL statements in each stage to help you analyze and locate problems.
      
      * **SQL analysis**: on the **SQL analysis** tab, you can view the following information.
      
         * **SQL text**: includes all SQL text information within the SQL template, click the copy icon to copy the SQL text.
      
         * **Execution plan**: Includes **select_type information interpretation**, **type information interpretation**, and **extra information interpretation**.
      
         * **Optimization suggestions**: Includes optimization suggestions for SQL statements. You can refer to these suggestions to optimize your SQL statements.
      
      
      </Tab>
      </Tabs>
      


<span id=".5LiL6L295oWi5pel5b-X"></span>
## Download a slow log

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Up to 1 million slow log entries can be downloaded in a single request.</div>


* <div data-tips="true" data-tips-type="tip">Slow log download tasks are retained for 1 day by default. Expired tasks will be automatically deleted.</div>


* <div data-tips="true" data-tips-type="tip">View and export the download file of slow log in the export history.</div>


* <div data-tips="true" data-tips-type="tip">Slow log files downloaded from the system are compressed in <code>.gz</code> (Gzip) format. For macOS users, please extract the downloaded file using the steps below:</div>


   * <div data-tips="true" data-tips-type="tip">Decompress using the built\-in gzip or gunzip command\-line tools:Open the Terminal and run the gzip or gunzip commands provided by the system to extract the files. The command format is <code>gzip -d your_filename.gz</code> or <code>gunzip your_filename.gz</code>.</div>


   * <div data-tips="true" data-tips-type="tip">To decompress the file using the tar tool: Download and install the tar tool to decompress the file. The command format is <code>tar -xz --force-local -f file_name.gz</code>.</div>


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. In the upper\-right corner of the **Observation and diagnosis** page, switch the database **Database ** **NDBfor MySQL **  instance type.

   By default, the information about the first instance in the **Instance list** page is displayed. Click the drop\-down icon in the upper\-left corner of the page to select the target instance.

5. On the **Observation and diagnosis** page, click **Log management**.

   In the slow SQL statistics area, select the time period you want to view.

6. In the **Slow log** tab, in the **Slow SQL list** area, click **Advanced filtering** to filter the SQL list as needed, and then click the download icon.

   Select the range of slow logs to download as needed. Currently, **Export slow log details** and **Export current page** are supported. The specific configurations are as follows:

      
      <Tabs>
      <Tab zoneid="lsnjucE94H" title="Export slow log details">
      <TabTitle>Export slow log details</TabTitle>
      
      1. The exported slow log details include slow SQL that can be executed directly.
      
      2. Click **Export slow log details**. In the **Export slow log details** dialog box, configure the following parameters.
      
         
         |**Parameter** |**Description** |
         |---|---|
         |**File format** |Currently, only the **CSV** slow log format for downloads is supported. No selection is required. |
         |**Export range** |Select the range of slow logs to download as needed. Currently, **Custom**, **Past 2 hours**, **Past 12 hours**, and **Past 24 hours** are supported. |
         |**Custom time period** |Select the time range for log export.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter can be set when <strong>Export range</strong> is set to <strong>Custom</strong>.</div><br> |
         
      
      3. Click **OK**.
      
      4. On the **Slow log details** tab, click the download icon, and then click **Export history**.
      
      5. In the **Export history** dialog box, select the target task whose **Status** is **Generated**, and click **Download file** in the **Actions** column.
      
      
      </Tab>
      <Tab zoneid="EiMxxlzUfh" title="Export current page">
      <TabTitle>Export current page</TabTitle>
      
      1. Click **Export current page**. In the **Export slow logs of the current page** dialog box, select the information included in the downloaded slow logs as needed.
      
         The current download can include **SQL template**, **Database name**, **Executing user**, **IP source**, **Execution times**, **Total time (s)** , **Maximum execution time (s)** , **Average execution time (s)** , **Maximum lock wait time (s)** , **Average lock wait time (s)** , **Maximum rows returned, average rows returned, maximum rows scaned, average rows scanned, maximum number of affected rows, average rows affected, first appearance time, last appearance time**, and **Table name**.
      
      2. Click **OK**.
      
      
      </Tab>
      </Tabs>
