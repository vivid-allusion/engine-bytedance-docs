---
title: "Add dashboard filters"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Adding_a_Dashboard_Filter"
---

This chapter explains how to add dashboard filters with related examples.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Log data has been collected and indexes have been configured. For details, refer to [Getting Started](https://docs.byteplus.com/docs/tls/getting_started_collecte_logs).

* The dashboard has been created, and statistical charts have been added to the dashboard. For details, refer to [Creating Dashboards](https://docs.byteplus.com/docs/tls/Creating_a_dashboard) and [Adding Charts to Dashboards](https://docs.byteplus.com/docs/tls/Adding_charts_to_a_dashboard).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The total number of filters, variables, and charts in each dashboard must not exceed 50.</div>


<span id="4ec640db"></span>
## Steps to add filters


1. Log in to the [Torch Log Service console](https://console.byteplus.com/tls/).

2. On the top navigation bar, select the region where the log service is located.

3. On the left navigation bar, select **Common Features** \> **Dashboard**.

4. In the dashboard list, click the dashboard under the target project.

5. Click the settings icon at the top of the page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_23b0bb5ea2494df2ba42d93b2745ff7b.png) </span>

6. On the **Filters and Variables** tab, click **Add Filter**.

7. In the **New Filter** panel, refer to [Parameter Description](https://docs.byteplus.com/en/docs/tls/Adding_filters_to_a_dashboard#31756bd2), complete the configuration, then click **New Filter**.


<span id="31756bd2"></span>
## Filter Parameter Description

The table below describes the parameters related to adding filters.


|Parameter |Description |
|---|---|
|filter name |Filter name. Filter names cannot be modified after creation.<br><br>This name is only for filter management and appears on the filter list page, not on the dashboard. |
|Filter alias (display name) |Alias for filters displayed in the dashboard.<br><br>For example, set an alias `Client IP` for the field `clientIP` to improve the dashboard experience. |
|Field name |The field used for filtering.<br><br>The log service uses this field as the filter key to filter the entire dashboard.<br><br>You can configure this field's value using **static values** or **dynamic values**. |
|filter method |filter method. supports the following methods.<br><br><br>* AND: returns the intersection of multiple search results by adding specified filter conditions to the chart’s query and analysis statements. the effective query and analysis statement is `[Value] AND [search query] \| [sql query]`.<br><br>* NOT: excludes the search results that match the chart’s specified query and analysis statement. the effective query and analysis statement is `[Value] NOT [search query] \| [sql query]`.<br><br><br>Value is the field value you configure in the **static value** or **dynamic value** parameter. |
|Supports multiple selection |Whether Value supports multiple selections when using filters.<br><br>It is off by default, meaning multiple selections are not supported. When enabled, you can select multiple values as filter criteria. When multiple selections are made, the filter criteria are connected by an OR relationship. The value is the field value you configure in the **static value** or **dynamic value** parameters. |
|Static value |Set static values (values) for filter fields.<br><br>The log service adds the static value to the list of values for the specified field. Supports adding multiple static values, and their order can be freely adjusted by dragging. Each static value can have the following configurations:<br><br><br>* **Field value**: the value used for filtering. Supports setting to an asterisk (\*), which matches all field values.<br><br>* **Field value alias**: the alias of the field value displayed in the filter. No. For example, set the alias `Zhang San` for the field value `zhangsan`.<br><br>* **Default selected**: whether the filter defaults to this field value selected. Off by default, meaning not selected. When **multi\-select support** is off, only one value can be set as **default selected**. |
|Dynamic value |Set dynamic values for filter fields.<br><br>The log service offers query and analysis results of the selected log topic as options for field values. Dynamic values change dynamically; their actual values depend on factors like the set time range and the query and analysis statement. |


<span id="babb1bff"></span>
## Example of adding a request method filter

For example, Chart A shows the number of requests per minute. To view the number of requests for each request method through Chart A, add a request method filter without manually modifying the query and analysis statement.


1. Add a statistical chart.

   Before creating a filter, add chart A to the dashboard first. For details, refer to [adding charts to the dashboard](https://docs.byteplus.com/docs/tls/Adding_charts_to_a_dashboard). The query and analysis statement corresponding to statistical chart A is as follows:

   ```SQL
   * | SELECT DATE_FORMAT(__time__ - __time__ % 60000, 'HH:mm:ss') AS time, count(*) AS PV GROUP BY time ORDER BY time
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>__time__</code> is a millisecond\-level timestamp, so <code>DATE_FORMAT(__time__ - __time__ % 60000, 'HH:mm:ss')</code> means aligning the time to the minute.   </div>
   

2. Add a filter.

   Key parameter description:

   * Set **name** to **method**.

   * Set **filter alias** to **request method**.

   * Set **field name** to **Method**.

   * Select **dynamic value** to extract the `Method` field value from logs through the query and analysis statement. The corresponding query and analysis statement is `*| SELECT DISTINCT Method`.

3. Save configuration.

   Click **Save** in the upper right corner of the **Settings** page.

4. Use filters.

   After adding filters, filters will be displayed on the dashboard. You can use them to filter chart data. For example, select **Request Method** as **POST**. Chart A will display the number of requests per minute for the POST method.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cc1143f19defde6d34a6f1638930f4fc.png) </span>


<span id="54f9d3ef"></span>
## Related actions

After adding filters and variables, you can conveniently use, modify, or delete them on the dashboard. For details, see [common dashboard operations](https://docs.byteplus.com/docs/tls/Managing_dashboards).
