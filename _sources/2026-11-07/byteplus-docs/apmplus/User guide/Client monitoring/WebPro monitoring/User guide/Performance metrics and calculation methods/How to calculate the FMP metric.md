---
title: "How to calculate the FMP metric"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/How_to_calculate_the_FMP_metric"
---

Calculating FMP incurs significant performance overhead, and minor changes can cause large fluctuations in its value. This metric can be replaced by LCP (Largest Contentful Paint).

<span id=".5LuA5LmI5pivIEZNUCDmjIfmoIc="></span>
## What is the FMP metric

FMP (First Meaningful Paint) refers to the time when meaningful content is first rendered. As shown in the figure below, First Meaningful Paint is considered complete when the entire page layout and textual content have finished rendering. Therefore, FMP measures the time when users see the main content of the webpage and is an important metric from the perspective of user experience.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_e633d54fa79c53768583cb7f9e9ca2c2) </span>

In the industry, the time of FMP is typically regarded as the first screen time. Although the two are not exactly equal in terms of absolute accuracy, both can accurately reflect the performance of the current page’s loading and rendering. FMP is generally considered to be the moment when users obtain the main information of the page, meaning that user needs are satisfied at this point. Therefore, Product usually pays attention to the FMP metric.

<span id=".5aaC5L2V6K6h566XIEZNUCDmjIfmoIc="></span>
## How to calculate the FMP metric

As the web page loads and is parsed, the browser gradually adds layout objects (Layout Object) to the layout tree (Layout Tree) to perform layout.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_68ed35ebc4ac4ed403b5b5a79fe3fbdf) </span><span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_022453e312bca966853b57914fb7c84d) </span>


* Figure 1 and Figure 2 show the process of loading the Google Search results page from two different perspectives.

* Figure 1 shows how the number of layout objects added to the layout tree changes over time during the loading of the Google Search results page.

* Figure 2 illustrates the visualization process during the loading and rendering of the Google Search results page.


The entire process of loading and rendering the Google Search results page is explained in detail below, using Figure 1 and Figure 2:


1. At 1.577 seconds, 60 layout objects have already been added to the layout tree (Figure 1), and at this point, only one Header has been rendered on the page (Figure 2).

2. At 1.760 seconds, the total number of layout objects is 103 (Figure 1), and at this point, the entire page header has finished rendering (Figure 2).

3. At 1.907 seconds, search result data is returned and rendered, and 261 layout objects are added to the layout tree (Figure 1). At this point, the main content of the page has already been rendered (see Figure 2). From the perspective of user experience, this point in time is FMP.

4. Subsequently, other search results and layout objects at the bottom of the page continue to be added to the layout tree and rendered. The page completed final loading and rendering in 2.425 seconds (Figure 2).


Based on the interpretation of Figure 1 and Figure 2, it can be seen from the above example of the Google Search results page loading process that the number of layout objects is closely related to the completeness of the page. A method currently recognized in the frontend industry for calculating FMP is to consider the time when the page is painted after the largest layout shift during loading and rendering as the FMP of the current page.

<span id=".5Luj56CB5a6e546w5Y6f55CG"></span>
### Principles of code implementation

The theoretical basis for the code implementation is that the time at which the DOM structure changes is approximately the same as the time at which the corresponding rendering occurs. The FMP time point is the time when the DOM structure changes most dramatically.

The time points at which the DOM structure changes can be obtained using [MutationObserver API](https://dom.spec.whatwg.org/#mutationobserver).

Use MutationObserver to monitor every change to the overall DOM of the page. When the MutationObserver callback is triggered, calculate the current DOM tree score in the callback. The time point when the score changes most dramatically is the FMP time point.

<span id=".5rWP6KeI5Zmo5YW85a655oCn6K-05piO"></span>
### Browser compatibility descriptions

The FMP metric requires the browser to support [MutationObserver API](https://dom.spec.whatwg.org/#mutationobserver). If the browser does not support MutationObserver API, the reported metric will have isSupport set to false.

<span id=".5pWw5o2u5YeG56Gu5oCn6K-05piO"></span>
### Data accuracy description

Based on the calculation method for FMP, we can determine that it is currently not possible to obtain the browser rendering time or the specific time of FMP through browser\-provided APIs (which is different from FP and FCP). As a result, the industry typically uses the time of the largest layout change as the FMP. However, this value is usually slightly less than the actual FMP; experimental data shows that the maximum observed error is within approximately 300 milliseconds.

Regarding the implementation of the FMP metric in the SDK, it is important to note that the absolute value calculated for FMP is not perfectly accurate, but it is relatively accurate. The calculation method is consistent across all web pages integrated with the SDK, which means that the data dimensions and measurement criteria are uniform for all pages. Under the current FMP metric calculation method, FMP can provide a relatively stable and accurate representation of web page loading and rendering performance. So we can pay more attention to the trend changes of FMP during report consumption.

<span id=".5aaC5L2V5LyY5YyWIEZNUCDmjIfmoIc="></span>
## How to optimize the FMP metric

To optimize the FMP metric, the key is to reduce the rendering time of the page's critical path. Common optimization methods


1. Optimize the page's [critical path](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/).

2. Reduce the number of external CSS resources.

3. Reduce the number of external JS resources loaded synchronously.

4. Use HTTP caching appropriately

5. Compress static resources.

6. Optimize JS execution time during page loading.

7. [When importing external font files, avoid the issue where text becomes invisible while waiting for the font file to load](https://web.dev/font-display/).


<span id=".5Y-C6ICD6LWE5paZ"></span>
## References


* https://web.dev/first\-meaningful\-paint/

* https://docs.google.com/document/d/1BR94tJdZLsin5poeet0XoTW60M0SjvOJQttKT\-JK8HI/view

* https://scotch.io/courses/10\-web\-performance\-audit\-tips\-for\-your\-next\-billion\-users\-in\-2018/FMP\-first\-meaningful\-paint
