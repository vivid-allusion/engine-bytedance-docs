---
title: "Preset User Properties/Preset Event Public Properties"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Preset_User_Properties_Preset_Event_Public_Properties"
---

<span id="88216db4"></span>
# Background information


* Environment description: The current DataFinder provides you with a variety of environments, and the list of preset events and preset properties supported by each environment varies slightly. You can view the preset events and preset property capabilities supported by the corresponding environment according to your current environment. If you are unsure which environment you are currently using, see [SaaS Cloud-Native & Privatized Environments](https://docs.byteplus.com/docs/DataFinder/SaaS_Cloud-Native_Privatized_Environments).

* Event/Attribute Type Description: Preset user properties and preset event public properties are currently introduced to you. In addition, the "preset events" and "preset event properties" supported by each end of DataFinder can view the preset events and property documents of each end. See the [Preset Property Summary Table](https://docs.byteplus.com/docs/DataFinder/Preset_Property_Summary_Table).

* Reporting mechanism: See details [Product logic: data reporting & caching strategy](https://docs.byteplus.com/docs/DataFinder/DataFinder_Data_Access_Overview#e98b6846).


<span id="ec9a1386"></span>
# SaaS\-cloud native

<span id="fca64860"></span>
## Preset event public properties

<span id="f6213c8d"></span>
### SDK acquisition: APP

<span id="965fae4c"></span>
#### Android, iOS, Harmony \- General Fields


|Preset event public property name |Attribute description |Attribute value type |Data source |Whether to collect automatically |Switch control |
|---|---|---|---|---|---|
|network_type |Network type, Mini Program side: Use the getNetworkType method provided by the platform to get the network type, the values are: wifi/2g/3g/4g/unknown (uncommon network type under Android)/none (no network) |string |System API |Yes |No |
|ab_version |AB test Experimental Version ID (VID). |list |System API |Yes |No |
|app_channel |Channel attribute, the reported result is the app_channel value manually set when integrating the SDK. |string |user incoming |Yes |No |
|language |system language |string |System API |Yes |No |
|os_name |Operating System |string |fixed value |Yes |No |
|os_version |System version |string |System API |Yes |No |
|package |install package name |string | |Yes |No |
|platform |Platform attributes for data reporting. |string |fixed value |Yes |No |
|region |System country/system region |string |System API |Yes |No |
|resolution |resolution |string |System API |Yes |No |
|sdk_lib |SDK version<br><br>Web: js, Android: android, ios: ios, Mini Program: mp_common, Harmony: openHarmony |string |fixed value |Yes |No |
|sdk_version |SDK version |string |fixed value |Yes |No |
|$user_unique_id_type |user ID type |string |user incoming |See if the customer sets it up. |No |


<span id="f64c6250"></span>
#### Android specific


|Preset event public property name |Attribute description |Attribute value type |Data source |Whether to collect automatically |Switch control |
|---|---|---|---|---|---|
|app_region |Software region/software country<br><br>Android：<br><br>Priority is given to the value in config.setRegion. If the current region of the system is not covered,<br><br>iOS<br><br>Get the value in track.setAppRegion first, if you don't go to the bottom of the current region of the system<br><br>It cannot be enumerated one by one. In China, it is cn. |String |user incoming |Yes |No |
|app_version_minor |The build number of the APP version iOS get the build number from the system API, and the Android side needs to be manually set when integrating the SDK. |String |user incoming |Yes |No |
|network_carrier |Operator information, DataFinder will have cleaning logic to the device library for mapping when the data is built. If it cannot be mapped, the reported value will be used.<br><br>iOS does not support the collection of operator\-related attribute data. |String |System API |Yes |Yes, the Android side controls whether to collect operator information through the "setOperatorInfoEnabled" switch |
|cpu_abi |abi corresponding to cpu architecture |String |System API |Yes |No |
|device_brand |Mobile phone brand |String |System API |Yes |No |


<span id="eafc58fd"></span>
#### iOS unique


|Preset event public property name |Attribute description |Attribute value type |Data source |Whether to collect automatically |Switch control |
|---|---|---|---|---|---|
|app_region |Software countries/regions.<br><br>Android：<br><br>Priority is given to the value in config.setRegion. If the current region of the system is not covered,<br><br>iOS<br><br>Get the value in track.setAppRegion first, if you don't go to the bottom of the current region of the system |String |User Incoming, System API |Yes |No |
|app_version_minor |The build number of the APP version iOS get the build number from the system API, and the Android side needs to be manually set when integrating the SDK. Harmony does not support it for the time being. |String |System API |Yes |No |


<span id="659b13c7"></span>
#### Harmony unique


|Preset event public property name |Attribute description |Attribute value type |Data source |Whether to collect automatically |Switch control |
|---|---|---|---|---|---|
|network_carrier |Operator information, DataFinder will have cleaning logic to the device library for mapping when the data is built. If it cannot be mapped, the reported value will be used.<br><br>iOS does not support the collection of operator\-related attribute data. |String |System API |Yes |Yes, Harmony terminal controls whether to collect operator information through the "setOperatorInfoEnabled" switch. |
|cpu_abi |abi corresponding to cpu architecture |String |System API |Yes |No |
|device_brand |Mobile phone brand |String |System API |Yes |No |


<span id="f188907f"></span>
### SDK acquisition: Web


|Preset event public property name |Attribute description |Attribute value type |Data source |Whether to collect automatically |Switch control |
|---|---|---|---|---|---|
|ab_version |AB test Experimental Version ID (VID). |list |application information |No |No |
|browser |Browser.<br><br>Web: Gained from the browser's userAgent.<br><br>Enumeration values are: Chrome, Safari, FireFox, Microsoft Edge, Microsoft Internet Explorer, sougoubrowser, qqbrowser, weixin, 360browser, baidubrowser, xiaomi, Opera |string |Device information |Yes |No |
|browser_version |Browser version.<br><br>Web: Collected from the browser's userAgent, first identify the corresponding browser model, and then parse the version number from a specific location, without enumeration values. Such as:<br><br>Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/ [134.0.0.0 ](http://134.0.0.0/)Safari/537.36 Browser Yes Chrome, version number is [134.0.0.0](http://134.0.0.0/) |string |Device information |Yes |No |
|device_brand |Mobile phone brand |string |Device information |Yes |No |
|language |system language |string |Device information |Yes |No |
|os_name |Operating System |string |Device information |Yes |No |
|os_version |System version |string |Device information |Yes |No |
|platform |Platform attributes for data reporting. |string |fixed value |Yes |No |
|resolution |resolution |string |Device information |Yes |No |
|screen_height/height |The height of the current screen, in px |int |Device information |Yes |No |
|screen_width/width |The width of the current screen, in px |int |Device information |Yes |No |
|web_id |Generated device web_id, see the Help documentation: [https://www.volcengine.com/docs/84129/1261513 ](https://www.volcengine.com/docs/84129/1261513). |string |Server level generation |Yes |No |
|$latest_traffic_source_type |Take the initiative to report after business setting traffic_type |string |System API |Yes |No |


<span id="5761fdca"></span>
### SDK acquisition: Mini Program


|Preset event public property name |Attribute description |Attribute value type |Data source |Whether to collect automatically |Switch control |
|---|---|---|---|---|---|
|device_brand |Mobile phone brand |string |System API |Yes |No |
|device_model |Mobile phone model |string |System API |Yes |No |
|language |system language |string |System API |Yes |No |
|os_name |Operating System |string |System API |Yes |No |
|os_version |System version |string |System API |Yes |No |
|platform |platform |string |fixed value |Yes |No |
|resolution |screen definition |string |System API |Yes |No |
|sdk_lib |SDK type |string |fixed value |Yes |No |
|sdk_version |SDK version number |string |fixed value |Yes |No |
|user_id |user's incoming login status |string |user incoming |customer initiative |No |
|$user_unique_id_type |The type of login status passed in by the user |string |user incoming |customer initiative |No |
|network_type |Network type, such as "wifi" |String |System API |Yes |No |
|device_brand |Mobile phone brands, for example, "iPhone" |String |System API |Yes |No |
|mp_platform_app_version |WeChat version number |String |System API |Yes |No |
|mp_platform_basic_version |Client side base library version, such as "1.1.0" |String |System API |Yes |No |
|mp_platform |Mini Program Platform |String |DataFinder server level generation |Yes |No |
|rangers_mp_from_uid |The source identifier used to record a Mini Program share, usually the `ssid`of the sharer. With this property, you can track which sharing link the user entered the Mini Program through, and then analyze the sharing behavior and effect |String |DataFinder server level generation |Yes |No |


<span id="0c65fe7b"></span>
### DataFinder server level generation


|Preset event public property name |Attribute description |Attribute value type |Data source |Whether to collect automatically |Switch control |
|---|---|---|---|---|---|
|$anonymous_id |The anonymous ID randomly generated by the SDK supports custom rewriting. The client side will report the unique device identifier generated by the client side as anonymous_id while reporting the device_id and web_id. |string |DataFinder server level generation |Yes |No |
|$app_id |The AppID value that uniquely identifies the app. The value is passed in for the customer. |int ||Yes |No |
|$event_name |event name |string ||Yes |No |
|$event_time |Event occurrence time, the client side SDK only has crash events, which is the crash occurrence time<br><br><br>* Crashes are currently only reported by the App<br><br>* Record the time of the crash, but report it the next time you enter the app<br><br>* The format is all timestamp, recorded in local_time_ms field |datetime ||Yes |No |
|$is_first_day |Whether to visit on the first day.<br><br>When the APP side reports the event, based on whether the indicator event activation time (first_event_time) and the event (event_time) of the indicator event occur on the same day, it can be used to identify whether the user is a new user.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">DataFinder also provides you with user_is_new properties that can be used to determine whether a user is a new user during an analysis cycle. The main differences from $is_first_day are:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">$is_first_day is to determine whether the activation time (first_event_time) of the indicator event and the event (event_time) of the indicator event occur on the same day;</div><br><br><br>* <div data-tips="true" data-tips-type="tip">user_is_new calculation result is the same as the time granularity of data analytics, which is whether the activation time (first_event_time) of the indicator event and the event (event_time) of the indicator event are the same time period, so the time period of the analysis is different user_is_new the calculation result is different.</div><br><br><br><br><div data-tips="true" data-tips-type="tip">See more about the comparison of the two properties <a href="https://docs.byteplus.com/docs/DataFinder/Statistical_Criteria_Value_Logic#3dac52c5">New and old users/whether it is relevant on the first day</a>.</div><br> |int ||Yes |No |
|$is_login |Whether to log in, user_unique_id not empty Assignment 1 otherwise 0 |int ||Yes |No |
|$latest_referrer |When a user visits the target page, they also report the address of the last page before visiting the current page. |string ||Yes |No |
|$latest_referrer_host |When a user visits the target page, they also report the domain name of the last page they were on before visiting the current page. |string ||Yes |No |
|device_id |Device ID |string ||Yes |No |
|loc_city_id |City information, the DataFinder generates values for this property based on client_ip when the data is constructed. |string ||Yes |No |
|loc_country_id |Country information, the DataFinder generates values for this attribute based on client_ip when the data is constructed. |string ||Yes |No |
|loc_province_id |Province information, the DataFinder generates values for this property based on client_ip at data build time. |string ||Yes |No |
|origin_ab_version |Wide aperture AB test VID, associated A/B test ablog table for screening. Users are always counted in the current group after they join the group for the first time, that is, they will still be counted in the first group after subsequent user group changes. Experimental statistics use this caliber. |int ||Yes |No |
|referrer |When reporting a page access (Page_view) event, the address information of the reported page referrer is mainly composed of three parts: protocol://host [: port]/path. The host is generated by parsing the string into a [java.net ](http://java.net/). URL object and calling the getHost () method. |string ||Yes |No |
|referrer_host |When reporting a page visit (Page_view) event, the domain name information of the reported page referrer, the generation logic and enumeration values are detailed in the official website help document https://www.volcengine.com/docs/84129/1270815. |string ||Yes |No |
|user_id |user ID |string ||Yes |No |
|client_ip |Internet Protocol Address |string ||Yes | |


<span id="a9937f71"></span>
## preset user properties


|User property name |Attribute description |Attribute value type |Data source |Whether to collect automatically |Switch control |
|---|---|---|---|---|---|
|first_event_time |activation time |Datetime |Server level generation |Yes |No |
|last_active_date |Last active date |Datetime |Server level generation |Yes |No |
|user_is_new |Whether the user is a new user during the time period of data query analysis.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">DataFinder also provides you with a $is_first_day attribute that can be used to determine whether a user is a new user on a given day. The main differences from user_is_new are:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">$is_first_day is to determine whether the activation time (first_event_time) of the indicator event and the event (event_time) of the indicator event occur on the same day;</div><br><br><br>* <div data-tips="true" data-tips-type="tip">user_is_new calculation results are related to the time granularity of data analytics, whether the activation time (first_event_time) of the indicator event and the event (event_time) of the indicator event are the same time period, so the time period of the analysis is different user_is_new the calculation results are different.</div><br><br><br><br><div data-tips="true" data-tips-type="tip">See more about the comparison of the two properties <a href="https://docs.byteplus.com/docs/DataFinder/Statistical_Criteria_Value_Logic#3dac52c5">New and old users/whether it is relevant on the first day</a>.</div><br> |Number |Server level generation |Yes |No |


&nbsp;

<span id="31d540dd"></span>
# Privatization

<span id="8fd784d9"></span>
### SDK acquisition: APP

<span id="ab8d4f32"></span>
#### Android, iOS, Harmony \- General Fields


|Preset event public property name |Attribute description |Attribute value type |Data source |Whether to collect automatically |Switch control |
|---|---|---|---|---|---|
|network_type |Network type, Mini Program side: Use the getNetworkType method provided by the platform to get the network type, the values are: wifi/2g/3g/4g/unknown (uncommon network type under Android)/none (no network) |string |System API |Yes |No |
|ab_version |AB test Experimental Version ID (VID). |list |System API |Yes |No |
|app_channel |Channel attribute, the reported result is the app_channel value manually set when integrating the SDK. |string |user incoming |Yes |No |
|language |system language |string |System API |Yes |No |
|os_name |Operating System |string |fixed value |Yes |No |
|os_version |System version |string |System API |Yes |No |
|platform |Platform attributes for data reporting. |string |fixed value |Yes |No |
|region |System country/system region |string |System API |Yes |No |
|resolution |resolution |string |System API |Yes |No |
|sdk_lib |SDK version<br><br>Web: js, Android: android, ios: ios, Mini Program: mp_common, Harmony: openHarmony |string |fixed value |Yes |No |
|sdk_version |SDK version |string |fixed value |Yes |No |
|$user_unique_id_type |user ID type |string |user incoming |See if the customer sets it up. |No |


<span id="d04f8b94"></span>
#### Android specific


|Preset event public property name |Attribute description |Attribute value type |Data source |Whether to collect automatically |Switch control |
|---|---|---|---|---|---|
|app_version_minor |The build number of the APP version iOS get the build number from the system API, and the Android side needs to be manually set when integrating the SDK. |String |user incoming |Yes |No |
|app_region |Software region/software country<br><br>Android：<br><br>Priority is given to the value in config.setRegion. If the current region of the system is not covered,<br><br>iOS<br><br>Get the value in track.setAppRegion first, if you don't go to the bottom of the current region of the system<br><br>It cannot be enumerated one by one. In China, it is cn. |String |user incoming |Yes |No |
|device_brand |Mobile phone brand |String |System API |Yes |No |
|network_carrier |Operator information, DataFinder will have cleaning logic to the device library for mapping when the data is built. If it cannot be mapped, the reported value will be used.<br><br>iOS does not support the collection of operator\-related attribute data. |String |System API |Yes |Yes, the Android side controls whether to collect operator information through the "setOperatorInfoEnabled" switch |
|cpu_abi |abi corresponding to cpu architecture |String |System API |Yes |No |


<span id="6c13c2b9"></span>
#### iOS unique


|Preset event public property name |Attribute description |Attribute value type |Data source |Whether to collect automatically |Switch control |
|---|---|---|---|---|---|
|app_region |Software countries/regions.<br><br>Android：<br><br>Priority is given to the value in config.setRegion. If the current region of the system is not covered,<br><br>iOS<br><br>Get the value in track.setAppRegion first, if you don't go to the bottom of the current region of the system |String |User Incoming, System API |Yes |No |
|app_version_minor |The build number of the APP version iOS get the build number from the system API, and the Android side needs to be manually set when integrating the SDK. Harmony does not support it for the time being. |String |System API |Yes |No |


<span id="715e77c0"></span>
#### Harmony unique


|Preset event public property name |Attribute description |Attribute value type |Data source |Whether to collect automatically |Switch control |
|---|---|---|---|---|---|
|network_carrier |Operator information, DataFinder will have cleaning logic to the device library for mapping when the data is built. If it cannot be mapped, the reported value will be used.<br><br>iOS does not support the collection of operator\-related attribute data. |String |System API |Yes |Yes, Harmony terminal controls whether to collect operator information through the "setOperatorInfoEnabled" switch. |
|cpu_abi |abi corresponding to cpu architecture |String |System API |Yes |No |
|device_brand |Mobile phone brand |String |System API |Yes |No |


<span id="eb788c42"></span>
### SDK acquisition: Web


|Preset event public property name |Attribute description |Attribute value type |Data source |Whether to collect automatically |Switch control |
|---|---|---|---|---|---|
|ab_version |AB test Experimental Version ID (VID). |list |application information |No |No |
|anonymous_id |user anonymous ID |string |user incoming |Yes |No |
|browser |Browser.<br><br>Web: Gained from the browser's userAgent.<br><br>Enumeration values are: Chrome, Safari, FireFox, Microsoft Edge, Microsoft Internet Explorer, sougoubrowser, qqbrowser, weixin, 360browser, baidubrowser, xiaomi, Opera |string |Device information |Yes |No |
|browser_version |Browser version.<br><br>Web: Collected from the browser's userAgent, first identify the corresponding browser model, and then parse the version number from a specific location, without enumeration values. Such as:<br><br>Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/ [134.0.0.0 ](http://134.0.0.0/)Safari/537.36 Browser Yes Chrome, version number is [134.0.0.0](http://134.0.0.0/) |string |Device information |Yes |No |
|device_brand |Mobile phone brand |string |Device information |Yes |No |
|language |system language |string |Device information |Yes |No |
|os_name |Operating System |string |Device information |Yes |No |
|os_version |System version |string |Device information |Yes |No |
|platform |Platform attributes for data reporting. |string |fixed value |Yes |No |
|resolution |resolution |string |Device information |Yes |No |
|web_id |Generated device web_id, see the Help documentation: [https://www.volcengine.com/docs/84129/1261513 ](https://www.volcengine.com/docs/84129/1261513). |string |Server level generation |Yes |No |
|$latest_traffic_source_type |Take the initiative to report after business setting traffic_type |string |System API |Yes |No |


<span id="6fb4404b"></span>
### SDK acquisition: Mini Program


|Preset event public property name |Attribute description |Attribute value type |Data source |Whether to collect automatically |Switch control |
|---|---|---|---|---|---|
|user_id |user's incoming login status |string |user incoming |Yes |No |
|$user_unique_id_type |The type of login status passed in by the user |string |user incoming |Yes |No |
|sdk_lib |SDK type |string |fixed value |Yes |No |
|sdk_version |SDK version number |string |fixed value |Yes |No |
|device_brand |Mobile phone brand |string |System API |Yes |No |
|platform |platform |string |fixed value |Yes |No |
|device_model |Mobile phone model |string |System API |Yes |No |
|language |system language |string |System API |Yes |No |
|os_name |Operating System |string |System API |Yes |No |
|os_version |System version |string |System API |Yes |No |
|resolution |screen definition |string |System API |Yes |No |
|network_type |Network type, such as "wifi" |String |System API |Yes |No |


<span id="1f0cf89f"></span>
### DataFinder server level generation


|Preset event public property name |Attribute description |Attribute value type |Data source |Whether to collect automatically |Switch control |
|---|---|---|---|---|---|
|$anonymous_id |The anonymous ID randomly generated by the SDK supports custom rewriting. The client side will report the unique device identifier generated by the client side as anonymous_id while reporting the device_id and web_id. |string |DataFinder server level generation |Yes |No |
|$app_id |The AppID value that uniquely identifies the app. The value is passed in for the customer. |int ||Yes |No |
|$event_name |event name |string ||Yes |No |
|$event_time |Event occurrence time, the client side SDK only has crash events, which is the crash occurrence time<br><br><br>* Crashes are currently only reported by the App<br><br>* Record the time of the crash, but report it the next time you enter the app<br><br>* The format is all timestamp, recorded in local_time_ms field |datetime ||Yes |No |
|$is_first_day |Whether to visit on the first day.<br><br>When the APP side reports the event, based on whether the indicator event activation time (first_event_time) and the event (event_time) of the indicator event occur on the same day, it can be used to identify whether the user is a new user.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">DataFinder also provides you with user_is_new properties that can be used to determine whether a user is a new user during an analysis cycle. The main differences from $is_first_day are:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">$is_first_day is to determine whether the activation time (first_event_time) of the indicator event and the event (event_time) of the indicator event occur on the same day;</div><br><br><br>* <div data-tips="true" data-tips-type="tip">user_is_new calculation results are related to the time granularity of data analytics, whether the activation time (first_event_time) of the indicator event and the event (event_time) of the indicator event are the same time period, so the time period of the analysis is different user_is_new the calculation results are different.</div><br><br><br><br><div data-tips="true" data-tips-type="tip">See more about the comparison of the two properties <a href="https://docs.byteplus.com/docs/DataFinder/Statistical_Criteria_Value_Logic#3dac52c5">New and old users/whether it is relevant on the first day</a>.</div><br> |int ||Yes |No |
|$is_login |Whether to log in, user_unique_id not empty Assignment 1 otherwise 0 |int ||Yes |No |
|device_id |Device ID |string ||Yes |No |
|loc_city_id |City information, the DataFinder generates values for this property based on client_ip when the data is constructed. |string ||Yes |No |
|loc_country_id |Country information, the DataFinder generates values for this attribute based on client_ip when the data is constructed. |string ||Yes |No |
|loc_province_id |Province information, the DataFinder generates values for this property based on client_ip at data build time. |string ||Yes |No |
|origin_ab_version |Wide aperture AB test VID, associated A/B test ablog table for screening. Users are always counted in the current group after they join the group for the first time, that is, they will still be counted in the first group after subsequent user group changes. Experimental statistics use this caliber. |int ||Yes |No |


<span id="7587d7eb"></span>
## Preset user properties


|user property name |Attribute description |Attribute value type |Data source |Whether to collect automatically |Switch control |
|---|---|---|---|---|---|
|first_event_time |activation time |Datetime |Server level generation |Yes |No |
|last_active_date |Last active date |Datetime |Server level generation |Yes |No |
|user_is_new |Whether the user is a new user during the time period of data query analysis.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">DataFinder also provides you with a $is_first_day attribute that can be used to determine whether a user is a new user on a given day. The main differences from user_is_new are:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">$is_first_day is to determine whether the activation time (first_event_time) of the indicator event and the event (event_time) of the indicator event occur on the same day;</div><br><br><br>* <div data-tips="true" data-tips-type="tip">user_is_new calculation results are related to the time granularity of data analytics, whether the activation time (first_event_time) of the indicator event and the event (event_time) of the indicator event are the same time period, so the time period of the analysis is different user_is_new the calculation results are different.</div><br><br><br><br><div data-tips="true" data-tips-type="tip">See more about the comparison of the two properties <a href="https://docs.byteplus.com/docs/DataFinder/Statistical_Criteria_Value_Logic#3dac52c5">New and old users/whether it is relevant on the first day</a>.</div><br> |Number |Server level generation |Yes |No |
|gender |Gender |String |Server level generation |Yes |No |


<span id="825099d0"></span>
# BytePlus

<span id="fb79e7cd"></span>
## Preset event public properties

<span id="5dc51cb2"></span>
### SDK acquisition: APP

<span id="091a1bc5"></span>
#### Android, iOS, Harmony \- General Fields


|Preset event public property name |Attribute description |Attribute value type |Data source |Whether to collect automatically |Switch control |
|---|---|---|---|---|---|
|bddid |Device ID, the did will be requested before the request. If there is no did, the data will not be reported. It will not be reported until the did request comes back. |String |Server level generation |Yes |No |


<span id="484f57d5"></span>
#### Android specific


|Preset event public property name |Attribute description |Attribute value type |Data source |Whether to collect automatically |Switch control |
|---|---|---|---|---|---|
|cpu_abi |abi corresponding to cpu architecture |String |System API |Yes |No |


<span id="ec1fc336"></span>
#### iOS unique

without

<span id="a25a5eae"></span>
#### Harmony unique


|Preset event public property name |Attribute description |Attribute value type |Data source |Whether to collect automatically |Switch control |
|---|---|---|---|---|---|
|cpu_abi |abi corresponding to cpu architecture |String |System API |Yes |No |


<span id="1742f947"></span>
### SDK acquisition: Web


|Preset event public property name |Attribute description |Attribute value type |Data source |Whether to collect automatically |Switch control |
|---|---|---|---|---|---|
|screen_height/height |The height of the current screen, in px |int |Device information |Yes |No |
|screen_width/width |The width of the current screen, in px |int |Device information |Yes |No |
|web_id |Generated device web_id, see the Help documentation: [https://www.volcengine.com/docs/84129/1261513 ](https://www.volcengine.com/docs/84129/1261513). |string |Server level generation |Yes |No |
|$latest_traffic_source_type |Take the initiative to report after business setting traffic_type |string |System API |Yes |No |


<span id="04541c96"></span>
### SDK acquisition: Mini Program

without

<span id="ccab6cfd"></span>
### DataFinder server level generation

without

<span id="46a38251"></span>
## Preset user properties


|User property name |Attribute description |Attribute value type |Data source |Whether to collect automatically |Switch control |
|---|---|---|---|---|---|
|ab_version |AB test VID |Number | |Yes |No |
|age |age |String | |Yes |No |
|app_channel |Channel attribute, the reported result is the app_channel value manually set when integrating the SDK. |String | |Yes |No |
|app_language |software language |String |user incoming |Yes |No |
|app_version |software version |String |System API |Yes |No |
|brand |Mobile phone brand |String |System API |Yes |No |
|browser |Browser, web side, collected from the browser's userAgent.<br><br>Enumeration values are: Chrome, Safari, FireFox, Microsoft Edge, Microsoft Internet Explorer, sougoubrowser, qqbrowser, weixin, 360browser, baidubrowser, xiaomi, Opera |String |System API |Yes |No |
|browser_version |Browser version, the Web side is collected from the browser's userAgent, first identifies the corresponding browser model, and then parses the version number from a specific location. Such as:<br><br>Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/ [134.0.0.0 ](http://134.0.0.0/)Safari/537.36 Browser Yes Chrome, version number is [134.0.0.0](http://134.0.0.0/) |String |System API |Yes |No |
|client_ip |Internet Protocol Address (final) |String | |Yes |No |
|continent |Country by continent (data is constructed based on client_ip) |String |Server level generation |Yes |No |
|custom_mp_platform |Mini Program Platform |String | |Yes |No |
|custom_mp_platform_app_version |Platform version number |String | |Yes |No |
|custom_mp_platform_basic_version |Mini Program base library version number |String | |Yes |No |
|custom_rangers_mp_from_uid |Current request ssid (data stream maintenance) |String |Server level generation |Yes |No |
|device_model |Device model, web: collect and report after parsing according to browser UA<br><br>Mini Program: Get it using the platform's getSystemInfo method<br><br>Android: Using the system API: Build. MODEL<br><br>iOS：systemInfo.machine<br><br>Harmony: deviceInfo.productModel |String |System API |Yes |No |
|gender |Gender |String | |Yes |No |
|language |system language |String |System API |Yes |No |
|loc_city_id |City information, the DataFinder generates values for this property based on client_ip when the data is constructed. |String |Server level generation |Yes |No |
|loc_country_id |Country information, the DataFinder generates values for this attribute based on client_ip when the data is constructed. |String |Server level generation |Yes |No |
|loc_province_id |Province information, the DataFinder generates values for this property based on client_ip at data build time. |String |Server level generation |Yes |No |
|network_carrier |Operator information, DataFinder will have cleaning logic to the device library for mapping when the data is built. If it cannot be mapped, the reported value will be used.<br><br>iOS does not support the collection of operator\-related attribute data. |String |System API |Yes |No |
|network_type |Network type, Mini Program side: Use the getNetworkType method provided by the platform to get the network type, the values are: wifi/2g/3g/4g/unknown (uncommon network type under Android)/none (no network) |String |System API |Yes |No |
|os_name |Operating System |String |System API |Yes |No |
|os_version |System version |String |System API |Yes |No |
|platform |platform type |String |fixed value |Yes |No |
|region |System area |String |System API |Yes |No |
|resolution |resolution |String |System API |Yes |No |
|sdk_lib |SDK type, value:<br><br>Web side: js; Android side: android; ios side: ios; Mini Program side: mp_common; Harmony side: openHarmony |String |fixed value |Yes |No |
|sdk_version |SDK version |String |fixed value |Yes |No |
|user_id |user ID |String | |Yes |No |
|user_is_new |Whether the user is a new user during the time period of data query analysis.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">DataFinder also provides you with a $is_first_day attribute that can be used to determine whether a user is a new user on a given day. The main differences from user_is_new are:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">$is_first_day is to determine whether the activation time (first_event_time) of the indicator event and the event (event_time) of the indicator event occur on the same day;</div><br><br><br>* <div data-tips="true" data-tips-type="tip">user_is_new calculation results are related to the time granularity of data analytics, whether the activation time (first_event_time) of the indicator event and the event (event_time) of the indicator event are the same time period, so the time period of the analysis is different user_is_new the calculation results are different.</div><br><br><br><br><div data-tips="true" data-tips-type="tip">See more about the comparison of the two properties <a href="https://docs.byteplus.com/docs/DataFinder/Statistical_Criteria_Value_Logic#3dac52c5">New and old users/whether it is relevant on the first day</a>.</div><br> |Number |Server level generation |Yes |No |
|utm_campaign |Property is the name of the campaign created in the ad monitor. The reporting time is mobile app: report when activation occurs; web: click tracking link to jump to the landing page and report with the event; Mini Program: open the landing page monitored by Mini Program and report with the event. |String |Server level generation |Yes |No |
|utm_content |Attributes are the ad content that was filled in during the creation of web and Mini Program promotions on the ad monitoring page. The reporting opportunity is web: click the tracking link to jump to the landing page and report with the event; Mini Program: open the landing page monitored by the Mini Program and report with the event. |String |Server level generation |Yes |No |
|utm_medium |Property is the ad media value that was entered in the ad monitoring page to create web and Mini Program promotions. The reporting time is web: click the tracking link to jump to the landing page and report with the event; Mini Program: open the landing page monitored by the Mini Program and report with the event. |String |Server level generation |Yes |No |
|utm_source |The attribute is the promotion channel created in the advertising monitoring, which can be a cooperative channel or a custom channel created by yourself. The reporting time is mobile app: report when activation occurs; web: click tracking link to jump to the landing page and report with the event; Mini Program: open the landing page monitored by Mini Program and report with the event. |String |Server level generation |Yes |No |
|utm_term |Attributes are the advertising keywords that were filled in to create web and Mini Program promotions on the ad monitoring page. The reporting time is web: click the tracking link to jump to the landing page and report with the event; Mini Program: open the landing page monitored by the Mini Program and report with the event. |String |Server level generation |Yes |No |
