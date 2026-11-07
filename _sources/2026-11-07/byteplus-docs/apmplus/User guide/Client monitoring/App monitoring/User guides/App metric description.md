---
title: "App metric description"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/App_metric_description"
---

This document introduces the metrics and their descriptions involved in APP Monitoring to help users better understand monitoring charts.

<span id="9ea7ed86"></span>
## Public description


* The speed of querying PV data depends on the selected dimensions.

* The results of querying PV or UV data are only affected by the specified dimensions.

* In the metric description, all filter criteria are specified dimensions.

* The defined dimensions are shown in the following table:

   
   |**Specify the dimensions** |**DescriptionS** |
   |---|---|
   |time |Includes aggregation time and time granularity.<br><br>Aggregation time includes:<br><br><br>* Five\-minute aggregations<br><br>* 1\-hour aggregation<br><br>* 1\-day aggregation<br><br><br>Time granularities include:<br><br><br>* Recent: 1 day or 7 days<br><br>* Range: Custom time range. |
   |System |App operating system.<br><br><br>* iOS<br><br>* Android |
   |OS version |The version of the App operating system. |
   |SDK version |SDK version. |
   |App version |App released versions. |
   |App name |App name |
   |App version code |App version code. |
   |download channel |The source of app package release. |
   |custom dimension |Custom dimension. |
   


<span id="zyGTAos7"></span>
## User analysis metrics


|Metric |Calculation method |
|---|---|
|PV |Number of app_launch event reports.<br><br><br>* For the iOS client, an app_launch event is reported for both Cold Start and Hot Start of the app.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">PV data for the iOS client is collected separately and is not equivalent to the data from startup analytic, which involves sampling.</div><br><br><br><br>* For the Android client, an app_launch event is reported in both of the following cases: when the SDK receives the first callback of the lifecycle method onResume after initialization, and when the lifecycle method onResume is called after the client returns to the Foreground from the Background, having been in the Background for 30 seconds. |
|UV |Number of device IDs after deduplication by PV |


<span id=".5bSp5rqD5YiG5p6Q5oyH5qCH"></span>
## Crash analytic metrics


|**Metric** |**Calculation method** |
|---|---|
|crash ratio |Number of crashes under filter conditions / total number of launches under filter conditions (PV) |
|crash Impacted users rate |Deduplicated UV count for crash errors under filter conditions / total deduplicated UV count under filter conditions |


<span id=".6ZSZ6K-v5YiG5p6Q5oyH5qCH"></span>
## Error analysis metrics


|**Metric** |**Calculation method** |
|---|---|
|error rate |Number of errors under filter conditions / total number of launches (PV) under filter conditions |
|error Impacted Users rate |Deduplicated UV count with errors under filter conditions / total deduplicated UV count under filter conditions |


<span id=".5Y2h6aG_5YiG5p6Q5oyH5qCH"></span>
## Lag analysis metrics


|**Metric** |**Calculation method** |
|---|---|
|lag ratio |Lag count under filter conditions / total launch count (PV) under filter conditions |
|lag impacted users rate |Number of deduplicated unique visitors experiencing lag under filter conditions / total number of deduplicated unique visitors under filter conditions |


<span id=".5YaF5a2Y5LyY5YyW5oyH5qCH"></span>
## Memory optimization metric


|**Metric** |**Calculation methods and description** |
|---|---|
|OOM count |Number of OOM occurrences under filter conditions (PV) |
|OOM ratio |OOM count under filter conditions / total launch count under filter conditions |
|impacted user |User count affected by OOM issues under filter conditions (UV) |
|impacted users rate |Number of deduplicated UVs with OOM error under filter conditions / total number of deduplicated UVs under filter conditions |


<span id=".SlPplJnor6_mjIfmoIc="></span>
## JavaScript error metrics


|**Metric** |**Calculation methods and descriptions** |
|---|---|
|error count |JavaScript error count under filter conditions |
|error rate |JavaScript error count under filter conditions / total webview count (PV) under filter conditions |


<span id=".6K-35rGC6ZSZ6K-v5oyH5qCH"></span>
## Request error metrics


|**Metric** |**Calculation methods and description** |
|---|---|
|request error |Request count with status code of 500 or higher under filter conditions |
|error rate |Request count with status code 500 or above under filter conditions / total request count under filter conditions |
|impacted user |Number of unique devices for requests with status code 500 or above under filter conditions |
|impacted users rate |Deduplicated device count of requests with status code 500 or above under filter conditions / total deduplicated device count of requests under filter conditions |


<span id=".6K-35rGC55uR5o6n5oyH5qCH"></span>
## Request monitoring metrics


|**Metric** |**Calculation method and description** |
|---|---|
|average time |Average time of requests with status codes below 500 under filter conditions |
|success rate |Number of requests with status code below 500 under filter conditions / total request count |
|slow query count |Number of requests that exceed the time threshold, after applying filter conditions and excluding error requests |
|slow query impacted user count |Under the filter criteria, after filtering out error requests, the deduplicated user count with request time exceeding the threshold |


<span id=".6aG16Z2i5Yqg6L295oyH5qCH"></span>
## Page loading metric


|**Metric** |**DescriptionS** |
|---|---|
|First Paint (FP) |First Paint is the time of the initial rendering. |
|First Contentful Paint (FCP) |First Contentful Paint is the time when content is first rendered. |
|First Meaningful Paint (FMP) |First Meaningful Paint, also known as the first meaningful paint time, is the time between when the user starts loading the page and when the first screen is rendered. |
|Interaction to Next Paint (INP) |Interaction to Next Paint monitors the delay between all user clicks, taps, and keyboard interactions with the webpage throughout the page lifecycle, and reports the longest delay. |
|Time to interactive (TTI) |Time to interactive records the time from when the page begins loading until it reaches a fully interactive status. |
|first load bounce rate |Bounce rate of users who leave before the first page is fully loaded. |
|slow launch ratio |Proportion of page views with complete load time over 5 seconds |


<span id=".55S16YeP5YiG5p6Q5oyH5qCH"></span>
## Battery analysis metric


|**Metric** |**Calculation method and description** |
|---|---|
|foreground current usage |The power value is a core metric for device power consumption, and is determined by voltage and current. In practice, voltage rarely changes, so current is a good metric for measuring power consumption. |
|battery temperature |Battery temperature indirectly reflects the device's power consumption. In general, devices with higher power consumption also have higher battery temperature. |
|traffic |Traffic usage |
|get location duration |Identify the monitored usage duration |
|AlarmManager set time |Number of times WakeUp\-type alarms are triggered |
|WakeLock Duration |The length of time that WakeLock is held, and the time interval between PowerManager's releaseWakeLock() and acquireWakeLock(). |
|Process Lifetime |The time period from process start until the process is killed |
|Exception count |Number of reported battery exceptions under filter conditions |
|Exception rate |Number of reported battery exceptions that occurred under filter conditions / total number of launches (PV) under the same conditions |
|Exception Impacted User count |Deduplicated device count for battery exception reports under filter conditions |
|Exception Impacted Users rate |Number of deduplicated devices reporting battery exceptions under filter conditions / total number of launches (UV) under filter conditions |


<span id=".Q1BV55uR5o6n5oyH5qCH"></span>
## CPU monitor metrics


|**Metric** |**Calculation method and description** |
|---|---|
|CPU utilization |Process CPU time / operating system CPU time |
|CPU utilization(max) |The maximum CPU utilization within the reporting period |
|CPU Usage Rate |Process CPU time/elapsed time |
|Maximum CPU Usage Rate |Maximum CPU usage rate within the reporting period |
|Thread CPU Usage |Thread CPU time/process CPU time |


<span id=".aU9T56OB55uY55uR5o6n"></span>
## iOS disk monitor


|**Metric** |**Calculation methods and description** |
|---|---|
|disk size |disk size |
|device free storage |Device free storage space |
|App Storage Usage |Total file size in the sandbox |
|App Storage Usage Percentage |App storage usage/phone storage |
|App Library and Document Storage Size |Total size of Library and Document files in the sandbox |


<span id=".QW5kcmlvZOejgeebmOebkeaOpw=="></span>
## Android disk monitor


|**Metric** |**Calculation method and description** |
|---|---|
|disk size |Mobile phone disk size.<br><br>Environment.*getDataDirectory*().getTotalSpace() + Environment.*getRootDirectory*().getTotalSpace() |
|device free storage |The size of the device free storage.<br><br>Environment.*getDataDirectory*().getFreeSpace() |
|App Storage Usage |Total size of files in the sandbox.<br><br>context.getFilesDir().getParent() + context.getExternalFilesDir(null).getParentFile() |
|App Storage Usage Percentage |App storage usage/phone storage |
|App Cache Storage |The disk space used by the cache in the sandbox.<br><br>context.getCacheDir() + context.getExternalCacheDir() |


<span id=".55uu5b2V5YiG5p6Q"></span>
## directory analytic


|**Metric** |**Calculation methods and description** |
|---|---|
|report volume |Catalog report count |
|path percentage |Current directory size/App storage usage |
|disk usage |Current directory size |
|reporting user |Directory user count |


<span id=".56OB55uY5byC5bi4"></span>
## disk anomaly


|**Metric** |**Calculation methods and description** |
|---|---|
|exception count |Exception reporting frequency under filter conditions |
|Exception rate |Number of exception reports under filter conditions / total page views under filter conditions |
|impacted user |Number of users reporting exceptions under filter conditions |
|impacted users rate |Exception reporting user under filter criteria / total UV under filter criteria |
