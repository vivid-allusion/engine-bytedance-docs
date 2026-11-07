---
title: "Integrate SPA scenarios"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Integrate_SPA_scenarios"
---

SPA (single\-page application) applications deliver a faster user experience and greater user experience fluency by dynamically updating the page. Unlike traditional multi\-page applications, SPA applications do not need to reload the entire page each time the user navigates. Instead, they dynamically load and update page content. This means that users can interact and navigate more quickly, without having to wait for loading time between pages. SPAs typically use frontend frameworks to manage application status and page routing. For example, Angular, React, or Vue.

<span id=".5o6l5YWl5oyH5a-8"></span>
## Integration guide

When monitoring SPA applications, you need to pay additional attention to the following aspects:


* **Page route monitoring**: The core of SPA applications is managing different pages and status through routing, and monitoring changes in page routes is necessary to understand user navigation and usage patterns.

* **Performance monitor**: The core of SPA applications is the dynamic loading and updating of page content, so it is necessary to monitor performance during route changes in order to identify and optimize performance issues.


<span id=".6aG16Z2i6Lev55Sx55uR5o6n"></span>
## Page route monitoring

By configuring the `routeMode` of the pageview plugin, you can enable SPA route monitoring and reporting.

Configuration examples

```TypeScript
import client from '@apmplus/web'

client('init', {
  ...
  plugins: {
    pageview: {
      routeMode: 'hash',  // hash or history
    }
  },
  ...
})
```


<span id=".5oCn6IO955uR5o6n"></span>
## performance monitor

Pageload performance is divided into first screen performance and non\-first screen performance.


* First screen performance refers to the performance when the page is loaded for the first time. As with ordinary applications, it can be measured using metrics such as timing, FP, FCP, FMP, TTI, and LCP.

* Non\-initial screen performance: Performance of route switching. The SPA performance plugin can automatically calculate and report the SPA_LOAD metric to measure route switching performance.


<span id=".5o6l5YWl"></span>
### Integrate

<span id=".54mI5pys5L6d6LWW"></span>
#### Version dependencies

@apmplus/web \>= 2.0.1 && @apmplus/integrations \>= 2.1.0

<span id=".6Ieq5Yqo6K6h566X5bm25LiK5oqlU1BBX0xPQUQ="></span>
#### Automatically calculate and report SPA_LOAD

```TypeScript
import client from '@apmplus/web'
import { SPALoadPlugin } from '@apmplus/integrations'

client('init', {
  ...
  plugins: {
    pageview: {
      routeMode: 'hash' // The default is history mode, so if you are using history routing, configuration is not required.
    }
  },
  integrations: [SPALoadPlugin()], // Manually import SPALoadPlugin
})
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">SPALoadPlugin primarily works by monitoring changes in routing and observing a series of events related to DOM changes, resource loading, request sending, and more after a route switch, in order to determine the time at which a page reaches a stable state. It then reports the SPA_LOAD metric.</div>


<span id=".5omL5Yqo5LiK5oqlU1BBX0xPQUQ="></span>
#### Manually report SPA_LOAD

```TypeScript
// Solution 1: Call performanceInit before routing switch, and call performanceSend after rendering
// Before route switching
client('performanceInit')

// After SPA rendering is complete, call this method and the SDK will help calculate the time difference, then report the spa_load performance metric.
client('performanceSend')

// Option 2: Report custom performance metrics: Manually calculate the rendering time (in ms), and report it via the single-metric performance reporting protocol
client('sendCustomPerfMetric', { name: 'spa_load', value: {{渲染时间}} })
```


There are two methods to manually report SPA_LOAD:


* **Log events using performanceInit and performanceSend**

   Cautions for using performanceIni and performanceSend:

   * **It is necessary to determine at the product level which URLs correspond to the concept of a page.** 

      For example, if a URL change corresponds to switching between two tabs on a page, and at the product level these two tabs are considered part of the same page, then in this case the URL change does not require calling performanceInit&&performanceSend.

   * **The time when the page finishes loading can be selected as the node where the framework layer completes rendering.** 

      For example, after the URL changes, the page requests two interfaces, a and b. The data for a corresponds to the primary content, and the data for b corresponds to the secondary content. After the data from request a has finished rendering, you can treat this as the page render completion time and call performanceSend to trigger metric calculation.

* **Manually report custom performance metrics**


<span id=".5bqU55So5LiO5raI6LS5"></span>
### Applications and consumption


1. Registration performance metrics.

   Assign a baseline to the metric based on its specific circumstances; this can be used to assess the quality of the metric. To register performance metrics, refer to [performance metric](https://vsop-online.bytedance.net/doc/manage/detail/7047/?DocID=0).

2. In the upper left corner of the console, select **All features \> site performance overview**.

3. Click the **Metric overview** tab to view the consumption status of the SPA_LOAD metric.

4. In the upper left corner of the console, select **All features \> data explore**.

5. Click the **Views** tab to view the waterfall chart.

   In the waterfall chart, you can view the duration of a series of resource requests and business requests preceding the SPA_LOAD metric, which helps identify the causes of poor route\-switching performance.
