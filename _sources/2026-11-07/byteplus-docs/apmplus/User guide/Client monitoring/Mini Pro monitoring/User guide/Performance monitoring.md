---
title: "Performance monitoring"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Performance_monitoring"
---

Performance monitoring provides an overview of the overall performance of the mini program, including start performance, page performance, and runtime performance. It reflects the speed at which the mini program loads and renders, as well as the responsiveness to user interactions. Combined with alerting and data exploration, it enables faster identification of performance issues and serves as a data foundation for performance optimization.

<span id="rac7S36Y"></span>
## Startup performance

The startup of a mini program is a critical factor in the mini program user experience. Paying attention to excessive startup times is an important aspect of improving the mini program user experience.

The start of a mini program begins when **the user opens the mini program** and ends when **the mini program home page is fully rendered**. The indicator that a mini program's **homepage has finished rendering** is the triggering of the `Page.onReady` event on the first page. The detailed timing diagram is as follows:

<span id="bQMoKtex"></span>
### Startup performance trend chart

Startup performance\-related metrics can be divided into three categories: startup overview, general performance metrics, and initialization performance metrics. and visualize metrics in the form of stacked charts, combination charts, and line charts.


* Each chart includes data: the average value of the metric in the current time period, the metric value in the previous period, and the fluctuation relative to **the previous period**.

   The value of the previous period refers to the value from the previous selected time period. For example, if you select a cycle of seven days, the previous cycle is the previous seven days.

* In the line chart, you can view the poor performance baseline set in the project settings, which helps you assess the distribution of metric values.

   
   |**Metric name** |**Calculation rules** |**DescriptionS** |**Compatibility status** |
   |---|---|---|---|
   |Total start count |Cold start count + hot start count |None |All |
   |Cold start |Pageview.source === number of launches |None |All |
   |Hot start |Pageview.source === showCount |None |All |
   |Total cold start time for the first screen |pageRenderEnd \- App.trigger |The total loading time from clicking the mini program to the completion of the first screen rendering includes the time for code package download (this is only included on the first launch), code execution, first screen rendering, and other similar durations. |* WeChat Mini Program<br><br>* Douyin Mini Program |
   |Mini program initialization time |appInitEnd \- App.trigger |From clicking the mini program until cold start completes |* WeChat Mini Program<br><br>* Douyin Mini Program |
   |Download duration |downloadPackage |Time taken to download the code package, time taken to download the mini program package during the first startup |* WeChat Mini Program<br><br>* TikTok mini program |
   |JS injection duration |performance.evaluateScript |JS code injection time, JS file injection time during the startup process |WeChat Mini Program |
   |First screen load time |pageLoadStart \- appInitEnd |None |All |
   |First screen build time |pageDomEnd \- pageLoadStart |None |All |
   |First screen rendering time |pageRenderEnd \- pageDomEnd |None |All |
   |Total time to load the first screen |pageRenderEnd \- appInitEnd |None |All |
   |Open rate |pageRenderEnd count / appInitEnd count |Completion rate from the start of the mini program to the first screen rendering |All |
   |Attrition rate |1 \- Open rate |Probability of exiting the mini program after starting it but before the first screen is rendered |All |
   |Slow start rate |Number of starts where the total first screen load time exceeds the set threshold |The slow start rate |All |
   


<span id="wGzxNAnh"></span>
### Page with suboptimal performance

The Poor Performance page displays information about PIDs with poor performance on the selected metrics, aggregated by PID, under the current sample size threshold. When you expand this information, a multi\-metric performance trend chart for this PID will be displayed on the right. Click **Number of slow pages** to go to **Data exploration** and view slow page details.

<span id="Qsb8Roif"></span>
### Startup duration distribution

You can view the distribution of startup time for the selected metrics.


* Drag the slider below to customize the duration range displayed. In the upper right corner, you can view the proportion of report volume within the duration range set by the slider.

* Hover over the bar to view the duration range, report count, and proportion of the bar for each segment.

* Clicking a column will navigate to **Data Exploration**.


<span id="1etWlaiQ"></span>
### Performance optimization/degradation

The optimization and degradation page aggregates data by PID and displays information about the PIDs with the most significant start performance optimization or degradation within the currently selected time range.


* Selecting the corresponding PID will display trend information for related metrics. If release\-related information is configured, the deployed version can be displayed in the trend chart.

* The comparison period refers to dividing the currently selected range into two parts for comparison. For example, when the current time range is three days, the comparison is made between the metric values from the first 1.5 days and those from the last 1.5 days.


<span id="kQRnnLAs"></span>
## The page performance

Mini program page performance refers to the performance during page transitions in a mini program. The timestamps corresponding to each performance metric are shown in the following figure.

<span id="t39Dm7Ek"></span>
### Page performance trend chart

Indicator descriptions


|**Metric name** |**Calculation rules** |**Compatibility status** |
|---|---|---|
|The total page redirect time |renderEnd \- navigateStart |All |
|Route switching time |loadStart \- navigateStart |All |
|Page build time |domEnd \- loadStart |All |
|Page rendering time |renderEnd \- domEnd |All |
|Initial render (FR) |performance.FR.duration |WeChat Mini Programs |
|Page first paint (FP) |FP.startTime \- loadStart |* WeChat Mini Program<br><br>   * [iOS is not supported](https://developers.weixin.qq.com/miniprogram/dev/api/base/performance/PerformanceEntry.html#.On46dGV4dD3ohJrmnKwtLHN0cmluZyBuYW1lLC3mjIfmoIflkI3np7A=)<br><br>* Douyin Mini Program |
|First Contentful Paint (FCP) |FCP.startTime \- loadStart |* WeChat Mini Program<br><br>   * [Not supported on versions below iOS 14.5](https://developers.weixin.qq.com/miniprogram/dev/api/base/performance/PerformanceEntry.html#.On46dGV4dD3ohJrmnKwtLHN0cmluZyBuYW1lLC3mjIfmoIflkI3np7A=) |
|Largest Contentful Paint (LCP) |LCP.startTime \- loadStart |* WeChat Mini Program<br><br>   * [iOS is not supported](https://developers.weixin.qq.com/miniprogram/dev/api/base/performance/PerformanceEntry.html#.On46dGV4dD3ohJrmnKwtLHN0cmluZyBuYW1lLC3mjIfmoIflkI3np7A=) |
|Bounce rate caused by page rendering issues |renderEnd count divided by navigateStart count, if navigateStart count is not zero |All |
|Slow page occurrences |Number of reports where total page redirect time exceeds the set threshold |All |


<span id="lB0semOy"></span>
### Pages with poor performance


* The suboptimal performance page aggregates data by PID and displays information about PIDs with poor performance for the selected metrics under the current sample size threshold.

* When PID information is expanded, the performance trend chart for multiple metrics of that PID will be displayed.

* Click PID to navigate to **Overview**, where you can view page details.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">All features of the Mini Program Pro Monitoring Platform rely heavily on PID settings. By configuring appropriate page identifiers relevant to the business, issues related to performance anomalies can be identified more effectively.</div>


<span id="iajuRL9a"></span>
### Page duration distribution

Page time distribution allows you to view the distribution of time consumption for selected metrics. Drag the slider below to customize the displayed duration range. You can also view the proportion of reported quantity within the selected duration range in the upper right corner.

<span id="EgS86FOf"></span>
### Performance optimization/degradation

The optimization and degradation page aggregates data by PID and displays information about the PIDs with the most severe performance optimization or degradation within the currently selected time range. Selecting the corresponding PID displays trend information for related metrics. Additionally, if release\-related configuration information is available, the live version can be displayed in the trend chart.

<span id="C2IpqkbL"></span>
## Runtime performance

<span id="caagk3qW"></span>
### setData list

setData is the most frequently used interface in mini program development and is also the one most likely to cause performance issues. Calling setData too frequently can keep the JS thread continuously busy, and if setData takes too long to execute, it can cause page rendering to become sluggish. Based on the list of metrics related to setData, you can sort by each metric to investigate problems.


* When you click the PID, you are navigated to **Data Exploration**, and the mini program type, system, and PID in the filter criteria are preserved.

* The setData list displays PID, setData count, setData duration, setData frequency, and setData size.

   Indicator description:

   
   |**Metric** |**Calculation rules** |**DescriptionS** |
   |---|---|---|
   |Number of setData calls |Number of reports within the time range |None. |
   |setData duration |Total setData time / number of page views |Average cumulative setData time per page view. |
   |setData calls per second |setData count / time range (unit: s) |None. |
   |Size of setData |Total setData size per PV |The average cumulative size of setData per page view. |
