---
title: "Custom dashboard"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/custom_dashboard"
---

The custom dashboard allows you to flexibly configure metrics and chart types.

<span id="2aad4dd8"></span>
## Metric descriptions

The metric types and metrics that can be configured in the custom dashboard are as follows:


|Categories |Metric |
|---|---|
|PV/UV |PV, UV, and session count |
|JavaScript error |Error count, error rate, impacted user, impacted users rate. |
|blank screen |Blank screen count, number of users impacted by blank screens. |
|request |sample size, request success count, request success rate, cancelled request count, request error, request error impacting user count, request error rate, request error user impact rate, slow request count, request time, SDK Instrumentation Time, Redirect Time, Cache Time, DNS Resolution Time, TCP Connection Time, SSL Handshake Time, Request Send Time, Response Time. |
|Performance |Sample DomReady, Load, slow\-pageload count, First Paint (FP), First Contentful Paint (FCP), First Meaningful Paint (FMP), Largest Contentful Paint (LCP), Cumulative Layout Shift (CLS), Time to Interactive (TTI), Time to First Byte (TTFB), DOM Parsing, Processing, ResourceLoad, Redirect, DNS, TCP, SSL, Request, Response.<br><br>Performance metrics support customization. For details, refer to [performance metric](https://docs.byteplus.com/en/docs/apmplus/performance_metric). |
|static resources |Sample Size, Slow Load Count, Redirect Time, Cache Time, DNS Resolution Time, TCP Connection Time, SSL Handshake Time, Request Send Time, Response Time, and Static Resources Cache Hit Rate. |
|static resource error |Static resource error count, static resource error impacted user count, static resource error rate, static resource error impacted user rate. |
|custom log |Sample size, user count. |


<span id="1d5254fb"></span>
## Create a dashboard


1. Log in to [the Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client/console/overview).

2. In the target application, click **WebPro client monitoring**.

3. Select **All Features \> Custom Dashboard**.

4. On the **dashboard list** page, click **create dashboard**.

5. On the **create dashboard** page, enter the dashboard name, and then click **confirm**.

   Configuration description:

   **Dashboard name**: Custom dashboard name, used to identify the dashboard. Dashboard name can be up to 100 characters long.


<span id="25a63f67"></span>
## **Configuration charts**


1. On the dashboard page, click **Add container**.

   A container is used to group a set of charts together and aggregate them within the container.

2. Click the edit button to modify the container name.

3. On the dashboard page, click **Add component**.

4. On the **Create Chart** page, configure components, then click **Save**.

   The custom dashboard supports adding four types of components: trend chart, number card, table, and pie chart.

   * **Configuration trend charts**

      Configuration description:

      
      |**Parameter** ||**DescriptionS** |
      |---|---|---|
      |Select a chart type |Chart name |Customize the chart name to identify the chart. |
      ||Decimal places |Select the number of decimal places for numerical values displayed in the chart. Supports up to four decimal places for numeric values. |
      ||Y axis |Configure the maximum and minimum values of the Y axis. |
      ||Legend |It supports legend configuration, as well as configuration of the fields displayed in the legend, including minimum, maximum, average, and current. |
      ||Month\-on\-month |Supports configuration of the period\-over\-period value. When enabled, the period\-over\-period value is displayed as a dashed line. |
      |Draw charts |Metric |Supports selecting metrics to query and allows adding multiple metrics. For details, refer to [metric description](https://docs.byteplus.com/en/docs/apmplus/custom_dashboard#2aad4dd8). |
      ||Groups |Supports configuration of grouping dimensions for a metric, allows you to add multiple dimensions, and after selecting, the trend chart will be grouped and displayed according to the selected dimensions.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The device_id, user_id, session_id, view_id, action_id, and Query(URL) fields in all modules do not support grouping.</div><br> |
      ||Statistics |Some metrics use the COUNT and UNIQUE statistical types. Duration\-type metrics support configuring statistical value types such as AVG, PCT50, and more.<br><br>The statistical method and description are as follows:<br><br><br>* **COUNT**: Count based on time granularity<br><br>* **UNIQ**: After calculating the sum within the time granularity, deduplicate by DID<br><br>* **AVG**: SUM(metric values within the time granularity) / sample size<br><br>* **PCT50**: The value at the 50th percentile after sorting in ascending order<br><br>* **PCT75**: The value at the 75th percentile after sorting in ascending order<br><br>* **PCT90**: The value at the 90th percentile after sorting in ascending order<br><br>* **PCT99**: The data at the 99th percentile after sorting in ascending order |
      ||Context link |Support adding context link If you observe a spike in data on the dashboard, you can navigate to the corresponding feature page to view detailed data, which will help you locate and analyze issues.<br><br>For example, to customize a dashboard to monitor changes in the metric for JavaScript error count, you need to complete the following actions.<br><br><br>1. On the **add context link** page, the following configuration needs to be completed:<br><br>   * Link name: JavaScript overview.<br><br>   * URL: URL of the page for adding the **JavaScript overview** feature. When copying a URL, remove the query and include only the domain name and path.<br><br>   * URL parameter: Check **Application ID**, **Start time**, **End time**, and **Filter criteria**. After you check the box, the filter criteria for these four dimensions will be automatically filled as variables in the URL.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When the feature page has two tabs, it defaults to navigating to tab A. To navigate to tab B, you need to specify a parameter in the URL. For example:   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The request overview includes all requests and error requests. By default, the page navigates to all requests. If you want to navigate to error requests, add <code>activeTab=err</code> to the URL.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The resources overview includes all resources and error resources. By default, the page redirects to all resources. If you want to redirect to error resources, please add <code>activeTab=err</code> to the URL.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Data explore includes many dimensions. To jump to an error resource, please add <code>ev_type=resource_error</code> to the URL.   </div><br>   <br><br>2. After configuration is complete, click a time node on the line in the trend chart to display the context name **JavaScript overview**.<br><br>3. Click the context name **JavaScript overview** to navigate to the **JavaScript overview** feature page and view specific data.<br><br>   Since the custom dashboard aggregates data by day by default, the JavaScript overview displays data for 2023\-07\-24 00:00:00 to 2023\-07\-25 00:00:00.<br><br>   If you configure a **filter condition** or **grouping** for the metric, then when you navigate to the **JavaScript overview** page, it will display data based on the configured filter condition and grouping. If the JavaScript overview page does not support the filter criteria and grouping dimensions you configured, these settings will be ignored when you navigate to the page. |
      ||Name metrics |You can name legends. Legends are displayed as the custom name followed by the metric name. |
      ||Quick filter |If you need to link with the dashboard's quick filter criteria, you can select a pre\-configured quick filter. |
      ||Filter criteria |You can configure filter conditions for metrics. The filter methods include: **contains**, **does not contain**, **regular expression match**, and **regular expression does not match**.<br><br>Multiple filter conditions can be configured, and the relationship between these filter conditions can be set to **and** or **or**. |
      ||Add the four arithmetic operations |If you need to perform arithmetic operations on existing metrics, for example, to sum the error count for all exception types, you can use the arithmetic operation feature. |
      ||Add a tag |You can add markers to the trend chart, including marker lines or marker areas, and name them. Multiple markers can be added. |
      

   * **Configuration value cards**

      The numeric card ultimately displays a statistic.

      Configuration description:

      
      |**Parameter** ||**DescriptionS** |
      |---|---|---|
      |Select chart type |Chart names |A custom chart name is used to identify the chart. |
      ||Decimal places |Select the number of decimal places for values displayed in the chart. Supports numerical values with up to four decimal places. |
      ||Month\-on\-month |Supports configuration of the sequential comparison value. When enabled, the sequential comparison value is displayed at the bottom right of the numerical value.<br><br>Method: Sequential comparison = (current value − comparison value) / comparison value |
      |Draw charts |Metric |Support selecting the metrics to query. For details, refer to [metric description](https://docs.byteplus.com/en/docs/apmplus/custom_dashboard#2aad4dd8).<br><br>When multiple original metrics are added, only the last added metric is displayed. |
      ||Statistics |Some metric statistics types are COUNT and UNIX. Time\-consuming metric types support configuring statistical value types such as AVG, PCT50, and others.<br><br>Statistical methods and description are as follows:<br><br><br>* **COUNT**: Count based on time granularity<br><br>* **UNIQ**: After calculating the sum within each time granularity, deduplicate by DID<br><br>* **AVG**: SUM of metric values within the time granularity / sample size<br><br>* **PCT50**: The value at the 50th percentile after sorting in ascending order<br><br>* **PCT75**: The data at the 75th percentile after sorting in ascending order<br><br>* **PCT90**: The data at the 90th percentile after sorting in ascending order<br><br>* **PCT99**: The data at the 99th percentile after sorting in ascending order |
      ||Unit |Supports configuring the unit for the final displayed value. For example, the unit configuration for FPS is s (seconds). |
      ||Context link |Support adding context links. If you observe spikes in data on the dashboard, you can navigate to the corresponding feature page to view detailed data, which helps locate and analyze issues.<br><br>For example, if you need to customize a dashboard to monitor changes in the metric for JavaScript error count, you need to complete the following actions.<br><br><br>1. On the **add context link** page, you need to complete the following configuration:<br><br>   * Link name: Configured as JavaScript overview.<br><br>   * URL: URL for adding the **JavaScript overview** feature page. When copying a URL, remove the query string and include only the domain name and path.<br><br>   * URL parameter: Check **application ID**, **start time**, **end time**, and **filter condition**. After you check, the filter criteria for these four dimensions will be automatically populated into the URL as variables.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When the feature page has two tabs, the default behavior is to navigate to tab A. To navigate to tab B, you need to specify a parameter in the URL. For example:   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The request overview includes all requests and error requests. By default, the page navigates to all requests. If you want to navigate to error requests, add <code>activeTab=err</code> to the URL.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The resources overview includes both all resources and error resources. By default, the page redirects to all resources. To redirect to error resources, add <code>activeTab=err</code> to the URL.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Data exploration includes many dimensions. If you want to navigate to an error resource, please add <code>ev_type=resource_error</code> to the URL.   </div><br>   <br><br>2. After the configuration is complete, click the context name **JavaScript overview** in the upper right corner of the value.<br><br>3. Go to the **JavaScript overview** feature page to view specific data.<br><br>   Because the custom dashboard aggregates data by default over a seven\-day period, the JavaScript overview displays data from the most recent seven days. If you modify the aggregation time and time range before chart configuration, for example, aggregate by 30 minutes and view data from the last 6 hours, the JavaScript overview will display data from the last 6 hours.<br><br>   If you have configured the **filter condition** for the metric, then navigating to the **JavaScript overview** page will display data reflecting that filter condition. If the JavaScript overview page does not support the filter condition you configured, that filter condition will be ignored during navigation. |
      ||Statistics for the selected time period |The statistical methods and descriptions for time intervals are as follows:<br><br><br>* **TOTAL**: Calculate the global metric value for the selected time range without time granularity.<br><br>* **AVG**: SUM(metric value for each time granularity) / number of periods<br><br>* **MAX**: Maximum value within the selected time range<br><br>* **MIN**: Minimum value within the selected time range<br><br>* **SUM**: SUM(the metric value for each time granularity)<br><br>* **LAST**: The last metric value in the selected time period<br><br>* **NUMS**: Items with metric values |
      ||Quick filter |If you need to link with the dashboard's quick filter criteria, you can select a quick filter that has already been configured. |
      ||Filter criteria |Supports configuring filter conditions for metrics. Filter methods include: **contains**, **does not contain**, **regular expression match**, and **regular expression does not match**. |
      ||Add the four arithmetic operations |If arithmetic operations are added to a metric, the final metric calculated using these operations will be displayed. |
      

   * **Configuration table**

      Configuration description:

      
      |**Parameter** ||**DescriptionS** |
      |---|---|---|
      |Select a chart type |Chart names |A custom chart name used to identify the chart. |
      ||Decimal places |Select the number of decimal places for values displayed in the chart. Supports numeric values with up to four decimal places. |
      ||Sort |If there are multiple metrics, you need to select which metric to use for sorting and configure the table to display the top values according to the sorting method.<br><br><br>* The sorting method supports **ascending** and **descending**.<br><br>* Top values include Top**10**, **20**, **30**, **40**, **50**, and **100**. |
      ||Month\-on\-month |Supports configuring the period\-over\-period value. When enabled, the period\-over\-period value is displayed in parentheses to the right of the numeric value.<br><br>Calculation method: month\-on\-month = (current value \- comparison value) / comparison value |
      |Draw charts |Metric |Supports selecting metrics to query and allows adding multiple metrics. For details, refer to [metric description](https://docs.byteplus.com/en/docs/apmplus/custom_dashboard#2aad4dd8). |
      ||Statistics |Some metrics have the statistical type COUNT and UNIQUE. Metrics of the duration type support configuration of statistical value types such as AVG, PCT50, and more.<br><br>The statistical method and description are as follows:<br><br><br>* **COUNT**: Count based on time granularity<br><br>* **UNIQ**: Calculate the sum within each time granularity, then deduplicate by DID<br><br>* **AVG**: SUM(metric values within the time granularity) / sample size<br><br>* **PCT50**: The value at the 50th percentile after sorting in ascending order<br><br>* **PCT75**: The data at the 75th percentile after sorting in ascending order<br><br>* **PCT90**: The value at the 90th percentile after sorting in ascending order<br><br>* **PCT99**: The value at the 99th percentile after sorting in ascending order |
      ||Statistics for the selected time range |The methods and descriptions for time segment statistics are as follows:<br><br><br>* **TOTAL**: Calculate the global metric value for the selected time range after removing time granularity<br><br>* **AVG**: SUM(metric value for each time granularity) / number of periods<br><br>* **MAX**: Maximum value within the selected time range<br><br>* **MIN**: Minimum value within the selected time range<br><br>* **SUM**: SUM(the metric value for each time granularity)<br><br>* **LAST**: The last metric value within the selected time period<br><br>* **NUMS**: Items with metric values |
      ||Context links |Support adding context link. If you observe spiking data on the dashboard, you can navigate to the corresponding feature page to view detailed data, which helps you identify and analyze issues.<br><br>For example, if you need to customize a dashboard to monitor changes in the JavaScript error metric, you must complete the following actions.<br><br><br>1. On the **add context link** page, you need to complete the following configuration items:<br><br>   * Link name: Configured as JavaScript overview.<br><br>   * URL: URL of the page for adding the **JavaScript overview** feature. When copying a URL, the query string must be removed so that only the domain name and path are included.<br><br>   * URL parameter: Check **Application ID**, **Start time**, **End time**, and **Filter criteria**. After you select the checkbox, the filter conditions for these four dimensions will be automatically filled into the URL as variables.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When the feature page has two tabs, it defaults to navigating to tab A. To navigate to tab B, you need to specify a parameter in the URL. For example:   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The request overview includes all requests and error requests. By default, the page navigates to all requests. If you want to navigate to error requests, add <code>activeTab=err</code> to the URL.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The static resources overview includes all resources and error resources. By default, the page navigates to all resources. If you want to navigate to error resources, please add <code>activeTab=err</code> to the URL.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Data explore includes many dimensions. To navigate to an error resource, please add <code>ev_type=resource_error</code> to the URL.   </div><br>   <br><br>2. After the configuration is complete, click the value. The context name **JavaScript overview** will appear.<br><br>3. Go to the **JavaScript overview** feature page to view specific data.<br><br>   Because the custom dashboard aggregates data by default over a seven\-day period, the JavaScript overview displays data from the most recent seven days. If you modify the aggregation time and time range before chart configuration, for example, set aggregation to 30 minutes and view data from the most recent 6 hours, the JavaScript overview will display data from the most recent 6 hours.<br><br>   If you have configured **filter conditions** or **grouping** for the metric, then when you navigate to the **JavaScript overview** page, the data displayed will reflect the configured filter conditions and grouping. If the JavaScript overview page does not support the filter criteria and grouping dimensions in your configuration, these filter criteria and grouping dimensions will be ignored when you navigate to the page. |
      ||Column Name |Supports custom table column names, with column names automatically including the selected statistical value type. |
      ||Units |Supports configuration of units for table column data. For example, the unit configuration for FPS is set to s (seconds). |
      ||Quick filter |If you need to link with the dashboard's quick filter criteria, select a configured quick filter. |
      ||Filter criteria |You can configure filter conditions for metrics. The available filter methods are: **Contains**, **Does not contain**, **Regular expression match**, and **Does not match regular expression**. |
      ||Add the four arithmetic operations |Supports adding multiple metrics and performing arithmetic operations on multiple original metrics. |
      ||Groups |You can add groups to metrics. |
      

   * **Pie chart configuration**

      Configuration description:

      
      |**Parameter** ||**DescriptionS** |
      |---|---|---|
      |Select a chart type |Chart name |A custom chart name is used to identify the chart. |
      ||Decimal places |Select the number of decimal places for values displayed in the chart. Supports numeric values with up to four decimal places. |
      ||Period\-on\-period |Supports configuration of the month\-on\-month value. After enabling, the month\-on\-month value is displayed at the lower right corner of the number.<br><br>Calculation method: Month\-on\-month = (current value \- comparison value) / comparison value |
      |Draw charts |Metric |Only the display of a single metric is supported. When multiple metrics are added or arithmetic operations are applied to metrics, you can select which metric to display by checking **Display this metric**. For details, refer to [metric description](https://docs.byteplus.com/en/docs/apmplus/custom_dashboard#2aad4dd8). |
      ||Statistics |Some metrics use the COUNT and UNIQUE statistical types. Duration\-type metrics support configuring statistical value types such as AVG, PCT50, and more.<br><br>The statistical methods and description are as follows:<br><br><br>* **COUNT**: Counts based on time granularity<br><br>* **UNIQ**: After calculating the sum within each time granularity, deduplicate by DID<br><br>* **AVG**: SUM of metric values within the time granularity divided by the sample size<br><br>* **PCT50**: The value at the 50th percentile after sorting in ascending order<br><br>* PCT75: The data at the 75% position after sorting in ascending order<br><br>* **PCT90**: The value at the 90th percentile after sorting in ascending order<br><br>* **PCT99**: The data at the 99th percentile after sorting in ascending order |
      ||Statistics for the selected time period |The statistical methods and description for time segments are as follows:<br><br><br>* **TOTAL**: Remove time granularity and calculate the global metric value for the selected time range<br><br>* **AVG**: SUM(value of the metric at each time granularity) / number of periods<br><br>* **MAX**: Maximum value within the selected time range<br><br>* **MIN**: Minimum value within the selected time range<br><br>* **SUM**: SUM(the metric value for each time granularity)<br><br>* **LAST**: The last metric value in the selected time period<br><br>* **NUMS**: Items with metric values |
      ||Context links |Support adding context links. If you observe a spike in data on the dashboard, you can navigate to the corresponding feature page to view detailed data, which helps locate and analyze issues.<br><br>For example, you need to customize a dashboard to monitor changes in the JavaScript error count metric. You need to complete the following actions.<br><br><br>1. On the **add context link** page, you need to complete the following configuration:<br><br>   * Link name: JavaScript overview.<br><br>   * URL: URL of the page for adding the **JavaScript overview** feature. When copying a URL, remove the query and include only the domain name and path.<br><br>   * URL parameters: Check **Application ID**, **Start time**, **End time**, and **Filter condition**. After checking the boxes for these four dimensions, the filter criteria will be automatically filled into the URL as variables.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When the feature page has two tabs, it navigates to tab A by default. To navigate to tab B, you need to specify a parameter in the URL. For example:   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The request overview includes both all requests and error requests. By default, the page displays all requests. If you want to switch to error requests, add <code>activeTab=err</code> to the URL.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The resources overview includes all resources and error resources. By default, the page displays all resources. If you want to navigate to error resources, add <code>activeTab=err</code> to the URL.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Data explore has many dimensions. To navigate to an error resource, please add <code>ev_type=resource_error</code> to the URL.   </div><br>   <br><br>2. After the configuration is complete, click one of the segments in the pie chart, and the context name **JavaScript overview** appears.<br><br>3. Click the context name **JavaScript overview** to go to the **JavaScript overview** feature page and view specific data.<br><br>   Because the custom dashboard aggregates data over a seven\-day period by default, the JavaScript overview displays data from the most recent seven days. If you modify the aggregation time and time range before configuring the chart, for example, set aggregation to 30 minutes and view data from the past 6 hours, the JavaScript overview will display data from the past 6 hours.<br><br>   If you have configured the **filter condition** or **grouping** for the metric, then when you navigate to the **JavaScript overview** page, it will display data based on the configured filter condition and grouping. If the JavaScript overview page does not support the filter criteria and grouping dimensions that you have configured, these filter criteria and grouping dimensions will be ignored when you navigate to the page. |
      ||Name metrics |You can name the legend by combining dimension variables from the group configuration with fixed text. For example: the performance of $tag_aid. |
      ||Quick filter |If you need to link with the dashboard's quick filter criteria, you can select a pre\-configured quick filter. |
      ||Filter criteria |You can configure filter conditions for metrics. The available filter methods are: **Contains**, **Does not contain**, **Regular expression match**, and **Regular expression does not match**. |
      ||Add four arithmetic operations |Supports adding multiple metrics and performing the four basic arithmetic operations (addition, subtraction, multiplication, and division) on multiple original metrics. |
      ||Groups |Supports grouping metrics for display. After a group is added, the top 20 grouped metrics are shown, and the remaining metrics are categorized as Other. |
      


<span id="bcbd0e45"></span>
## View the predefined Real\-time Statistic dashboard

The platform includes a real\-time dashboard feature based on the analytical capabilities of the custom dashboard.


1. Log in to the [Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client/console/overview).

2. In the target application, click **webpro client Monitoring**.

3. Select **All Features \> Custom Dashboard**.

4. On the **dashboard category** page, click **Predefined**.

5. A **Real\-time Statistic** dashboard is preset in the dashboard list. Click the dashboard name to view the platform\-recommended observation metrics and corresponding configuration.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the Real\-time Statistic dashboard, the default aggregation granularity is 5 minutes and the time range is the most recent hour. The 30\-second auto\-refresh feature is turned on.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">It is not recommended to change the time aggregation granularity and the time range. If you temporarily adjust the aggregation granularity and time range, this configuration will not be saved when you re\-enter the dashboard.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The Real\-time Statistic dashboard integrates all analytical capabilities from the custom dashboard, including period\-over\-period analysis and configuration of context link.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The Real\-time Statistic dashboard does not support editing. If you have special dashboard requirements, you can copy the Real\-time Statistic dashboard to use it as a real\-time dashboard template, and then edit the custom dashboard generated after copying.   </div>
   


<span id="9ad3b292"></span>
## Add a quick filter

The quick filter can filter metrics within the dashboard according to dimensions configured in advance. Each dashboard can configure its own quick filter.


1. On the dashboard page, click **Manage quick filters**.

2. In the **Common filter settings** dialog box, click **add common filter**.

3. In the **Set Common Filter** dialog box, complete the following configuration and then click **Finish**.

   Configuration descriptions

   
   |**Parameter** |**DescriptionS** |
   |---|---|
   |Name |Custom filter name, used to identify the current filter. |
   |Subnamespace |Configure filter dimensions |
   |Include |Select the values that are **included** in the dimension, or configure the dimension to **exclude** them. |
   |default value |The values that are included or excluded from the dimension. The default value is empty, which means no filter is applied by default. |
   


<span id="1b10d874"></span>
## Configure quick filter

A quick filter will only take effect on the chart if it is set for the metric in the chart configuration.


1. On the dashboard page, click  **···**  in the upper right corner of the target chart, then click **edit**.

2. In the **charting** area, click **Expand** to the right of the target metric.

3. In the metric expansion configuration, check the quick filter option, then click **Save**.


<span id="36ec01b3"></span>
## Public dimension filter configuration


* You can directly select public dimension filter criteria in the toolbar. The filter criteria you set will apply to all charts on the dashboard.

* The filter conditions for public dimensions and those configured in each metric are combined as follows: for dimensions that are the same, their intersection is used; for dimensions that are different, their union is used.

   * Take the intersection when dimensions are the same

      For example, if the filter condition for the public dimension is device model: iPhone 5, iPhone 6, and the filter condition for the chart is device model: iPhone 6, iPhone 7, then the final filter condition applied will be device model: iPhone 6.

   * Take the union across different dimensions

      For example, if the filter condition for the public dimension is device model: iPhone 5, iPhone 6, and the filter condition for the chart is APP version number 1.1.0, then the final filter condition applied will be device model: iPhone 5, iPhone 6, and APP version number 1.1.0.

* The filter criteria for public dimensions support regular expression filtering.


<span id="43fd6cbf"></span>
## Management views

A view is simply a collection of quick filters and does not affect the charts within the dashboard. When there are many filter conditions and multiple users are collaborating on a dashboard, you can use the view feature to save your commonly used filter conditions.

For example, in a business scenario, Person A views information for Dimension A in dashboard M, while Person B views information for Dimension A and Dimension B in dashboard M. Person A needs to perform the following actions to create a view.


1. On the dashboard page, add a quick filter in the default view.

   For details, refer to [Add quick filter](https://docs.byteplus.com/en/docs/apmplus/custom_dashboard#9ad3b292). For example, name it Common Filter A.

2. On the dashboard page, configure quick filters for the target metrics in the target chart.

   For details, refer to [Configure quick filter](https://docs.byteplus.com/en/docs/apmplus/custom_dashboard#1b10d874).

3. On the dashboard page, click **Save view as**.

4. In the **Save View As** dialog box, enter a name for the view, for example, name it View A, and then click **Save**.

5. On the dashboard page, switch the default view to View A.

6. In the dashboard, User A can access View A, which displays the commonly used Filter A. Person A can switch filter values to view changes in the chart.


At this time, Person A can view information about Dimension A in dashboard M. If user B wants to view information about dimension A and dimension B in dashboard M, user B needs to perform the following actions to create a view.


1. Add a quick filter in the default view of the dashboard page.

   For details, refer to [Add quick filter](https://docs.byteplus.com/en/docs/apmplus/custom_dashboard#9ad3b292). For example, name it Common Filter B.

2. On the dashboard page, configure a quick filter for target metrics in the target chart.

   For details, refer to [Configure quick filter](https://docs.byteplus.com/en/docs/apmplus/custom_dashboard#1b10d874).

3. On the dashboard page, click **Save view as**.

4. In the **Save View As** dialog box, enter a name for the view, for example, name it View B, and then click **Save**.

5. On the dashboard page, switch the default view to View B.

6. In the dashboard, User B can view View B, which displays common filter A and common filter B. Person B can switch filter values to view changes in the chart.


<span id="af4d980f"></span>
## Subscribe to dashboards

Subscribing to a dashboard allows you to receive dashboard updates at scheduled intervals via your chosen subscription method.


1. On the dashboard page, click **Subscribe to dashboard**.

2. In the **Create schedule report** dialog, complete configuration, then click **Confirm**.

   Configuration descriptions

   
   |**Parameter** |**DescriptionS** |
   |---|---|
   |Subscription name |By default, it is set to the dashboard name and can be customized. |
   |Subscription period |Configure the time to receive subscription notifications. Supports configuration for a specific time on a daily, weekly, or monthly basis. |
   |Query interval |Supports customizing the query period, that is, the time range for dashboard data. |
   |Subscription methods |Supports selecting different subscription methods and allows multiple selections. Supports configuration as **Email**, **WeCom**, **Lark**, and **DingTalk**.<br><br>For details on webhook configuration, see [How do I configure a webhook?](https://docs.byteplus.com/en/docs/apmplus/How_to_configure_a_webhook). |
   |Receiving groups |Configure the object to receive schedule report subscription information. |
   |Subscription switch |Configure subscription switches.<br><br><br>* Open: Receive dashboard information.<br><br>* Turn off: Do not receive dashboard information. |
