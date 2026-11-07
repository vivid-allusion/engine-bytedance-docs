---
title: "Dashboard"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-playback-quality"
---

The Dashboard leverages data from the BytePlus VOD Player and Upload SDKs to provide metrics and multi\-dimensional analysis for video playback, external subtitles, and uploads. This guide explains how to use the Dashboard's modules to monitor service quality, analyze user experience, and assess business costs.

This document introduces the modules of the Dashboard and provides detailed instructions on how to use them.

<span id="c6f85c30"></span>
## Feature overview

The Dashboard includes the following core analysis modules, covering key stages of the video service lifecycle:


|**Data category** |**Module** |**Description** |**Key metrics** |
|---|---|---|---|
|**Playback data** |Overview |Provides a real\-time dashboard to monitor core playback metrics and help you quickly identify abnormal fluctuations. |Aggregated playback QoS, QoE, and cost metrics. |
||Play QoS |Monitors Quality of Service (QoS) to reflect the performance of the Player SDK. |Play Count, Actual Play Count, Play Failure Rate, Time to First Frame, Stall Rate, Interruption Rate, Start Failure Rate, Stalling Duration per 100s, Stalling Count per 100s, Average Bitrate, Average Seek Time. |
||Play QoE |Provides insights into the Quality of Experience (QoE), reflecting the actual viewing experience of end\-users. |Completion Count, Unique Viewers, Avg. Play Duration per User, Avg. Plays per User, Avg. Completions per User, Completion Rate, Avg. Play Duration, Avg. Video Duration. |
||External subtitles |Monitors the loading performance and success rate of external subtitles to ensure feature stability. |Plays with subtitles enabled, subtitle display failure rate, subtitle load time, subtitle cache hit rate |
||Cost metrics |Analyzes traffic and bandwidth consumption from a client\-side perspective to support cost optimization decisions. |Player Bandwidth Consumption, Player Traffic Consumption. |
|**Upload data** |Upload |Monitors the success rate and efficiency of upload tasks based on core metrics reported by the Upload SDK. |Includes key metrics such as Total Uploads, Upload Failure Rate, Average Upload Speed, Average Upload Time, and Average File Size. |


For detailed descriptions of each metric, see [Metrics and dimensions ](https://docs.byteplus.com/docs/byteplus-vod/docs-dimensions-and-metrics).

<span id="f15c2407"></span>
## Viewing and analyzing playback data

<span id="caf7750f"></span>
### Getting a quick overview of playback data


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. In the left navigation pane, click **Quality insights** \> **Dashboard**. You will be directed to the **Overview** tab by default.

3. Configure the data filter as prompted on the page.

   
   |**Filter** |**Description** |
   |---|---|
   |App name |Enter the name of the app you want to query or select it from the drop\-down list. |
   |Client type |Select the client type from the drop\-down list:<br><br><br>* Mobile<br><br>* Web |
   |Operating system |Select the operating system from the drop\-down list. The relationship between client type and operating system is as follows:<br><br><br>* **Mobile**: Includes Android, iOS, and Harmony.<br><br>* **Web**: Includes Android, iOS, Linux, Mac, and Windows. |
   |Metrics |Select the metrics you want to view in the Overview. For the metric description, see [Metrics](https://docs.byteplus.com/docs/byteplus-vod/docs-dimensions-and-metrics#dbce7eb2). |
   |Time range |Set the time range for your query.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Only data for the past 365 days is available.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Each query can cover a maximum of 93 days.</div><br> |
   |Time granularity |Set the time granularity for your query. The available options for time granularity vary depending on the timeframe of your query.<br><br><br>* If your query covers a timeframe of less than one day, you can choose between time granularity options of 5 minutes, 1 hour, and 1 day.<br><br>* If your query covers a timeframe between 2 and 7 days, you can select either 1 hour or 1 day as the time granularity.<br><br>* For queries that span more than 7 days, the only available time granularity option is 1 day. |
   

4. Click **Query**. The data appears in a few minutes. The **Overview** tab supports period\-over\-period comparisons, with results displayed in different colors based on the metric type.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f085d83138764dd3ab3108ce5d42cd67~tplv-goo7wpa0wc-image.image) </span>


<span id="24b7ca30"></span>
### Performing an in\-depth analysis of playback data

To conduct a detailed analysis of specific playback metrics, switch to the **Play QoS**, **Play QoE**, or **Cost metrics** tabs. Here, you can use dimensional analysis and filtering to pinpoint issues.


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. In the left navigation pane, click **Quality insights** \> **Dashboard**.

3. Switch to the **Play QoS**, **Play QoE**, or **Cost metrics** tab.

4. Choose an analysis mode:

   * **Breakdown by dimension**: Select 1\-3 dimensions (such as business tag, operating system, app version) to break down the data and understand how different factors impact the metrics. For a full list of supported dimensions, see [Dimensions](https://docs.byteplus.com/docs/byteplus-vod/docs-dimensions-and-metrics#61a5815c).

   * **Filter mode**: Apply pre\-configured filters to display only the data that meets specific criteria for more precise analysis. You can apply up to 3 filters simultaneously. For instructions on configuring filters, see [Adding a filter](https://docs.byteplus.com/docs/byteplus-vod/docs-settings#c5ed699c).

5. Configure the query filters. The available filters are similar to those in the **Overview** tab.

6. Click **Query**. The system will display detailed data for the selected metrics in a few minutes.

7. Within an individual metric card, you can perform the following operations:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cca549aa87894b2a80ab035cf3defd25~tplv-goo7wpa0wc-image.image) </span>

   
   |**No.**  |**Action** |
   |---|---|
   |1 |Switch between line charts and bar charts. |
   |2 |Export chart data as a CSV file for offline analysis. |
   |3 |Refresh an individual chart. This is useful if a chart fails to load. |
   |4 |Enlarge a chart to set more specific query conditions for a single metric. |
   |5 |Filter the data by setting a comparison operator (greater than or less than) and a value. |
   |6 |Use the Top N feature to filter and display only the most significant data series when there are too many dimensions. |
   |7 |Apply additional dimensions to the specific metric. |
   


<span id="7f45c4b9"></span>
### Viewing external subtitle data

The **External subtitle** tab helps you monitor the loading performance and usage of subtitles, allowing you to assess the stability and user experience of the feature.


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. In the left navigation pane, click **Quality insights** \> **Dashboard**.

3. Switch to the **External subtitle** tab.

4. Select an analysis mode and configure the filters. The filters and multi\-dimensional analysis capabilities are consistent with the Play QoS dashboard. For details, see [Performing an in-depth analysis of playback data](https://docs.byteplus.com/docs/byteplus-vod/docs-playback-quality#24b7ca30).

5. Click **Query** to view the detailed metric data.


<span id="c1ee3ae2"></span>
## Viewing and analyzing upload data

The **Upload** tab provides multi\-dimensional statistics based on core metrics reported by the Upload SDK. You can use custom filters to obtain quality data under specific conditions.


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. In the left navigation pane, click **Quality insights** \> **Dashboard**.

3. Switch to the **Upload** tab.

4. Configure the data filter. The page supports the following filters.

   
   |**Filter** |**Description** |
   |---|---|
   |App name |Select your app name from the drop\-down list. |
   |Client type |Select the client type from the drop\-down list:<br><br><br>* Mobile<br><br>* Desktop |
   |Upload SDK version |If you select Mobile as the client type, you can specify the Upload SDK version as one of the following options:<br><br><br>* The Upload SDK version < 3.x<br><br>* The Upload SDK version ≥ 3.x |
   |Time range |Set the time range for your query. By default, the chart shows the most recent 24 hours of metrics data.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Each query can cover a maximum of 90 days.</div><br> |
   |Time granularity |Set the time granularity for your query. The available options for time granularity vary depending on the timeframe of your query.<br><br><br>* If your query covers a timeframe of less than one day, you can choose between time granularity options of 5 minutes, 1 hour, and 1 day.<br><br>* If your query covers a timeframe between 2 and 7 days, you can select either 1 hour or 1 day as the time granularity.<br><br>* For queries that span more than 7 days, the only available time granularity option is 1 day. |
   |Operating system |Select the appropriate operating system from the drop\-down list according to the client type:<br><br><br>* If you select **Mobile** as the client type, the options are Android or iOS.<br><br>* If you select **Web** as the client type, the options are Android, iOS, Linux, Mac, and Windows. |
   |More dimensions |* If you select **Mobile** as the client type, the supported filters include **Network**, **App version**, **Operator**, and **Province**.<br><br>* If you select **Web** as the client type, the supported filters include **Province**, **Operator**, and **Browser**. |
   

5. Click **Query**. The data appears in a few minutes.
