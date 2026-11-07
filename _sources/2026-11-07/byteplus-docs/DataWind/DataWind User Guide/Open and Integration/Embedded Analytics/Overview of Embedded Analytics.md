---
title: "Overview of Embedded Analytics"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Overview_of_Embedded_Analytics"
---

<span id="_1-概述"></span>
# 1. Overview

DataWind DataWind provides embedded analytics capabilities, allowing users to embed completed dashboards and charts into third\-party platforms for relevant personnel to view. For example, users can embed dashboards or charts into business systems such as CRM or ERP to enable business data monitoring.

Users can flexibly select which features to integrate based on their business needs. Currently, DataWind supports three methods for embedding dashboards and chart viewing modules: quick embed, **Iframe, and SDK**. Dashboard viewing also includes mobile dashboards and large screens. Since Iframe integration does not fully support embedded analytics features such as event listening, method invocation, and token updates, these features are not available. To use these features, it is recommended to integrate using the SDK.

<span id="_2-集成仪表盘查看"></span>
# 2. **Integrate dashboard viewing**


* Dashboards completed in DataWind (in viewing mode) can be embedded into other systems.

* The integration effect is shown in the following figure:


<span id="_3-集成图表"></span>
# 3. Integrate charts


* When only a few charts are needed rather than the entire dashboard, you can choose to embed only individual charts.

* Caution: Charts must be saved to a dashboard to support third\-party embedding. When saving a chart, you must select a dashboard.

* The integration effect is as follows. Users can view and edit the chart.


<span id="_4-快速嵌出"></span>
# 4. Quick embed

Once users have completed dashboard or chart creation, they can quickly embed dashboards or charts on the page in a visual manner. For detailed steps, see [Chart Embedding](https://docs.byteplus.com/docs/DataWind/Chart_Embedding).

<span id="_5-iframe-集成"></span>
# 5. Iframe integration


* You can control data switching via URL parameters, including language, hiding the header menu, and more. For operation steps, see [Iframe Integration Solution](https://docs.byteplus.com/docs/DataWind/Iframe_Integration_Solution).

* Permissions are controlled by DataWind DataWind (for permission details, see [Permission Overview](https://docs.byteplus.com/docs/DataWind/Permission_Overview).), and third parties cannot control permissions for embedded pages.


<span id="_6-sdk-集成"></span>
# 6. SDK integration


* Users can perform frontend development and integration using the SDK. For operation steps, see [JS SDK Integration Solution](https://docs.byteplus.com/docs/DataWind/JS_SDK_Integration_Solution).

* The user's visibility, permissions, and direct access to the dashboard are consistent with those for Smart Data Insight DataWind.
