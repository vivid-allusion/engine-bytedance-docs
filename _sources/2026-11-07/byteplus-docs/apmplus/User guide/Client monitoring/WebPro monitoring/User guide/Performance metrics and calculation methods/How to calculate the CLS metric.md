---
title: "How to calculate the CLS metric"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/How_to_calculate_the_CLS_metric"
---

Cumulative Layout Shift (CLS) is an important user\-centric metric for measuring [visual stability](https://web.dev/user-centric-performance-metrics/#types-of-metrics), as this metric helps quantify how often users experience unexpected layout shifts. A lower CLS provides users with a natural interaction flow, free from delay and lag.

<span id=".Q0xTIOaMh-agh-S7i-e7jShDdW11bGF0aXZlIExheW91dCBTaGlmdCk="></span>
## Introduction to the CLS metric (Cumulative Layout Shift)

CLS measures the highest cumulative score of a sequence of [unexpected layout shifts](https://web.dev/cls/#expected-vs.-unexpected-layout-shifts) that occur during the entire page lifecycle. A layout shift occurs whenever the position of a visible element changes from one rendered frame to the next. For more information, please refer to [layout shift score](https://web.dev/cls/#layout-shift-score).

<span id=".Q0xTIOWIhuaVsOWmguS9leiuoeeul--8nw=="></span>
## How is the CLS score calculated?

When calculating the layout shift score, the browser will view the size of the viewport and the displacement of unstable elements within the viewport between two rendered frames. The layout shift score is the product of two metrics for this displacement: the impact score and the distance score (both defined below).

```Plain Text
Layout shift score = Impact score * Distance score
```


<span id=".5b2x5ZON5YiG5pWw"></span>
## Impact scores

[Impact score](https://github.com/WICG/layout-instability#Impact-Fraction) measures the effect of unstable elements on the visible area between two frames. The set of visible regions of all unstable elements in the previous and current frames, which accounts for a portion of the total visible area, is the impact score for the current frame.

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_a74d8687f6ef005f028db94684b2059d) </span>

In the image above, there is an element that occupies half of the visible area within a single frame. Next, in the next frame, the element moved down by 25 percent of the height of the visible area. The red dashed rectangular box represents the set of visible regions of elements across two frames. In this example, this set accounts for 75% of the total visible area. Therefore, its impact score is `0.75`.

<span id=".6Led56a75YiG5pWw"></span>
## Distance score

Another part of the layout shift score calculation formula measures the distance that unstable elements move relative to the viewport. The distance score is defined as the maximum displacement of any unstable element within a single frame (either horizontally or vertically), divided by the largest dimension of the viewport (width or height, whichever is greater).

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_a65b8a25ed702b70a8020f37453a2ed6) </span>

In the example above, the largest dimension of the visible area is height. The displacement distance of the unstable element is 25 percent of the visible area’s height, so the distance score is 0.25.

Therefore, in this example, the impact score is `0.75` and the distance score is `0.25`, so the layout shift score is `0.75 * 0.25 = 0.1875`.

Initially, the layout shift score was calculated only on the basis of the impact score. The distance score is introduced to avoid excessive penalization when large elements undergo minor shifts.

<span id=".6aKE5pyf5biD5bGA5YGP56e7IHZzLiDmhI_lpJbluIPlsYDlgY_np7s="></span>
## Expected layout shift vs. Unexpected layout shift

Layout offset is not always a bad thing. In fact, many dynamic network applications frequently change the initial position of page elements.

<span id=".55Sx55So5oi35Y-R6LW355qE5biD5bGA5YGP56e7"></span>
### User\-initiated layout shift

Layout shifts are only considered undesirable when users do not expect them to occur. In other words, layout shifts in response to user interactions—such as clicking a link, selecting a button, or typing information in the search box—are generally acceptable, provided that the shift occurs close enough in time to the interaction for users to clearly understand the relationship between the action and the result.

For example, if a user interaction triggers a network request that may take some time to complete, it is best to immediately reserve some space and display a loading indicator to prevent unpleasant layout shifts when the request is finished. If users are not aware that certain content is currently loading, or do not know when resources will be ready, they may attempt to click other content during the waiting period in order to break the deadlock.

Layout shifts that occur within 500 milliseconds of user input are marked with the `[hadRecentInput](https://wicg.github.io/layout-instability/#dom-layoutshift-hadrecentinput)` flag, making it easier to exclude these shifts from calculations.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The hadRecentInput flag applies only to non\-continuous input events, such as tap, click, or key actions. Continuous interactions such as scrolling, dragging, or pinch\-to\-zoom gestures are not considered "recent input." For details, refer to <a href="https://github.com/WICG/layout-instability#recent-input-exclusion">layout instability specification</a>.</div>


<span id=".5oCO5qC3566X5piv6Imv5aW955qEIENMUyDliIbmlbDvvJ8="></span>
### [What is a good CLS score?](https://web.dev/cls/#cls-2)

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_9ac0509dd757b1af64c4ed9cae7c74c6) </span>

To provide a good user experience, the website should keep the CLS score at 0.1 or below. To ensure that you can achieve the recommended target value during most user visits, a good measurement threshold is the 75th percentile of page load times, which applies to both mobile and desktop devices.

<span id=".5bmz5Y-w5aaC5L2V5raI6LS5IENMU--8nw=="></span>
## How does the platform consume CLS?

<span id=".56uZ54K55oCn6IO95oC76KeI"></span>
### site performance overview

In the metric overview of the site performance overview, you can see the CLS status and trends for the entire site.

<span id=".6aG16Z2i5YiX6KGo"></span>
### page list

In the overview table of the page list, after checking the desired experience metrics in the custom columns, you can observe these metrics from the perspective of the page.

<span id=".6aG16Z2i6K-m5oOF"></span>
### Page details

Click a pid in the page list to enter its details, where you can also view the CLS status for the individual page.

<span id=".55uR5o6n5oql6K2m"></span>
### Monitoring alerts

When configuring CLS alerts in the monitoring alert module, the [recommended score](https://web.dev/cls/#cls-2) provided by web.dev is 0.1. You may adjust this value as appropriate based on the specific features of your site.

<span id=".5pWw5o2u5o6i57Si"></span>
### data explore

In the Views module of data explore, after you turn on CLS in custom columns, you can view the CLS metric for each page visit.

<span id=".5pWw5o2u5YiG5p6Q"></span>
### data analytic

On the data analytic page, you can filter the CLS dimension and freely combine it with other metrics to generate charts for analysis. After configuration is complete, you can add the charts to the dashboard. For more details, refer to [LCP consumption method](https://docs.byteplus.com/en/docs/apmplus/How_to_calculate_the_LCP_metric#.5pWw5o2u5YiG5p6Q).

<span id=".5oyH5qCH6I635Y-W5a6e546w57uG6IqC"></span>
## Implementation details for obtaining metrics

Layout Shift is defined by the [Layout Instability API](https://github.com/WICG/layout-instability). When a visible element in the view changes its starting position between two frames, the API reports a layout shift. These elements are considered unstable elements.

Create a [PerformanceObserver](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceObserver) and use the [Layout Instability API](https://github.com/WICG/layout-instability) to monitor unexpected layout changes.

```javascript
let clsValue = 0;
let clsEntries = [];
let sessionValue = 0;
let sessionEntries = [];
new PerformanceObserver((entryList) => {
    for (const entry of entryList.getEntries()) {
        // Only count layout shifts without recent user input.
        if (!entry.hadRecentInput) {
            const firstSessionEntry = sessionEntries[0];
            const lastSessionEntry = sessionEntries[sessionEntries.length - 1];
        // If the entry occurred less than 1 second after the previous entry and
        // less than 5 seconds after the first entry in the session, include the
        // entry in the current session. Otherwise, start a new session.
         if (sessionValue
         && entry.startTime - lastSessionEntry.startTime < 1000
         && entry.startTime - firstSessionEntry.startTime < 5000) {
             sessionValue += entry.value;
             sessionEntries.push(entry);
          } else {
              sessionValue = entry.value;
              sessionEntries = [entry];
           }
           // If the current session value is larger than the current CLS value
           // update CLS and the entries contributing to it.
           if (sessionValue > clsValue) {
               clsValue = sessionValue;
               clsEntries = sessionEntries;
               // Log the updated value (and its entries) to the console.
               console.log('CLS:', clsValue, clsEntries)
           }
       }
}}).observe({type: 'layout-shift', buffered: true});
```


<span id=".5rWP6KeI5Zmo5YW85a655oCn6K-05piO"></span>
## Browser compatibility description

The metric requires the browser to support [Largest Contentful Paint](https://wicg.github.io/largest-contentful-paint/), [Layout Instability API](https://github.com/WICG/layout-instability), and [PerformanceObserver](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceObserver). If these features are not supported, the isSupport field in the reported metric is set to false.

<span id=".5aaC5L2V5LyY5YyWQ0xT5oyH5qCH"></span>
## How to optimize the CLS metric


1. Include size attributes in picture and video elements, or use something like a CSS aspect ratio box to retain the required space.

2. Do not insert content above existing content unless it is in response to user interaction.

3. Prefer transform animations over animation properties that trigger layout changes.


For in\-depth optimization, refer to [Optimize Cumulative Layout Shift (CLS)](https://web.dev/optimize-cls/).
