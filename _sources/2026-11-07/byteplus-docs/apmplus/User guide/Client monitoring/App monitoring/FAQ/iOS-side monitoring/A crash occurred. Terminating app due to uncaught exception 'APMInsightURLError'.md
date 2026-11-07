---
title: "A crash occurred. Terminating app due to uncaught exception 'APMInsightURLError'."
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/A_crash_occurred_Terminating_app_due_to_uncaught_exception_APMInsightURLError"
---

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/97863e82f09943fd962940a3055c2577) </span>

The solution: Import the CN sub\-library.

```Plain Text
  pod 'RangersAPM', '>=2.1.0', :subspecs => [
      'Crash',
      'WatchDog',
      'OOM',
      'LAG',
      'UserException',
      'Monitors',
      'UITrackers',
      'Hybrid',
      'MemoryGraph',
      'Network',
      'EventMonitor',
      'CN'
  ]
```
