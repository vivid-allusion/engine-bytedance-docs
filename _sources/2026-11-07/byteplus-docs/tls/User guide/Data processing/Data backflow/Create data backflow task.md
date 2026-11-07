---
title: "Create data backflow task"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Create_data_backflow_task"
---

The data backflow task will automatically create a scheduled SQL task and a log delivery task (with the target type set to deliver to TOS), helping you export logs that meet the requirements.

This section describes how to create a data backflow task.

<span id="a8fdd8d5"></span>
## Prerequisites


* The source\-side project and log topic have been created, and a key\-value type index has been configured.

* The target\-side project and log topic have been created, and an index has been configured.

* If the target\-side is set to deliver to TOS, the following conditions must also be met:

   * Object storage has been enabled in BytePlus, and a bucket has been created in the same region as the specified log topic. For details, see [Create a bucket](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).

   * TLS needs to assume the ServiceRoleForTLS role to access other cloud service resources across services. That is, you must grant TLS permission to access and write to TOS resources.

      If you have not yet created the ServiceRoleForTLS role, TLS will guide you through the process when you create the delivery configuration. It is recommended to use a BytePlus account for authorization. For related instructions, see [cross-service access authorization](https://docs.byteplus.com/66o8pm3q/155604).


<span id="2df18f57"></span>
## Create a data backflow task


1. Log in to [TLS console](https://console.byteplus.com/tls).

2. Select the region where log service is located from the top navigation bar.

3. In the left navigation bar, select **Data processing** \> **Data backflow**.

4. On the **Data backflow list** page, click **Create** **LogBackFlow task**.

5. On the Create LogBackFlow task page, complete the following configuration steps.

   1. Enter the basic configuration.

      
      |Configuration |Description |
      |---|---|
      |Task name |The name of the data backflow task. This name will be automatically used as the scheduled SQL task name. |
      |Description |A brief description of the data backflow task. |
      

   2. Configure the data source.

      
      |Configuration |Description |
      |---|---|
      |Data source type |Select the data source type for the data backflow task: currently, only **Torch** **Log** **Service** **TLS** is supported. |
      |Project |The project where the original logs for data backflow are located. |
      |Topic |The log topic where the original logs for data backflow are located. |
      

   3. Configure the target.

      
      |Configuration |Description |
      |---|---|
      |Target Region |The target Region where the logs for data backflow are located. |
      |Project |The project where the target logs for data backflow are located. |
      |Topic |The log topic where the target logs for data backflow are located.<br><br>The target log topic must not be the same as the source log topic. |
      |Other goals |Log shipping to TOS is supported. After enabling, you must also configure the following:<br><br><br>* Bucket: The name of the designated bucket for log shipping to TOS.<br><br>* Select file path:<br><br>   Select or manually enter the file prefix (folder path) or the complete file path. Leaving it empty means collecting all files under this bucket.<br><br>* Shard format:<br><br>   The TOS bucket directory will be dynamically generated according to the creation time of the shipping task. It must not start with a forward slash (/). The default value is `%Y/%m/%d/%H/%M`, such as `2022/06/30/14/00`.<br><br>* Compressed mode: The compression mode for the data. Supported modes are none, snappy, gzip, and lz4.<br><br>* Shipping format: The format for log shipping. Supported formats are CSV, JSON, and JSONL. |
      

   4. Configure the time range.

      
      |Configuration |Description |
      |---|---|
      |Start time |The scheduling start time for the data backflow task, that is, the time when the first instance is scheduled. |
      |End time |The scheduling end time for the data backflow task.<br><br><br>* Continuous execution: The task is executed continuously.<br><br>* Custom time: Manually select the end time for task scheduling. |
      

   5. Configure the rules.

      
      |Configuration |Description |
      |---|---|
      |upper limit of single return |The log backfill task is executed periodically and continuously. You can set the upper limit for a single backfill, up to 10,000 entries. |
      |Scheduling cycle |The scheduling period of the scheduled SQL analysis task determines the scheduling time for each instance. The scheduling period supports specifying a time interval or a fixed trigger time.<br><br>It is recommended that the length of the **scheduling period** **be greater than or equal to** the length of the query **time window**; otherwise, scheduling may not be timely and query results may be incorrect. For example, if the scheduling period is every 10 minutes, the maximum length of the SQL time window is 10 minutes.<br><br>You can select any of the following configurations:<br><br><br>* **Minutes**: Execute once every 1–1440 minutes.<br><br>* **Days**: Execute once at a fixed time each day.<br><br>* **Cron**: Specify the task scheduling time using a Cron expression. The minimum granularity is one minute, the maximum is 30 days, and the 24\-hour format is supported.<br><br>   For example, `0 18 * * *` means the scheduled SQL analysis task is triggered once every day at 18:00. |
      |Time zone selection |A time zone must be selected when the **scheduling period** is Cron. For a list of common time zones, see [Select a time zone](https://docs.byteplus.com/en/docs/38/%2F66o8pm3q%2Fsqi77bug). |
      |SQL time window |When the scheduled SQL analysis task runs, the time range for log query and analysis uses a left\-closed, right\-open format.<br><br>The maximum SQL time window is 31 days, and the minimum is 1 minute. Setting the SQL time window to more than 24 hours may cause the execution instance to fail or the calculation results to be inaccurate due to excessive data volume. For the syntax of the SQL time window, refer to [SQL time window syntax](https://docs.byteplus.com/66o8pm3q/1130975).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="default">Configuration example:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Start time: 2023\-8\-14 10:00</div><br><br><br>* <div data-tips="true" data-tips-type="default">Schedule interval: Execute once every 60 minutes</div><br><br><br>* <div data-tips="true" data-tips-type="default">SQL time window: <code>[@h-1h,@h)</code></div><br><br><br>* <div data-tips="true" data-tips-type="default">Execution delay: 10 seconds</div><br><br><br><br><div data-tips="true" data-tips-type="default">Create the first instance at 2023\-8\-14 10:00:00, start the instance execution at 10:00:10, and analyze log data from [09:00:00~10:00:00).</div><br><br><br><div data-tips="true" data-tips-type="default">Create the second instance at 2023\-8\-14 11:00:00, start the instance execution at 11:00:10, and analyze log data from [10:00:00~11:00:00).</div><br> |
      |Task timeout |If the task exceeds the maximum timeout or the maximum number of retries, the scheduled SQL analysis task will set the status to failed and end. You can receive alerts and retry manually.<br><br><br>* Maximum time range: 60–1800 seconds.<br><br>* Maximum number of retries: 1–20 times. |
      |Maximum number of retries |If the task exceeds the maximum timeout or the maximum number of retries, the scheduled SQL analysis task created by the data backfill task will set the status to failed and end. You can receive alerts and retry manually. |
      |Execution delay |The delay time for each scheduling can be set from 0 to 120 seconds.<br><br>When the log data volume is large and collection tasks are busy, there may be some delay in writing data to the log topic. In this scenario, you can specify an execution delay time to ensure data integrity during query and analysis. |
      |Return fields |Return fields originate from key\-value fields in the data source index.<br><br>You can use the original field name or set an alias (aliases must not be duplicated) as the exported field name. Aliases must be set in the following scenarios:<br><br><br>* JSON format fields<br><br>* TLS reserved fields |
      |Filter configuration |You can filter by setting filter conditions for return fields, and multiple `AND` relationship filter conditions are supported. |
      |Preview |Click **Preview filter results** to view the preview results.<br><br>After modifying field selection or field names, click **Refresh filter results** to update the table. |
      

   6. Click **Create data backflow task.** 


<span id="84870070"></span>
## Analyze data backflow logs

After the data backflow task runs successfully and the scheduled SQL task is executed successfully, you can view and analyze the data backflow logs in the target project.


1. Log in to [TLS console](https://console.byteplus.com/tls).

2. Select the region where log service is located from the top navigation bar.

3. On the left navigation pane, select **Resource management**  **\> Project**.

4. Click the name of the target project to enter its details page.

5. Click the target log topic name, or click **query and analysis** in the **Actions** column to enter the log query and analysis page.

6. Manually enter a query statement, or use the AI assistant to analyze logs after data backflow. For details, see [Log analysis](https://docs.byteplus.com/en/docs/38/%2F66o8pm3q%2F3aox5wed).


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Notice</div>


<div data-tips="true" data-tips-type="default">You can view the target project and log topic in schedule SQL tasks.</div>


<div data-tips="true" data-tips-type="default">In the data return task list, click the schedule SQL task name in the <strong>Schedule SQL Task Name/ID </strong>column to enter the schedule SQL task details page, where you can view the target project and target log topic name.</div>


<span id="82e59beb"></span>
## Next steps

View or edit data backflow tasks. For details, see [Manage data backflow tasks](https://docs.byteplus.com/en/docs/38/%2F66o8pm3q%2Fx1tgb6j7).
