---
title: "Service log dashboards"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/service_log_dashboards"
---

After a data transformation task or a task of shipping data to Torch Object Storage (TOS) is created, Torch Log Service (TLS) records the status and progress of the task using service logs. In addition, TLS offers service log dashboards to visualize data. You can quickly view the task run information on service log dashboards.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">By default, dashboards display statistical data in the last 5 minutes. You can change the time range as needed. The service logs are retained for 7 days, so you can only view data in the last 7 days.</div>


<span id=".5Luq6KGo55uY57G75Z6L"></span>
## Dashboard types

The service log feature supports the following predefined dashboards. To view a dashboard, find the target project tls_service\-project. In the left\-side navigation pane, click **Dashboard** and select a dashboard from the list of dashboards.


|Dashboard |Description |
|---|---|
|tls\-service\-etl\-dashboard |Data transformation dashboard. After you create a data transformation task for the first time, TLS automatically creates a dashboard to display the run data and abnormal data of the data transformation task. |
|tls\-service\-shipper\-dashboard |Data shipping dashboard. After you create a task of shipping data to TOS for the first time, TLS automatically creates a dashboard to display the data shipping progress, read and write traffic, and task details. |
|tls\-service\-alarm\-dashboard |Alarm history dashboard. After you create and enable an alarm policy for the first time, TLS automatically creates a dashboard to display the number of alarm times, execution success rate, alarm triggering trend, and alarm history. |


<span id="tls-service-etl-dashboard"></span>
## tls\-service\-etl\-dashboard

By default, the data transformation dashboard displays the data of all data transformation tasks in the project, including data processing exceptions and task progress information such as the number of input log entries. You can filter data in the dashboard by task_id and view the details of a specified task.

<span id="tls-service-shipper-dashboard"></span>
## tls\-service\-shipper\-dashboard

By default, the data shipping dashboard displays the run data of all tasks of shipping data to TOS in the project, including the number of shipped log entries, processing rate trend, and read and write traffic trends. You can filter data in the dashboard by task_id and view the details of a specified task.

<span id="0cbb0660"></span>
## tls\-service\-alarm\-dashboard

By default, the alarm history dashboard displays the execution history of alarm policies, including the number of alarm times, execution success rate, alarm triggering trend, and alarm history. You can filter data by alarm policy ID in the dashboard to view the execution history of a specified alarm policy. You can also find the target alarm policy and click the **Execution information** tab to view the dashboard. For more information on the charts, refer to [Viewing execution information](https://docs.byteplus.com/docs/tls/view_alarm_policy#.5p-l55yL5omn6KGM5L-h5oGv).
