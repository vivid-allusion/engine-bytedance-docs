---
title: "Add dashboard custom variables"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Adding_custom_variables_to_the_dashboard"
---

This section explains how to add dashboard custom variables with related examples.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Collected log data and configured indexes. For details, refer to [Quick Start](https://docs.byteplus.com/docs/tls/getting_started_collecte_logs).

* A dashboard has been created, and statistical charts have been added to it. For details, refer to [Create Dashboard](https://docs.byteplus.com/docs/tls/Creating_a_dashboard) and [Add Charts to Dashboard](https://docs.byteplus.com/docs/tls/Adding_charts_to_a_dashboard).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The total number of filters, variables, and charts in each dashboard must not exceed 50.</div>


<span id="48c64961"></span>
## Steps to add custom variables


1. Log in to the [Torch Log Service console](https://console.byteplus.com/tls/).

2. On the top navigation bar, select the region where the log service is located.

3. In the left navigation bar, select **Common Functions** \> **dashboard**.

4. In the dashboard list, click the dashboard under the target log project.

5. Click the **Settings** icon at the top right of the page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_23b0bb5ea2494df2ba42d93b2745ff7b.png) </span>

6. On the **Filters and Variables** tab, click **Add Custom Variable**.

7. In the **Create Custom Variable** panel, refer to [Parameter Description](https://docs.byteplus.com/docs/tls/Adding_filters_to_a_dashboard#625f537c), complete the configuration, then click **Create Variable**.

8. At the top right of the **Settings** page, click **Save**.


<span id="625f537c"></span>
## Custom Variable Parameter Description

The following table describes the parameters related to adding custom variables.


|Configuration |Description |
|---|---|
|Variable name |Variable name used for filtering.<br><br>The log service uses this variable as the key for filtering, affecting the charts on the dashboard where this variable is applied. |
|Variable alias (display name) |Alias of variable name. For example, set an alias `client IP` for the variable `clientIP` to improve the dashboard experience. |
|Static value |Set static values for variables. The log service adds these static values to the specified variable’s value list. Supports adding multiple static values, and the order of each static value can be freely adjusted by dragging. Each static value can have the following configurations:<br><br><br>* **Field value**: the variable value used for filtering, required. Supports setting to an asterisk (\*), which matches all variable values.<br><br>* **Field value alias**: alias of the variable value. No; For example, set the alias `zhangsan `for the variable value `zhangsan`.<br><br>* **Default selected**: whether this field is selected by default in the variable. The default is off, meaning not selected. When **multi\-select** is not enabled, only one value can have **default selected** enabled. |
|Dynamic value |Set dynamic values for variables. The log service uses the query and analysis results of the selected log topic as optional values for variables.<br><br>Dynamic values change over time and depend on factors such as the configured time range and query and analysis statements. |


<span id="6919ecf4"></span>
## Example of Adding Interval Variable

For example, chart A shows the number of requests per minute. When you need to check website visits for different time intervals (such as per second, per hour) using chart A, you can add a time interval variable without manually modifying the query and analysis statement.


1. Add a chart.

   Before adding a custom variable, add chart A to the dashboard first. For detailed steps, see [Add charts to the dashboard](https://docs.byteplus.com/docs/tls/Adding_charts_to_a_dashboard). The query and analysis statement corresponding to chart A is as follows:

   ```SQL
   * | SELECT DATE_FORMAT(__time__ - __time__ % 60000, 'HH:mm:ss') AS time, count(*) AS PV GROUP BY time ORDER BY time
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>__time__</code> is a millisecond\-level timestamp, so <code>DATE_FORMAT(__time__ - __time__ % 60000, 'HH:mm:ss')</code> aligns the time to the minute.   </div>
   

2. Modify the query and analysis statement of chart A by adding the variable placeholder `\${{interval|60000}}` in the statement.

   ```SQL
   * | SELECT DATE_FORMAT(__time__ - __time__ % \${{interval|60000}}, 'HH:mm:ss') AS time, count(*) AS PV GROUP BY time ORDER BY time
   ```
   

3. Add a variable.

   Important configuration example is as follows:

   * Set the **variable name** to **interval**.

   * Set the **field alias** to **time interval**.

   * Set the **field values** to **3600000**, **60000**, and **1000**, representing time intervals of one hour, one minute, and one second respectively.

4. Save the configuration.

   Click **Save** at the top right corner of the **Settings** page.

5. Use variables.

   After adding variables, the variable option box will appear on the dashboard, allowing you to filter chart data through it. For example, selecting **Time Interval** as **Hourly** will display the number of website visits per hour in Chart A.

&nbsp;


<span id="54f9d3ef"></span>
## Related actions

After adding filters and variables, you can conveniently use, modify, or delete them on the dashboard as needed. For details, refer to [common dashboard operations](https://docs.byteplus.com/docs/tls/Managing_dashboards).
