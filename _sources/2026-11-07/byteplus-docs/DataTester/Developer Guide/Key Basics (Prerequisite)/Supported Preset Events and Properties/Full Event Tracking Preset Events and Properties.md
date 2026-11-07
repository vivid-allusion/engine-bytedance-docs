---
title: "Full Event Tracking Preset Events and Properties"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Full-Event-Tracking-Preset-Events-and-Properties"
---


|End type |Event name |Event display name |Property |Property display name |Property value type |Property value example or description |
|---|---|---|---|---|---|---|
|App side |bav2b_page |page visit |page_key |page ID |string |page unique identifier |
||||referrer_page_key |source page ID |string | |
||||is_back |Whether to go back |int | |
||||page_title |page title |string |Page title |
||||page_path |page address |string |Path to the page |
||||referrer_page_path |Forward Address |string | |
||||url |visit link |string | |
||bav2b_click |element click |page_key |page ID |string |page unique identifier |
||||element_path |widget identifier |string |A string that uniquely identifies the control, xPath |
||||positions |element position |string array |The position of the element in the list at each level, possibly 2\-2 0\-1. |
||||texts |element copy |string array |Element copy is an array, and the length of each copy in the array is limited to 200 characters |
||||element_width |element width |string |Element width in the same unit as header.resolution |
||||element_height |element height |string |Element height, unit same as header.resolution |
||||touch_x |element left margin distance |int |The distance between the click position and the left border of the element, in the same unit as header.resolution |
||||touch_y |element right boundary distance |int |The distance between the click position and the upper boundary of the element, in the same unit as header.resolution |
||||page_title |page title |string |Page title |
||||element_id |element ID |string |The element ID is obtained by default on the Android side; each control on the iOS side generally does not set the ID, so the iOS side will not obtain it by default. Can be set manually |
||||element_type |element type |string |Element type, the type of control, such as Button |
|web |bav2b_page |page visit |page_key |page ID |string | |
||||is_html |HTML page |int | |
||||page_start_ms |page launch time |float | |
||||page_total_width |total page width |float | |
||||page_total_height |total page height |float | |
||||scroll_width |Right margin scroll position |float | |
||||scroll_height |Lower boundary scroll position |float | |
||||page_title |page title |string | |
||||page_path |page path |string | |
||||page_host |page address domain name |string | |
||||referrer_page_host |Forward Domain Name |string | |
||||referrer_page_path |Forward Address |string | |
||||url |visit link |string | |
||bav2b_click |element click |page_key |page ID |string | |
||||is_html |HTML page |int | |
||||positions |element position |list | |
||||texts |element copy |list | |
||||element_width |element width |string | |
||||element_height |element height |string | |
||||touch_x |element left margin distance |int | |
||||touch_y |element right boundary distance |int | |
||||page_start_ms |page launch time |long | |
||||since_page_start_ms |Time from page launch |long | |
||||element_title |element text |string | |
||||page_title |page title |string | |
||||element_id |element name |string | |
||||element_class_name |element style name |string | |
||||element_type |element type |string | |
||||element_target_page |element link address |string | |
||||page_path |page path |string | |
||||page_host |page address domain name |string | |
|Mini Program |bav2b_page |page visit |title |Text |string |Value data\-title |
||||index |location |string |Value data\-index |
||bav2b_click |element click |title |Text |string |Value data\-title |
||||index |location |string |Value data\-index |
||||path |page path |string |Value the path of the corresponding page |
||||pagetitle |page name |string | |
||bav2b_longpress |element long press |title |Text |string |Value data\-title |
||||index |location |string |Value data\-index |
||||path |page path |string |Value the path of the corresponding page |
||||pagetitle |page name |string | |
||bav2b_change |Text selection |selecttext |text content |string | |
||||path |page path |string |Value the path of the corresponding page |
||||pagetitle |page name |string | |
||bav2b_confirm |content input |inputtext |input content |string | |
||||path |page path |string |Value the path of the corresponding page |
||||pagetitle |page name |string | |
