---
title: "Web Preset Events and Properties"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Web-Preset-Events-and-Properties"
---

<span id="a82f51d4"></span>
# Preset event public properties

<span id="898b95ad"></span>
## Common Preset Event Public Properties


|**Property name** |**Property display name** |**Field type** |**Data source** |**Property description or example** |
|---|---|---|---|---|
|os_name |Operating System |String |System API |The value is ios/android/windows/mac. |
|os_version |System version |String |System API | |
|device_model |Equipment model |String |System API | |
|language |system language |String |System API | |
|platform |platform type |String |fixed value | |
|sdk_version |SDK version |String |SDK generation | |
|sdk_lib |SDK type |String |fixed value | |
|timezone |Time Zone |String |System API | |
|resolution |resolution |String |System API | |


<span id="1a15b4d3"></span>
## Web\-side\-specific preset event public properties


|**Property name** |**Property display name** |**Field type** |**Data source** |**Property description or example** |
|---|---|---|---|---|
|browser |browser |String |System API |Example: chrome |
|browser_version |Browser version |String |System API |Example: 8.7 |
|referrer |source address |String |System API | |
|referrer_host |Forward Domain Name |String |System API | |


<span id="726f3a6a"></span>
# Preset event public properties

<span id="258102f0"></span>
## Common Preset Event Public Properties

Both the Web side and the Mini Program side have event public properties.


|**Property name** |**Property display name** |**Field type** |**Data source** |**Property description or example** |
|---|---|---|---|---|
|$current_path |Current page path |String |System API |Mini Programs only, the path to the current page |
|$current_query |Current page query |String |System API |Mini Program only, query on current page |


<span id="01da3ba2"></span>
## Page access events (predefine_page_)


|**Event name** |**Event display name** |**Property name** |**Property display name** |**Property value type** |**Property description** |
|---|---|---|---|---|---|
|predefine_pageview |page visit<br><br>The pv event, when the sdk initialization is complete, that is, the start event is called, the pv will be sent once and only once. It will bring page title, url, path, referrer and other properties.<br><br>When you are on an SPA page and the page changes, you can call the following API and pass in some custom parameters, which will be merged with the default parameters. （ Tea.predefinePageView(params)） |_ip_int |without |int | |
|||referer_full_domain |source domain name |string | |
|||referer_site_name |Source website (name) |string | |
|||referer_type |source type |string |1. If the referrer of the webpage is the same as the domain, referer_type property is inner, and it is judged as in\-app jump inner;<br><br>2. social network social_network classification and search engine search_engine classification of the site we are exhaustive;<br><br>3. If the referrer is empty, it will be regarded as direct access;<br><br>4. Except for in\-app jump inner, social network social_network, search engine search_engine, the rest are referring_site external links. |
|||url_full_domain |access domain name |string |Through url derivation, the url string is parsed as a java.net . URL object and obtained by calling the getHost () method. |
|||visit_from_outside |Whether to visit out\-of\-app |string |Derived from the url and referrer, true if the top\-level domains of the url and referrer are different, otherwise false (constant false if one of the url/referrer cannot resolve the host due to a problem with the reporting format). |
|||url |visit link |string |After the SDK initialization is complete, the PV will obtain the location.href of the current page as the URL. |
|||url_path |URL address |string |After the SDK initialization is complete, the PV gets the location.pathname of the current page as url_path. |
|||$is_first_time |Whether to visit for the first time |string | |
|predefine_page_alive |Duration of Stay Active |tiltle |page title |string | |
|||url |visit link |string | |
|||url_path |URL address |string | |
|||duration |length of stay |int | |
|predefine_page_close |Duration of Stay Close |tiltle |page title |string | |
|||url |visit link |string | |
|||url_path |URL address |string | |
|||duration |length of stay |int | |


<span id="21a14545"></span>
## Full event tracking (bav2b_)


|**Event name** |**Event display name** |**Property name** |**Property display name** |**Property value type** |**Property value example or description** |
|---|---|---|---|---|---|
|bav2b_click |Click on all buried points |is_html |is_html |int |Default is 1. |
|||page_key |Page key |string |The key of the page is equivalent to the address of the page |
|||page_title |page title |string |The title of the page "xx page" |
|||element_path |element path |string |The absolute path of the element relative to the body'body/div.div' |
|||positions |element position |string |Position of the element relative to the body<br><br>[1,0,1,0] |
|||element_title |element title |string |The title of the element, if the title property is set on dom, there will be |
|||texts |element text content |string |The content of an element, such as: 'I am a line of text' |
|||element_id |Element ID |string |The id of the element, if the id property is set on the dom, there will be |
|||element_class_name |element class name |string |The class of the element, if the class property is set on the dom, there will be |
|||element_type |element type |string |The type of element, different elements have different types, such as 0, 1, 3, etc |
|||element_width |element width |int |Click the width of the element |
|||element_height |element height |int |The height of the clicked element |
|||touch_x |Click position X coordinate |int |The abscissa of the click position relative to the upper left corner of the element |
|||touch_y |Click position Y coordinate |int |The ordinate of the click position relative to the upper left corner of the element |
|||page_start_ms |page opening time |int |Page opening timestamp |
|||since_page_start_ms |The time since the page opened when the click occurred |int |Time elapsed since the click occurred, in milliseconds |
|||page_path |page path |string |The path to the page,/aa/b.html |
|||page_host |page domain name |string |The domain name of the page, www.aaaa.com |
|bav2b_page |Full event tracking access |is_html |is_html |int | |
|||is_back |is_back |int | |
|||page_key |Page key |string | |
|||url |page address |string | |
|||page_title |page title |string | |
|||page_path |page path |string | |
|||page_host |page domain name |string | |
|||page_total_height |total page height |int | |
|||page_total_width |total page width |int | |
|||scroll_height |page scroll bar height |int | |
|||scroll_width |page scrollbar width |int | |
|||page_manual_key |Page manual_key |string | |
|||page_start_ms |page opening time |int | |
|||refer_page_title |Source page title |string | |
|||refer_page_duration_ms |access time to the source page |int | |
|||refer_page_key |Source page key |string | |
|||refer_page_manual_key |Source page manual_key |string | |
|||is_first_time |Whether to visit for the first time |int | |
|bav2b_beat |Full event tracking heartbeat |is_html |is_html |int | |
|||page_key |Page key |string | |
|||beat_type |Beat type |int | |
|||page_title |page title |string | |
|||page_viewport_width |Page visual window width |int | |
|||page_viewport_height |Page viewable window height |int | |
|||page_total_height |total page height |int | |
|||page_total_width |total page width |int | |
|||scroll_height |page scroll bar height |int | |
|||scroll_width |page scrollbar width |int | |
|||page_manual_key |Page manual_key |string | |
|||page_start_ms |page opening time |int | |
|||since_page_start_ms |since_page_start_ms |int | |
|bav2b_page_statistics |Full event tracking statistics |is_html |is_html |int | |
|||page_key |Page key |string | |
|||page_title |page title |string | |
|||page_manual_key |manual_key |string | |
|||page_start_ms |page opening time |int | |
|||page_init_cost_ms |page opening time |int | |
|||refer_page_key |Source page key |string | |
|||refer_page_manual_key |Source page manual_key |string | |
|$bav2b_exposure |exposure event |$exposure_type |Exposure Type |int | |
|||is_html |is_html |int | |
|||page_key |Page key |string | |
|||page_title |page title |string | |
|||element_path |element path |string | |
|||positions |element position |string | |
|||element_title |element title |string | |
|||element_id |Element ID |string | |
|||element_class_name |Element class name |string | |
|||element_type |element type |int | |
|||element_width |element width |int | |
|||element_height |element height |int | |
|||touch_x |Click position X coordinate |int | |
|||touch_y |Click position Y coordinate |int | |
|||page_start_ms |page opening time |int | |
|||since_page_start_ms |since_page_start_ms |int | |
|||page_path |page title |string | |
|||page_host |page domain name |string | |
|$bav2b_slide |Slide event |$direction |sliding direction |int | |
|||$offsetX |lateral offset |float | |
|||$offsetY |vertical offset |float | |
|||element_path |element path |string | |
|||positions |element position |string | |
|||texts |element text |string | |
|||element_title |element title |string | |
|||element_id |Element ID |string | |
|||element_class_name |Element class |string | |
|||element_type |element type |int | |
|||element_width |element width |int | |
|||element_height |element height |int | |
|||touch_x |Click position X coordinate |int | |
|||touch_y |Click position Y coordinate |int | |
|||page_manual_key |Page manual_key |string | |
|||elememt_manual_key |Element manual_key |string | |
|||since_page_start_ms |since_page_start_ms |int | |
|||page_start_ms |page opening time |int | |
|||page_path |page path |string | |
|||page_host |page domain name |string | |
|||is_html |is_html |int | |
|||page_key |Page key |string | |
|||page_title |page title |string | |


<span id="ed8f444b"></span>
## Heartbeat detection (be_active)


|**Event name** |**Event display name** |**Property name** |**Property display name** |**Property value type** |**Property value example or description** |
|---|---|---|---|---|---|
|_be_active |Heartbeat detection |start_time |start time |int | |
|||end_time |end time |int | |
|||url |visit link |string | |
|||referrer |source link |string | |
|||title |Visit page title |string | |


<span id="c05bb1ec"></span>
## Other events/properties

<span id="3377f330"></span>
### AB exposure event


|**Event name** |**Event display name** |**Property name** |**Property display name** |**Property value type** |**Property value example or description** |**Description** |
|---|---|---|---|---|---|---|
|abtest_exposure |experimental exposure |ab_url |page address |string | | |
