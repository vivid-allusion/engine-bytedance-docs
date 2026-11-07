---
title: "What is the purpose of the maximum start duration during start analysis?"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/What_is_the_purpose_of_the_maximum_start_duration_during_start_analysis"
---

The activity onResume indicates that the start is complete. Setting a maximum start duration helps prevent dirty data in case of exceptions and serves as a fallback policy. If most of the large data is essentially dirty data, you can avoid this by setting the start time in the platform settings; a common value is 20 seconds.

If the startup duration exceeds the upper limit set in the settings, the data cannot be queried, but it is not lost. You can disable the startup duration limit in the settings, and then check the Slow Start section to find the data.
