---
title: "Mini Pro metric descriptions"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Mini_Pro_indicator_instructions"
---

This document introduces the metrics and metric descriptions involved in Mini Pro Monitoring to help users better understand monitoring charts.

<span id="e65b63a1"></span>
## User analysis metrics


|**Metric** |**Calculation rules** |**DescriptionS** |
|---|---|---|
|PV(Page View) |Deduplicate reported pageviews based on view_id. |Page views. |
|UV(User View) |Deduplicate the reported pageviews by user_id. |Unique visitor count. |
|session count |Deduplicate reported pageviews based on session_id. |Number of user sessions (each session is counted from when the user enters the page until the page is closed). |
|page time on site |Subtract the timestamps of two pageviews with the same view_id |The duration from when a user enters a page to when they leave it. |
|average time on site |Page time on site / UV |Average time each user spends on the page. |


<span id="4e5381b5"></span>
## JavaScript monitoring metrics


|**Metric** |**Calculation rules** |
|---|---|
|JavaScript error |Total JavaScript errors. |
|impacted user |Total number of unique visitors who experienced JavaScript errors. |
|error rate |Number of page views with JavaScript errors / total number of page views. |
|affected user rate |Number of unique visitors with JavaScript error / total number of unique visitors. |


<span id="74be6e20"></span>
## Request monitoring metrics


|**Mini program type** |**Calculation rules** |
|---|---|
|WeChat Mini Program |Request time: responseEnd \- fetchStart. |
|TikTok Mini Program ||
|Alipay Mini Program |SDK Instrumentation Time.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Since Alipay and Baidu Mini Program cannot obtain fetchStart, the request time for these two types of mini programs is the SDK Instrumentation Time.</div><br> |
|Baidu Mini Program ||



|**Metric** |**Calculation rules** |
|---|---|
|request count |Total request count. |
|user count |Total number of unique users who initiated requests. |
|slow request count |The sum of the request count where the request time exceeds the set threshold. |
|slow request rate |slow request count / request count. |
|slow request affected user |Number of users who experienced slow requests. |
|slow request affected user rate |User count with slow requests / user count. |
|callback time |The sum of callback time for success, fail, and complete. |
|cancelled request count |Total number of cancellation requests. |
|successful request count |Total number of successful requests. |
|request error |Total number of failed requests. |
|request error affected user |Total number of unique users with failed requests |
|request error rate |Request error count / request count |
|request time |response_end\-fetch_start |
|SSL Handshake Time |connect_end\-secure_connection_start |
|received data size |Size of received request |
|transmitted data size |Request size. |


<span id="fa970b5a"></span>
## Performance monitoring metrics

<span id="5d812b97"></span>
### Startup performance metrics


|**Metric name** |**Calculation rules** |**DescriptionS** |**Compatibility overview** |
|---|---|---|---|
|total launch count |cold\-start count + warm start count |None |All |
|Cold Start |Pageview.source === launch count |None |All |
|Warm Start |Pageview.source === showCount |None |All |
|first screen cold start total time |pageRenderEnd \- App.trigger |The total load time from when your user clicks the mini program until the first screen is rendered includes code package download (not included for subsequent launches), code execution, and first screen rendering. |* WeChat Mini Program<br><br>* TikTok Mini Program |
|Mini Program Initialization Time |appInitEnd \- App.trigger |From the moment your user clicks the mini program to the completion of Cold Start. |* WeChat Mini Program<br><br>* TikTok Mini Program |
|download time |WeChat Mini Program: performance.downloadPackage<br><br>TikTok Mini Program: performance.miniprogram\-package |Code package download time, the download time for the mini program package when your users start for the first time. |* WeChat Mini Program<br><br>* TikTok Mini Program |
|JS injection time |performance.evaluateScript |Time consumed by JS code injection and time consumed by injecting JS files during the start process. |* WeChat Mini Program |
|first screen load time |pageLoadStart \- appInitEnd |None |All |
|first screen build time |pageDomEnd \- pageLoadStart |None |All |
|first screen render time |pageRenderEnd \- pageDomEnd |None |All |
|first screen total load time |pageRenderEnd \- appInitEnd |None |All |
|open rate |pageRenderEnd count / appInitEnd count |The completion rate of your users who start the mini program and reach first screen rendering. |All |
|churn rate |1 \- Open rate |The probability that your users start the mini program but exit before the first screen finishes rendering. |All |
|slow start count |first screen cold start total time \> cold\-start count exceeding the set threshold |Number of slow start occurrences. |All |
|slow start rate |slow start count / cold\-start count for which start performance data has been reported |The slow start ratio. |All |


<span id="cf5d6eef"></span>
### Page performance metrics


|**Metric name** |**Calculation rules** |**Compatibility information** |
|---|---|---|
|total page navigation time |renderEnd \- navigateStart |All |
|route change time |loadStart \- navigateStart |All |
|page build time |domEnd \- loadStart |All |
|page render time |renderEnd \- domEnd |All |
|First render (FR) |performance.FR.duration |* WeChat Mini Program |
|First paint (FP) |FP.startTime \- loadStart |* WeChat Mini Program<br><br>   * [iOS is not supported](https://developers.weixin.qq.com/miniprogram/dev/api/base/performance/PerformanceEntry.html#.On46dGV4dD3ohJrmnKwtLHN0cmluZyBuYW1lLC3mjIfmoIflkI3np7A=)<br><br>* TikTok Mini Program |
|First Contentful Paint (FCP) |FCP.startTime \- loadStart |* WeChat Mini Program<br><br>   * [Versions below iOS 14.5 are not supported.](https://developers.weixin.qq.com/miniprogram/dev/api/base/performance/PerformanceEntry.html#.On46dGV4dD3ohJrmnKwtLHN0cmluZyBuYW1lLC3mjIfmoIflkI3np7A=) |
|Largest Contentful Paint (LCP) |LCP.startTime \- loadStart |* WeChat Mini Program<br><br>   * [Not supported on iOS](https://developers.weixin.qq.com/miniprogram/dev/api/base/performance/PerformanceEntry.html#.On46dGV4dD3ohJrmnKwtLHN0cmluZyBuYW1lLC3mjIfmoIflkI3np7A=) |
|page render bounce rate |renderEnd count / navigateStart count != 0 |All |
|slow page count |Number of instances where total page navigation time exceeds the set threshold |All |
|slow page rate |slow page count/total page request count |All |


<span id="c4f09426"></span>
### Runtime performance metrics


|**Metric** |**Calculation rules** |**DescriptionS** |
|---|---|---|
|setData Call Count |Number of reports within the time range |None |
|setData Time |Total setData time divided by number of page views |Represents the average cumulative time spent on setData for each page view. |
|setData Frequency (per second) |SetData call count / Time range (unit: s) |None |
|setData Size |setData total size / number of PVs |Represents the average cumulative size of setData per page view. |


<span id="b1f1a9e9"></span>
### Performance of interface requests

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4c451b2749dfcef13dd4b264b681c349.png) </span>

Metric description:


|**Metric** |**Calculation rules** |**DescriptionS** |**Compatibility overview** |
|---|---|---|---|
|redirect time |redirectEnd \- redirectStart |If no redirection occurs, or if any of the redirections is cross\-origin, the value is 0. |WeChat Mini Program |
|Cache Time |domainLookupStart \- fetchStart |Cache. |WeChat Mini Program |
|DNS Resolution Time |domainLookupEnd \- domainLookupStart |Domain name resolution time. During parsing, the cache is 0. |WeChat Mini Program |
|TCP Connection Time |connectEnd \- connectStart |The TCP connection duration. |WeChat Mini Program |
|Request duration |responseStart \- requestStart |Time taken from when a request is sent from the client to when the first response is received from the server side, after the SSL link has been established. |WeChat Mini Program |
|Response time |responseEnd \- responseStart |The time elapsed from the server side's initial response to the completion of the data response. |WeChat Mini Program |


<span id="f0a4766a"></span>
## custom log


|**Metric** |**Calculation rules** |
|---|---|
|sample size |Total number of custom reports. |
