---
title: "How to calculate the TTI metric"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/How_to_calculate_the_TTI_metric"
---

Time to Interactive (TTI) is an important [laboratory metric](https://web.dev/user-centric-performance-metrics/#in-the-lab) for measuring [loading responsiveness](https://web.dev/user-centric-performance-metrics/#types-of-metrics). This metric helps identify pages that *appear* to be interactive but actually are not. A fast TTI helps ensure the [effectiveness](https://web.dev/user-centric-performance-metrics/#questions) of the page.

<span id=".5LuA5LmI5pivIFRUSSDmjIfmoIc="></span>
## What is the TTI metric

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_bf1f73dc0b8a1771ebf0afb7bf6855db) </span>

TTI (Time To Interactive) refers to the time from when a page begins loading until it reaches a fully interactive status. When the page is in a fully interactive status, the following three conditions must be met:


1. The page already displays useful content.

2. The event handler functions associated with visible elements on the page have been registered.

3. Event response functions can begin execution within 50 ms after the event occurs.


In many cases, developers tend to focus only on metrics related to page rendering, such as FP, FCP, and more, while overlooking metrics related to page usability. TTI is an important metric that reflects page usability. The smaller the TTI value, the earlier users can interact with the page, resulting in a better user experience.

<span id=".5bmz5Y-w5aaC5L2V5raI6LS5IFRUSQ=="></span>
## How platforms consume TTI

<span id=".56uZ54K55oCn6IO95oC76KeI"></span>
### site performance overview

In the PID aggregation module of the site performance overview, you can view the overall TTI compliance rate for pages, and also display the pages with the lowest TTI compliance rates ranked by performance.

In the metric overview module of the site performance overview, you can view the TTI status and trends for the entire site.

<span id=".6aG16Z2i6K-m5oOF"></span>
### Page details

After clicking a single pid link in the site performance overview and entering the page details, you can also observe the TTI status for the individual page.

<span id=".6aG16Z2i5YiX6KGo"></span>
### page list

In the overview table of the page list, after selecting the desired experience metrics in the custom columns, you can view the metrics from the perspective of the page.

<span id=".5pWw5o2u5o6i57Si"></span>
### data explore

In data explore, after you check the TTI metric in the custom columns of the Views module, you can view the TTI metric for each page visit.

<span id=".5pWw5o2u5YiG5p6Q"></span>
### data analytic

On the data analytic page, you can filter by the TTI dimension and freely combine it with other metrics to generate charts for analysis. After configuration is complete, you can add these charts to the dashboard.

<span id=".55uR5o6n5oql6K2m"></span>
### Monitoring and alerts

When configuring alerts for the TTI metric in the Monitoring alert module, the [recommended time](https://web.dev/tti/#tti-3) provided by web.dev is 5 seconds. You can adjust this value accordingly based on your site's unique characteristics.

<span id=".5aaC5L2V6I635Y-WIFRUSSDmjIfmoIc="></span>
## How to obtain the TTI metric

When users access Web pages, there are usually two modes:


* Synchronous navigation scenarios via direct server\-side route switching

* SPA page switching scenarios via client routing


<span id=".566X5rOV5o-P6L-w"></span>
### Algorithm description

Long Task: A task whose execution time on the browser main thread exceeds 50 ms.

Silent window period: During the time corresponding to the window, there is no Long Task, and the request count of ongoing network requests does not exceed two.

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_b10594201c466064aba4c97f0562ed68) </span>

Refer to the diagram above (where 'First Consistently Interactive' in the figure represents TTI).


1. Starting from the time of the initial point (usually FCP or FMP), search forward for a silent window of at least 5 seconds. Silent window period: During the time corresponding to the window, there are no Long Tasks, and the number of ongoing network requests does not exceed two.

2. After identifying the quiet window period, search forward from this period to locate the nearest Long Task. The end time of that Long Task is the TTI.

3. If no Long Task is found, use the start point time as TTI.

4. If the TTI obtained in Step 2 or Step 3 is less than DOMContentLoadedEventEnd, use DOMContentLoadedEventEnd as the TTI.


<span id=".5rWP6KeI5Zmo5YW85a655oCn6K-05piO"></span>
### Browser compatibility description

The TTI metric requires the browser to support [Long Tasks API](https://www.w3.org/TR/2017/WD-longtasks-1-20170907/) and [Resource Timing API](https://www.w3.org/TR/resource-timing-2/). If the browser is not compatible, the reported metric will have isSupport set to false.

<span id=".5aaC5L2V5LyY5YyWIFRUSSDmjIfmoIc="></span>
## How to optimize the TTI metric

To learn how to improve the TTI of a specific website, you can run a Lighthouse performance audit and pay close attention to the various specific [opportunities](https://web.dev/lighthouse-performance/#opportunities) suggested by the audit.

To learn about common methods for improving TTI for any website, refer to the following performance guide:


* [Optimize: Reduce the size of JavaScript](https://web.dev/unminified-javascript/)

* [Optimize: Pre-connect to required sources](https://web.dev/uses-rel-preconnect)

* [Optimize: Preload critical requests](https://web.dev/uses-rel-preload/)

* [Optimize: Reduce the impact of third-party code](https://web.dev/third-party-summary/)

* [Optimize: Minimize critical request depth](https://web.dev/critical-request-chains/)

* [Optimize: Reduce JavaScript execution time](https://web.dev/bootup-time/)

* [Optimize: Minimize main thread work](https://web.dev/mainthread-work-breakdown/)

* [Optimize: Maintain a low request count and small transfer size](https://web.dev/resource-summary/)


<span id=".5Y-C6ICD6LWE5paZ"></span>
## References


* https://docs.google.com/document/d/1GGiI9\-7KeY3TPqS3YT271upUVimo\-XiL5mwWorDUD4c

* https://web.dev/tti
