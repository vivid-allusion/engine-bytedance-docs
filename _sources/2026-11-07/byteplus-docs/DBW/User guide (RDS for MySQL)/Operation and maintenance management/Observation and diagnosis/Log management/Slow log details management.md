---
title: "Slow log details management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/slow-log-management-for-mysql"
---

This topic describes how to view the analysis results of slow logs and download target slow logs on the Database Workshop (DBW) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance and account for RDS for MySQL have been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1) and [Creating an account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_databases_and_accounts#.5Yib5bu66LSm5Y-3).

* If the target instance has security control enabled, you need to apply for operation and maintenance read\-only or read/write permissions for the current account. For more information, refer to [Enabling instance security control (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql), and [Applying for operation permissions (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/creating-an-operation-permission-ticket).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* When you access the Slow log analysis tab through Operation observability on the left navigation bar, slow log information about the first instance in the Instance list is viewed by default.

* Default displays slow log information from the past 10 minutes, such as the number of slow SQL, CPU usage, and Slow SQL list.

* You can view slow log data for up to the past 30 days, with a maximum query time span of 7 days.

* The database proxy is enabled by default for the RDS for MySQL instance. Therefore, the connection pool may be reused, that is, one connection is shared by multiple clients, which may cause the IP source to be inconsistent with the actual IP address and port.

* When filtering to view slow SQL queries within a certain period, the query end time must be later than the start time.

* When you filter by time to view the number of slow SQL queries and CPU usage of an instance or read\-only node within a specified time, the slow SQL list pane displays the database, execution user, IP source, average execution time(s), maximum lock wait time(s), average rows returned, and first wait time for each SQL template within the specified time.

* Index optimization suggestions:

   * The index optimization suggestion function needs to sample and analyze the content of the database and table. Therefore, when you view the index optimization suggestion of SQL for the first time, you need to authorize DBW to read the database and table.

   * It takes about 10 to 20 seconds to view SQL index optimization suggestions.

   * Index optimization suggestions are based on sampling analysis of partial data in the table. The generated optimization suggestions are for reference only and need to be further evaluated based on the actual situation.

* When downloading slow logs, note the following:

   * Up to 1 million slow log entries can be downloaded in a single request.

   * Slow log download tasks are retained for 1 day by default. Expired tasks will be automatically deleted.

   * When you select to download slow log details, you will get the slow SQL that can be executed directly.

   * You can view and export slow log download files in Export history.

   * Slow log files downloaded from the system are compressed in `.gz` (Gzip) format. For macOS users, please extract the downloaded file using the steps below:

      * Decompress using the built\-in gzip or gunzip command\-line tools:Open the Terminal and run the gzip or gunzip commands provided by the system to extract the files. The command format is `gzip -d your_filename.gz` or `gunzip your_filename.gz`.

      * To decompress the file using the tar tool: Download and install the tar tool to decompress the file. The command format is `tar -xz --force-local -f file_name.gz`.


<span id=".5p-l6K-i5oWi5pel5b-X"></span>
## Query a slow log


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

3. On the top menu bar, select the region.

4. On the **Observation and diagnosis** page, click **Log management**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also switch to the target instance by searching for the instance ID.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you access the slow log analysis through <strong>Observation and diagnosis</strong> on the left navigation bar, information about the first instance in the <strong>Instance list</strong> is displayed by default.   </div>
   

5. On the **Slow log** tab, filter by the desired time frame and select the target node (such as the primary or secondary node) from the Node ID dropdown to view its slow log trend, statistical summary, and details, as shown below.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If no Node ID is selected, the slow log information for all nodes is displayed by default.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the Node ID dropdown, each node shows the number of slow logs within the selected time frame:   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">0 article: Indicates no slow logs during this period, with normal system response, and performance bottlenecks can be ruled out.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Greater than 0 article: Indicates potential performance issues. It is recommended to further analyze the specific slow SQL.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When selecting a time range, the query end time must be later than the start time.   </div>
   

   * View slow log trends: In the left area of the **Slow log details** tab, you can view the slow log trends within a certain period. You can also click a specific time point to view the **Slow SQL number** and **CPU usage** at that moment.

   * View slow log statistics: On the right side of the **Slow log** tab, you can view the **Top 1\-day slow SQL locations** and **Top 7\-day slow SQL locations** for a certain period.

   * View slow log details: In the **Slow SQL List** section, filter slow SQL templates as needed and view detailed information of slow SQL within the templates. Specific parameters are shown in the table below.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Before viewing slow SQL details on the slow SQL list pane, you need to click the bar graph of a certain point in time in the slow log development trend graph.      </div>
      

      
      |**Target** |**Description** |
      |---|---|
      |Enable/Disable shard compatibility |* After enabling **Shard compatible**, in the sharding scenario, SQL templates with the same logical database and table names will be aggregated together, and the aggregated SQL template will be displayed.<br><br>* After disabling **Shard compatible**, all SQL templates are displayed in the sharding scenario.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">In general, the number of SQL templates after shard compatibility is enabled is less than the number of SQL templates after shard compatibility is disabled.</div><br> |
      |Filter slow SQL |Click **Advanced filtering**. In the expanded filter area, configure the following parameters as needed, and then click **Query**.<br><br><br>* **Aggregation method**: Select whether to check **Aggregation ignores execution User**, **Aggregate ignore IP source**, or **Aggregate ignore DB** as needed. You can select multiple options at the same time.<br><br><br>By default, execution User and IP source are ignored for aggregation. To view by User or IP dimension, deselect the corresponding aggregation method options here.<br><br><br>* **Database**: Select the target database from the drop\-down list. Multiple selections are supported.<br><br>* **User**: Select the target user from the drop\-down list. Multiple selections are supported.<br><br>* **IP**: Select the IP from the drop\-down list. Multiple selections are supported.<br><br>* **Keywords**: Enter the keywords to be queried in the input box, such as `select`, `from`, and `drop`.<br><br>* **Execution time range**: Set the execution time range in the input box. The minimum time range must be less than or equal to the maximum time range. |
      |View slow SQL list |On the **Slow SQL list** pane, you can perform the following operations:<br><br><br>* View the information of each SQL template, including the SQL template's **Database name**, **Execution user**, **IP source**, **Execution times**, **Total time consumption(s)** , **Maximum execution time(s)** , **Average execution time(s)** , **Maximum lock wait time(s)** , **Average lock wait time(s)** , **Maximum rows returned, Average rows returned, Maximum rows scaned, Average rows scanned, First appearance time, Last appearance time**, and **Table name**. You can also click **Advanced filtering** to view the SQL template that meets the target.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The SQL template column can display up to 3 lines of SQL text.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <strong>Slow SQL list</strong> area displays slow logs from the past 10 minutes by default.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Each SQL template aggregates all SQL commands that match the template.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The database proxy is enabled by default for the RDS for MySQL instance. Therefore, the connection pool may be reused, that is, one connection is shared by multiple clients, which may cause the IP source to be inconsistent with the actual IP address and port.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Total time consumption(s)</strong> refers to the total time consumption of all executions of SQL statements in the SQL template, in seconds.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Maximum execution time(s)</strong> and <strong>Average execution time(s)</strong> refer to the maximum and average execution time of a single SQL statement in the SQL template, in seconds.   </div><br>   <br><br>* View SQL index optimization suggestions:<br><br>   1. Click **SQL optimization** in the **Actions** column of the target SQL template. In the **Allow authorization** dialog box, click **Authorize**.<br><br>      * The SQL optimization suggestion function needs to sample and analyze the content of the database and table. Therefore, when you view the index optimization suggestion of SQL for the first time, you need to authorize DBW to read the database and table. If it is enabled, you do not need to perform this operation again.<br><br>      * It takes approximately 10 to 20 seconds to view SQL optimization suggestions.<br><br>   2. In the **SQL optimization suggestions** dialog box, view SQL optimization suggestions, including the executed SQL statement, **Execution plan**, and **Optimization suggestions**, including **Index optimization** and **SQL rewrite**.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the <strong>Automatic index creation</strong> function has been enabled in AutoOps, DBW automatically creates indexes for the current slow SQL based on the SQL optimization suggestions. For more information, refer to <a href="https://docs.byteplus.com/en/docs/DBW/Automatic_index_creation_management_MySQL">Automatic index creation management</a>.   </div><br>    |
      |View slow SQL details |Click the target **SQL template** under the SQL template column. In the **SQL details** panel, you can view relevant parameter information under different tabs:<br><br><br>* **Execution details**: On the **Execution details** tab, you can perform the following operations:<br><br>   * View the information of each SQL statement, including the SQL statement's **Start time**, **SQL text**, **Database**, **Execution user**, ** IP source**, **Execution time(s)** , **Lock wait time(s)** , **Rows scanned**, and **Rows returned**. At the same time, you can click the copy icon to copy the SQL text, and click the filter icon after **Execution user** or **IP source** to filter User or IP.<br><br>      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The database proxy is enabled by default for the RDS for MySQL instance. Therefore, the connection pool may be reused, that is, one connection is shared by multiple clients, which may cause the IP source to be inconsistent with the actual IP address and port.      </div><br>      <br><br>   * View SQL optimization suggestions:<br><br>      1. Click **SQL optimization** in the **Actions** column of the target SQL text. In the **Allow authorization** dialog box, click **Authorize**.<br><br>         * The index optimization suggestion function needs to sample and analyze the content of the database and table. Therefore, when you view the index optimization suggestion of SQL for the first time, you need to authorize DBW to read the database and table. If it is already enabled, you do not need to perform this operation again.<br><br>         * It takes about 10 to 20 seconds to view SQL index optimization suggestions.<br><br>      2. In the **SQL optimization suggestions** dialog box, view SQL optimization suggestions, including the executed SQL statement, **Execution plan**, and **Optimization suggestions**, including **Index optimization** and **SQL rewrite**.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If the <strong>Automatic index creation</strong> function has been enabled in AutoOps, DBW automatically creates indexes for the current slow SQL based on the SQL optimization suggestions. For more information, refer to <a href="https://docs.byteplus.com/en/docs/DBW/Automatic_index_creation_management_MySQL">Automatic index creation management</a>.   </div><br>   <br><br>* **Execution statistics**: On the **Execution statistics** tab, you can view all SQL text information that meets the filtering criteria in the SQL template.<br><br>   * **Total time consumption ratio**: The proportion of the total time consumption of the current SQL template to the total time consumption of all SQL lists within a certain period of time.<br><br>   * **Total lock wait time ratio**: The ratio of the total lock wait time of the current SQL template to the total lock wait time of all SQL lists within a certain period of time.<br><br>   * **Percentage of total rows scanned**: The ratio of the total number of scanned rows in the current SQL template to the total time consumption of all SQL lists within a certain period of time.<br><br>   * **Percentage of total rows returned**: The ratio of the total number of returned rows in the current SQL template to the total number of returned rows in all SQL lists.<br><br>   * **SQL execution times**: view the trend of slow SQL within the filtered time period.<br><br>   * **Execution profiling**: Displays the execution status of SQL statements in each stage to help you analyze and locate problems.<br><br>* **SQL analysis**: on the **SQL analysis** tab, you can view the following information.<br><br>   * **SQL text**: includes all SQL text information within the SQL template, click the copy icon to copy the SQL text.<br><br>   * **Execution plan**: Includes **select_type information interpretation**, **type information interpretation**, and **extra information interpretation**.<br><br>   * **Optimization suggestions**: Includes optimization suggestions for SQL statements. You can refer to these suggestions to optimize your SQL statements. |
      


<span id=".5LiL6L295oWi5pel5b-X"></span>
## Download a slow log

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Up to 1 million slow log entries can be downloaded in a single request.</div>


* <div data-tips="true" data-tips-type="tip">Slow log download tasks are retained for 1 day by default. Expired tasks will be automatically deleted.</div>


* <div data-tips="true" data-tips-type="tip">View and export the download file of slow log in the export history.</div>


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, switch the region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the upper\-left corner of the **Observation and diagnosis** page, click the icon to the right of the **Instance name**.<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span>icon, and select the target instance.

5. On the target instance page, click **Log management**.

6. On the **Slow log** details tab, select a node ID and a timeframe as needed.

7. In the **Slow SQL list** area, filter the target slow logs as needed, and then click the<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_79fd9094eb01b1e0f325f9af1f38225b.jpg) </span>icon.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_309fb1f5262fc00ca698f614ba7ca103.png) </span>

   Select the range of slow logs to download as needed. Currently, **Export slow log details** and **Export current page** are supported. The specific configurations are as follows:

   * Export slow log details

      The exported slow log details include slow SQL that can be executed directly.

      Click **Export slow log details**. In the **Export slow log details** dialog box, configure the following parameters.

      
      |**Parameter** |**Description** |
      |---|---|
      |**File format** |Currently, only the **CSV** slow log format for downloads is supported. No selection is required. |
      |**Export range** |Select the range of slow logs to download as needed. Currently, **Custom**, **Past 2 hours**, **Past 12 hours**, and **Past 24 hours** are supported. |
      |**Custom time period** |Select the time range for log export.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter can be set when <strong>Export range</strong> is set to <strong>Custom</strong>.</div><br> |
      

   * Export current page

      Click **Export current page**. In the **Export slow logs of the current page** dialog box, select the information included in the downloaded slow logs as needed.

      The current slow log download can include **SQL template**, **Database name**, **Executing user**, **IP source**, **Execution times**, **Total time (s)** , **Maximum execution time (s)** , **Average running time (s)** , **Maximum lock wait time (s)** , **Average lock wait time (s)** , **Maximum rows returned, Average rows returned, Maximum rows scaned, Average rows scanned, First appearance time, and Last appearance time**, and **Table name**.

7. Click **OK**.

8. On the **Slow log** tab, click<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_79fd9094eb01b1e0f325f9af1f38225b.jpg) </span>icon, and then click **Export history**.

9. In the **Export History** dialog box, select the target task whose **Status** is **Generated**, and click **Download file** in the **Actions** column.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[DescribeSlowLogs](https://docs.byteplus.com/en/docs/DBW/describeslowlogs) |Call the DescribeSlowLogs API to query slow log information. |
