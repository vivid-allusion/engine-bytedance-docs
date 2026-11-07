---
title: "How to calculate FP and FCP metrics"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/How_to_calculate_FP_and_FCP_metrics"
---

<span id=".5oyH5qCH6Kej6YeK"></span>
## Metric explanation

<span id="FP (First Paint)"></span>
### FP (First Paint)


* The time of first render. In performance metrics, the period from when the user begins to access the web page to the FP time point can be considered blank screen time. That is, during the process of accessing a web page, before the FP time point, the user only sees a white screen with no content, and cannot perceive any meaningful activity taking place at this stage.

* Therefore, blank screen time usually reflects the page's blank screen time, which in turn indicates the network loading performance of the current web page. When loading performance is excellent, the blank screen time becomes shorter, users spend less time waiting for content, and the likelihood of user loss decreases.


<span id="FCP (First Contentful Paint)"></span>
### FCP (First Contentful Paint)


* The time point when content is first rendered. In performance metric analysis, the period from when the user begins to access the web page to the FCP time point can be considered none content time. That is, during the process of accessing the web page, before the FCP time point, the user only sees a screen without any actual content and cannot obtain any useful information at this stage.

* Therefore, this metric typically reflects the time when content first appears on the page. The time to first content appearance indicates the current Web page’s network loading performance, the complexity of the page’s DOM structure, and the efficiency of inline script execution. When performance at all stages is optimized, the time to first content appearance will be shorter, users will wait less, and the probability of user loss will decrease.

* The First Contentful Paint (FCP) metric measures the time from when a page begins loading until any part of the page content is rendered on the screen. For this metric, "content" refers to text, images (including background images), `<svg>` elements, or non\-white `<canvas>` elements.


The main difference between the FP and FCP metrics is:


* FP refers to the moment when the browser begins to render content on the screen. As soon as any visual change occurs—regardless of what triggers it—this point in time is called FP.

* FCP refers to the browser's first rendering of content from the DOM. For example: text, picture, SVG, canvas elements, and more. This time point is called FCP.


<span id=".5oCO5qC3566X5piv6Imv5aW955qEIEZDUCDliIbmlbDvvJ8="></span>
## What is considered a good FCP score?

To provide a good user experience, the website should strive to keep the first contentful paint within 1.8 seconds. To ensure that you can achieve the recommended target value for the majority of user visits, a good measurement threshold is the 75th percentile of page load times, which applies to both mobile and desktop devices.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The 75th percentile here means that, assuming the good threshold for FCP is 1.8 seconds, the goal is for 75 percent of pages (by page count) to have a load time within this threshold, that is, to complete First Contentful Paint in 1.8 seconds or less.</div>


<span id=".5bmz5Y-w5aaC5L2V5raI6LS5IEZQ44CBRkNQ"></span>
## How to consume FP and FCP on the platform

<span id=".56uZ54K55oCn6IO95oC76KeI"></span>
### site performance overview

In the PID aggregation module of the site performance overview, you can view the overall FCP compliance rate for pages, and you can also display the pages with the worst FCP compliance rate in ranked order.

In the metric overview module of the site performance overview, you can see the FCP status and trends for the entire site.

<span id=".6aG16Z2i6K-m5oOF"></span>
### Page details

From the site performance overview, click on a pid link to view the page details. You can then observe the FCP metrics for the individual page.

<span id=".6aG16Z2i5YiX6KGo"></span>
### page list

In the overview table of the page list, after you check the desired experience metrics in the custom columns, you can observe each metric from the perspective of the page.

<span id=".5pWw5o2u5o6i57Si"></span>
### data explore

During data exploration, you can view the FP and FCP metrics for each page visit in the Views module.

<span id=".5pWw5o2u5YiG5p6Q"></span>
### data analytic

On the data analytic page, you can add FP and FCP, and combine them with other metrics to generate charts for analysis. Once configuration is complete, you can add them to the dashboard.

<span id=".55uR5o6n5oql6K2m"></span>
### Monitoring alerts

You can configure alerts for FP and FCP metrics in the Monitoring alert module. The [recommended time](https://web.dev/fcp/#fcp-2) for FCP provided by web.dev is 1.8 seconds. You can adjust this as appropriate based on your site's own characteristics.

<span id=".5aaC5L2V6I635Y-W5oyH5qCH"></span>
## Obtain a metric

According to the description in the [W3C Paint Timing specification draft](https://w3c.github.io/paint-timing/#sec-PerformancePaintTiming), PerformancePaintTiming contains paint performance measurement data for the current web page, which can be obtained using the `*performance.getEntriesByType('paint')*` method. FP and FCP are included in this data.


* Locate the object with the name 'first\-paint'; its description contains the FP metric data, where startTime is the FP time.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_41418be36bef412e1d40d1ba4a040bff) </span>

* Locate the object with the name 'first\-contentful\-paint'; its description contains the FCP metric data, where startTime is the FCP time.

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_825c3b98aa36e5d2b03c82527ac6d09b) </span>


<span id=".5rWP6KeI5Zmo5YW85a655oCn6K-05piO"></span>
## Browser compatibility description

The metric requires the browser to support [Paint Timing API](https://docs.byteplus.com/en/docs/apmplus/How_to_calculate_FP_and_FCP_metrics). If the browser is not compatible, isSupport in the reported metric will be false.

<span id=".5aaC5L2V5LyY5YyWRlAgJiYgRkNQ5oyH5qCH"></span>
## How to optimize FP and FCP metrics


* [Optimize: Eliminate blocking resources](https://web.dev/render-blocking-resources/)

* [Minimize CSS](https://web.dev/minify-css/)

* [Optimize: remove unused CSS](https://web.dev/unused-css-rules/)

* [Optimize: Pre-connect to the required sources](https://web.dev/uses-rel-preconnect)

* [Optimize: Reduce server side response time (TTFB)](https://web.dev/time-to-first-byte/)

* [Optimize: Avoid multiple page redirects](https://web.dev/redirects/)

* [Optimize preloading key requests](https://web.dev/uses-rel-preload/)

* [Optimize: Avoid heavy network load](https://web.dev/total-byte-weight/)

* [Optimization: How to use an efficient caching policy to cache static resources](https://web.dev/uses-long-cache-ttl/)

* [Optimize: Avoid an excessively large DOM](https://web.dev/dom-size/)

* [Optimize: Minimize key request depth](https://web.dev/critical-request-chains/)

* [Optimize: Ensure text remains visible during web font loading](https://web.dev/font-display)

* [Optimize: Maintain a lower request count and smaller transfer size](https://web.dev/resource-summary/)


<span id=".5Y-C6ICD5paH56ug"></span>
## Reference articles

https://web.dev/fcp

[https://github.com/berwin/Blog/issues/46](https://github.com/berwin/Blog/issues/46)
