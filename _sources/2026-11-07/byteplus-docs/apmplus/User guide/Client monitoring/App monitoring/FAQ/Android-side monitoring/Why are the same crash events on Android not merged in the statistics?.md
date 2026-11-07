---
title: "Why are the same crash events on Android not merged in the statistics?"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Why_are_the_same_crash_events_on_Android_not_merged_in_the_statistics"
---

**Problem descriptions**

The same crash on Android was not aggregated in the statistics; for the differences, refer to the screenshot.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_c41b080c5e237d3c2ffc3044435a0ae1.png) </span>

**Description of the cause**

The difference between the two crashes is that one includes description information and the other does not. When the Android system throws an exception because a binder call fails for the first time, it includes information such as description information. In addition to the description information found in the link, there is other information as well. It is also meaningful to categorize the exceptions based on the information they contain, so they were not counted together in the statistics.
