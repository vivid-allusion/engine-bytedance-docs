---
title: "Preset Property Summary"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Preset-Property-Summary"
---


| |Property name |Property display name |Property value type |Property example |Specific explanation |
|---|---|---|---|---|---|
|User properties |user_is_new |Is it a new user? |int |New users/old users |The main difference between new and old users (user_is_new) and whether the first day of access ($is_first_day) is that the former is affected by the selected time period, while the latter is not affected, so the latter has better consistency in the calculation results obtained in different chart types. It is recommended to use No first day of access ($is_first_day) to judge new and old users.<br><br>Whether the first day of visit ($is_first_day): the target event and the first event occurred on the same day;<br><br>user_is_new: The target event and the first event occur in the same cycle. For example, in a bar chart, the period is the time frame selected by the user. |
|Event properties |$source_platform |$source_platform |string |Example: web |Record the end type of event reporting (this property is not reported by the SDK, filled by data flow inference, and is only used by the system background. If you need to distinguish the end type of reporting, please use the platform field) |
||$is_first_time |Whether to visit for the first time |string |First time/non\-first time |Indicates that this event is the first to occur<br><br>When the preset logic on each end is set to true for the first time, and the subsequent ones are set to false, the prefabricated event app_launch/predefine_pageview has been processed, and the custom event needs to be handled by itself. |
||$url_query |$url_query |string |Example: query_1 = xxx & query_2 = yyy |Mini Program URL Query Parameters |
|Event public property |$is_login |Whether to log in |string |Logged in/not logged in |Indicates whether to log in |
||is_login |Whether to log in |int |Logged in/not logged in |Indicates whether to log in |
||$is_first_day |Whether to visit on the first day |int |Yes/No |The main difference between new and old users (user_is_new) and whether the first day of access ($is_first_day) is that the former is affected by the selected time period, while the latter is not affected, so the latter has better consistency in the calculation results obtained in different chart types. It is recommended to use No first day of access ($is_first_day) to judge new and old users.<br><br>Whether the first day of visit ($is_first_day): the target event and the first event occurred on the same day;<br><br>user_is_new: The target event and the first event occur in the same cycle. For example, in a bar chart, the period is the time frame selected by the user. |
||$event_name |event name |string |*  |The name of the event |
||$event_time |Event time |datetime |*  |Event triggered client side time |
||$user_register_time (privatization called first_event_time) |Registration time |datetime |*  |The time of the user's first event |
||bd_did |bd_did |string |Example: 4H66KFOXKF2FBO4KN2WVCY4GMQKCLDUCADOVMHUU76HA6L3U4PGA01 |Confused device_id |
||web_id |Web ID |string |Example: 7035549511104382505 |Default generated id, obtained from the dataflow interface |
||$latest_referrer |Last out\-of\-app address |string | | |
||$latest_referrer_host |Last out\-of\-app domain name |string | | |
||$latest_search_keyword |Search engine keywords |string | | |
||$latest_traffic_source_type |Last traffic source type |string | | |
||$user_unique_id_type | |string | | |
||app_channel |channel |string |Example: app store |User manual setting |
||app_region |Software region |string |Example: HK |User manual setting |
||region |System area |string |Example: AO |System API acquisition |
||app_version |software version |string |Example: 4.0.41 |System API acquisition |
||app_version_minor |Four\-digit version number |string |Example: 4 |iOS get the build number from the system API, Android needs to set it manually |
||device_model |Equipment model |string |Example: huawei meta 30 5g |The APP side is obtained from the system API, the Web side is parsed from ua, and the Mini Program side is obtained from getSystemInfo. |
||os_name |Operating System |string |Example: andriod |The web side is parsed from ua, and the Mini Program side is obtained from getSystemInfo. |
||os_version |System version |string |Example: 15.2.1 |The APP side is obtained from the system API, the Web side is parsed from ua, and the Mini Program side is obtained from getSystemInfo. |
||sdk_version |SDK type |string |Example: 60700 |The version number of the SDK itself |
||sdk_lib |SDK version |string |Example: ios | |
||ab_version |AB test VID |int |Example: 24105 | |
||client_ip |Internet Protocol Address |string |Example: 59.51.125.143 | |
||loc_city_id |city |string |Example: Dongying |Based on the value of the client_ip |
||loc_province_id |province |string |Example: Shandong |ditto |
||loc_country_id |country |string |Example: China |ditto |
||network_type |network type |string |Example: wifi |The APP side is obtained from the system API, and the Mini Program side is obtained from getNetworkType. |
||network_carrier |operator |string |Example: China Mobile |The APP side is obtained from the system API. |
||resolution |resolution |string |Example: 1440 \* 2960 |The APP side is obtained from the system API, and the Mini Program side is obtained from getSystemInfo. |
||language |system language |string |Example: de |The APP side is obtained from the system API, and the Mini Program side is obtained from getSystemInfo. |
||platform |platform type |string |Example: ios |The APP side is obtained from the system API, and the Mini Program side is obtained from getSystemInfo. |
||browser |browser |string |Example: chrome |iOS fixed to "ios", Android fixed to "Android" |
||browser_version |Browser version |string |Example: 8.7 | |
||package |install package name |string |Example: [com.zwqn.cn](http://com.zwqn.cn) |The APP side is obtained from the system API. |
||user_id |user ID |string |Example: 4311234 | |
||Brand (privatization called device_brand) |Mobile phone brand |string |Example: Huawei | |
