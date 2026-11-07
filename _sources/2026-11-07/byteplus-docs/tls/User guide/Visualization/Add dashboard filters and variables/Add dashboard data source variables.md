---
title: "Add dashboard data source variables"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Add_dashboard_data_source_variables"
---

This section explains how to add dashboard data source variables with related examples.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Log data has been collected and the index is configured. For details, see [Getting Started](https://docs.byteplus.com/docs/tls/getting_started_collecte_logs).

* The dashboard has been created, and statistical charts have been added to it. For details, see [Create dashboard](https://docs.byteplus.com/docs/tls/Creating_a_dashboard) and [Add charts to dashboard](https://docs.byteplus.com/docs/tls/Adding_charts_to_a_dashboard).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The total number of filters, variables, and charts in each dashboard must not exceed 50.</div>


<span id="60aebfcd"></span>
## Steps to add data source variables


1. Log in to the [Torch Log Service console](https://console.byteplus.com/tls/).

2. On the top navigation bar, select the region where the log service is located.

3. In the left navigation bar, select **Common Functions** \> **dashboard**.

4. In the dashboard list, click the dashboard under the target log project.

5. Click the **Settings** icon at the top right corner of the page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_23b0bb5ea2494df2ba42d93b2745ff7b.png) </span>

6. On the **Filters and Variables** tab, click **Add Data Source Variable**.

7. In the **New Data Source Variable** panel, refer to the [Parameter Description](https://docs.byteplus.com/docs/tls/Adding_filters_to_a_dashboard#33021d1f), complete the related configuration, and then click **New Data Source Variable**.

8. At the top right corner of the **Settings** page, click **Save**.


<span id="33021d1f"></span>
## Parameter Description of Data Source Variables

The following table describes the relevant parameters for adding data source variables.


|Configuration |Description |
|---|---|
|Data source variable name |Data source variable name.<br><br>The log service uses this variable as the key for filtering and it takes effect on charts in the dashboard that have this variable set. |
|Alias (display name) |Alias of the variable name. For example, set an alias `Client IP` for the variable `clientIP` to improve the dashboard experience. |
|Option source |Specifies the scope of the data source, supporting selection of all log topics or custom log topics.<br><br><br>* All log topics: include all log topics in the current dashboard's project.<br><br>* Custom log topics: support selecting the log topics you need within the current dashboard's project.<br><br>   Support matching target log topics through regular expressions. |
|Default log topic |Specify the default log topic to use. |


<span id="2b464df0"></span>
## Example of Adding a Multi\-topic Request Quantity Variable

For example, project A contains multiple log topics that store access logs for websites A, B, C, and others separately. When you want to display the number of requests per minute for each log topic in a statistical chart, you can add a data source variable.


1. Add a data source variable.

   Important configuration examples are as follows:

   * Set **the data source variable name** to **website**.

   * Set **the alias (display name) to website access logs**.

   * Set **the option source** to **all log topics**.

2. Save the configuration.

   In the upper right corner of the **Settings** page, click **Save**.

3. Add a statistical chart.

   Add statistical chart A to the dashboard. For detailed steps, see [Add charts to the dashboard](https://docs.byteplus.com/docs/tls/Adding_charts_to_a_dashboard). Set the **data source** as **data source variable**, **website visit log (${{website}})** . The corresponding query and analysis statement is as follows:

   ```SQL
   * | SELECT DATE_FORMAT(__time__ - __time__ % 60000, 'HH:mm:ss') AS time, count(*) AS PV GROUP BY time ORDER BY time
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>__time__</code> is a millisecond\-level timestamp, so <code>DATE_FORMAT(__time__ - __time__ % 60000, 'HH:mm:ss')</code> means aligning the time to the minute.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After selecting the data source variable, the system defaults to executing query and analysis based on the log topic specified when you added the variable and generates results.   </div>
   

&nbsp;

4. Use data source variables.

   After adding variables, a variable option box will appear on the dashboard. You can switch data sources (log topics) via this box. For example, when you select different log topics in the **website visit log** variable, the system automatically updates the query and analysis results based on your selection.


<span id="4bc9f8ab"></span>
## Related actions

After adding filters and variables, you can conveniently use them on the dashboard. You can also modify or delete filters and variables as needed. For details, refer to [Common dashboard operations](https://docs.byteplus.com/docs/tls/Managing_dashboards).
