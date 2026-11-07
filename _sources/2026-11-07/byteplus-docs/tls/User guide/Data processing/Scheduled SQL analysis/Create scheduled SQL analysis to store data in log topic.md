---
title: "Create scheduled SQL analysis to store data in log topic"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/create_a_scheduled_sql_task"
---

The log service supports creating scheduled SQL analysis tasks through the console to regularly query and analyze the source log topic, then save the processed log data to the target log topic or store it as time series data metrics in the Prometheus workspace.

This document describes the steps to create a scheduled SQL analysis task and save the data to the target log topic.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Log data has been successfully collected to the source log topic. See [Overview](https://docs.byteplus.com/docs/tls/getting_started_overview) for detailed steps.

* The target log topic has been created to store the processed log data. See [Log Topic](https://docs.byteplus.com/docs/tls/Managing_topics) for detailed steps.

* Both source and target log topics have configured indexes. See [Configure Index](https://docs.byteplus.com/docs/tls/Configure-indexes-2) for detailed steps.

* Before using the schedule SQL feature for the first time, you need to complete cloud resource access authorization, granting the schedule SQL analysis task permission to access and write data to the specified log topic. After completing authorization and successfully starting the schedule SQL analysis task, the task uses the ServiceRoleForTLS role to write computation results to the specified log topic.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When creating a schedule SQL analysis task for the first time in the log service console, the system guides you through the authorization process. It is recommended to authorize using an account. For details, see <a href="https://docs.byteplus.com/docs/tls/Authorizing_cross-service_access">cross\-service access authorization</a>.   </div>
   

<span id=".5pON5L2c5q2l6aqk"></span>
## Steps


1. Log in to the [Torch Log Service console](https://console.byteplus.com/tls).

2. On the top navigation bar, select the region where the log service is located.

3. In the left navigation pane, choose **data processing** \> **schedule SQL analysis**.

4. On the **schedule SQL analysis task list** page, click **create schedule SQL analysis task**.

5. On the create schedule SQL task page, complete the following configurations.

   1. Fill in the basic task settings, then click **next: SQL analysis rule configuration.** 

      
      |Configuration |Description |
      |---|---|
      |Task name |the name of the schedule SQL analysis task |
      |Description |A brief description of the scheduled SQL analysis task. |
      |Source log project |The original logs for scheduled SQL query and analysis are located in the project. |
      |Source log topic |The log topic containing the original logs for scheduled SQL analysis. |
      |target log topic |After executing the scheduled SQL query and analysis task, specify the target Region, project, and log topic for storing the processed log data.<br><br><br>* Target type: select **TLS log topic**.<br><br>* Target Region: select the Region for storing log data.<br><br>* Project: select the project for storing log data.<br><br>* Log topic: select the log topic for storing log data. Ensure the log topic is indexed. |
      |Task status |Whether to start the scheduled SQL analysis task immediately.<br><br><br>* Checked (default): start the schedule SQL analysis task immediately after task configuration is completed.<br><br>* Unchecked: the schedule SQL analysis task will be paused after configuration is completed and requires manual activation when appropriate. |
      

   2. Fill in the SQL analysis rule configuration, then click **Submit**.

      
      |Configuration |Description |
      |---|---|
      |Start time |The schedule start time for a scheduled SQL analysis task, indicating when the first instance is triggered.<br><br>After starting, the log service creates instances and launches scheduled SQL analysis on time according to the specified rules. |
      |End time |End time for scheduling the scheduled SQL analysis task.<br><br>After the end time, the log service will no longer create instances or execute scheduled SQL analysis, but the task status remains running until the task is manually paused. |
      |Scheduling cycle |Schedule cycle of the schedule SQL analysis task; the schedule cycle determines the scheduling time for each instance. The schedule cycle supports specifying either a time interval or a fixed trigger time.<br><br>It is recommended that the **schedule cycle** length be **greater than or equal to** the length of the **query time window** to avoid delays in scheduling and incorrect query results. For example, if the schedule cycle runs every 10 minutes, the maximum SQL time window length is 10 minutes.<br><br>You can select any of the following configurations:<br><br><br>* **Minutes**: runs once every 1~1440 minutes.<br><br>* **Days**: runs once daily at a fixed time.<br><br>* **Cron**: uses a Cron expression to specify the task schedule time, with a minimum granularity of minutes and a maximum support of 30 days, using the 24\-hour format.<br><br>   For example, `0 18 * * *` means scheduling the scheduled SQL analysis task once daily at 18:00. |
      |Time zone selection |When the **schedule cycle** uses Cron, a time zone must be selected.  |
      |SQL time window |For scheduled SQL analysis tasks, specify the time range for log query and analysis in a left\-closed, right\-open format.<br><br>The SQL time window ranges from a minimum of 1 minute to a maximum of 31 days. Setting the SQL time window to over 24 hours may cause execution instance failures or inaccurate results due to excessive data volume. Please refer to [SQL time window syntax](https://docs.byteplus.com/docs/tls/sql_time_window_syntax) for the SQL time window syntax.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Configuration example:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Start time: 2023\-8\-14 10:00</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Schedule: execute every 60 minutes</div><br><br><br>* <div data-tips="true" data-tips-type="tip">SQL time window: <code>[@h-1h,@h)</code></div><br><br><br>* <div data-tips="true" data-tips-type="tip">execution delay: 10 seconds</div><br><br><br><br><div data-tips="true" data-tips-type="tip">create the first instance at 2023\-8\-14 10:00:00, start executing the instance at 10:00:10, analyzing log data during [09:00:00~10:00:00)</div><br><br><br><div data-tips="true" data-tips-type="tip">create the second instance at 2023\-8\-14 11:00:00, start executing the instance at 11:00:10, analyzing log data during [10:00:00~11:00:00)</div><br> |
      |SQL |Scheduled SQL analysis tasks regularly execute query and analysis statements that comply with the log service's query and analysis syntax. For detailed syntax, refer to [query overview](https://docs.byteplus.com/docs/tls/Query-overview-2) and [analysis overview](https://docs.byteplus.com/docs/tls/Analysis-overview). |
      |task timeout |If the task exceeds the maximum timeout or retry limit, the scheduled SQL sets the status to failed and ends. You can acknowledge alerts and retry manually.<br><br><br>* Maximum time range: 60~1800 seconds.<br><br>* Maximum count range: 1~20 times. |
      |Execution delay |Delay time for each schedule, adjustable from 0 to 120 seconds.<br><br>When log data is large and collection tasks are busy, data writing to the log topic may be delayed. In this case, specify the execution delay time to ensure data completeness during query and analysis. |
