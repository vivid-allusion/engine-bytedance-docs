---
title: "Resource consumption"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Resource-consumption"
---

The "Resource Consumption" page allows you to view resource consumption statistics for all Standard workspaces within the current account, including basic metrics and other & custom metrics. This helps you understand the distribution of the metrics in the system and adjust metric collection rules accordingly. This topic describes how to view the resource consumption of a workspace.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A Vital Managed Service for Prometheus (VMP) workspace has been created. For more details, refer to [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

<span id="LWIfnvnt"></span>
## Limits


* Resource consumption data is retained for up to 6 months.

* After a workspace is deleted, you cannot view its historical resource consumption.


<span id="9YhTmTYX"></span>
## Metric overview


|Metric type |Description |Common source |
|---|---|---|
|Basic metric |Basic resource metrics collected by the VMP service in standard monitoring scenarios. They are primarily used to reflect the health status of the infrastructure. |Basic resources such as clusters, nodes, workloads, Pods, and containers. |
|Other & user\-defined metrics |Metrics other than basic metrics, as well as user\-defined metrics. They are primarily used for business monitoring, application performance observability, and add\-on monitoring. |Custom collection tasks, business applications, exporters, and remote writes. |
|Workspace metrics |Statistics on metric consumption within the current workspace. They are used to display resource consumption, such as the number of metrics reported and written in this workspace. |Various metrics that are integrated into the current workspace, including basic metrics, other metrics, and custom metrics. |


<span id="lLUwVe0Y"></span>
## Procedure


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus).

2. In the left navigation pane, click **Resource Consumption** to go to the resource consumption query page.

3. Select the target workspace and time range to view resource consumption for the workspace within the time range.

   
   |Filter item |Description |
   |---|---|
   |Workspace filter |Select one or more target workspaces. Selecting the **All standard workspaces** option means viewing all workspaces that have not been deleted within the current account. |
   |Time range filter |Configure the time range for this query. Available options include preset time ranges (Last 3 days, Last 5 days, Last 7 days, and Last 14 days) and a custom time range.<br><br><br>* The maximum length for a custom time range is 6 months.<br><br>* When you select **Last x days**, the current day is included by default. For example, if today is 12:00 on October 7th and you select **Last 7 days**, the data displayed is from 00:00 on October 1st to 12:00 on October 7th. |
   

4. View statistics on the resource consumption monitoring dashboard, including workspace metric consumption statistics and job metric consumption charts.

   
   |Category |Metric |Description |
   |---|---|---|
   |Metric consumption statistics |Basic Metric Samples Reported |The total basic metric samples (in **millions**) cumulatively reported in the **past 24 hours** and the **past 14 days** within the selected data scope. |
   ||Other & Custom Metric Samples Reported |The total other & custom metric samples (in **millions**) cumulatively reported in the **past 24 hours** and the **past 14 days** within the selected data scope. |
   ||Metric Reporting Volume Trend (Million) |A trend chart showing the changes in the total reported volume of basic metrics and that of other & custom metrics over time within the selected data scope<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can drag the horizontal axis control to dynamically adjust the start and end times in the trend chart.</div><br> |
   ||Basic Metric Write Volume |The total size (**GB**) of basic metric samples cumulatively written in the **past 24 hours** and the **past 14 days** within the selected data scope. |
   ||Other & Custom Metric Write Volume |The total size (**GB**) of other & custom metric samples cumulatively written in the **past 24 hours** and the **past 14 days** within the selected data scope. |
   ||Metric Write Volume Trend (GB) |A trend chart showing the changes in the total written volume of basic metrics and that of other & custom metrics over time within the selected data scope.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can drag the horizontal axis control to dynamically adjust the start and end times in the trend chart.</div><br> |
   ||Workspace metric consumption list |The list of workspaces that have incurred metric resource consumption within the selected data scope, along with their metric consumption details. The consumption details include the workspace name, the specification, the cumulative reported metric samples, and the metric volume written over the past 24 hours. |
   |Top 50 job metrics in past 24h |Top 50 Job metric consumption in the last 24 hours |The top 50 jobs ranked by resource consumption over the past 24 hours within the selected data scope and their resource usage details. The resource usage details include the job name, owning workspace, cumulative metric samples reported, and cumulative metric volume written. This information helps you evaluate the reasonableness of metric consumption and adjust metric collection rules accordingly.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Job metric sample consumption statistics can be stored for up to 24 hours.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The search box in the upper\-right corner of the chart supports fuzzy search by job name.</div><br> |
   

5. In the workspace metric consumption list, click **Details** in the Actions column on the right side of the target workspace to view metric consumption for the workspace.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can select a preset time range (including Last 3 days, Last 5 days, Last 7 days, and Last 14 days) or specify a custom time range for this query.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The maximum length for a custom time range is 6 months.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When you select <strong>Last x days</strong>, the current day is included by default. For example, if the current time is 12:00 on October 7th and you select <strong>Last 7 days</strong>, the data displayed is from 00:00 on October 1st to 12:00 on October 7th.   </div>
   

   In addition to metric statistics and details, you can also view the top 50 metric consumption list by metric dimension, as well as metric reporting statistics, metric write statistics, and their details, including metric name, metric type, and the number of samples (millions).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can select a statistical time range of the last 10 minutes, 30 minutes, 1 hour, 3 hours, 6 hours, or 12 hours.   </div>
