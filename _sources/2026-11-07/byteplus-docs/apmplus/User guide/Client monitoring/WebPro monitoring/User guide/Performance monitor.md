---
title: "Performance monitor"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/performance_monitor"
---

The performance monitor page contains two main modules: PID aggregation and performance overview. With alerts and data explore, you can more quickly identify performance issues and serve as the data basis for pageload performance optimization.

<span id="6d184cd9"></span>
## Prerequisites

LongTask has been integrated. For details, refer to [Web SDK integration](https://docs.byteplus.com/en/docs/apmplus/Integrate_WebPro_SDK). The SDK turns on LongTask Monitoring by default, with a default sampling rate of 0.01.

<span id=".UElE6IGa5ZCI"></span>
## PID aggregation

By default, pid is automatically obtained from the pathname or hash of the current page URL. However, if a pid is provided during initialization, the pid provided by the business takes precedence. In a single\-page application, unless the pid is hardcoded during initialization, each page will have a different pid.

<span id=".5oyH5qCH6L6-5qCH546H"></span>
### Metric compliance rate

On the site settings page, set the compliance rate for each performance metric for the current site. Afterwards, you can see the number of PIDs that currently meet the criteria at the top of the performance monitor.

The compliance rate trend chart displays the number of PIDs meeting the baseline requirements divided by the total number of PIDs within the selected time period as a reference for optimization.


* By default, the page displays the FP compliance rate, FCP compliance rate, LCP compliance rate, FMP compliance rate, TTI compliance rate, and LOAD compliance rate. To view the compliance rate of custom performance metrics, please first register the performance metrics on the performance metric management page. For details, refer to [performance metric management](https://docs.byteplus.com/en/docs/apmplus/performance_metric).

* Default performance metrics and custom performance metrics both support setting metric baselines in **project setting \> performance baseline setting**.


<span id=".5oCn6IO95pyA5beu6aG16Z2i"></span>
### The worst\-performing page

You can sort by which performance metric and statistical method to view the top 5 pages with the worst performance across all pages on the site. Performance metrics include default and custom metrics. Statistical measures include average, 50th percentile, 75th percentile, 90th percentile, and 95th percentile.


* The page list displays the Top 5 pages with the worst performance across the entire site, filtered from all pages according to the specified filter criteria. These five pages can also be sorted by custom or default metrics. For example, you can sort the pages by FP in ascending order, and then, among the top five pages with the worst performance, identify the one with the longest FP.

* Aggregate by PID and display the PID with the worst performance for the selected metric under the current sample size threshold.

   All features of the WebPro Monitoring platform are highly dependent on PID settings. Configuring appropriate business\-related pages can help better identify performance exception\-related issues.

* Expanding the PID information will display the performance trend chart for multiple metrics of that PID.

* Click PID content to enter the **page details** page, where you can view the trend chart, distribution, Bounce Rate, and other information for that page.

* Click slow\-pageload count to navigate to the **data explore** page, where you can view slow page details.


<span id=".6aG16Z2i6ICX5pe25Yy66Ze05YiG5biD"></span>
### Distribution of page load times by interval

The page load time interval distribution allows you to view the distribution of load times for the selected metric.


* Drag the slider below to customize the display range for duration. In the upper right corner, you can also view the proportion of report volume for the included time range.

* Hover over a bar to view the time range, report volume, and proportion for each segment.

* Click the column to navigate to the **data explore** page to view details for each URL under the Views page.


<span id=".5LyY5Yqj5YyW"></span>
### Performance optimization/degradation

The performance optimization and degradation page aggregates data by PID and displays information about the PIDs with the most significant performance optimization or degradation within the currently selected time range.


* In the trend chart, the currently selected range is split into two for comparison. As shown in the figure, the current time range is 3 days, so the mean FCP on the data explore page during the latter 1.5 days is 697 ms lower than during the first 1.5 days.

* Click the corresponding PID to go to the **page details** page to view the performance overview of that page.

* If release\-related information is included in the configuration, released versions can be displayed in the trend chart to help determine whether performance improvements or degradations are caused by new versions. To configure release information, refer to [version management](https://docs.byteplus.com/en/docs/apmplus/version_management)


<span id=".6aG16Z2i6K-m5oOF"></span>
## Metrics overview

The metrics overview provides overview details of both default and custom performance metrics when the filter is set to the entire site. It includes trend charts, distribution, and Bounce Rate, serving as a data foundation for performance optimization. To modify the baseline for each metric, you can adjust them in **project settings \> performance baseline settings**.

<span id="2e723c1a"></span>
### Performance metrics overview

The performance metrics overview displays the performance metrics for the entire site. These site\-wide performance metrics are affected by multiple factors from different pages and provide limited assistance for troubleshooting actual performance issues. If you want to better observe performance metrics, please view them under the specific PID.

In web monitoring scenarios, in addition to common performance metrics such as FP, FCP, and LCP, Application Performance Management Plus also provides Long Task monitoring and corresponding usage data. In the metric overview, the **longtask count** and **longtask time** are displayed as cards based on the current filter conditions.


* Longtask count: The average number of longtasks for the next PV under the corresponding PID.

* longtask time: The average cumulative lag duration for the next PV under the corresponding PID.


LongTask is an experimental API that intuitively tells us which tasks take 50 milliseconds or more to execute. For the 50\-millisecond threshold standard, refer to [Response: process events in under 50ms](https://developers.google.com/web/fundamentals/performance/rail#response) in the RAIL Model.

So, what can LongTask be used for?

LongTask measures any continuous, uninterrupted period of time during which the main UI thread is busy for 50 milliseconds or longer.

Typical scenarios are as follows:


* Long\-running event callbacks (Long\-running event handlers)

* Expensive reflows and other re\-renders

* Work the browser does between adjacent cycles of the event loop when the interval between them exceeds 50 milliseconds.


What problems can tasks that block the main thread for 50 milliseconds or longer cause?


* Interactive latency.

* Severe instability and delay in interactive actions (tap, click, scroll, mouse wheel, and more).

* Severe and unstable delay in event callbacks.

* Chaotic animation and scrolling.


<span id="dac34656"></span>
### Trend charts

In the trend chart, the left side displays how the default metrics and custom metrics relate to the baseline value under the PID filter condition, while the right side shows the trend chart for the filtered time range.

Click the corresponding metric name on the left to navigate to **data explore** for further analysis of performance details, with the performance baseline setting carried into the search conditions of **data explore** as a filter. Then, clicking on a single data item allows you to view a summary of all performance metrics for the selected View, as well as the corresponding waterfall chart of resource loading and API durations. This helps identify whether a decline in overall page performance metrics is caused by individual resources or requests.

<span id="7890ee77"></span>
### Distribution

In the duration distribution chart, the left side displays the relationship of the default and custom metrics to the baseline value with the PID filter applied, while the right side shows the duration distribution within the selected time range.

Different performance metrics are visualized in different colors within the elapsed time distribution, according to the baseline setting. In the chart, blue represents meeting expectations, yellow represents slightly below expectations, and red represents significantly below expectations.

<span id="e72484ed"></span>
### Bounce Rate

The method for calculating metrics is as follows:


|**Metric** |**Calculation method** |
|---|---|
|FP Bounce Rate |Number of sessions that exited the page before FP reporting / total number of sessions |
|FCP Bounce Rate |Number of sessions that exited the page before FCP reporting / total number of sessions |
|LCP Bounce Rate |Number of sessions that exited the page before LCP reporting / total number of sessions |
|FMP bounce rate |Sessions that exited the page before FMP reporting / total sessions |
|CLS bounce rate |Number of sessions that exited the page before CLS reporting / total number of sessions |
|LOAD bounce rate |Number of sessions that exited the page before LOAD reporting / total number of sessions |
|TTI bounce rate |Number of sessions that exited the page before TTI reporting / total number of sessions |


<span id=".5pyA5L2z5a6e6Le1"></span>
## best practices

<span id=".5Y-R546w5bm25a6a5L2N5Y2h6aG_55qE6aG16Z2i"></span>
### Discover and locate lagging pages

<span id="1eb3bbca"></span>
#### **Enter from Data Explore**


1. On the data explore page, select the **Long Tasks** tab.

2. Click details for the specific LongTask.

3. Click a specific View in the session to view the waterfall information corresponding to a single pageview and fully reproduce the scenario.


<span id="5f8bdea0"></span>
#### **Access from performance monitor**


1. On the site performance overview page, click the **metric overview** tab.

   The performance metrics overview displays the longtask count and longtask time as cards under the current filter conditions.

2. Click the specific value in the performance metric overview to jump to the **data explore** **LongTask** tab to view the corresponding details.

3. Click the corresponding page in the details list. Then, in the hierarchy, click the specific View to view the waterfall information for a single pageview and fully reconstruct the scene.


<span id=".6YWN5ZCI5oql6K2m5L2_55So"></span>
### For use with alert

After selecting performance metric as the alert type and selecting longtask time as the alert metric, you can configure alerts related to LongTask.
