---
title: "What is Mini Pro Monitoring?"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/What_is_Mini_Pro_Monitoring"
---

Mini Pro Monitoring is a capability provided by APMPlus for JavaScript error analysis and page load performance analysis in mini programs such as Douyin, WeChat, Alipay, Baidu, and Lark, helping you track and analyze issues.

<span id=".5bCP56iL5bqPUHJv56uv55uR5o6n6K-05piO"></span>
## Mini Pro Monitoring description

Users with Mini Monitoring requirements generally experience the following pain points:


* JavaScript monitor, request monitor, and performance monitor are insufficient.

* The SDK has complex configuration, large size, and high performance overhead.

* It is not possible to seamlessly obtain detailed DOM information and the DOM Path; users must manually mark.


Monitoring on the mini program side primarily provides a series of monitoring capabilities, including JavaScript monitors, request monitors, performance monitors, and custom monitors.

To address user pain points, Mini Program Pro provides the following solutions:


* performance monitor

   * Provides a wide range of performance\-related metrics and enables comprehensive monitoring of start performance, pageload performance, and runtime performance.

* Mini program performance score

   * We perform multi\-dimensional scoring based on the core metrics of mini programs, including pageload performance, request time, request error, and JavaScript error. You can customize the thresholds and weights for each metric to flexibly quantify and analyze the overall performance of your mini program.

* data explore

   * Simultaneously analyze various types of monitoring data, provide fine\-grained information about reported events, and aggregate all events from a user's single site visit and display them in chronological order.

   * SessionID links together events such as route changes, network requests, setData rendering, JavaScript errors, and custom events, helping address the issue of not being able to obtain detailed DOM information.


<span id=".5LyY5Yq_"></span>
## Advantages


* **Supports a wider range of platforms**

   Supports WeChat, Douyin, Alipay, Baidu, and Lark mini programs. It supports both integration with native frameworks and adaptation for third\-party frameworks, including Uni App and Taro.

* **More comprehensive performance metrics**

   By integrating the App and Page lifecycles with performance metrics to form a complete rendering trace, it is possible to quickly identify the specific times when performance issues occur for targeted troubleshooting.

* **More flexible integration**

   * The adaptation layer and feature modules can be loaded as needed, and performance loss is minimized. Pluggability and user customization are supported, with performance loss minimized.

   * Supports sampling for all reported fields, filtering with various operators, and logical AND and OR for sampling conditions, and supports more comprehensive scenarios.

   * Diverse lifecycles enable more flexible transformation.


<span id=".55uR5o6n6IO95Yqb5qaC6KeI"></span>
## Overview of monitoring capabilities


|**Application scenarios** |**Feature entry** |**DescriptionS** |
|---|---|---|
|Troubleshoot JavaScript errors |[JavaScript monitoring trends](https://docs.byteplus.com/en/docs/apmplus/JS_monitoring_minipro#.SlPplJnor6_otovlir_lm74=) |* Review specific error details, check stack trace details, and review version distribution and reporting trends.<br><br>* Navigate to data explore and observe, taking into account the specific user context. Use breadcrumbs and other methods to identify how issues are triggered. |
||[page list](https://docs.byteplus.com/en/docs/apmplus/JS_monitoring_minipro#.6ZSZ6K-v5Y-K6aG16Z2i5YiX6KGo) |* Filter out pages with a high error rate or error count, then view the details of each page to examine its JS metric.<br><br>* Observe specific error details, check stack trace details, and observe version distribution and reporting trends.<br><br>* Navigate to data explore to observe and analyze how specific user context, breadcrumbs, and other factors contribute to locating and triggering issues. |
||[Configure JavaScript error alerts](https://docs.byteplus.com/en/docs/apmplus/alert_management_minipro) |* When an alert occurs, related JavaScript errors are identified through intelligent attribution analysis.<br><br>* You can view error details and navigate to Data Explore to view specific reports. |
||[Query metrics](https://docs.byteplus.com/en/docs/apmplus/Mini_Pro_indicator_instructions) |By using metric queries, you can analyze the macro distribution, trends, and grouping of certain error metrics under specific conditions, generate dashboards, and continuously observe them. |
|Observe and improve pageload performance |[performance monitor](https://docs.byteplus.com/en/docs/apmplus/Performance_monitoring) |* View start performance, pageload performance, and runtime performance<br><br>* View the trends of all metrics within the selected time range<br><br>* Observe the pages currently performing worst for each metric, as well as the pages with the greatest deterioration compared to the previous time period.<br><br>* Navigate to data explore view. |
||[Page with suboptimal performance](https://docs.byteplus.com/en/docs/apmplus/Performance_monitoring#lB0semOy) |* Sort and filter pages by specific performance metrics to identify those with more severe performance issues, then go to the page details to review its performance metrics.<br><br>* For the metrics you are interested in, navigate to Data Explore. Observe and analyze potential performance bottlenecks by combining specific user context, timing, and setData information. |
||[Performance alert](https://docs.byteplus.com/en/docs/apmplus/alert_management_minipro) |* When an alert occurs, intelligent attribution analysis is used to identify relevant pages with poor performance.<br><br>* Click the attribution link to go directly to the corresponding page details, view specific metrics, and navigate to data explore to observe specific reported data. |
|Check the error data for the request |[request monitor](https://docs.byteplus.com/en/docs/apmplus/Request_monitoring) |View trends for all request times, error data, and callback time. |
||[request list](https://docs.byteplus.com/en/docs/apmplus/Request_monitoring#.5oWi6K-35rGC5YiX6KGo) |Sort by different metrics and view details of slow requests and error requests. |
|The page crashes or becomes extremely slow under certain conditions |[data explore](https://docs.byteplus.com/en/docs/apmplus/data_explore_minipro) |Identify all complete data reported within a specified time period based on parameters such as user_id, device model, time range, and more, in order to troubleshoot specific issues. |
|Define performance metrics appropriate to your situation |[project setting](https://docs.byteplus.com/en/docs/apmplus/project_setting_minipro#.5oCn6IO95oyH5qCH5Z-65YeG57q_) |Customize metric baselines according to different project complexities. |
|Filter data by the version dimension |\- |1. Integrate according to the development process. Complete the configuration and conceptual understanding of the version and its corresponding development process.<br><br>2. You can directly filter data based on release and env on the platform. |


<span id=".5YW45Z6L5Zy65pmv"></span>
## Typical scenarios

<span id=".6KeC5a-f5bm25pS56L-b6aG16Z2i5oCn6IO9"></span>
### Observe and improve pageload performance

The mini program start process includes preparing the runtime environment, downloading, injecting, and executing the mini program code package, and rendering the mini program homepage. Optimizing code package size and rendering time can effectively optimize startup speed. Mini Program Pro provides several metrics, including first screen cold start total time, Mini Program Initialization Time, download time, JS injection time, and others. Pages with poor performance and the top 5 degraded items help you better identify and locate optimization targets.

<span id=".5Z-65pys5qaC5b-1"></span>
## Basic concepts

The following summarizes the basic concepts involved in the process of using Mini Pro Monitoring, making it convenient for you to look up and understand related concepts.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The storage period for all data in Mini Pro Monitoring is three months.</div>



|**Glossary** |**DescriptionS** |
|---|---|
|aid |Application ID. The Application ID is a globally unique identifier for a project and remains consistent across both the SDK and the platform. Unlike the common APP_ID, it does not require a special application; you only need to ensure that it does not duplicate the Application ID (AID) of any existing project. |
|pid |The ID that identifies a specific page in the application can be used on the platform to filter, group, and view data. You must specify the PID in the SDK\-related configuration. By default, the SDK sets the PID to the URL of the current page. It is recommended to configure the aggregation policy in the SDK for activity pages or pages with unique IDs. |
|user_id |Identifies the ID of the current visiting user, which is used to calculate UV, impacted user, and other related information. You can specify it yourself. By default, the operating system will automatically generate a uuid for you and store it in localstorage. |
|session_id |ID that identifies a session. A session refers to the entire period from when a user opens a page until the page is closed. The session_id is used to calculate site\-wide PV, error rate, and other metrics, and also for deduplication counting in reporting. You do not need to specify session_id yourself; the operating system will generate it for you. |
|view_id |ID for a single page visit. In scenarios such as SPA, a page visit is a subset of a session, and a single session may include multiple page visits. We use page visits to calculate single PID PV and to link together related static resources, requests, and Longtask reporting. |
|env |The online environment of the Mini Program. After integrating the SDK, the online environment identifier of the current mini program will be automatically obtained. |
|release |The online version of the mini program. After integrating the SDK, the current online version of the mini program will be obtained automatically. For example: 1.0.0 (X.X.X). |
|metric baseline |Baseline setting is provided for the collected performance metrics. By setting good\-base\-line and bad\-base\-line, you can quickly identify the current status of your site or page and further perform targeted optimization. |
