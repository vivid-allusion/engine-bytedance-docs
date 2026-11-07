---
title: "What is RUM?"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/What_is_App_Monitoring"
---

RUM provides comprehensive mobile app monitoring capabilities and also supports Native and hybrid monitoring.

## RUM description

iOS and Android monitoring support the collection, restoration, and analysis of various on\-site data. It also covers comprehensive performance analysis, enabling precise tracing of root causes to help developers resolve issues efficiently. In addition, it supports reporting custom exceptions and custom logging metrics.

## Advantages

* **Lower integration costs, non\-intrusive SDK**

   Most app\-side features can be integrated non\-intrusively, and it also supports JS SDK injection.

*  **‌Advanced anomaly tracing and analysis**

   Extensive anomaly tracing and analysis capabilities are available, including but not limited to stack tracing, log capture, scheduling analysis, tombstone analysis, and user interaction replay.

* **Flexible, cost\-saving sampling methods**

   You can use multiple sampling configurations (module\-specific or user\-based sampling configurations) to reduce event volume.

* **Custom error reporting**

   In addition to collecting common anomalies, custom errors can be reported, enabling a more comprehensive analysis of application anomalies.

* **Supports custom logging**

   It provides various custom logging features to meet different scenarios, including flexible event tracking for in\-depth analysis and lightweight, simple front\-end custom logging.

* **Provides technical optimization solutions**

   The expert team with extensive experience in optimizing applications with hundreds of millions of users are ready to deliver technical solutions that optimize your application quality and performance with platform\-provided capabilities.

## Feature overview

This topic provides an overview of all features of app\-side monitoring.

|**Category** |**Feature** |**Description** |
|---|---|---|
|[Crash analysis](https://docs.byteplus.com/en/docs/apmplus/Crash_analyses) |[Crash trends](https://docs.byteplus.com/en/docs/apmplus/Crash_analyses) |Supports the collection and analysis of various crash types on both iOS and Android, enabling more precise resolution. |
||[Crash rankings](https://docs.byteplus.com/en/docs/apmplus/Crash_analyses) |Supports detailed crash rankings for both iOS and Android, recording crash counts, crash rates, number of affected users, and the proportion of affected users. |
||[App exit causes](https://docs.byteplus.com/en/docs/apmplus/Crash_analyses) |Supports analyzing the exit causes of Android apps, providing on\-site data, tracking logs, and other auxiliary information to help analyze why the app exited. |
|[Lag analysis](https://docs.byteplus.com/en/docs/apmplus/Lag_analysis) |Lag trends |Monitor whether main thread messages time out to analyze smoothness issues that occur when users are using the app. |
||Lag ranking |Supports detailed lag rankings for both iOS and Android, recording lag counts, lag rates, number of affected users, and the proportion of affected users. |
||Lag tree |Stack traces are aggregated, with each node representing a method, allowing you to analyze from a macro perspective which node suffers lags more intensively. |
|[Event analysis](https://docs.byteplus.com/en/docs/apmplus/Event_analytics) |Event trends |In addition to built\-in metrics, it also supports reporting custom metrics, which corresponds to the event analysis feature. For events added through event management, you can analyze their metrics via event trends. |
||Event management |Add events. Set event information and sampling rates through forms. |
|[Battery analysis](https://docs.byteplus.com/en/docs/apmplus/Power_consumption_analysis) |Battery metrics |View Android Foreground current value and battery temperature. |
||Power\-consuming factors |Preliminary attribution of the application's power consumption has been performed. |
||Battery anomalies |Monitors three metrics: the duration of obtaining Location, the number of AlarmManager settings, and the duration of WakeLock wake\-ups. Exceeding the thresholds is considered abnormal power consumption. |
|[User experience](https://docs.byteplus.com/en/docs/apmplus/User_experience) |Startup analysis |Learn about the time\-consumption data during the app startup by viewing trend charts and distribution charts of startup\-related metrics. |
||Native page experience |Learn about the page experience metrics of the app and locate anomalies by analyzing page response latency, page lag, and lag\-related crashes. |
|[Dashboards](https://docs.byteplus.com/en/docs/apmplus/daily_trend) |Real\-time statistics |Provides dashboards that auto\-refresh in real time, including statistics on commonly used core metrics and alert statuses. |
||Daily trends |View trend charts of core metrics on a daily basis. |
||Custom dashboard |Customize the metrics in the dashboard according to business requirements. |
||Dashboard subscription |Receive dashboard updates periodically through the configured subscription method. |
|Single\-point tracing |[Log queries](https://docs.byteplus.com/en/docs/apmplus/log_query) |Perform single\-point tracing based on detailed logs collected by RUM according to DID, UUID, SSID, and UserID. |
||[Log retrieval](https://docs.byteplus.com/en/docs/apmplus/Recovery) |The platform sends a command to a specified user to retrieve logs and upload the custom log information, helping developers to conduct targeted investigations and locate issues. It can also be configured to upload automatically upon a crash.<br><br><br>* iOS and Android: Support log retrieval and custom log retrieval.<br><br>* Harmony: Only supports log retrieval. |
||[Custom logs](https://docs.byteplus.com/en/docs/apmplus/Custom_log) |Files automatically uploaded through the APIs exposed by the SDK, logs reported with crashes, and logs retrieved can all be queried here. |
|[MetricKit](https://docs.byteplus.com/en/docs/apmplus/MetricKit) |Stability |MetricKit's exception monitoring capabilities, including crash, CPU anomaly, lag, and disk monitoring. |
|[Exception protection](https://docs.byteplus.com/en/docs/apmplus/iOS_crash_protection) |Crash protection |Provides crash protection for iOS to effectively prevent apps from exiting unexpectedly The statistics on the page represent exceptions captured by crash protection. Developers need to fix these issues. |
|[Network analysis](https://docs.byteplus.com/en/docs/apmplus/Network_analytic) |HTTP |View metrics such as the overall latency and success rate of network requests. |
||DNS |Provides the ability to analyze the distribution ranking and trend charts of average DNS latency. |
|[Memory optimization](https://docs.byteplus.com/en/docs/apmplus/Memory_optimization) |OOM trends |View metrics and trends for OOM errors. |
||Leak analysis |View the list of object types causing leaks and detailed analysis. |
||Large objects |View large objects that consume excessive memory, as well as numerous small objects aggregated together. |
||Single\-device memory details |Directly analyze memory issues on a single device. |
|[CPU monitoring](https://docs.byteplus.com/en/docs/apmplus/CPU_monitoring) |CPU metrics |View the two core metrics: CPU utilization and the max CPU utilization. |
||CPU anomalies |CPU anomalies occur when apps continuously consume a large amount of CPU resources in the foreground or background. A continuously high CPU utilization will lead to rapid battery drain and cause mobile phones to overheat. This requires focused monitoring and optimization. |
|[Disk monitoring](https://docs.byteplus.com/en/docs/apmplus/disk_monitor) |Disk metrics |View the average values of key disk metrics and their reporting volumes. |
||Directory analysis |Analyze which directories and files of the app occupy the largest amount of disk space. |
||Disk anomalies |For abnormal scenarios where the app's disk usage exceeds a specified threshold, analyze current large files and folders, as well as expired files older than a certain period. |
|[Alert management](https://docs.byteplus.com/en/docs/apmplus/alert_management) |Crash alerts |Create and view crash alert tasks. |
||Crash protection alerts |Create and view crash protection alert tasks. |
||Error alerts |Create and view error alert tasks. |
||Lag alerts |Create and view lag alert tasks. |
||Event alerts |Create and view event alert tasks. |
||Page monitoring alerts |Create and view page monitoring alert tasks. |
||Traffic alerts |Create and view traffic alert tasks. |
||Disk alerts |Create and view disk alert tasks. |
||Battery alerts |Create and view battery alert tasks. |
||CPU alerts |Create and view CPU alert tasks. |
|[Platform setting](https://docs.byteplus.com/en/docs/apmplus/Platform_setting) |Receiver group management |Create, edit, and delete recipient groups. |
||Tag management |Create templates and add new tags to modules. |
||SDK reporting configuration |Configure the sampling settings and thresholds for data reported by the SDK on the platform. |
||Platform parameter configuration |Configure platform parameters, including ACK time, slow startup threshold, and single large object definition. |
||Request settings |Define your own services and network request filtering content. |
||Open settings |Configure the webhook address. |
|[H5 monitoring](https://docs.byteplus.com/en/docs/apmplus/HTML5_monitoring) |H5 page list |Provides the ability to view the rankings of key metrics for each H5 page, including PV, UV, JS error rate, request success rate, first paint time, and full page loading time. |
||JS error |It can collect statistics and locate JS errors. |
||H5 request errors |For Ajax request statistics, the error portion is included, allowing analysis of the impact scope and the causes of failed requests. |
||H5 request monitoring |Statistics for all Ajax requests are collected. You can view overall metric statistics to analyze request success rates, request latency, and more. |
||H5 page loading |View various RUM metrics during page loading and technical metrics in the navigation. This helps frontend developers understand the user's real experience during page loading and the specific factors affecting duration. |
|[New H5 monitoring](https://docs.byteplus.com/en/docs/apmplus/New_H5_monitoring) |JS overview |The "JS overview" displays information related to errors occurring in the app and can be filtered by attributes such as browser, device, OS, region, user and access information, and error status. This feature allows you to better understand and observe exceptions occurring at runtime and handle them effectively. |
||Sourcemap management |Provides the ability to manually upload SourceMap files. |
||Request overview |The "Request overview" allows you to view trend charts and lists of all requests and failed requests, helping you locate issues related to request errors and slow requests more quickly. |
||Site performance overview |The performance monitoring page includes two major modules: PID aggregation and metric overview. These help you discover performance issues faster and serve as a basis for page performance optimization. |
||Page list |The page list provides data such as page errors, performance, and requests based on the page dimension, allowing for analysis based on the data of specific pages. |
|File management |Symbol table management |Supports uploading and downloading symbol tables. |
||Sourcemap management |Supports uploading and downloading sourcemap files. |
|Error analysis |Custom errors |View custom error counts, error rates, number of users with errors, proportion of users with errors, and error distribution. |
||Network errors |View the network failure rate, network error categories, and the proportion of network errors for all network requests. |
|Dimension analysis |Regional analysis |Displayed in a map format, it supports viewing the various metrics across provinces and cities, allowing you to quickly identify issues in a particular province or city. |
|Report subscription |Report subscription |Receive reports periodically based on the configured report policy and format. |
|Issue management |Issue overview |View issue overview reports, resolution distribution, exception types, and more. |
||My issues |View issue handling statistics under the account. |

## Glossary

The following summarizes the concepts you may encounter while using RUM, helping you look up and understand related concepts.

|**Noun** |**Description** |
|---|---|
|Event name (eventName/serviceName) |Reported event name.<br><br>String format. Composed of digits, letters, or underscores and cannot start with an underscore or digit. |
|Event metrics |The metrics that correspond to an event. A single event supports multiple metrics. Usually represents the values or data of a type that requires numerical computation and analysis. Example: A page load event named page_duration has an event metric called duration (the time for the first page load). Its value is a value representing a duration (e.g., 34.6s). |
|Event dimensions (dimension/category) |The dimensions that correspond to an event. They enable more precise problem analysis. A single event supports multiple dimensions.<br><br>Usually represents enumerable (discrete) state information. It does not require or support numerical calculation. However, the proportion of a specific dimension value can be calculated. A single dimension can have many dimension values, which can be considered as the discrete values of that dimension. |
|issue |The platform performs aggregation matching based on the crash's key stack information. It aggregates crash information of the same type to generate an issue, facilitating processing by category. Therefore, an issue represents the aggregated form of a certain type of crash information. |
|Period\-on\-period comparison |A comparison of the metrics in the currently selected time period with those in the previous equivalent time window.<br><br>For example, if the current time period is 2022\-04\-08 14:00–15:00 with a metric value of 30, and the previous period\-over\-period time window is 2022\-04\-08 13:00–14:00 with a metric value of 40, then the period\-over\-period result is (30\-40)/40 = \-25%, a decrease of 25%. |
|Custom files |Files automatically uploaded through the APIs exposed by the SDK, logs reported along with crashes, and logs retrieved are all custom files. |
|Lag tree |The Lag Tree aggregates stack traces, with each node representing a method, allowing you to analyze from a macro perspective which node suffers lags more intensively. It also supports adding weights to nodes for more accurate analysis. |
|OOM |OOM (OutOfMemoryError) errors occur when the memory required by the program exceeds the maximum memory range that the virtual machine can allocate. |
|Memory leaks |Memory leaks occur when useless objects (objects no longer in use) continuously occupy memory, or when the memory of those objects is not released as expected, resulting in a waste of memory space. |
|Large objects |A large object refers to **a single object larger than 1000 KB** or **a class with more than 50 instances and a total memory size greater than 10000 KB**. Large objects are the main contributors to memory usage and are a key focus during memory optimization. |

## Integration workflow

## API

The app\-side provides the OpenAPI for events, logs, alerts, and other related business features. By calling these APIs, you can use the corresponding app\-side features. For details, see [API overview](https://docs.byteplus.com/en/docs/apmplus/Available_APIs_app).
