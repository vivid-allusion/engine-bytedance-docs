---
title: "Cohorts (User Grouping)"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Cohorts_User_Grouping"
---

The practice of finding and saving users who have had the same attributes or behaviors over a period of time is to group users. User grouping is one of the important support means for fine operation. You can carry out user portrait, fine analysis, and accurate access to the subdivided user group. This article introduces you to the considerations and operational points for creating and using user clusters.

<span id="_1-概念介绍"></span>
# Background information

Typical use cases for user grouping include (but are not limited to):


* Screening specific populations for precise reach, such as defining lost populations and conducting reach recalls;

* Carry out sub\-regional user operations, such as: carry out different operations for first\-line, second\-line and third\-line users;

* Hierarchical division and analysis of users, such as: according to the frequency of use of core functions, users are divided into core users, active users, inactive users, lapsed users, etc., and analyzed separately;

* Targeted grouping of users according to behavioral characteristics, such as: UGC content platform divides users into content creators and content consumers.


<span id="46326edc"></span>
# Create user groups

User grouping supports three creation methods: rule creation, upload file creation, and SQL creation.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db737ca25da04f59b221d8fef4887714~tplv-goo7wpa0wc-image.image) </span>

Click "Create Now" in the corresponding creation method card to create a cluster in the corresponding way on the pop\-up page.

<span id="ec9d7389"></span>
## Creation method 1: Rule creation

That is to create user groups through event filtering, attribute filtering and other conditions, and support the selection of'daily routine 'or'manual update'.


1. Configuration basic information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0985030484ac482b9f46369ce5559346~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Configuration instructions |
   |---|---|
   |Subgroup name |Custom cluster name. |
   |Calculation period |Select what time period to calculate the user clustering results according to the user clustering rules configured below.<br><br><br>* Daily routine: After the user group is created, it will be calculated regularly every day. When selecting a daily routine, you also need to configure the calculation time below.<br><br>   * The calculation time is the "default time": based on the fixed scheduling time of the system, the data of the previous day is routinely calculated every day.<br><br>   * The calculation time is "specified time": You can customize the grouping calculation time according to the actual situation of business data.<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The actual cluster computation time is affected by factors such as the computing resources of the current DataFinder, so the actual computation time may be later than the "specified time" set here.      </div><br>      <br><br>* Manual update: After the user group is created, it will be calculated, and it will not be automatically updated after the calculation is completed. If you need to recalculate, you need to manually click "Update". |
   |Analysis subject |Only users with multi\-principal enabled need to configure, where you can choose in which principal the user grouping is created.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Multi\-subject is an advanced function, which is only open to users who have actively applied for activation, and can only be used by users after SaaS\-cloud native and privatized version 4.5. Please refer to the details <a href="https://docs.byteplus.com/docs/DataFinder/Multi-Application_Multi-Agent_Multi-ID_Type_Overview">Multi\-Application/ Multi\-Agent/ Multi\-ID Type Overview</a>.</div><br> |
   |Statistical caliber |SaaS\-cloud native environment supports setting the statistical caliber of grouping. The default statistical caliber of DataFinder is "user (ssid) ". If you want to statistically analyze data of other calibers, you can first **metadata management** \> **statistical caliber** Create other statistical calibers in the page and set them to be applied in "user grouping". After completion, you can switch here to select other analysis calibers.<br><br>Please see for details [Use statistical criteria](https://docs.byteplus.com/docs/DataFinder/Statistical_Criteria#_3-%E5%8A%9F%E8%83%BD%E4%BD%BF%E7%94%A8).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">At present, SaaS\-cloud\-native environments support the use of multi\-criteria clustering.</div><br> |
   |Grouping description |Custom grouping description. |
   

2. Configure user cluster creation rules.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7daccf3477c147bf9b80e7dc63ee0ea4~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Configuration instructions |
   |---|---|
   |Same time period/different time periods |* Same time period: All filters have the same time period.<br><br>* Different time periods: Customize the time period for each filter.<br><br>* Each time frame only supports selecting 365 consecutive days. |
   |User grouping rule |You can flexibly use a combination of the following rules to filter users in the currently created cluster: "User has done", "User has not done", "User has not done globally", "Users have done in turn", and "User is".<br><br><br>* Each rule supports increasing the filter conditions of the corresponding rule, and the logical relationship between multiple filter conditions supports "AND/OR" switching. As shown in the figure below.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b60d37c0834b422cabd1a502aabfe35b~tplv-goo7wpa0wc-image.image) </span><br><br>* When combining multiple rules, up to two layers of rules are supported, and the outer and inner rules support modifying the logical relationship between the rules, and support "AND/OR" switching.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65c512681d6249f08f7683134a9e91be~tplv-goo7wpa0wc-image.image) </span><br><br><br>For more details on the "user has done", "user has not done", "user has not done it globally", "user has done it in turn", and "user is" rules, please see the following [Reference: User grouping creation logic](https://docs.byteplus.com/docs/DataFinder/Cohorts_User_Grouping#579b6f4b)chapters. |
   |Estimated number of people |Click the refresh icon to immediately calculate the number of people in the current group. |
   


<span id="f4466f79"></span>
## Create method 2: Upload file creation

Create user groups by uploading id list files. When the project has multiple user IDs, you can choose one of them to upload. Please pay attention to keep the uploaded document ID type consistent with the page selection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7594c6dc0ade44aa96d78ed8bdcae4f1~tplv-goo7wpa0wc-image.image) </span>

<span id="b1d3abba"></span>
## Create method 3: SQL creation


1. Configuration basic information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d98719e4a79e405f974987c71209a804~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Configuration instructions |
   |---|---|
   |Subgroup name |Custom cluster name. |
   |Calculation period |Select what time period to calculate the user clustering results according to the user clustering rules configured below.<br><br><br>* Daily routine: After the user group is created, it will be calculated regularly every day. When selecting a daily routine, you also need to configure the calculation time below.<br><br>   * The calculation time is the "default time": based on the fixed scheduling time of the system, the data of the previous day is routinely calculated every day.<br><br>   * The calculation time is "specified time": You can customize the grouping calculation time according to the actual situation of business data.<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The actual cluster computation time is affected by factors such as the computing resources of the current DataFinder, so the actual computation time may be later than the "specified time" set here.      </div><br>      <br><br>* Manual update: After the user group is created, it will be calculated, and it will not be automatically updated after the calculation is completed. If you need to recalculate, you need to manually click "Update". |
   |Analysis subject |where you can choose in which principal the user cluster is created. |
   |Grouping description |Custom grouping description. |
   

2. Configure the creation rules for user clusters through custom SQL.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1eb6b27ca71c4c84a447e28fcf5d3fb1~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Configuration instructions |
   |---|---|
   |Select a time zone |Select the corresponding time zone according to your actual time zone at the top of the configuration box to ensure that the data will not have errors due to time zone problems, and the default is the time zone configured in the first application. |
   |Configuring SQL Rules |Customize the SQL code that creates the cluster in the SQL code box.<br><br><br>* The current SQL rules are defined in a similar way to SQL custom queries. You can query the events table, users table, Items table, cohorts table, and use supported functions. Please refer to the details of the currently supported tables, table fields, functions, etc [Custom SQL Query](https://docs.byteplus.com/docs/DataFinder/Custom_SQL_Query).<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When configuring SQL rules, you must return the " <strong>stat_standard_id</strong> " and " <strong>hash_uid</strong> " fields (user ID fields) to filter users when creating clusters.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">DataFinder will deduplicate the user IDs of the two fields based on the query results of these two fields, and the deduplicated users are the people in the cluster.   </div><br>   <br><br>* Querying data up to 730 days is currently supported; you can also click "  **+ event time** " at the bottom of the code box to define dynamic time parameters for use in SQL rule code.<br><br>* You can click "Format" and "Reset" at the top right to quickly adjust the SQL command format and clear the SQL command.<br><br><br>Configuration example:<br><br><br>* SaaS\-cloud native environment:<br><br>   ```SQL```<br>```   select```<br>```     hash_uid,```<br>```     stat_standard_id```<br>```   from```<br>```     events```<br>```   where```<br>```     event_date >= '2025-07-11'```<br>```     and event_date <= '2025-07-13'```<br>```     and ((event = 'predefine_pageview'))```<br>```   group by```<br>```     hash_uid,```<br>```     stat_standard_id```<br>```   ```<br>    |
   |Estimated number of people |Click the "Estimated Number of People" refresh small icon above to immediately calculate the number of people in groups under the current rules. |
   

3. Once the configuration is complete, click **Save** to save the cluster to the cluster list.

   When saving a cluster, DataFinder will verify your SQL rules. If there are any errors, please follow the interface prompts to modify the SQL rules.


<span id="dedc8960"></span>
# Use clustering after creation


* Analyze sub\-group users. In the user cluster list, find the newly created user cluster, and then:

   * Click "user portrait" to analyze the user profile of the subgroup;

   * Click "View User List" to view the users of the group, and you can check the corresponding attributes to download at the same time;

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65c9c8cae03b462ba56975219707ba7b~tplv-goo7wpa0wc-image.image) </span>

* Use user grouping in other Finder analysis functions. Take the "Event Analysis" function as an example:

   * Enter "Event Analysis" and select the event to analyze.

   * Select the user group in the user filter as the filter criterion.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee9948bf9d9a439eb838148e784c4285~tplv-goo7wpa0wc-image.image) </span>


<span id="_3-1-用户分群列表"></span>
# View, edit, and manage user groups

Here, the following management operations can be performed on user groups:


* If there are many user groups, you can use the "I created" or search function to find user groups.

* Analyze the user groups in the list, as well as download, edit, refresh, copy, delete, and other operations.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/79b232e6c1e34cd28a7404631d3fe854~tplv-goo7wpa0wc-image.image) </span>

* View User List.


After entering the user list, it is pointed out that user attributes are ticked, and downloads are supported at the same time, as shown below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df7e570c174645c8817d2338750898bc~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-历史分群结果"></span>
# Retrospective historical clustering results

<span id="历史回溯（仅规则创建）："></span>
## Historical backtracking (rule creation only)

This feature allows you to retrace the cluster results 7 days after the creation date, in order to quickly understand the historical trends of the cluster.


* The clusters created after 2022\-05\-16, the cluster details page \- list area shows the latest calculation results by default, and supports you to re\-run the data 7 days after the creation date to help you quickly understand the trend of cluster results under this condition.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9e078e26e953481baa094b1a38b3cd30~tplv-goo7wpa0wc-image.image) </span>

* Clusters created before 2022\-05\-16 do not support history backtracking by default.

   * If you need to backtrack the data "7 days after the creation date", please do not modify the clustering conditions and click "Recalculate".

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14930587f3e74dcba4ad3ef5e9f48e31~tplv-goo7wpa0wc-image.image) </span>

   * If you modify the clustering conditions, you can also perform batch recalculation of the clustering of existing historical results (calculated according to the latest conditions).


<span id="历史结果："></span>
## Historical results

The grouping task of rule creation & file upload can view **the calculated historical results of the grouping**.


* The clustered task created by the rule.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ddfcc17b83f43a69eebe896647a3f3c~tplv-goo7wpa0wc-image.image) </span>

   Whether it is a manual update or a daily routine grouping task, you can see in the details page **the actual historical results of the calculation within the selected date range** .

   * **Historical results:**  Take the manually updated grouping task as an example, if the grouping creation date is 2022\-5\-10, and update the excessive group calculation result in the 2022\-5\-12, in the grouping details, only the calculation data of 5\-10 & 5\-12 is recorded.

   * **Multiple calculations on the same day:**  If you perform multiple calculations on the cluster on the natural day, only the last calculation result will be retained (for example, on the day of 5\-12, 3 recalculations have been generated, and the system only retains the last calculation result on the day).

   * **View the user list** : Click to jump to the user review to view the subgroup user list.

   * **Recalculate** : After clicking, recalculate according to the latest calculation conditions of the subgroup.

   * **Download** : Then download according to the latest results.

* Grouping tasks for file uploads

   On the details page, you can see **the actual historical results of the calculation within the selected date range**; and support'view user list 'and'download' grouping.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ddfcc17b83f43a69eebe896647a3f3c~tplv-goo7wpa0wc-image.image) </span>


<span id="579b6f4b"></span>
# Reference: User grouping creation logic

<span id="8af69362"></span>
## **Cluster creation rule description**


|**Rule condition** |**Explain** |||
|---|---|---|---|
|User did |In the total number of users (the default is active users in the past year), filter out the users who have done something a specified number of times within a specified time frame.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When circling with "user done", in the filter rule, you need to ensure that the number of times the user has done an event is \> 1, and the result of circling is empty when the number of times = 0 or the number of times < 1.</div><br><br><br>**Calculation conditions** :<br><br><br>* Total number of times: The total number of times the event occurred<br><br>* Daily number: The total number of times the event occurs per day<br><br>* Day distribution: The distribution of the number of days that the user triggered the event<br><br>* Consecutive days: The number of consecutive days that the user triggered the event<br><br>* Sum/Maximize/Minimize/Average/Deduplicate by<br><br><br>**Value range** :<br><br>equal to, greater than, greater than or equal to, less than, less than or equal to, or interval<br><br>**Example** :<br><br>We have 100 active users in the past year. In the past seven days, 10 people have had the behavior of [starting the app 100 times], and 20 people have had the behavior of [starting the app 50 times], then:<br><br><br>* There are 10 users who meet the requirements of [In the past 7 days, users have launched the app more than 70 times].<br><br>* There are 30 users who meet the requirements of [In the past 7 days, users have launched the app more than 30 times]. |||
|The user has not done it. |In the total number of users (default is active users in the past year), remove (not in) users who have done something within the specified time frame.<br><br>**Example** :<br><br>We have 100 active users in the past year. In the past seven days, 10 people have had the behavior of [starting the app], and 90 users meet the requirements of [users have not started the app in the past 7 days]. |||
|The user has not done it globally. |In all objects (including users who have not had any events), remove (not in) users who have done something within the specified time frame.<br><br>**Example** :<br><br>There are 100 global users, of which 10 have engaged in arbitrary behavior and 3 have done the behavior of [Launch App in the past 7 days], and 97 users meet the requirements of [Launch App in the past 7 days, the global has not done it]. |||
|Users did it in turn |Specifies a sequence of event behaviors that will be selected only if the user fires these events in sequence. |||
|User is |Support for selecting user attributes, user groups, and user labels (the latest value is selected by default).<br><br>**Value range**:<br><br>equal to, not equal to, contain, do not contain, empty, not empty, custom include, regular match |||


<span id="d475edeb"></span>
## Time of grouping computation


* At present, the system will start routine calculation and grouping at 6 o'clock every day, and usually complete a calculation before 8 o'clock.

* If'today 'is included in the grouping time condition, real\-time calculation will be triggered when the first calculation & refresh is performed; the daily routine task only calculates the data of t\-1 days.


Current clustering computing strategies ensure that users are as up\-to\-date as possible when using clustering.

<span id="b9e496a8"></span>
## Calculation time of static grouping


* If your clustering condition contains only static time (such as 2022.1.1 \- 2022.2.1), the calculation only supports manual updates.

* If you don't need to update the cluster results daily, you can also choose to update them manually.


<span id="8f470fd6"></span>
## Cluster calculation logic change description

Cluster calculation logic changes, please pay attention to:


1. Calculation logic change description

   * When the condition is "the user is the province is not equal to Jiangsu" (the province is the attribute that calculates all values), only the users whose provinces are not equal to Jiangsu in the time range are calculated. (Previously, the rules would also include users who have reported data in the past 1 year but have not reported data in the query range)

   * When the condition is "User has done event A less than 3 times", the query result is that users who have done event A equal to 2 or 1 times among active users, and users who have done event A 0 times are not counted. (The old version will count non\-DAUs. If you need to cover this part of the user, you can add "User has not done event A")

2. Adjustment impact

   * Clusters created/updated before February 9, 23 are still calculated according to the old rules. If the historical version of the cluster needs to be calculated according to the new rules, you can click "Recalculate"; the updated version from February 9 is calculated according to the new rules.

   * Clusters created/updated after 9/2/23 are all calculated according to the new rules.


<span id="5ba4c378"></span>
# Usage example

<span id="be4045a1"></span>
## [Low Active Users] Circle selection example

In the daily operation process of content products, manual re\-engagement is required through some operations, so operation students often need to find "low\-active" users for operation actions. Re\-engagement is generally aimed at two types of users, one is users with low activity frequency in the past 7/14 days, which can directly send push messages to recent popular content to promote such customers to open recommended content; the other is nearly 7/14 days Not active, but the previous period was active lapsed users can send text messages with stronger incentives such as friend comments or like records to attract users to return.

The low\-frequency user circling logic is relatively simple, and it is only necessary to select the number of times the user triggers the target event within a specified time to be less than or equal to a certain value:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8bb51bd82fef4375b4a5bbbea72a5158~tplv-goo7wpa0wc-image.image) </span>

Lapsed users involve different time periods and need to be logically combined with undone logic:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02e40a8d16ba49649360d621b9ff3c35~tplv-goo7wpa0wc-image.image) </span>

<span id="1786d804"></span>
## [Recall dormant users] I have used it in the last 30 days but not in the last 7 days

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e4e56b6fde1444c8bfa6db5bd5dc84a5~tplv-goo7wpa0wc-image.image) </span>

<span id="f91474c5"></span>
## [Users have done it in a row] I have done it in the last 30 days. Open the app first and then search...

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9a8122635e14949a999abda766cd260~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-常见问题"></span>
# Common problem

<span id="_3-4-1-为什么有的分析图表旁提示我“所选择-用户分群-不支持今日实时数据分析”？"></span>
### Q1 Why do some analysis charts prompt me "The selected" user segmentation "does not support today's real\-time data analytics"?

When the condition includes user grouping, we temporarily do not support the calculation of the data of the day together.

<span id="_3-4-2-为什么选择平台是-ios-或-android-的访问次数大于5次的用户时的结果要大于分别查询平台是-ios-和-android-的数量之和？"></span>
### Q2 Why is the result of choosing a platform that is iOS or a user with more than 5 visits to Android greater than the sum of the number of queries that the platform is iOS and Android respectively?

Because some users are using both iOS and Android. The two devices were used less than five times each, but adding them together was just over five times. Then the user will be included in the cluster.

<span id="_3-4-3-打开导出用户id的文件，为什么用户id是以科学计数法表示，如何才能正确展示？"></span>
### Q3 Open the file that exports the user ID. Why is the user ID represented by scientific notation, and how can it be displayed correctly?

The file for exporting the user ID is in CSV format. It may be opened with Excel or WPS by default on your computer. After opening it, you will see that the value of the user ID is displayed in scientific notation, and the original value cannot be restored. As shown in the following figure:

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_71db2cefa66ae3c25bfc35eb6f365ee1) </span>

The reason for this problem is that when Excel and WPS open CSV, they automatically convert long numbers into scientific notation and save them as strings. This conversion is irreversible, so the original value of the number cannot be restored.

**Solution**

**Option 1: Import CSV directly into Excel**

Through the import function of Excel, the data format of the column containing the super\-long value is changed to "text" in the import process, which can be displayed correctly. If your Mac Excel version is 16.59, you may not be able to correctly recognize the content of the CSV due to known issues with Excel.

Mac Excel example


1. Create a blank Excel document.

2. Click `File > Import`and select the csv file you just downloaded;

3. In the second step, select "comma" as the separator.

4. In the third step, select "Text" in the `column data format`, and select "User ID" column in the `preview selected data`(black when selected);

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac5208751bb243f886ce4ae60bae67b8~tplv-goo7wpa0wc-image.image) </span>

5. Click `Finish`and complete the next steps by default;


As shown in the figure below, the A column imported according to the above steps can be directly displayed as the correct content.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_3e091b59ed63eb5db4d1dd825786ee34.png) </span>

**Option 2: Import through the Excel "Get Data" function**

Mac Excel example


1. Create a blank Excel document.

2. Click "Data" \> "Get Data" and select the data source of "Text/csv".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/05999e5f0b774f6ea08b4f5c61a179ae~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_bcf90cf53dbd6abd0104666593e66fa3.jpg) </span>

3. Click "Browse" and select the CSV file you just downloaded.

4. Preview file data, the default file raw format is (UTF\-8), delimiters are commas, and data type monitoring is based on the first 200 lines.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_dcac0e7c837b4bc12172cd0508d7991e.jpg) </span>

5. Click Load to complete the data import.


**Option 3: Open it through other software first and save the Excel format**

MacOS Numbers, Lark documents, or text editors do not automatically convert extremely long numbers. You can use these software to open CSV, then save the file to Excel format, and then open it with Excel or WPS to display it correctly.

This situation is also more convenient for small files. But if the file is large and slow to process, consider importing it directly into Excel.
