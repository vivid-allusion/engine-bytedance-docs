---
title: "User Lifecycle"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/User_Lifecycle"
---

<span id="_1-概念介绍"></span>
# Concept introduction

After we acquire users through different growth methods, we consider that the user's lifecycle begins when the user opens the app for the first time (acquiring new users), and we consider that the user churns after the last time the user opens the app (lapsed user). The operational goal of conventional Internet products is to analyze the user's behavior characteristics during the life cycle in as much detail as possible, extend the cycle time as much as possible, and maximize the value of business objectives within this cycle time. Therefore, we have a detailed analysis function related to the "user lifecycle".


* User life cycle: It can be understood as the time from the first time the user opens the product to the last time the user opens the product.

* In DataFinder's user lifecycle tool, you can perform user lifecycle analysis for specified events, that is, analyze the data of the user's entire lifecycle from first occurrence to churn to return for a specific event.


When using DataFinder for user lifecycle analysis, you need to understand the following core concepts in conjunction with the operational configuration interface.


|Concept |Concept note |Example |
|---|---|---|
|**Time Range** & **Time Interval**<br><br>( **Current period** & **previous period** ) |When using DataFinder for user lifecycle analysis, you need to configure the time frame for data analytics and specify the interval at which this time frame is divided into multiple time periods. |For example, configure the analysis 2026.07.06 to 2026.07.12 the data in this time range, and the time interval of the breakdown time period is 2 days:<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a75576139dc4892a32004f1f8387f34~tplv-goo7wpa0wc-image.image) </span><br><br><br>* The subsequent query and analysis results of user life cycle data will be divided into three sub\-time periods: 07\-06~ 07\-07, 07\-08~ 07\-09, and 07\-10~ 07\-11, 07\-12~07\-12.<br><br>* Taking the 07\-08~ 07\-09 cycle as an example, the data for this period is the data for 07\-08~ 07\-09, and the data for the previous period is the data for 07\-06~ 07\-07. |
|**Active user** |* In a segmented time period, the user who triggered the indicator event is the active user in the current period.<br><br>* Active users can be further divided into new users, retained users, and returned users. |For example, when the indicator event configured for the user lifecycle configuration is "Page Visit", the active users in the 07\-06\-07\-07 timeframe are all users who triggered the "Page Visit" event within the 07\-06\-07\-07 timeframe. |
|**New user** |In a segment of active users in the time period, the user attributes user_is_new to determine whether the user is a new user.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">DataFinder provides you with preset user properties to determine whether a user is a new user: user_is_new, when configuring user lifecycle analysis, you need to configure indicator events. During the query analysis process, DataFinder will automatically query all new users who triggered the corresponding event through the preset user properties.</div><br> |For example, a new user in the 07\-06 to 07\-07 timeframe is a user who meets the following conditions at the same time:<br><br><br>* The "Page Visit" event was triggered within the time range of 07\-06~ 07\-07<br><br>* User properties user_is_new the result is the user of the new user |
|**Retained user** |Users who were active users in the previous time period and are also active users in the current time period. |For example, an active user during the 07\-08 to 07\-09 timeframe is:<br><br><br>* Active user in the previous period (07\-06~ 07\-07)<br><br>* Also an active user during the current period (07\-08~ 07\-09) |
|**Lapsed user** |Users who were active users in the previous time period but are not active users in the current time period. |For example, a lapsed user in the 07\-08~ 07\-09 timeframe is:<br><br><br>* Active user in the previous period (07\-06~ 07\-07)<br><br>* Not an active user during the current period (07\-08~ 07\-09) |
|**Returned user** |Users who were inactive in the previous time period and are active in the current time period (excluding new users). |For example, the returned user in the 07\-08~ 07\-09 time period is:<br><br><br>* Not an active user in the previous period (07\-06~ 07\-07)<br><br>* Active users who are not new users during the current period (07\-08~ 07\-09)<br><br>   * Active users during the current period (07\-08~ 07\-09)<br><br>   * Not a new user in this period (07\-08~ 07\-09) |


<span id="_2-快速入门"></span>
# Application scenario


* It can monitor daily active users and quickly locate the groups and causes that affect the rise and fall of DAU.

* Can be split lapsed user, locate the type of lapsed user;

* You can select a period of lapsed users to create user groups;

   * Segmented user characteristics can be found through component analysis

   * User behavior can be viewed through behavioral scrutiny

* You can view the proportion of new users, retained users, and returned users, and observe the recent pull\-in, retention, and recall;

* You can view the subsequent retention of returned users, lapsed user behavior before the loss, and push users with different active levels and re\-engage churned users;

* You can view the number of deduplicated statistics users for an event that occurred in any 30\-day period.


<span id="_2-2-使用过程示例"></span>
# Operation steps


1. After logging into the DataFinder console, select **Analytics Tools \> Advanced Analytics \> User Lifecycle** in the top navigation bar to enter the User Lifecycle page.

2. Configure metrics and segmentation filters.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b67429d0c7c54261bb707ac322f1faf8~tplv-goo7wpa0wc-image.image) </span>

   * Configuration metrics: According to the needs of business analysis, select the specific event of the user's life cycle analysis, that is, analyze the data of the whole life cycle of the user from the first occurrence, to the churn, to the return for a specific event. Supports configuring filters for selected events.

   * Configuration segmentation screening: Comprehensive use of segmentation screening capabilities can achieve more complex crowd segmentation and filtering screening, you can refer to " [In-Text Grouping (Segmentation Filtering)](https://docs.byteplus.com/docs/DataFinder/In-Text_Grouping_Segmentation_Filtering)" .

3. Configure the time range and interval of data analytics and view the corresponding data charts and detailed data tables.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/62f76e7eb4344e7d96d4cd9b9d0ab4bf~tplv-goo7wpa0wc-image.image) </span>

   * Support to select the time range to be analyzed by day or month, and divide the time range into multiple time periods according to the configured time interval.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Currently, it supports querying data for up to 4 months. If you choose a time frame that exceeds the maximum time limit, the query results will automatically adjust the time frame for you.      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1998f62aed8c457a8dcd7272dcab92cf~tplv-goo7wpa0wc-image.image" width="2080px" />      </div>
      

   * You can click toggle in the upper right corner of the chart to view the numerical distribution or the proportion distribution.

   * Or toggle at the top of the ratio to view detailed data for active users, or lapsed user detailed data.

4. The query results are further analyzed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe7478248a2d448cac893f0952d53a4e~tplv-goo7wpa0wc-image.image) </span>

   Click on the query results in the corresponding chart area to further analyze and process the query results, such as saving as user grouping, exporting user IDs, etc. Please refer to this section for details [Microscope Function](https://docs.byteplus.com/docs/DataFinder/Microscope_Function).


<span id="0c96dd99"></span>
# View chart details

<span id="活跃用户"></span>
## View active users

The number and proportion of active users (new users, retained users, returned users) during the current time interval, as well as the number and proportion of lapsed users between the two time intervals, are graphed in two ways, as follows:


* **Numerical distribution map**

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b1ccf890e5194336be288cb5e0ef3490~tplv-goo7wpa0wc-image.image) </span>

* **Proportion distribution map**

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4fb25f82c9a04fcfaa4ebec474f3f14f~tplv-goo7wpa0wc-image.image) </span>

   **The calculation logic of the proportion distribution map:** 

   * Proportion of new users: Number of new users in the current period/Number of active users in the current period \* 100%

   * Retained users: Number of retained users in the current period/Number of active users in the current period \* 100%

   * Percentage of returned users: Number of returned users in the current period/Number of active users in the current period \* 100%

   * Percentage of lapsed users: Number of lapsed users in the current period/Number of active users in the previous period \* 100%


<span id="流失用户"></span>
## View lapsed users

The distribution of new users, retained users, and returned users in lapsed users during the current time interval. Similarly, there are also two forms of chart presentation, as shown in the following figure:


* **Numerical distribution map**

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a4b2edae9dc342bdb77931a018b06a3b~tplv-goo7wpa0wc-image.image) </span>

* **Proportion distribution map**

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5cae1ebdcee40a7b5ea0647b8dec3e6~tplv-goo7wpa0wc-image.image) </span>


**Result data calculation logic:** 


* Loss of new users: the number of new lapsed users in the current period

* Loss of retained users: the number of lapsed users in the current period and retained users in the previous period

* Lapsed returned users: The number of lapsed users in the current period and returned users in the previous period

* Percentage of new users lost: the number of new users in the previous lapsed user in this period/the lapsed user in this period \* 100%

* Percentage of retained users: number of lapsed users in the current period/lapsed users in the current period \* 100%

* Percentage of returned users: number of lapsed users in the current period returned users/lapsed users in the current period \* 100%


<span id="_3-4-详细数据"></span>
## View detailed data

You can view the detailed data table for active/lapsed users below.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cafccd11cca54e4f93d95e334c31000b~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-用户生命周期视频讲解"></span>
# Video explanation

<video src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3738badbb096a8dc84e847e5207a0641.mp4" controls></video>
