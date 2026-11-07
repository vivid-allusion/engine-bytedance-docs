---
title: "Dashboard common operations"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Managing_dashboards"
---

After you create a dashboard and add charts to the dashboard, you can perform various operations to manage the dashboard. This topic describes how to manage a dashboard, such as modifying the configurations of the dashboard, and viewing and sharing the dashboard and charts on the dashboard.

<span id="编辑操作"></span>
## Dashboard operations


|Operation |Description |
|---|---|
|Modify the description of dashboard |In the upper\-right corner of the dashboard, click **Settings**. On the **General settings** Tab, modify the description of the dashboard. |
|Modify the name of dashboard |In the upper\-right corner of the dashboard, click **Settings**. On the **General settings** Tab, modify the name of the dashboard. |
|Delete a dashboard |In the upper\-right corner of the dashboard, click **Settings**. On the **General settings** Tab, click **Delete dashboard**. |
|Filter dashboards |Search for dashboards based on project name or ID, dashboard name or ID. Fuzzy search based on a portion of project name, project ID, dashboard name or dashboard ID is supported. |
|Refresh a dashboard |Refresh a dashboard with the current settings to retrieve the latest query and analysis results.<br><br>On the upper\-right corner of the dashboard page, click the Refresh icon to refresh the dashboard and update the analysis results. |
|Share a dashboard |Share a dashboard with users who are granted the permissions on the dashboard.<br><br>On the upper\-right corner of the dashboard page, click the Share icon to copy the dashboard URL quickly. When the target users obtain the dashboard URL, they can log on and view the dashboard in a quick manner.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only the users who are granted the permissions on the dashboard can log on to BytePlus to view the dashboard through the shared link.</div><br> |
|View dashboard JSON |Each dashboard has a corresponding JSON script, which allows you to quickly copy a new dashboard. For specific operation, please refer [Import a dashboard](https://docs.byteplus.com/docs/tls/Import_dashboard).<br><br>You can click the **Settings** icon in the dashboard and view the dashboard's JSON script in the **JSON Model** tab or download it locally as a file. |


<span id="29306748"></span>
## Chart operations


|Action |Description |
|---|---|
|Add a chart |Click **Add chart** in the upper right corner of the dashboard to add various types of statistical charts. For detailed explanations, please refer to [Chart overview](https://docs.byteplus.com/docs/tls/chart_overview). |
|Modify the settings of a chart |Modify the settings of a chart on a dashboard.<br><br>Edit the topic, query statement, chart type and settings, time range, and name of the chart. |
|Copy a chart |Copy a chart to add an identical chart on a dashboard, then revise the copied chart. This enables you to quickly add multiple similar charts.<br><br>In the upper\-right corner of the chart that you want to copy, click the More icon to expand the collapsed list, then click **Copy** to copy the chart. The default name of the copied chart is  **{chartname}\-copy**. |
|Delete a chart |Delete a chart from a dashboard.<br><br>In the upper\-right corner of the chart that you want to delete, click the More icon to expand the collapsed list, then click **Delete**. |
|Save as an image |Expand the dropdown menu in the upper right corner of the specified chart and click **Save as image** to save the search analysis results displayed in the current chart as a PNG image. |
|Save a CSV table |Expand the dropdown menu in the upper right corner of the specified chart and click **Download as CSV** to save the search analysis results displayed in the current chart as a CSV table.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Currently, table, line chart, column chart, pie chart, single value chart, statistics chart, histogram, progress bar, timeline, treemap, and measurement chart are supported.</div><br> |
|Adjust the location and size of a chart |Adjust the location and size of a chart on the dashboard.<br><br>Drag the lower\-right corner of the chart to adjust the size of the chart or drag the chart to change its location on the dashboard. |
|Check whether the query analysis results of the current chart are accurate. |Check whether the query analysis results of the current chart are accurate. When the query analysis results of the chart are not accurate, a prompt message will be displayed in the upper right corner of the chart. |
|Add a group |Set up groups for statistical charts to achieve chart summarization and folding.<br><br>Click **Add group** in the upper right corner of the dashboard and set a group name to add a group. After setting up the group, you can drag the statistical chart into the target group. |
|creating an alarm police |The statistical charts that have been added to the dashboard can be directly used as monitoring tasks for alarm strategies, for quickly creating an alarm police.<br><br>Expand the dropdown menu in the upper right corner of the specified chart and click **Add alarm**, then complete the alarm configuration according to business needs. For detailed instructions, please refer to [Create alarm policies](https://docs.byteplus.com/docs/tls/create_alarm_policies).<br><br>In the alarm police, the execution statement part of the monitoring task area automatically filled in the monitoring object, search analysis statement, and time query range corresponding to the statistical chart. You can modify or use it directly as needed. |


<span id="0ae095f7"></span>
## Filter or variable operations


|Action |Description |
|---|---|
|Create a filter or variable |Torch Log Service supports linkage of charts in a dashboard through filters or variables. After you create a filter or variable, you can filter the chart data by specifying the field values of the fields. For more information, refer to [Add filters to a dashboard](https://docs.byteplus.com/docs/tls/Adding_filters_to_a_dashboard). |
|Modify a filter or variable |In the upper\-right corner of the dashboard, click **Settings**. On the **Filters and variables** Tab, locate the filter you want to modify, click **Edit** in the **Action** column, then modify the filter settings. |
|Delete a filter or variable |In the upper\-right corner of a dashboard, click **Settings**. On the **Filters and variables** Tab, locate the filter that you want to delete, then click **Delete** in the **Action** column. |
|Use a filter |After you add a filter to a dashboard, use the filter to filter data based on the specified key field.<br><br>On the top navigation menu of the dashboard page, find the filter that you want to use, then select the desired value from the drop\-down\-list. You can then view the statistics of logs containing the specified key:value pair. |


<span id="添加告警"></span>
## Set a query time range (global time)

Specify the time range for querying data for all charts on a dashboard.

On the upper\-right corner of the dashboard page, specify a time range. Select a relative time range or specify a custom time range, then click **OK**. The system queries data for all charts on the dashboard according to the specified time range.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you open the dashboard page again, the time range setting is automatically cleared.</div>


* <div data-tips="true" data-tips-type="tip">If you click the Refresh icon on the upper\-right corner to refresh the dashboard, the time range setting is retained.</div>
