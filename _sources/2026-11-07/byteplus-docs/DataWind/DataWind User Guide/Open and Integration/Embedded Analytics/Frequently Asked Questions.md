---
title: "Frequently Asked Questions"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Frequently_Asked_Questions"
---

<span id="_1-仪表盘如何自适应宽高"></span>
# 1. How does the dashboard adapt to width and height

<span id="_1-1-自适应宽度"></span>
## 1.1 Adaptive width


* Upgrade to the new version of the dashboard

* Set adaptive width in view mode


<span id="_1-2-自适应高度"></span>
## 1.2 Adaptive height

To set the container height based on the dashboard's height, you can listen for the `dashboardHeightChange` event on the SDK and set the obtained `height` value to the outer container. You can refer to [Event](https://docs.byteplus.com/docs/DataWind/Event) for integration.

<span id="_2-覆盖筛选器不生效"></span>
# 2. Filter override not working

Please use the following checklist to troubleshoot possible errors:

<span id="_2-1-嵌入仪表盘"></span>
## 2.1 Embedding a dashboard


* Has a public filter been added to the dashboard? When embedding a dashboard, overriding chart filter conditions is not supported; only public filters can be overridden.

* Has the public filter been added to the query container? Currently, only public filters outside the query container can be overridden.

* Are you using the public filter name for the override? If the identifier you pass is the dataset field name instead of the public filter name, it will not be recognized.

* Does the public filter name contain spaces? Public filter name overrides support both Chinese and English, but do not support spaces. Please modify the filter name.


<span id="_2-2-嵌入图表"></span>
## 2.2 Embedding a chart


* Has a filter field been added to the chart? When embedding a chart, you need to locate the chart filter condition and override it. If the filter condition is not in the chart configuration, the override will not take effect.

* Are you using the field name for the override? Other identifiers will not be recognized.

* Has the field name been changed? You can delete the corresponding filter condition from the chart, re\-add it, and then verify whether the override works.


<span id="_3-浏览器兼容性"></span>
# 3. Browser compatibility

Supported browsers for DataWind Intelligent Data Insight are Chrome 87 and above. Other browsers have not been thoroughly tested. Running on incompatible browsers may result in issues such as page crashes, unresponsiveness, or incorrect layouts.

We recommend that users update their browsers to the latest version for a better browsing experience.

<span id="_4-在微前端框架中使用"></span>
# 4. Use in micro\-frontend frameworks

If you use the SDK in micro\-frontend frameworks, pages may fail to load and console errors may occur. This is because the SDK is implemented as a Web Component based on [Lit](https://lit.dev/) and relies on a normal browser execution environment, while micro\-frontend frameworks commonly intercept or proxy the DOM/BOM objects of the browser runtime environment.

If you encounter these issues, consult the documentation for the corresponding micro\-frontend framework or contact official Volcano Engine personnel to confirm how to load the SDK in the relevant framework.
