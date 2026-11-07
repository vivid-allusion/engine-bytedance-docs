---
title: "Full Event Tracking Preset Events and Properties"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Full_Event_Tracking_Preset_Events_and_Properties"
---

<span id="f1e09e47"></span>
# APP


* App\-side full event tracking preset events and preset properties

   When accessing data, after turning on the full event tracking switch, you can report the following preset full event tracking events and properties. At the same time, you can also report custom event properties, custom events, or configure pages to be filtered for full event tracking reports. For details, please refer to the full event tracking relevant chapters in the SDK event tracking document at each end.

   
   |**Event name** |**Event description** |Trigger mechanism |**Property** |**Property value type** |**Property description** |
   |---|---|---|---|---|---|
   |bav2b_page |page visit |Trigger the report after the page is opened |page_key |string |page unique identifier |
   ||||refer_page_key |string |When there is a page switching operation, the refer_page is the previous page information, refer_page_key the source page **class name (class_name)**  , when the application is cold start, such property value will be empty. |
   ||||is_back |int | |
   ||||page_title |string |Page title |
   ||||page_path |string |Path of the page |
   ||||referrer_page_path |string |When there is a page switching operation, the refer_page is the previous page information, referrer_page_path the page path relationship, when the application is cold start, such property values will be empty. |
   ||||refer_page_title |string |When there is a page switch operation, the refer_page is the previous page information, refer_page_title the name of the previous page (page title), when the application is cold start, such property values will be empty. |
   ||||$is_rn |int |Determine whether to RN page |
   ||||$rn_root_tag |int |RN page unique number |
   ||||$is_flutter |int |Whether to use flutter full event tracking |
   |$bav2b_page_leave |page leave |Trigger a report after the page leaves |$page_duration |int |page duration.<br><br><br>* Android side: page stay time property. At this time, the length is calculated by recording the page entry and exit timestamp. If the corresponding timestamp cannot be calculated due to the failure to obtain the corresponding timestamp normally, the default value of 1s will be assigned as the bottom value.<br><br>* iOS: Record a duration event with when the page is the key when the page enters, and record the current entry time. Extract the duration event when the page exits, subtract the page entry time from the current time, and the median difference is the length of the dwell time. |
   ||||page_key |string |page unique identifier |
   ||||page_title |string |Page title |
   ||||$is_rn |int |Determine whether to RN page |
   ||||$is_flutter |int |Whether to use flutter full event tracking |
   ||||$rn_root_tag |int |RN page unique number |
   |bav2b_click |element click |Trigger a report after clicking on a page element |page_key |string |page unique identifier |
   ||||element_path |string |A string that uniquely identifies the control, xPath |
   ||||positions |Data (array of type string) |The position of the element in the list at each level, possibly ["2\-2", "0\-1"] |
   ||||texts |Data (array of type string) |Element copy is an array, and the length of each copy in the array is limited to 200 characters |
   ||||element_width |string |Element width in units equal to header.resolution |
   ||||element_height |string |Element height, unit same as header.resolution |
   ||||touch_x |int |The distance between the click position and the left border of the element, in the same unit as header.resolution |
   ||||touch_y |int |The distance between the click position and the upper boundary of the element, in the same unit as header.resolution |
   ||||page_title |string |Page title |
   ||||element_id |string |The element ID is obtained by default on the Android side; each control on the iOS side generally does not set the ID, so the iOS side will not obtain it by default. Can be set manually |
   ||||element_type |string |Element type, the type of control, such as Button |
   ||||$is_rn |int |Determine whether to RN page |
   ||||$is_flutter |int |Whether to use flutter full event tracking |
   ||||$rn_root_tag |int |RN page unique number |
   

* Other related events: $bav2b_exposure element exposure.

   When using full event tracking, you can combine the $bav2b_exposure element to expose relevant property data to further analyze user behavior.

   
   |**Event name** |**Event description** |**Property** |**Property value type** |**Property description** |
   |---|---|---|---|---|
   |$bav2b_exposure |element exposure |page_key |string |page unique identifier |
   |||element_path |string |A string that uniquely identifies the control, xPath |
   |||positions |Data (array of type string) |The position of the element in the list at each level, possibly ["2\-2", "0\-1"] |
   |||texts |Data (array of type string) |Element copy is an array, and the length of each copy in the array is limited to 200 characters |
   |||element_width |string |Element width in units equal to header.resolution |
   |||element_height |string |Element height, unit same as header.resolution |
   |||page_title |string |Page title |
   |||element_id |string |The element ID is obtained by default on the Android side; each control on the iOS side generally does not set the ID, so the iOS side will not obtain it by default. Can be set manually |
   |||element_type |string |Element type, the type of control, such as Button |
   |||$exposure_type |int |Exposure Type |
   


<span id="fb97bf1b"></span>
# Web Side

When accessing data, after turning on the full event tracking switch, you can report the following preset full event tracking events and properties. At the same time, you can also report custom event properties, custom events, or configure pages to be filtered for full event tracking reports. For details, please refer to the full event tracking relevant chapters in the SDK event tracking document at each end.


|**Event name** |**Event display name** |**Property name** |**SaaS/privatization support** |**Property display name** |**Property value type** |**Property value example or description** |
|---|---|---|---|---|---|---|
|bav2b_click |Click on all buried points |is_html |SaaS/Privatization |is_html |int |Default is 1. |
|||page_key |SaaS/Privatization |Page key |string |The key of the page is equivalent to the address of the page |
|||page_title |SaaS/Privatization |page title |string |The title of the page "xx page" |
|||element_path |SaaS/Privatization |element path |string |The absolute path of the element relative to the body'body/div.div' |
|||positions |SaaS/Privatization |element position |string |Position of the element relative to the body<br><br>[1,0,1,0] |
|||element_title |SaaS/Privatization |element title |string |The title of the element, if the title property is set on the dom, there will be |
|||texts |SaaS/Privatization |element text content |string |The content of an element, such as: 'I am a line of text' |
|||element_id |SaaS/Privatization |Element ID |string |The id of the element, if the id property is set on the dom, there will be |
|||element_class_name |SaaS/Privatization |element class name |string |The class of the element, if the class property is set on the dom, there will be |
|||element_type |SaaS/Privatization |element type |string |The type of element, different elements have different types, such as 0, 1, 3, etc |
|||element_width |SaaS/Privatization |element width |int |Click the width of the element |
|||element_height |SaaS/Privatization |element height |int |The height of the clicked element |
|||touch_x |SaaS/Privatization |Click position X coordinate |int |The abscissa of the click position relative to the upper left corner of the element |
|||touch_y |SaaS/Privatization |Click position Y coordinate |int |The ordinate of the click position relative to the upper left corner of the element |
|||page_start_ms |SaaS/Privatization |page opening time |int |Page opening timestamp |
|||since_page_start_ms |SaaS/Privatization |The time since the page opened when the click occurred |int |Time elapsed since the click occurred, in milliseconds |
|||page_path |SaaS/Privatization |page path |string |The path to the page,/aa/b.html |
|||page_host |SaaS/Privatization |page domain name |string |The domain name of the page, www.aaaa.com |
|bav2b_page |Full event tracking access |is_html |SaaS/Privatization |is_html |int | |
|||is_back |SaaS/Privatization |is_back |int | |
|||page_key |SaaS/Privatization |Page key |string | |
|||url |SaaS/Privatization |page address |string | |
|||page_title |SaaS/Privatization |page title |string | |
|||page_path |SaaS/Privatization |page path |string | |
|||page_host |SaaS/Privatization |page domain name |string | |
|||page_total_height |SaaS/Privatization |total page height |int | |
|||page_total_width |SaaS/Privatization |total page width |int | |
|||scroll_height |SaaS/Privatization |page scroll bar height |int | |
|||scroll_width |SaaS/Privatization |page scrollbar width |int | |
|||page_manual_key |SaaS/Privatization |Page manual_key |string | |
|||page_start_ms |SaaS/Privatization |page opening time |int | |
|||refer_page_title |SaaS/Privatization |Source page title |string | |
|||refer_page_duration_ms |SaaS/Privatization |access time to the source page |int | |
|||refer_page_key |SaaS/Privatization |Source page key |string | |
|||refer_page_manual_key |SaaS/Privatization |Source page manual_key |string | |
|||is_first_time |SaaS/Privatization |Whether to visit for the first time |int | |
|bav2b_beat |Full event tracking heartbeat |is_html |SaaS/Privatization |is_html |int | |
|||page_key |SaaS/Privatization |Page key |string | |
|||beat_type |SaaS/Privatization |Beat type |int | |
|||page_title |SaaS/Privatization |page title |string | |
|||page_viewport_width |SaaS/Privatization |Page visual window width |int | |
|||page_viewport_height |SaaS/Privatization |Page viewable window height |int | |
|||page_total_height |SaaS/Privatization |total page height |int | |
|||page_total_width |SaaS/Privatization |total page width |int | |
|||scroll_height |SaaS/Privatization |page scroll bar height |int | |
|||scroll_width |SaaS/Privatization |page scrollbar width |int | |
|||page_manual_key |SaaS/Privatization |Page manual_key |string | |
|||page_start_ms |SaaS/Privatization |page opening time |int | |
|||since_page_start_ms |SaaS/Privatization |since_page_start_ms |int | |
|bav2b_page_statistics |Full event tracking statistics |is_html |SaaS/Privatization |is_html |int | |
|||page_key |SaaS/Privatization |Page key |string | |
|||page_title |SaaS/Privatization |page title |string | |
|||page_manual_key |SaaS/Privatization |manual_key |string | |
|||page_start_ms |SaaS/Privatization |page opening time |int | |
|||page_init_cost_ms |SaaS/Privatization |page opening time |int | |
|||refer_page_key |SaaS/Privatization |Source page key |string | |
|||refer_page_manual_key |SaaS/Privatization |Source page manual_key |string | |
|$bav2b_exposure |exposure event |$exposure_type |SaaS/Privatization |Exposure Type |int | |
|||is_html |SaaS/Privatization |is_html |int | |
|||page_key |SaaS/Privatization |Page key |string | |
|||page_title |SaaS/Privatization |page title |string | |
|||element_path |SaaS/Privatization |element path |string | |
|||positions |SaaS/Privatization |element position |string | |
|||element_title |SaaS/Privatization |element title |string | |
|||element_id |SaaS/Privatization |Element ID |string | |
|||element_class_name |SaaS/Privatization |Element class name |string | |
|||element_type |SaaS/Privatization |element type |int | |
|||element_width |SaaS/Privatization |element width |int | |
|||element_height |SaaS/Privatization |element height |int | |
|||touch_x |SaaS/Privatization |Click position X coordinate |int | |
|||touch_y |SaaS/Privatization |Click position Y coordinate |int | |
|||page_start_ms |SaaS/Privatization |page opening time |int | |
|||since_page_start_ms |SaaS/Privatization |since_page_start_ms |int | |
|||page_path |SaaS/Privatization |page title |string | |
|||page_host |SaaS/Privatization |page domain name |string | |
|$bav2b_slide |Slide event |$direction |SaaS/Privatization |sliding direction |int | |
|||$offsetX |SaaS/Privatization |lateral offset |float | |
|||$offsetY |SaaS/Privatization |vertical offset |float | |
|||element_path |SaaS/Privatization |element path |string | |
|||positions |SaaS/Privatization |element position |string | |
|||texts |SaaS/Privatization |element text |string | |
|||element_title |SaaS/Privatization |element title |string | |
|||element_id |SaaS/Privatization |Element ID |string | |
|||element_class_name |SaaS/Privatization |Element class |string | |
|||element_type |SaaS/Privatization |element type |int | |
|||element_width |SaaS/Privatization |element width |int | |
|||element_height |SaaS/Privatization |element height |int | |
|||touch_x |SaaS/Privatization |Click position X coordinate |int | |
|||touch_y |SaaS/Privatization |Click position Y coordinate |int | |
|||page_manual_key |SaaS/Privatization |Page manual_key |string | |
|||elememt_manual_key |SaaS/Privatization |Element manual_key |string | |
|||since_page_start_ms |SaaS/Privatization |since_page_start_ms |int | |
|||page_start_ms |SaaS/Privatization |page opening time |int | |
|||page_path |SaaS/Privatization |page path |string | |
|||page_host |SaaS/Privatization |page domain name |string | |
|||is_html |SaaS/Privatization |is_html |int | |
|||page_key |SaaS/Privatization |Page key |string | |
|||page_title |SaaS/Privatization |page title |string | |


<span id="2806ecb8"></span>
# Mini Program


|**Event name** |**Monitoring timing** |**Event description** |**Property name** |**Property display name** |**SaaS/privatization support** |**Property description** |**Property type** |**Version** |**Remarks** |
|---|---|---|---|---|---|---|---|---|---|
|predefine_pageview |Page.onShow |Report when the page is displayed, and also report when the reverse operation is performed. |session_id |Session ID |SaaS/Privatization |ditto | |1.3.12+ | |
||||scene |scene value |SaaS/Privatization |ditto | | | |
||||path |startup path |SaaS/Privatization |Path to the current page |string | |Get the path to the current page through getCurrentPages () |
||||query_$ | |SaaS/Privatization |Each option property in the options object of the current page is prefixed with "query_". |any | |Get options to the current page through getCurrentPages ()<br><br>Consistent with app_launch approach |
||||title |Visit page title |SaaS/Privatization |Current page title | |1.5.4+ | |
||||refer_path | |SaaS/Privatization |Previous page path | | |The field may not be available, depending on whether there is a previous page |
||||refer_query | |SaaS/Privatization |Previous page query parameters | | |The field may not be available, depending on whether there is a previous page |
|bav2b_click |When the event handler defined in Page is fired |Currently only tap events are supported. |path |startup path |SaaS/Privatization |Path to the current page |string |1.13.0+ |Get the path to the current page through getCurrentPages () |
||||page_key | |SaaS/Privatization |Currently equal to path |string | | |
||||query_$ | |SaaS/Privatization |Some custom data (dataset) currently attached by the triggered node |string | |Example:<br><br>Data\-xxx = "This is xxx" is set on the component and is collected as query_xxx: "This is xxx" |
