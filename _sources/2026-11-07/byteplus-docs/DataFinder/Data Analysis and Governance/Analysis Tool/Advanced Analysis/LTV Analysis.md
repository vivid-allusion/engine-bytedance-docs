---
title: "LTV Analysis"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/LTV_Analysis"
---

LTV (Life Time Value) analysis refers to the process of quantifying and analyzing the total value created by customers for the company throughout its life cycle. It is an important reference indicator for whether products can achieve high profits. It is widely used in marketing, Customer relationship management and financial planning. DataFinder provides you with LTV analysis tools. This article introduces the computational logic and configuration essentials of DataFinder's LTV analysis.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">DataFinder's LTV analysis function currently only supports the calculation and analysis of real revenue data, and does not support the prediction and analysis of future revenue value for the time being.</div>


<span id="_1-功能简介"></span>
# Computational logic

It can be seen from the above introduction that the main analysis focus of LTV analysis is on the revenue value effect of new users. DataFinder's LTV analysis tool supports configuration analysis of revenue event scenarios including revenue from **ordinary events** and revenue from **advertising events**.

As shown in the figure below, when configuring revenue events for LTV analytics, you can choose **internal purchase event metrics** or **ad event metrics**. The configuration interface examples and calculation formulas for the two types of indicators are as follows.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c5191aa616754090af44379d9bbe44f0~tplv-goo7wpa0wc-image.image) </span>


|LTV calculation formula |
|---|
|[ **Internal purchase event indicator** ]: Assuming that the per capita LTV on a certain day is LTVn, the calculation formula is:<br><br>```Plain```<br>```LTVn = The total revenue from purchasing events of newly added users in the following n days on the same day / Number of new users added on the same day```<br>```     = Sum up the amount of expenses incurred by the newly added user in the following n days on the same day / Number of new users added on the same day```<br> |
|[ **Advertising Event Indicator** ]: Assuming that the per capita LTV on a certain day is LTVn, the calculation formula is:<br><br>```Plain```<br>```LTVn = The total revenue from advertising events in the following n days for newly added users on the same day / Number of new users added on the same day```<br>```     = The number of ad clicks for new users added on the same day in the following n days*(daily ecpm/1000)Sum up accumulation/Number of new users added on the same day```<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><strong>ECPM</strong> , short for "effective cost per mille" (mille is Latin for thousand), is one of the most important Key Performance Indicators in digital advertising, showing profit margins for certain ad slots, apps, websites, and other dimensions.</div><br> |


From the above calculation formula, it can be seen that to understand the calculation results of two types of event indicators, the key data lies in the following concepts:


|Key concepts |Detailed description |
|---|---|
|**New users on the day** |In DataFinder's LTV analysis, the number of new users on a given day is counted by counting the user uids that triggered the " **starting event** " on a given day. |
|**The sum** of the **amount spent over the next n days** |In DataFinder's LTV analysis, the properties of the statistically configured internal purchase events are summed:<br><br><br>* Statistical user range: All new users added on a given day.<br><br>* Revenue calculation: From the day the user first triggers the " **starting event** ", to the subsequent nth day, the internal purchase event attributes of each day are summed cumulatively. |
|**Number** of **ad clicks in subsequent n days** |In DataFinder's LTV analysis, the number of ad clicks is calculated by statistically configuring the number of revenue events \- the number of events (PV) for ad events.<br><br><br>* Statistical user range: All new users added on a given day.<br><br>* Revenue calculation: the sum of the **number of ad clicks** \* ( **daily ecpm/1000** ) for each day from the day the user first triggers the " **starting event** " to the subsequent nth day. |


The following configuration example will provide you with a detailed description of the configuration operation and calculation logic of LTV analysis.

<span id="_2-使用说明"></span>
# Operation steps

<span id="_2-1-顶部配置区说明"></span>
## Step1: Configure metrics and global filters


1. Configure **Initial Events** and **Revenue Events** in the **Configuration Metrics** area to calculate the sum of new users and revenue for subsequent LTV analysis. Configuration instructions and examples are as follows.


<div style="text-align: center">
<strong>(1) schematic diagram of internal purchase event indicator configuration</strong></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d2e22c8dbf1d42fd8a94f8844aef53fa~tplv-goo7wpa0wc-image.image" width="1076px" /></div>


<div style="text-align: center">
<strong>(2) Schematic diagram of advertising event indicator configuration</strong></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e52f6c709db1468e87d8558bb34f0d43~tplv-goo7wpa0wc-image.image" width="1052px" /></div>



|Parameter |Internal purchase event indicator configuration instructions |Ad Event Metrics Configuration Instructions |
|---|---|---|
|**Initiating event** |We use the starting event to delineate the target population.<br><br><br>* After configuring the start event, the number of user UIDs that triggered the start event will be counted as the number of new users to be analyzed.<br><br>* You can click the Filter Criteria button to filter the subsequent statistics of users by their properties.<br><br><br>As shown in the figure above, the subsequent calculation will count the user uids that have triggered the "clickhouse_query" event every day and the "query_type" is not empty, and the number of users will be the " **number of new users on that day** " in the subsequent calculation formula. ||
|**Revenue event** |Calculate the amount of revenue by revenue events and attributes:<br><br><br>* You can click " **+ LTV Metrics**" to add multiple event metrics as revenue events, and participate in subsequent revenue data calculation. Up to 10 are supported.<br><br>* Includes "**internal purchase event metrics**" and "**advertising event metrics**". The configuration details of the two types of revenue events are different, as detailed below.<br><br>* Support configuring filter conditions for each revenue event, and filter the revenue events calculated by subsequent statistics through attributes. ||
||"**Internal purchase event indicator**" configuration guide:<br><br><br>* Select revenue events and attributes, and then add up the configured event attributes as revenue effect data.<br><br>* Support the configuration of profit ratio, up to 3 decimal places. After configuration, the cumulative sum of attributes will be multiplied by the profit ratio in the calculation of revenue effect data as the final revenue effect data.<br><br><br>As shown in the figure above, in subsequent calculations, the "time_cost" attribute of each new user's "clickhouse_query" event is summed and multiplied by the profit ratio of 100% as the revenue data of these new users. |"**Ad Event Metrics**" configuration guide:<br><br><br>* Select the ad event and upload the ad eCPM file as required by the eCPM document template.<br><br>* The eCPM file template can be downloaded in the upload interface, and the date and corresponding eCPM value need to be filled in according to the template requirements, which is convenient for subsequent Computational Advertising revenue effect data.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ce84e50cd514297be4bf334c790043f~tplv-goo7wpa0wc-image.image) </span> |



2. Configure segmentation filtering.

   Comprehensive use of segmentation screening capabilities, can achieve more complex crowd segmentation and filtering screening, the scene can refer to " [In-Text Grouping (Segmentation Filtering)](https://docs.byteplus.com/docs/DataFinder/In-Text_Grouping_Segmentation_Filtering)", the ability of privatization 4.4 version after support, saas after April 1, 23 support.

   By configuring segmentation filtering, users to be analyzed can be filtered based on the following criteria or a combination of multiple criteria:

   * By user group: Select "By user group" as the filter criterion and specify the user group to filter.

   * According to public attributes: Select public attributes (such as operating system, software version, etc.) as the filter criteria, and refine the filter criteria.

   * You can select and set multiple conditions simultaneously, and the relationship between these conditions is "and", that is, to filter users who meet these conditions at the same time.

3. Configuration control group: establish a comparison, compare the LTV situation of different populations.

4. Configure property grouping.

   1. Click "+ Properties Grouping" and select event properties, user properties, etc. for grouping in the drop\-down box.

      After configuring attribute grouping, the result chart of subsequent query analysis will be grouped and displayed according to the dimension of each attribute value configured, which is convenient for more refined analysis.

      For example, when analyzing the differences in LTVn data between different system versions of an app, you can group the display by the attribute "system version".

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Attribute grouping supports grouping by event attributes, user attributes, user labels, etc. A total of up to 20 layers of grouping are supported.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Selecting revenue event related attributes for grouping attributes of query analysis results is not currently supported.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">After setting the attribute grouping, in the subsequent data query chart, if a group has multiple values, for example, there are iOS and android two attribute groupings after grouping according to the "system platform" attribute, when a user uses ios and android at the same time After reporting the revenue event, in the query results of LTV, the data results of the two groupings will respectively count the data of the user in the corresponding attribute (that is, ios and android will be counted, and in the scenario without grouping, a user will only be counted once).      </div>
      

   2. You can set the query chart to display the top xx grouped query results by the current query condition.

      When there are too many values of the grouped attributes, in order to avoid the fact that too many groupings displayed in the chart make it impossible to perform data analytics efficiently, DataFinder will sort the grouped result attributes, and by default only the grouped result data configured here is displayed in the query result chart.

      See more detail about attribute grouping [Property (Custom) Grouping and Properties](https://docs.byteplus.com/docs/DataFinder/Property_Custom_Grouping_and_Properties).


<span id="_2-2-ltv指标说明"></span>
## Step2: Configure and view analysis charts


1. You can configure the time range and chart presentation type for LTV analysis in the upper left.

2. After completion, you can view the corresponding LTV analysis chart and detailed daily calculation data.

   * LTV analysis chart: The graph presents the last 7 days of data by default. You can switch between LTV trends or LTV comparisons.

      * Under LTV Trends, you can view all people or people on a given day, from LTV1 to LTVn indicator trends;

      * In the LTV comparison, you can view the client base on different days, the data performance on a certain LTVn indicator;

      * True value calculations include LTV1\-10, LTV14, LTV30, LTV60, and LTV to date.

      * Summary LTVn = all internal purchase events LTVn + all advertising events LTVn. The indicator is displayed in the chart area by default.

   * LTV analysis table: The table is presented as a pyramid, the first column is the date, the second column is the number of new users, and the first row header mainly represents the value from LTV0 to LTVn.


<span id="40a0ca64"></span>
# Calculation and analysis examples

<span id="098d4499"></span>
### Internal purchase events

<div style="text-align: center">
LTV Analysis Chart</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e10b8807c5ed4034a4e11975273c3e6e~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
LTV Analysis Form</div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e9b451dc419c4a57a5bd59ac89b5de5a~tplv-goo7wpa0wc-image.image" width="2446px" /></div>



|Event/date |Calculation example |
|---|---|
|Detailed explanation of the calculation of the number of new users |* In Event Analysis, you can see the number of new users who triggered clickhouse_query event on 07\-12, as shown in the figure below, which is 7,754.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dd25934814884ed6ab242c2b766b4709~tplv-goo7wpa0wc-image.image) </span><br><br>* Then in the result table of the LTV analysis tool, the number of new users on the day of 07\-12 is 7,754. You can click the number of users to view the detailed user list. |
|Detailed explanation of LTV0 calculation<br><br>(Take the start date of 07\-12 as an example) |* In the event analysis, you can sum all the new users who triggered the clickhouse_query event on the day of 07\-12 by time_cost, and the result is 386,221.<br><br>* Then in the result table of the LTV analysis tool:<br><br>   * 07\-12 Day: LTV0 = 386,221/8 = 48,277.625 Technologies 48,277.63 (keep two\-decimal approximations) |
|A Detailed Explanation of LTVn Calculation for N Days After a Certain Day<br><br>(Take the start date of 07\-12 as an example) |* You can save the new users on the day of 07\-12 as a user group, view the n days after 07\-12 in the event analysis, and sum the time_cost of these users every day.<br><br>* Then in the result table of the LTV analysis tool:<br><br>   * 07\-13：LTV1 =（386,221+0）/ 8 = 48,277.625 ≈ 48,277.63<br><br>   * 07\-14：LTV2 =（386,221+0+0）/ 8 = 48,277.625 ≈ 48,277.63<br><br>   * 07\-15：LTV3 =（386,221+0+0+64,237）/ 8 = 56,307.25<br><br>   * …… |
|Detailed explanation of overall LTVn calculation |* Overall LTV0 = {<br><br>   (Number of new users on 07\-12 \* LTV0 on 07\-12)<br><br>   + (Number of new users on 07\-13 \* LTV0 on 07\-13)<br><br>   + (Number of new users on 07\-14 \* LTV0 on 07\-14)<br><br>   + ……<br><br>   } / {<br><br>   New users on 07\-12 + new users on 07\-13 + new users on 07\-14...<br><br>   }<br><br>* Overall LTV1 = {<br><br>   (Number of new users on 07\-12 \* LTV1 on 07\-12)<br><br>   + (Number of new users on 07\-13 \* LTV1 on 07\-13)<br><br>   + (Number of new users on 07\-14 \* LTV1 on 07\-14)<br><br>   + ……<br><br>   } / {<br><br>   New users on 07\-12 + new users on 07\-13 + new users on 07\-14...<br><br>   }<br><br>* …… |
|LTV Trend Analysis |You can choose to analyze the overall LTVn trend, or you can choose to analyze a specific day in the time frame as the starting date for subsequent LTVn trends.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/254390e67f22468c8d9d50b86012e5e3~tplv-goo7wpa0wc-image.image) </span><br><br>Through the LTVn trend chart, you can intuitively see the overall trend or the change trend of the total revenue brought by each new user in the subsequent N days when a certain day is used as the starting date. This can be combined with some other data for business judgment. For example, if the LTVn trend chart continues to rise, it may indicate that users are willing to spend more and more money over time, and it may indicate that the revenue contributed by long\-term users exceeds the cost of new user acquisition. |
|LTV comparative analysis |You can choose to view the daily values of LTV1 to 10, LTV14, LTV30, LTV60, and LTV for comparison and analysis during the analysis period.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c56f6ecf91e145168500cb13c26f587a~tplv-goo7wpa0wc-image.image) </span><br><br>As shown in the figure above, it is a line chart of LTV0 for each day as the start date within the time range of 06\-18 to 07\-16. You can compare and analyze the LTV0 value for each day, for example, to see if LTVn has obvious time period regularities and so on. |


<span id="780a7fd4"></span>
### Advertising event

<div style="text-align: center">
LTV Analysis Chart</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/574a212b33334912afd9edea48d3ae87~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
LTV Analysis Form</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a8f02727c4643148df6bcc9dce865f4~tplv-goo7wpa0wc-image.image) </span>


|Event/date |Calculation example |
|---|---|
|Detailed explanation of the calculation of the number of new users |* Similar to the internal purchase event metric analysis process, in the event analysis, you can see the number of new users who triggered the clickhouse_query event on the day of 07\-12, which is 8, and save these users as user groups.<br><br>* Then in the result table of the LTV analysis tool, the number of new users on the day of 07\-12 is 8. You can click the number of users to view the detailed user list. |
|A Detailed Explanation of LTVn Calculation for N Days After a Certain Day<br><br>(Take the start date of 07\-12 as an example) |* The eCPM file uploaded in the example is as follows, and the daily eCPM value can be queried, where the eCPM value of 07\-12 is 65.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ce84e50cd514297be4bf334c790043f~tplv-goo7wpa0wc-image.image) </span><br><br>* In the event analysis, you can query the total number of events per day for all new users who triggered clickhouse_query events on the day of 07\-12, where the data on the day of 07\-12 is 720.<br><br>* Then in the result table of the LTV analysis tool: **number of ad clicks** \* ( **daily ecpm/1000** )/ **number of new users on the day**<br><br>   * 07\-12 Day: LTV0 = 720 \* (65/1000)/8 = 5.85<br><br>   * 07\-13：LTV1 = LTV0 + 0\*（32/1000） / 8 = 5.85<br><br>   * 07\-14：LTV2 = LTV0 + 0\*（32/1000） / 8 + 0\*（45/1000） / 8 = 5.85<br><br>   * 07\-15: LTV3 = LTV0 + 0 \* (32/1000)/8 + 0 \* (45/1000)/8 + 115 \* (3/1000)/8) Technologies 5.89 (keep two decimal places)<br><br>   * …… |
|Detailed explanation of overall LTVn calculation |* Overall LTV0 = {<br><br>   (Number of new users on 07\-12 \* LTV0 on 07\-12)<br><br>   + (Number of new users on 07\-13 \* LTV0 on 07\-13)<br><br>   + (Number of new users on 07\-14 \* LTV0 on 07\-14)<br><br>   + ……<br><br>   } / {<br><br>   New users on 07\-12 + new users on 07\-13 + new users on 07\-14...<br><br>   }<br><br>* Overall LTV1 = {<br><br>   (Number of new users on 07\-12 \* LTV1 on 07\-12)<br><br>   + (Number of new users on 07\-13 \* LTV1 on 07\-13)<br><br>   + (Number of new users on 07\-14 \* LTV1 on 07\-14)<br><br>   + ……<br><br>   } / {<br><br>   New users on 07\-12 + new users on 07\-13 + new users on 07\-14...<br><br>   }<br><br>* …… |


LTV Trend Analysis & LTV Comparison Analysis is consistent with internal purchase event indicators.

<span id="_3-ltv分析视频讲解"></span>
# Video explanation

<video src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7c2e56eb1f9f62000e1df595a44299ff.mp4" controls></video>
