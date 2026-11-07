---
title: "How to calculate the LCP metric"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/How_to_calculate_the_LCP_metric"
---

Largest Contentful Paint (LCP) is an important user\-centric metric for measuring [perceived load speed](https://web.dev/user-centric-performance-metrics/#types-of-metrics), as it marks the point on the page load timeline when the main content has essentially finished loading. A fast LCP helps reassure users that the page is [usable](https://web.dev/user-centric-performance-metrics/#questions).

<span id=".5oyH5qCH6Kej6YeK"></span>
## Metrics explanation

<span id="LCP (Largest Contentful Paint )"></span>
### LCP (Largest Contentful Paint )

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_4236953005c4279feaafab5a2677479a) </span>

The Largest Contentful Paint (LCP) metric reports the relative time at which the largest [image or text block](https://web.dev/lcp/#what-elements-are-considered) visible in the viewport has finished rendering, based on the time when the page [first starts loading](https://w3c.github.io/hr-time/#timeorigin-attribute).

<span id=".5ZOq5Lqb5YWD57Sg5Zyo6ICD6YeP6IyD5Zu05YaF77yf"></span>
### Which elements are within the scope of consideration?

According to the current [Largest Contentful Paint API](https://wicg.github.io/largest-contentful-paint/) specification, the element types considered for Largest Contentful Paint are:


* `<img>`element

* An `<image>` element embedded within an `<svg>` element

* `<video>` element (using a cover image)

* Elements with background images loaded via the [url()](https://developer.mozilla.org/docs/Web/CSS/url()) function (rather than using [CSS gradients](https://developer.mozilla.org/docs/Web/CSS/CSS_Images/Using_CSS_gradients))

* A [block-level element](https://developer.mozilla.org/docs/Web/HTML/Block-level_elements) that contains text nodes or other inline\-level text element children.


<span id=".5L2V5pe25oql5ZGK5pyA5aSn5YaF5a6557uY5Yi277yf"></span>
### When should Largest Contentful Paint be reported?

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_cd17b009a9bca2b61f36f82a166cd095) </span>

Web pages are typically loaded in stages; therefore, the largest element on the page may change. For example, on a page containing both text and images, the browser may initially render only the text. At this point, the browser dispatches a largest\-contentful\-paint entry. Later, after the image finishes loading, a second largest\-contentful\-paint entry will be dispatched.

<span id=".5bmz5Y-w5aaC5L2V5raI6LS5IExDUA=="></span>
## How to consume LCP on the platform

<span id=".56uZ54K55oCn6IO95oC76KeI"></span>
### site performance overview

In the PID aggregation module of the site performance overview, you can view the overall LCP compliance rate for pages, and also display a ranking of the pages with the worst LCP.

In the metric overview module of the site performance overview, you can view the LCP status and trends for the entire site.

<span id=".6aG16Z2i5YiX6KGo"></span>
### page list

In the overview table of the page list, after selecting experience metrics in the custom columns, you can view the metrics for each page.

<span id=".6aG16Z2i6K-m5oOF"></span>
### Page details

From the site performance overview, click a single pid link to enter the page details, where you can also observe the LCP status for the individual page.

<span id=".5pWw5o2u5o6i57Si"></span>
### data explore

In the Data Explore module, you can view the LCP metric for each page visit in the Views module.

<span id=".5pWw5o2u5YiG5p6Q"></span>
### data analytic

On the data analytic page, you can filter by the LCP dimension and freely combine other metrics to generate charts for analysis. After configuration is complete, you can add the charts to the dashboard.

<span id=".55uR5o6n5oql6K2m"></span>
### Monitoring alerts

You can configure alerts for the LCP metric in the Monitoring alert module. The [recommended time](https://web.dev/lcp/#lcp-2) provided by web.dev is 2500 ms, and you can adjust it appropriately based on the features of your site.

<span id=".5oyH5qCH6I635Y-W5a6e546w57uG6IqC"></span>
## Implementation details for obtaining metrics

Create a [PerformanceObserver](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceObserver) and use the [Largest Contentful Paint API](https://wicg.github.io/largest-contentful-paint/) to observe and report. The specific timing for settlement can be found in the code implementation below.

```Plain Text
new PerformanceObserver((entryList) => {
    for (const entry of entryList.getEntries()) {
        console.log('LCP candidate:', entry.startTime, entry);
    }})
.observe({type: 'largest-contentful-paint', buffered: true});
```


<span id=".5rWP6KeI5Zmo5YW85a655oCn6K-05piO"></span>
## Browser compatibility

The metric requires the browser to support [Largest Contentful Paint API](https://wicg.github.io/largest-contentful-paint/) and [PerformanceObserver](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceObserver). If the browser does not support these, the isSupport field in the reported metric is false.

<span id=".5aaC5L2V5LyY5YyWTENQ5oyH5qCH"></span>
## How to optimize the LCP metric

LCP is mainly affected by four factors:


* Slow server response speed

* Render\-blocking JavaScript and CSS

* Resource loading time

* Client\-side rendering


For more information on how to improve LCP, see [Optimize LCP](https://web.dev/optimize-lcp/). For further guidance on individual performance tips that can improve LCP, see:


* [Use the PRPL pattern to achieve instant loading](https://web.dev/apply-instant-loading-with-prpl/)

* [Optimize the critical rendering path](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/)

* Optimize CSS

   * [Optimize: Defer non-critical CSS](https://web.dev/defer-non-critical-css/)

   * [Optimize: Minify CSS](https://web.dev/unminified-css/)

   * [Extract critical CSS](https://web.dev/extract-critical-css/)

   * [Optimize CSS background images with media queries](https://web.dev/optimize-css-background-images-with-media-queries/)

* Optimize images

   * [Choose the right image format](https://web.dev/choose-the-right-image-format/)

   * [Choose the correct level of compression](https://web.dev/compress-images/)

   * [Use Imagemin to compress images](https://web.dev/use-imagemin-to-compress-images/)

   * [Replace animated GIFs with video for faster page loads](https://web.dev/replace-gifs-with-videos/)

   * [Serve responsive images](https://web.dev/serve-responsive-images/)

   * [Serve images with correct dimensions](https://web.dev/serve-images-with-correct-dimensions/)

   * [Use WebP images](https://web.dev/serve-images-webp/)

   * [Use image CDNs to optimize images](https://web.dev/image-cdns/)

* Optimize web page fonts

   * [Optimize: Ensure text remains visible during web font loading](https://web.dev/font-display)

   * [Avoid invisible text during font loading](https://web.dev/avoid-invisible-text/)

   * [Optimize WebFont loading and rendering](https://web.dev/optimize-webfont-loading/)

   * [Reduce WebFont Size](https://web.dev/reduce-webfont-size/)

* Optimize JavaScript (for client\-side rendered websites)

   * [Optimize: use the PRPL pattern to enable instant loading](https://web.dev/apply-instant-loading-with-prpl/)

   * [Reduce JavaScript size](https://web.dev/unminified-javascript/)

   * [Optimize: Reduce JavaScript execution time](https://web.dev/bootup-time/)

   * [Reduce JavaScript payloads with code splitting](https://web.dev/reduce-javascript-payloads-with-code-splitting/)

   * [Optimize: Remove unused code](https://web.dev/remove-unused-code/)

   * [Minify and compress network payloads](https://web.dev/reduce-network-payloads-using-text-compression/)

   * [Serve modern code to modern browsers for faster page loads](https://web.dev/serve-modern-code-to-modern-browsers/)

   * [Publish, ship, and install modern JavaScript for faster applications](https://web.dev/publish-modern-javascript/)

   * [How CommonJS is making your bundles larger](https://web.dev/commonjs-larger-bundles/)


<span id=".5YW25LuW6LWE5rqQ"></span>
## Other resources

[Annie Sullivan (安妮·沙利文)](https://perfnow.nl/)'s talk at [performance.now()](https://youtu.be/ctavZT87syI): [Lessons learned from Chrome's performance monitoring tools](https://anniesullie.com/) (2019)
