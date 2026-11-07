---
title: "Analysis and diagnosis"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-diagnostic"
---

When you notice anomalies in your QoS metrics in the dashboard, the **Analysis and diagnosis** feature enables you to perform a deep\-dive analysis to identify the root cause. By breaking down data across multiple dimensions, you can pinpoint the factors contributing to playback issues and resolve them effectively. This article explains how to use this feature for root cause identification.

<span id="9a1df73e"></span>
## Feature overview


* **Deep multi\-metric diagnosis**: Supports in\-depth analysis of core QoS metrics, including unsuccessful playback rate, time to first frame, video freezing rate, no playback rate, and many others.

* **Global dimension breakdown**: Supports breaking down the main trend chart by core dimensions (such as business tag) to quickly detect high\-level differences.

* **Multi\-dimensional drill\-down**: Supports manually selecting up to 3 dimensions (such as operating system, business tag and App version) to break down the metric and use cross\-analysis to locate the specific user group or scenario causing the problem.

* **Assisted attribution**: Provides assisted charts based on the selected metric, such as metric distribution charts and top 10 error codes, to help you locate the root cause.


<span id="998accf7"></span>
## Procedures


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **Quality insights** \> **Analysis and Diagnosis** in the left navigation bar.

3. Define the analysis cycle and locate the issue via the metric trend chart.

   1. **Set query conditions**: In the **Locate abnormal data** area:

      * **Basic filters**: Set filters based on the analysis goal.

      * **Dashboard metric**: Select the metric you want to investigate. It supports the following core QoS metrics:

         * Time to first frame

         * Unsuccessful playback rate

         * Video freezing rate

         * Video freezing duration within 100 seconds

         * Video freezing count within 100 seconds

         * Average playback bitrate

         * Interruption rate

         * No playback rate

         * Average seek time

      * **Global breakdown dimension**: Select one dimension to split the metric trend chart. This helps you quickly compare data differences between groups.

   2. **Analyze high\-level trends**: Observe the metric trend chart to understand the overall performance. Different curves represent different splitting dimensions. The example below shows the unsuccessful playback rate trend split by app version.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/537c564f95c34f56806c843179775047~tplv-goo7wpa0wc-image.image) </span>

4. In the **Split dimensional analysis**, select dimensions for root cause analysis:

   1. **Select splitting dimensions**: Select up to 3 dimensions from the dropdown. The system generates a separate in\-depth drill\-down analysis table for each dimension selected.

   2. **Analyze data and locate root cause**: Use the data tables to compare metric performance across different dimension values, quickly identifying the key factors for the anomaly.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e6772a868514270b9deb958f65a70c7~tplv-goo7wpa0wc-image.image) </span>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The platform also offers an <strong>AI</strong> \*\*analysis and diagnosis \*\*tool. Simply specify the date you want to investigate, and the system does the rest. It intelligently selects a normal performance baseline for comparison and automatically pinpoints the key dimensions and likely causes behind the data anomaly.</div>



5. After key dimensions are identified, the system provides corresponding assisted charts based on your selected metric for a more detailed analysis.

   * Metric value distribution: For metrics, such as time to first frame, video freezing duration within 100 seconds, average playback bitrate, and average seek time, the system uses bar charts to visualize the distribution of video views across value ranges. For example, in the time to first frame distribution chart below:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92d6c02cc1a448cfa8776af9fc466fd5~tplv-goo7wpa0wc-image.image) </span>

      The X\-axis shows the first\-frame time range, and the Y\-axis shows the video views in that range.

   * Top 10 Error Codes: When analyzing unsuccessful playback rate, the system lists the top 10 error codes under current filters, showing the affected playback volume and percentage. This provides clear technical troubleshooting guidance.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7931a3f4b55147fb9c31428911672648~tplv-goo7wpa0wc-image.image) </span>
