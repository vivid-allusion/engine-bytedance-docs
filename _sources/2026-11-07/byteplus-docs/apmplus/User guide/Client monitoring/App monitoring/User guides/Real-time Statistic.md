---
title: "Real-time Statistic"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Real-time_Statistic"
---

Real\-time Statistic provides dashboards that refresh data in real time, including statistics for common core metrics and alert statistics. It is commonly used in scenarios where metric changes need to be monitored in real time after a release goes live.

This page only displays today's data, and the dashboard automatically refreshes every 30 seconds.

<span id="29992503"></span>
## Filter dimensions

Support filtering data by time and Operating System.


|**Subnamespace** |**DescriptionS** |
|---|---|
|time |Filter data by a time interval.<br><br><br>* **Recent**: View data for the last X days. By default, data for the past 7 days is displayed. You can configure it to display data for the past **1 day**, **7 days**, **30 days**, or **60 days**.<br><br>* **Scope**: View data within the yyyy\-mm\-dd to yyyy\-mm\-dd time period. The platform retains data for up to 90 days, so the earliest start time you can select is 90 days ago. |
|System |Select an operating system.<br><br><br>* **All**<br><br>* **iOS**<br><br>* **Android** |


<span id="1e04a348"></span>
## Statistical data

The statistical data area displays **alert count**, **crash alert count**, **error alert count**, **top 3 tasks triggering alerts**, **PV**, **UV**, and **user usage duration**.


|**Metric** |**DescriptionS** |
|---|---|
|alert count |Alert count with filter conditions applied |
|Crash alert count |Crash alert count under filter conditions |
|Error alert count |Error alert counts under filter conditions |
|PV |Filtered page views |
|UV |Unique visitor count under filter conditions (Unique Visitor) |
|Top 3 tasks that trigger alerts |The alert task with the highest alert count under filter conditions |
|user session duration |User foreground application usage time under filter conditions<br><br>User session duration = time the application remains active in the Foreground = Background entry time \- Foreground entry time<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only Android supports viewing the user session duration metric. For the user session duration metric on iOS, refer to <a href="https://docs.byteplus.com/en/docs/apmplus/MetricKit">MetricKit</a>.</div><br> |
