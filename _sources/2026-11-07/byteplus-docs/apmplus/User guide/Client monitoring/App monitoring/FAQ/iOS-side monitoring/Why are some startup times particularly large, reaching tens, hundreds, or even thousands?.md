---
title: "Why are some startup times particularly large, reaching tens, hundreds, or even thousands?"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Why_are_some_startup_times_particularly_large_reaching_tens_hundreds_or_even_thousands"
---

1. These data are real data collected by APMInsight; however, they do not conform to the usage patterns of most users and are considered abnormal data. Such data have little significance for problem analysis or troubleshooting and represent a form of "pollution" in dashboard data. You can configure the custom settings to filter out these data:

2. Why is this kind of data generated?

   Startup monitoring tracks data from the following stages of app startup:

   If the user switches the APP to the background before completing these four stages and then reopens the APP after a long period of time, there are two possible scenarios: If the iPhone terminates the APP process, the next time the user opens the APP, it will start anew. The previous incomplete startup will no longer exist, and APMInsight will also not report the previous startup. If the iPhone does not terminate the process, the APP will resume the previous incomplete startup. Once the startup completes, APMInsight will report the duration of this startup, which will result in an unusually long startup time.

3. How can you determine whether an abnormal start data point is caused by the reasons mentioned above? User behavior can be determined by analyzing it in combination with other types of logs.

   On the abnormal statistics and tracking page, locate an abnormal start entry and copy the DeviceID.

   When performing single\-point tracing, search for the user's logs by DeviceID. Use the original information from the start logs to obtain two timestamps. APMInsight calculates the app start time based on these two timestamps. Then, check whether there is an extended period between these two timestamps during which no other logs are generated.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/66f38dffcbe144ea95e787411a80b4c9) </span>

   As shown in the figure below, there are several network logs at 7:38, and no further logs are generated afterward. 7:38 is the first timestamp recorded in the start logs. No new logs appear until 17:46, which is the last timestamp recorded in the start logs. As a result, the calculated start time will be extremely large.
