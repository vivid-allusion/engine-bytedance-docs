---
title: "Event usage"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Event_usage_app"
---

Event usage is closely related to billing. You can regularly view event usage in App Monitoring and make adjustments based on your actual business scenarios.

<span id="5aa9a7e1"></span>
## View event usage in the console


1. Log in to the [Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client/console/overview).

2. Click the target application name to enter the application service management page.

3. Under **App Monitoring**, click **usage details**.

4. In **Usage trends**, view event usage for the App.

   Usage trend page supports filtering event usage by operating system and time.

5. (Optional) If you want to adjust the event usage for a specific data category in usage trends, please adjust the sampling rate in the SDK setting according to the table below.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Page view is the app's PV metric and is required for calculating crash ratio, lag ratio, and other metrics. The sampling rate for this metric cannot be turned off or reduced.   </div>
   

   
   |**Usage trends**<br><br>**Event name** |**SDK setting configuration modification path** |**Android projects** |**iOS project** |**The Harmony project** |**Affected feature modules** |
   |---|---|---|---|---|---|
   |application exit |application exit |The application exit sampling rate |\- |\- |application exit |
   |CPU metrics |CPU monitor |Sampling rate for CPU metric reporting |CPU metric sampling rate |\- |CPU metric |
   |CPU exception ||Sampling rate for reporting CPU anomaly data |CPU anomaly sampling rate |\- |CPU anomaly |
   |Thread CPU metric ||The thread CPU usage exception threshold |CPU threshold for thread stack trace capture |\- |CPU metric |
   |Memory metric |memory optimization |Memory metric sampling rate |Memory metric sampling rate |\- |OOM trend \> Extended metric |
   |custom file |crash analytic |Upload a custom log? |Upload a custom log? |Upload custom log? |Crash details \> Custom log |
   ||custom log |Actively report custom log sampling rate |Proactively report custom log sampling rate |\- |custom log |
   |crash |crash analytic |Sampling not supported |Sampling not supported |Sampling not supported |\- |
   |lag |lag analytic |Lag sampling rate |Lag sampling rate |\- |lag trend |
   |traffic metric |traffic monitor |Sampling rate for traffic metric monitoring |Sampling rate for traffic metric monitoring |\- |traffic metric |
   |traffic anomaly ||Traffic anomaly monitoring sampling rate |Traffic anomaly monitoring sampling rate |\- |traffic anomaly |
   |start |user experience |* Startup sampling rate<br><br>* Does an app update count as a first launch |* Startup sampling rate<br><br>* Does an app update count as the first launch |Startup sampling rate |startup analytic |
   |Frame rate ||Page sampling rate |Page sampling rate |\- |Native page experience |
   |Frame rate drop ||||||
   |Page load ||||||
   |Hybrid performance |Page analysis |The web_view sampling rate |Web_view sampling rate |\- |H5 monitor |
   |hybird page view ||||||
   |Hybrid JS error ||||||
   |hybrid ajax ||||||
   |Battery metrics summary |battery analytic |Overall battery sampling rate |\- |\- |Power consumption factors |
   |Power consumption tracking ||Sampling rate for battery exception attribution reporting |\- |\- |Battery error |
   |Power consumption scenario metric ||Overall battery sampling rate |\- |\- |battery metric |
   |custom error |error analytic |Custom error sampling rate |Custom error sampling rate |Custom error sampling rate |custom error |
   |Android object |memory optimization |The OOM analysis sampling rate |\- |\- |Single device memory detail, leak analysis, and large objects |
   |Android memory files ||OOM analysis sampling rate |\- |\- ||
   |iOS memory files |memory optimization |\- |The OOM analysis sampling rate |\- ||
   |iOS objects ||\- ||\- ||
   |disk metrics |disk monitor |Disk metrics sampling rate |Disk metrics sampling rate |\- |disk metrics |
   |directory analytic ||Disk metrics sampling rate |Disk metrics sampling rate |\- |directory analytic |
   |Exception folder ||Disk threshold for exception folder |Exception folder disk thresholds<br><br>Exception folder count threshold |\- |disk anomaly |
   |Exception files ||Maximum number of exception files reported |Maximum number of exception files that can be reported |\- ||
   |Expired files ||Expired file threshold |Expired file threshold |\- ||
   |App events |Event management |Event reporting sampling rate |Event reporting sampling rate |Event reporting sampling rate |event trend |
   |Http network |network analytic |Network sampling rate |Network sampling rate |Network sampling rate |HTTP |
   |crash protection |crash protection |\- |Crash protection sampling rate |\- |crash protection |
   |MetricKit |MetricKit |\- |MetricKit sampling rate |\- |stability |
   


<span id="a5deed9e"></span>
## View event usage

Supports obtaining usage trends via OpenAPI and performing alert monitoring independently. For details, refer to [GetAidQuotaUsedTrend](https://docs.byteplus.com/en/docs/apmplus/GetAidQuotaUsedTrend).
