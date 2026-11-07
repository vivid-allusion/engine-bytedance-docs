---
title: "Exporting monitoring data"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Exporting_monitoring_data"
---

Data export allows you to export cloud resource metrics within a specified time range to a local .xlsx file. You can use the exported data to compare historical data across time periods, verify data in batches, perform in\-depth local analysis, and create reports. The data can support fault reviews, capacity planning, and business optimization. This topic describes how to use the data export feature.

<span id="30eJdhxD"></span>
## Prerequisites


* The target resource has connected to Cloud Monitor and has metric data available for query.

* Your account has permissions to view the target resource. For authorization instructions, see [Authorizing IAM users](https://docs.byteplus.com/en/docs/cloudmonitor/Granting_permissions_to_an_IAM_user).


<span id="wY3o8t8p"></span>
## Limits


* Data export is supported only for resources whose metric data has been collected. If a resource has not been connected to Cloud Monitor or has no metric data, the export result will be an empty file.

* If the current account has insufficient permissions, the resource list will be empty or the task will fail.

* To export the monitoring data of API Gateway (APIG), ModelArk, Container Registry (CR), Machine Learning Platform (MLP), Microservices Engine (MSE), and VKE, see [Exporting metrics to Message Queue for Kafka](https://docs.byteplus.com/en/docs/vmp/Creating_an_export_task), [Exporting metrics to self-managed Prometheus](https://docs.byteplus.com/en/docs/vmp/Exporting_metrics_to_self-managed_Prometheus), and [Exporting metrics to TOS](https://docs.byteplus.com/en/docs/vmp/Exporting_metrics_to_TOS).


<span id="V6oljHXg"></span>
## Procedure


<Tabs>
<Tab zoneid="u2KA5srUpa" title="Method 1: Access via the Data export page">
<TabTitle>Method 1: Access via the Data export page</TabTitle>

This method is suitable when you have a specific export target and want to select resource types and metrics as needed. On the **Data export** page, you can centrally manage all export tasks.


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/observe/cloud-monitor/overview). 

2. In the left navigation pane, click **Data Export**.

3. Click **New export task**. Complete the parameter configuration and then click **Confirm**.

   
   |Parameters |Description |
   |---|---|
   |Task name |Specify a custom name for the export task to identify it and distinguish it from other tasks in the task list. |
   |Export time range |The time range of monitoring data to be exported. For troubleshooting, select a shorter time range to reduce interference from irrelevant data. For trend analysis or periodic reviews, select 3 days, 7 days, or a custom range.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The custom export time range can be up to 31 days.</div><br> |
   |Statistical method |Specify the calculation method for data in each aggregation period. You can select multiple options.<br><br><br>* **Maximum value**: Reflects the peak value within the period. This is suitable for identifying abnormal spikes.<br><br>* **Minimum value**: Reflects the trough value within the period. This is suitable for evaluating the lower limit of availability.<br><br>* **Average**: Reflects the overall level. This is suitable for viewing normal trends.<br><br>* **Sum value**: Adds the data values within the period. This is suitable for cumulative metrics such as counts and totals. |
   |Aggregation time granularity |The interval at which data is exported, which determines the duration covered by each data point. A smaller granularity delivers more detailed data but a larger file, while a larger granularity delivers a smoother trend but may hide short\-term fluctuations. |
   |Resource type |The cloud product type for which monitoring data is exported. For supported resource types, see the console. |
   |Region |The region where the resource is located.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Select the region where the resource is deployed. Otherwise, the resource list may be empty.</div><br> |
   |Select resources |Select the specific instance whose data you want to export. |
   |Subnamespace |The data aggregation level, which determines how the exported data is broken down by dimension. Make sure the selected dimension matches the target metric. |
   |Select metrics |Select the metrics to export. You can search for metrics and select multiple metrics, such as `5xx_send_ratio` and `504_count`. |
   

4. After creating the task, wait for it to complete. The **Completed** state indicates that the task is complete.

5. In the Actions column of the target task, click **Download** to download the exported .xlsx file.


</Tab>
<Tab zoneid="pfu3naV1NQ" title="Method 2: Access via the Cloud Monitor page">
<TabTitle>Method 2: Access via the Cloud Monitor page</TabTitle>

This method is suitable when you want to view monitoring charts first and then export data as needed. You can directly create an export task on the current monitoring page. After the task is created, you can go to the **Data export** page to view the task progress and download the result file.


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/observe/cloud-monitor/overview). 

2. In the left navigation pane, click **Cloud Service Monitor**. On the page that appears, select the target cloud product.

3. Click **Export monitoring data**. Specify the parameters and click **Confirm**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For parameter configuration descriptions, see <strong>Method 1: Access via the Data export page</strong>.   </div>
   

4. In the pop\-up dialog box, click **Go to data export**. On the **Data export** page, view the task progress and download the result file.

5. After creating the task, wait for it to complete. The **Completed** state indicates that the task is complete.

6. In the Actions column of the target task, click **Download** to download the exported .xlsx file.


</Tab>
</Tabs>


<span id="606mFld7"></span>
## What to do next

To delete an export task, click the "..." icon in the Actions column of the target task or click **Delete** on the task details page.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Deleted tasks cannot be recovered. Before deleting the task, make sure that you have downloaded and saved the result file.</div>
