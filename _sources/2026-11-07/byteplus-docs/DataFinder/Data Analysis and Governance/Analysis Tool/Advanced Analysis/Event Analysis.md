---
title: "Event Analysis"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Event_Analysis"
---

Event analysis, as one of the most important analysis methods in data analysis, can help us study the value impact of a behavioral event on an enterprise. BytePlus Growth Analysis "Event Analysis" supports multi\-dimensional analysis of user behavior by building metrics, grouping filters, and a variety of visual charts. At the same time, it provides abnormal data analysis capabilities in data intelligence insights, which can help us discover the impact of more data anomalies. This article provides you with detailed instructions on using the DataFinder event analysis tool.

<span id="_1-概述"></span>
# Background information

<span id="_1-1-整体概述"></span>
## Related concepts

Before doing event analysis, you need to understand the main concepts involved in event analysis tools to help you understand the analysis logic of event analysis tools. The introduction is as follows. Please refer to the introduction of data model related concepts involved in detailed event analysis tools .


|Term |Concept introduction |
|---|---|
|**Event** |Events are datafied descriptions of user behavior. For example, in a video app, a user becomes interested in the products recommended by the blogger after watching content A, and then clicks on the product link in the comment area to complete the purchase in the e\-commerce platform. A series of user behaviors such as watching videos, clicking links, and placing orders can be described by "events" after being datafied through event tracking. |
|**Attributes (Params)**  |In the BytePlus Growth Analysis platform, we describe user behavior in detail and accurately by combining "event name + attribute list":<br><br><br>* The **event name** is used to distinguish different types of user behavior, such as "video_play (play video) ", "like (like) ".<br><br>* The event is described in detail through **attributes** , such as "video_id = 12358" and "play_mode = normal" to further describe the specific video and playback method played.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">In the growth analysis platform, attributes currently support string (string), numeric (int/float), and other types.</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">String type properties such as video_id, video_name.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Int type properties such as video_play_time (duration of video playback).</div><br><br><br><br><div data-tips="true" data-tips-type="warning">See more about attribute data format requirements <a href="https://docs.byteplus.com/docs/DataFinder/Supported_Data_Formats_and_Event_Property_Classification#_1-%E5%B1%9E%E6%80%A7%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B">1. Attribute data types</a>.</div><br><br><br>According to the scope of application, attributes are divided into "**event attributes**" and "**event public attributes**". |
|**Event properties** |Attributes that relate to a single or several events, such as video_id, video_name, play_mode attributes of video_play events, or video_id attributes of video_add_favorite events. |
|**Event public property** |Event public properties can be shared by all events, such as the time the event occurred, the app version, the IP address, and so on.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In DataFinder, in addition to event attributes and event public attributes, there are also <strong>user attributes</strong>, which are used to describe the relevant information of the user, such as the user's age, gender, etc.</div><br> |
|**Event analysis** |DataFinder provides you with "event analysis" tools that allow for multi\-dimensional analysis of user behavior by building metrics, grouping filters, and various visual charts.<br><br>Typical analysis scenarios include:<br><br><br>* Product team: Count users' usage of product functions (such as search, video playback, add favorites, etc.);<br><br>* User operation team: statistics on the operation conversion of different segments of the population, such as the subsequent conversion of users participating in different promotional activities (such as receiving activity coupons) (using coupons to place orders to buy goods);<br><br>* Content operation team: statistics of user use and consumption of content, such as statistics of the number of video content players, playback times and playback time in the video app;<br><br>* Marketing team: Count the conversion of users through different channels, such as comparing the number of new app users brought to different app stores.<br><br>* Analyst team: Can quickly conduct multi\-dimensional drill\-down analysis and configure business\-related analysis metrics.<br><br>* ……<br><br><br>The event analysis function of DataFinder is very flexible and can well meet the statistical requirements in various scenarios. |
|**Indicator** |The metrics of data analysis are related to the business goals of the analysis, and the business metrics to be analyzed can usually be reflected by quantified event values  **.**  In the DataFinder, you can define the metrics of event analysis by selecting the calculation method of event, event/attribute value, and support filter analysis by attribute filter conditions.<br><br>For example, a page visits UV, PV, number of times per capita, duration, click through rate, penetration rate, retention rate, success rate. Indicators can be divided into attributes data and composite indicators, such as UV, PV, and orders. |


<span id="_1-4-事件分析支持分析哪些指标（metric）"></span>
## Calculation Logic: Supported Metric Operators

When using DataFinder event analysis, you can choose the metrics to analyze based on your business goals. Indicators can be logically calculated and statistically analyzed by indicator operators based on selected events. The following are the indicator operators supported by the DataFinder event analysis indicator and the calculation logic of each operator.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">In the following operator descriptions, numeric properties currently refer to two types: int and float.</div>



|Index operator |Explanation of the computational logic of operators |Example |
|---|---|---|
|Total number of times (PV) |count the number of events |Count the total number of times users have played videos in the app |
|Total headcount (UV) |Count the number of occurrences of the event |Count the total number of deduplicated users who have played videos in the app |
|Penetration rate (UV/AU) |Total number of event triggers/total active people, where the denominator is the number of triggers any_active_event event<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">any_active_event preset events for the system, see <a href="https://docs.byteplus.com/docs/DataFinder/Inter-Side_Preset_Properties">Inter\-Side Preset Properties</a>.</div><br> |Check the percentage of active users after the new feature goes live |
|Number of times per person (PV/UV) |That's pv/uv, the number of occurrences per person. |Count the number of times users play videos per capita: pv/uv |
|Number of fully active users per capita (PV/AU) |Total number of event triggers/total active people, where the denominator is the number of triggers any_active_event event |Check the number of active users per capita after the new feature goes live |
|Press... Sum (SUM) |Sum by the numeric properties of the event |Total length of video playback: sum (video_play_duration) |
|Press... to find the maximum value (MAX) |The maximum value of an attribute, only numeric attributes are supported |The maximum video playback time |
|Press... to find the minimum value (MIN) |The minimum value of the value of an attribute, only numeric attributes are supported |The minimum value of video playback time |
|Average by |The sum of the values of a property/the number of events, only numeric properties are supported |Average video playback time: sum (video_play_time)/pv |
|Per person |The sum of the values of a property/the number of events, only numeric properties are supported |Stats timespan per person: sum (video_play_time)/uv |
|Press... to find the average number of active users |The sum of the values of a numeric property/the total number of active people, where the denominator is the number of triggers for the any_active_event event |Stats active users' video playback timespan per person: sum (video_play_time)/total active users |
|To percentiles |That is, after sorting the data in the unit time range from small to large, find the number on a certain bit;<br><br>Common examples such as median (50% percentiles) and 90% percentiles only support numeric values. |View the distribution of the number of daily user target events (in this case, watching videos) |
|Press... to deduplicate |That is, deduplicate statistics on event parameters |Count the number of videos played in a played video event |
|Press... deduplicate with user |That is, deduplicate statistics on event parameters and users who have done the event |Count the total number of videos viewed by users |


<span id="_2-功能使用"></span>
# Function usage

<span id="_2-1-功能界面组成"></span>
## Functional interface composition

Before using the event analysis tool, you can browse the event analysis tool interface to understand the main functional modules. The event analysis function interface consists of the following parts.


|Interface example |Page module introduction |
|---|---|
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/13f92cff4a4e4035b59513afa2909e2e~tplv-goo7wpa0wc-image.image) </span><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92ebcf7921d1433b9ae84a77c6e2770d~tplv-goo7wpa0wc-image.image) </span><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ff9afa30a29c45619c5e3d2341a4ad94~tplv-goo7wpa0wc-image.image) </span> |* Event selection and configuration metrics: You can choose one or more target events to be analyzed, and set the calculation operator and filter conditions of the target events as the analysis indicators for event analysis.<br><br>* Subdivision filtering: filtering users for query analysis by attributes, user grouping, etc.;<br><br>* Attribute grouping: Set the query analysis results by attributes, user labels, etc. to be grouped and displayed in what dimension;<br><br>* Event analysis chart: Display analysis results through visual charts.<br><br>* Detailed data: a detailed data table of the analysis results;<br><br>* Abnormal diagnosis: common dimension analysis for abnormal data;<br><br>* Transpose: The data of the analysis chart can be displayed and adjusted in rows and columns;<br><br>* Download data: You can download detailed data locally;<br><br>* Save to Dashboard: Save the current analysis results to Dashboard. |
|Other common configurations<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ebb2bcad5deb4c9aa43ed3b566243b5b~tplv-goo7wpa0wc-image.image) </span> |* Analysis mode: The default is "event" analysis mode, and it supports switching to session analysis. This article mainly introduces event analysis, please refer to the session analysis content [Custom Session](https://docs.byteplus.com/docs/DataFinder/Custom_Session).<br><br>* Statistical criteria: DataFinder's default data statistical analysis criteria is "user", you can also switch the statistical criteria of the current analysis data, the selected statistical criteria can be viewed in the statistical criteria of metadata management, see for details [Statistical Criteria](https://docs.byteplus.com/docs/DataFinder/Statistical_Criteria).<br><br>* Time zone: You can switch the time zone of the current analysis data. The supported time zone configurations can be viewed in the Common Settings \- Multi\-Time Zone Configuration in the Project Center/Application Management.<br><br>* Principal: If you also have multi\-agent enabled, it is supported to switch the principal of the current analysis. The multi\-agent function is currently only open on demand for SaaS\-cloud native user customers with relatively complex business. Please refer to the details [Multi-Application/ Multi-Agent/ Multi-ID Type Overview](https://docs.byteplus.com/docs/DataFinder/Multi-Application_Multi-Agent_Multi-ID_Type_Overview). |


The usage process of the event analysis tool and detailed usage instructions for each module can be found below.

<span id="_2-2-选择事件和指标"></span>
## Configuration analysis metrics

After logging in and entering the DataFinder console, select Select **Analysis Tools** \> **Advanced Analysis** \> **Event Analysis** at the top, go to the Event Analysis Tools page, and then select the target event and statistics to analyze.


* You can analyze a single metric, or you can add multiple metrics to analyze it together.

* DataFinder provides you with universal event metrics, as well as flexible configurable custom metrics, formula metrics (only SaaS\-cloud native support), which you can choose from on demand.


The detailed introduction and operation steps are as follows.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/46a1329b2ed74f55adbeaacc453579c4~tplv-goo7wpa0wc-image.image) </span>

<span id="e4933beb"></span>
### Add regular metrics


1. Select the indicator event to analyze and the calculation operator for the indicator event.

   * Current indicator events support the selection of "general events", "virtual events" and "circled events".

      If there is no indicator event you want to analyze in the current indicator event drop\-down box, you can go to the "General Events", "Virtual Events" and "Circled Events" pages of **Data Management** \> **Metadata Management** to see if the event exists.

   * Currently supported operators can be found above: [Calculation Logic: Supported Metric Operators](https://docs.byteplus.com/docs/DataFinder/Event_Analysis#_1-4-%E4%BA%8B%E4%BB%B6%E5%88%86%E6%9E%90%E6%94%AF%E6%8C%81%E5%88%86%E6%9E%90%E5%93%AA%E4%BA%9B%E6%8C%87%E6%A0%87%EF%BC%88metric%EF%BC%89).

   * Typical scenario indicator configuration examples can be found below [Usage example](https://docs.byteplus.com/docs/DataFinder/Event_Analysis#6f1ffee3).

2. Add filter criteria for metrics.

   * You can add filters to events as needed, support the configuration of multiple filters, and specify the logical relationship between filters as "and", "or".

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">When selecting the time attribute value of the filter condition, the current interface drop\-down box supports displaying up to 1000 attribute values. If your attribute value exceeds 1000 and the attribute value you need to use is not displayed in the drop\-down box, you can search for and select the corresponding attribute value.      </div>
      

   * For string properties, the following features are also supported:

      1. Click the "Switch" button to change the way the filter is added from selected to manually entered (copy and paste support).

      2. With regular expression matching, note that regular expressions only support [re2 ](https://github.com/google/re2/wiki/Syntax)syntax.

3. (Optional) Add multiple metrics.

   * In addition to regular metrics, DataFinder also provides you with custom metrics and formula metrics. You can click the corresponding button to add the corresponding metrics. See below for the introduction of these two types of metrics.

   * You can hover the mouse over the added indicator, click the copy button above to copy the configured indicator, or click "+ Event Indicator", "+ Custom Indicator", etc., to quickly copy the existing indicator, and repeat the above steps to configure more indicators.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Event Indicators + Formula Indicators + Custom Indicators Add up to 50 groups.   </div>
   

<span id="c466b815"></span>
### Add custom metrics


* If you want to customize the calculation of the general indicators that have been added, and analyze the calculation results as indicators, you can create **custom indicators** , realize the calculation between indicators, and choose whether to display the atomic indicators at the same time.

* See the configuration example for custom metrics [[Custom indicator] penetration rate calculation](https://docs.byteplus.com/docs/DataFinder/Event_Analysis#0221e4b6).


Detailed operating instructions are as follows.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e1d8641356d64757b7cefdcfca8ef012~tplv-goo7wpa0wc-image.image) </span>


1. First refer to the above steps to add the corresponding regular indicators.

2. Click "+ custom indicator", set the calculation logic of the regular indicator in the custom indicator, the operator supports （+、\-、\*、/、 parentheses, and the parentheses only support one layer), and get the custom indicator expression you want through four operations.

3. Select the precision and unit of the resulting value in the drop\-down box on the right.

4. You can click the Settings button to set whether to "also display atomic metrics".

   * By default, it is not checked, that is, only the added custom metrics are displayed in the query results chart, and the added atomic metrics (general metrics at the top of the page) are not displayed.

   * When checked, the added custom metrics, atomic metrics (general metrics at the top of the page) will be displayed in the query results chart at the same time.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After adding custom metrics, it has the following effects on the resulting charts of subsequent query analysis:</div>



* <div data-tips="true" data-tips-type="warning">When no "custom indicator" is added, the line chart shows the trend change of each event separately.</div>


* <div data-tips="true" data-tips-type="warning">When a custom indicator has been added, click Calculate and the line chart will additionally show the trend of all combined results.</div>


* <div data-tips="true" data-tips-type="warning">When a specific grouping by event attribute is selected, the line chart is displayed in groups according to specific attributes on the above event data logic.</div>



<span id="d56ad31d"></span>
### Add formula metric


* DataFinder provides you with the function of formula indicators, which can configure the calculation logic of formula indicators according to business analysis needs, and supports flexible setting of whether each calculation condition participates in grouping.

* Configuration examples can be found below [[Formula indicator] View the proportion of visiting users who visit links on each page](https://docs.byteplus.com/docs/DataFinder/Event_Analysis#c4675704).


Detailed operating instructions are as follows.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d88fcdb1f3ed43a5b55266c501e8e7ed~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/072f730eb13743de86ed4d204a065bf2~tplv-goo7wpa0wc-image.image) </span>


* The configuration method of the phase formula indicator and the configuration method type of the custom indicator, you can choose the calculation conditions of the indicator and configure the calculation method.

* Compared with custom indicators, formula indicator configuration is more flexible in use, and supports flexible setting of whether each calculation condition participates in grouping.


<span id="afe0151c"></span>
### Tips for indicator configuration

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d9ec3cd07d6b468fa5690043b202febf~tplv-goo7wpa0wc-image.image) </span>


1. Metric renaming.

   After adding the indicator, DataFinder automatically generates the indicator name for you based on the selected indicator events and operators. You can also hover the mouse over the indicator and click the Edit button after the indicator name to rename the indicator for subsequent identification of the indicator.

2. For commonly used configurations, you can quickly solidify and save them as indicators for direct screening next time.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Metric nesting, where a saved metric reappears in another saved metric, is not supported. If the saved custom metric does not appear in the drop\-down metric list, check the metric management page for unrelated metric nesting.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fd5d77e60cf54ca3aa2156c330884597~tplv-goo7wpa0wc-image.image) </span>


<span id="_2-3-细分筛选（曾用名：“全局筛选”）"></span>
## Configure segmentation filtering (formerly "global filtering")

Segmentation screening is mainly used to filter users to determine which users meet the requirements for analysis. For example, users who are selected as "cities are Dongying and Shangqiu, and users are grouped into tests" are analyzed for corresponding indicators.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ba9b87c17a54cf1a67a110958c8854e~tplv-goo7wpa0wc-image.image) </span>


1. Configure primary and secondary filter conditions.

   * Select the first filter condition of the user to be analyzed in the sub\-filter area, and refer to the filter logic details [In-Text Grouping (Segmentation Filtering)](https://docs.byteplus.com/docs/DataFinder/In-Text_Grouping_Segmentation_Filtering).

      * **Attribute filtering** : event attributes, user grouping, user attributes, user tags (such as open), etc. The user group selects the latest one\-day calculation result by default, and can switch the calculation logic by clicking "Latest Data" to specify a certain one\-day result.

      * **Behavior Circle** : Users who have "done/not done/done XX behavior in turn" within the specified time frame.

      * **Dynamic matching** : Filter by dynamically matching events with the crowd at specified intervals.

   * You can click  **+ Attribute Filter**,  **+ Behavior Circle Selection**,  **+ Dynamic Circle Selection** below to add multiple first\-level filter conditions, and the logical relationship between multiple filter conditions can be set to **AND** or **OR**.

   * You can hover the mouse behind the filter to add a secondary filter to the filter. Supports the addition of multiple secondary filter conditions, and the logical relationship between multiple secondary filter conditions can be set to **AND** or **OR**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8a0bb3a1f0344d2387a32746ec2986b3~tplv-goo7wpa0wc-image.image) </span>

2. Add a control group.

   * You can click  **+ control group**, which is equivalent to grouping and comparing the results.

   * Supports the creation of multiple control groups, and replicates created control groups.

3. Other supported operations:

   * Modify the name of each filter group.

      You can click the "small pencil" button after the filter group name to rename the filtered user group for easy memory.

   * Batch entry filter criteria.

      You can click the "small pencil" button after the filter conditions, and enter the filter conditions in batches according to the interface prompts to improve the configuration efficiency.


<span id="_2-4-分组展示"></span>
## Configure attribute grouping

After configuring attribute grouping, the result chart of subsequent query analysis will be grouped and displayed according to the dimension of each attribute value configured, which is convenient for more refined analysis.

For example, when analyzing the distribution of the number of DAUs in different system versions of an app, you can group the DAU number metric by the "system version" attribute of the app. See the configuration example [[Attribute Grouping] View DAU data under different system versions](https://docs.byteplus.com/docs/DataFinder/Event_Analysis#12d77dd9).

The operation instructions are as follows.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d82ded638bce44eb9f0d15d085ee99e7~tplv-goo7wpa0wc-image.image) </span>


1. Click "+ Properties Grouping" and select event properties, user properties, etc. for grouping in the drop\-down box.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Attribute grouping supports grouping by event attributes, user attributes, and user labels, for a total of up to 20 layers of grouping.   </div>
   

2. You can set the query chart to display the top xx grouped query results by the current query condition.

   When there are too many values of the grouped attributes, in order to avoid the fact that too many groupings displayed in the chart make it impossible to perform data analysis efficiently, DataFinder will sort the grouped result attributes, and by default only the grouped result data configured here is displayed in the query result chart.

3. You can set which analysis event metric the grouping applies to.

   See more detail about attribute grouping [Property (Custom) Grouping and Properties](https://docs.byteplus.com/docs/DataFinder/Property_Custom_Grouping_and_Properties).


<span id="2bf5c6c8"></span>
### Filter detailed data

When property grouping is configured, the Property Grouping column supports filtering the specified range of property values in the **detailed data** list at the bottom of the page.

<span id="_2-5-事件分析图表"></span>
## Configure and view result graphs

After completing the configuration of rising indicators and segmentation filters and attribute groupings, you can view a visual chart of the analysis results of the corresponding indicators and adjust them according to your needs.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/093de4d8eb5f48d39ae99c2e2b28d5bb~tplv-goo7wpa0wc-image.image) </span>

<span id="6c0c8600"></span>
### Configure query time granularity and time range

By default, the system automatically displays the statistical results for the past 7 days as a line chart. You can make the following adjustments to the analysis chart as required:


* Set the time granularity of the analysis: 5\-minute, hour, day, week, month;

* The analysis time period and custom time period can be quickly set through the calendar component;

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7f6ad732becc4173a7eb69440096407c~tplv-goo7wpa0wc-image.image) </span>

   * Quick Set Time Instructions

      
      |**granularity** |**Quickly set the analysis time period** |**In the past n..**  |**Latest** (today, this week, this month, etc.) |**Next update** (yesterday, last week, last month, etc.) |
      |---|---|---|---|---|
      |5 minutes |Today, yesterday<br><br>Last 2 days |God |today |Yesterday |
      |hour |Today, yesterday, this week, last week<br><br>Last 2 days, last 7 days |God |today |Yesterday |
      |God |Today, yesterday, this week, last week, this month, last month, this year, last year<br><br>Last 5 days, last 7 days, last 14 days, last 30 days, last 60 days, last 180 days, online so far |God |today |Yesterday |
      |week |This week, last week, this month, last month, this year, last year<br><br>Last 2 weeks, last 4 weeks, last 8 weeks, last 16 weeks, last 50 weeks, last 100 weeks, last 90 days, online so far |God |today |Yesterday |
      |month |This month, last month, this year, last year<br><br>Last February, Last March, Last June, Last December, Last 24 months, Last 90 days, Online so far |God |today |Yesterday |
      

   * Custom setting time description: specific time to yesterday, today, n days ago; n days ago to yesterday, today, n days ago.

* The options that can be compared in time: the previous cycle, the same cycle, the same period last month, the same period last year, and a custom time;

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aae2dfe3592d48eaaafa80962118a175~tplv-goo7wpa0wc-image.image) </span>

   
   |Date |Meaning |
   |---|---|
   |Previous cycle |A period of time preceding end to end |
   |Same period last week |Translate forward one week, corresponding to the order of each week. |
   |Same period last month |Pull forward by one month, corresponding to the monthly order. Considering that the number of days in each month is inconsistent, it is impossible to directly pan one month, so this option is not supported. |
   |Same period last year |The specific strategy is to directly change the year, and then subtract the time interval of the compared time from the end time of the comparison time to obtain the start time of the comparison time. |
   


<span id="78629dca"></span>
### Switch chart type

Event analysis current support shows you: line chart, stack chart, column chart, biaxial chart, ring chart, percentage chart, indicator card. You can switch chart types on demand.

<span id="582e6caa"></span>
#### Line chart

Line charts can be easily used to analyze trending data and are one of the most common analytical charts.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3dcc2258faa04d62b06b9640fa0ae726~tplv-goo7wpa0wc-image.image) </span>


* Hovering over the points on the line chart will show you the detailed values of each indicator.

* Click on the point on the corresponding line chart to display the microscope function. You can choose to create a new date annotation, save as a user group, export users, etc. The scope of microscope functions supported by different time granularities and different analysis criteria is slightly different. The details are subject to the interface. For more detailed microscope functions, see [Microscope Function](https://docs.byteplus.com/docs/DataFinder/Microscope_Function).


<span id="4b1e5b08"></span>
#### Stack chart

Stack charts are particularly well\-suited for analytical needs that require simultaneous observation of **overall trends** and **the evolution of components over time** . It combines the trend expressiveness of area graphs with the structural decomposition ability of stacked graphs.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/437b45db02274fc69d10b5b02bd279ee~tplv-goo7wpa0wc-image.image) </span>

<span id="d1045d47"></span>
#### **Bar chart**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c9c26f1e8b684da3a102a47e9c3fe996~tplv-goo7wpa0wc-image.image) </span>

The indicator of the bar chart is described below.


* When viewing the PV, the column represents the sum of each group PV in the time interval;

* When viewing the UV, the column indicates that the user is deduplicated within the time interval;

* When looking at PV/UV, the corresponding ratio calculation is performed with the above two calculation results of each group;

* When looking for sum by..., add all the values of this attribute in the time interval;

* Check that when finding the average/per capita value by..., use the results of 4 above to calculate the ratio of the results of 1 and 2;

* When looking at deduplicates, the column represents the deduplicate results for the entire time interval.

* When looking at percentiles, the column represents the result of percentiles over the entire time interval.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you want to see a histogram comparing control groups and dates, use the "Stacked Chart" chart style.</div>


<span id="a79a8ccd"></span>
#### Biaxial chart

When analyzing multiple metrics or multiple grouped values, a biaxial graph can be used, and it is supported to configure biaxes to display details.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0cb836b2d95c4145abe17a4b40a03b2c~tplv-goo7wpa0wc-image.image) </span>

<span id="fe8a9a73"></span>
#### Donut chart

Donuts are suitable for analysis scenarios that show the proportion of each category in the overall picture.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bdc08636a3854800821180466d43208e~tplv-goo7wpa0wc-image.image) </span>

<span id="3de48acb"></span>
#### Percentage stack chart

Percentage plots are suitable for analyzing scenarios where the proportion of composition changes across time/grouping.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7954ff4f2b204aeba9b223a7e004cfda~tplv-goo7wpa0wc-image.image) </span>

<span id="d48a6edd"></span>
#### Metric chart

Support to display the analysis results of an indicator in the form of an indicator card. In addition to the indicator result data, support to flexibly tick the same ring ratio data, cumulative value, average value and other data of the indicator in the indicator card.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a87296cd708946a791737521d6219d2e~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When there are multiple indicators, the use of indicator cards for display is currently not supported.</div>


<span id="5c555805"></span>
#### Chart Tips


* Configure chart visualization parameters

   You can click the "Chart Configuration" button at the top right of the chart to configure the visual parameters of the chart in the pop\-up side border, such as whether you need to display the accumulated calculated values in the chart, the sorting method of the chart, the color, etc.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/faff8c6cc90b4217836e00b7fd407346~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0933f4ebfaba4754b4d50d4fa30bf174~tplv-goo7wpa0wc-image.image) </span>

* Zoom the analysis time period to see a finer or more complete chart of the data.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b03fa2ceaaf4c63bd0071a26298575b~tplv-goo7wpa0wc-image.image) </span>


<span id="_2-6-详细数据"></span>
### View and analyze detailed data

Detailed data table showing statistical results.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fc3d341a96f8492e98c8b2381be69355~tplv-goo7wpa0wc-image.image) </span>

The detailed data table supports the following operations:


* Support transpose; after transposing, the indicator name will be displayed in the column; due to the limited number of groups that can be displayed in the table, if there are multiple indicators and multi\-group values, the transposed table will take the first data by default in the configured indicator order. The groupings of indicators are aligned backwards in turn.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c5a17766bdd34ebfa236782918f4b98b~tplv-goo7wpa0wc-image.image) </span>

* Supports setting whether to display growth percentage data.

* Support for sorting events, event attributes, user attributes, and statistical results.

* Support after clicking on detailed data, export users, save as user groups and other operations.


<span id="016527d2"></span>
# The next step: in\-depth analysis

If you wish to perform further in\-depth analysis/data validation on the queried data, currently:


* Export the user information under the current indicator.

* Download the queried structured data as an offline Excel sheet.

* Save the queried result data to the Dashboard board for subsequent daily viewing in the Dashboard board.


<span id="11b18cf3"></span>
## Download/view user information


|In the chart |In detailed data |
|---|---|
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bcbe3bfd971a4380b42bd22309215492~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/72e62f6d5c7a4d6ebfc3937246269fb4~tplv-goo7wpa0wc-image.image) </span> |


<span id="173501fa"></span>
## Download query results as offline data


* It can be downloaded as an excel file.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1d02a467173f4216937b919fe95b7cca~tplv-goo7wpa0wc-image.image) </span>

   When downloading query analysis results, it supports flexible selection of the downloaded data range, and supports selection:

   * **Page Results** : Downloading data directly from the current query results page is a real\-time data download process that downloads data directly to your local computer.

   * **More data** : If you need to download data that is beyond the scope of the page display to select Download "More data", the subsequent DataFinder will create asynchronous download tasks to ensure successful data download. After the task is completed, you will be notified through an in\-app letter. You can download the data locally in the **Project Center** \> **Task Management** \> **Query the task list**.

      See more about asynchronous download tasks [Asynchronous download task description](https://docs.byteplus.com/docs/DataFinder/Query_Task_List#b500e0e0).


<span id="_2-7-保存看板"></span>
## Save analysis results to Dashboard

Click "Save to Dashboard" in the upper right corner to add indicator charts that require long\-term monitoring to the Dashboard board.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e5c11a7f572a44d19f5893be030ac290~tplv-goo7wpa0wc-image.image) </span>


|Parameter |Configuration instructions |
|---|---|
|Chart name |Charts can be renamed for subsequent viewing. |
|Save location |* You can choose to save the diagram to **personal space** or **public space** , more information can be viewed [Dashboard Overview](https://docs.byteplus.com/docs/DataFinder/Dashboard_Overview)in the description of personal and public space.<br><br>* Once selected, you can select the Dashboard path where the chart is saved in the drop\-down box. |
|Chart Type |Select the type of chart to save. Current Event Analysis supports saving query result charts as line charts, stacked charts, column charts, and other types of charts. You can choose which chart to save according to the needs of subsequent Dashboard viewing data.<br><br>For example, the data of the amount class can be saved as "indicator card"; the data of the trend class of uv can be saved as "line chart"; the result data of two events can be selected as "biaxial display", etc. |
|Simultaneous display |* If you want to save to Dashboard, in addition to displaying the chart selected above, you can also display data such as total value, year\-on\-year value, month\-on\-month ratio, etc. in the chart, you can check the configuration box here on demand.<br><br>* Currently supports simultaneous display: total value, latest value, average value, maximum value, minimum value, month\-on\-month, year\-on\-year.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When the chart type is "ring chart", "table", "indicator card", it is not supported to set the data displayed at the same time.   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the chart of the indicator card type needs to display the total, the same ring ratio and other data at the same time, you can check the corresponding data when querying the data, and it will be consistent with your selection results when querying and analyzing when saved to the Dashboard board.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If other types of charts need to display month\-on\-month and year\-on\-year data at the same time, they must first check "Show the latest value" before checking "Show month\-on\-month and year\-on\-year data", because month\-on\-year and year\-on\-year data need to be calculated and displayed based on the latest value.   </div><br>   <br><br><br>For example, after selecting an indicator, the number of new users per fortnight is displayed through the indicator card, and I hope to see the specific month\-on\-month and year\-on\-year changes. After selecting here, the corresponding data will be displayed simultaneously when saved to the Dashboard board, as shown in the figure.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4bd1ada2ace148fb91e9d4b14b6e766b~tplv-goo7wpa0wc-image.image) </span> |


<span id="6f1ffee3"></span>
# Usage example

<span id="31bfd7e5"></span>
## [Configuration metrics] New user data in the last N days

For example, when filtering the number of new users in the last 7 days (excluding today), the configuration example is as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7d37958005c94ea795bb285a5090cc14~tplv-goo7wpa0wc-image.image) </span>

You can use DataFinder's preset properties: **first day access (recommended)**  , **new user** , .

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">It is recommended \*\*to use whether first day access ($is_first_day) \*\*to determine new and old users.</div>


* <div data-tips="true" data-tips-type="tip">Only new and old users (user_is_new) can be used in DataFinder's advanced analysis, and other scenarios try to <strong>not directly use new and old users (user_is_new)</strong> , the data may not meet user expectations.</div>


* <div data-tips="true" data-tips-type="tip">If you need to set the time range flexibly, you can also use the .</div>



<div data-tips="true" data-tips-type="tip">More information on whether to visit on the first day ($is_first_day), new and old users (user_is_new). Please <a href="https://docs.byteplus.com/docs/DataFinder/Statistical_Criteria_Value_Logic#3dac52c5">New and existing users/whether it is relevant on the first day</a></div>


<span id="3a58ee41"></span>
## [Configuration Indicators] DAU data in the last XX days

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b483340eda746078887b615789e26d8~tplv-goo7wpa0wc-image.image) </span>

<span id="f294cf25"></span>
## [Configuration Index] Calculate the stay time pct 95

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/695c2c2da65f4b30a537505c9c4cc5f7~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9922e0d613694b1a9f34083846d80444~tplv-goo7wpa0wc-image.image) </span>

<span id="0221e4b6"></span>
## [Custom indicator] penetration rate calculation

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3cb047bf0a4d4e9997ea743d49f08c47~tplv-goo7wpa0wc-image.image) </span>

<span id="c4675704"></span>
## [Formula indicator] View the proportion of visiting users who visit links on each page


* Example scenarios and analysis objectives

   The access links to a product page include domain1, domain2, domain3,... multiple links. Currently, I want to analyze the proportion of the number of visiting users of each visiting link in the total number of visiting users.

* Configuration example

   
   |Formula indicator configuration example |Group configuration example |
   |---|---|
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71064cb91b8a4cd9b672fa57f38679a2~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/62e523d3a8344033b6890c1df75ffc8e~tplv-goo7wpa0wc-image.image) </span> |
   |Configuration instructions:<br><br>In this analysis scenario, you can use the formula indicator function to calculate the number of page visitors as the calculation condition. The calculation formula is A/B. When viewing the proportion of visiting users of each access link, you only need to set the analysis results to be grouped by access link, and in the formula indicator: the calculation condition A needs to be grouped, and the calculation condition B does not need to be grouped. ||
   


<span id="791d636b"></span>
## [Segmentation Screening] Compare the per capita usage of high, medium and low active users

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/951e6dc55b6f488683e14c725f4126aa~tplv-goo7wpa0wc-image.image) </span>


* Metrics for analysis Select number of app launches per capita

* User segmentation screening:

   * Divided into three control groups, namely high active users, medium active users, low active users

   * Use **behavior circling** for user filtering in each subdivided filtered control group:

      * Circled user behavior: The user has done application launch

      * Circle the time frame: Last 30 days

      * Filter conditions: according to the corresponding control group, filter the application startup days range


<span id="12d77dd9"></span>
## [Attribute Grouping] View DAU data under different system versions

You can see the data situation under different versions, and it will be displayed in order from high to low. At the same time, you can also see how the reported format is, showing the original reported attribute value field. The image below is "System version = X.X.X".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9dd79b8a4ae74248a69580435311c1a3~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a02847f349e44677aa806def2923cf51~tplv-goo7wpa0wc-image.image) </span>

<span id="60a8f197"></span>
## [Same ring ratio] Compare the data of the previous cycle

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d8e9500b015e4bca8a70cad67a97b168~tplv-goo7wpa0wc-image.image) </span>

<span id="5209f641"></span>
# Reference: Intelligent Analysis \- Anomaly Diagnosis

<span id="ec63d2a8"></span>
#### What is an abnormal diagnosis?

When conducting trend analysis, abnormal fluctuations in data provide important clues for us to identify business problems or opportunities. We often judge whether fluctuations are normal based on experience, but we often ignore data that seem normal but do not conform to fluctuations. Through anomaly diagnosis, we can quickly identify these abnormal data and expand the commonly used dimensions, which can help business personnel locate the cause of data fluctuations.


* **How is abnormal data discovered?** 

   With the help of anomaly diagnosis, we will find a periodic pattern based on historical data, predict the range of data that meets this pattern within the query time, and assist users in finding abnormal data to avoid missed opportunities and problems.

* **Is it valuable to expand common dimensions?** 

   Under normal circumstances, after discovering abnormal fluctuations in data, it is often necessary to combine different dimensions and drill down to locate the dimensions that may cause fluctuations. This process is often made very difficult by the plethora of dimensions and the inexperience of analysts.

   In the growth analysis product, by expanding the commonly used dimensions at one time, the dimensions and dimensional combinations with high contribution can be quickly discovered, saving the time of drilling down one dimension after another and lowering the threshold for locating data fluctuations.


<span id="afd04b00"></span>
#### Operating Instructions (New Version)

Since the September 25, 2025 version of DataFinder, the anomaly detection capability has been upgraded and optimized, and the intelligent anomaly attribution analysis capability has been added.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0835cef2a024de19856edf356150df8~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f21f74e849b84ceab9471c9c85c1e0e3~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Currently, this feature is only available for Advanced Analysis \- Event Analysis and Dashboard functions.</div>


* <div data-tips="true" data-tips-type="tip">At present, this function is turned off by default. If you want to use this function, you can contact the BytePlus technical support staff to apply to turn on the function switch.</div>



If you need to use the anomaly detection feature of the new version of Data Query, see how to do it [Data Query Anomaly Detection](https://docs.byteplus.com/docs/DataFinder/Data_Query_Anomaly_Detection).

<span id="87da4c4f"></span>
#### Operating Instructions (Old Version)

**Function activation**

When the product of events and control groups in event analysis does not exceed 10 (e.g. 2 events \* control group 5 = 10, available, 3 events & control group 4 = 12, not available) and the chart type is line chart, the "anomaly diagnosis" function is activated.


|**Chart Type** |**Number of events (including custom metrics) \* Number of control groups** |**Event Attributes + Public Attribute Grouping** |
|---|---|---|
|Line chart |<= 10 |without |


As shown below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42467015a9a745338121732c179fab05~tplv-goo7wpa0wc-image.image) </span>

**Chart area description**

After the abnormal diagnosis function is activated, the system will take the data within the backtracking days for calculation, predict and fit the data within the current query time range and display it in dotted lines. The lighter color ribbon behind the dotted line indicates the expected data range, and the width of the color ribbon is determined by the "confidence interval". The larger the confidence interval value, the higher the tolerance, the more actual data on the solid line will appear in the color ribbon range, and those data points on the solid line that do not appear in the color ribbon range will be marked as "abnormal" points, highlighted in red, and the latitude expansion of the abnormal data can be entered through the microscope function.

As shown below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/975510185a474a768a08b7872a010d68~tplv-goo7wpa0wc-image.image) </span>


* **Parameter setting**

   Confidence intervals and backtracking days can be configured in the drop\-down menu, as shown below:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e3e7a234cbf34bf7844de30c4328a808~tplv-goo7wpa0wc-image.image) </span>

   
   | |Meaning |Value range |
   |---|---|---|
   |Confidence interval |The proportion of data contained within the threshold range to all data |80%\-99%<br><br>Default: 95. |
   |Backtrack days |The number of days earlier than the selected start date, select enough days to calculate a more realistic threshold range. |At least one currently selected date ranges up to 365 days.<br><br>Default: 5 Minute Level: 1 Day (Range: 1, 2) Hour Level: 3 Days (Range: 1 \- 7) Day Level: 60 Days (Range: 1 \- 90) Week Level & Month Level: 180 Days (Range: 1 \- 180) |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the "confidence interval" is 100%, all true data points are not anomalies.   </div>
   

* **Exception tag**

   When Anomaly Diagnostics is activated, the predicted value and the predicted interval value appear in the prompt box of the data point. If the hovering data point happens to have an exception, the "Exception" label will appear in the prompt box.

* **Microscope function and turn\-on abnormal diagnosis**

> The current abnormal diagnosis function is the BETA version, which only supports a single indicator for diagnosis; if you have any suggestions and feedback, please give us feedback.


   1. Click on the abnormal data point, and the microscope function will appear. Through the microscope function, we click to enter the abnormal diagnosis, as shown below:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dd766a4e03154e36bb943283ac93690a~tplv-goo7wpa0wc-image.image) </span>

   2. After entering the abnormal diagnosis, we will see detailed data at the bottom.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">      ```Plain
        * Data will not be displayed in the anomaly diagnosis before clicking through the microscope to enter the anomaly diagnosis;
        * In the dimension details, all metric dimensions included in the "reference value" and "actual value" of query metric data anomalies will be listed. Each page will display 20 dimensions by default, and the number of displayed dimensions can also be reset in the lower right corner (as shown in the figure below).
      ```
            </div>
      

   3. Above the expansion dimension, the basic information of the selected abnormal data, including indicators, reference values, actual values, and differences, can also support the agile search attribute dimension, as shown below:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/999baeacf2f14b8f8b956ca6737d7b88~tplv-goo7wpa0wc-image.image) </span>

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">      ```Plain
        * Search: Support search for attribute dimensions of metrics;
        * Metric: The metrics chosen in event analysis;
        * Reference value: Expected value;
        * Actual value: The actual value of anomaly dot;
        * Difference: The difference between actual value and expected value. 
      ```
            </div>
      

   4. In the expanded dimension, you can choose to "top/untop" and "bottom/cancel" the latitude, and you can choose to open it in a new window.

   5. After the new window opens, you will enter the event analysis viewed by grouping the selected attribute dimensions, allowing for more detailed analysis, as shown below:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/86bf4b212a204bb6abc0149949c16da6~tplv-goo7wpa0wc-image.image) </span>


<span id="_4-事件分析功能视频讲解"></span>
# Reference: Event analysis function video explanation


* <video src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6a812a2ee36ea220a197ffb8689c9db2.mp4" controls></video>


* <video src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f80985fa9997c4f122a9e9e21f7eb6c7.mp4" controls></video>
