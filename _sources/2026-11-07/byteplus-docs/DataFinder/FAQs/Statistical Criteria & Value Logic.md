---
title: "Statistical Criteria & Value Logic"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Statistical_Criteria_Value_Logic"
---

<span id="43f4a8e5"></span>
# Analysis subject

<span id="6c278561"></span>
## The main role of multiple subjects?


* The actual business analysis process needs to clarify the core object or focus of the analysis, usually the "subject" refers to the users who use the product or service. However, in some scenarios, it may also be necessary to analyze multiple entities, such as the automotive industry, where data analytics needs to be conducted from different perspectives such as consumers, automobiles, and merchants. In this scenario, you can enable the multi\-agent function of DataFinder.

* After enabling the multi\-subject function, you need to mark clearly which subject's data is reported when reporting the data. The DataFinder identifies the reported application information by setting the reported application ID ( **appid** ) at the time of data access initialization, and can identify which subject's data is the reported data through the binding relationship between the application and the subject.

* After enabling the configuration of multi\-agent function, when you perform data analytics in the future, you can switch the analysis subject in the analysis tool, and then you can analyze all application data associated with a subject. In the segmentation filter, you can filter through the application ID to analyze only the subject data of some applications.


<span id="4e305647"></span>
## Does a custom event tracking belong to two principals?

After activating the multi\-agent function, when reporting event tracking data, it is necessary to indicate the reported application ID (appid), and associate the reported data with which subject's data through the application. Since an application can only bind one subject, so:


* If an app is specified when you customize an event tracking report, the reported data belongs to the body associated with the app.

* If you modify the reported application ID after the event tracking data has been reported for a period of time, and the subject associated with the modified application is also inconsistent with the previous subject, the modified event tracking data will be reported to another subject. However, no event tracking data is reported to both subjects simultaneously.


<span id="3b724363"></span>
# Statistical criteria & unique user identification

<span id="370b1090"></span>
## What are the statistical criteria of user data on DataFinder?

The default statistical criteria of DataFinder is the user. DataFinder uses ssid to uniquely identify the user and uses ssid to count user behavior data. You can also modify the statistical criteria to other statistical criteria by yourself.


* For ssid introduction, see [User ID (uid, ssid, did)](https://docs.byteplus.com/docs/DataFinder/User_ID_uid_ssid_did).

* Create and use operating instructions for other statistical criteria, see [Statistical Criteria](https://docs.byteplus.com/docs/DataFinder/Statistical_Criteria).


<span id="e78dfbb1"></span>
## A user logged in to account a on the web and app respectively, so the ssid should be the same, right?

Yes, a uuid corresponds to an ssid.

<span id="078da0b5"></span>
## What are the statistical criteria of UV?


* When using the DataFinder default user (ssid) as the statistical criteria, UV refers to the data after ssid deduplicate.

* If you create and use other custom statistical criteria, UV refers to the deduplicated value of the custom statistical criteria property, and is no longer the regular user UV value for the user criteria. Create and use operating instructions for other statistical criteria, see [Statistical Criteria](https://docs.byteplus.com/docs/DataFinder/Statistical_Criteria).


<span id="4766ba29"></span>
## What do I need to do if I use custom statistical criteria?

If you want to use custom statistical criteria, you need to see if the subsequent analysis tools support switching to use custom statistical criteria, you need to ensure that the property data using custom statistical criteria can be reported normally, and then go to the DataFinder console to create and use, please see [Statistical Criteria](https://docs.byteplus.com/docs/DataFinder/Statistical_Criteria).

<span id="9da040e6"></span>
## Click on the activity page to jump to the Mini Program through the H5 official account. Can you identify it as an ssid?

H5 and Mini Program are two end products, and the generated device identifiers are different, so anonymous access to ssid is different. If you want to unify the user identity, you can achieve the behavior after logging in, that is, both ends report the same real\-name uuid. It is impossible to get through both ends anonymously.

<span id="cf1902e2"></span>
# User ID & Multi\-ID Types

<span id="702d0f60"></span>
## Multi\-ID type application scenarios?

Usually when conducting user behavior data analytics, there may be a variety of identification IDs we use to identify users, such as mobile phone number, application account number, user device ID, etc. DataFinder presets the commonly used user identification ID types for you, and also supports you to add more ID types. It also provides you with ID\-MAPPING computing capabilities, MAPPING calculations for multiple types of IDs, and uses ssid to restore a real natural person as much as possible to improve the accuracy and reliability of the data.

<span id="5ed54eb1"></span>
## ID identification logic for multiple ID types?

When using multi\-ID types, that is, there are n types of user_unique_id, so when mapping to generate ssid, n type (user_unique_id) and ssid are used for mapping, as shown below.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b1d42c4f15e248109ec223f0e8c45a9f~tplv-goo7wpa0wc-image.image) </span>

You can refer [Example 2: Global association identity](https://docs.byteplus.com/docs/DataFinder/User_ID_uid_ssid_did#10d176cb) to a specific example to understand the mapping generation logic of ssid when the multi\-ID type is enabled. For more information on user ID, please refer to [User ID (uid, ssid, did)](https://docs.byteplus.com/docs/DataFinder/User_ID_uid_ssid_did).

<span id="95c796ee"></span>
## Considerations for multi\-ID data access?


* You need to contact the DataFinder technical support staff to add the required ID type in the background configuration according to the ID design plan. The ID type can only be lowercase letters at present, and can be connected between characters by _.

* Report criteria ID and ID type: When reporting the ID value of the user ID, you need to mark clearly which ID type the reported ID data is. Take the web as an example:

   ```JavaScript
   window.collectEvent('config', {
    user_unique_id: '12345656788888' The actual value of the business ID
    user_unique_id_type: 'cust_num' //user id type. Same id design scheme
   })
   ```
   

* Report the relationship between ID criteria: id binding. In some scenarios, we can obtain other ID types associated with the subject. To ensure the accuracy of the association relationship, we recommend setting id bind to report the relationship between the criteria and the criteria in real time. The timing of ID bind: It is recommended that the ID relationship be bound as much as possible before reporting the event. ID bind can bind multiple types of ID and ID values at one time (such as mobile phone number, customer number, and other ID numbers to achieve association in one ID bind call), but the same ID type can only appear once. Take the web as an example:

   ```JavaScript
   window.collectEvent('bindToken', {
      phone: '1230000000' //key is an enumeration value of type id, the same as the id design scheme
      cust_num: '12345656788888' //key is an enumeration value of type id, the same as the id design scheme
   }, (result) => {
     //Do the corresponding operation according to the return success and failure
   })
   ```
   


For more instructions on data access and data analytics in multi\-ID scenarios, please refer to [(不发布)Using Multi-ID Types](https://docs.byteplus.com/docs/undefined/6a4ce26a8f7714051e96f4c5).

<span id="533cc58e"></span>
# SSID correlation

<span id="ddca6924"></span>
## After the user's real name, the ssid is changed. During the process of anonymizing the user to the real name, the server level generates a new ssid instead of using the original ssid.

The problem may be due to the server level reporting the user's profile before the client side's real name, and then generating a new uuidssid. The solution to this problem is to report it at the server level after the real name of the client side. Also, it is important to note that the real\-name order of users should be Anonymous \> Real Name \> User Properties \> Real\-Name Behavior.

<span id="25167d18"></span>
## When users perform anonymous and real\-name operations on different browsers, how can they ensure that the data is recorded to the same SSID?

In a SaaS\-cloud native environment:


1. Existing product logic: Anonymous and real\-name events on browser A will be logged to the same SSID, and real\-name status will also be logged to the same SSID. However, the anonymity status on the B browser is unlikely to be recorded to the same SSID.

2. SaaS\-cloud\-native has no multi\-device repair function yet, so the anonymous data of device 2 will be attributed to SSID, and the other data will be on SSID 1. At present, there is no other standard solution that can achieve multi\-device repair.

3. For anonymous and real\-name operations on different browsers by the same user, anonymous IDs can be used for statistics, because anonymous IDs are not reported web_id, so there is no priority issue.

4. Composition of web_id and relationship to cookies: user login does not affect web_id values, clearing cookies does not affect web_id values, but clearing the browser localStorage changes web_id values.

5. web_id generation logic: web_id is always self\-incrementing, no matter what the parameters are, as long as the request will generate a new web_id. Changing the browser, changing the domain name, changing the appid, or emptying the cache will rerequest the web_id.


<span id="9c77340e"></span>
# user_unique_id related

<span id="e5764605"></span>
## What is the reason for multiple user_unique_id in the same browser?


1. Check if multiple accounts are logged in in the same browser, and if so, try to turn off asynchronous operations.

2. If devtool is used, close devtool, because devtool will have a built\-in reporting address for statistics on its usage.

   3. Confirm whether there are multiple SDK instances and check whether the webid is consistent.

3. If the problem persists, it is recommended to check the framework for any issues.


<span id="04249c8a"></span>
# web_id, device_id related

<span id="0a7d1bb2"></span>
## Device ID generation logic


1. web_id: The request parameters are: app_id, the current URL, the referer of the URL, the useragent of the current browser, and user_unique_id (usually null), mainly relying on the appid and the current environment. The request will generate a unique webid return at the server level;

2. device_id：

   * The priority of ios is idfv \> idfa.

   * Android is Androidid \> google_aid \> oaid + device_brand

      Then match according to the relevant priority. If it does not match, a new did will be generated according to the algorithm in the background, and device_id generated when the SDK is initialized, which is earlier than the time of event reporting;

      Generation of device_id is only related to device information, independent of APP (app_id). If the device information actually collected by different APPs is consistent, then the theoretical device_id is the same.

3. Ssid: Get ssid according to the device_id obtained, and the user_unique_id and user_unique_id_type in the request request ssid service related interface


<span id="6a04bea4"></span>
## WeChat Mini Program webid

A. When no custom web_id is used, the SDK will go to the data stream interface to obtain web_id, cache it to storage, and reuse it later;

B. If the custom web_id is turned on, the customer needs to manually set the web_id (need the value of the number type), or by using the setWebIDviaUnionID method to set the unionid to generate web_id, or by using the setWebIDviaOpenID method to set the openid to generate web_id, in this case, it is controlled by the business itself;

Another: The generation rules of webID are the same as those of H5. The specific rules are as follows:

When sdk is initialized, that is, when the init method is called, a webid request is made to the server. The request parameters are: app_id, the current URL, the referer of the URL, the useragent of the current browser, and user_unique_id (usually null). The request will generate a unique webid return at the server level, and will return ssid. (Description: The url and referer values on the Mini Program side are all null values).

<span id="e4a71900"></span>
## Under what circumstances does the device_model in the mini\-game change and how is the web_id generated?

The generation logic of the device_model and web_id of the mini\-game is obtained through the system API. If device_model changes, it may be due to the use of an emulator. The emulator may affect the value of device_model. In addition, if you simply change the device model without recreating the emulator, the device_model may also change. It is recommended to use a real Android device for testing.

<span id="3dac52c5"></span>
# New and existing users/whether it is relevant on the first day

<span id="f84d6ace"></span>
## What are the properties used to identify new and existing users?


|Property name |Property description |
|---|---|
|Old and new users: user_is_new |* Judgment logic: In a period of time, determine whether the time of the target event ($event_time) and the activation event (first_event_time, that is, the time of the first event) occur within the [ **same time period** ].<br><br>* Note: The calculation results of new and existing users (user_is_new) will be affected by the time granularity of data analytics. When the time period of analysis is inconsistent, the judgment results of new and existing users will change. |
|Whether the first day: $is_first_day |* Judgment logic: Determine whether the time of the target event ($event_time) and the activation event (first_event_time, that is, the time of the first event) occurred within the [ **same day**].<br><br>* Note: Whether the first day ($is_first_day) is calculated is not affected by the time granularity of data analytics. |
|Whether to visit for the first time: $is_first_time<br><br>(Hidden, not recommended) |The first launch event for each user adds a value of true for this property, and a value of false for other launches.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This property currently defaults to the "hidden" state (earlier history items may still be "started" state), you cannot use this property directly, if you need to use it, it is recommended to use the event public property "$is_first_day" as the property of whether the event is triggered on the first day.</div><br> |
|Activation time: first_event_time |* The event trigger time generated when the user first generated an event. When an event occurs for the first time for a user, the DataFinder records an activation time property: first_event_time.<br><br>* Note: The activation time (first_event_time) for the same user is fixed. |
|Registration time: register_time |* The trigger time of the registration event generated when the device was registered.<br><br>* Note: Usually the mobile end will initiate a device registration request in scenarios such as switching uuid and local did. Even for the same device, a registration time is generated as soon as a registration event is triggered, so the registration time may change. |


<span id="998dfb39"></span>
## How is user_is_new defined?

According to whether the user event is first reported within the query time period, it is determined whether the user is a new user within this event.

For example, if the query time range is January 1, 2020 to January 3, 2020, the date granularity is day\-level, and the first activation time of a user is 18:27 on January 1, 2020, then the user is counted as a new user on January 1, 2020 under the current query conditions.

<span id="86a2b59b"></span>
## Some questions about new and existing users (user_is_new) after adding the preset event property $is_first_day (whether it is accessed on the first day)


1. How can we distinguish between new and existing users in our analysis?

   After adding the preset event property $is_first_day, when we analyze, we need to distinguish between new and existing users by selecting "Whether it's the first day". The event property is $is_first_day = true for new users, and $is_first_day = false for existing users;

   **Take event analysis as an example to illustrate the following:** 

   If you want to analyze the situation of new users who have visited the page, you need to select "Whether it's the first day" through the filter conditions, and select "first day" as the new user; similarly, select "non\-first day" as the existing user.;

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/852f77de684a48e5bea17aaf236c005f~tplv-goo7wpa0wc-image.image) </span>

   At the same time, enable grouping display by event properties, and select "Whether it's the first day" to group by new and existing users.

2. **There is already a "new and existing users" property to distinguish between new and existing users. Why do you need to add the $is_first_day property to distinguish between new and existing users? What changes have been made to computational logic?** 

   The calculation logic of $is_first_day is exactly the same as that of new and existing users, except that the calculation of new and existing users will be affected by time granularity, while $is_first_day is only calculated by day:

   * In the judgment logic of "new and existing users":

      The new user judgment logic is that the target event and the user's first event occur within the same period, otherwise it is determined to be an existing user. This can lead to some problems. For example, a user is considered a new user within a 30\-day cycle (e.g., the first event occurs on the 1st, and the target event occurs on the 5th, which counts as a new user), but it is considered an existing user within a 1\-day cycle.

   * In the judgment logic of "Whether it's the first day":

      The new user decision logic is that the target event and the user's first event occur on the same day, rather than within the same cycle. When an event occurs for the first time, the DataFinder records an activation time property: first_event_time, if the event time of subsequent events is equal to first_event_time, then $is_first_day = true; otherwise, false.

3. **Will the "old and new users" property continue to be retained?** 

   Considering the issue of historical data, this property platform will be retained for a certain period of time.


<span id="aa8ce155"></span>
## What is the difference between first\-day access to $is_first_day and new user user_is_new?

Whether the first day of access is an event property depends on the event and will not change. Whether the new user is related to the query time range can be checked by detailed verification. Whether the first day of access is different from whether the new user is used.

<span id="e646df48"></span>
## What is is_first_time computational logic?

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This property currently defaults to the "hidden" state (earlier history items may still be "started" state), you cannot use this property directly, if you need to use it, it is recommended to use the event public property "$is_first_day" as the property of whether the event is triggered on the first day.</div>


is_first_time build premise: need to report $is_first_time in params (note to add dollar sign);

App\-side launch, predefine_pageview, Mini Program\-side app_launch These three events do not require customers to customize and report $is_first_time to build (saas does not support app\-side launch for the time being, and will support it in the future)

Reporting side logic:

Follow (ssid, event, is_first_time) to record whether an event is generated for the first time locally, if the event has occurred, $is_first_time is directly set to "false", otherwise set to "true" (note that string is not a boolean value)

Receiving side logic:

(1) If the received event $is_first_time "false", no processing is done;

(2) If the received event $is_first_time is "true", the client side time (local_time_ms) reported by the [user of the event] [first time] will be recorded, set only once, the recorded timestamp will be compared with the client side time reported by the subsequent [user of the event], if equal, keep $is_first_time = "true", otherwise correct to "false"

<span id="94941482"></span>
## What is the reason for the existing user data in the user data reported by the first installation of the application?

The judgment of installing the first installation is based on the application, and the first day of access is the judgment of the entire project. If a project contains multiple applications, if one of the applications is activated on the first day and the other application is activated the next day, then the latter activation is the first installation, and whether the first day of access is not the first day.

<span id="c783188d"></span>
## What is the reason for the difference between the total value of a new user over a period of time and the sum of the values counted by day?

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d01295ec725450a872cc9b5bc116013~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/46f72f6341a842758ba4ae82342753b5~tplv-goo7wpa0wc-image.image) </span>

If the metric calculation is to calculate the total number of times, and the segmentation filter is for new users, then the meaning of the total value for a period of time can be roughly summarized as: the total amount of all events belonging to new users during this period.

2. The calculated value by day means: the number of reported events belonging to new users that day.

3. There is a data difference between the total value and the sum calculated by day. The difference is mainly: the number of new user events on non\-registration dates

<span id="dd979f70"></span>
# Duration data related

<span id="03cccf5f"></span>
## What duration properties are currently supported?


* APP: Android/iOS/Harmony

   
   |Event |Event properties |Property description |
   |---|---|---|
   |`app_terminate` |`duration` |* `The duration` property is the duration of the session in which the app is opened this time, based on the summation statistics of the duration of the device in the foreground.<br><br>* Unit: second (s). |
   |`$crash` |`$session_duration` |* `$session_duration` Property, is the duration of this Session. Session means a single session, and there will be a corresponding Session after each launch.<br><br>* Unit: milliseconds (ms). |
   |Duration Event |`$event_duration` |* `$event_duration`Property is the duration of the event, such as the video playback duration data reported when the video playback duration event was captured. Statistical calculations are performed by the timestamp of the start and end of the event.<br><br>* Unit: milliseconds (ms). |
   |Full event tracking |`$page_duration` |* `The $page_duration`property is the page duration property.<br><br>* Unit: milliseconds (ms). |
   

* Web

   
   |Event |Event properties |Property description |
   |---|---|---|
   |`predefine_page_alive` |`duration` |* `The duration` property is the active time, which is simply the time the user actually uses it.<br><br>* Unit: milliseconds (ms). |
   |`predefine_page_close` |`duration` |* `The duration` property is the active time, which is simply the time the user actually uses it.<br><br>* Unit: milliseconds (ms). |
   ||`total_duration` |* `total_duration`Property The entire length of time the user visited the page, from start to close, including the length of time the user was inactive (the length of time the user switched the page was not in actual use).<br><br>* Unit: milliseconds (ms). |
   |Full event tracking |`refer_page_duration_ms` |* `refer_page_duration_ms` property is the length of access to the source page, and the value is consistent with the value of the `duration` property.<br><br>* Unit: milliseconds (ms). |
   

* Mini Program

   
   |Event |Event properties |Property description |
   |---|---|---|
   |`app_terminate` |`session_duration` |* `session_duration`Property is session duration, a time is recorded at app_launch, and then the time difference is calculated at app_terminate.<br><br>* Unit: second (s). |
   |`predefine_page_hide` |`duration` |* `The duration` property is the active time, which is simply the time the user actually uses it.<br><br>* Unit: milliseconds (ms). |
   


<span id="4ac19373"></span>
## What is the difference between the "total_duration" property and the "duration" property?

The differences are as follows:


* Duration: is the active duration, which is simply the time the user actually uses it.

* total_duration: is the total time the page is open to close, including the length of inactivity (the user switched the page is not in actual use). For example, minimization, background, etc., switching the page will be understood as "leaving the page" and a close event will be reported at this time.


<span id="93cfe950"></span>
## What is the "duration" data of the APP calculated based on? Why is the duration of database records different from the results calculated by DataFinder?

The duration is calculated by the session ID.


* For Android devices, the termination event duration is calculated as follows:

   Terminate.time = last_page + duration, terminate.duration = sum of all page.duration in the current session.

* For iOS devices, the calculation logic for duration is: (terminate\-launch)/1000.


The page.duration of Android devices is automatically calculated by the system, while the duration of iOS devices needs to be manually turned on.

The calculation logic is different because the android terminates the reporting logic is different, and it is generally reported in a supplementary manner rather than in real time.

<span id="dee6de80"></span>
# Page access related

<span id="a2303899"></span>
## predefine_pageview, predefine_page_close, predefine_page_alive, predefine_pageview_hide What are the triggering times of these events?

predefine_pageview: the page is opened and sent when the sdk initialization is completed;

predefine_page_alive: Open the stay time, send it every 1 minute, switch the page to send it once, and close the page to send it once;

predefine_page_close: Open the stay time, record the timestamp of each time the user [enters the page, switches the state, leaves the page], and then report the predefine_page_close event when leaving or closing the page;

predefine_pageview_hide: This is a Mini Program specific event that will be reported when each page leaves pv_hide.

<span id="a835a1f4"></span>
# app_ related

<span id="ad29f133"></span>
## Apply exit (app_terminate) event reporting logic


* iOS: After the user cuts the background (including the lock screen), it will be counted as the end of the session immediately, and a Terminate event will be generated

* Android: When the user stays in the background for 30s (including the lock screen), and then turns on the next time and listens for more than 30s, it will not generate terminate.


app_terminate event is a supplementary event reported in the mobile end, each time leaving the page will generate bav2b_page event, the next time you open the APP will be based on the bav2b_page event to determine whether to report app_terminate event, and clearly app_terminate event generation time. If the program crashes without collecting bav2b_page events, you cannot catch app_terminate events.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b00c7681c23943e983d0727abcba93aa~tplv-goo7wpa0wc-image.image) </span>

<span id="68a88aa9"></span>
## app_channel property value logic


* This field is left in the predefined position of the Mini Program SDK, but the Mini Program SDK itself does not set this field value. You can follow up the business situation to set it yourself;

   * iOS and Android can set channels at initialization, such as "XiaoMi, HuaWei, Baidu" and other channels. iOS if not set, generally default "App Store" channel.

* If the app_channel value is not reported, SaaS\-non\-cloud\-native will automatically build the value as unknown for you; SaaS\-cloud\-native environments will not be built, so data with null channels will not be displayed under the current SaaS\-cloud\-native filter conditions.


<span id="0b75b4e3"></span>
## app_name properties support customization

app_name fields are the app name and App Name set when creating the app;

The application name can be modified in the application list, but modification is not supported after app_name setting.

<span id="6a16ec6a"></span>
## app_platform value logic? Why can't I find this property on the property management page?

app_platform property is not a real collected and reported property, but calculated by DataFinder based on the data you collected and reported, so this property cannot be found on the property management page.

<span id="8aa185f9"></span>
## What is the difference between app_platform and platform?


* app_platform: the end of the application, such as the customer's application has the app end, the web end, and the Mini Program end

* Platform: platform, this field is a field to distinguish different ends, the field values are ios, android, mp (Mini Program), web, wap (H5)


Overall, the platform is more detailed.

<span id="af90ebac"></span>
## app_launch and app_terminate reporting time?

app_Launch: When the user launches the app or enters the foreground, a Launch event will be generated inside the AppLog;

app_terminate: iOS is when the user cuts the background (including the lock screen), immediately counted as the end of the session, will generate a Terminate event; while Android is when the user stays in the background for 30s (including the lock screen), and then the next time you open the monitor to more than 30s will generate terminate.

<span id="39218e76"></span>
## app_launch event is triggered from the background start, in this scenario app_launch event will be warehoused?

SaaS\-non\-cloud\-native (including overseas BytePlus environments) will filter out app_launch events launched in the background, but SaaS\-cloud\-native does not filter out, so SaaS\-cloud\-native scenarios will be warehoused. Whether the trigger is initiated from the background is identified by the is_background property reported.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d21f6113a084fb9a860c493247ed991~tplv-goo7wpa0wc-image.image) </span>

<span id="6a99e4cb"></span>
# Network/referrer/reporting platform type related

<span id="ad01f334"></span>
## What is the meaning of mobile in the network_type property value?

Mobile: Mobile network connection

Value logic: It is the bottom of the mobile network connection. For example, if we cannot identify that it is 3G, 4G, or 5G, return to mobile (mobile network connection).

<span id="2a2993b0"></span>
## network_carrier data generation logic? Why can't I get it sometimes?


* network_carrier is the carrier property that the SDK gets through the system interface, and then the data stream cleans it to network_carrier property. If it is empty (or empty string), it means that it cannot be obtained, which mostly occurs on Android devices.

* Since iOS 16, the official API has deprecated the API obtained by the operator and no longer supports access. So the IOS SDK does not currently support the acquisition of public properties of network_carrier events.


<span id="db624188"></span>
## Mini Program sdk mp_platform field number (0, 1, 2,...) what are the corresponding values?

0 WeChat Mini Program

1 Alipay Mini Program

2 Toutiao Mini Program

3 Quick applications

4 Mini games

5 Baidu Mini Program

6 QQ Mini Program

7 uniApp Mini Program

<span id="2646219c"></span>
# Internet Protocol Address, continent/country/province/city related

<span id="21ced6bb"></span>
## client_ip property values support using custom values to override?

client_ip properties are preset properties of the DataFinder that are automatically calculated and generated by the DataFinder server level based on the collected data. You can override them by directly reporting the value of the client_ip when integrating the SDK. For example, when reporting through the server level SDK, you can upload the IP directly in the header to overwrite the client_ip field.

<span id="ac8454d0"></span>
## How do I override automatically generated client_ip field values?

You can override this by reporting the value of the client_ip directly when integrating the SDK, for example, by uploading the IP directly in the header to override client_ip fields when reporting through the server level SDK.

<span id="41b1be99"></span>
# A/B experiment related

<span id="ab3e3db5"></span>
## origin_ab_version with ab_version property data calculation logic?


|Comparison description |Origin_ab_version |ab_version |
|---|---|---|
|Property description definition |Wide aperture AB test VID, associated A/B test ablog table for screening. |Narrow bore AB test VID. |
|value logic |* The value is taken from the bottom sheet ablog table of the A/B test, and the vid data is taken from it; the value is associated with the ablog table of the A/B test at the granularity of days (only one vid value is taken a day).<br><br>* Properties similar to user properties, independent of the event, strongly associated with the user, as long as the user into a certain experimental grouping, the user's origin_ab_version will be associated with the user's first packet of the day of the vid value, if this user packet changes that day, but the user's origin_ab_version will still be counted in the first packet vid. |* The value is taken from the bottom sheet of the event reported by the DataFinder; the value is taken with the event report (if there are multiple events reported in a day, there may be multiple vid values), and the event report has ab_version property value and has a value<br><br>* Properties are similar to event properties and are reported with events |
|Data exception description |* When using the analysis tool for A/B test correlation analysis on the DataFinder, origin_ab_version when calculating in the DataFinder, if multiple AB test vid values are selected, the pv statistical results will be larger than the actual data.<br><br>* For example, if an app conducts an A/B experiment with 4 experimental versions (i.e. 4 vids), when analyzing the PV of the app's "app_visit" event in the DataFinder, if you want to see the PV that filters the "app_visit" event of vid = 1 and vid = 2 through the "origin_ab_version" property, the screening result will be larger than the PV data of the actual "app_visit" event.<br><br>* The reason for this phenomenon is that on the DataFinder side, each vid will calculate a PV. When multiple vids are selected for data query, the PV number data will become larger. ||
|Suggestions for use |* When analyzing experimental data, if you need to do a query from the day the experiment started, it is recommended to use the "origin_ab_version" property for query analysis, and the resulting data will be more accurate.<br><br>* When using origin_ab_version, if you filter multiple vids, it is recommended to add origin_ab_version to the group to view the data according to the granularity of vids. |When querying a specific scene or event, it is recommended to use the "ab_version" property for troubleshooting, and the query result data will be more accurate |


<span id="b01411ab"></span>
# Other

<span id="f3d439db"></span>
## What is the mechanism for deduplicating the data reported by the client side?

The event reported by the client side generates a key, and at the same time, there is a buffer area in the server, which can cache about 10w of data, and the data cached in the buffer area is updated in real time. The data flow is judged in the same buffer, and the data with the same key is deduplicated, and more data is discarded. However, if the duplicate data in this scenario is not in the same buffer, it will not be deduplicated. Generally, the phenomenon is that the erver_time interval is relatively long.
