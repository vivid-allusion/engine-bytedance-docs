---
title: "Create scheduled SQL analysis and store data to managed Prometheus"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Create_scheduled_SQL_analysis_data_storage_to_managed_Prometheus"
---

The Log Service supports creating scheduled SQL analysis tasks through the console to regularly query and analyze source log topics, saving the processed log data to target log topics or converting it to [time series data format](https://docs.byteplus.com/en/docs/vmp/Format-of-Prometheus-time-series-data), and storing [Gauge type metrics](https://docs.byteplus.com/en/docs/vmp/Prometheus-metric-types) in the Vital Managed Service for Prometheus (VMP) workspace.

This document describes the steps to create scheduled SQL analysis tasks and convert data into metrics saved in the managed Prometheus workspace.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Log data has been successfully collected to the source log topic. Refer to [Overview](https://docs.byteplus.com/docs/tls/getting_started_overview) for detailed steps.

* The source log topic has indexing configured. Refer to [Configure Index](https://docs.byteplus.com/docs/tls/Configure-indexes-2) for detailed steps.

* The managed Prometheus workspace has been created and must be in the same region as the Log Service. For detailed steps, refer to [Create a general workspace](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* Before using the schedule SQL feature for the first time, complete cloud resource access authorization by granting the schedule SQL analysis task permission to access and write data to the managed Prometheus workspace. After authorization and successfully starting the schedule SQL analysis task, the task will use the ServiceRoleForTLS role to write computing results to the managed Prometheus workspace, so users must also have write permissions for managed Prometheus data.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When creating a schedule SQL analysis task for the first time in the log service console, the system guides you through the authorization process. It is recommended to authorize with the  account. For details, refer to <a href="https://docs.byteplus.com/docs/tls/Authorizing_cross-service_access">Cross\-service access authorization</a> and <a href="https://docs.byteplus.com/en/docs/vmp/Permission-overview">Permission overview</a> for managed Prometheus permissions.   </div>
   

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Torch Log Service console](https://console.byteplus.com/tls).

2. On the top navigation bar, select the region where the log service is located.

3. In the left navigation bar, choose **Data Processing** \> **Schedule SQL analysis**.

4. On the **Schedule SQL analysis task list** page, click **Create schedule SQL analysis task**.

5. Fill in the basic configuration of the task, then click **Next: SQL analysis rule configuration.** 

   
   |Configuration |Description |
   |---|---|
   |Task name |Name of the scheduled SQL analysis task. |
   |Description |Simple description of the schedule SQL analysis task. |
   |Source log project |The project containing raw logs for scheduled SQL analysis. |
   |Source log topic |Log topic containing the original logs for scheduled SQL query and analysis. |
   |Target log topic |After executing the scheduled SQL analysis task, the processed log data is stored in a hosted Prometheus workspace.<br><br><br>* Target type: select a **hosted Prometheus workspace**.<br><br>* Workspace: select a hosted Prometheus workspace to store data. If there is no suitable workspace, create one based on page instructions. |
   |task status |Whether to start the scheduled SQL analysis task immediately.<br><br><br>* Checked (default): start the scheduled SQL analysis task immediately after completing the configuration.<br><br>* Unchecked: the scheduled SQL analysis task remains paused after configuration and must be started manually later. |
   

6. Fill in the SQL analysis rule configuration, then click **Submit**.

   
   |Configuration |Description |
   |---|---|
   |Start time |The scheduled start time of the timed SQL analysis task, which is the start time when the first instance is scheduled.<br><br>After startup, the log service creates instances and starts scheduled SQL analysis on time according to the specified rules. |
   |End time |Scheduled SQL query and analysis task end time.<br><br>After the end time, the log service will no longer create instances or execute scheduled SQL query and analysis, but the task status remains running until manually paused. |
   |Schedule cycle |The schedule cycle for schedule SQL analysis tasks; this cycle determines each instance's scheduling time. The schedule cycle supports specifying time intervals or fixed trigger times.<br><br>The **schedule cycle** length is recommended to be **greater than or equal to** the **query time window** length; otherwise, scheduling may be delayed and query results may be inaccurate. For example, if the schedule cycle triggers every 10 minutes, the SQL time window length should be at most 10 minutes.<br><br>You can select any of the following configurations:<br><br><br>* **seconds**: execute every 30 to 600 seconds.<br><br>* **Minutes**: execute once every 1~1440 minutes.<br><br>* **Days**: execute once daily at a fixed time.<br><br>* **Cron**: specify task schedule using Cron expression, with a minimum granularity of minutes and maximum support of 30 days, using 24\-hour format.<br><br>   For example, `0 18 * * *` means scheduling the schedule SQL analysis task daily at 18:00. |
   |Time zone selection |**When the schedule cycle** is set to **Cron**, a time zone must be selected.  |
   |SQL time window |During scheduled SQL query and analysis task execution, the time range for log query and analysis, left\-closed and right\-open interval.<br><br>The maximum SQL time window for managed Prometheus is about 6 hours. Refer to the [SQL time window syntax](https://docs.byteplus.com/docs/tls/sql_time_window_syntax) for details. Support quick filling of the following expressions:<br><br><br>* Last 15 minutes: @m\-15m, @m<br><br>* Last 3 hours: @h\-3h, @h<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Configuration example:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Start time: 2023\-8\-14 10:00</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Schedule cycle: execute once every 60 minutes</div><br><br><br>* <div data-tips="true" data-tips-type="tip">SQL time window: <code>[@h-1h,@h)</code></div><br><br><br>* <div data-tips="true" data-tips-type="tip">Execution delay: 10 seconds</div><br><br><br><br><div data-tips="true" data-tips-type="tip">Create the first instance at 2023\-8\-14 10:00:00, start executing the instance at 10:00:10, analyzing log data during [09:00:00~10:00:00).</div><br><br><br><div data-tips="true" data-tips-type="tip">Create the second instance at 2023\-8\-14 11:00:00, start executing the instance at 11:00:10, analyzing log data during [10:00:00~11:00:00).</div><br> |
   |SQL |Schedule SQL analysis tasks regularly execute query and analysis statements that comply with the log service’s query and analysis syntax. For detailed grammar instructions, refer to [query and analysis overview](https://docs.byteplus.com/docs/tls/Query-overview-2) and [analysis overview](https://docs.byteplus.com/docs/tls/Analysis-overview). |
   |Metric name |Select fields of **numeric type** from SQL execution results as metric names delivered to hosted Prometheus time series, reflecting the meaning of the monitored samples. Related concepts can be found in [hosted Prometheus time series data format](https://docs.byteplus.com/en/docs/vmp/Format-of-Prometheus-time-series-data).<br><br><br>* Can only consist of ASCII characters, digits, underscores, and colons, and must conform to the regular expression `[a-zA-Z_:][a-zA-Z0-9_:]*`.<br><br>* If naming rules are not met, AS syntax can be used to rename the field. |
   |Metric label |Select **non\-time type** fields from SQL execution results as metric labels for time series delivered to the hosted Prometheus. These labels represent sample feature dimensions, allowing hosted Prometheus to filter and aggregate sample data through these dimensions, such as `group by` dimensions.<br><br><br>* Must consist only of ASCII letters, digits, and underscores, conforming to the regular expression `[a-zA-Z_][a-zA-Z0-9_]*`.<br><br>* When the naming conventions are not met, the AS syntax can be used to rename fields. |
   |Custom tag |Customize the metric tag's key and value.<br><br><br>* Only ASCII characters, numbers, and underscores are allowed, matching the regular expression `[a-zA-Z_][a-zA-Z0-9_]*`.<br><br>* The total number of custom tags and metric tags cannot exceed 30. |
   |Time column |Select the **time type** field from the SQL execution results as the time column, which serves as the timestamp for the metric data.<br><br>If not selected, the start time from the SQL time range is used as the timestamp for the metric data.<br><br><br>* The metrics time hosted by Prometheus supports up to 6 hours; data exceeding this time range will fail to be written.<br><br>* Supports selecting UNIX time and Timestamp type with millisecond precision.<br><br>   For example: 1629876543.123, 2021\-08\-25T12:22:23.123+08:00.<br><br>* Supports using DATE_FORMAT and TO_UNIXTIME functions to convert time types. |
   |Task timeout |When the task exceeds the maximum timeout or retry limit, the schedule SQL will mark the status as failed and end. You can receive alerts and retry manually.<br><br><br>* Maximum time range: 60 to 1800 seconds.<br><br>* Maximum count range: 1 to 20 times. |
   |Execution delay |The delay time for each schedule, which can be set from 0 to 120 seconds.<br><br>When log data volume is large and collection tasks are busy, data writing to the log topic may be delayed. In this scenario, an execution delay time can be set to ensure data integrity during query and analysis. |
   

7. View data dumped to the hosted Prometheus.

   1. Confirm the scheduled SQL task has been successfully scheduled.

      In the log service’s **data processing** \> **schedule SQL analysis** **schedule SQL analysis task list**, click the name of the created scheduled SQL task to check the task execution status, ensuring at least one instance is **successfully scheduled**.

   2. Log in to the hosted Prometheus console.

   3. In the top navigation bar, select the region where the workspace set in the scheduled SQL task is located.

   4. In the left navigation bar, click **Explore.** 

   5. Select the workspace set in the scheduled SQL task and choose the query time.

   6. Enter the query statement or click **Metric search**, and select the metric name from the list to search. Refer to [metric query](https://docs.byteplus.com/en/docs/vmp/explore-metrics) for related syntax.


<span id="4a59fc3e"></span>
## Example of log data dumping

<span id="d0b0425d"></span>
### Raw logs from the log service

```Python
{
        "ErrorLog": "",
        "__package_offset__": "1610612771",
        "__path__": "",
        "__process_end_time__": "1754240400",
        "__process_id__": "31373534-3234-3034-3030-2d3238373463",
        "__process_start_time__": "1754229600",
        "__process_time__": "1754240400",
        "__schedule_time__": "1754240461720",
        "__source__": "",
        "__task_id__": "fe948057-0410-430e-8280-d7a4e1e8fc1c",
        "__time__": 1754362780000,
        "__tls_svc_model_version__": "1750953766",
        "__tls_svc_signature_id__": "485795292"
}
```


<span id="fb23fca1"></span>
### Example of dump metric configuration


* SQL：`* | SELECT * limit 10000`

* Metric names: `__schedule_time__`, `__process_time__`

* Metric labels: `__task_id__`, `__time__`

* Time column: `__time__`


<span id="0afecaf8"></span>
### Metrics stored in managed Prometheus

Generates the following 2 metrics and stores data into the managed Prometheus workspace ordered by the selected time column `__time__`.

```Python
__schedule_time__{__task_id__="fe948057-0410-430e-8280-d7a4e1e8fc1c", __time__="1754362780000"}
__process_time__{__task_id__="fe948057-0410-430e-8280-d7a4e1e8fc1c", __time__="1754362780000"}
```
