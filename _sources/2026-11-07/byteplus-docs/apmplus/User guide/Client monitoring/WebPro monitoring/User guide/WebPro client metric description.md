---
title: "WebPro client metric description"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/WebPro_client_metric_description"
---

This article introduces the metrics and metric descriptions involved in monitoring on the Webpro interface to help users better understand monitoring charts.

<span id=".55So5oi35YiG5p6Q5oyH5qCH"></span>
## User analysis metrics


|**Metric** |**DescriptionS** |
|---|---|
|PV |Page View, number of page views. Reported pageviews are deduplicated based on view_id. |
|UV |User View, number of user visits. Deduplicate reported pageviews by user_id. |
|Session |The number of user session accesses is counted from entering the page to turning off the page as one session. Deduplicate reported pageviews based on session_id. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">In an SPA, a view is reported when a route change is detected, while in an MPA, each page corresponds to a view.</div>


* <div data-tips="true" data-tips-type="tip">In an SPA application, a Session generates a session_id only during initialization, and this session_id remains valid until the user leaves the page. If session_id is not manually specified for multiple pages, a new session_id will be generated each time initialization occurs, and each page will be treated as a separate session.</div>


* <div data-tips="true" data-tips-type="tip">The performance monitor for single\-page applications provides the SPA_LOAD load time metric, which is calculated based on route changes.</div>



<span id="bd1de422"></span>
## JavaScript error metrics


|**Metric** |**DescriptionS** |
|---|---|
|error count |Number of JavaScript error occurrences |
|error rate |Page views with JavaScript error / total page views |
|impacted user |Number of unique visitors with a JavaScript error |
|affected user rate |UVs with JavaScript error / total UVs |


<span id="f3c56d4e"></span>
## request overview


|**Metric** |**DescriptionS** |
|---|---|
|request count |Request count |
|user count |Unique visitors for requests |
|slow request count |Number of requests exceeding the slow request threshold |
|slow request rate |Slow request count/total reported request count |
|slow request affected user |Unique visitors with slow requests |
|slow request affected user rate |Slow request affected user count per total request count per unique visitor |
|error count |Request count with status code greater than or equal to 400 |
|error rate |Error count/request count (status code != 0) |
|impacted user |Unique visitors with request errors |
|affected user rate |The total reporting volume for impacted user count and request count is deduplicated by user_id. |
|request time |timing.duration != 0。 Obtain the duration from the browser's resource timing records using performance.getEntriesByName(url). This is the actual elapsed time. |
|SDK Instrumentation Time |The SDK reports two timing metrics: one is the request time, and the other is the Request Tracking Time. The Request Tracking Time is obtained by the SDK marking the start and end of a request and calculating the duration between these points.<br><br>This time measurement tends to be longer than the request time in most cases because it includes the time spent in the browser event loop. Under exceptional circumstances, there are cases where the logging time is less than the request time, because some requests have very long response times and the logging mechanism can only determine the timing of responseStart. Therefore, the end is marked at responseStart rather than at responseEnd. |


<span id="5a68457b"></span>
## Request metrics


|**Metric** |**DescriptionS** |
|---|---|
|successful request count |status code < 400 && status code != 0 |
|Request success rate |successful request count / request count (status code != 0) |
|cancelled request count |Request count (status code = 0) |
|request error |status code \>= 400 |
|request error rate |request error / request count (status code != 0) |
|request error affected user |Number of UVs with request errors |
|Redirect Time |redirectEnd \- redirectStart。<br><br>If no redirect occurs, or if any of the redirects is cross\-origin, the value is 0. |
|Cache Time |domainLookupStart \- fetchStart |
|DNS Resolution Time |domainLookupEnd \- domainLookupStart。<br><br>Domain name resolution time is zero when the resolution cache is hit. |
|TCP Connection Time |connectEnd \- connectStart。<br><br>The TCP connection duration. |
|SSL Handshake Time |connectEnd \- secureConnectionStart。<br><br>SSL security connection duration |
|Request Send Time |responseStart \- requestStart。<br><br>After the SSL link is established, the time taken from when the client sends a request to when the server side provides the first response. |
|Response Time |responseEnd \- responseStart。<br><br>Elapsed time from the server side's initial response until all data has been sent. |


<span id="54ae29f4"></span>
## resources monitor


|**Metric** |**DescriptionS** |
|---|---|
|load count |Number of static resources loaded |
|user count |Unique visitors who loaded static resources |
|slow load count |Load count exceeding the slow load threshold |
|slow load rate |Slow load count/total report count |
|slow resource affected user |User count exceeding the slow load threshold |
|slow resource affected user rate |Slow resource affected user count / total UV |
|error count |Number of reported errors in static resources. Static resource errors collected using window.addEventListener |
|error rate |Static resource error PVs / total PV |
|impacted user |Unique visitors for static resources with reported errors |
|affected user rate |UVs experiencing static resource errors / total UVs |
|Redirect Time |redirectEnd \- redirectStart |
|Cache Time |domainLookupStart \- fetchStart |
|DNS Resolution Time |domainLookupEnd \- domainLookupStart |
|TCP Connection Time |connectEnd \- connectStart |
|SSL Handshake Time |connectEnd \- secureConnectionStart |
|Request Send Time |responseStart \- requestStart |
|Response Time |responseEnd \- responseStart |
|static resource cache hit rate |transferSize = 0 |


<span id="037f640b"></span>
## performance monitor

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_6f529d3a0675dbeec1aa1fc6d16b25de) </span>


|**Metric** |**DescriptionS** |
|---|---|
|FP |FP (First Paint) refers to the moment when the page is rendered for the first time. In performance metrics, the period from when a user begins to access a web page to the FP time point is considered blank screen time. In other words, during the process of accessing a web page, before the FP time point, the user only sees a white screen with no content, and cannot perceive any meaningful activity taking place. |
|FCP |FCP (First Contentful Paint) refers to the time point when content is first rendered. In performance metrics, the period from when a user begins to access a Web page until the FCP time point can be considered a time with none content. In other words, before the FCP time point during the user's visit to a Web page, the user only sees a screen without any actual content and cannot obtain any useful information during this stage. |
|LCP |LCP (Largest Contentful Paint) is a Core Web Vitals metric that measures when the largest content element in the viewport becomes visible. It can be used to confirm when the main content of the page has finished rendering on the screen. |
|FMP |FMP (First Meaningful Paint) refers to the time when meaningful content is first rendered. This occurs when the overall page layout and all text content have been fully rendered, at which point the first meaningful paint is considered complete. The new version is gradually being deprecated. |
|INP |INP (Interaction to Next Paint), that is, the interaction to next paint, is used to measure user interface responsiveness by observing the delay time of all clicks, taps, and keyboard interactions performed by the user on the web page throughout the page lifecycle, and reports the longest duration. |
|CLS |CLS (Cumulative Layout Shift) is a metric that measures the largest layout shift score caused by any unexpected layout change occurring throughout the entire lifecycle of a page. |
|LOAD |LOAD reflects the time when the page and all its dependent resources have finished loading. In the server side routing scenario, the LOAD metric corresponds to the time when the page load event occurs. According to the page load phase model defined by Navigation Timing 2.0, in synchronous navigation scenarios, the calculation method for LOAD is: LOAD = loadEventStart \- fetchStart. |
|TTI |TTI (Time to Interactive) is a non\-standardized web performance metric that represents the point in time when the last long task completes, immediately followed by five seconds during which both the network and the main thread remain idle. |
|TTFB |TTFB (Time To First Byte) is the time from sending a page request to receiving the first byte of response data. |
|DomReady |domContentLoadedEventEnd \- fetchStart<br><br>Time taken to complete all synchronization scripts |
|DOM Parsing |domInteractive \- responseEnd<br><br>Time from the end of the request response to DOM interactivity |
|Processing |domComplete \- domLoading<br><br>DOM parsing duration from start to finish |
|ResourceLoad |loadEventStart \- domContentLoadedEventEnd<br><br>Resource loading time after DOM parsing |
|Redirect |redirectEnd \- redirectStart<br><br>If no redirect occurs, or if any of the redirects is cross\-origin, this value is 0. |
|DNS |domainLookupEnd \- domainLookupStart<br><br>Domain name resolution time (is 0 if the resolution cache is hit) |
|TCP |connectEnd \- connectStart<br><br>Tcp connection time |
|SSL |connectEnd \- secureConnectionStart<br><br>SSL security connection time |
|Request |responseStart \- requestStart<br><br>The time taken for the server side to send the first response to the client after the SSL connection is established. |
|Response |responseEnd \- responseStart<br><br>The time taken from the server side's first response to the completion of the data response |
|longtask count |Number of longtasks divided by number of pageviews, representing the average number of longtasks per pageview. |
|longtask time |Longtask total time divided by the number of pageviews represents the average cumulative longtask duration per pageview. |


<span id="52ff4eb2"></span>
## Performance metric: Bounce Rate


|**Metric** |**DescriptionS** |
|---|---|
|FP Bounce Rate |Number of sessions that exited the page before FP reporting / total number of sessions |
|FCP Bounce Rate |Number of sessions that exited the page before FCP is reported / total number of sessions |
|LCP Bounce Rate |Number of sessions that exited the page before LCP reporting / total number of sessions |
|Load Bounce Rate |Number of sessions that exit the page before the Load event is reported divided by the total number of sessions |


<span id="92d045c2"></span>
## Blank screen metric


|**Metric** |**DescriptionS** |
|---|---|
|blank screen count |The number of blank screen occurrences |
|blank screen affected user |Number of unique visitors with blank screen |


<span id="7e8cf93b"></span>
## custom log


|**Metric** |**DescriptionS** |
|---|---|
|sample size |Total number of custom reports |
