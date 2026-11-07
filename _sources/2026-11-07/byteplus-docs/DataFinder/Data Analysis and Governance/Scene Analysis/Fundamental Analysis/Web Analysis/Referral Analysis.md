---
title: "Referral Analysis"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Referral_Analysis"
---

"Referral Analysis" shows you the basic situation of visitors, including the number of visitors, new/old visitors, source type, source URL, etc. You can use this module to gain a basic understanding of the composition of visitors to your website.

<span id="_1-概述"></span>
# Precautions


* The analysis module will only appear after accessing the web/JavaScript data.

* At present, DataFinder has upgraded the interface function of the referral analysis module. This article introduces the operation points of the new version of referral analysis.


<span id="_2-指标配置"></span>
# Configuration metrics

In the "Referral Analysis" module, we can configure metrics, dimensions, etc. through the sections at the top of the page. As shown below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da797628bd454e4eabad5ca94307f6c8~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-1-时间范围选择"></span>
## Configure time range

Select the time range from the drop\-down menu.


* Support "Every 5 Minutes", "Hourly", "Dayly, "Weekly", "Monthly" data;

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef1f16ea8b0247ae94d6c78219ce95f7~tplv-goo7wpa0wc-image.image) </span>

* You can add a comparison time:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/47a71c2603e1497ca8caa271339a3d07~tplv-goo7wpa0wc-image.image) </span>

   * You can set a time interval to compare with the target time indicator.

   * You can select the start and end points of the comparison period interval in the icon area. By default, the comparison period interval is the same length as the original focus period.

* The time range that can be queried with different time granularity supports is inconsistent. If the time range requirements are not met, DataFinder will automatically adjust the time range of the query result data for you.


<span id="_2-2-指标选择"></span>
## Configure devices and users

Select the device type and user type for referral analysis according to the interface prompts.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ead5eaab41545debf23eb1d11a91a17~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-维度选择"></span>
## Configure grouping dimension

Configure the grouping dimension according to the interface prompts.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ddb1c47ea65542f8a8fb991ff5e9c3aa~tplv-goo7wpa0wc-image.image) </span>

<span id="2c5211a9"></span>
## Configure Segmentation Filtering

Support adding multiple filter conditions. The logical relationship between filter conditions is "AND". You can click the Batch Enter button to enter batches.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bc04fbaa24ef4353b4c7913f250282be~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-图表展示"></span>
# View the result chart

<span id="b648394b"></span>
## Result graph

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d96bf430381c4d5cac35452d6b966dee~tplv-goo7wpa0wc-image.image) </span>


* The chart is the cumulative value (top value), proportion data (pie chart on the left), and change trend (line chart on the right) of each indicator within the range configured above;

* The metrics supported by "Referral Analysis" include:

   * Number of visitors: unique visitors to your website in the selected time frame (based on cookies), deduplicated by user identity;

   * Number of sessions: The number of sessions on your website within the selected time frame.

   * Average session duration: the ratio of the total duration of all sessions to the total number of sessions in the selected time range.

   * Average session depth: the ratio of the sum of the session depths of all sessions to the total number of sessions in the selected time frame.

   * Bounce rate: the percentage of sessions that left the site after only one page was viewed;

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Related terms and concepts:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Conversation: Conversation is a series of behaviors that users engage in while continuously active on a website. By default, two page browsing events or two any page interaction events are more than <strong>30 minutes</strong> apart, and the latter is included in the new session. On the contrary, if you close the browser or stop the operation, but continue to access within 30 minutes, you will still be included in the same session. Under normal circumstances, we do not recommend that you modify the default duration, but if you need it, you can also modify the default configuration in "Session Management", which is located in "Session Management" of "Data Management". It is important to note that the session\-related metrics will only change after modifying the configuration here.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Session depth: The number of page access events contained in a session.   </div>
   

* When you configure the grouping dimension as "Source Sites", the top 20 source sites are displayed in the chart by default.


<span id="_4-表格展示"></span>
## Detailed result data

<span id="_4-1-来源类型"></span>
### Source type


* When the dimension you are focusing on is "Source Type", the data displayed is as follows:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/18fc368fa8b84c1ba7c50931518f10ed~tplv-goo7wpa0wc-image.image) </span>

* Source type grouping:

   * Grouping values include: in\-app jump, direct access, external links, and search engines.

   * After the "+" sign is expanded, the specific search engine name and external link URL under the group are presented.

* The data in the table supports download.


<span id="_4-2-来源网站"></span>
### Source sites

When the dimension you are focusing on is "source sites", the TOP20 source website data is displayed, as shown below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/09d75da25a6c4e9fac87053fa9555f3e~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-3-对比时间"></span>
# View the results chart: Comparative analysis

If you have configured a comparison time above, the query chart shows you the comparison data for the current time range and the comparison time range.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8d076e06e8524176a421480c5590479d~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cb22e46dce2740e59eab9f6684fd0c7f~tplv-goo7wpa0wc-image.image) </span>


* Each group in the table presents three parts of data: current time period data, comparative time period data, and rate of change.

* Rate of change value = | current time period value/comparison time period value \-1 | \* 100%.
