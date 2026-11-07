---
title: "Custom dashboard"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/custom_dashboard_app"
---

The custom dashboard allows you to flexibly configure metrics and chart types.

<span id="3fde5e85"></span>
## Metric description

The metric types and metrics that can be configured in the custom dashboard are as follows:


|Categories |DescriptionS |
|---|---|
|PV/UV |PV、UV。 |
|iOS crash |error count, error rate, impacted user count, and affected user rate. |
|iOS hang |error count, error rate, impacted user count, affected user rate. |
|OOM_iOS |error count, error rate, impacted user count, affected user rate. |
|iOS extension crash |error count, error rate, impacted user count, affected user rate. |
|Android Java Crash |Error count, error rate, impacted user count, and affected user rate. |
|Android launch crash |error count, error rate, impacted user count, affected user rate. |
|Android Native Crash |Error count, error rate, impacted user count, affected user rate. |
|Android ANR Crash |error count, error rate, impacted user count, affected user rate. |
|iOS Crash Protection |error count, error rate, impacted user count, and affected user rate. |
|custom error |error count, error rate, impacted user count, and affected user rate. |
|lag |error count, error rate, impacted user count, affected user rate. |
|startup analytic |cold\-start count, cold start time, normal cold start count, slow cold start count, slow cold start rate, warm start count, warm start time, normal warm start count, slow warm start count, slow warm start rate, pre\-initialization time, application build time, page load time. |
|page experience |Sample size, failure rate, availability rate, crash rate, smooth rate, FPS, FPS Fast Rate, FPS Normal Rate, FPS Bad Rate, FPS Bad Growth Rate. |
|Memory_Android |OOM count, OOM impacted user count, Physical Memory (Background), Java Memory Usage (Foreground), Virtual Memory (Foreground), Java Memory Usage Rate (Background), Java Memory Usage (Background), Virtual Memory (Background), Java Physical Memory Usage (Background), Java Physical Memory Usage (Foreground), Physical Memory (Foreground), Graphics Memory (Background), Native Physical Memory Usage (Foreground), Graphics Memory (Foreground), Java Memory Usage Rate (Foreground), Native Physical Memory Usage (Background). |
|Memory_iOS |OOM count, impacted user, App Memory Usage Ratio, App Memory Usage Size. |
|Network |Request volume, Response time, Throughput rate, Total time, Transmission data volume, Number of normal requests, Number of slow requests, Number of HTTP error requests, Transport layer error request count. |
|page request |Request count, error count, error rate, impacted user count, impacted users rate, success count, success rate, average time, slow query count, slow query rate, slow query impacted user count, slow query impacted users rate. |
|page error |error count, error rate, impacted user count, and affected user rate. |
|pageload performance |Sample size, First Paint, First Contentful Paint, First Meaningful Paint, First Input Delay, Maximum Interaction Latency, Time to Interactive, DOM Parsing Time, Resource Load Time, Time to First Byte, DOM Ready Time, Complete Load Time, TCP Connection Time, Network Request Time to First Byte, DNS Query Time, Network Transmission Time, First Load Bounce Rate, Slow Launch Ratio, and Slow Load Count. |
|User Metrics_Android |User session duration, background duration |
|MetricKit |Error count, user count. |
|application exit |Error count, error rate, impacted user count, impacted users rate. |
|PV/UV (New H5 Monitoring) |PV, UV, and session count. |
|JS Error (New H5 Monitoring) |Error count, error rate, impacted user count, impacted users rate. |
|Request (New H5 Monitoring) |Sample size, request success count, request success rate, cancelled request count, request error count, request error impacted user count, request error rate, request error user impact rate, slow request count, request time, SDK Instrumentation Time, Redirect Time, Cache Time, DNS Resolution Time, TCP Connection Time, SSL Handshake Time, Request Send Time, Response Time. |
|Performance (New H5 Monitoring) |Sample size, DOM Ready, Load, Slow page load count, First Paint (FP), First Contentful Paint (FCP), First Meaningful Paint (FMP), Largest Contentful Paint (LCP), Cumulative Layout Shift (CLS), Time to Interactive (TTI), Time to First Byte (TTFB), DOM Parsing, Processing, ResourceLoad, Redirect, DNS, TCP, SSL, Request, Response. |
|HarmonyOS JS Crash |error count, error rate, impacted user count, impacted users rate. |
|HarmonyOS App Freeze |error count, error rate, impacted user count, impacted users rate. |
|HarmonyOS Native Crash |error count, error rate, impacted user count, impacted users rate. |
|user count |New user count. |


<span id="66d5bf1c"></span>
## Create a dashboard


1. Log in to the [Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client/console/overview).

2. In the target application, click **App Monitoring**.

3. Select**All features \> Custom dashboard**.

4. On the **dashboard list** page, click **create dashboard**.

5. On the **create dashboard** page, enter the dashboard name, then click **confirm**.

   Parameter description:

   
   |Parameter |DescriptionS |
   |---|---|
   |Dashboard name |The custom dashboard name is used to identify the dashboard.<br><br>Dashboard name length must not exceed 100 characters. |
   


<span id="68352f3a"></span>
## **Configuration charts**


1. On the dashboard page, click **Add container**.

   A container is used to group a set of charts together and aggregate them within the container.

2. Click the Edit button to modify the container name.

3. On the dashboard page, click **Add component**.

4. On the **Create Chart** page, configure components, and then click **Save**.

   The custom dashboard supports adding four types of components: trend chart, number card, table, and pie chart.

   * **Configuration trend charts**

      Parameter description:

      
      |**Parameter** ||**DescriptionS** |
      |---|---|---|
      |Select a chart type |Chart name |Custom chart name used to identify the chart. |
      ||Decimal places |Select the number of decimal places for values displayed in the chart. Supports up to four decimal places for numeric values. |
      ||The Y axis |Configure the maximum and minimum values of the Y\-axis. |
      ||Legend |Supports configuring the legend, as well as the fields displayed in the legend, including minimum, maximum, average, and current. |
      ||Period\-over\-period |Supports configuration of the month\-over\-month value. When enabled, the month\-over\-month value is displayed as a dashed line. |
      |Draw charts |Metric |Supports selecting metrics to query and allows adding multiple metrics. For specific details, refer to [metric description](https://docs.byteplus.com/en/docs/apmplus/custom_dashboard_app#3fde5e85). |
      ||Groups |Supports configuring grouping dimensions for metrics, allowing you to add multiple dimensions. After you select the desired dimensions, the trend chart will be grouped and displayed according to your selection. |
      ||Statistics |Some metrics have a statistical type of COUNT and UNIQUE. Duration\-type metrics support configuring the statistical value type, such as AVG, PCT50, and more.<br><br>Statistical method and description:<br><br><br>* COUNT: Count based on time granularity<br><br>* UNIQ: Deduplicate by DID after calculating the sum within each time granularity<br><br>* AVG: SUM of metric values within the time granularity / sample size<br><br>* PCT1: The data at the 1st percentile after sorting in ascending order<br><br>* PCT5: The value at the 5th percentile after sorting in ascending order<br><br>* PCT25: The 25th percentile value after sorting the data in ascending order<br><br>* PCT50: The data at the 50th percentile after sorting in ascending order<br><br>* PCT75: The data at the 75th percentile after sorting in ascending order<br><br>* PCT90: The value at the 90th percentile after sorting in ascending order<br><br>* PCT99: The value at the 99th percentile after sorting in ascending order |
      ||Name metrics |Supports assigning names to legends. The display rule is to display the custom name followed by the metric name. |
      ||Quick filter |If you need to link with the dashboard's quick filter criteria, you can select a pre\-configured quick filter. |
      ||Filter criteria |Supports configuring filter conditions for metrics. The filter methods include: include, exclude, regular expression match, and regular expression does not match. |
      ||Add the four arithmetic operations |If you need to perform arithmetic operations on existing metrics, for example, to sum the error count for all exception types, you can use the arithmetic operations feature. |
      ||Add a tag |You can add markers to the trend chart, including marker lines or marked areas, and name them. Multiple markers can be added. |
      

   * **Configuration numeric cards**

      The final result of the display of a numeric card is a statistic. Parameter description:

      
      |**Parameter** ||**DescriptionS** |
      |---|---|---|
      |Select a chart type |Chart name |A custom chart name is used to identify the chart. |
      ||Decimal places |Select the number of decimal places for chart values. Supports up to four decimal places for numerical values. |
      ||Period\-on\-period |You can configure the period\-over\-period value. When enabled, the period\-over\-period value is displayed at the lower right corner of the numeric value.<br><br>Calculation method: Period\-over\-period change = (current value – comparison value) / comparison value |
      |Draw charts |Metric |Support selecting metrics to query. For details, refer to [metric description](https://docs.byteplus.com/en/docs/apmplus/custom_dashboard_app#3fde5e85).<br><br>When multiple original metrics are added, only the last added metric is displayed. |
      ||Statistics |Some metrics have the COUNT and UNIQUE statistical types. Duration\-type metrics support configuring the statistical value type to AVG, PCT50, and so on.<br><br><br>* COUNT: Counts based on time granularity<br><br>* UNIQ: Calculate the sum within the time granularity, then deduplicate by DID<br><br>* AVG: SUM(metric values within the time granularity) / sample size<br><br>* PCT1: The data at the 1st percentile after sorting in ascending order<br><br>* PCT5: The data at the 5th percentile position after sorting in ascending order<br><br>* PCT25: Data at the 25th percentile after sorting in ascending order<br><br>* PCT50: The median value after sorting in ascending order<br><br>* PCT75: The value at the 75th percentile after sorting in ascending order<br><br>* PCT90: The value at the 90th percentile after sorting the data in ascending order<br><br>* PCT99: The data value at the 99th percentile after sorting in ascending order |
      ||Units |Supports configuration of the unit for the final displayed value. For example, the unit configuration for FPS is set to s (seconds). |
      ||Statistics for the selected time period |* Total: Aggregate across the entire time range and calculate the global metric value for the selected period<br><br>* AVG: SUM(the metric value at each time granularity) / number of periods<br><br>* MAX: Maximum value within the selected time range<br><br>* MIN: Minimum value within the selected time range<br><br>* SUM: SUM(the metric values for each time granularity)<br><br>* LAST: The last metric value in the selected time period<br><br>* NUMS: Items with metric values |
      ||Quick filter |If you need to link with the dashboard's quick filter criteria, you can select a pre\-configured quick filter. |
      ||Filter criteria |You can configure filter conditions for metrics. The available filter methods are: contains, does not contain, regular expression match, and regular expression does not match. |
      ||Add basic arithmetic operations |If you add the four arithmetic operations to the metric, the final metric calculated using these operations is displayed. |
      

   * **Configuration tables**

      Parameter description:

      
      |**Parameter** ||**DescriptionS** |
      |---|---|---|
      |Select a chart type |Chart name |A custom chart name used to identify the chart. |
      ||Decimal places |Select the number of decimal places for chart values. Supports up to four decimal places for values. |
      ||Sort |If there are multiple metrics, you need to select which metric to sort by and configure the table to display the Top values according to the sorting method. Please refer to [metric description](https://docs.byteplus.com/en/docs/apmplus/custom_dashboard_app#3fde5e85) for details.<br><br><br>* The sorting method supports ascending and descending order.<br><br>* Top values include Top10, Top20, Top30, Top40, Top50, and Top100. |
      ||Period\-on\-period |You can configure the comparative value. When enabled, the comparative value is displayed in parentheses to the right of the numeric value.<br><br>Calculation method: Month\-on\-month = (current value \- comparison value) / comparison value |
      |Draw charts |Metric |Supports selecting metrics to query and allows adding multiple metrics. |
      ||Statistics |Some metrics have statistical types of COUNT and UNIX. Time consumption metrics support configuring the statistical value type, such as AVG, PCT50, and more.<br><br>Statistical methods and description:<br><br><br>* Count according to time granularity<br><br>* UNIQ: Calculate the total sum within the time granularity, then deduplicate by DID<br><br>* AVG: SUM of metric values within the time granularity / sample size<br><br>* PCT1: The data at the 1% position after sorting in ascending order<br><br>* PCT5: The value at the 5th percentile after sorting in ascending order<br><br>* PCT25: The value at the 25th percentile after sorting in ascending order<br><br>* PCT50: The value at the 50th percentile after sorting in ascending order<br><br>* PCT75: The value at the 75th percentile after sorting in ascending order<br><br>* PCT90: The value at the 90th percentile after sorting in ascending order<br><br>* PCT99: The data at the 99% position after sorting in ascending order |
      ||Statistics for the selected time period |* TOTAL: Remove time granularity and calculate the global metric value for the selected time range<br><br>* AVG: SUM(metric value for each time granularity) / number of periods<br><br>* MAX: Maximum value within the selected time range<br><br>* MIN: Minimum value within the selected time range<br><br>* SUM: SUM(the metric values for each time granularity)<br><br>* LAST: The last metric value within the selected time period<br><br>* NUMS: Items with metric values |
      ||Column Name |Supports custom table column names, with column names automatically including the type of statistical value selected. |
      ||Unit |Supports configuration of units for table column data. For example, the unit configuration for FPS is s (seconds). |
      ||Quick filter |If you need to link with the dashboard's quick filter criteria, you can select a pre\-configured quick filter. |
      ||Filter criteria |Supports configuring filter conditions for metrics. Filter methods include: contains, does not contain, regex match, and regex does not match. |
      ||Add the four arithmetic operations |Supports adding multiple metrics and performing the four basic arithmetic operations (addition, subtraction, multiplication, and division) on multiple original metrics. |
      ||Groups |You can group metrics. |
      

   * **Configure pie charts**

      Parameter description:

      
      |**Parameter** ||**DescriptionS** |
      |---|---|---|
      |Select a chart type |Chart name |A custom chart name is used to identify the chart. |
      ||Decimal places |Select the number of decimal places for chart values. Supports numeric values with up to four decimal places. |
      ||Period\-over\-period |Supports configuring the month\-over\-month value. After enabling this option, the month\-over\-month value is displayed at the lower right corner of the numeric value.<br><br>Calculation method: month\-on\-month = (current value \- comparison value) / comparison value |
      |Draw charts |Metric |Only a single metric can be displayed. When multiple metrics are added or the four basic arithmetic operations are applied to metrics, check **Show this metric** to select the metric to display. For details, refer to [metric description](https://docs.byteplus.com/en/docs/apmplus/custom_dashboard_app#3fde5e85). |
      ||Statistics |Some metrics have statistical types of COUNT and UNIQUE. Duration\-type metrics support configuring statistical value types such as AVG, PCT50, and more.<br><br><br>* Count based on time granularity<br><br>* UNIQ: Deduplicate by DID after calculating the total within each time granularity<br><br>* AVG: SUM(metric values within the time granularity) / sample size<br><br>* PCT1: The data at the 1st percentile after sorting in ascending order<br><br>* PCT5: The data at the 5th percentile after sorting in ascending order<br><br>* PCT25: The data at the 25th percentile after sorting in ascending order<br><br>* PCT50: The data at the 50th percentile after sorting in ascending order<br><br>* PCT75: The data at the 75th percentile after sorting in ascending order<br><br>* PCT90: The data at the 90th percentile after sorting in ascending order<br><br>* PCT99: The data at the 99th percentile after sorting in ascending order |
      ||Statistics for the selected time period |* TOTAL: Remove time granularity and calculate the global metric value within the selected time range<br><br>* AVG: SUM(metric value at each time granularity) / number of periods<br><br>* MAX: Maximum value in selected time range<br><br>* MIN: Minimum value within the selected time range<br><br>* SUM: SUM(the metric values for each time granularity)<br><br>* LAST: Last metric value within the selected time period<br><br>* NUMS: Items with metric values |
      ||Name a metric |Legends can be named by using dimension variables from the group configuration combined with fixed text. For example: the performance of $tag_aid. |
      ||Quick filter |If you need to synchronize with the dashboard's quick filter criteria, you can select a configured quick filter. |
      ||Filter criteria |You can configure filter conditions for metrics. The available filter methods are: contains, does not contain, matches regular expression, and does not match regular expression. |
      ||Add the four arithmetic operations |Supports adding multiple metrics and performing arithmetic operations on multiple original metrics. |
      ||Groups |Supports grouping of metrics for display. After grouping is enabled, the top 20 metric groups are displayed, and the remaining groups are categorized as Other. |
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The legend includes metric names and data details, including group values, metric names, metric values, and proportions.      </div>
      

<span id="63afeb0d"></span>
## Add a quick filter

Quick filter allows filtering metrics in the dashboard by dimensions configured in advance. An independent quick filter can be set up for each dashboard.


1. On the dashboard page, click **Manage quick filters**.

2. In the **common filter settings** dialog box, click **add common filter**.

3. In the **Common filter settings** dialog box, complete the following configuration, and then click **Finish**.

   Parameter description:

   
   |**Parameter** |**DescriptionS** |
   |---|---|
   |Name |Custom filter name, used to identify the current filter. |
   |Subnamespace |These are the dimensions for configuration filtering. |
   |Include |Select the values included in the dimension; you can also configure it to exclude them. |
   |Default value |The values that are included or not included in the dimension. The default value is empty, which indicates that no filter is applied by default. |
   


<span id="911c6911"></span>
## Configure quick filters

The quick filter will only take effect on the chart when it is set for the metric in the chart configuration.


1. On the dashboard page, click the  **···**  in the upper right corner of the target chart, then click **edit**.

2. In the **chart drawing** area, click the **Expand** to the right of the target metric.

3. In the metric configuration panel, check the quick filter option, then click **Save**.


<span id="26c69518"></span>
## Configuration of public dimension filter


* The public dimension filter allows you to directly select filter criteria in the toolbar, and the criteria you set will apply to all charts on the dashboard.

* The filter conditions for public dimensions and the filter conditions configured in each metric are combined as follows: for dimensions that are the same, their intersection is used; for dimensions that are different, their union is used.

   * Take the intersection when dimensions are the same

      For example, the filter condition for the public dimension is device model: iPhone 5, iPhone 6, and the filter condition for the chart is device model: iPhone 6, iPhone 7. The final filter condition is device model: iPhone 6.

   * Take the union of different dimensions

      For example, when the filter condition for the public dimension is device model: iPhone 5, iPhone 6, and the filter condition for the chart is APP version number 1.1.0, the final effective filter condition is device model: iPhone 5, iPhone 6, and APP version number 1.1.0.

* Filter conditions for public dimensions support regex filtering.


<span id="d5e565a5"></span>
## The management view

A view is simply a collection of quick filters and does not apply to the charts within the dashboard. When there are many filter conditions and multiple users collaborating on a dashboard, you can use the view feature to save your commonly used filter conditions.

For example, in a business scenario, Person A views information about Dimension A on dashboard M, while Person B views information about Dimension A and Dimension B on dashboard M. Person A needs to perform the following actions to create a view.


1. Add a quick filter to the default view on the dashboard page

   For details, refer to [Add quick filter](https://docs.byteplus.com/en/docs/apmplus/custom_dashboard_app#63afeb0d). For example, name it Common Filter A.

2. On the dashboard page, configure quick filters for target metrics in the target chart.

   For details, refer to [Quick filter configuration](https://docs.byteplus.com/en/docs/apmplus/custom_dashboard_app#911c6911).

3. On the dashboard page, click **Save view as**.

4. In the **Save view as** dialog box, enter a name for the view, for example, name it View A, and then click **Save**.

5. On the dashboard page, switch the default view to View A.

6. In the dashboard, User A can access View A, which displays common filter A. Person A can switch filter values to view changes in the chart.


At this time, Person A can view information about Dimension A in dashboard M, while Person B wants to view information about Dimension A and Dimension B in dashboard M. Person B needs to perform the following actions to create a view.


1. Add a quick filter in the default view on the dashboard page.

   For details, refer to [Add quick filter](https://docs.byteplus.com/en/docs/apmplus/custom_dashboard_app#63afeb0d). For example, name it Common filter B.

2. On the dashboard page, configure a quick filter for the target metric in the target chart.

   For details, refer to [Quick filter configuration](https://docs.byteplus.com/en/docs/apmplus/custom_dashboard_app#911c6911).

3. On the dashboard page, click **Save as view**.

4. In the **Save view as** dialog box, enter a name for the view—for example, name it View B—and then click **Save**.

5. On the dashboard page, switch the default view to View B.

6. In the dashboard, User B can access View B, which displays common filter A and common filter B. Person B can switch filter values to view changes in the chart.


<span id="967b1c70"></span>
## Subscribed dashboards

The purpose of subscribing to a dashboard is to receive regular updates about the dashboard through a subscription method you set up.


1. On the dashboard page, click **Subscribe to dashboard**.

2. In the **create schedule report** dialog box, complete the configuration and then click **confirm**.

   Parameter description:

   
   |**Parameter** |**DescriptionS** |
   |---|---|
   |Subscription name |Defaults to the name of the dashboard, but you can customize it. |
   |Subscription cycles |Configure when to receive subscription notifications. Supports configuration for a specific time point each day, week, or month. |
   |Query interval |You can customize the query period, which defines the time range for dashboard data. |
   |Subscription methods |Supports selecting different subscription methods and allows multiple selections. Can be configured as email, WeCom, Lark, or DingTalk.<br><br>For details about webhook configuration, see [How to configure a webhook?](https://docs.byteplus.com/en/docs/apmplus/How_to_configure_a_webhook). |
   |Receiving groups |Configure the object that receives dashboard schedule report information. |
   |Subscription switch |Configure subscription switches.<br><br><br>* Open: Receive the dashboard information.<br><br>* Turn off: Do not receive dashboard information. |
