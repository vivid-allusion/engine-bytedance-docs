---
title: "Viewing monitoring data"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/viewing_monitoring_data"
---

Database Transmission Service (DTS) supports viewing monitoring metrics related to data transmission, helping you understand the running status and usage of instances in detail. This topic describes how to view the monitoring data of DTS.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* By default, the monitoring metrics data for the most recent 1 day is displayed. For more information about monitoring metrics, refer to [Monitoring metrics](https://docs.byteplus.com/en/docs/DTS/monitoring_metrics).

* It supports viewing migration or synchronization monitoring metrics data within the last 7 days at most.

* The units adopted in the monitoring metrics table are all base units. You can find details of the exact units used for each monitoring item on the console. The units displayed on the console will be flexibly adjusted based on the monitoring values following the SI standards. For example, the base unit of full transmission BPS is Byte/s. If the monitoring value of full transmission BPS is large, the unit on the console may be adjusted to KB/s, MB/s, GB/s, etc.


<span id=".5p-l55yL5pWw5o2u6L-B56e755uR5o6n5pWw5o2u"></span>
## Viewing data migration monitoring data


1. Log on to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.


3. In the left navigation pane, click **Data migration**.

4. On the **Migration task list** page, find the target task and click the task name.

4. Click the **Monitor** tab. Under the **Monitor** tab, you can view the monitoring metric details of the full migration and incremental migration rates within the specified time.

<span id=".5p-l55yL5pWw5o2u5ZCM5q2l55uR5o6n5pWw5o2u"></span>
## Viewing data synchronization monitoring data


1. Log on to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.


3. In the left navigation bar, click **Data synchronization**.

4. On the synchronization task list page, find the target synchronization task, and select  **...**  \> **Task details** on the right of the task progress.

5. Click the **Monitor** tab. Under the **Monitor** tab, you can view the monitoring metric details of the full synchronization and incremental synchronization rates within the specified time.

<span id=".5p-l55yL5pWw5o2u5qCh6aqM55uR5o6n5pWw5o2u"></span>
## Viewing data verification monitoring data


1. Log on to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.


3. In the left navigation bar, click **Data verification**.


4. On the Data validation list page, find the target verification task, and click the task name.

5. Click the **Monitor** tab. Under the **Monitor** tab, you can view the monitoring metric details of the full validation and incremental validation rates within the specified time.


<span id=".55u45YWz5paH5qGj"></span>
## Related document

Cloud Monitor allows you to set alert policies. You can monitor DTS's data transmission performance and running status on Cloud Monitor. You can configure the parameters as needed. For parameter instructions, refer to [Creating alarm strategy](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy).
