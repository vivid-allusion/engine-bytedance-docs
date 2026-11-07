---
title: "Query Analysis & Analysis Metrics"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Query_Analysis_Analysis_Metrics"
---

<span id="45199b10"></span>
# Metrics configuration and calculation logic consulting

<span id="bf568686"></span>
## Do you currently support event tracking event combinations to calculate comprehensive metrics? For example (B + C) deduplicate /A

You can use the virtual event function, B and C are our two different paid events, A is the total number of starters, calculated by the virtual event indicator event (B + C) deduplicate /A.

<span id="c5241df8"></span>
## How to merge and view several related events?


* Events are OR relationships \-\- virtual events.

   In "virtual events", you can combine multiple events in BytePlus Growth Analysis into virtual events through certain logical relationships, which is convenient for users to manage and view the combination of regular composite events. View the [Virtual Events](https://docs.byteplus.com/docs/DataFinder/Virtual_Events) help documentation specifically;

* It's an AND relationship \-\- a combination metric.

   In the event analysis function, you can create "composite metrics" to calculate between events and present the calculated results.


For event analysis related content, please refer to ([Event Analysis](https://docs.byteplus.com/docs/DataFinder/Event_Analysis)) help documentation.

<span id="f29d910f"></span>
## How to calculate the average screen time per month for the web?

On the web side, you can use the page closed or the page active to see the specific average screen time, refer to the documentation for details: [Web/JS SDK Classification Function](https://docs.byteplus.com/docs/DataFinder/Web_JS_SDK_Classification_Function).

<span id="e7ded05b"></span>
## How can I check the IP address of the visiting user in BytePlus Growth Analysis?

You can see through [User Details](https://docs.byteplus.com/docs/DataFinder/User_Details) the function that in the corresponding user's behavior flow, the value corresponding to the "client_ip" field is the user's IP.

<span id="16cd9469"></span>
## How can I count the average daily visit time of all users in the Finder?

Since the Finder's Session analysis function does not support adding custom metrics directly, it is not possible to directly query the daily average access time. It can be converted through the following steps:


1. Calculate the total session duration.

2. Calculate the total number of people.

3. Divide the total session duration by the total number of people to get the per capita visit duration.


<span id="be1d50ec"></span>
## In a custom SQL query, how do I calculate the number of uses in the last 30 days, especially the number of uses in the last day?


1. Query an example of SQL used in the past 30 days:


```sql
select
    sum(b.ac)
from
    (
        select
            a.event_date as event_date,
            a.used_events as used_events,
            arraySum(
                arrayMap(x -> if(x = 'app_launch', 1, 0), a.used_events)
            ) as ac
        from
            (
                select
                    event_date,
                    JSONExtract(
                        JSONExtractRaw(content, 'string_array_params'),
                        'used_events',
                        'Array(Nullable(String))'
                    ) as used_events
                from
                    rangers.events_all
                where
                    app_id = 666666
                    and event = 'event_param_using'
                    and event_date >= '2024-08-01'
                    and event_date <= '2024-08-30'
            ) a
    ) b;
```



2. To find the number of times you used the previous day, simply modify the date range and add the corresponding event name.

3. When customizing a query, it is recommended not to use `select *`, `group by`multiple key values and other performance\-consuming query conditions, limit the `event_date`time range within 30 days, and reduce the query frequency to avoid the impact on system performance.

4. Queries in the past 30 days (events and attributes support statistics on the number of queries on the Finder platform in the last 30 days, including Kanban, virtual events, and all analysis modules (Finder only).

5. Virtual events and events queried by Kanban will be counted.


<span id="79937661"></span>
# Segmentation filtering and grouping

<span id="7836656a"></span>
## When doing attribute screening, I hope to be able to classify channels so that I can directly filter to the corresponding classification when screening, and when screening mobile ends (such as oppo, vivo), I can filter them at one time without checking them one by one. How to achieve?

You can use properties to customize the grouping feature, for details, see [Property (Custom) Grouping and Properties](https://docs.byteplus.com/docs/DataFinder/Property_Custom_Grouping_and_Properties).

<span id="9add01de"></span>
## I want to group an event indicator according to attribute A, and sum attribute B in each group. How can I achieve this?

You can configure attribute B summation of events when event analysis, filtering an event metric, and then use attribute A to group when configuring attribute grouping of subdivision filtering.

<span id="60685eb4"></span>
# Advanced Analysis

<span id="2acb01b1"></span>
## Event analysis

<span id="_1、事件分析为什么没有日期对比按钮？"></span>
### Why is there no date comparison button for event analysis?

The use of date comparison function needs to meet: 1. It must be a line chart 2. It cannot be in the abnormal detection state 3. It cannot be set to remove weekends.

<span id="dd5c99dd"></span>
### What is the calculation logic for the total number of people in the event analysis?

The total count is the number of people who happened the event, and the total is deduplicated according to the ssid dimension.

<span id="6b4089ce"></span>
### In the event analysis, when the "Download Data" button is clicked multiple times, will the downloaded data later be cached with the previously queried data?

Whether it is real\-time data or offline data, when you click Download, you will restart the query, and the cache that has been checked before will not be used.

<span id="78943a30"></span>
### Event analysis According to the condition that the mobile phone is not empty, it is found that there are still users with the mobile phone number "\-" grouped according to the mobile phone number

This "\-" means empty string, and empty string is also considered to have a value.

<span id="2f494a36"></span>
### When viewing UV data on the event analysis page, what is the reason why the data displayed by clicking to view the user list is inconsistent with the data in the query result?


* Problem scenario:

   For example, there is more than 30,000,000 query result data when viewing user UV data on the event analysis page:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/61a5defa2a0843ed9caffc1532cd1a14~tplv-goo7wpa0wc-image.image) </span>

   However, when you click to view the user list, there are only over 80 pieces of data left:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0160d93ee5c7483fa93873f42eb23d33~tplv-goo7wpa0wc-image.image) </span>

* Possible reason: When using row\-to\-column transposition, the total data does not have a specific date, so the user query time in the user list is the date of the day.


<span id="085c4f77"></span>
## Custom Retention analysis

<span id="5fa6543b"></span>
### Why is it that the number of events that day has increased, but the retention of the next day has decreased?


* From a computational perspective, the Day Retention Ratio at Day 1 is influenced by the number of event visits the following day. The simple formula for the Day Retention Ratio at Day 1 can be equivalent to: (number of return visits on the second day)/(number of all visitors on the day). The increase in the number of events on that day may be due to the increase in the number of visits from new users due to the customer's arrangement of new activities (the magnitude of the denominator increases), but there is no corresponding activity on the next day to ensure the retention rate of new users, resulting in a decrease in the number of return visits on the next day (molecular decrease). The chart shows that the Day Retention Ratio at Day 1 fell significantly.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/93fad96d91c54dbf93ee27db346445d2~tplv-goo7wpa0wc-image.image) </span>

* From a business logic perspective, the increase in the number of events caused by the customer's activities on that day was mainly due to the increase in new users, with lower user stickiness and fewer new users returning the next day, resulting in a decrease in the Day Retention Ratio at Day 1.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02b0a67580a84f1ca39a8489dfd40003~tplv-goo7wpa0wc-image.image) </span>


<span id="2d494f91"></span>
## Funnel analysis

<span id="ceca7551"></span>
### Attribute Grouping Logic for Transformation Analysis?

Applied to all groupings, the result is the same as the attribute grouping applied to the first event. It will only calculate conversions by grouping the properties of the first event, and will not group the other event property values in the conversion chain when calculating conversions.

<span id="f00fbf21"></span>
## Distribution analysis

<span id="2218c52b"></span>
### Why is distributed analysis so slow?

If the distribution range of distribution analysis is not selected, the shortcut option \- default will be used to query, which is time\-consuming due to the large number of queries. You can choose a custom interval or an aliquot to bypass.

<span id="9b376c6d"></span>
## User path

<span id="c90f7869"></span>
### Why doesn't the user path support analysis principal switching?


1. The user path is mainly analyzed by human calculation, so the data of other subjects will not be calculated, which is in line with expectations.

2. You can consider selecting the specific computing application id by subdivision filtering to limit the scope of calculation

    &nbsp;


<span id="heat-map-analysis"></span>
## Heat map analysis

<span id="_6、finder只接入了小程序，高级分析里没有“热力图分析”模块"></span>
### Finder only connects to the Mini Program, and there is no "heat map analysis" module in the advanced analysis

When only the Mini Program is connected and no events from other terminals are reported, the heat map now does not support the use of the Mini Program application.

<span id="a478121b"></span>
### What is the meaning of heat map histogram clicks and why is there an empty histogram displayed?

The histogram display data is to view the distribution of elements by the number of clicks, click on the corresponding bar diagram of the element, and the corresponding element will be highlighted in the heat map below. Empty is because if the target of the click is a non\-text content like the picture, and then there is no circling event, empty will be displayed. For customers, you can add the circling event to the key elements, but there is no guarantee that there is no empty in this histogram.

<span id="00c9d6d9"></span>
### Heat map is not displayed, filter click event has data, why?

There is a high probability that the reason is that the heat map does not support viewing the heat map of non\-HTTPS sites in the finder due to browser security policy factors. It is recommended to use https or view it on the original page.

<span id="6a1273a7"></span>
### The heat map has been unable to load, and it has been loading after clicking on the chart?

The heat map function page has data such as the number of people and the number of views. After clicking "Open on the original page" to jump, there is no obvious data. It may be because the page is not allowed to be embedded in an iframe. The solution is to open the heat map function page. If the heat map event tracking page needs to be logged in, click the small eye to close the heat map, and then check it again after logging in on the login page.

<span id="2aec5e27"></span>
### App embedded H5 scene, create heat map analysis, there is no element click data what is the reason?

Heat map currently does not support data collection in the H5 scenario embedded in the app. The reason is that the embedded H5 adds an extra '/\*' logic at the end of the path when collecting the element path, resulting in problems when the heat map queries the element path.

<span id="_7、事件分析中的总人数的计算逻辑是什么？"></span>
## LTV analysis

<span id="_9、ltv的计算逻辑"></span>
### Computational Logic of LTV

The calculation logic of LTV is as follows:

LTV per capita on a given day LTVn = the amount spent by the daily news user in the following n days/the number of daily news users

The numerator is: the sum of the payment amounts that triggered "payment" within n days for new users who triggered "application launch" on that day

The denominator is: new users who triggered "app launch" on that day

<span id="8f74e297"></span>
## Custom SQL query

<span id="a3fdcbe0"></span>
### Advanced Analysis \- \> Custom SQL Query, what does the hash_uid in the events table mean and what is the use? [How to generate hash_uid? What's the use?]

Generate method: The generated method is the hash value calculated by combining user_id and app_id with cityhash, hash_uid = cityhash ("< app_id \>:")

Field function: hash_uid is a user id field, which is used for transaction table and user table join. Since hash_uid is a numerical type, it can effectively improve performance when using hash_uid association.

<span id="f0ec03ef"></span>
### Can virtual events be found in the data table of custom SQL?

Virtual events are only logically constructed when participating in analysis and are not saved as entities, so querying in custom SQL is not supported

<span id="9c481926"></span>
### How to query the dictionary value of a property configuration?

All values can be found by SQL query property names without specifying a version. If you need to specify a version, you need to use version to find the latest dictionary value. In addition, if there is a situation like the wrong appid, you can first confirm whether the appid is correct, or check whether the app_id in the metadata table is maintained according to the project granularity.

<span id="70a8139d"></span>
### Does Custom SQL query support querying event_date as function parameters?

Currently not supported Querying event_date as function parameters is not supported. If necessary, the query can be nested in the outer layer to achieve. The specific query example is as follows:

```SQL
select t1.user_id, count(t1.aa) as bb from (
    select  user_id,event_date as aa  
           from events
           where  event_date <= '2024-05-29'
           limit 500
) t1 group by t1.user_id
```


<span id="7342d160"></span>
### Custom SQL query, prompt column does not exist?

Check whether the prefix of the table name is added in the query SQL, for example, if the data you need to query is in the `user_profiles`table, then the query SQL needs to have a `user_profiles`prefix, as follows.

```SQL
SELECT user_id, last_active_date, user_profiles.verificationState
FROM users
WHERE user_id = '4d0fb2c2-9c1d-44ac-aac7-3d23630f7c49'
    AND last_active_date >= '2024-01-01'
    AND last_active_date <= '2024-12-31';
```


<span id="f96b8a6a"></span>
### What is the reason for the Custom SQL query zoneId error?


1. Check whether the format of the Custom SQL query is correct

2. Check whether the toDateTime function is used in the Custom SQL query . The argument to the toDateTime function requires time zone information. For example, toDateTime (event_time, 'Asia/Shanghai')

    &nbsp;


<span id="in-a-custom-sql-query-when-group-by-userid-is-added-the-data-cannot-be-queried-after-removing-group-by-it-can-be-queried-normally"></span>
### In a custom SQL query, when group by userID is added, the data cannot be queried. After removing group by, it can be queried normally.

This query method is not currently supported. Bypass scheme: You can try to store these users as a cluster, and then use this cluster to query when customizing SQL.

<span id="b5702ff5"></span>
### In a custom SQL query, prompt "device_id doesn't exist, Please check your SQL query" when using the `$is_login`field?

In a SaaS\-non\-cloud native environment, the above error may occur because the `device_id`field is disabled in the query because of the privacy risk. You can query using the `bddid`field, `which`is the encrypted version of `device_id`. Use the `bddid`field directly in the SQL query.

<span id="9c10f758"></span>
### When using custom SQL statistics usage, why do I find that the exported data does not match the actual usage? What is the daily usage of SQL queries?

Existing usage statistics caliber (relatively accurate):

```SQL
event not in ('_be_active','bav_scheme','bav2b_monitor','bav2b_sdk_init_cost','bav2b_sdk_start_cost','bav2b_sdk_register_cost','bav2b_sdk_active_cost','bav2b_sdk_logsetting_cost','bav2b_sdk_abtest_cost','tt_fetch_did_error','stream_req_stat_channel','stream_req_stat_feed','bav_replay' )
-- (This condition is mainly for background code statistics, custom SQL does not have this field, and the data accounts for less) and (int_params {'$source_id'} = -1 or int_params {'$source_id'} is null)
```


Note: source_id is the background calculation logic, and SQL custom queries are not supported for the time being. The dosage caliber is subject to the latest official explanation. There may be scenarios of subsequent adjustments (such as new product events). The logic may not be completely equivalent to the results obtained by the above SQL. It is recommended that the details of the application event volume under the group information function shall prevail.

<span id="9daa9652"></span>
### After a property is desensitized, can't you use SQL functions to filter the property in custom SQL?

The desensitized data should not be allowed to support SQL function queries, otherwise the desensitized content can be intercepted through the function, and the meaning of desensitization will be lost. Therefore, when the SQL query has been desensitized, an error will be reported and the function cannot be used.

<span id="194f2f28"></span>
### When using a Custom SQL query to User_tags the user label table, the result is found to be empty, but on the page it is actually directly looking at the user label with data.

Custom SQL query usertags table, do not support user_tags.xxx way to customize the query, subsequent versions to query need to use mapElement (string_profiles, 'tag_cc') way.

<span id="22c42e3a"></span>
## Business dimension query analysis (Item Analysis)

<span id="c68686aa"></span>
### After reporting the id field of the business dimension (item) table, why can't the id field of the item be found?

After the id field of the business dimension is reported to the database, it will be written into the item_id field. When you query and analyze, you can query the item_id field. Direct query of the id field is not supported.

<span id="bfef1b40"></span>
## What are the restrictions on reporting query item data?


* The business dimension (item) usage scenario is an extension of the event attribute, not a separate use, so the query must be bound to the event to query;

* You can set multiple association keys for events in the interbinding association between the business dimension (item) and the event, but the business must use id, not an attribute with the same name as the event attribute in the business.


<span id="d737eddd"></span>
## Fusion analysis

<span id="392538b9"></span>
### How to enable Fusion Analysis?

If you have purchased both DataFinder and other products, such as the Customer Data Platform (VeCDP) and Growth Marketing Platform (GMP), you can purchase and use DataFinder's converged analysis capabilities to directly connect and analyze data from other products in DataFinder. Fusion Analysis is a value\-added feature that needs to be purchased separately.

<span id="ce8783f5"></span>
# User analysis

<span id="379167e4"></span>
## What is the reason why Finder user scrutiny only has user information and no behavioral data?

Finder product users are screened according to the subject granularity. You need to ensure that the subject in the upper right corner is correct. Secondly, the behavior flow is displayed according to the application granularity. You can select the application where the user reports the behavior in the behavior.

<span id="131b26d1"></span>
## What is the reason why the record of data related to the user's startup event cannot be found in the user scrutiny function?

It may be because this user triggered the application startup event in an anonymous state, and in the user scrutiny, you used the UUID to query, and the startup record will not be found at this time. You need to use ssid search to view in user scrutiny, and only display the behavior in the real\-name state when querying through UUID.

<span id="de963a6b"></span>
## Users scrutinize the page and see an A logo. What does it mean?

This tag is a tag that the user highlights when an attribute is highlighted.

<span id="ac607003"></span>
## Why can't users query the real\-time data of today and yesterday?

In SaaS\-non\-cloud native (including overseas Byteplus environments), because of the offline table logic, users query offline tables in groups. Since the offline data has not been built on the same day, the data cannot be found. The event analysis query is real\-time + offline, so the data can be found. This phenomenon should not exist in SaaS\-cloud native environments.

<span id="e8cf60dd"></span>
## Why is it that when the rule creates a cluster, the time filter is past 7 days, and the user list contains users who are active today?

When users are filtered by group, the "today" and specified time frame filters include data for the day. Specifically, time_created is a user attribute that analyzes the final value, so the final value of the user table is checked, and there is no event filtering, so the time condition of the past 7 days is not actually used. If you filter using "user is", time_created is a user attribute that analyzes the final value, and therefore looks up the final value of the user table. If based on the filtering of events (user "did", "didn't do", "did in turn"), the final value user attribute is applied to the time period range. If a user has not done something in the past 7 days, they will not be screened out. Users can be filtered by customizing the registration event + event property (create_time) time range.

<span id="70b63ebe"></span>
## Is the "range" in the user subgroup open or closed?

In the Finder, the range settings for user grouping are usually closed intervals, i.e. greater than or equal to and less than or equal to. For example, if you set the user age grouping to range from 18 to 25, then users aged 18 and 25 will be included in that grouping. The specific SQL expressions are \> = 10 and < = 15 (between 10 and 15).

<span id="六、广告监测"></span>
# Advertising monitoring and analysis

<span id="_1、有什么办法可以拉取激活用户的imei-oaid-idfa-等数据？"></span>
## Is there any way to pull data such as imei/oaid/idfa of the activated user?

You can use the push API of the advertising monitoring module to pull the activation event, which contains these three fields.

<span id="_2、外部信息流广告，点击广告后还未到达app下载的落地页后就退出了，那这个会有广告点击数据吗？"></span>
## External in\-feed ad, after clicking on the ad, it exits before reaching the landing page of the app download. Will there be ad click data?

Ad click data is accounted for once.

<span id="_3、什么情况下激活渠道（activation-channel）会为null"></span>
## Under what circumstances will the activation channel (activation_channel) be null?

activation_channel this public attribute is null because: old users, no activation event is triggered, and ad monitoring will not be reported.

<span id="_4、渠道，激活渠道，首次广告推广渠道和广告推广渠道这四个渠道的区别。"></span>
## The differences between channels, activation channels, first\-time advertising promotion channels, and advertising promotion channels.

Channel: Corresponding field channnel, generally refers to the channel of the app, that is, the channel field when SDK is integrated, such as Huawei, oppo, appstore, etc.;

The activation channel is the same as the channel: the channel in the package is the channel written when the app is packaged;

The first advertising promotion channel and advertising promotion channel are promotion channels. The first advertising promotion channel refers to which channel the user was first brought to, and the advertising promotion channel refers to which channel the user is now brought to.

<span id="a66b87ae"></span>
## How to check the name in the English mapping table corresponding to the Chinese name of the promotion name?

Event analysis \- any event \- select the promotion properties \- click the filter box \- toggle the network of the developer tool to find the preview\-data\-values of the properties interface. It can also be obtained through metadata OpenAPI, see [API Description and Public Parameters](https://docs.byteplus.com/docs/DataFinder/API_Description_and_Public_Parameters_).

<span id="19409928"></span>
## Joint debugging tool, the test joint debugging failed, and the click sent by the media was not received. What is the reason?


1. You need to check whether the device ID is filled in correctly, and you need to use an accurate device ID such as oaid, etc.

2. You need to see if the selected promotion monitoring link is the same.

3. Check the joint debugging steps on the official website

    &nbsp;


<span id="in-the-alink-module-can-user-a-be-identified-from-alink-after-user-b-clicks-the-link-to-download-and-launch-the-application-by-sharing-the-link"></span>
## In the alink module, can user A be identified from alink after user B clicks the link to download and launch the application by sharing the link?

In the alink module, the app side cannot recognize user A. Because the shared link is a parameter configured in the background, it is a static parameter and cannot be modified dynamically.

<span id="1f66ea2f"></span>
## Can the data of the advertising promotion channel "Apple Search Advertising" be decomposed to the dimension of keywords?

At present, there are only three dimensions: advertising group, advertising activities, and advertising creativity, and the dimension of keywords cannot be supported for the time being.

<span id="dcd5113f"></span>
## After the ad monitoring link is replaced, will the old link data continue to be returned, and how to terminate the return data of the old link?

After switching activities, the old activities:


1. Attributed: There will only be non\-retained and activated returns. You can edit and delete the return event on the page.

2. Pending attribution: no longer available after the conversion window (click about 7 days)


<span id="28ac9471"></span>
## Why is the total number of activations displayed in the ad monitor 0, while the activation events can be found in other Finder analysis tools?


1. The total activation data monitored by the ad is different from the activation data in the Finder, and the two data cannot be directly compared. In advertising monitoring, activation refers to the activation of the device dimension, mainly the activation data of the promotion activities, while the activation events queried in the Finder refer to all active users, and the activation\-related attributes are recorded in the SSID dimension.

2. There may be several reasons why the total amount of activation is 0:

   * Ad not triggered: If the ad is not clicked or displayed, no activation event will occur.

   * SDK integration issues: If the ad monitoring SDK is not properly integrated into the app, or if activation events are not properly configured, activation data cannot be reported.

   * Attribution issues: Activation events may not be correctly attributed to advertising campaigns, resulting in activation data not being recorded.

   * User behavior: Users may not open the app immediately after installing it, or they may not activate it for a period of time after installation.

   * Privacy settings: The user's privacy settings may limit the tracking and reporting of activation events.

3. Verify that the operating system platform of the device is correct, and ensure that the platform parameters (such as iOS or Android) are set correctly.

4. If the joint debugging device attribution is successful, you can verify for yourself whether the activation type of the activation event is "promotion".

5. If you have followed the documentation through the joint debugging process and the activation event has not been successfully attributed, it is recommended to further check the attribution service filter criteria.

6. If it is an Android app, ensure that there are no other platforms (such as Windows) impacting the device attribution.


<span id="e6b5a2c1"></span>
## In the dashboard of the data overview in ad monitoring, the number of registrations and payments is 0?


1. Verify that registration and paid events return the `platform`property.

2. It is recommended to use client side reporting to avoid missing attributes required for ad monitoring analysis.

3. If it is reported at the server level, you need to carry the `platform`attribute (distinguish app, web, mp platform) when reporting according to the SDK.


<span id="d9b472ac"></span>
## Does the activation data in ad monitoring not match the activation data of DataFinder's other analysis tools?


* The total amount of activation is equal to the PV activated by the platform as an App.

* Promotional activation refers to the activation brought by advertising promotion, and the total is slightly higher than the activation data of the ad monitoring page, because the ad monitoring page filters out the activation data after installing the update during the conversion window, and other analysis pages of the Finder will contain this data.


You can select the activation event through the Finder page and get more accurate promotion activation data by filtering: `Promotion Type = Promotion Activation`.

<span id="0425d60a"></span>
## What are the reasons why the user registration and activation data in ad monitoring does not match the data in Bilibili?


* Anomalies: In a SaaS\-cloud\-native environment, the data for user registration and activation events appears to be abnormal, the number of registrations and activations is much lower than expected, and the data displayed by Bilibili does not match.

* Solution:

   1. Check the user properties query to ensure that the creative ID and device ID are included in the user properties.

   2. Filter through user properties to confirm if there is an activation event but no creative ID.

   3. Verify whether the activation event has a creative ID and check whether there is an activation event without a creative ID.

   4. Verify that the SSIDs of the activation events match, and check if any activation events are not associated with a creative ID.

   5. Confirm multiple registrations of the same device and avoid multiple returns of registration information.


<span id="b55667cd"></span>
## Ad monitoring joint debugging Does it support exposure joint debugging?

At present, only click joint debugging is supported, and exposure joint debugging is not supported. Joint debugging sequence: start joint debugging \- click the link \- download \- open the app.

<span id="a47d0772"></span>
## In the Vivo app store channel scenario, what is the reason why the data returned by Volcano registration is less than that returned by the account?


* Abnormal phenomenon: In the Vivo app store, the data returned by Volcano registration is less than the data returned by the account, and some data does not have the previous event of registration. At the same time, the client side activation callback failed and returned DDL response data empty.

* Solution:

   1. Verify that the returned data is within the window period, which is the time set in the attribution configuration.

   2. Check whether the device is activated outside the window period. If so, no activation event is triggered.

   3. Verify whether any data was missed during the query process, and check the data report by yourself.


<span id="c87c2e72"></span>
## Is the exposure attributed to the Ocean Engine channel remaining exposed for more than 24 hours after the shutdown?

After exposure attribution is turned off, exposure data will still be collected, but there will be a delay, usually within 2\-3 days.

<span id="da1bed2c"></span>
## What is the reason why the WeChat scan code download of the custom channel is attributed to the media channel?


1. Verify whether the data is obtained from a third\-party channel platform.

2. Check the data return time and device ID.

3. After confirming whether the user clicks the long chain, click the short URL, and the long chain will be attributed first.

4. If the short URL does not have device ID information, you need to provide the link, time node and device model of the short URL.

5. If the short URL does not trigger clicks on data, it is attributed to other channels.


<span id="b21d35e8"></span>
## In a marketing campaign configured using Share Fission Analysis, when a user triggers to browse multiple campaign pages and view ads from multiple different channels, does the user's final attribution use last attribution?

Yes, the final attribution of users is the last attribution. The attribution logic is the last click, the last clicked ad. If a user clicks Download in the app store and triggers an ad slot, the last attribution is still used.

<span id="d2960f7f"></span>
# Scenario analysis tool

<span id="3c8fed44"></span>
## Why is unkown seen in end point analysis \- web side \- operating system?

os_name is obtained through the useragent, but some non\-enumerated value ua data is recognized as unknown, such as crawler data.

The operating system enumeration values are generally android, ios, windows, mac, linux, unknow.

Unknown data is mainly non\-enumerated value ua data, such as crawler data, data that is not in the range of enumerated values, etc.

<span id="a7f5666f"></span>
## Scenario analysis calculation logic: How is the exit rate indicator calculated?

Exit rate = exit page/page views pv, i.e. exit rate = app_terminate/predefine_pageview event

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/174661d5eba74b57ba0213406b874282~tplv-goo7wpa0wc-image.image) </span>

<span id="425b88d4"></span>
# Circle event

<span id="2e6acf7d"></span>
## When circling an event, some areas have clicks, but there is no data. What is the reason?

When circling events, the circled path needs to be consistent with the full event tracking path before the data is available. Circular events have a wide range and do not necessarily have full event tracking events.

<span id="8cb6a722"></span>
# Query performance and usage skills

<span id="e44ce149"></span>
## Why is the page loading so slowly?

Please check whether you have uploaded the number of properties under the event. Uploading too many properties under the event will cause the page to load slower. Please check whether you have set value to key.

<span id="c099e585"></span>
## Front querying statistical event data, is there a caching mechanism?

Yes, real\-time data is refreshed every 10 minutes, with no limit on the number of items.

<span id="23b5f0bd"></span>
## How to use analysis to win the bidding process for important changes?

Users can use BytePlus Growth Analysis's "date annotation" function to record important changes made at certain time points (such as version releases, operational activities, online incidents, etc.), and the analysis function can be seen at a glance. Click "App Management \- Date Annotation" to operate the date annotation.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d81bd5ca202d428f85ee8a4a06b4b57f~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa6b8a4213aa475ead858a7c16d0141f~tplv-goo7wpa0wc-image.image) </span>

<span id="0921082e"></span>
## Sorting restrictions after transpose?


1. Before transposing, all columns support sorting, but only single\-column sorting is supported.

2. After transposing, only the indicator column supports sorting, and only the sorting of a single column is supported.

    &nbsp;


<span id="how-do-i-view-the-enumeration-values-reported-by-properties-for-fields-that-are-qualified-by-an-enumeration-value-can-i-configure-the-qualified-enumeration-value"></span>
## How do I view the enumeration values reported by properties? For fields that are qualified by an enumeration value, can I configure the qualified enumeration value?

For the first problem, as long as the property is displayed in groups, all reported values will be found. For the second problem, a dictionary is used to solve the problem that a qualified enumeration value can be configured for a field that is qualified by an enumeration value. If the reported value is not in the enumeration range, the original value is displayed. If the client does not want to limit reporting, the mapping may not be performed.

<span id="b358cba8"></span>
# Data query exception

<span id="ff0dd0c2"></span>
## The query failed in AnalysisBase. error message:can not get distribute lock。

The limited viewership of the query is usually the same query is triggered again before the end of the previous query, resulting in the limited viewership of subsequent queries. Usually it takes a while.

<span id="e4ae1fb8"></span>
## The enable_stay_duration: true configuration is enabled, but the data of the page stay time is not found through the page access event in DataFinder. Why?

(1) Because the page access event has no duration attribute, it is necessary to use the page active and page closed events to see the duration of stay; enable_stay_duration this switch is for the two events of page active and page closed to collect the duration.

(2) Page exit: Record the timestamp of each action of the user [entering the page, switching to the inactive state, returning to the active state, leaving the page], report the predefine_page_close event tracking when leaving the page, and add the duration of each active state as the user's single use time.

<span id="f633b27c"></span>
## Why does the software version number only display the large version number?

The app_version in the SDK displays the large version number by default. If you have the need to count the small version number, you need to set the app_version_minor (that is, the second version number, the four\-digit version number of the app, and the string reported by yourself can support any format. The data stream is not processed) as the small version number. It should be noted that the historical data cannot be filtered after the setting, and the statistics will start after the setting is successful.

<span id="360b17b6"></span>
## The historical data will change slightly on different dates. Why?

There are two main types of historical data changes:

(1) Differences between real\-time and offline data: The data of the day is a real\-time caliber, and T + 1 will become an offline caliber (completed before T + 1 18:00). Due to the differences in real\-time and offline logic, there will be a certain amount of data change, generally no more than 5%.

(2) Cache data replenishment: Due to network problems or closing the app immediately after access, there will be a small amount of data that cannot be reported when the event occurs. This part of the data will be reported when the app is opened next time, and the network situation is normal. Because the time is the actual time of the event, not the time of the replenishment, the phenomenon is that the historical data will increase. As long as the event occurs within 7 days, a supplementary report will be made, and those that exceed 7 days will be discarded; the magnitude of this part of the data will vary depending on the situation of the operating area network and the business characteristics of the app itself; in most cases, the proportion is actually very small, but some applications will account for a larger proportion.

<span id="a71bcd37"></span>
## What is the reason for the inconsistency between event analysis and custom SQL data with the same filtering criteria?


1. Confirm that the query conditions and query range are consistent when event analysis and custom query.

2. The calculation results of event analysis may be cached, and you can use refresh to update all invalid data and compare it.

3. If the environment has multiple time zones enabled, you need to convert the query time range to the corresponding query time zone in the custom query.

    &nbsp;


<span id="is-there-a-difference-between-the-number-of-uvs-for-activation-and-app-launch-screening-new-users"></span>
## Is there a difference between the number of UVs for $activation and app launch (screening new users)?

When there is a significant difference in retention between $activation and app launch, the solution is:


1. The $activation event usually refers to a user's activation behavior, such as installing and opening an app for the first time. And "app launch" is the event that is triggered every time the user opens the app. The reasons for the difference in UV numbers between the two may include:

   * Different event definitions: The $activation event is usually only fired on the first open after the first installation, while the "App Launch" event is fired every time the app is opened.

   * Differences in user behavior: Users may not open the app immediately after the first installation, or only open it for the first time at a certain point after installation, which results in different time distributions for activating UV and activating UV.

   * Data reporting delay: There may be a delay in data reporting, resulting in inconsistent statistics for activation events and start events.

   * User reinstalls app: The user may reinstall the app after uninstalling, which will trigger the $activation event again, but the statistics for app startup may vary.

2. In the user's detailed investigation, only the devices activated by the App are presumed to have activated the APP, and no follow\-up behavior has occurred or the APP has been closed. There should be relevant events reported during subsequent startup.

   There are many App activation data in the user scrutiny, you need to look at the activation install_type type and app_version fields, install_type is 1 (first installation), install_type is 3 (uninstall and reinstall), such as install_type and app_version have changed, indicating that the client side APP version has been upgraded or adjusted.

    &nbsp;


<span id="after-using-the-analysis-tool-to-query-and-analyze-the-result-page-of-the-temporary-query-is-invalid"></span>
## After using the analysis tool to query and analyze, the result page of the temporary query is invalid.

After configuring the query analysis parameters in the advanced analysis page of DataFinder, click Query to view the query results on the current page. After copying the URL of the current query results page, the query results can be temporarily retained. The temporary storage time of this URL is about 1 month. After more than 1 month, it will expire. Clicking the page URL again will prompt that the analysis results do not exist. It is recommended to save query results that require long\-term retention as Kanban boards.

<span id="fd12969f"></span>
## What is the reason why the data query result is NULL when querying on the DataFinder?


* Abnormal scenario: After an event tracking data is reported, the query result of the data at the time of query is null. For example, when the Data Transmission Service is accessed, the referrer event tracking is integrated, but the event tracking data value is null when querying.

* Possible reason: This may happen because the custom event tracking you reported has the same name as the preset event tracking of DataFinder. There is a conflict during data warehousing, resulting in the data not being warehoused normally. The event tracking result is null when querying. In the above example, DataFinder provides you with a preset attribute referrer. If you also customize the referrer attribute when reporting a custom event tracking, the referrer attribute data will not be warehoused normally.

* Solution: Before integrating and reporting custom event tracking and custom attribute data, you can check whether it has the same name as the preset event/attribute and the disabled attribute to avoid subsequent data reporting abnormalities.


<span id="8158ba11"></span>
## The event attribute value of the finder product is dirty and garbled. What should be done?

The data brought by the crawler has no analytical value and affects the real data. It is recommended that you refer to the "Crawler Data Filtering" document, turn on the anti\-crawl configuration, and clean up the dirty data.

For the "Crawler Data Filtering" document, please see [General Settings - Crawler Data Filtering](https://docs.byteplus.com/docs/DataFinder/General_Settings_-_Crawler_Data_Filtering).
