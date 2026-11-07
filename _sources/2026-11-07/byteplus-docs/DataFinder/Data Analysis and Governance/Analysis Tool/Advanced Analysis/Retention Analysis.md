---
title: "Retention Analysis"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Retention_Analysis"
---

Retention analysis is a method used to analyze how a user continues to use a product or service (customer engagement/activity) over a specific period of time. Retention analysis can help you understand user behavior patterns and retention trends to optimize products, improve user experience, and develop marketing strategies to increase user retention and loyalty.

<span id="_1-概念介绍"></span>
# Concept introduction

<span id="d72ede67"></span>
## Initial events and follow\-up events


* Initial event: refers to a key action that a user completes within a specific period of time, such as registering, downloading an application, purchasing a product, etc. This event signals the beginning of user interaction with your product or service.

* Return event: refers to an action that the user completes again within a specific period of time after the initial event. For example, users log in again after registering, use the app again after downloading, purchase a product again after purchasing, and so on.


By analyzing the time interval between originating and returning events, you can gain an understanding of user retention. For example, you can calculate how many users completed the return visit event in a specific time period after the initial event, and the proportion of those users. This helps to evaluate user loyalty, engagement, and retention, and to determine which factors may affect a user's re\-engagement.

<span id="6c37d50a"></span>
# Computational logic

<span id="_1-1-留存"></span>
## Retention Metrics: Retention Rate

Retention refers to the user returning to the product after starting (adding or using the product) for a period of time, and the retention rate is used to measure the rate of returning to the product. User retention is one of the key metrics for improving product and operational efforts. Therefore, after product upgrades and operational activities, it is often necessary to monitor and analyze the retention rate of the client base affected by upgrades or activities.

DataFinder provides you with a pre\-set new user/active user retention rate calculation and analysis tool, and also allows you to use "Retention Analysis", a high\-level analysis tool, to flexibly calculate custom retention rates.


* For new/active user retention, directly use "New" and "Active" as the starting and return visit calculation basis for retention, you can view it on the page [Basic Retention](https://docs.byteplus.com/docs/DataFinder/Basic_Retention).

* **Custom retention** allows you to specify start events and return events at analysis time and use them as the basis for retention calculations.


<span id="c79a8ed4"></span>
## Retention Metrics: Custom Retention Rate

Using "Retention Analysis", a high\-level analysis tool, allows us to flexibly calculate custom retention rates, which can help us identify and analyze the parts of user return behavior that are truly valuable to the product business. For example: In order to cultivate users' habit of using the app to take a taxi, the operation team of a taxi app launched an activity of "signing in for a beautiful gift clock in 15 consecutive days" in the app.


* After the event was launched, the retention of new users and active users of the app improved significantly, but this was not enough to prove that the event achieved the expected results.

* By changing the custom retention rate (starting event = taxi, return visit event = taxi), the effect of the activity can be analyzed: if the custom retention rate improves significantly during the activity, it means that the activity is effective.


<span id="bc807ff7"></span>
### **Custom Retention Type Segmentation**


* From the time interval where the retention rate is calculated, DataFinder supports viewing: **the retention rate of the default retention interval** and **the retention rate of the custom retention interval** .

   
   |Retention breakdown |Retention Indicator Description |
   |---|---|
   |Retention rate for default retention interval |* It means that DataFinder provides you with a default retention rate calculation interval based on the data query time range you configure, that is, the ratio of the number of users who return to the product after a specific point in time to the number of initial users.<br><br>* It is suitable for evaluating key milestones of a product or important points in the user journey. Through retention analysis, trends and patterns in user retention can be identified, providing data to support product improvement, user retention strategies, and market positioning. For example, measuring the short\- and long\-term impact of a particular promotion or advertising campaign on user retention. |
   |Retention rate for custom retention intervals |* Custom interval retention allows you to define a time horizon for retention analysis based on specific business needs or goals.<br><br>* It is suitable for retention analysis scenarios that are strongly related to the operating cycle of a business. For example:<br><br>   * Analyze how many users returned during the 7\-day free trial period after the first registration; and which users returned within 30 days after the free probation period ended.<br><br>   * Analyze retention between daily and weekly retention, such as every 3 days. |
   

* From the date of calculation of the retention rate, DataFinder supports viewing: **the retention rate for a specific day** and the **overall retention rate** .

   
   |Retention breakdown |Retention Indicator Description |
   |---|---|
   |The retention rate for a specific day |* Refers to the **N\-th day after the initial behavior occurs** , the proportion of users who are still active to the total number of initial users.<br><br>* Must be active **on the N\-day day** , the indicator sensitivity is high, can reflect the product performance on that day.<br><br>* It is suitable for analyzing user churn points, optimizing key node experience, etc. |
   |Overall retention rate |* Taking the overall retention as an example, it refers to the proportion of all users who triggered the starting event within the selected time frame (e.g. the past 7 days), and how many users triggered the return event the day after the starting event was triggered.<br><br>* The indicator is less sensitive and more relaxed, reflecting the long\-term stickiness of the product.<br><br>* It is suitable for evaluating overall user activation effectiveness and channel quality. |
   


<span id="3cb422ed"></span>
### Custom retention calculation logic


|Retention breakdown ||Calculation formula |
|---|---|---|
|Specific date retention rate |**Day retention rate** :<br><br>The percentage of users who return to the product on the day they add or use it. |* The retention rate for a specific day:<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb147f02b629493ba22f9f043b1f2e94~tplv-goo7wpa0wc-image.image) </span><br><br><br>* The overall retention rate for a specific day<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/61b4183512894621a08786af087fcb7f~tplv-goo7wpa0wc-image.image) </span> |
||**Day Retention Rate at Day 1** :<br><br>The rate at which users return to the product on the second day after adding or using it. |* Day Retention Rate at Day 1:<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d69771a511f4eeb985c01c9bb41ed15~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Overall Day Retention Rate at Day 1:<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/81285e042bcc4afda24697d60665c131~tplv-goo7wpa0wc-image.image) </span> |
||**N\-day retention rate** :<br><br>The rate at which users return to the product on the nth day after adding or using it. |* The n\-day retention rate for a specific day:<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e2185e1045a740fbae76695af5622687~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Overall n\-day retention rate:<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b50c03efd67c4452810bb82ecc71f21c~tplv-goo7wpa0wc-image.image) </span> |
||**Next Week Retention Rate** :<br><br>The percentage of users who return to the product 8 to 14 days after adding or using the product.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The week here refers to the 7\-day week, not the natural week.</div><br> |* The following week's retention rate for a specific week:<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6b65b4e95f148ef8fc90fb04b399fd2~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Overall next\-week retention rate:<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/acfaa009bba242bab3ad354a6ae58868~tplv-goo7wpa0wc-image.image) </span> |
||**N week retention rate** :<br><br>The percentage of users who return to a product within nth week of adding or using it.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The week here refers to the 7\-day week, not the natural week.</div><br> |* The n\-week retention rate for a specific week:<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dbbfbe0affca4c74a3b19fb8afb82e9e~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Overall n\-week retention rate:<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d60e2ab3f3904a19bf25ebbd455d1ef1~tplv-goo7wpa0wc-image.image) </span> |
||**The monthly retention rate** :<br><br>The percentage of users who return to the product the following month after adding or using it. |* Specific monthly retention rate:<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/73c2edadbd5d47e4bd347e3da2857cc3~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Overall monthly retention rate:<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0870eb13b44245ffb4a3ae205aae3214~tplv-goo7wpa0wc-image.image) </span> |
||**N monthly retention rate** :<br><br>The percentage of users who return to a product within the nth month after adding or using it. |* Specific month n monthly retention rate:<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c1cb764922fb463c83a8b2dfd7896f8b~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Overall n monthly retention rate:<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cfbb666e929541a092bee712061b9343~tplv-goo7wpa0wc-image.image) </span> |
|Retention rate for custom retention intervals |Retention rate for custom intervals:<br><br>After the initial behavior, custom viewing occurs within the nth day/week/month to the mth day/week/month. |* A day's retention rate for a custom range<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b3c722f8ee34e8baf9eb96f828ae3ac~tplv-goo7wpa0wc-image.image) </span><br><br><br>* The overall retention rate for a custom range<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9e96d0d87a784feb887fbff62fb48503~tplv-goo7wpa0wc-image.image) </span> |


<span id="_1-2-新用户留存"></span>
## Retention Metrics: New User Retention Rate

New user retention analysis tools are preset in DataFinder, and you can [Basic Retention](https://docs.byteplus.com/docs/DataFinder/Basic_Retention) see how to directly analyze new user retention metric data on the page.


* New user retention is calculated with " **new user** " as the retention starting condition.

   That is, if 50 of the 100 new users added yesterday return to the product today, the new user's Day Retention rate at Day 1 yesterday is 50%.

* New user retention is the most commonly used retention calculation. In most cases, unless otherwise specified, "retention = retention of new users".


<span id="分析指标：活跃用户留存率"></span>
## Retention Metrics: Active User Retention Rate

The analysis tool for active user retention is preset in DataFinder, and you can [Basic Retention](https://docs.byteplus.com/docs/DataFinder/Basic_Retention) see how to directly analyze active user retention on the page.


* Active user retention is calculated with "**active user**" as the retention starting condition.

   If 50 of the 100 users who were active yesterday return to the product today, the Day Retention rate at Day 1 is 50%.


<span id="_1-5-流失率"></span>
## Retention indicator: attrition rate

Retention analysis supports toggle viewing attrition rates.


* The definition of a lapsed user in retention analysis is that it is considered a lapsed user after multiple consecutive "days" (that is, counting from the second day of triggering the initial behavioral event, for multiple "days" in a row) without subsequent events. For example, "Day 5" churn means that after 2,005 people perform the initial event, there is no follow\-up event from the second day until the fifth day. That is to say, a user may be a lapsed user on the 2nd day, but a return visit on the 5th day is not a lapsed user on the 5th day.

* Calculation logic:

   1. N daily churn rate （%）= （ number of no return visit events on each day from the 2nd to the N day of the closed interval/number of starting events on the day) \* 100%;

   2. Day 1 churn: that is, the churn on the same day. After the user has an initial behavioral event on the same day, there is no subsequent event on the same day, which is regarded as the churn on the same day.


<span id="6fe15caf"></span>
## Business metrics: analytical metrics

The SaaS\-cloud native environment also supports the analysis of business analysis metrics in the business objective dimension based on the analysis of retention metrics for user behavior. For example, while analyzing the user retention metrics of the application, monitoring and analyzing business metrics such as the per capita order amount of the user.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The analytical metrics function of the current business objective dimension is turned off by default. If you wish to use this function, you can contact the BytePlus technical support staff to enable this function.</div>


<span id="_2-快速入门"></span>
# Function usage

<span id="_2-1-新用户留存和活跃用户留存"></span>
## Retention Analysis: New User Retention and Active User Retention

In the growth analysis platform, new user retention and active user retention are the default general metrics, which can be viewed in the top navigation bar **Scenario Analysis** \> **Basic Analysis** \> **General Analysis**. Please check the detailed introduction [Basic Retention](https://docs.byteplus.com/docs/DataFinder/Basic_Retention).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cccdad08828f450c866232d829a2f0da~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-自定义留存"></span>
## Retention Analysis: Custom Retention

After logging in and entering the DataFinder console, select Select **Analysis Tools** \> **Advanced Analysis** \> **Retention Analysis** at the top to enter the Event Retention Analysis Tools page, which supports self\-setting start events and return visit events for retention analysis.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Retention analysis in a growth analysis platform refers to custom retention analysis.</div>


<span id="f028ff74"></span>
### Configuration calculation calculation method

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71ad212b586e4389a98e16feb9e3608b~tplv-goo7wpa0wc-image.image) </span>


|Parameter |Configuration instructions |
|---|---|
|Subject |If you have enabled the multi\-principal function, you can switch which principal to use at the top, see for details [Multi-Application/ Multi-Agent/ Multi-ID Type Overview](https://docs.byteplus.com/docs/DataFinder/Multi-Application_Multi-Agent_Multi-ID_Type_Overview). |
|Statistical caliber |The current DataFinder uses the user (ssid) as the statistical caliber of the analysis data by default. If you want to use other statistical calibers, you can create a good caliber and switch it. Please refer to the details . |


<span id="_2-2-1-留存条件设定"></span>
### Configuration analysis metrics

<span id="85b97c3f"></span>
#### Add retention metrics

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2eca6b9829cb4dd3b80f2666e911f019~tplv-goo7wpa0wc-image.image) </span>


1. Select the starting event and the return event. You can select the Start Event and Return Event, and click the Filter Criteria button after the Start Event or Return Event to add a filter to the event.

2. Configure the associated properties of the metric. Associated properties are used to keep the value of a property consistent between the starting event and the return event, and are often used for things like event names, page titles, or product names.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The two associated properties must have values, and the value types must be consistent; for example, two visits to the product details page and a return visit to the same product (product IDs need to be consistent) are considered retention.   </div>
   

3. (Optional) If you have multiple analytical metrics, you can click  **+ Retention Metrics** to add a new one.


<span id="22b9c207"></span>
#### Add analytical metrics

You can select the event of the business metric in the drop\-down box, and at the same time support the calculation of the following operators on the event, and use the calculation result as the final analysis metric.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The analytical metrics function of the current business objective dimension is only supported by the SaaS\-cloud native environment and is turned off by default. If you wish to use this function, you can contact the BytePlus technical support staff to enable this function.</div>



|Operators supported by analytical indicators |calculation logic description |
|---|---|
|Total number of times (PV) |Number of occurrences |
|Total headcount (UV) |Total number of triggers for the event |
|Number of times per person (PV/UV) |Number of incidents/number of return visits |
|Sum by... (SUM) |The sum of the values of an attribute |
|According to the average person (SUM/UV) |sum of a certain attribute value/number of return visits |
|Cumulative Sum by Stage (CUMSUM) |The sum of the historical accumulation of a certain attribute value |
|Cumulative per capita by stage (CUMSUM/UV) |The sum of the historical accumulation of a certain attribute value/the number of returns |
|Cumulative mean per person by stage (CUMSUM/FUV) |The sum of the accumulated history of a certain attribute value/the starting number of people |


<span id="dd0ccffc"></span>
### Configure Segmentation Filtering

Segmentation screening is mainly used to filter users to determine which users meet the requirements for analysis.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2cc4b77881b44ccb92676d49fd559126~tplv-goo7wpa0wc-image.image) </span>


1. Configure primary and secondary filter conditions.

   * Select the first filter condition of the user to be analyzed in the sub\-filter area, and refer to the filter logic details [In-Text Grouping (Segmentation Filtering)](https://docs.byteplus.com/docs/DataFinder/In-Text_Grouping_Segmentation_Filtering).

      * **Attribute filtering** : event attributes, user grouping, user attributes, user tags (such as open), etc. The user group selects the latest one\-day calculation result by default, and can switch the calculation logic by clicking "Latest Data" to specify a certain one\-day result.

      * **Behavior Circle** : Users who have "done/not done/done XX behavior in turn" within the specified time frame.

      * **Dynamic matching** : Filter by dynamically matching events with the crowd at specified intervals.

   * You can click  **+ Attribute Filter** ,  **+ Behavior Circle Selection** ,  **+ Dynamic Circle Selection** below to add multiple first\-level filter conditions, and the logical relationship between multiple filter conditions can be set to **AND** or **OR**.

   * You can hover the mouse behind the filter to add a secondary filter to the filter. Supports the addition of multiple secondary filter conditions, and the logical relationship between multiple secondary filter conditions can be set to **AND** or **OR**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/78dda6f9200b4bb8b0e084d113bcf7e5~tplv-goo7wpa0wc-image.image) </span>

2. Add a control group.

   * You can click  **+ control group**, which is equivalent to grouping and comparing the results.

   * Supports the creation of multiple control groups, and replicates created control groups.

3. Other supported operations:

   * Modify the name of each filter group.

      You can click the "small pencil" button after the filter group name to rename the filtered user group for easy memory.

   * Batch entry filter criteria.

      You can click the "small pencil" button after the filter conditions, and enter the filter conditions in batches according to the interface prompts to improve the configuration efficiency.


<span id="e22f6eca"></span>
### Configure attribute grouping

After configuring attribute grouping, the result chart of subsequent query analysis will be grouped and displayed according to the dimension of each attribute value configured, which is convenient for more refined analysis.

For example, when analyzing the distribution of the number of DAUs in different system versions of an app, you can group the DAU number metric by the "system version" attribute of the app. See the configuration example [[Attribute Grouping] View DAU data under different system versions](https://docs.byteplus.com/docs/DataFinder/Event_Analysis#12d77dd9).

The operation instructions are as follows.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31c803a86f9049d3b4805834e99f41ad~tplv-goo7wpa0wc-image.image) </span>


1. Click "+ Properties Grouping" and select event properties, user properties, etc. for grouping in the drop\-down box.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Attribute grouping supports grouping by event attributes, user attributes, and subject labels, for a total of up to 10 layers of grouping.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Attribute grouping conditions apply only to the starting event of each metric.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After adding analysis metrics, setting attribute grouping is not supported.   </div>
   

2. You can set which analysis event metric the grouping applies to.


See more detail about attribute grouping [Property (Custom) Grouping and Properties](https://docs.byteplus.com/docs/DataFinder/Property_Custom_Grouping_and_Properties).

<span id="_2-2-2-留存分析图"></span>
### Configure and view retention analysis charts


1. **Configure the retention analysis time range and retention analysis time period.** 

   By default, the system automatically displays the statistical results for the last 7 days in the form of a retention trend chart. You can make the following adjustments to the analysis chart as required.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ed1d19b48b642798184d81383283989~tplv-goo7wpa0wc-image.image) </span>

   * You can choose the time granularity of the analysis to be day, week, or month, and choose the corresponding start time for the retention analysis.

   * In the Retention Analysis interval, you can choose whether to use the default interval or customize the retention analysis interval.

   
   |Configuration parameters |Configuration instructions |
   |---|---|
   |Time granularity |That is, according to the day, week, month these granularity to summarize statistical user data.<br><br><br>* Select Sky: Retain all charts for analysis. When presented in Sky, today's data is displayed by default.<br><br>* Select the week level: the default display period is Monday to Sunday, you can click to modify the statistical range;<br><br><br>See below for more details on time granularity [Reference: Time granularity in retention analysis](https://docs.byteplus.com/docs/DataFinder/Retention_Analysis#81362cb9). |
   |Start time |That is, to count the users who have initiated the behavior within a certain period of time. |
   |Cycle comparison |The options for time comparison can be selected: the previous cycle, the same cycle, the same period last month, the same period last year, and a custom time.<br><br><br>* Previous cycle: The previous period of time that meets end to end<br><br>* On the same cycle: move forward one week, corresponding to the weekly order.<br><br>* The same period last month: move forward by January, corresponding to the monthly order.<br><br>* The same period last year: move forward by one year, corresponding to the month and date. The specific strategy is to directly change the year, and then subtract the time interval of the compared time from the end time of the comparison time to obtain the start time of the comparison time.<br><br>* Custom time: Customize the start time and end time of the comparison time period. |
   |Retention interval |That is, the time period of statistical retention, support setting as the default interval and custom interval retention.<br><br>Configuration examples can be found below [use example](https://docs.byteplus.com/docs/DataFinder/Retention_Analysis#4f9d6085). |
   |Retention time |That is, the retention of the user whose initial behavior occurred at a specified time is counted.<br><br><br>* When you choose to view retention from days 2 to n, you can view up to 120 days of retention (Day 120). |
   

2. **View the retention analysis results chart.** 

   * **Retention trend graph**

      If you want to see a retention trend graph, you can select "Trends" in the presentation method.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/20194431b88d4f2db86b6c20771055bd~tplv-goo7wpa0wc-image.image) </span>

      * In the Retention Trend Chart, it is supported to view the overall retention trend (default), and it is also supported to view the process trend on a specific day. You can click the " **Date** " drop\-down box above the chart to select the date you need to view the retention trend.

      * Only when selecting the retention trend chart for a specific day, clicking on the dots on the polyline can support the microscope function (save as a user group, export users, view samples), but the overall retention trend does not support the use of the microscope function. For more detailed microscope functions, see the documentation: [Microscope Function](https://docs.byteplus.com/docs/DataFinder/Microscope_Function).

   * **Retention comparison chart**

      If you want to observe the change of indicators such as next\-day retention and day 7\-day retention rate over time, you can choose "Retention Comparison" in the presentation method.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a300b88aeb604e8085436a18b9e103ad~tplv-goo7wpa0wc-image.image) </span>

      * Click on the point on the retention comparison chart to support microscope functions (new date annotation, save as user group, export user ID, view user list).

      * The Retention Comparison Chart supports viewing the next day's (default) retention comparison data, and also supports clicking the date in the "Date" drop\-down box at the top of the chart to set up a view of the retention comparison data for another day.

3. Charting tips. You can zoom the analysis time period to view a finer or more complete chart of the data.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e9c46007016448fe8f4bbdc10b243df1~tplv-goo7wpa0wc-image.image) </span>


<span id="_2-2-3-留存分析图表"></span>
### View and analyze detailed data

Review the retention analysis statistics.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/96d45d6a1201428f87cf77ca76716168~tplv-goo7wpa0wc-image.image) </span>


* You can choose whether to display the number of users.

* Support switching sorting according to the starting number;

* Statistical results can be downloaded as an Excel file.


<span id="8727fa46"></span>
# The next step: in\-depth analysis

<span id="9e37e484"></span>
## Analysis of day retention and attrition rates


* The data retained on the day is not displayed in the chart area by default. If you need to view it, you need to click "Calculate the retention of the day".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c0ad105f065c4c4fa87753e257d61122~tplv-goo7wpa0wc-image.image) </span>

   Day1 is the day of retention:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f78d904ad91444f8b9fea71604d47a2c~tplv-goo7wpa0wc-image.image) </span>

* If you need to view the attrition rate, you can view the attrition rate in the Retention Analysis Chart, click the "Retention" drop\-down and select "Drop\-off".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ba081d5bcd546c48dec1c66cf3ad3cf~tplv-goo7wpa0wc-image.image) </span>


<span id="cb2dfa96"></span>
## Export/view user information


|In the chart |In detailed data |
|---|---|
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/87dfb6ea287a40bfaea86cc19af19b71~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cbbdac96daca4c50832cc4a329d09d7f~tplv-goo7wpa0wc-image.image) </span> |


<span id="14df1c7b"></span>
## Download query results as offline data

You can download the query results as an Excel file.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0960bd2669a9422795908b305046a27f~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-4-保存到看板"></span>
## Save analysis results to Dashboard

Click "Save to Dashboard" in the upper right corner to add indicator charts that require long\-term monitoring to the Dashboard board.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7d8c1b6f5aea449291be08bc62bc5e8a~tplv-goo7wpa0wc-image.image) </span>


|Parameter |Configuration instructions |
|---|---|
|Chart name |Charts can be renamed for subsequent viewing. |
|Save location |* You can choose to save the diagram to **personal space** or **public space** , more information can be viewed [Dashboard Overview](https://docs.byteplus.com/docs/DataFinder/Dashboard_Overview)in the description of personal and public space.<br><br>* Once selected, you can select the Dashboard path where the chart is saved in the drop\-down box. |
|Chart Type |Select the type of chart to save. Current Retention Analysis supports saving retention curves and retention tables to Dashboard. |


<span id="4f9d6085"></span>
# Usage example

<span id="8422c37a"></span>
## [Default range retention] Default day level retention for the past 7 days

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5e7780b6e7a14137ac5bde361bf9cf73~tplv-goo7wpa0wc-image.image) </span>

<span id="38c2a5e2"></span>
## [Default interval retention] Weekly level retention for the past 30 days

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c05b4e2976a4ea083c3a3ae58c4b2b1~tplv-goo7wpa0wc-image.image) </span>

<span id="6b71ad14"></span>
## [Custom interval retention] According to the business policy statistics  **++custom period ++** retention

Example scenario: The customer expects to count the retention of  **++custom cycles ++** based on business policies. Taking a content application as an example, the onboarding policy for beginners is as follows:


* 1 to 3 days: Conduct user interest spying through recommendation strategies to establish users' initial understanding of the platform

* 4 to 7 days: Guide users to improve their personal information through points/membership policies

* 8 days to 30 days: Establish user connections by guiding users to share/like/follow, and improve long\-term user stickiness


Therefore, customers expect to observe user retention according to the business cadence, which can be configured by customizing the retention interval.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aaa89fbabe1c4dcdb09b6f4e5fd14b4e~tplv-goo7wpa0wc-image.image) </span>


|Date |Starting number |Custom interval 1:1~ 3 days |Custom interval 2:4~ 7 days |Custom interval 3:8~ 30 days |
|---|---|---|---|---|
|January 1, 2023 |100 |80% |60% |50% |
|January 2, 2023 |150 |77% |63% |45% |
|January 3, 2023 |89 |83% |59% |51% |
|... | | | | |


<span id="_4-常见问题"></span>
# Common problem


1. **Why is today's, week's, or month's retention rate lower than expected?** 

   In order to ensure that the data is reported correctly, it is possible to further compare whether the calculation methods of retention are consistent. The Finder has the following policies when calculating day retention:

   1. The return visit event must be later than the starting event.

   2. When the return visit event and the starting event occur at the same time, they are not included in the retention on the same day;

   3. Multiple identical starting events are evaluated only once.

   4. The time range of the natural day, natural week and natural month will be affected by the application time zone setting.

   5. The day, week, and month granularities are all natural days, natural weeks, and natural months. When selecting the week granularity, the starting day can be modified, and the default is Monday.


<span id="81362cb9"></span>
# Reference: Time granularity in retention analysis

The "day", "week", and "month" time granularities involved in the retention analysis query refer to the natural day, week (the start day of the week can be modified, and the default is Monday), and month. Each column in the retention is divided according to the time granularity you set (the "week" granularity is set as shown in the figure below). We count the day, week, or month as the first cycle, so when the time granularity is arranged from left to right, take the days as an example: the starting day, the second day in total, the third day in total, the fourth day in total,...

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/40b0a61560ca401b87456a63e2db1f53~tplv-goo7wpa0wc-image.image) </span>


* **When selecting day granularity**

   * The starting time is 00:00:00 on each natural day, and the ending time is 23:59:59 on that day.

   * The time zone set when creating the application will also affect the division of natural days, and the domestic default is Beijing time;

   * When calculating retention for the day, a return visit event occurs later than the start event. If a user's initial event occurs at 23:52 on March 1, then only if the return visit event occurs later than 23:52 on March 1, and before 23:59:59 on March 1, the user will be counted for retention on the day.

   * Users will only have multiple initiation events in a calendar day, which will be counted once. If the starting event occurs on a different calendar day, the user is counted in the starting population on a different date.

* **When selecting weekly or monthly granularity**

   * The starting time is 00:00:00 on the first day of each natural week or month, and the ending time is 23:59:59 on the last day of the week or month.

   * The time zone set when creating the application will also affect the division of natural days, and the domestic default is Beijing time;

   * The starting day of the week granularity can be selected in the calendar, and the default Monday is the starting day;

   * Weekly or monthly granularity extends the range of dates selected in the calendar to correspond to the full natural week or month. Take the choice of week granularity as an example: the date range selected by the user in the calendar is April 1 (Wednesday) to April 10 (Friday), and the query will push April 1 forward to find the first day of the week, March 30 (Monday), and April 10 back to find the last day of the week, April 12 (Sunday). Finally, the actual query was conducted between March 30 and April 12.

   * When calculating retention for the current week or month, return events that occur later than the start event are counted. If a user's starting event occurs on Wednesday, April 1, then only if the return visit event occurs later than 00:00:00 on April 1 and before the end of April 5, the user will be counted as retained for the week.


<span id="504d3edd"></span>
# Reference: Video explanation of retention analysis function

<video src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6540a6dc74720e224c53442aa2e0233f.mp4" controls></video>
