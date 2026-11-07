---
title: "APP Preset Events and Properties"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/APP-Preset-Events-and-Properties"
---

<span id="f2ca8ecb"></span>
# Background information


* Preset event public properties are the public properties that all events have.

   In the APP terminal can be further subdivided into Android terminal, iOS terminal. Of which:

   * Android\-side and iOS\-side event public property content can be found below [Common Preset Event Public Properties](https://docs.byteplus.com/docs/DataTester/APP-Preset-Events-and-Properties#d891db3e).

   * Android\-specific event public property content can be found below [Android specific](https://docs.byteplus.com/docs/DataTester/APP-Preset-Events-and-Properties#094a5bc8).

   * iOS end\-specific event public property content can be found below [iOS unique](https://docs.byteplus.com/docs/DataTester/APP-Preset-Events-and-Properties#132c76dc).

* The event properties unique to a specific preset event are the preset event properties.

   In the APP terminal can be further subdivided into Android terminal, iOS terminal. Of which:

   * Android\-side and iOS\-side event public property content can be found below [Event properties for all preset events](https://docs.byteplus.com/docs/DataTester/APP-Preset-Events-and-Properties#240f7a9d).

   * Android\-specific event public property content can be found below [Android-specific events and properties](https://docs.byteplus.com/docs/DataTester/APP-Preset-Events-and-Properties#3755d1a4).

   * iOS end\-specific event public property content can be found below [iOS specific events and properties](https://docs.byteplus.com/docs/DataTester/APP-Preset-Events-and-Properties#efc235db).

* Content related to user properties can be found [Preset User Properties](https://docs.byteplus.com/docs/DataTester/Preset-User-Properties).


<span id="304b1a07"></span>
# Preset event public properties


* Event/Property Type Description: Android/iOS have event public properties.

* Reporting mechanism: The SDK defaults to batch reporting of packaged events every 60s.


<span id="d891db3e"></span>
## Common Preset Event Public Properties


|**Property name** |**Property display name** |**Field type** |**Data source** |**Property description or example** |
|---|---|---|---|---|
|is_login |Whether to log in |String |Server level generation |Whether to log in |
|$is_first_day |Whether to visit on the first day |int |Server level generation |This property indicates that the target event and the first event occurred on the same day.<br><br>Similar functionality to the Old and New User (user_is_new) properties.<br><br><br>* user_is_new: The target event and the first event occur in the same cycle. For example, in a bar chart, the period is the time frame selected by the user.<br><br>* The main difference between new and old users (user_is_new) and whether the first day of access ($is_first_day) is that the former is affected by the selected time period, while the latter is not affected, so the latter has better consistency in the calculation results obtained in different chart types. It is recommended to use whether the first day of access ($is_first_day) to judge new and old users. |
|$event_name |event name |String |Server level generation |The name of the event |
|$event_time |Event time |DateTime |Server level generation |Event triggered client side time |
|network_type |network type |String |System API |Current network type, example: wifi |
|aid |— |String |user incoming |app_id |
|app_version |software version |String |System API |APP version number, system API acquisition. |
|app_channel |channel |String |user incoming |Channel, manually set by the user. |
|loc_country_id |country |String | |Based on the value of the client_ip, the administrative region is inferred. Example: China |
|language |system language |String |System API |System language, the APP side is obtained from the system API, and the Mini Program side is obtained from getSystemInfo. |
|os_name |Operating System |String |fixed value |Operating System |
|os_version |System version |String |System API |System version, the APP side is obtained from the system API, the Web side is parsed from ua, and the Mini Program side is obtained from getSystemInfo. |
|platform |platform type |String |fixed value |platform |
|region |System area |String |System API |System area |
|resolution |resolution |String |System API |Screen definition, the APP side is obtained from the system API, and the Mini Program side is obtained from getSystemInfo |
|sdk_lib |SDK type |String |fixed value |SDK type, example: ios |
|sdk_version |SDK version |String |fixed value |SDK version number |
|timezone |Time Zone |String |System API |System Time Zone |


<span id="094a5bc8"></span>
## Android specific

Android\-specific, iOS unsupported event public properties.


|**Property name** |**Property display name** |**Field type** |**Data source** |**Property description or example** |
|---|---|---|---|---|
|device_brand |Mobile phone brand |String |System API |Example: iPhone |
|cpu_abi |abi corresponding to cpu architecture |String |System API | |
|app_version_minor |Four\-digit version number |String |user incoming |iOS get the build number from the system API, Android needs to set it manually. |
|app_region |Software region |String |user incoming | |
|network_carrier |operator |String |System API |Carrier information |


<span id="132c76dc"></span>
## iOS unique

Event public properties specific to the iOS.


|**Property name** |**Property display name** |**Field type** |**Data source** |**Property description or example** |
|---|---|---|---|---|
|app_version_minor |Four\-digit version number |String |System API |Build number, iOS get the build number from the system API, Android needs to set it manually. |
|app_language |software language |String |User Incoming, System API |User setting manually. If not passed in, the system language will be used to cover the bottom line. |
|app_region |Software region |String |User Incoming, System API |User setting manually. No incoming will use the system area to cover the bottom line. |


<span id="3af816ef"></span>
# Preset events and event properties

Preset events and event properties specific to the corresponding event. It is also divided into event properties that all preset events have, and event properties specific to the corresponding event.

<span id="240f7a9d"></span>
## Event properties for all preset events


|**Property name** |**Property display name** |**Field type** |**Data source** |**Property description or example** |
|---|---|---|---|---|
|$screen_orientation | |Number |System API |The local time of the event |
|$longitude |Geographical location longitude |Number |User Incoming, System API |Andoid only supports user incoming, iOS supports automatic fetching |
|$latitude |Geographic location latitude |Number |user incoming |Andoid only supports user incoming, iOS supports automatic fetching |
|$geo_coordinate_system | |String |user incoming |Andoid only supports user incoming, iOS supports automatic fetching |
|$app_version |software version |String |System API | |


<span id="74a674db"></span>
## Application Launch Event (app_launch)


|**Event name** |**Event description** |**Property name** |**Property display name** |**Property value type** |**Property description** |**Trigger timing** |
|---|---|---|---|---|---|---|
|app_launch |Application launch |session_id |Session ID |string | |* When user launches App(enter the splash screen), there will be a launch event.<br><br>* When switch users, the previous session will end and a new launch event will be generated. |
|||session_duration |The session duration of this open app |int |Session duration, based on the summation of the duration of the device in the foreground, in seconds, no such property in the app_launch or a value of 0. ||
|||$page_title |page title |string | | |
|||$page_key |page name |string | | |
|||$resume_from_background |Whether to restore from the background |string | | |


<span id="06bebc82"></span>
## Application Exit Event (app_terminate)


|**Event name** |**Event description** |**Property name** |**Property display name** |**Property value type** |**Property description** |**Trigger timing** |
|---|---|---|---|---|---|---|
|app_terminate |app exit |session_id |Session ID |string |Session ID |* When the user stops using the App (entering the background), a terminate event will be generated. In Android, entering the background will stay for 30s before triggering. iOS, entering the background will trigger immediately.<br><br>* When switching users, the last session ends and a terminate event occurs. |
|||session_duration |The session duration of this open app |int |Session duration, based on the summation of the duration of the device in the foreground, in seconds. ||
|||$page_title |page title |string | | |
|||$page_key |page name |string | | |


<span id="84bc27a7"></span>
## Full event tracking (bav2b_)


|**Event name** |**Event description** |**Property** |**Property value type** |**Property description** |
|---|---|---|---|---|
|bav2b_page |page visit |page_key |string |page unique identifier |
|||refer_page_key |string | |
|||is_back |int | |
|||page_title |string |Page title |
|||page_path |string |Path to the page |
|||referrer_page_path |string | |
|||refer_page_title |string | |
|||$is_rn |int |Determine whether to RN page |
|||$rn_root_tag |int |RN page unique number |
|||$is_flutter |int |Whether to use flutter full event tracking |
|$bav2b_page_leave |page leave |$page_duration |int |page duration |
|||page_key |string |page unique identifier |
|||page_title |string |Page title |
|||$is_rn |int |Determine whether to RN page |
|||$is_flutter |int |Whether to use flutter full event tracking |
|||$rn_root_tag |int |RN page unique number |
|bav2b_click |element click |page_key |string |page unique identifier |
|||element_path |string |A string that uniquely identifies the control, xPath |
|||positions |string array |The position of the element in the list at each level, possibly 2\-2 0\-1. |
|||texts |string array |Element copy is an array, and the length of each copy in the array is limited to 200 characters |
|||element_width |string |Element width in the same unit as header.resolution |
|||element_height |string |Element height, unit same as header.resolution |
|||touch_x |int |The distance between the click position and the left border of the element, in the same unit as header.resolution |
|||touch_y |int |The distance between the click position and the upper boundary of the element, in the same unit as header.resolution |
|||page_title |string |Page title |
|||element_id |string |The element ID is obtained by default on the Android side; each control on the iOS side generally does not set the ID, so the iOS side will not obtain it by default. Can be set manually |
|||element_type |string |Element type, the type of control, such as Button |
|||$is_rn |int |Determine whether to RN page |
|||$is_flutter |int |Whether to use flutter full event tracking |
|||$rn_root_tag |int |RN page unique number |
|$bav2b_exposure |element exposure |page_key |string |page unique identifier |
|||element_path |string |A string that uniquely identifies the control, xPath |
|||positions |string array |The position of the element in the list at each level, possibly 2\-2 0\-1. |
|||texts |string array |Element copy is an array, and the length of each copy in the array is limited to 200 characters |
|||element_width |string |Element width in the same unit as header.resolution |
|||element_height |string |Element height, unit same as header.resolution |
|||page_title |string |Page title |
|||element_id |string |The element ID is obtained by default on the Android side; each control on the iOS side generally does not set the ID, so the iOS side will not obtain it by default. Can be set manually |
|||element_type |string |Element type, the type of control, such as Button |
|||$exposure_type |int |Exposure Type |
|$bav2b_slide |Slide event |$direction |int |sliding direction |
|||$offsetX |float |lateral offset |
|||$offsetY |float |vertical offset |
|||page_key |string |page unique identifier |
|||element_path |string |A string that uniquely identifies the control, xPath |
|||element_width |string |Element width in the same unit as header.resolution |
|||element_height |string |Element height, unit same as header.resolution |
|||page_title |string |Page title |
|||element_id |string |The element ID is obtained by default on the Android side; each control on the iOS side generally does not set the ID, so the iOS side will not obtain it by default. Can be set manually |
|||element_type |string |Element type, the type of control, such as Button |


<span id="592ce49f"></span>
## Application crash event (crash)


|**Event name** |**Event description** |**Property** |**Property display name** |**Property value type** |**Property description** |
|---|---|---|---|---|---|
|$crash |Detect the application generated when Crash, Android currently supports Java layer Exception, iOS support NSException. |$is_backstage |Is it background? |string |Is it background? |
|||$event_time |Event time |datetime |Crash time |
|||$crash_thread |Crash thread |string |Crash thread |
|||$crash_process |Crash process |string |Crash process |
|||$detailed_stack |detailed stack |string |detailed stack |
|||$os_version<br><br><br>* Android not reported |System version |string |System version |
|||$app_version<br><br><br>* Android not reported |software version |string |software version |
|||$device_model<br><br><br>* Android not reported |Equipment model |string |Equipment model |
|||$resolution<br><br><br>* Android not reported |resolution |string |resolution |
|||$app_channel<br><br><br>* Android not reported |channel |string |channel |
|||$cpu<br><br><br>* Android not reported |CPU architecture |string |CPU architecture |
|||$session_duration<br><br><br>* Android not reported |Duration of use (seconds/milliseconds) |int |Usage time (milliseconds) |
|||$rom<br><br><br>* Android not reported |ROM |string |ROM |


<span id="3755d1a4"></span>
## Android\-specific events and properties

Not yet.

<span id="efc235db"></span>
## iOS specific events and properties

iOS\-specific preset events and corresponding event properties.


|**Event name** |**Event description** |**Property name** |**Property display name** |**Property value type** |**Property description** |
|---|---|---|---|---|---|
|$app_launch_passively |passive start |$resume_from_background |Whether to restore from the background |bool |Whether to restore from the background |


<span id="f026cf54"></span>
## Other events/properties

<span id="ab781be5"></span>
### Inter\-App communications events and properties

Inter\-App communications events are events on each end, see the details of the current Inter\-App communications events and properties involved [Inter-Side Preset Properties](https://docs.byteplus.com/docs/DataTester/Inter-Side-Preset-Properties).

<span id="8c050565"></span>
### AB exposure event


|**Event name** |**Event description** |**Property** |**Property value type** |**Property description** |
|---|---|---|---|---|
|abtest_exposure |AB experimental exposure |ab_sdk_version |string |AB experiment vid |


<span id="b3758ee7"></span>
### Reserved property name


|**Property name** |**Property display name** |**Property value type** |
|---|---|---|
|$target_uuid_list |Active Event UUID List |list |
|$inactive |Is it a passive event? |string |
|$inline |Is it a relational event? |string |
|$source_uuid |active event UUID |string |
|$inactive |Is it a passive event? |string |
|aid | |int |
|__param_from_special | |string |
