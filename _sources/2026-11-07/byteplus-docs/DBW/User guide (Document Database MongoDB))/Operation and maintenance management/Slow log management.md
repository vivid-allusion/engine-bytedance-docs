---
title: "Slow log management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/slow-query-log-management"
---

This topic describes how to view the analysis results of slow logs and download target slow logs on the Database Workshop (DBW) console.

<span id="uB0ZI2x0"></span>
## Prerequisites


* An instance and account for Document Database for MongoDB have been created, and the instance status is running. For detailed steps, refer to Creating an instance and Creating an account.

* If the target instance has security control enabled, you need to apply for operation and maintenance read\-only or read/write permissions for the current account. For details, see [Enable security control for Document Database for MongoDB instances](https://docs.byteplus.com/en/docs/DBW/MongoDB_Enabling_security_control) and [Apply for Operation and maintenance permissions for Document Database for MongoDB](https://docs.byteplus.com/en/docs/DBW/creating-an-operation-permission-ticket__).


<span id="KBVsGLLD"></span>
## Precautions


* Default displays slow log information from the past 10 minutes, such as the number of slow SQL, CPU usage, and Slow SQL list.

* You can view slow log data within the last 30 days, with a maximum query time span of 7 days.

* When filtering to view slow SQL queries within a certain period, the query end time must be later than the start time.

* The slow query log management system retains up to 10 KB of slow log data per entry. Any content exceeding this limit will be truncated and not recorded.

* When you filter by time to view the number of slow SQL statements and CPU utilization for an instance or read\-only node within a specified period, the Slow SQL List section will display, for each SQL template during that period, the following details: Database, Executing UserSource IP, Average Execution Time (s), Maximum Lock Wait Time (s), Average Number of Rows Returned and First Occurrence Time

* When downloading slow logs, note the following:

   * Up to 1 million slow log entries can be downloaded in a single request.

   * Download tasks for slow log details are retained for 1 day by default and will be automatically deleted upon expiration.

   * When you select to download slow log details, you will get the slow SQL that can be executed directly.

   * You can view and export slow log download files in Export history.

   * Slow log files downloaded from the system are compressed in `.gz` (Gzip) format. For macOS users, please extract the downloaded file using the steps below:

      * Decompress using the built\-in gzip or gunzip command\-line tools:Open the Terminal and run the gzip or gunzip commands provided by the system to extract the files. The command format is `gzip -d your_filename.gz` or `gunzip your_filename.gz`.

      * To decompress the file using the tar tool: Download and install the tar tool to decompress the file. The command format is `tar -xz --force-local -f file_name.gz`.


<span id="ZcSNG6Jj"></span>
## Query a slow log


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. Select one of the following options to navigate to the slow log analysis for your target instance:

   
   <Tabs>
   <Tab zoneid="PIZxsr0Qtd" title="Path 1: Access slow log analysis via observation and diagnosis">
   <TabTitle>Path 1: Access slow log analysis via observation and diagnosis</TabTitle>
   
   1. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.
   
   2. On the **Observation and diagnosis** page, click **Log management**.
   
      1. From the dropdown in the upper\-right corner, select **Document Database for MongoDB** as the target database type.
   
      2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.
   
   
   </Tab>
   <Tab zoneid="UWavGTE4Ln" title="Path 2: Access slow log analysis via instance list">
   <TabTitle>Path 2: Access slow log analysis via instance list</TabTitle>
   
   1. On the left navigation bar, click **Instance list**.
   
   2. On the **Instance list** page, click **Observability and diagnostics** in the **Actions** column for your target instance.
   
   3. On the target instance's **Session management** page, click **Log management**.
   
   
   </Tab>
   </Tabs>
   

4. On the **Log management** tab, select the component, node ID, and time range as needed to view slow log information for all nodes or a specific node within the instance, such as slow log trends, statistics, and details. Details are as follows:

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When the instance type of the Document Database for MongoDB is a sharded collection, you need to select the component and node. If the instance type is a replica set, you only need to select the node without choosing a component.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can also filter slow logs within a specified time period as needed.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can view slow log data within the last 30 days, with a maximum query time span of 7 days.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When selecting a time range, the query end time must be later than the start time.   </div>
   

   * View slow log trends: In the **Slow SQL number** section of the **Slow SQL management** tab, you can view the slow log trends for a specific time period. You can also click on a specific time point to view the **Slow SQL number** for that time.

   * View slow log statistics: On the right side of the **Log Management** tab, you can view the **Daily Top Slow SQL** and **7\-Day Top Slow SQL** for a specified period.

   * View slow log details: In the **Slow SQL List** section, filter slow SQL templates as needed and view detailed information of slow SQL within the templates. Specific parameters are shown in the table below.

   Before viewing slow SQL details on the slow SQL list pane, you need to click the bar graph of a certain point in time in the slow log development trend graph.

   
   <Tabs>
   <Tab zoneid="qmuUAD4fFH" title="Filter slow SQL">
   <TabTitle>Filter slow SQL</TabTitle>
   
   Click **Advanced filtering**. In the expanded filter area, configure the following parameters as needed, and then click **Query**.
   
   
   * **Aggregation method**: Select whether to **Aggregate ignore execution User**, **Aggregate ignore IP source**, or **Aggregate ignore DB** as needed. Multiple selections are supported.
   
   
   By default, the execution User and IP source are ignored for aggregation. To view by User or IP dimension, deselect the corresponding aggregation method options here.
   
   
   * **Database name**: Select the target database from the dropdown list. Multiple selections are supported.
   
   * **Collection name**: Enter the name of the collection to query in the input box.
   
   * **User**: Select the target user from the drop\-down list. Multiple selections are supported.
   
   * **IP**: Select the IP from the drop\-down list. Multiple selections are supported.
   
   * **Keyword**: Enter the keywords to query in the input box, such as select, from, or drop.
   
   * **Execution time range**: Set the execution time range in the input box. The minimum time range must be less than or equal to the maximum time range.
   
   * **Command type**: Enter the command type to query in the input box, then press Enter.
   
   
   </Tab>
   <Tab zoneid="EgW5RuAlWD" title="View slow SQL list">
   <TabTitle>View slow SQL list</TabTitle>
   
   In the **Slow SQL list** area, you can view information for each SQL template, including: **Database name**, **Command type**, **Executing user**, **IP source**, **Execution times**, **Total time (ms)** , **Maximum execution time (ms)** , **Average execution time (ms)** , **Maximum rows returned**, **Average rows returned**, **Maximum number of scanned documents**, **Average number of scanned documents**, **Maximum number of index entries scanned**, **Average number of index entries scanned**, **Collection**, **Is it truncated?** , **First appearance time**, and **Last appearance time**. You can also click **Advanced filtering** to view the SQL template that meets the target.
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   
   * <div data-tips="true" data-tips-type="default">The SQL template column can display up to 3 lines of SQL text.</div>
   
   
   * <div data-tips="true" data-tips-type="default">The <strong>Slow SQL list</strong> area displays slow logs from the past 10 minutes by default.</div>
   
   
   * <div data-tips="true" data-tips-type="default">All SQL commands that meet the template are aggregated within each SQL template.</div>
   
   
   * <div data-tips="true" data-tips-type="default"><strong>Total time (ms)</strong> refers to the cumulative execution time of all invocations of SQL statements under this SQL template, measured in milliseconds.</div>
   
   
   * <div data-tips="true" data-tips-type="default"><strong>Maximum execution time (ms)</strong> and <strong>Average execution time (ms)</strong> refer to the maximum and average execution times for a single execution of SQL statements under this SQL template, measured in milliseconds.</div>
   
   
   
   </Tab>
   <Tab zoneid="X3OqpwCwU5" title="View slow SQL details">
   <TabTitle>View slow SQL details</TabTitle>
   
   Click the target **SQL template** under the SQL template column. In the **SQL details** panel, you can view relevant parameter information under different tabs:
   
   
   * **Execution details**: Under the **Execution details** tab, you can view up to 5,000 execution records. Additionally, you can view information for each SQL statement, including **Start Time**, **execution text**, **Database name**, **Executing user**, **IP source**, **Execution time (ms)** , **number of scanned documents**, **number of index entries scanned**, **Collection**, **Use index**, **Is it truncated?** , **Reading time (ms)** , and **Rows returned**. You can also click the copy icon to copy the SQL text.
   
   * **Execution statistics**: On the **Execution statistics** tab, you can view all SQL statements matching your filter criteria within a given SQL template, including: **of total time spent** (the proportion of the total time consumed by the current SQL template to the total time of all SQL lists during a certain period), **Percentage of total rows returned** (the proportion of the total rows returned by the current SQL template to the total rows returned by all SQL lists during a certain period), Number of SQL executions, and Execution profiling.
   
   
   </Tab>
   </Tabs>
   


<span id="rlSeuYDO"></span>
## Download a slow log

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Up to 1 million slow log entries can be downloaded in a single request.</div>


* <div data-tips="true" data-tips-type="default">Tasks for exporting slow log details are retained for 1 day by default and will be automatically deleted upon expiration.</div>


* <div data-tips="true" data-tips-type="default">View and export the download file of slow log in the export history.</div>


* <div data-tips="true" data-tips-type="default">Slow log files downloaded from the system are compressed in <code>.gz</code> (Gzip) format. For macOS users, please extract the downloaded file using the steps below:</div>


   * <div data-tips="true" data-tips-type="default">Decompress using the built\-in gzip or gunzip command\-line tools:Open the Terminal and run the gzip or gunzip commands provided by the system to extract the files. The command format is <code>gzip -d your_filename.gz</code> or <code>gunzip your_filename.gz</code>.</div>


   * <div data-tips="true" data-tips-type="default">To decompress the file using the tar tool: Download and install the tar tool to decompress the file. The command format is <code>tar -xz --force-local -f file_name.gz</code>.</div>


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. Select one of the following options to access the slow log analysis for your target instance:

   
   <Tabs>
   <Tab zoneid="shf0tJtH" title="Path 1: Access slow log analysis via observation and diagnosis">
   <TabTitle>Path 1: Access slow log analysis via observation and diagnosis</TabTitle>
   
   1. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.
   
   2. On the **Observation and diagnosis** page, click **Log management**.
   
      1. From the dropdown in the upper\-right corner, select **Document Database for MongoDB** as the target database type.
   
      2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.
   
   
   </Tab>
   <Tab zoneid="NiYMZhXI" title="Path 2: Access slow log analysis via instance list">
   <TabTitle>Path 2: Access slow log analysis via instance list</TabTitle>
   
   1. On the left navigation bar, click **Instance list**.
   
   2. On the **Instance list** page, click **Observability and diagnostics** in the **Actions** column for your target instance.
   
   3. On the target instance's **Session management** page, click **Log management**.
   
   
   </Tab>
   </Tabs>
   

4. On the **Log management** tab, select the component, node, and time range as needed.

5. In the **Slow SQL list** area, filter target slow logs based on requirements, then click the download icon and select the export range (supports exporting slow log details or current page). The specific configurations are shown follows:

   
   <Tabs>
   <Tab zoneid="Q5ZzQNpSK1" title="Export slow log details">
   <TabTitle>Export slow log details</TabTitle>
   
   The exported slow log details include slow SQL that can be executed directly.
   
   
   1. Click **Export slow logs**, then configure the parameters in the **Export slow logs** dialog.
   
      
      |**Parameter** |**Description** |
      |---|---|
      |**File format** |Select the file format for downloading slow logs as needed, supporting **CSV** and **JSON**. |
      |**Export range** |Select the range of slow logs to download as needed. Currently, **Custom**, **Past 2 hours**, **Past 12 hours**, and **Past 24 hours** are supported. |
      |**Custom time period** |Select the time range for log export.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter can be set when <strong>Export range</strong> is set to <strong>Custom</strong>.</div><br> |
      
   
   2. Click **OK**.
   
   
   In the **Export history** dialog box, when the task status changes to **Completed**, click **Download file** in the **Actions** column of the target task to obtain the slow log details.
   
   
   3. In the **Slow SQL list** section, click the download icon and select **Export history**.
   
   4. In the **Export history** dialog box, click **Download file** in the **Actions** column of the target export task name.
   
   
   </Tab>
   <Tab zoneid="KHbZ3ux5bN" title="Export current page">
   <TabTitle>Export current page</TabTitle>
   
   1. Click **Export current page**. In the **Export slow logs of the current page** dialog box, select the information included in the downloaded slow logs as needed.
   
      Select the slow log information to download as needed, including **SQL template**, **Database name**, **Command type**, **Execution User**, **IP source**, **Execution times**, **Total time (ms)** , **Maximum execution time (ms)** , **Average execution time (ms)** , **Maximum lock waiting time (s)** , **Average lock waiting time (s)** , **Average physical SQL execution time (ms)** , **Maximum physical SQL execution time (ms)** , **Maximum rows returned**, **Average rows returned**, **Maximum number of scanned documents**, **Average number of scanned documents**, **Maximum number of index entries scanned**, **Average number of index entries scanned**, **Collection**, **Is it truncated?** , **Maximum rows scaned**, **Average rows scanned**, **Maximum number of affected rows**, **Average rows affected**, **First appearance time**, **Last appearance time**, **Table name**, **PSM**, and **Actions**.
   
   2. Click **OK**.
   
   
   </Tab>
   </Tabs>
