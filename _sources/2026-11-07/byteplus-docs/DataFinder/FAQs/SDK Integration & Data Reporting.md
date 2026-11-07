---
title: "SDK Integration & Data Reporting"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/SDK_Integration_Data_Reporting"
---

<span id="644d96bd"></span>
# Common Preset Event/Attribute Consultation

<span id="65f3b4af"></span>
## What preset events/properties are supported?

Supported preset events and properties: [Preset Property Summary Table](https://docs.byteplus.com/docs/DataFinder/Preset_Property_Summary_Table).

<span id="a76e6489"></span>
## Can preset properties be deleted?

Preset properties cannot be deleted, which will affect the calculation of some basic metrics.

<span id="448ac886"></span>
## How is the reported data of preset properties calculated?


* Whether it is the calculation criteria of the new user: [New and existing users/whether it is relevant on the first day](https://docs.byteplus.com/docs/DataFinder/Statistical_Criteria_Value_Logic#3dac52c5).

* Page referrer calculation criteria: [Logic for Judging the Source of Page Visits](https://docs.byteplus.com/docs/DataFinder/Logic_for_Judging_the_Source_of_Page_Visits).


See more calculation methods and value logic [Statistical Criteria & Value Logic](https://docs.byteplus.com/docs/DataFinder/Statistical_Criteria_Value_Logic).

<span id="61a23cf5"></span>
## Will preset events contain custom public properties?

Custom public properties will also be reported in the public field header when reporting, and will be reported in the public field header along with the triggered preset events, custom events and other data.

<span id="6a5a4341"></span>
## Do all events necessarily carry event public properties?

Event public property Only when the property value is explicitly set will all events be reported with this public property. If the value of the public property is not set, all events will not be reported.

Therefore, under normal circumstances, the mobile SDK will report some preset events, and some public properties will be set before reporting, so the preset events and custom events reported by the mobile end SDK will generally carry some public properties.

However, the event reporting of the server level SDK does not set public properties in advance, so it needs to be set manually.

For example, the platform type belongs to the event public attribute, and the mobile end SDK will automatically collect and set it, so the general mobile end event will carry this attribute. However, server\-side events are not carried unless the server level manually sets the platform event public property.

<span id="d8d47f54"></span>
## Preset Exposure Event Capture Supported Versions

iOS, Android SDK: 6.10.1 version starts to support

Web SDK: 5.1.1 version is supported

<span id="78307b37"></span>
## Can version data be converted to string?

Changing from version type to string type does not affect historical data, and historical data can be queried normally.

<span id="9cd9ab25"></span>
# Full event tracking preset events/properties

<span id="6098c5b9"></span>
## Application scenarios for full event tracking? Differences with custom event tracking?


|comparison term |Code event tracking |Full event tracking |
|---|---|---|
|Event tracking |Code event tracking refers to the development engineer, according to business personalized needs, manually write the code to achieve data collection logic. |Full event tracking, also known as "no event tracking", "no trace event tracking" and "automatic event tracking". Full event tracking is automatically collected and reported for the browsing of standard pages and the clicking of standard elements, without the need to develop and develop code for event tracking integration. |
|capture event |The acquisition range is wide, and theoretically, as long as it is an interactive operation on the application side, it can be collected.<br><br><br>* DataFinder provides you with preset events and properties that you can combine with the supported preset events and properties to supplement with custom code event tracking.<br><br>* For details of supported preset events/properties, see [Preset Property Summary Table](https://docs.byteplus.com/docs/DataFinder/Preset_Property_Summary_Table). |All event tracking events collected are bav2b_click button clicks, bav2b_page page browsing and other events. For details, see [Full Event Tracking Preset Events and Properties](https://docs.byteplus.com/docs/DataFinder/Full_Event_Tracking_Preset_Events_and_Properties). |
|applicable scenario |* It is suitable for scenarios where the logic of related fields of the collection and analysis business is tight, and the analysis is more focused.<br><br>* Especially some non\-click, **non\-visual** behavior, non\-code event tracking implementation is not possible.<br><br><br>For example: search results return, registration results return, banner, floor, personalized recommendation/thousand people and thousand faces page. |* Applicable to activity pages, landing pages, simple analysis of UV, PV, clicks and other basic indicators;<br><br>* Simple analysis or statistical requirements, events that do not require custom attribute settings such as parameter transfer for event tracking events; |
|advantage |* Complete business information;<br><br>* Events, properties, reporting timing, etc. can be customized and controlled<br><br>* Capable of fully restoring user behavior links |* No need for developers to enter manually, the least intrusive to business code,  **++less work ++** ;<br><br>* Full event tracking event data is automatically and continuously collected when the SDK is deployed, which means that even if specific events are not explicitly specified to analyze initially, full event tracking's continuous and comprehensive data collection enables **data re\-run** \- that is, past data can be queried and analyzed at any time. |
|disadvantage |* The event tracking of each control needs to add corresponding code, which is a lot of work and requires developer support and coupling with business code;<br><br>* After the version is launched, the iteration flexibility of event tracking content is low |* Undifferentiated full collection generates invalid data reporting, wasting traffic/storage/computing resources;<br><br>* The data format is non\-business\-oriented, with automatic collection of all event data.<br><br>* Unable to collect business\-related properties<br><br>* There are some limitations to the development framework, as detailed in the full event tracking section of the [Client side](https://docs.byteplus.com/docs/DataFinder/SDK_Feature_List#%E5%AE%A2%E6%88%B7%E7%AB%AF).<br><br>* Still need to target specific user behavior through virtual or circled events |
|Integrated Operations Guide |* Preset events and properties: You don't need to do any configuration, and the corresponding data will be automatically collected and reported according to the triggering mechanism.<br><br>* Custom code event tracking:<br><br>   * First, according to business analysis needs, plan the custom event tracking and properties that need to be collected and reported.<br><br>   * Enter the corresponding event tracking and properties in the DataFinder console, and drop the event tracking and property names into the library first.<br><br>   * When integrating the SDK, refer to the operation guide for reporting code event tracking to configure. |* When integrating the SDK, turn on the full event tracking switch. |
|Stop data reporting |If you don't want to collect and report some code event tracking data, you can disable the corresponding event or attribute in the **Data Management** \> **metadata management** of the DataFinder console. |If you do not want to collect and report full event tracking data, you can turn off the full event tracking switch in the DataFinder console. No need to modify the full event tracking switch in the integration code. |
|data analytics |* Most analysis tools can directly use the event tracking data reported to the database.<br><br>* Heat map and circle event functions can only be used if full event tracking is enabled. ||


<span id="7055f6e1"></span>
## How to turn on and off the full event tracking switch?


1. If you want to collect full event tracking data, you need to turn on the full event tracking switch in the integrated SDK code during the Data Transmission Service phase. Some SDKs turn on the full event tracking switch by default. If it is not turned on by default, you need to turn it on manually.

2. After the Data Transmission Service is completed, in the subsequent data query and analysis stage, you need to ensure that the full event tracking switch is turned on in the Project Center \> Project Management \> SDK Settings.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ae4e1b94a89475dbc719124ea3ad98d~tplv-goo7wpa0wc-image.image) </span>

3. If you don't need to continue collecting full event tracking data in the future, you can turn off the full event tracking collection switch in Project Center \> Project Management \> SDK Settings.


<span id="df7c34a1"></span>
## Does full event tracking collect sensitive user information, such as mobile phone numbers and ID numbers?

Full event tracking events do not collect user sensitive data. Please refer to [Full Event Tracking Preset Events and Properties](https://docs.byteplus.com/docs/DataFinder/Full_Event_Tracking_Preset_Events_and_Properties).

When DataFinder collects data, it collects data based on data analytics requirements, such as the process information of the host app (that is, the developer app) itself, the restart time of the mobile phone system, etc. Please refer to the details [[Growth Marketing Kit SDK] Privacy Policy](https://docs.byteplus.com/docs/DataFinder/Growth_Marketing_Kit_SDK_Privacy_Policy).

<span id="abdb554d"></span>
## What are the events that are enabled by default in the full event tracking event?

For the full range of event tracking data currently supported, see [Full Event Tracking Preset Events and Properties](https://docs.byteplus.com/docs/DataFinder/Full_Event_Tracking_Preset_Events_and_Properties).

<span id="34854f15"></span>
## What is the meaning of the attribute value corresponding to the element_class_name of the full event tracking event? Why is the element_class_name attribute value of a click or exposure event reported in the same second sometimes empty?


* element_class_name for the full event tracking event property "element class name", which is used to record the name of the front\-end frame element, such as the element name using the Vue frame. In the full event tracking scenario, if the class attribute is set on the page dom, the class name of the element will be reported.

* Click or exposure event reported in the same second element_class_name property value is empty, it may be because the content of the control is empty at the first exposure, and then the content of the control is refreshed instantaneously, resulting in the content of the second exposure is empty. The existing full event tracking logic is to automatically collect and report the browsing of standard pages and the clicking of standard elements. For exposure events of non\-standard pages or elements, it is currently not supported.


<span id="eb0380f4"></span>
## In custom event, if you want to reuse some properties in the full event tracking event, can the finder SDK support it?

Direct reuse of properties in full event tracking events is not currently supported. You need to manually add the required properties in the custom event.

If you want to include certain properties in every event, you can do so by setting public properties so that they are automatically included in all events.

<span id="73b11fab"></span>
## Flutter\-only app with integrated webview, does it support full event tracking?

Flutter\-based apps enable and use full event tracking.

<span id="c77910a2"></span>
## What is the difference between bav2b_page and bav2b_page_statistics?

bav2b_page event: The reporting time is divided into independent page and SPA (single page application), and the independent page is reported once after the page is opened and the SDK initialization is completed. If it is a SPA page, it will be reported once after the SDK initialization is completed, and once when clicking to switch the page. The main data collected are some parameters of page browsing, which are used to analyze page browsing behavior.

bav2b_page_statistics event: the reporting opportunity is after the page is opened, the SDK initialization is completed and reported once (both the independent page and the SPA are reported only once), the data collected is mainly the page loading time, page width and height statistics, used to analyze page loading statistics and other information.

<span id="8e10d09b"></span>
# Ad monitoring preset events/properties

<span id="27f3f320"></span>
## When is the time for app activation callbacks?

When the user installs, uninstalls and reinstalls, and installs updates for the first time, the app activation will be triggered and returned in real time.

<span id="eaf4d78e"></span>
## The UTM parameter is recorded for the first time. How long will this UTM link exist? When will it be out of stock?

The valid period of the UTM parameter depends on the lifetime of the SDK. If SDK is shut down or restarted, the UTM parameter will be invalidated. If the SDK continues to the next page, the UTM parameter will continue to take effect. If the page is single\-page and multi\-routed, the utm parameter will also continue to take effect. If the customer finds that they will bring it when they operate the page up and down, but also when they re\-enter the page, then this utm parameter will be stored in the cookie. If each page is independent, then the utm parameter will disappear. If you re\-enter because you reset the utm parameter, or use this, it can be passed to the next domain name.

<span id="278bead5"></span>
## If you don't buy the ad monitoring function and want to use the url to carry the utm parameter, how can the utm parameter be collected in this case?

You can customize the parameter utm_xxx on the landing page path of web/js or Mini Program, and it will be automatically collected after integrating the sdk.

<span id="65724fd0"></span>
## Will the ad monitoring SDK collect users' CAIDs and provide corresponding privacy protocols when performing ad attribution?

Caid belongs to the ID provided by the China Broadcasting Association sdk. At present, Finder has not yet established a cooperative relationship with the China Broadcasting Association, so it has not been connected to caid for the time being, and there is no need to provide a privacy statement. Advertising attribution is dependent on device ID, IDFA, and IP.

<span id="35a98025"></span>
## Can advertising monitoring connect to the app store on the APP side to collect app download data?

Currently, docking with the app store to obtain relevant data is not supported.

<span id="ac657843"></span>
# Custom events/properties

<span id="b60a536e"></span>
## Is nested list data supported when reporting custom event/attribute data?

Property of the current list type do not support nesting when reporting data. In this scenario, it is currently recommended to convert the data into a String by escaping and then report it. For example:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a7d252aefa294acb8160572704ccadbd~tplv-goo7wpa0wc-image.image) </span>

<span id="69f872fd"></span>
## Can the display name and event description in a general event be added during event tracking? Or can it only be added on the front end?

Event tracking cannot be added, it can only be added on the data management page.

<span id="d0bb51f6"></span>
## Custom processing logic for user properties

In SaaS\-non\-cloud native scenarios (including overseas BytePlus environments), custom user properties are divided into real\-time data and offline data.


* The data of the day is real\-time data, and the custom user properties are reported following the event. When querying real\-time data, the custom user properties are also displayed according to the attribute values carried by the event at that time. For example: A event reports the custom user attribute as iOS, B event reports the custom user attribute as Android, then event analysis. If the A and B events are selected, the custom user attribute will display iOS and Android. Select the A event individually, and customize the user properties to display iOS.

* Non\-day data is offline data, and offline data will be built uniformly after the end of the day. When custom user properties are built offline, the latest value of the day will be taken as the value of all this attribute today according to the day dimension. For example: The customized user properties reported on 3\-12 are sorted by time. There are iOS, Android, mp. When the offline data is built on the 3rd\-13th, the value of the latest customized user attribute = mp will be refreshed to all the values of this attribute on the 3rd\-12th.


<span id="58ecd792"></span>
## Does it support custom IP properties and be resolved to the corresponding country and city?

No, the ip is detected by the gateway and added to the data stream after reporting. The preset properties of the ip cannot be customized.

<span id="62c6129b"></span>
# SDK Integration: Universal

<span id="6bfb3748"></span>
## What are the differences between client side Data Transmission Service and server level Data Transmission Service?

In most business scenarios, you will need to access both client side and server side data.


* Using the client side for SDK integration, most of the user behavior data can be collected and reported directly based on the client side.

* The main scenarios for using server level SDK integration are:

   * Customers have special scenarios such as self\-built SDKs, which can only forward data through the server level.

   * The event data to be collected does not come from front\-end user operations, such as issuing coupons, changing transaction status, etc. Such data is stored at the server level and needs to be reported through the server level.

   * For some very specific device types, such as ATM machines, the current DataFinder client side SDK does not support direct data collection, so it needs to access the data through the server level.


In addition, some users will also consider whether subsequent upgrades are convenient when choosing to use the client side or server level to access data.


* The upgrade of the client depends on the operation of the front\-end user, and the upgrade reach efficiency is relatively slow.

* The upgrade of the server is operated by the business itself, and the upgrade is highly efficient.


<span id="11271445"></span>
## Business applications have their own real\-name ID data. How to report user data so that a specific user can be found in the DataFinder later?

If your business application is mainly an application that requires the user's real name to log in, and has a field that uniquely identifies the user (for example, by account ID \- account_id, to uniquely identify a user), in this scenario, you can report the user ID field account_id to the user_unique_id (uuid) attribute field of DataFinder, and then need to query a user:


* You can find this user by filtering `user_unique_id = this user's account_id`.

* If you also want to query the ssid of the corresponding user, you can find the corresponding ssid through uuid in the user details.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ea0f70d073d4272801252d661bcf07c~tplv-goo7wpa0wc-image.image) </span>


<span id="eca95112"></span>
## How to set up UUID?

UUID (User_Unique_ID) can not be set if the user is not logged in, we will fill it with DID (Device ID). After a user logs in, they can be set to their own UID, and our statistical metrics will identify users before and after logging in as the same user.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Please do not set the UUID to a fixed value, as this will identify a large number of users as the same user, causing statistical differences.</div>


<span id="6f8d3956"></span>
## Can UUID be set to Chinese?

No, please do not upload UUID to Chinese. UUID only supports numbers, letters and symbols. If uploaded in Chinese, the data cannot be reported, resulting in data quality problems.

<span id="3e4a7a37"></span>
## When reporting UUID, I hope to bring the source channel for reporting UUID. How to set it up?

Through the interface reported by the server level, the data will be reported by the server level source by default; the content of the reported data is customized. If you want to distinguish the client side types of different UUID sources, you can also use the preset source side to distinguish.

<span id="358185c3"></span>
## The UUIDs of the two APPs are inconsistent, but the mobile phone numbers are the same. Can the data be connected?

In the case of inconsistent UUIDs, SSIDs cannot be kept consistent. If you need to keep the data open, you need to ensure that the UUIDs (user_unique_id) of the two APPs are consistent.

<span id="6d7c54c0"></span>
## In a SaaS\-non\-cloud\-native environment, user_id attribute is reported in custom event, but user_id not present when queried?

In a SaaS\-non\-cloud\-native environment user_id this attribute is a preset user attribute if:


* If you report user_unique_id, user_id = user_unique_id;

* If you do not report user_unique_id, user_id = web_id/device_id.


<span id="7148b6a3"></span>
## When querying user properties, there is only one userid and no other data, and user properties cannot be queried in white screen operation and maintenance?


* In the case of a single user ID type, the reported user attribute is generally not constructed but the user is created. You can check whether the reported user attribute type and the corresponding value of the type are correct.

* In the case of multiple user ID types, after using the one_id service, the user ID system items are unified, and the user attribute display needs to be checked in the user portrait. If you still can't find the user attribute after checking, it may be because the user attribute has nothing to do with the uuid that can be found, and you need to confirm whether the data report is accurate.


<span id="2f1c8f78"></span>
## How to get Web_id?


* Request backend service: `window.collectEvent ('getToken')`

* Do not call the backend interface: `window.collectEvent ('ready ', () => { const web_id = window.collectEvent (' getConfig ',' web_id ') })`


<span id="73e9e6e7"></span>
## How to configure the collection of geolocation data?

The Finder SDK will resolve the address information through the Internet Protocol Address by default. If you need to collect coordinate information, additional configuration is required. Internet Protocol Address Resolution is the location of the Internet Protocol Address resolved by the data stream when an event is reported to the Finder. SDK itself does not collect IP information, but by the server according to the source IP resolution. The SDK can collect coordinate information, but if you need relevant configuration, you can consult the access documentation.

<span id="b18c4d88"></span>
## How to capture the uninstallation behavior of applications on the device through the SDK?

The DataFinder SDK cannot directly capture the uninstalled behavior of applications on the device, but you can calculate the uninstalled behavior data of applications by filtering app activation events in subsequent data analytics. For example:


* Select `Installation Type = Uninstall Reinstall`to count how many users have uninstalled.

* Business can be calculated by "uninstall users" as `users who activate the reinstallation`plus `users who do not trigger behavior and do not activate multiple times within a certain business scope`, which can approximately handle the uninstall behavior.


<span id="6eb4d3d2"></span>
## There is a problem with the set operation of profile, and the second set operation will fail.

First, you need to check the integration SDK code for any issues. If there is no problem with the user's code, then consider bypassing the problem at the code level. The specific solution is to extract a tool method from the method of setting user properties, store all the user properties that need to be set in an array, and then call the profileset to send the user properties one by one by traversing, rather than calling the interface to send all the user properties at once. The array method guarantees the order of calls and avoids user property override errors. At the same time, in the current version, there will be a 60\-second time limit when calling profile_set. When reporting user properties within the time limit, if the same key exists, it cannot be reported, and the restriction needs to be lifted.

<span id="95b4d642"></span>
## The reporting frequency of the SDK is set to less than 10s, which does not take effect?

Confirm that the SDK internally limits the minimum reporting frequency to 10 seconds, so setting a frequency less than 10 seconds will not take effect.

<span id="6b02a12b"></span>
## What is the role of web and Mini Program time configuration in the SDK settings of the Project Center?

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/80297e6a7d084d768d6ca108f5255676~tplv-goo7wpa0wc-image.image) </span>

It controls the maximum completion time of each request. If the request does not come back after this time, it will actively consider it timed out and deal with it accordingly according to the request failure.

<span id="b9b5fc63"></span>
## When using the AppLog.setUserUniqueID method, is the data immediately reported to the server level or is there a delay?

The AppLog.setUserUniqueID method is immediately reported to the server. If you want to stop the service of the business application, you want to decide whether to delete the business data according to the situation reported by the AppLog.setUserUniqueID method. If you encounter the problem that the uniqueid cannot be found, it may be due to the absence of a set id, or the timing of setting the id is problematic. You can try to capture the package to view the log, or view the log on the debug board.

<span id="1d46ebee"></span>
## How to collect data on the proportion of users who have read an article?

The Finder can capture the read percentage of articles through custom events. You can add code to the article page to track the user's reading progress and report it as an event property. For example, you can set an event named "article_read_progress" and trigger an event report every certain percentage of reads (e.g. 10%, 20%,..., 100%), and the event property contains a "progress" field to indicate the read percentage. This way, you can analyze the user's reading depth of the article in the Finder.

<span id="2d283969"></span>
## How is JSON type data reported?

If you need to collect and report data in JSON format, you can escape the data into string type for storage. Please see for details [Example 1: How nested JSON type properties are reported and used for filtering and grouping](https://docs.byteplus.com/docs/DataFinder/Property_Custom_Grouping_and_Properties#1fafd5b2).

<span id="265efce2"></span>
## When integrating the SDK, there is a class duplication between the pangle pangolin dependency package and the volcano finder dependency package, and the compilation reports an error. How to solve it?


* Abnormal phenomenon:

   * Pangle pangolin dependency package: api 'com.pangle.global: ads\-sdk: 6.0.0.7'

   * DataFinder Data Access SDK: com.bytedance.applog: RangersAppLog\-Lite\-cn: 6.14.3

   * Error report:

      ```JavaScript
      Duplicate class com.bytedance.applog.encryptor.EncryptorUtil found in modules jetified-encryptor-0.0.9-rc.2-private-runtime (com.pangle.global:encryptor:0.0.9-rc.2-private) and jetified-encryptor-1.0.1.noasan-runtime (com.bytedance.frameworks:encryptor:1.0.1.noasan)
      ```
      

* Solution:

   Pangle modify the integration method:

   ```JavaScript
   implementation ('com.pangle.global:ads-sdk:6.0.0.7 '){
   exclude group: 'com.pangle.global', module:'crash_monitor'
   exclude group: 'com.pangle.global', module:'global:encryptor'
   }
   ```
   


<span id="82e9699d"></span>
## There are APP\-side applications and Web\-side applications at the same time. Now what should I do if I want to report the data collected by both ends to the same application (appid)?


* If you just want to report the data of the two ends to the same application (appid), and do not need to get through the user data of the two ends, then you can directly set the app_id parameters to the same app_id in the initialization configuration when integrating the SDK.

   * For example, you can integrate the APP\-side SDK, Web\-side SDK, the app_id parameters are set to the APP\-side app_id, the subsequent APP\-side, Web\-side data will be reported to the APP\-side application, you do not need to switch applications frequently when subsequent data query analysis, you can query the APP\-side, Web\-side data in an application.

   * However, note that in this way, although the data is reported to the same application, the data is not connected to each other, especially user data. That is, if the same user uses the APP\-side application and the Web\-side application respectively, a user identification ID (ssid) will be generated on both the APP\-side and the Web\-side, which will be identified as two users.

* If you want to report the data to the same application, but also want to APP\-side, Web\-side user data to get through, you can integrate the two\-side SDK, turn on the embedded H5 switch. Turn on the embedded H5 switch, the subsequent H5 page data will be reported to the application of the APP side, and the user identification data of the H5 page and the user identification data of the APP side can be connected.


<span id="_1-sdk接入"></span>
# SDK Integration: APP \- Android

<span id="_1-5-android-sdk-接入为什么会出现didn-t-find-class-com-android-id-impl-idproviderimpl-报错？"></span>
## Android SDK access Didn't find class " com.android.id .impl. IdProviderImpl" error?

This error does not affect the normal initialization of the SDK.

The reason for the error is that the current version of the SDK provides the ability to obtain the device ID of Huawei and Xiaomi's latest version (AndroidQ) mobile phones. When running in the emulator or lower version of the device, the console will print this error message, but it will not affect the normal initialization and use of the SDK.

<span id="1d398312"></span>
## Which version of Android cannot capture Android_id?

Android_id not available on Android 10 or above.

<span id="8b7902e0"></span>
## Which version of Android supports turning off device IMEI capture?

Android 6.9.0 and above.

<span id="b9dae3ec"></span>
## Android SDK 6.16.9 version integration error: "java.util.ConcurrentModificationException"


1. It is recommended that customers do not add modification logic after passing in the JsonObject to avoid crashing.

2. In 6.16.10 version, the SDK will copy the JsonObject after receiving it to avoid crashes caused by customer modifications.

    &nbsp;


<span id="what-should-the-android-sdk-pay-attention-to-when-switching-users-across-multiple-criteria"></span>
## What should the Android SDK pay attention to when switching users across multiple criteria?

Example path: (1) Default criteria uuid \- \> (2) Specify criteria card number \- \> (3) Default criteria uuid

At this time, when 2\- \> 3 switches, the third step setUserUniqueID (uuid) is equal to = setUserUniqueID (uuid, oldUuidType)

There are two methods of rejection:


1. Use the following code:

   ```Plain
   AppLog.setUserUniqueID("001")
   AppLog.setUserUniqueID("card number aaa","card_no")
   AppLog.setUserUniqueID("001","")
   ```
   

2. Use the following code:

   ```Plain
   AppLog.setUserUniqueID("001","id_type")
   AppLog.setUserUniqueID("card number aaa","card_no")
   AppLog.setUserUniqueID("001","id_type")
   ```
   


The above two methods can achieve multi\-aperture switching users.

<span id="293a8d3a"></span>
## Android SDK call `AppLog.setHeaderInfo`set a header property, immediately event tracking event, this event tracking must be able to bring the set header property, right?

Not necessarily.


1. Setting public properties is not real\-time, so there is a delay. If event binding is required, it is recommended to set event custom parameters. If you need the event to carry the value of that moment, you can consider using event custom parameters, or reporting event tracking immediately after calling `AppLog.setHeaderInfo`.

2. If an event and custom are updated when switching users

   The event is returned to the previous user, and an immediate report is triggered when switching. At this time, the custom update cannot be perceived after copying the header.

   The follow\-up events should be reported normally and regularly, and they will also enjoy the updates of custom.

    &nbsp;


<span id="does-the-android-sdk-integrate-com-google-android-play-services-maps-library"></span>
## Does the Android SDK integrate com.google.android: play\-services\-maps library?

DataFinder's Android SDK does not directly integrate the com.google.android: play\-services\-maps library, which the current Android SDK relies on.

<span id="514a6cd1"></span>
## What is the reason for the crash after integrating Android 5.5.1 version and ICT SDK 1.0.26 version at the same time?

Android SDK 6.4.0 version is adapted to the 1.0.26 version, it is recommended that customers upgrade the Android SDK version.

<span id="cf9aed3e"></span>
# SDK Integration: APP \- iOS

<span id="f42fe80b"></span>
## iOS if using swift, does the pod require users to bridge themselves?

Yes, the current iOS SDK only supports object\-c, but Swift does not directly support it.

<span id="bf1d05a8"></span>
## iOS manually import the SDK, the editing stage prompts: Undefined symbol: *OBJC_CLASS* $_BDAutoTrackConfig What is the reason?

Such abnormal prompts may be caused by engineering configuration problems. You can check whether there are redundant dependencies or missing necessary dependencies in the dependency configuration, remove redundant dependencies (such as sg modules), supplement necessary dependencies (such as volc encryption modules), adjust Header Search Paths and Linker Flags, and then perform SDK integration to see if the integration is successful.

<span id="d3873f75"></span>
## When integrating the SDK on the iOS side, if you are using a SaaS\-non\-cloud\-native\-overseas BytePlus environment, does it support the installation and use of DevTools components?

The version of iOS SDK for SaaS\-non\-cloud\-native\-overseas BytePlus environments needs to be upgraded to 6.17.0 and the following code added to the Podfile to integrate DevTools components:

```SQL
pod 'RangersAppLog', '6.17.0',
    :subspecs => [
        'Host/SG',
        'Core',
        'UITracker',
        'OneKit',
        'Log',
        'Picker',
        'Unique',
        'VolMetaSecML',
        'DevTools'
    ]
```


Make sure that the DevTools button is displayed in the view lifecycle method of the main controller to avoid being obscured by other UI elements.

<span id="8ebc17cb"></span>
# SDK Integration: APP \- HarmonyOS

<span id="60c43536"></span>
## When HarmonyOS integrates the DataFinder data access SDK, what is the minimum version requirement of Harmony system?

API12 (Developer Beta 3) and above.

<span id="65d30cf5"></span>
## Does the HarmonyOS SDK support A/B testing related events?

Support.

<span id="ed1b15cc"></span>
## Does the HarmonyOS SDK support OAID/carrier information acquisition switches?

HarmonyOS SDK supports OAID/Carrier information acquisition switch since 1.3.0 version.

<span id="250e3d64"></span>
## Does the HarmonyOS SDK support multithreading/multiprocessing?

Multithreading/multiprocessing is not currently supported.

<span id="02b34bba"></span>
## Does the HarmonyOS SDK support x86 emulators?

1.3.1 version supports the x86 emulator.

<span id="5573de61"></span>
## What is the function of Pako in the HarmonyOS SDK?

Pako is the gzip tool officially recommended by Harmony. At present, the DataFinder system does not have a ready\-made gzip interface. It is recommended to use pako dependency. The SDK has request encryption internally, and encryption is accompanied by gzip, so it is necessary to rely on it.

<span id="a64c3f8b"></span>
## How to get offline pako har?

If your environment cannot support the introduction of dependencies online, you can contact BytePlus technical support for offline pako's har.

<span id="33be3fff"></span>
## 1.3.0 version of offline integration pako found error?

Add the overrides configuration to force the offline version or a specific version.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7de5f2496b6745f0b5dff9c8bd2f2bfe~tplv-goo7wpa0wc-image.image) </span>

<span id="2e445509"></span>
## HarmonyOS SDK integration error: ERROR: ArkTS: ERROR Failed to resolve OhmUrl?

This error occurs because pako is not dependent. You need to refer to the help documentation to complete the configuration of pako dependencies.

<span id="99a2a6a3"></span>
## HarmonyOS SDK integration error: Cannot read property eventHub of undefined?

This error occurs because the context of the initialization SDK is incorrect.

<span id="699db9bc"></span>
## HarmonyOS SDK upgrade error: Can't find  **@volcengine/applog**

It may be caused by regular customers upgrading the SDK version. The SDK import of the previous version is @ohos/applog. You need to adjust the import name. Please refer to the latest documentation: [HarmonyOS Next SDK Integration](https://docs.byteplus.com/docs/DataFinder/HarmonyOS_Next_SDK_Integration_).

<span id="ed89076f"></span>
## ERROR: Bytecode HARs: [@volcengine/applog, @volcengine/applog_devtools, @volcengine/applog] not supported when useNormalizedOHMUrl is not true?


* Full error report:

   ```JavaScript
   ERROR: Bytecode HARs: [@volcengine/applog, @volcengine/applog_devtools, @volcengine/applog] not supported when useNormalizedOHMUrl is not true.* Try the following:> Please check useNormalizedOHMUrl in the project-level build-profile.json5 file.
   ```
   

* Solution: Add this configuration in the root directory and compatibleSdkVersion adjusted to 12.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e9b9fc1d1314aadb9c735a2965dd7b8~tplv-goo7wpa0wc-image.image) </span>

   [Reasons to add this configuration(Building a Bytecode HAR) ](https://developer.huawei.com/consumer/en/doc/harmonyos-guides-V5/ide-hvigor-build-har-V5#section179161312181613):

   * The bytecode of the compiled product is compiled in advance, so the efficiency of application\-side compilation can be improved.

   1. Projects after Ide 800 are enabled by default.


<span id="1e33f1f0"></span>
## After upgrading to the new version of the HarmonyOS SDK, don't you see the features of the new version?

After upgrading the SDK, you need to sync it.

<span id="47ee7b1f"></span>
## Error: ERROR: ArkTS: ERROR Failed to resolve OhmUrl?


* Complete the error message:

   ```JavaScript
   ERROR: ArkTS:ERROR Failed to resolve OhmUrl.
   Error Message: Failed to get a resolved OhmUrl for "@volcengine/applog" imported by "/Users/bytedance/DevecostudioProjects/SDK50/oh_modules/.ohpm/@volcengine+applog_devtools@7hba3+yrkmv76lfmmoxyslxamstpksemeh++r+9qtz8=/oh_modules/@volcengine/applog_devtools/src/main/ets/plugin/DevTools.js".
   ```
   

* Possible reasons:

   * Possible reason 1: AppLog introduces a wrong name.

      The main reason for encountering this problem is that when relying on components, the names of the previous components can actually be written arbitrarily, but the agreement between applog and devtools is specific, which is written as @ **volcengine/applog** . Please check whether the name of the AppLog dependency is written correctly. Please strictly follow the documentation integration.

      ```JavaScript
      //Import AppLog strictly by that name
      "@volcengine/applog": "file:../applogx/applogx.har",
      "@volcengine/applog_devtools": "file:../applogx/applogx_devtools.har"
      ```
      

   * Possible reason 2: AppLog is depended on in the sub\-module, and an error is found after the sub\-module is also depended on by other modules.

      Since Harmony does not support dependency passing, the SDK depended on in the sub\-module cannot be referenced by other modules. Please add dependencies to the corresponding module. For example, if a submodule depends on applog and entry depends on submodules, please also add applog full dependencies to the entry module.


<span id="0d7499f8"></span>
## The HarmonyOS SDK only reported an error after upgrading DevTools: Can't find BavEvent?

Due to the adaptation of new features, AppLog and devtools need to be upgraded to 1.2.0 \-xx version, only upgrade Devtools can not.

<span id="8132a077"></span>
## When integrating the HarmonyOS SDK, an error is reported when integrating DevTools with the new version of the IDE?

Remember to override applog, and override to the oh\-package.json5 of the root node.

<span id="de36249d"></span>
## When HarmonyOS SDK integrates DevTools, the pop\-up window display is abnormal. What is the reason why the pop\-up window content is displayed in Devtools?


* Solution 1: It may be that there is a problem with you getting the window object. LastWindow does not distinguish between the main window and sub\-windows. It is recommended to change window.getLastWindow to context.windowStage.getMainWindowSync ().

* Solution 2: If the first solution is not good, you can upgrade to the 130\-rc1 version, turn off the sub\-window mode, and use the page mount method.


<span id="05232fae"></span>
## How to get the data of Harmony side did?

Please refer to the official website document: [Subscribe to DID](https://docs.byteplus.com/docs/DataFinder/HarmonyOS_Next_SDK_Event_Tracking_and_Properties#07e460b1).

<span id="e39b8028"></span>
## What type of event reports are received at Harmony?

The event custom property is of EventRecord type, which is a custom type. Other types are not supported because the SDK needs to do type checking to avoid receiving types that cannot be parsed, so the SDK restricts the receiving types.

1.1.0 EventRecord = Record<string, number | string | boolean\>

1.2.0 EventRecord = Record<string, number | string | boolean | string[]\>

<span id="3a1bb035"></span>
## What is the HarmonyOS SDK reporting strategy?

Default is reported once a minute, but there is no specific number of reports, SDK strategy for the new reporting strategy by volume query events (Android/iOS query by the number of queries), each report query about 1M data to report, no longer 200 shall prevail (can be reported as much as possible).

<span id="814fa6f6"></span>
# SDK Integration: APP \- Embedded H5 related

<span id="e8059bc9"></span>
## The H5 page is embedded in the APP. Which SDK should be connected to the Data Transmission Service?

If the APP has an embedded H5 page, when you want to collect H5 page data and APP data at the same time, you need to integrate the APP SDK and the Web SDK respectively, and turn on the embedded H5 switch on both sides when integrating the SDK. After turning on the switch with embedded H5, the data of the subsequent H5 page will be reported to the application on the APP side, and the user identification data of the H5 page can be connected with the user identification data of the APP side. For details, see [H5 through the introduction](https://docs.byteplus.com/docs/DataFinder/Android_SDK_Integration_Scenario_Practice#5dca8fbf), [APP gets through to H5 to report](https://docs.byteplus.com/docs/DataFinder/Web_JS_SDK_Integration_Scenario_Practice#317fefda), and [Associated with H5 page web_id](https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_Integration_Scenario_Practice#f1c46931).

<span id="477959c1"></span>
## The H5 page is embedded in the APP. What is the reason why H5 and the APP cannot be connected when opened for the first time?

Determine whether the APP has the setting of checking the privacy permission and the function linkage. There is a possibility that the APP SDK did not start because the user did not check the privacy configuration, but at this time the H5 page has loaded the JS SDK, resulting in the JS SDK being reported.

<span id="5f2074e4"></span>
## After the Android SDK and H5 are connected, the WebView white screen does not load the content. Why?

The Android SDK will intercept the LoadUrl method to identify the H5 address when connecting with H5. If there is a LoadUrl method in the user's Activity, it may be intercepted by the SDK, resulting in WebView failing to load content.

<span id="f1d3623e"></span>
# SDK integration: web\-side

<span id="8cb140f6"></span>
## Web page iFrame the content of another page, how to integrate SDK integration?

If the A page iframe introduces the B page, you need to integrate the data access SDK of the web side in the A and B pages at the same time. After the integration is completed, the subsequent front\-end users operate the B page of the iframe in the A page to generate behavioral data. After the data is reported to the app_id reported on the B page.

Therefore, there are the following considerations in this scenario:


* Since the SDK integration of A and B pages is integrated separately, the data is reported in two applications. If you want to report the data to the same application, you can configure app_id parameter value to the same appid when integrating the SDK.

* The user data of pages A and B in this scenario cannot be accessed.


<span id="a569564d"></span>
## The log: true switch is turned on during initialization, and the browser console prompts "app_id param is error must be number, please check!"

Check that the initialization code app_id configured correctly should be of type number. If it is a string type, initialization fails with the above error message.

<span id="9609a387"></span>
## Why does the browser console keep printing logs on the web?

In the SDK initialization code, after setting log: true, the debug log will be printed. If it does not need to be enabled, it can be set to false.

<span id="db20d476"></span>
## When using the 5.1.11 version of the web\-side SDK, there is no response to implanting content **in the browser plug\-in** . After initializing the SDK, the console has no information, and the initialization is not successful

When integrating JSSDK code into content, you can try to load it using the npm package, and then use tools such as webpack to compile the import syntax in content.js into a syntax that can be run in the browser environment. [Operate the reference link ](https://www.npmjs.com/package/@datarangers/sdk-javascript), the core steps are as follows.


1. Use the npm package and import it in content.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/35c73983e4a24639a794f62325fa464a~tplv-goo7wpa0wc-image.image) </span>

2. Compile with webpack.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/278d041a13464ca9a9d5c00d19870e25~tplv-goo7wpa0wc-image.image) </span>

3. Modify the entry file in manifest.json.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f457897bc7c47b7b8f0c8c79c414491~tplv-goo7wpa0wc-image.image) </span>


<span id="a7e9dd58"></span>
## In web/js sdk, after opening full event tracking, the element_id of the full buried click event cannot be obtained?

As shown in the figure below, the element_id of clicking on the < div \> inside is the id of the ancestor element. Currently, collection is not supported. It is recommended to customize the event tracking report, or divide the button into two layers and apply the id respectively.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2d5b3847f5a4b7dbe4c76cb728f0d96~tplv-goo7wpa0wc-image.image) </span>

<span id="289584ea"></span>
## Web SDK on allow_hash switch does not take effect?

In a single\-page application environment, the spa automatically collects page dwell time. But if it is not accurate and you want to calculate it yourself, you can use `disable_route_report`to turn off hash routing listening. But at this point allow_hash configuration will fail.

<span id="887d276e"></span>
## When using web/js sdk to report events, the Request Headers of individual list interfaces contain Content\-Type: text/plain; charset = UTF\-8, while Response Headers: Content\-Type: application/json; charset = utf\-8. Why is it different?


* Problem description

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92fcb149400840a9a89d8dbb0711f6a4~tplv-goo7wpa0wc-image.image) </span>

* Answer: This situation is as expected. It is known that predefine_page_alive, predefine_page_close events sent using beconEvent. The default data type of this method is text/plain; charset = UTF\-8.


<span id="017df88a"></span>
# SDK Integration: Mini Program

<span id="2379a379"></span>
## Why is there no preset event reported when Mini Program accesses the SDK?

The current Mini Program side supports the use of preset events. If there is no reporting, it may be that the automatic reporting switch is not turned on when integrating the SDK. Please set the auto_report to ture.

<span id="84c183e4"></span>
## Why is the sharing analysis data of Mini Program not reported normally?

The use of "sharing analysis" depends on the reporting of "on_share". Please confirm whether the Mini Program SDK is configured auto_report true during initialization. For details, please refer to the Mini Program SDK related documentation, for example: [Mini Program SDK Integration](https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_Integration).

<span id="0039aefe"></span>
## How is the data uploaded in the Mini Program without the Internet?

For Mini Program, our SDK does not actively monitor the network, open enable_storage parameters will save the event first, if the report is unsuccessful, there is a chance to supplement the report after the next SDK initialization.

Note: The storage in the Mini Program has a size limit, and the event will be thrown when the limit is exceeded.

(1) If this parameter is false, the data that causes the upload to fail will be lost regardless of the circumstances

(2) If this parameter is true, all events will be stored in the storage, and then reported. If the report is successful, the uploaded data will be deleted. If it is unsuccessful, it will always be stored in the storage. When the SDK re\-initializes the process, it will see if there is any in the storage, and if there is any, it will be reported.

Scenario example:

When the Mini Program is currently running, there is no network at this time, and then suddenly there is a network, then the follow\-up behavior is reported normally, and those that have existed in Storage before will not be transmitted now. The Mini Program must be re\-initialized before the step of going to the storage to see if there is any.

<span id="69ed3e07"></span>
## What platforms does Mini Program sdk support for full event tracking?

At present, the full event tracking event of Mini Program only supports WeChat Mini Program, and the component implementation methods of other Mini Programs are different and have not been adapted for the time being. For example, Alipay Mini Program does not support bav2b_click. If the page is a Component implementation, it supports bav2b_page. If the page is a Page implementation, it is not supported.

<span id="ed7a3b7b"></span>
## What are the triggers for on_share and on_addtofavorites in WeChat Mini Program? How can these methods be implemented?

on_share and on_addtofavorites are preset events of the Mini Program itself, which are triggered depending on whether the methods of the Mini Program itself are implemented. If the onShareAppMessage and onAddToFavorites methods were not implemented during the development of the Mini Program, they can be implemented by adding these methods to the page.

<span id="b5ae1763"></span>
# SDK Integration: Mini Games

<span id="caa62850"></span>
## Mini game start (app_launch) and close (app_terminate) events are not reported

Due to the limitations of the framework, the lifecycle of the mini\-game cannot be monitored when it is compiled by the framework. Therefore, the SDK cannot automatically collect and report startup and shutdown events, and the current SDK cannot avoid them.

We provide functions for manually reporting start\-up and shutdown events. If customers can monitor the framework life cycle by themselves (or the framework provides a life cycle monitoring method), they can report start\-up and shutdown events by self\-reporting

Manually call the shortcut:

Launch event: $$sdk.appLaunch ()

Exit event: $$sdk.appTerminate ()

<span id="5c189774"></span>
# SDK Integration: Flutter

<span id="5f5d649c"></span>
## When accessing the Flutter app SDK, access the iOS native SDK and reference pod'RangersAppLog ',' 6.xx.xx ', but an error appears when compiling and running, prompting "Use of undeclared identifier' BDAutoTrackServiceVendorCN '; did you mean' BDAutoTrackServiceVendorSG '?"

The overseas version cannot be initialized directly with RangersApplogFlutterPlugin .initRangersAppLog, it needs to be initialized in the native code and set as an overseas environment.

<span id="37c6ea4b"></span>
## When integrating the SDK in a Flutter project, event tracking real\-time verification is not possible, and the prompt message shows Android integration steps, but the project runs on iOS platform?

The Flutter project does not support verification using real\-time event tracking, but can integrate with Android or iOS platforms. It is recommended to choose Android or iOS platform for integration as needed and use DevTools for verification.

<span id="8ab9e4e8"></span>
## Does the Flutter SDK currently support multiple engines?


* If DataFinder uses multiple instances (instances of multiple applogs), it does not currently support multiple engines.

* If the DataFinder uses a single instance, it supports multiple engines.


<span id="6b0ca367"></span>
# SDK Integration: React Native

<span id="0efc52a5"></span>
## Using the React Native framework to integrate the SDK, the event reporting delay is high, what is the reason for the main thread card and how to deal with it?


* React Native framework to develop the Android SDK and iOS SDK, event reporting is asynchronous processing (RN side receives the event and sends it to the native side for processing; the native side handles the event, for example, stores db, and then reports in batches).

* All event tracking operations are performed in the background thread, including writing to the local database, without blocking the main thread. You don't need to manually optimize thread switching. Thread prioritization and asynchronous callbacks are handled internally in the SDK.

* You can perform log tracking before and after event reporting to assist in judging the reporting time.


<span id="f57ebc11"></span>
# SDK integration: server level

<span id="b977c7f3"></span>
## When using the Java SDK, I occasionally get a "Connection or outbound has closed" error, how to fix it?

It is recommended to upgrade the SDK to the latest version and set the keepalivetimeout parameter reasonably, such as keepalivetimeout to 10 seconds.

<span id="06e1765e"></span>
## When using the PHP SDK to report server level events, what scenarios will have their own device_id?

The PHP SDK does not automatically include device_id by default. If you need to bring device_id, you can refer to the following steps:


1. Call the setDeviceId method in the PHP SDK code to pass the deviceid value.

2. The AppEventCollector object is used when reporting data (WebEventCollector does not generate device_id), app_type type is APP device_id

3. Applog service supplements user information through IDM


<span id="f841b7a8"></span>
## Can the platform field value in the HTTP API be passed casually?

platform platform type, not required field, you can customize the value to upload;

However, random transmission may affect the analysis of the application profile function; the end point platform field value in the application profile is mp is Mini Program, web, wap is web, ios, android is mobile end; other data can only be viewed in all.

Recommendation: Try to assign values according to the correct platform type.

<span id="a0031b50"></span>
## How do I report mp_platform properties via HTTP API?

The specific instructions are as follows:

Field: mp_platform

Field values: 0, 1, 2

Type: string

Use: Use in custom in the header, as follows:

"header": {

"app_name": "android",

"device_model": "vivo X20A",

"client_ip": "223.91.16.13",

"custom": "{"is_vip":"2","mp_platform":"0"}"

},

<span id="8a1683c0"></span>
# SDK Integration: Business Dimension (item)

<span id="17052c9d"></span>
## How to access business dimension data?


1. You need to create the item first and configure the item properties in the item. The built\-in id attribute field will be written to the item_id field when it is reported to the database later.

2. After creating the item, you can access the item data according to the situation.

   * When accessing business dimension data, ak/sk is required. You need to contact BytePlus technical support staff to obtain ak/sk information, and then perform business dimension data access.

   * For business dimension data access operations in SaaS\-non\-cloud native scenarios.

   * For data access operations in SaaS\-cloud native and privatization scenarios, please refer to the corresponding HTTP API documentation: [6. Report business object properties](https://docs.byteplus.com/docs/DataFinder/HTTP_API#_6-%E4%B8%8A%E6%8A%A5%E4%B8%9A%E5%8A%A1%E5%AF%B9%E8%B1%A1%E5%B1%9E%E6%80%A7).

   * The SaaS\-cloud native environment also supports directly uploading business dimension data by uploading CSV files locally, see [Business Dimension (Item) Data Access (Local File Upload)](https://docs.byteplus.com/docs/DataFinder/Business_Dimension_Item_Data_Access_Local_File_Upload) for details.


See more best practices for item data access [Business Dimension (Item) Data Access and Usage Practices](https://docs.byteplus.com/docs/DataFinder/Business_Dimension_Item_Data_Access_and_Usage_Practices).

<span id="f4d15c50"></span>
# Sensitive Data & Privacy & Security & Authorization

<span id="1963e7a6"></span>
## National Secret SM2 configuration related


* National secret configuration requires both the mobile end and the back end to be configured, and the mobile end configuration national secret refers to the official website document;

   
   |SDK type |Does it support SM2? |SDK supports SM2 version (\> =) |Does it support SM4? |Does it support other encryption algorithms? |
   |---|---|---|---|---|
   |Android |support |6.15.4 |No |The default encryption algorithm is AES. |
   |Harmony |support |1.0.0 |No |The default encryption algorithm is AES. |
   |IOS |support |6.15.0 |No |The default encryption algorithm is AES. |
   |WEB/H5 |support |5.16 |No |without |
   |Mini Program |support |2.9.1 |No |without |
   

* State secret SM2 is a symmetric encryption algorithm, and configuration requires a private key and a public key. The customer needs to generate the private key by himself and then generate the corresponding public key according to the algorithm. The generation method can refer to the public forum documentation.

* Effective immediately after opening the national secret

* After opening the national secret, it is compatible with the old reported data, and does not affect the data reporting of the unopened national secret.


<span id="0599f146"></span>
## Is there an authorization to read phone state in the SDK? If so, what information about the device will be obtained after authorization?

Yes. After authorization, you will get the device's deviceId, sim card serial number, subscribeID and other relevant information. But iOS do not have permission to apply, and will not collect the SIM card serial number.

<span id="c3d1997d"></span>
## When integrating the Android SDK, what does the permission com.asus.msa. SupplementaryDID. ACCESS do, and can it be removed?

This permission is used by the Andorid SDK to obtain oaid, using scenarios: device registration and deep linking: cross\-app identification of devices. Note: OAID is an important device tracking information. If OAID is turned off, it will affect the attribution results of ad monitoring. Please consider carefully if you use the ad monitoring function. If the customer does not buy ads and needs to turn off oaid, you can follow the instructions in the documentation on the official website [8. Permissions Description](https://docs.byteplus.com/docs/DataFinder/Android_SDK_Integration_#_8-%E6%9D%83%E9%99%90%E8%AF%B4%E6%98%8E).

<span id="a71cc16e"></span>
## What is the oaid obtained by the Android SDK?

Background: Disable IMEI and MAC after Android 10.

The Mobile Security Alliance has launched a set of ad tracking identifiers for domestic mobile phone manufacturers, called OAID. OAID can be accessed across apps, but users can reset it at any time in the system settings. OAID has certain authority and can meet the usage scenarios of user behavior statistics.

<span id="9cc4eb4d"></span>
## Can I obtain the IDFA manually?

You can obtain the IDFA manually. Use the requestAuthorizationWithHandler method instead of calling the system's ATTrackingManager to get the IDFA. The specific code is as follows:

```Plain
#import <AppTrackingTransparency/AppTrackingTransparency.h>
#import <AdSupport/ASIdentifierManager.h>
```


Use the `(nullable NSString *) trackingIdentifier;`method to get the IDFA.

<span id="d8129c71"></span>
## After closing the IDFA tracking permission, cold start will crash when detecting event tracking in real time. What is the reason for the thread deadlock?

You can upgrade the SDK version to 6.17.0 and above to solve this problem.

<span id="91993f6d"></span>
## Can I get the decrypted did through the interface provided by the sdk?

No, what is obtained through the did interface exposed by the sdk is bd_did, bd_did is encrypted did. If you want to decrypt the bd_did, you can use the bddid robot internally to obtain it, and the decryption is not provided externally. bd_did is encrypted using group id + did via AES.

<span id="5df55faa"></span>
## Can the Finder identify falsified or altered reports?


1. The reporting interface has no authentication, and theoretically the data can be reported. It is not possible to identify whether the data is forged or tampered with from the server level.

   2, the Finder server level does not verify whether the device_id is issued by itself, and cannot identify forged data from the id side

   Clients are advised to take the following measures to prevent data tampering:

2. Do a good job of request encryption (not only relying on https encryption), preferably with its own additional encryption (preferably asymmetric encryption). Other measures require the customer to consider whether there is a better solution.

    &nbsp;


<span id="can-the-datafinder-sdk-collect-data-from-other-sdks"></span>
## Can the DataFinder SDK collect data from other SDKs?

No, the DataFinder SDK will only collect configured event and behavior data and will not hack into other SDKs.

<span id="_2-数据统计差异"></span>
# Event tracking verification & data reporting exception

<span id="fbcfc689"></span>
## How can I verify the accuracy of the reported data?


* Through a single user's [User Details](https://docs.byteplus.com/docs/DataFinder/User_Details), check whether the events and attributes in the reported behavior data are consistent with the design of event tracking;

* Compare statistical metrics such as active users and event triggers with business systems or other systems to see the analysis variance rate.


<span id="261d26e5"></span>
## When using the event tracking real\-time verification function, why do you not see the event and attribute data reported by the test normally on the page?

Check and ensure that the data reporting address is configured correctly. If the data reporting address is cancelled, the problem can be solved by re\-adding the data reporting address.

<span id="24e7ff6a"></span>
## When using real\-time event tracking verification, the reported data can be successfully viewed, but when the reported data is collected in the follow\-up, the data is not normally stored in the DataFinder, resulting in the inability to query the data?

The real\-time event tracking verification function uses the unified test appid for data reporting, which is mainly used to verify the correctness of event tracking such as whether there are missing fields and whether the data type is correct. When the actual data collection is reported, the data will be reported to the application and environment address you configured. At this time, if the data is not checked, you can further confirm whether the configuration results such as the data reporting address and application ID in the integrated SDK are correct.

<span id="8437dffa"></span>
## Which version of H5 real\-time event tracking verification is supported?

Web/JavaScript SDK supports real\-time event tracking verification from V5.1.2.

<span id="f50b8029"></span>
## The web side uses the event tracking verification function, and there is no response after scanning the code to open the webpage. What is the reason?

It is recommended to check the web SDK version first. The JS SDK version of the web integration needs to be 5.1.2 and above

<span id="b7c436dc"></span>
## When using the real\-time event tracking verification function to verify the mobile end event tracking, after scanning the QR code, sometimes it can be connected, and sometimes it reports an error?

First, confirm whether the phone you are using is iOS or Android. Then, check the settings app_name, scheme, proxy methods, sublibraries, etc. according to the details in the corresponding SDK integration documentation. If the problem persists, it is recommended that users check their network connection and device settings.

<span id="db846294"></span>
## When using the real\-time event tracking verification function to verify the web side, after configuring the web page URL information, the real\-time monitored page has not changed?

Check whether the url is correct and confirm whether it is a different testing environment for the same customer. Also, check if the wrong application is selected. If the problem persists, it may be due to the wrong use during page switching and needs to be retested.

<span id="d6706a91"></span>
## Why is the data displayed by real\-time event tracking detection in finder different from the data actually put into storage?

The data detected by real\-time event tracking is read and displayed in real time according to the reported data, and the displayed logic will not be exactly the same as the actual database; the actual database is accurate data.

Real\-time event tracking detection, what you see is used as a reference, which is a bit similar to the function of grabbing bags; the database will compensate for a lot of information, and the database shall prevail.

<span id="57fce77d"></span>
## After reporting the data, how long can I see the data in the system, such as events, event attributes, users, user attributes, etc.?

Whether using server level or client side sdk, upload user, user properties, events, event properties

(1) You can see the corresponding event and attribute data in the data management in about 10 minutes, because this piece of data is metadata.

(2) In about 15 minutes, you can see the uploaded user details in the user's careful inspection

(3) For user attributes and event attributes, the old attributes will directly display the uploaded attribute values, and the new attributes will be built first, but they will be built after the metadata falls into the library (that is, 10 minutes later). (When the new attribute is not built successfully, the uploaded new attribute value data will be lost). After the construction is completed, the new attribute values will fall into the library. The attribute values can be found in about 2 hours.

<span id="533c1e94"></span>
## The event attribute data was reported normally, but the user attribute data was not reported successfully. What is the reason?

You can refer to the following investigation steps to check the cause of positioning:


1. Enter the metadata \> user properties page to confirm whether the user properties to be reported are created correctly. Especially when using the userprofile api and go sdk to report user attributes, you must enter it before reporting user attributes normally.

2. Verify that the app ID and AppKey configured when reporting user properties are correct.

3. The first report of a new attribute may be discarded, and it is recommended to report a few more.

4. Check the reported data for error logs.


<span id="c90e2cd3"></span>
## The event tracking data was reported successfully, but it cannot be found on the metadata management page/analysis tool page?

You need to see if the setting has turned on the event tracking acceptance function. If it is turned on, the reported event tracking needs to be clicked on the metadata management page for acceptance, and it can only be queried and used after the acceptance is completed.

<span id="3acdfb66"></span>
## When adding an input event to the metadata management \> general events page, the creation fails?

You can check the metadata\-general event limit in the project settings and application settings to confirm whether the number of general events already in the current metadata exceeds the set limit.

<span id="a6a3f353"></span>
## Does the unaccepted event tracking limit affect event tracking? What will happen to the data if the set amount is exceeded?

The limit of the number of unaccepted event tracking is to avoid reporting too many useless events and attributes, and to avoid the situation that R & D and products are not aligned and are all dirty data. If the set amount is exceeded, the data will be discarded and will not be displayed in the system. At the same time, if the data is intercepted, it will enter the acceptance pending event, but it will not enter the dropped_event, because it is the expected interception event. If you want to make up data, you can only restore it from HDFS.

<span id="5231ead2"></span>
## Abnormal app_version data reported

Preset attribute app_version field, there is special processing logic in SaaS\-non\-cloud native and SaaS\-non\-cloud native overseas\-byteplus environment, must be x.x.x three\-segment format, otherwise it will be forcibly filtered into this format by applog, such as: 12.1 will be filtered as: 1.2.1

<span id="26969efe"></span>
## Report an abnormal application startup event: no application startup event when opening the app for the first time

When initialized not in the application, but in the activity, since the initialization is displayed after the activity, the event will not be started, and a third parameter needs to be added to the initialization init () method to the current Activity object.

<span id="7d48e92f"></span>
## Report a datetime type data exception


* Abnormal scenario: There is an event created by the main order submission event that needs to pass the datetime type. It seems to be passed in the interface, but this parameter is missing in the test from the volcano side.

* Solution: This issue may be due to a date format issue. If you don't need a timezone, just pass in the format yyy\-MM\-dd HH: mm: ss.


<span id="8eac809c"></span>
## Error when reporting user attributes using user profile api: user xxx not exist


* Error scenario: Error when reporting user attributes using the user profile api, the error code is: `{"code": 4000, "message": "user 20 ********** not exist.", "data": null}`

* Possible reasons: You may currently be using a SaaS\-non\-cloud native environment, and the user who currently reports user attributes has never reported any event\-related data before, that is, the user has never dropped into the DataFinder (the user does not have a unique identifier ssid in the DataFinder). In this scenario, if automatic registration is not enabled and user attributes are directly reported, an error will be reported because the user does not exist.

* Processing method:

   * Method 1: You can use the current user to report an event first. At this time, the user will generate a user ssid while reporting the event, drop the user into the DataFinder, and then report the user attribute data later, so that no errors will be reported.

   * Method 2: If you cannot report the event data first, you can also contact the BytePlus technical support staff to enable automatic registration (auto_create_ssid) for you. After opening, you can directly report the user attributes without warehousing.


<span id="9b58e349"></span>
## WeChat/Alipay Mini Program reported failure

(1) SaaS version

WeChat Mini Program: Add the data reporting address to the WeChat Mini Program's domain name whitelist.

Alipay Mini Program: You need to add the server address of the reported data to the whitelist of the Alipay Mini Program's domain name.

(2) The privatized version

WeChat Mini Program: You need to report the address of the private deployment to the whitelist of the WeChat Mini Program's domain name.

Alipay Mini Program: You need to report the data of the private deployment to the address and add it to the whitelist of the Alipay Mini Program's domain name.

<span id="34f552ed"></span>
## The device login data reported by Mini Program is abnormal, and it is found that 1 device ID logs in to a large number of user accounts every day.

You can check whether the device data on the Mini Program side uses bddid. The Mini Program side does not need to pay attention to bddid. It is recommended to use webid.

<span id="aad32456"></span>
## Mini Program from anonymous to real name, during the period did not quit Mini Program, but why there is an exit event (app_terminate event)?

The above phenomenon is in line with expectations, and the supplementary event is the processing logic of the Mini Program, which will report the app_terminate and app_launch events synchronously when reporting the user's real\-name information (that is, when reporting the user_unique_id).

<span id="d4f4e67d"></span>
## Why can't WeChat Mini Program SDK collect this collection/sharing event?

The mechanism of Mini Program is that the customer needs to implement the corresponding event handler function before triggering the relevant event report. See [onAddToFavorites](https://developers.weixin.qq.com/miniprogram/en/dev/reference/api/Page.html#onAddToFavorites-Object-object).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8e7096db24e44cfcbcffd521816c67fb~tplv-goo7wpa0wc-image.image) </span>

<span id="9290c694"></span>
## In the Mini Program preset sharing event, what is the reason why the title cannot be obtained when sharing after jumping to an external link?


1. Verify that the page has a title set at share time. If the title is empty or not set, the `title`in the preset properties will be empty.

2. Make sure the title is set correctly when the page loads. If the title is set dynamically, make sure to set the title before data reporting.

3. If the page is reported without a title set at load time, the `title`attribute may be empty.

4. Make sure to load the page and set the title before reporting the data.

5. Check whether the `onShareAppMessage`definition is returned asynchronously. If it is returned asynchronously, the SDK does not currently support obtaining the `title`attribute, because the `title`is defined by the business itself. If the value is `undefined`, the `title`field will be filtered out.


<span id="0dbeb19b"></span>
## The DAU in the Finder product does not match the self\-counted Mini Program data.


* Question


The DAU in the Finder product does not match the Mini Program data counted by itself. The customer has not reported the anonymous behavior to the Finder at present. How to ensure that the DAU statistics are the same while distinguishing the user status?

User status is divided into: visitor (no device id and uuid), registered (no uuid), certified (with uuid)


* Answer


It is recommended that customers report in a multi\-criteria manner, create visitor criteria, and maintain a set of anonymous user IDs by themselves.


1. Tourists: Report data to refer to XXX events, user_id = tourists, user_unique_id_type = tourists

2. Registration: Report data reference XXX event, user_id = visitor, anonymous_id = custom anonymous id, user_unique_id_type = XXX

3. Authentication: Report data reference XXX event, user_id = real name id, anonymous_id = custom anonymous id


<span id="2f6edca8"></span>
## The data reported regist_time server level is abnormal, which is inconsistent with the time reported by the actual customer. What is the reason?

Cause: If there is a time difference, confirm whether the value of the timezone field reported on the server level is 0;

Take the difference of 8 hours as an example, the solution: the timezone field of the server level is changed to 8.0

Attention: The timezone must be placed under the header.

<span id="eacda997"></span>
## How to check if there is a data difference between BytePlus Growth Analysis data and its own back\-end or third\-party platform?


* Statistical criteria: It is recommended that you compare BytePlus Growth Analysis with the statistical criteria of your own back\-end or third\-party platform data;

* Event tracking report timing/logic: It is recommended that you confirm whether BytePlus Growth Analysis is consistent with your own background or third\-party platform tracking event reporting timing and event tracking report logic;

* If you still have questions, please click the button in the lower right corner of the BytePlus Growth Analysis page and give us a detailed comparison description by submitting a work order.


<span id="d671f76e"></span>
## How is the ssid calculated on the web and PC, and why is it so much worse?

Ssid's computational logic can participate [User ID (uid, ssid, did)](https://docs.byteplus.com/docs/DataFinder/User_ID_uid_ssid_did). If your reported data is very poor and there are obviously abnormal data scenarios, you can check whether it is due to abnormal data generated by data crawlers. It is recommended that you filter crawler data during data query. DataFinder also supports crawler recognition function, you can set the crawler recognition rules to identify and filter crawler data.

<span id="156d1500"></span>
## Why doesn't the total conversion rate of the query results by channel add up?

After grouping, if a user meets multiple grouping conditions, one will be calculated separately in the relevant group, so that the sum of the groupings will be larger than the total value.

<span id="35eda97f"></span>
## A/B experiment shunt exception: Why can't A/B test traffic be allocated?

BytePlus Growth Analysis's A/B testing function has 100% traffic and does not support traffic reuse. Therefore, when the experimental traffic you open has reached the upper limit of 100%, when you start a new experiment, the traffic will not be distributed. You need to end some experiments and create them again, or contact customer service to upgrade and use the advanced product DataTester for A/B testing.
