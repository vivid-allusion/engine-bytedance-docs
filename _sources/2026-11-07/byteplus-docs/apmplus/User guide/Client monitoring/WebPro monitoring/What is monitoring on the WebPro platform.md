---
title: "What is monitoring on the WebPro platform"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/What_is_monitoring_on_the_WebPro_platform"
---

WebPro Monitoring is a front\-end monitoring product provided by APMPlus. It is suitable for browser pages, H5 pages within mobile apps, and similar pages, enabling monitoring of site performance and user experience, timely detection of anomalies, and assisting in tracking and analyzing issues.

<span id=".V2ViUHJv56uv55uR5o6n6K-05piO"></span>
## WebPro\-side monitoring description

Users with front\-end monitoring needs generally have the following pain points:


* Site stability issues

   Issues that prevent users from using the service normally can cause direct losses to the enterprise.

* Site performance issues

   Performance issues with the initial screen and during page transitions—such as long page loading and rendering times, poor interaction experience, the feeling of frame drops or stuttering, and cases where a single operation may require the user to wait a long time, among other issues—may cause users to leave due to poor experience.

* Limited site monitoring data

   Only routine monitoring data is available, for example, viewing user page views, usage paths, and more.


WebPro monitoring provides Page View monitoring, performance monitoring, JavaScript error monitoring, white screen monitoring, request monitoring, static resource monitoring, user behavior monitoring, and a range of other monitoring capabilities. To address the above user pain points, the following solutions are provided:


* Stability monitoring systems

   * Supports white screen monitoring, monitors online white screen anomalies, and provides attribution capabilities to help troubleshoot the true cause of white screen occurrences.

   * Supports JS error monitoring and the collection of more stack traces and more user behaviors. Accurately aggregates abnormal issues, helping you quickly detect, locate, and resolve problems.

   * Supports request anomaly monitoring to promptly detect unstable requests and assist in monitoring server\-side stability.

   * Supports resource anomaly monitoring, detects resource failures on the user side, and helps assess resource health and CDN stability.

* Performance monitoring

   * Page performance

      * Provides the most comprehensive set of performance metrics, not only displays the metrics but also defines baselines for each one. This enables rapid assessment of user satisfaction with site performance, the rate of compliance with baselines, and satisfaction for each individual page.

      * Provides sufficient information to help analyze and locate performance issues and resolve problems.

   * Interface performance

      * Record the time taken by the interface, and obtain the duration of each stage.

   * Resource loading performance

      * Monitoring data is granular down to each stage.

      * Analyze the download speed of each domain based on monitoring data to help optimize domain acceleration.

   * Runtime performance

      * Provide LongTask monitoring and corresponding processing

      * Supports user behavior monitoring by displaying time consumption waterfall charts and user behavior funnels. This enables you to understand performance related to user actions, assess users’ runtime performance experience when using the site, and guide runtime performance optimization.

* Analytical data

   * Provides standard monitoring data to help understand the site's user data, reconstruct the action path of an individual user, and understand user conversion.


<span id=".5LyY5Yq_"></span>
## Advantages


* **Low\-cost access**

   SDK integration is non\-intrusive; you can successfully integrate it by simply adding initialization code.

* **Flexible sampling methods**

   Supports sampling for all reported fields, filtering with various operators, and combining sampling conditions using logical AND and OR, in order to reduce costs.

* **Comprehensive use of scenarios**

   Supports multi\-page applications, single\-page applications, micro\-frontend applications, and cross\-platform applications.

* **An easier\-to\-extend SDK**

   * A variety of lifecycles supports more flexible modification.

   * Supports multiple instances. Multiple monitoring instances can be introduced on the same page without conflicts.

   * Monitoring items are plugin\-based, are pluggable, can be integrated as needed, and support user customization.

   * Provides global identifiers such as release, env, and viewod; enables comparison of data between different versions to assess their respective strengths and weaknesses; supports isolated data consumption across different environments; and collects various types of reported data throughout a single page lifecycle, thereby providing a basis for performance optimization and troubleshooting.

* **Higher performance**

   * After the SDK has been optimized for performance, its impact on page performance is so minimal that it can be ignored.


<span id=".55uR5o6n6IO95Yqb5qaC6KeI"></span>
## Monitoring capabilities overview


|**Application scenarios** |**Feature entry point** |**DescriptionS** |
|---|---|---|
|Troubleshoot JS errors |[JS monitoring overview](https://docs.byteplus.com/en/docs/apmplus/JS_monitoring) |* Observe specific error details, check stack details, and observe version distribution and reporting trends.<br><br>* Navigate to the Data Exploration and Observation page. Combine specific user context, breadcrumbs, and other information to identify the method by which the issue is triggered. |
||[List of pages](https://docs.byteplus.com/en/docs/apmplus/Page_List) |* Filter pages with a high error rate or error count, then go to the page details to review the JS metrics for that page.<br><br>* Observe specific error details, check stack details, and observe version distribution and reporting trends.<br><br>* Navigate to the data exploration and observation view, and use specific user context, breadcrumbs, and other factors to identify the method by which the issue was triggered. |
||[JS error alert configuration](https://docs.byteplus.com/en/docs/apmplus/alert_management_webpro) |* When an alert occurs, related JavaScript errors are identified through intelligent attribution analysis.<br><br>* View error details and navigate to Data Exploration to inspect specific reports. |
||[Query metrics](https://docs.byteplus.com/en/docs/apmplus/custom_dashboard) |If you want to analyze the overall distribution, trends, and grouping of certain error indicators under specific conditions, you can combine indicator queries to generate dashboards and continuously monitor them. |
|Observe and improve the page performance |[Performance overview](https://docs.byteplus.com/en/docs/apmplus/performance_monitor) |* Select site performance metrics to observe the current Web Vitals performance trends and how they are distinguished by benchmark lines for the entire site.<br><br>* Observe the pages with the poorest current performance across all metrics, as well as the pages whose performance across all metrics has deteriorated the most compared to the previous time period.<br><br>* Go to the page details and observe the specific metrics.<br><br>* Navigate to Data Exploration Observation. |
||[Page list](https://docs.byteplus.com/en/docs/apmplus/Page_List) |* Sort and filter pages by specific performance metrics to identify those with more severe performance issues, then go to the page details to review its performance metrics.<br><br>* For the metrics you are interested in, navigate to data exploration to observe them, and then analyze potential performance bottlenecks by combining specific user context, timing, and longtask information. |
||[Performance alerts](https://docs.byteplus.com/en/docs/apmplus/alert_management_webpro) |* When an alarm occurs, use intelligent attribution analysis to identify related pages with relatively poor performance.<br><br>* Click the attribution link to go directly to the corresponding page details, where you can view specific metrics and navigate to data exploration to view specific reported data. |
|Check data on request errors |[Overview of requests](https://docs.byteplus.com/en/docs/apmplus/request_monitor) |* View request trends and view the overall status of site request monitoring.<br><br>* The All Requests page is mainly used to examine the overall status and duration of page requests. |
||[Request list](https://docs.byteplus.com/en/docs/apmplus/request_monitor) |* Aggregate the request list based on the request's domain name and path.<br><br>* Supports sorting by different criteria. After selecting the corresponding path, you can view detailed information about the current path.<br><br>* Trends and distribution: view Timing information and the distribution of request durations. |
|Check error data for static resources |[Overview of static resources](https://docs.byteplus.com/en/docs/apmplus/resources_monitor#0168b14d) |* View static resource request trends. View the overall status of site static resource request monitoring.<br><br>* This page displays all static resource requests, primarily for examining the overall status and duration of page static resource requests. |
||[List of static resources](https://docs.byteplus.com/en/docs/apmplus/resources_monitor#f2a77336) |* The static resource list uses the combination of the requested domain name and path as the aggregation dimension.<br><br>* You can sort by different criteria. After selecting the corresponding path, you can view detailed information about the current path.<br><br>* Trends and distribution: view timing information and its distribution for static resource requests. |
|The page crashes or becomes extremely slow under certain conditions. |[Data exploration](https://docs.byteplus.com/en/docs/apmplus/data_explore) |To troubleshoot specific issues, view the user's complete reporting information based on the user_id or session_id. |
|Define performance metrics for your specific circumstances |[Project settings](https://docs.byteplus.com/en/docs/apmplus/project_setting#.5oCn6IO95oyH5qCH5Z-65YeG57q_) |Configure metric baselines for the metrics you are interested in. |
|Filter data by the version dimension |\- |1. Integrate by following the R&D process, and complete the configuration and conceptual understanding for both the version and the corresponding R&D process.<br><br>2. You can directly filter data by release and env on the platform. |


<span id=".5YW45Z6L5Zy65pmv"></span>
## Typical scenarios

<span id=".5o6S5p-lSlPplJnor68="></span>
### Troubleshoot JS errors

JavaScript errors are often related to abnormal code execution and require prompt attention. The browser provides the ability to catch exceptions. However, catching exceptions is only the first step; it is even more important to quickly locate the problem. The Webpro client provides stack parsing and exception aggregation features to help you efficiently resolve issues and statistically track the progress of issue resolution.

<span id=".6KeC5a-f5bm25pS56L-b6aG16Z2i5oCn6IO9"></span>
### Observe and improve page performance

The main problem addressed by page performance optimization is how to optimize user\-centric key metrics. Different metrics use different calculation methods and focus on different dependencies, so the optimization methods also differ. As long as you clearly understand the dependencies of the metrics, just focus on optimizing them and that will suffice. As the data for dependencies gradually improves, metrics can be quickly optimized.

**Data exploration**

<span id=".5Z-65pys5qaC5b-1"></span>
## Glossary

Certain terms are defined in WebPro\-side monitoring and are frequently referenced and used in documentation and daily platform usage.


|**Glossary** |**DescriptionS** |
|---|---|
|aid |The Application ID is the globally unique identifier for the project. It must remain consistent across the SDK and platform, but unlike the common APP_ID, it does not require a dedicated application process; you only need to ensure that it does not duplicate the AID of any existing project. |
|pid |The ID that marks a specific page in your application can be used on the platform to filter, group, and view data. You also specify this in the relevant SDK configuration. By default, the SDK sets the PID to the URL of the current page. For activity pages or pages with a unique ID, it is recommended that you configure your own aggregation policy in the SDK. |
|user_id |Indicates the ID of the current visiting user. The user_id is used to calculate unique visitors, affected user count, and other related information. You can specify the user ID yourself. By default, the system automatically generates a uuid for you and stores it in localstorage. |
|session_id |The ID that identifies a session. A "session" refers to the entire period from when a user enters the page until they close the page. The session_id is used to calculate site\-wide metrics such as page views, error rate, and more, and is also used for deduplication counting in reporting. You do not need to specify the `session_id` yourself; the system will generate it for you. |
|view_id |An ID that marks a single page visit. In scenarios such as SPA, a page visit is a subset of a session, and a single session may include multiple page visits. This ID is used to calculate the page views (PV) for a single PID and to link related static resources, requests, and Longtask reports. |
|env |This field is used to distinguish reporting environments. By specifying different env values in the SDK, data can be grouped by environment, preventing contamination between online and offline environments. |
|Indicator baselines |WebPro provides baseline settings for all collected metrics, such as performance metrics, error metrics, and so on. By setting good\-base\-line and bad\-base\-line, you can quickly identify the current status of your site or page and further perform targeted optimization. |


<span id=".5o6l5YWl5rWB56iL"></span>
## The integration process

<span id="API"></span>
## API

WebPro Monitoring provides OpenAPI interfaces for alarm, white screen monitoring, custom monitoring, and related services. For details, refer to [API Overview](https://docs.byteplus.com/en/docs/apmplus/Available_APIs_webpro).
