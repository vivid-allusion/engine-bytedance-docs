---
title: "Link configuration"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Link_configuration"
---

Custom dashboards support link configuration, including dashboard links, panel links, and data links. This enables quick redirection in different scenarios. This topic describes link configuration paths, URL configuration methods, and the supported link variable types and usage.

<span id="LMzEh1qJ"></span>
## Configuration paths


<Tabs>
<Tab zoneid="ytUaSkBLyr" title="Dashboard link">
<TabTitle>Dashboard link</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Up to 3 dashboard links can be added to each dashboard.</div>



1. Navigate to[ Custom Dashboard](https://console.byteplus.com/observe/dashboard/dashboard) and click the name of the target dashboard to enter the dashboard details page.

2. Click the **Edit** button in the upper right corner to enter edit mode.

3. Click the **Settings** button in the upper right corner and select the **link** tab.

4. Click **Create link** and configure dashboard link parameters as needed, including: link title, link address, Tooltip, and navigation method.

5. Save the configurations and exit edit mode. The configured dashboard link will be displayed in the upper right corner of the dashboard.


</Tab>
<Tab zoneid="rCSnTm4rnO" title="Panel link">
<TabTitle>Panel link</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Currently, all types of charts support panel links. Up to 3 panel links can be added per chart.</div>



1. Navigate to[ Custom Dashboard](https://console.byteplus.com/observe/dashboard/dashboard) and click the name of the target dashboard to enter the dashboard details page.

2. Click the **Edit** button in the upper right corner to enter edit mode.

3. In the upper right corner of the target chart, select `...` and **edit** in sequence to enter the chart edit page.

4. Select the chart type as needed, and add the panel link in the panel configuration section. Parameters include: URL title, URL, and navigation method.

5. Save the configuration and exit edit mode. The configured panel link will be displayed in the upper left corner of the chart.


</Tab>
<Tab zoneid="rNIAhNIanf" title="Data link">
<TabTitle>Data link</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Currently, you can add data links only for time series diagrams. Up to 3 data links can be added per chart.</div>



1. Navigate to [Custom Dashboard ](https://console.byteplus.com/observe/dashboard/dashboard)and click the name of the target dashboard to enter the dashboard details page.

2. Click the **Edit** button in the upper right corner to enter edit mode.

3. In the upper right corner of the target chart, select `...` and **edit** in sequence to enter the chart edit page.

4. Select the target time series chart, and in the data link configuration, click **Add URL**. Configure the relevant data link parameters as needed, including the URL title, URL, and navigation method.

5. Save the configurations and exit edit mode. The configured data link will be displayed below the currently selected data.


</Tab>
</Tabs>


<span id="KoWlBCJf"></span>
## URL configuration methods


|Configuration methods |Description |
|---|---|
|Full URL |Configure a complete URL.<br><br>```HTML```<br>```https://log.example.com/search?query=${instance}&from=${__from}&to=${__to}```<br><br><br> |
|Path only |Configure only the path part of the URL. The domain of the current page is automatically prepended during redirection.<br><br>```HTML```<br>```/logs/search?query=${instance}```<br><br><br> |
|Query only |Prefix: `?` Configure only the query part. The domain and path of the current page are automatically prepended during redirection.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If "Open new window" is not enabled, the redirection does not occur. This method can be used for scenarios such as switching global variables through links.</div><br><br><br>```HTML```<br>```?query=${instance}&from=${__from}&to=${__to}```<br><br><br> |


<span id="iuSubPns"></span>
## Variable types


|Variable type |Description |
|---|---|
|Global variables |* Usage: `${variable name}/${variable name:queryparam}`. `${variable name:queryparam}` is resolved to the format `var-variable name=variable value`.<br><br>* Examples: `https://example.com?${cluster:queryparam}`, `https://example.com?cluster=${cluster}`. |
|Built\-in variables |* `${__url_time_range}`: Retains the current time range.<br><br>* `${__from}`: Start of the current time range.<br><br>* `${__to}`: End of the current time range.<br><br>* `${__all_variables}`: Includes all current variables. |
|Data context variables |<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Data context variables are currently supported only in data links.</div><br><br><br><br>* `${__series.name}`: Series name.<br><br>* `${__field.name}`: Field name.<br><br>* `${__field.labels.<labelKey>}`: Field label value. This variable is available when a label exists and the VMP or APMPlus\-Server data source is used.<br><br>* `${__data.fields.<DisplayName>}`: Displays the value of another field in the same row. This variable can be used for chart types that display data by row, such as tables. |
