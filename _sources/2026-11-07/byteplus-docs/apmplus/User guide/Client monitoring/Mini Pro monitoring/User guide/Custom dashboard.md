---
title: "Custom dashboard"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/custom_dashboard_minipro"
---

The custom dashboard allows you to flexibly configure metrics and chart types.

<span id="f706c82c"></span>
## Metric description

The metric types and metrics that can be configured in the custom dashboard are as follows:


|Classifications |Metric |
|---|---|
|User analyses |PV, UV, session count, page time on site, average time on site. |
|Performance |total launch count, cold start count, warm start count, first screen cold start total time, Mini Program initialization time, download time, JS injection time (WeChat only), first screen load time, first screen render time, first screen total load time, open rate, churn rate, slow start rate, total launch count, route change time, page build time, page render time, total page navigation time, first render time (FR), page first paint (FP), page first contentful paint (FCP), page largest contentful paint (LCP), slow page, total page count, slow page rate, setData call count, setData time, setData frequency, setData size. |
|JavaScript error |Error count, error rate, impacted users, impacted users rate. |
|request |cancelled request count, user count, slow request rate, slow request affected user count, slow request affected user rate, request success count, request success rate, request count, request time, redirect time, Cache Time, DNS Resolution Time, TCP Connection Time, SSL Handshake Time, Request Send Time, Response Time, callback time, transmitted data size, received data size, request error, request error affected user count, request error rate. |
|custom log |Sample sizes and user numbers |


<span id="df627592"></span>
## Create a dashboard


1. Log in to the [Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client/console/overview).

2. In the target application, click **Mini Program Pro Monitoring**.

3. Select**All features \> Custom dashboard**.

4. On the **dashboard list** page, click **create dashboard**.

5. On the **create dashboard** page, enter the dashboard name, then click **confirm**.

   Configuration description:

   **Dashboard name**: Custom dashboard name used to identify the dashboard. Dashboard name must not exceed 100 characters.


<span id="ce459e52"></span>
## **Configuration charts**


1. On the dashboard page, click **Add container**.

   A container is used to group multiple charts together and summarize them within the container.

2. Click the edit button to modify the container name.

3. On the dashboard page, click **Add component**.

4. On the **create chart** page, configure components, then click **Save**.

   The custom dashboard supports adding four types of components: trend charts, number cards, tables, and pie charts.

   * **Configuration trends chart**

      Configuration description

      
      |**Parameter** ||**DescriptionS** |
      |---|---|---|
      |Select chart types |Chart name |Customize the chart name to identify the chart. |
      ||Decimal places |Select the number of decimal places for values displayed in the chart. Supports numbers with up to four decimal places. |
      ||Y axis |Configure the maximum and minimum values of the Y\-axis. |
      ||Legend |Supports legend configuration and the fields displayed in the legend, including minimum, maximum, average, and current. |
      ||Period\-on\-period |Supports configuration of the month\-over\-month value. When enabled, the month\-over\-month value is displayed as a dashed line. |
      |Draw charts |Metric |Supports selecting metrics to query and allows adding multiple. For details, refer to [metric description](https://docs.byteplus.com/en/docs/apmplus/custom_dashboard_minipro#f706c82c). |
      ||Groups |Supports configuration of grouping dimensions for a metric, allows you to add multiple dimensions, and after selection, the trend chart will be grouped and displayed according to the selected dimensions. |
      ||Statistics |Some metrics have the statistical types COUNT and UNIX. Duration\-type metrics support configuring the statistical value type, such as AVG, PCT50, and more.<br><br>Statistical methods and descriptions are as follows:<br><br><br>* **COUNT**: Count based on time granularity<br><br>* **UNIQ**: After calculating the sum within each time granularity, deduplicate by DID<br><br>* **AVG**: SUM of metric values within the time granularity / sample size<br><br>* **PCT50**: The data at the 50th percentile after sorting in ascending order<br><br>* **PCT75**: The data at the 75% position after sorting in ascending order<br><br>* **PCT90**: The data point at the 90% position after sorting in ascending order<br><br>* **PCT99**: The data at the 99th percentile after sorting in ascending order |
      ||Name metrics |Legend naming is supported, and the display rule is custom name plus metric name. |
      ||Quick filter |If you need to synchronize with the dashboard's quick filter, you can select a pre\-configured quick filter. |
      ||Filter criteria |You can configure filter conditions for metrics. Filter methods include: **contains**, **does not contain**, **Regex match**, and **Regex does not match**.<br><br>Multiple filter conditions can be configured, and the relationship between these filter conditions can be set to **and** or **or**. |
      ||Add the four basic arithmetic operations |If you need to perform arithmetic operations on existing metrics, for example, to sum the error count for all exception types, you can use the arithmetic operations feature. |
      ||Add tag |You can add marker lines or marker areas to the trend chart, name them, and add multiple markers. |
      

   * **Configure numeric cards**

      The final effect of displaying a numeric card is that it shows a statistical number.

      Configuration description:

      
      |**Parameter** ||**DescriptionS** |
      |---|---|---|
      |Select a chart type |Chart name |Customize the chart name to identify the chart. |
      ||Decimal places |Select the number of decimal places to display for chart values. Supports up to four decimal places for numeric values. |
      ||Month\-over\-month |Supports configuring the month\-over\-month value. When enabled, the month\-over\-month value is displayed at the bottom right of the value.<br><br>Calculation method: month\-on\-month = (current value \- comparison value) / comparison value |
      |Draw charts |Metric |Support selecting the metrics to query. For details, refer to [metric description](https://docs.byteplus.com/en/docs/apmplus/custom_dashboard_minipro#f706c82c).<br><br>When multiple original metrics are added, only the last added metric is displayed. |
      ||Statistics |The statistical type for some metrics is COUNT or UNIQUE. Duration\-type metrics support configuring the statistical value type, such as AVG, PCT50, and so on.<br><br>The statistical method and description are as follows:<br><br><br>* **COUNT**: Count based on time granularity<br><br>* **UNIQ**: After calculating the sum within each time granularity, deduplicate by DID<br><br>* **AVG**: SUM(metric values within the time granularity) / sample size<br><br>* **PCT50**: The value at the 50th percentile after sorting in ascending order<br><br>* **PCT75**: The data value at the 75th percentile after sorting in ascending order<br><br>* **PCT90**: Data at the 90% position after sorting in ascending order<br><br>* **PCT99**: The data at the 99th percentile after sorting in ascending order |
      ||Unit |Supports configuration of the unit for the final displayed value. For example, the unit configuration for FPS is set to s (seconds). |
      ||Statistics for the selected time period |The statistical method and descriptions for time segments are as follows:<br><br><br>* **TOTAL**: Remove time granularity and calculate the global metric value for the selected time range<br><br>* **AVG**: SUM of the metric values for each time granularity / number of periods<br><br>* **MAX**: Maximum value within the selected time range<br><br>* **MIN**: Minimum value within the selected time range<br><br>* **SUM**: SUM(the metric value for each time granularity)<br><br>* **LAST**: The last metric value within the selected time period<br><br>* **NUMS**: Items with metric values |
      ||Quick filter |If you need to link with the dashboard's quick filter criteria, you can select a configured quick filter. |
      ||Filter criteria |You can configure filter conditions for metrics. The available filter methods are: **Contains**, **Does not contain**, **Regex match**, and **Does not match regex**. |
      ||Add the four arithmetic operations |If arithmetic operations are added to a metric, the final metric calculated through these operations will be displayed. |
      

   * **Configuration table**

      The configuration description

      
      |**Parameter** ||**DescriptionS** |
      |---|---|---|
      |Select a chart type |Chart name |A custom chart name is used to identify the chart. |
      ||Decimal places |Select the number of decimal places for values displayed in the chart. Supports numerical values with up to four decimal places. |
      ||Sorting |If there are multiple metrics, you need to select which metric to use for sorting, and configure the table to display the top N values according to the selected sorting method.<br><br><br>* Sorting method supports **ascending** and **descending**.<br><br>* Top values include Top**10**, **20**, **30**, **40**, **50**, and **100**. |
      ||Month\-over\-month |Supports configuration of the sequential comparison value. When enabled, the comparison value is displayed in parentheses to the right of the main value.<br><br>Method: Sequential comparison = (current value \- comparison value) / comparison value |
      |Create charts |Metric |Supports selecting metrics to query and allows adding multiple metrics. For details, refer to [metric description](https://docs.byteplus.com/en/docs/apmplus/custom_dashboard_minipro#f706c82c). |
      ||Statistics |Some metrics use COUNT and UNIX as their statistical type. Duration\-type metrics support configuration of the statistical value type as AVG, PCT50, and more.<br><br>Statistical methods and description are as follows:<br><br><br>* **COUNT**: Counts by time granularity<br><br>* **UNIQ**: After calculating the sum within the time granularity, deduplicate by DID<br><br>* **AVG**: SUM(metric values within the time granularity) / sample size<br><br>* **PCT50**: The data at the 50% position after sorting in ascending order<br><br>* **PCT75**: The data at the 75th percentile after sorting in ascending order<br><br>* **PCT90**: The data at the 90th percentile after sorting in ascending order<br><br>* **PCT99**: The value at the 99% position in the data sorted in ascending order |
      ||Statistics for the selected time period |The statistical methods and description for time intervals are as follows:<br><br><br>* **TOTAL**: Disregard time granularity and calculate the global metric value for the selected time range<br><br>* **AVG**: SUM(metric value for each time granularity) / number of periods<br><br>* **MAX**: Maximum value within the selected time range<br><br>* **MIN**: The minimum value within the selected time range<br><br>* **SUM**：SUM(each time granularity's metric values)<br><br>* **LAST**: The last metric value within the selected time period<br><br>* **NUMS**: Items with metric values |
      ||Column Name |Supports custom table column names, with column names automatically including the type of statistic value selected. |
      ||Unit |Supports configuration of units for data in table columns. For example, the unit configuration for FPS is s (seconds). |
      ||Quick filter |If you need to link with the dashboard's quick filter criteria, you can select a quick filter that has already been configured. |
      ||Filter criteria |You can configure filter conditions for metrics. The available filter methods are: **Contains**, **Does not contain**, **Regular expression match**, and **Regular expression does not match**. |
      ||Add the four arithmetic operations |Supports add multiple metrics and perform arithmetic operations on multiple original metrics. |
      ||Groups |You can group metrics. |
      

   * **Pie chart configuration**

      Configuration description

      
      |**Parameter** ||**DescriptionS** |
      |---|---|---|
      |Select a chart type |Chart name |A custom chart name used to identify the chart. |
      ||Decimal places |Select the number of decimal places for chart values. Supports up to four decimal places for numerical values. |
      ||Month\-on\-month |Supports configuration of the period\-over\-period value. When enabled, the period\-over\-period value is displayed at the lower right corner of the value.<br><br>Calculation method: Period\-over\-period = (current value \- comparison value) / comparison value |
      |Draw charts |Metric |Only single metric display is supported. When multiple metrics are added or arithmetic operations are applied to metrics, you can select which metric to display by checking **Show this metric**. For details, refer to [metric description](https://docs.byteplus.com/en/docs/apmplus/custom_dashboard_minipro#f706c82c). |
      ||Statistics |The statistical types for some metrics are COUNT and UNIX. Duration\-type metrics support configuration of statistical value types such as AVG, PCT50, and more.<br><br>Statistical methods and descriptions are as follows:<br><br><br>* **COUNT**: Count by time granularity<br><br>* **UNIQ**: After calculating the total within each time granularity, deduplicate by DID<br><br>* **AVG**: SUM(metric values within the time granularity) / sample size<br><br>* **PCT50**: The data at the 50% position after sorting in ascending order<br><br>* PCT75: The data at the 75th percentile after sorting in ascending order<br><br>* **PCT90**: The data at the 90th percentile after sorting in ascending order<br><br>* **PCT99**: The data at the 99th percentile after sorting in ascending order |
      ||Statistics for the selected time period |The statistical methods and descriptions for time segments are as follows:<br><br><br>* **TOTAL**: Shows the global metric value for the selected time range, without time granularity<br><br>* **AVG**: SUM(the metric value for each time granularity) / number of periods<br><br>* **MAX**: The maximum value within the selected time range<br><br>* **MIN**: Minimum value within the selected time range<br><br>* **SUM**: SUM (the metric value for each time granularity)<br><br>* **LAST**: The last metric value in the selected time period<br><br>* **NUMS**: Items with metric values |
      ||Name metrics |Legend names can be created by combining dimension variables and fixed text from the group configuration. For example: the performance of $tag_aid. |
      ||Quick filters |If you need to link with dashboard quick filter criteria, you can select a pre\-configured quick filter. |
      ||Filter criteria |Supports configuring filter conditions for metrics. The available filter methods are: **Contains**, **Does not contain**, **Regular expression match**, and **Regular expression does not match**. |
      ||Add the four basic arithmetic operations |Supports adding multiple metrics and performing the four basic arithmetic operations (addition, subtraction, multiplication, and division) on multiple original metrics. |
      ||Groups |Supports displaying metrics by group. After grouping is enabled, the top 20 metric groups are displayed, and the remaining groups are categorized as Other. |
      


<span id="49014c07"></span>
## Add a filter

Quick filter allows metrics in the dashboard to be filtered by dimensions configured in advance. Each dashboard can be configured with its own independent quick filter.


1. On the dashboard page, click **Manage quick filter**.

2. In the **Commonly used filter settings** dialog box, click **Add commonly used filter**.

3. In the **Common filter settings** dialog box, configure the following settings, then click **Finish**.

   Configuration description:

   
   |**Parameter** |**DescriptionS** |
   |---|---|
   |Name |Custom filter name, used to identify the current filter. |
   |Subnamespace |Configure the filter dimensions. |
   |Include |Select which dimension values to **include**, or configure to **exclude**. |
   |Default value |Values for inclusion or exclusion in the dimension. The default value is empty, which means no filter is applied by default. |
   


<span id="432928f0"></span>
## Quick filter configurations

The quick filter will only take effect on the chart if it is set for the metric in the chart configuration.


1. On the dashboard page, click the  **···**  in the upper right corner of the target chart, then click **edit**.

2. In the **charting** area, click the **Expand** button to the right of the target metric.

3. In the metric expansion configuration, check the quick filter option, then click **Save**.


<span id="97e155d2"></span>
## Configure public dimension filters


* Public dimension filtering allows you to directly select filter conditions for public dimensions in the toolbar. The filter conditions you set will apply to all charts on the dashboard.

* The filter conditions for public dimensions and the filter conditions already configured in each metric are combined as follows: if the dimensions are the same, take the intersection; if the dimensions are different, take the union.

   * Take the intersection of the same dimensions

      For example, the filter condition for the public dimension is device model: iPhone 5, iPhone 6, and the filter condition for the chart is device model: iPhone 6, iPhone 7. Therefore, the final filter condition applied is device model: iPhone 6.

   * Take the union when dimensions differ

      For example, if the filter condition for the public dimension is device model: iPhone 5, iPhone 6, and the filter condition for the chart is APP version number 1.1.0, then the final applied filter condition will be device model: iPhone 5, iPhone 6, and APP version number: 1.1.0.

* Filter criteria for public dimensions support regular expression filtering.


<span id="ab5b3fc5"></span>
## Management views

A view is simply a collection of quick filters and does not affect the charts within the dashboard. When there are many filter conditions and multiple users are collaborating on a dashboard, you can use the view feature to save your frequently used filter conditions.

For example, in a business scenario, Person A views information about Dimension A in dashboard M, and Person B views information about Dimension A and Dimension B in dashboard M. Person A needs to perform the following actions to create a view.


1. On the dashboard page, add a quick filter in the default view.

   For details, refer to [add quick filter](https://docs.byteplus.com/en/docs/apmplus/custom_dashboard_minipro#49014c07). For example, name it Common Filter A.

2. On the dashboard page, configure quick filters for the target metrics in the target chart.

   For details, refer to [Quick filter configuration](https://docs.byteplus.com/en/docs/apmplus/custom_dashboard_minipro#49014c07).

3. On the dashboard page, click **Save view as**.

4. In the **Save View As** dialog box, enter a view name, for example, name it View A, and then click **Save**.

5. On the dashboard page, switch the default view to View A.

6. In the dashboard, user A can access View A, which displays the commonly used Filter A. User A can switch filter values to view chart changes.


At this time, person A can view information about dimension A in dashboard M. Therefore, to view information about Dimension A and Dimension B in dashboard M, Person B needs to perform the following actions to create a view.


1. Add a quick filter to the dashboard page under the default view.

   For details, refer to [Add quick filter](https://docs.byteplus.com/en/docs/apmplus/custom_dashboard_minipro#49014c07). For example, name it Common Filter B.

2. On the dashboard page, configure a quick filter for the target metric in the target chart.

   For details, refer to [Configure quick filter](https://docs.byteplus.com/en/docs/apmplus/custom_dashboard_minipro#49014c07).

3. On the dashboard page, click **Save view as**.

4. In the **Save View As** dialog box, enter a view name, for example, name it View B, and then click **Save**.

5. On the dashboard page, switch the default view to View B.

6. In the dashboard, Person B can view View B, which displays Common Filter A and Common Filter B. Person B can switch filter values to view changes in the chart.


<span id="a7cabeb2"></span>
## Subscribed dashboards

The purpose of subscribing to a dashboard is to receive dashboard updates at scheduled intervals via the configured subscription method.


1. On the dashboard page, click **Subscribe to dashboard**.

2. In the **create schedule report** dialog box, complete the configuration, then click **confirm**.

   Configuration description

   
   |**Parameter** |**DescriptionS** |
   |---|---|
   |Subscription name |By default, the name is set to the dashboard name. You can customize it. |
   |Subscription period |Configure the time to receive subscription notifications. Supports configuration for a specific time on a daily, weekly, or monthly basis. |
   |The query cycle |Supports custom query periods, that is, the time range for dashboard data. |
   |Subscription methods |Supports selecting different subscription methods and allows multiple selections. Can be configured as **Email**, **WeCom**, **Lark**, and **DingTalk**.<br><br>For details on webhook configuration, see [How to configure a webhook?](https://docs.byteplus.com/en/docs/apmplus/How_to_configure_a_webhook). |
   |Receiving groups |Configure the object to receive schedule report information. |
   |Subscription switch |Configure subscription switches.<br><br><br>* Open: Receive dashboard information.<br><br>* Turn off: Do not receive dashboard information. |
