---
title: "How to calculate the value of each stage based on the page timing metrics"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/How_to_calculate_the_value_of_each_stage_based_on_the_page_timing_metrics"
---

Navigation Timing provides data that can be used to measure a website's performance. Unlike other JavaScript\-based mechanisms used for the same purpose, it can provide more useful and more accurate end\-to\-end latency data. You can measure data that was previously difficult to obtain, such as the time spent on the previous page before it is unloaded, the time spent on domain name resolution, the total time spent executing the [load (en-US)](https://developer.mozilla.org/en-US/docs/Web/API/Window/load_event) event handler, and more.

<span id="Navigation Timing"></span>
## Navigation Timing

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_28a157baf093d7ceaba68f9f0e839273) </span>

<span id=".5a2X5q616Kej6YeK"></span>
## Field explanations

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1222065a98945a671795d67ce8d9ddfe) </span>

<span id=".5Yid5aeL5YyW6Zi25q61"></span>
### The initialization phase


* navigationStart: The time when the user completes unloading the previous documentation.

* redirectStart: The start time of a page redirect, if a redirect occurs, or 0 otherwise.

* redirectEnd: If there are redirects, redirectEnd indicates the time when the response data from the server has been fully received after the final redirect. Otherwise, it is 0.


<span id=".6K-35rGC6Zi25q61"></span>
### The request phase


* fetchStart: When the browser initiates a resource request, if a cache is available, it returns the start time when the cache was read.

* domainLookupStart: The time when DNS lookup starts. If the request does not initiate a DNS request, such as keep\-alive, caching, and more, back the fetchStart time.

* domainLookupEnd: The time when DNS lookup ends. If no DNS request is initiated, such as keep\-alive or cache, the fetchStart time point is returned.

* connectStart: The time when the browser starts connecting to the server. If no connection is established, such as when the request uses keep\-alive, caching, and similar mechanisms, its value is equal to domainLookupEnd.

* secureConnectionStart: If the page uses HTTPS, its value is the moment before the secure connection handshake. If the property is unavailable, back undefined. If this property is available but HTTPS is not used, back 0.

* connectEnd: The moment when the browser has completed establishing a connection with the server. If no connection is established, for example, if the request uses keep\-alive, caching, and so on, its value is equal to domainLookupEnd.

* responseStart: Refers to the moment when the client receives the first byte of data in the response from the server, cache, or local resources.

* responseEnd: The moment when the client receives the last byte of data in the response from the server, cache, or local resource.


<span id=".6Kej5p6Q5riy5p-T6Zi25q61"></span>
### Analyze the rendering phase


* domLoading: The browser is about to begin parsing the first batch of HTML document bytes it has received.

* domInteractive: The time when the browser has finished parsing all HTML and the DOM has been constructed is the time when the DOM is ready.

* domContentLoaded: The time when the DOM is ready and no stylesheet is blocking JavaScript execution, allowing the rendering tree to be constructed. This generally refers to the time when [both the DOM and CSSOM are ready](https://docs.byteplus.com/en/docs/apmplus/How_to_calculate_the_value_of_each_stage_based_on_the_page_timing_metrics).

* domComplete: As the name suggests, this is the point in time when all processing is complete and all resources on the web page, such as images and so on, have been downloaded. In other words, the loading spinner has stopped spinning, indicating that the web page and all its sub\-resources are fully ready.

* loadEventStart: As the final step in loading each web page, the browser triggers the `onload` event to initiate additional application logic.

* loadEventEnd: The `onload` event has completed execution.

   Many JavaScript frameworks wait for the `onload` event to occur before executing their own logic. Therefore, the browser captures the `loadEventStart` and `loadEventEnd` timestamps to track the execution time.


<span id=".5ZCE6Zi25q616K6h566X5YWs5byP"></span>
## Formulas for each stage

After the explanations of each field above, the following formula can be clearly derived.


|Field |Formula |Calculation conditions |
|---|---|---|
|Redirect |redirectEnd \- redirectStart |redirectEnd is not zero and redirectStart is not zero |
|DNS |domainLookupEnd \- domainLookupStart |domainLookupEnd is not zero and domainLookupStart is not zero |
|TCP |connectEnd \- connectStart |connectEnd is not zero and connectStart is not zero |
|SSL |connectEnd \- secureConnectionStart |connectEnd is not zero and secureConnectionStart is not zero |
|Request |responseStart \- requestStart |responseStart is not zero and requestStart is not zero |
|Response |responseEnd \- responseStart |responseEnd is not zero and responseStart is not zero |
|Load |loadEventEnd \- navigationStart |loadEventEnd is not 0 and navigationStart is not 0<br><br>The total time for a page to fully load refers to the time from the start of the NavigationStart event to the end of the LoadEventEnd event. |
|DomReady |domContentLoaded \- fetchStart |domContentLoaded is not 0 and fetchStart is not 0 |
|DomParse |domInteractive\-responseEnd |domInteractive is not zero and responseEnd is not zero |
|Processing |domComplete \- domLoading |domComplete is not zero and domLoading is not zero |
|resourceLoad |loadEventStart\-domContentLoaded |loadEventStart is not zero and domContentLoaded is not zero |
|TTFB |responseStart \- navigationStart |\- |
|Time To First Byte |The total time from initiating a page request to receiving the first byte of response data, including DNS resolution time, TCP connection time, time to send the HTTP request, and time to receive the first byte of the response message. |responseStart is not 0 and navigationStart is not 0 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Other: Selecting navigationStart as the starting point is to ensure consistency with the web\-vitals specification.</div>


* <div data-tips="true" data-tips-type="tip">Link: https://github.com/GoogleChrome/web\-vitals/blob/main/src/getTTFB.ts</div>



<span id=".5Y-C6ICD6LWE5paZ"></span>
## References


* https://www.w3.org/TR/navigation\-timing/

* https://www.w3.org/TR/navigation\-timing\-2/

* https://developer.mozilla.org/zh\-CN/docs/Web/API/Navigation_timing_API
