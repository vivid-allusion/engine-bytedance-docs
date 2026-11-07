---
title: "Lag analysis"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Lag_analysis"
---

The Application Performance Monitoring Full\-Link Edition provides a lag analysis feature, supporting monitoring of whether main thread messages time out. This can effectively help you analyze smoothness issues during app usage.

Lag analysis provides four analytical views—lag trend, lag distribution, lag list, and lag details—enabling you to more comprehensively analyze different types of lag in your application.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**


* Lag analysis has already been integrated. For details, refer to [Android SDK integration](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_Android_SDK_into_the_application) or [iOS SDK integration](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_iOS_SDK_app).

* The master switch for SDK reporting configuration has been turned on, and the sampling rate configuration for lag analysis has been completed. For details, refer to [SDK reporting configuration](https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration).

   The default threshold for lag is 2.5 seconds, and the default threshold for severe lag is 4 seconds. Supports custom thresholds.


<span id="b43fde3e"></span>
## Filter conditions

You can filter data using the following filter criteria:


* Filter dimensions supported by the Android system:

   Time, lag details, device ID, user ID, issue creation status, foreground and background, system version, device model, app version, app minor version number, APM SDK version, download channel, ROM information, province, usage duration, process name, manufacturer, lag type, parsing status, app page, issue status, assignee, tags, custom dimension, PV custom dimension.

* Filter dimensions supported by the iOS system:

   Time, stutter details, device ID, User ID, issue creation status, scroll stutter, foreground and background, jailbreak status, system version, device model, app version, app minor version, APM SDK version, download channel, province, usage duration, parsing status, app page, issue status, assignee, tags, custom dimension, PV custom dimension.


<span id=".5Y2h6aG_6LaL5Yq_"></span>
## **Lag trend**

The stutter trend chart displays the trend of stutter metrics based on the filter conditions. You can also display the trend chart according to grouping dimensions. You can view changes in crash data compared to the previous period on the right side of the metric data.

Indicator descriptions


|**Metric** |**DescriptionS** |
|---|---|
|Lag count |Number of stutters under filter conditions |
|Lag rate |Number of stutters under the filter conditions / total number of launches under the filter conditions |
|Number of users experiencing lag |Number of deduplicated unique visitors that experienced stalls under filter conditions |
|Proportion of users experiencing lag |Number of deduplicated unique visitors who experienced lag under filter conditions / total number of deduplicated unique visitors under filter conditions |


<span id=".5Y2h6aG_5YiG5biD"></span>
## Stutter distribution

The stutter distribution shows how stutter data is distributed across various dimensions.


* The platform displays the following four distribution dimensions by default: **system version**, **APP version**, **APP minor version number**, and **device model**.

* Settings: Click the settings button in the upper right corner to customize distribution dimensions. You can select up to four dimensions.

* **Reported volume**: The platform displays the distribution based on reported volume data by default. You can switch to **user count** to view the distribution of stuttering.


<span id=".5Y2h6aG_5YiX6KGo"></span>
## Lag list

The platform will aggregate similar instances of lag into a single issue. By reviewing the information in the list, you can get an overview of the ranking of each issue and key metrics. Additionally, you can assign a handler to the issue.


* The lag list displays the lag description, number of affected users, number of lag occurrences, lag duration, most recent occurrence time, status, and assignee.

* Download: Click the download button in the upper right corner to download the first 100 entries of the lag list as an .xlsx file.

* Settings: Click the settings button in the upper right corner to configure which columns' data are displayed in the lag list.

* Note: Click an issue title to view the trends, distribution, details, stack, and more for this type of issue on the issue details page. By using dimension information, stutter trend charts, and the detailed data of each stutter event, it is possible to analyze and identify potential causes of stuttering.


<span id=".5Y2h6aG_6K-m5oOF"></span>
## Lag details

<span id=".5Z-65pys5L-h5oGv"></span>
### Basic information

The basic information section displays the name of this type of lag, the most recent reporting time, the most recent occurrence time, the first occurrence time, status, and assignee. It also highlights the lag description, number of lag occurrences, number of users who experienced lag, lag rate, and the ratio of users who experienced lag.

<span id=".5Y2h6aG_6LaL5Yq_"></span>
### Stuttering trend

The stutter trend section displays the trend of this type of stutter under the filter conditions.


* By default, the trend chart displays the trend for **stutter count**. You can switch to the trend chart for **affected user count**.

* Grouping: By default, items are displayed without grouping. You can view trend charts grouped by dimensions such as app version, app minor version, foreground or background status, system version, device model, and more.

* Click the download button to download the trend chart. You can then view the stutter trend chart in `.png` file format.


<span id=".5Y2h6aG_5YiG5biD"></span>
### Stutter distribution

The stutter distribution displays how this type of stutter is distributed under the current filter criteria.


* The platform displays the following four dimensions by default: **system version**, **device model**, **app version**, and **app minor version number**.

* Settings: Click the settings button in the upper right corner to customize the distribution dimensions. You can select up to four dimensions.

* By default, the platform displays the distribution based on **number of reports** data. You can switch to **number of users** to view the distribution of stuttering.


<span id=".6K-m57uG5L-h5oGv"></span>
### Detailed information

On the details page, you can view the specific information at the time the issue occurred.


* Switch: Click the upper right corner to switch between different issues. View detailed information about these similar issues when lag occurs to help analyze and identify possible causes of the lag.

* Download: Click the download button to download the log file, then view the issue details in the log information displayed in the `.txt` file format.


<span id=".5Y6f5aeL5aCG5qCIJlJldHJhY2U="></span>
### Original stack & retrace


* Click to expand the call stack. You can then expand to view information about the main thread stack.

* Click **Copy Stack** to copy the stack information displayed on the page.

* In the search stack text box, you can use keywords to search and locate within the stack.


<span id=".5Y2h6aG_5L-h5oGv"></span>
### Stutter details

In the lag information, you can view metrics related to lag and their values.

<span id=".56ym5Y-36KGo"></span>
### Symbol table

In the symbol table, you can upload a symbol table. After uploading, you can view the stack parsed using the symbol table on the Retrace page.

<span id=".546w5Zy65pWw5o2u"></span>
### Field data

You can view page information, custom data, and page tracking in live data.

<span id=".5Y2h6aG_5o6S6KGM"></span>
## Lag rankings

The stuttering ranking list displays the ranking of stuttering data based on the filter conditions.

<span id="3343e148"></span>
### Filter criteria

Time supports selecting today, yesterday, recent (1 day, 7 days, 30 days), or a range (the range cannot exceed 30 days). Supports filtering by system, system version, APP version, SDK version, APM SDK version, and APP ID.

If you frequently need to view data with certain filter criteria, you can save these filter criteria and quickly apply them in the frequently used section later.

<span id="4ff00ba9"></span>
### Detailed data

The detailed data displays ranking, APP name, APP ID, APP version, SDK version, most recent occurrence time, number of freezes, freeze rate, number of affected users, and percentage of affected users.

In addition to APP name, APP ID, and APP version, you can sort by any of the above columns to investigate factors contributing to lag.

You can click the download button to view the ranking of lag data presented in `.xlsx` file format.

<span id=".5Y2h6aG_5pWw"></span>
## Lag tree

A stutter tree aggregates the main thread stack, with each node representing a method. It is used to analyze, from a high\-level perspective, where the lag is most severe. It also supports assigning weights to nodes for more accurate analysis.

If, over a period of time, there are a large number of lag reports, or if lag is abnormally concentrated on a particular device model or version, you can use the lag tree to perform aggregate analysis and identify the method nodes that may be causing significant lag.

<span id=".5a6e5pe25p-l55yL"></span>
### Real\-time view

The real\-time view can only provide a rough analysis to determine whether there may currently be nodes that cause lag. If you want to analyze the flame graph of the lag tree directly on the platform, you can select the real\-time view.

In the flame graph, the number after each node indicates how many times it appears in the entire lag stack. If the same library appears consecutively, the same color will be used.


* Supports searching in the search box by instance name and instance ID.

* Support filtering nodes by **minimum proportion**. If the proportion of stutter occurrences for a node is less than the selected value, it will be filtered out.

* Click **Highlight non\-system nodes** to emphasize non\-system nodes and view their lagging status.

* Click **Hide system nodes** to hide system nodes from the diagram and view stalling issues for non\-system nodes.


<span id=".56a757q_5p-l55yL"></span>
### View offline

Offline view enables targeted analysis of stutter tree information for a specific version or a certain period, and the data volume is large. Because the process takes a long time, an email will be sent to the operator after the calculation is completed successfully.

If the time range exceeds 12 hours and the minimum proportion is less than 1 percent, prioritize using offline queries.


* In the offline list view, you can view the creation time, task status, time range, minimum percentage, filter criteria, and creator.

* In the search box, you can query offline tasks based on the creator's account.

* **Create an offline task**: Click to set the time range, filter criteria, keywords, minimum proportion, and other information for the offline task.
