---
title: "Log management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/slow-log-analysis-management-for-PG"
---

This topic describes how to view the slow log analysis results and export slow logs of an RDS for PostgreSQL instance on the DBW console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance for RDS for PostgreSQL has been created, and the instance status is running. For detailed steps, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/create_instance).

* If the target instance has security control enabled, you need to apply for operation and maintenance read\-only or read/write permissions for the current account. For more information, refer to [Enabling instance security control (RDS for PostgreSQL)](https://docs.byteplus.com/en/docs/DBW/enabling-security-control), and [Applying for operation permissions (RDS for PostgreSQL)](https://docs.byteplus.com/en/docs/DBW/Create_operation_permission_ticket).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* When you access the Slow log analysis tab through Operation observability on the left navigation bar, slow log information about the first instance in the Instance list is viewed by default.

* Default displays slow log information from the past 10 minutes, such as the number of slow SQL, CPU usage, and Slow SQL list.

* You can view slow log data for up to the past 30 days, with a maximum query time span of 7 days.

* When filtering to view slow SQL queries within a certain period, the query end time must be later than the start time.

* When you filter by time to view the number of slow SQL queries and CPU usage of an instance or read\-only node within a specified time, the slow SQL list pane displays the database, execution user, IP source, average execution time(s), average rows returned, and first wait time for each SQL template within the specified time.

* When exporting slow logs, note the following:

   * You can export up to 1,000,000 slow log execution details at a time.

   * Slow log export tasks are retained for 1 day by default. Expired tasks will be automatically deleted.

   * When you select to download slow log details, you will get the slow SQL that can be executed directly.

   * You can view and export slow log download files in Export history.


<span id=".5p-l55yL5oWi5pel5b-X"></span>
## View slow logs


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. In the upper right corner of the **Observation and diagnosis** page, switch the instance type to **RDS for PostgreSQL**.

5. On the **Log management** tab, switch the target instance in the upper left corner.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you access log management through <strong>Observation and diagnosis</strong> in the left navigation bar, the information related to the first instance in the <strong>Instance list</strong> is displayed by default.   </div>
   

6. On the **Log management** tab, select the node ID and time range as needed to view the slow log information of all nodes or a certain node in the instance, such as slow log trends, statistics, and details. Details are as follows:

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If no node ID is selected, it means viewing slow log information of all nodes.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also filter slow logs within a specified time period as needed.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can view slow log data for up to the past 30 days, with a maximum query time span of 7 days.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When selecting a time range, the query end time must be later than the start time.   </div>
   

   * View slow log trends: In the left area of the log management tab, you can view the slow log trends within a certain period. You can also click a specific time point to view the **Slow SQL number** and **CPU usage** at that moment.

   * View slow log statistics: On the right side of the Log Management tab, you can view the **Daily Top Slow SQL** and **7\-Day Top Slow SQL** for a specified period.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2"><strong>SlowSQLdaily TOP</strong> and <strong>Top 7\-day slow SQL indicate</strong> the slow SQL that is executed most in one day and the slow SQL that is executed most in seven days, respectively. By default, the top 10 slow SQL that are executed are returned.      </div>
      

   * View slow log details: In the **Slow SQL List** section, filter slow SQL templates as needed and view detailed information of slow SQL within the templates. Specific parameters are shown in the table below.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Before viewing slow SQL details on the slow SQL list pane, you need to click the bar graph of a certain point in time in the slow log development trend graph.      </div>
      

   
   |**Target** |**Description** |
   |---|---|
   |Filter slow SQL |Click **Advanced filtering**. In the expanded filter area, configure the following parameters as needed, and then click **Query**.<br><br><br>* **Aggregation method**: Select whether to check **Aggregation ignores execution User**, **Aggregate ignore IP source**, or **Aggregate ignore DB** as needed. You can select multiple options at the same time.<br><br><br>By default, execution User and IP source are ignored for aggregation. To view details by User or IP dimension, clear the corresponding aggregation method options here.<br><br><br>* **Database**: Select the target database from the drop\-down list. Multiple selections are supported.<br><br>* **User**: Select the target user from the drop\-down list. Multiple selections are supported.<br><br>* **IP**: Select the IP from the drop\-down list. Multiple selections are supported.<br><br>* **Keywords**: Enter the keywords to be queried in the input box, such as `select`, `from`, and `drop`.<br><br>* **Execution time range**: Set the execution time range in the input box. The minimum time range must be less than or equal to the maximum time range.<br><br>* **SQL type**: Select the SQL types you want to filter as needed. |
   |View slow SQL list |In the **Slow SQL list** area, you can view the **Database**, **SQL type**, **Execution User**, **IP source**, **Execution times**, **Total time**, **Maximum execution time (s)** , **Average execution time (s)** , **Maximum lock waiting time (s)** , **Average lock waiting time (s)** , **Maximum rows returned**, **Average rows returned**, **Maximum rows scanned**, **Average rows scanned**, **First appearance time**, and **Last appearance time** for each **SQL template**. You can also click **Advanced filtering** to view the SQL template that meets the target.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The <strong>Slow SQL list</strong> area displays slow logs from the past 10 minutes by default.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The SQL template column can display up to 3 lines of SQL text.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">All SQL commands that meet the template are aggregated within each SQL template.</div><br> |
   |View slow SQL details |Click the target **SQL template** under the SQL template column. In the **SQL details** panel, you can view relevant parameter information under different tabs:<br><br><br>* **Execution details**: On the **Execution details** tab, you can view information such as the **Start time**, **SQL text**, **Database**, **Execution user**, **IP source**, **Execution time(s)** , and **Rows returned** of each SQL statement. At the same time, you can click the copy icon to copy the SQL text, and click the filter icon after **Execution user** or **IP source** to filter User or IP.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Each SQL template supports displaying up to 5,000 execution details.   </div><br>   <br><br>* **Execution statistics**: On the **Execution statistics** tab, you can view all SQL text information that meets the filtering criteria in the SQL template.<br><br>   * **Total time consumption ratio**: The proportion of the total time consumption of the current SQL template to the total time consumption of all SQL lists within a certain period of time.<br><br>   * **Percentage of total rows returned**: The ratio of the total number of returned rows in the current SQL template to the total number of returned rows in all SQL lists.<br><br>   * **SQL execution times**: view the trend of slow SQL within the filtered time period. |
   


<span id=".5a-85Ye65oWi5pel5b-X"></span>
## Download a slow log

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can export up to 1,000,000 slow log execution details at a time.</div>


* <div data-tips="true" data-tips-type="tip">Slow log export tasks are retained for 1 day by default. Expired tasks will be automatically deleted.</div>


* <div data-tips="true" data-tips-type="tip">View and export the download file of slow log in the export history.</div>


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. In the upper right corner of the **Observation and diagnosis** page, switch the instance type to **RDS for PostgreSQL**.

5. On the **Log management** tab, switch the target instance in the upper left corner.

6. On the **Log management** tab, select the node ID and timeframe as needed.

7. In the **Slow SQL list** section, filter for the target slow logs as needed, then click the download icon. Select the range of slow logs to export as needed. Currently, **Export slow log details** and **Export current page** are supported. The specific configurations are as follows:

   * Export slow log details

      * Click **Export slow log details**. In the **Export slow log details** dialog box, configure the following parameters.

      * The exported slow log details include slow SQL that can be executed directly.

      
      |**Parameter** |**Description** |
      |---|---|
      |**File format** |The default format for exported files is **CSV**, and it cannot be modified. |
      |**Export range** |Select a slow log range to export as needed. The system supports **Custom**, **Past 2 hours**, **Past 12 hours**, and **Past 24 hours**. |
      |**Custom time period** |Select the time range for log export.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter can be set when<strong> Export range</strong> is set to <strong>Custom</strong>.</div><br> |
      

   * Export current page

      Click **Export current page**. In the **Export slow logs of the current page** dialog box, select the information included in the exported slow logs as needed. The exported slow log information may include **SQL template**, **SQL type**, **Database**, **Executing user**, **IP source**, **Execution times**, **Total time (s)** , **Maximum execution time (s)** , **Average execution time (s)** , **Maximum rows returned**, **Average rows returned**, **First appearance time**, and **Last appearance time**.

7. Click **OK**.

8. On the **Log management** tab, click the download icon, and then click **Export history**.

9. In the **Export history** dialog box, select the target task whose **Status** is **Generated**, and click **Export file** in the **Actions** column.
