---
title: "New H5 monitoring"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/New_H5_monitoring"
---

This article introduces the JavaScript overview and sourcemap management in the New H5 monitor. The New H5 monitor inherits the collection capabilities of the WebPro SDK and adds new features such as blank screen monitoring and page scoring to the core functions of web monitoring. These enhancements significantly improve both collection capabilities and the use of product features, helping you better locate and analyze page issues.

<span id="e5557336"></span>
## JavaScript overview

The JavaScript overview displays information about errors that occur in the application and allows filtering by attributes such as browser, device, operating system, region, user, access information, and error status. With this feature, you can better understand and observe exceptions that occur at runtime, and handle them effectively.

<span id="d6820d82"></span>
### JavaScript error trend chart

The JavaScript error trend chart displays the trends of JavaScript error metrics under filter conditions. On the right side of the metric data, you can view the changes in JavaScript error data compared to the previous period.

Metric description:


|Metric |DescriptionS |
|---|---|
|error count |JavaScript error count under filter conditions |
|impacted user |User count (UV) affected by JavaScript errors under filter conditions |
|error rate |JavaScript error count under filter conditions / total launch count under filter conditions |
|affected user rate |Number of deduplicated UVs for which a JavaScript error occurred under filter conditions / total deduplicated UVs under filter conditions |


<span id="92005ece"></span>
### Errors and page list


|Error types |Illustration |
|---|---|
|A JavaScript error list |* **Error content**: JavaScript errors aggregated by error type. Click to go to the JavaScript error details page.<br><br>* **Start and stop time**: The start and stop time of a JavaScript error.<br><br>* **error count**: The number of times a JavaScript error occurred. Hovering over the trend chart allows you to view the specific time when a JavaScript error occurred and the corresponding error count.<br><br>* **Impacted user count**: Number of users affected by JavaScript error. Hovering over the trend chart allows you to view the specific time when a JavaScript error impacted users, as well as the corresponding impacted user count.<br><br>* **Assignee**: Configure the assignee for this issue.<br><br>* **issue status**: The assignee adjusts the issue status according to the processing progress. Including **Unresolved**, **Being fixed**, **Fixed**, **Ignored**, and **Duplicate**. |
|page list |* **PID**: The ID of the page where a JavaScript error occurred.<br><br>* **error count**: The number of times a JavaScript error occurred. Hovering the mouse over the trend chart allows you to view the specific time when JavaScript errors occurred and the corresponding error count.<br><br>* **Impacted user count**: The number of users impacted by JavaScript errors. Hovering the mouse over the trend chart allows you to view the specific time when a JavaScript error impacted users, as well as the corresponding impacted user count. |
|Error message list |* **Error content**: Aggregated JavaScript error content.<br><br>* **error count**: The number of JavaScript errors that occurred. Hover the mouse over the trend chart to view the specific time when JavaScript errors occurred and the corresponding error count.<br><br>* **Impacted user count**: The user count impacted by JavaScript error. Hover over the trend chart to view the time point and impacted user count for each JavaScript error. |


<span id="826edc99"></span>
### JavaScript error details

<span id="66d9e3d8"></span>
#### Summary

The summary displays the JavaScript error type, JavaScript error file, JavaScript error content, issue owner, issue status, as well as the aggregated error count and impacted user count.

<span id="8f2819fa"></span>
#### Stack trace


* Original: Original code.

* minified: Code after packaging.

* Support version selection. 'unspecified' indicates that the version number is empty.

* Retry parsing: During data reporting, the platform will attempt to symbolicate the stack trace. If symbolication fails, click **Retry parsing** to have the platform attempt to symbolicate the stack trace again.

   Reverse mapping failure is usually caused by not uploading a sourcemap or by uploading an incorrect sourcemap. You can click the upload button to re\-upload a correct sourcemap file.

* in: Function name.

* line: Line number where the code is located.


<span id="437999be"></span>
#### Start and end information

The start and end time information displays the PID, time, and version release for both the earliest and latest JavaScript errors.

<span id="b4282669"></span>
#### Trends

The trends display trend charts for metrics for aggregated JavaScript errors, including error count, impacted user count, error rate, and affected user rate.

<span id="df479d7a"></span>
#### Version distribution

The version distribution displays the versions in which this type of aggregated JavaScript error occurs.

<span id="4eaa2259"></span>
#### Page layout

The page distribution displays the pages where this type of aggregated JavaScript error occurs.

<span id="9ab8f4d4"></span>
## sourcemap management

A SourceMap is an information file that stores the mapping between positions in the source code and the compiled code. It enables you to restore compressed, obfuscated, or merged production code to its original, unpackaged form, helping you accurately locate the line and column where issues occur in the production environment.

<span id="6202c150"></span>
### Manually upload sourcemap


1. Log in to [Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client).

2. Click **App Monitoring** under the target application.

3. In the upper left corner of the console, select **New H5 monitor \> sourcemap management**.

4. In the **sourcemap list** area, click **upload sourcemap**.

5. On the **Upload Sourcemap File** page, complete the following settings, then click **confirm**.

   Parameter description:

   
   |Parameter |DescriptionS |
   |---|---|
   |js source map filename |Custom sourcemap file name for representing this file. |
   |Upload sourcemap files |Click or drag files to upload. |
   |Release |Select or enter the corresponding version. |
   

6. After a successful upload, you can view the file in the **sourcemap list**.


<span id="eb9fc50e"></span>
## request overview

In the request overview, you can view trend charts and lists for all requests and error requests, helping you more quickly locate issues related to request errors and slow requests.

<span id="f042fc69"></span>
### All requests trend chart

In the overall request trend chart, the trends of request metrics based on the filter conditions are displayed. On the right side of the metric data, you can view the change in request data compared to the previous period.

Metric description:


|Metric |DescriptionS |
|---|---|
|request count |Request count under filter conditions |
|user count |Number of deduplicated devices under filter conditions |
|slow request count |Slow request count under filter conditions |
|slow request rate |slow request count under filter conditions / total request count under filter conditions |
|slow request affected user |Number of deduplicated devices for slow requests under filter conditions |
|slow request affected user rate |Number of unique devices with slow requests under filter conditions / number of unique devices with total requests under filter conditions |


<span id="4f581545"></span>
### Slow request list

By default, the slow request list displays the top 10 entries sorted by request count. You can view the response time and slow request status for each request URL. The slow request threshold is set to 3000 milliseconds by default. If you need to modify it, you can set the slow request threshold for the current site in **platform parameter configuration**.


* Slow request metrics: You can sort by the following slow request metrics: slow request rate, slow request count, average request time, 25th percentile of request time, 50th percentile of request time, 70th percentile of request time, 90th percentile of request time, and 99th percentile of request time.

* In the list, you can view the request path for slow requests, request time, slow request rate, data for the affected user rate metric, and trend charts.

* Request time: By default, view the average request time. You can also view the 25th, 50th, 70th, 90th, 95th, and 99th percentiles of request time.


<span id="e849f8b3"></span>
### Trend chart of error requests

The error request trend chart displays error request trends based on the filter criteria. On the right side of the metric, you can view changes in the number of error requests compared to the previous period.

Metric description:


|Metric |DescriptionS |
|---|---|
|request error |Number of requests with status code not 200 under filter conditions |
|error rate |Request count with status code not 200 under filter conditions / total request count under filter conditions |
|request error affected user |Number of unique devices for requests with a status code other than 200 under filter conditions |
|affected user rate |Number of deduplicated devices for requests with a status code other than 200 under filter conditions / total number of deduplicated devices for requests under filter conditions |


<span id="01e892e3"></span>
### List of error requests

The error request list allows you to view aggregated data for requests of the same type, including request path, exception status code distribution, error count, impacted user count, assignee, and issue status.

<span id="7f2c190a"></span>
## site performance overview

The performance monitoring page includes two main modules: PID aggregation and metric overview. These modules help you identify performance issues more quickly and serve as a basis for optimizing page performance.

<span id="82443d9b"></span>
### PID aggregations

<span id="d9805f93"></span>
#### Metric compliance rate

After setting the compliance rates for each performance metric for the current site in **platform parameter configuration**, you can view the number of PIDs that are currently compliant.

Compliance rate calculation method: number of PIDs meeting baseline requirements within the filter time / total number of PIDs.


* By default, the page displays FP compliance rate, FCP compliance rate, LCP compliance rate, FMP compliance rate, TTI compliance rate, and LOAD compliance rate.

* You can configure performance metric baselines for both default and custom performance metrics on the platform parameter configuration page.


<span id="6a9301b9"></span>
#### The page with the worst performance

By default, the worst\-performing pages are sorted by FCP using avg (average value), displaying the top 5 worst\-performing pages across the entire site. This helps you identify performance issues and optimize performance.


* avg: By default, sorting is based on avg (average value). Sorting by percentile values is also supported, including pct50, pct75, pct90, and pct95.

* FCP: Sorted by FCP by default; sorting by other metrics is also supported, including FP, FMP, TTI, LOAD, and LCP.

* The list shows the top 5 pages with the worst performance, selected from all pages on the site according to the filter criteria. If you sort by FP in ascending order, you can view, among the five pages with the worst performance, the one with the longest FP.

* On the worst performance page, data is aggregated using PID as the aggregation dimension, and the PID with the lowest performance for the selected metric under the current sample size threshold is displayed.

* Expand PID information, and you can view the trend charts for multiple performance metrics of this PID.

* Click the PID content to enter the **page details** and view the trend charts, distributions, and Bounce Rate status for each metric on the page.


<span id="1042e37c"></span>
#### Distribution of page load time intervals

The page time interval distribution allows you to view how the response times for the selected page metric are distributed.


* Drag the slider below to customize the display range for elapsed time. In the upper right corner, you can also view details about the reporting proportion within the specified time range.

* Hover over a bar to view the time range, report volume, and proportion for different segments.


<span id="74b9f095"></span>
#### Top 5 performance optimizations/degradations

The performance optimization and degradation page aggregates data by PID, allowing you to view information about the PID with the most severe performance optimization or degradation during the currently selected time period.


* In the trend chart, the currently selected range is split into two parts for comparison. For example, the current time range shown in the figure is two days, so the mean FP value on the demo page is 1,398 ms lower on the second day than on the first day.

* Click the corresponding PID, enter the **page details**, and view the performance overview of the page.


<span id="b87e4f27"></span>
### Metrics overview

The metric overview displays details of the default performance metrics under site\-wide filter conditions, including trend charts, distribution, and Bounce Rate, serving as a data basis for performance optimization. To modify the baseline of each metric, you can do so on the platform parameter configuration page. Display different performance metrics in different colors based on the baseline setting. Blue: meets expectations, yellow: slightly below expectations, red: significantly below expectations.

In the trend chart, the left side displays the relationship between the default metric for this PID and the baseline value under the filter criteria. The right side shows the trend of metrics within the filter criteria range.

In the duration distribution section, the left side displays the relationship between the default metric for this PID and the baseline value under the filter conditions. The right side shows the distribution of time consumption for the metric within the filtered time range.

In the Bounce Rate section, the left side displays the relationship between this PID's default metric and the baseline value with the applied filters. The right side shows the distribution of the duration metric within the selected time range.

Metric calculation method:


|**Metric** |**Calculation method** |
|---|---|
|FP Bounce Rate |Number of sessions that exited the page before FP reporting / total number of sessions |
|FCP Bounce Rate |Number of sessions that bounced before FCP was reported / total number of sessions |
|LCP Bounce Rate |Number of sessions that exited the page before LCP reporting / total number of sessions |
|FMP bounce rate |Number of sessions that exited the page before FMP reporting / total number of sessions |
|CLS bounce rate |Number of sessions that exited the page before CLS reporting / total number of sessions |
|LOAD bounce rate |Number of sessions that exited the page before LOAD reporting / total number of sessions |
|TTI bounce rate |Number of sessions that exited the page before TTI reporting / total number of sessions |


<span id="340eb507"></span>
## page list

The page list provides page error, performance, request, and other data organized by page, enabling targeted analysis based on the data for specific pages.

<span id="00dcf974"></span>
### Data overview

The data overview allows you to view the total number of pages for the current site, the page with the highest number of visits, the page with the highest JavaScript error count, and the page with the worst FP performance.


* Page with the highest JavaScript error count: Click the URL to navigate to the JavaScript error details page and view the JavaScript error trend chart and error list.

* Page with the worst FP performance: Click the URL to go to the **performance overview** page, where you can view the trend chart, distribution, and bounce rate for page metrics.


<span id="2f7147b7"></span>
### page list

The page list displays specific data at the page level.


* PID: Click PID to go to the page details, where you can view the JavaScript error trend chart and error list.

* Click the checkbox to pin this page to the top.

* Supports keyword search and custom columns. The metric categories included in custom columns are as follows: user analysis, JavaScript error, performance, and request data.

* Download: Supports downloading up to the first 1,000 entries, displaying the data from the list in `.xlsx` file format.
