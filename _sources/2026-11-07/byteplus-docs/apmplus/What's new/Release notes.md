---
title: "Release notes"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Release_notes"
---

This topic describes the release notes for APMPlus features. New features will be rolled out across regions. We are looking forward to your hands\-on experience.

> **tip**

* > The **Regions** column lists the regions where the feature change applies at the time of the release. The actual supported regions are subject to those displayed in the console. In this column, **All** refers to all regions where the service is available. For details, see [Server\-launching region](https://docs.byteplus.com/en/docs/apmplus/server-launching_region).

## October 2026

|**Module** |Feature |**Description** |Regions |**Related document** |
|---|---|---|---|---|
|Server\-side Monitoring |Trace analysis |Supports specifying custom filter fields displayed on the filter panel. You can add or remove fields as needed and restore the default system configuration with a few clicks. |All |[Trace analysis](https://docs.byteplus.com/en/docs/apmplus/Trace_analysis) |

## September 2026

|**Module** |Feature |**Description** |Regions |**Related document** |
|---|---|---|---|---|
|Server\-side Monitoring |Trace association configuration |Adds the trace correlation configuration feature, which maps Span fields to logs in TLS. After the configuration, you can be directly redirected to the corresponding logs from the Trace details page with a few clicks. This helps you quickly pinpoint the root cause. |All |[Trace association configuration](https://docs.byteplus.com/en/docs/apmplus/Trace_correlation_configuration) |
|Server\-side Monitoring |Middleware monitoring |DynamoDB is supported. After integration, you can view DynamoDB call relationships and performance metrics. This helps you quickly identify abnormal nodes and affected traces, improving access troubleshooting efficiency. |All |[Middleware monitoring](https://docs.byteplus.com/en/docs/apmplus/Middleware_monitoring?lang=en) |
|Server\-side Monitoring |Topology analysis |Service topology supports configuring color thresholds based on metrics. With color threshold settings in place, topology nodes are rendered in real time with corresponding colors based on current metric values. This allows you to quickly identify abnormal performance nodes despite complex dependency relationships and shorten the fault location path. |All |[Service monitoring](https://docs.byteplus.com/en/docs/apmplus/Service_monitoring) |

## August 2026

|**Module** |Feature |**Description** |Regions |**Related document** |
|---|---|---|---|---|
|Server\-side Monitoring |Topology analysis |Call relationships can be displayed from two dimensions: service topology and interface topology, with shortcut navigation entries provided. This helps you identify abnormal nodes and affected traces more quickly. |All |[Service monitoring](https://docs.byteplus.com/en/docs/apmplus/Service_monitoring) |

## July 2026

|**Module** |Feature |**Description** |Regions |**Related document** |
|---|---|---|---|---|
|Server\-side Monitoring |Performance profiling |The performance profiling feature is now available. This feature continuously collects and analyzes CPU performance data associated with pods, precisely identifying CPU hotspot functions. This addresses the limitation of metrics and traces that can only locate abnormal interfaces, enabling function\-level root cause analysis. |All |* [Performance profiling](https://docs.byteplus.com/en/docs/apmplus/Performance_profiling?TagIDs=2,237&lang=en&type=preview)<br><br>* [Parameter management](https://docs.byteplus.com/en/docs/apmplus/parameter_management) |
|Server\-side Monitoring |Workspace\-level IAM permission control |Server\-side Monitoring supports fine\-grained control over the permission scope of IAM users based on workspaces. |All |[Workspace-level IAM permission control](https://docs.byteplus.com/en/docs/apmplus/Workspace-level_IAM_permission_control) |

## May 2026

|**Module** |Feature |**Description** |Regions |**Related document** |
|---|---|---|---|---|
|Server\-side Monitoring |Probe settings |Adds two API configurations: invalid API call filtering and HTTP status code allowlist. Data reporting includes metric data reporting, log data reporting, and trace data reporting. |All |[Parameter management](https://docs.byteplus.com/en/docs/apmplus/parameter_management) |
|Server\-side Monitoring |Workspace management |Server\-side Monitoring supports workspaces for data management and isolation. Each workspace has independent data reporting credentials and can centrally manage traces, logs, and metrics for different application ownership scenarios. |All |[Workspace management](https://docs.byteplus.com/en/docs/apmplus/Workspace_management) |
|Server\-side Monitoring |Custom dashboard |The creation of custom dashboards for application performance monitoring is prohibited. To use dashboards for insight analysis, we recommend going to [Custom dashboard](https://console.byteplus.com/observe/dashboard/dashboard). |All |[Custom dashboard](https://docs.byteplus.com/en/docs/apmplus/Custom_dashboard) |
|General |Root Span list |A Root Span list is displayed in the Trace analysis module. All Root Span\-related Traces and Trace\-related details within the specified filter range are displayed. |All |* [Server-side Monitoring Trace Analysis](https://docs.byteplus.com/en/docs/apmplus/Trace_analysis)<br><br>* [AI Application Trace Analysis](https://docs.byteplus.com/en/docs/Observability_Platform/LLM_trace_analysis)<br><br>* [AgentKit trace analysis](https://docs.byteplus.com/en/docs/Observability_Platform/Trace_analysis) |

## April 2026

|**Module** |Feature |**Description** |Regions |**Related document** |
|---|---|---|---|---|
|Server\-side Monitoring |Official release of the Asia Pacific (Jakarta) region |The Server\-side Monitoring service is officially available for sale in the Asia Pacific (Jakarta) region. To ensure stability and fault tolerance, we recommend selecting the region where the target resource is deployed to reduce network latencies and accelerate access. |Asia Pacific (Jakarta) |[[Product update] Official release of Server-side Monitoring in the Asia Pacific (Jakarta) region](https://docs.byteplus.com/en/docs/apmplus/APMPlus_is_now_available_in_the_Jakarta_region) |

## March 2026

|**Module** |Feature |**Description** |Regions |**Related document** |
|---|---|---|---|---|
|Server\-side Monitoring |Official release of the China (Hong Kong) region |The Server\-side Monitoring service is officially available for sale in the China (Hong Kong) region. To ensure stability and fault tolerance, we recommend selecting the region where the target resource is deployed to reduce network latencies and accelerate access. |China (Hong Kong) |[[Product update] Official release of Server-side Monitoring in the China (Hong Kong) region](https://docs.byteplus.com/en/docs/apmplus/APMPlus_officially_available_in_Hong_Kong_region) |
|Server\-side Monitoring |Trace‑based metric generation |The system can aggregate trace data of a specified application cluster based on production metric rules, dynamically generate high\-value metrics, and address challenges such as occasional errors that are difficult to capture and quantify, as well as the inability to track experience data for specific business scenarios over the long term.<br><br>Additionally, you can quickly integrate generated metric data into custom dashboards for visualization or configure alert rules to enable real\-time detection of anomalies in seconds, eliminating monitoring blind spots at the source. |All |[Production metrics](https://docs.byteplus.com/en/docs/apmplus/Tag_cardinality_limit) |
|Server\-side Monitoring |Disabling TLS |Supports the global switch for TLS. You can disable or enable TLS based on your business requirements.<br><br>> **danger**<br><br><br>> If you disable TLS, historical log data and log topics are simultaneously deleted. After deleted, the data cannot be recovered. Proceed with caution.<br> |All |[Parameter management](https://docs.byteplus.com/en/docs/apmplus/parameter_management) |
|Server\-side Monitoring |Instance\-level metric analysis |Collects and monitors information attributed to service Pods, hosts, containers, and other objects. Provides instance‑level metric analysis, such as process statistics, RED metrics, host monitoring, container monitoring, runtime monitoring, process metrics, connection pool monitoring, and thread pool monitoring. |All |[Service monitoring](https://docs.byteplus.com/en/docs/apmplus/Service_monitoring) |
|Server\-side Monitoring |A trace analysis redirect URL is added to the Service overview page. |Adds panel links or data links to the monitoring charts for overview, requests, latency, errors, and logs on the Service overview page. You will be redirected to the Trace analysis page associated with the current service after clicking a link. |All |[Service monitoring](https://docs.byteplus.com/en/docs/apmplus/Service_monitoring) |
|Server\-side Monitoring |Alert trigger condition supports configuration of time interval |The time interval in the alert trigger condition is changed from the default 30 seconds to a custom time interval. When the time interval in the alert trigger condition matches that of API monitoring, consistency between alert messages and the data in API monitoring can be ensured. |All |[Alert task](https://docs.byteplus.com/en/docs/apmplus/Alert_tasks) |
|Server\-side Monitoring |Span export |Offline Span data can be exported to the agent evaluation platform. |China (Beijing)<br><br>China (Shanghai) |[Span export](https://docs.byteplus.com/en/docs/apmplus/Span_export) |

## February 2026

|**Module** |Feature |**Description** |Regions |**Related document** |
|---|---|---|---|---|
|Server\-side Monitoring |New monthly free quota |In the pay‑as‑you‑go billing model based on written data volume, a promotional offer is introduced. It provides a monthly free quota for traces and metrics. Charges apply only when usage exceeds the monthly free quota, based on the standard billing rates. |All |[[Billing update] Server-side Monitoring offers a new monthly free tier](https://docs.byteplus.com/en/docs/apmplus/Application_Performance_Monitoring_introduces_free_quota) |

## January 2026

|**Module** |Feature |**Description** |Regions |**Related document** |
|---|---|---|---|---|
|Server |Preset alert templates |The system provides multiple common preset alert templates for common services and AI services. This enables you to create alert tasks quickly by using preset alert templates and monitor the health status of your services in real time. |All |[Application preset alert templates](https://docs.byteplus.com/en/docs/apmplus/Alert_templates) |
|Server |Service overview |Optimizes the Service overview dashboard. In addition to the existing basic metric trends, the dashboard now adds two new chart types: overview charts and ranking lists. It also adds overall statistics for golden metrics and Top 5 APIs based on the request count, error count, and average response time. This helps you quickly detect abnormal service fluctuations. |All |[Service monitoring](https://docs.byteplus.com/en/docs/apmplus/Service_monitoring) |
|Server |Production metrics |The system can aggregate log data of a specified application cluster based on production metric rules, dynamically generate high\-value metrics, and address challenges such as occasional errors that are difficult to capture and quantify, as well as the inability to track experience data for specific business scenarios over the long term.<br><br>In addition, the generated metric data can be quickly integrated with a custom dashboard for visual monitoring, or alert rules can be configured to achieve second\-level awareness of exceptions, quickly resolving monitoring blind spots at the source. |All |[Production metrics](https://docs.byteplus.com/en/docs/apmplus/Tag_cardinality_limit) |
|Server |Sampling settings |Optimizes the data collection configuration. You can configure either fixed sampling or failed or slow request sampling rules based on actual business conditions. |All |[Sampling settings](https://docs.byteplus.com/en/docs/apmplus/parameter_management) |
|Server |Interface settings |Adds an API configuration section on the Parameter management page. It allows you to configure path convergence and the RPC service API list based on actual conditions. The system generates HTTP service API names based on the actual URL by using the default URL convergence rules, aggregating relative paths. |All |[Interface settings](https://docs.byteplus.com/en/docs/apmplus/parameter_management) |
|Client |Release of Flutter module alternative |APMPlus allows you to report and monitor custom errors, custom events, custom logs, and other monitoring data related to Flutter applications via the Flutter‑Native bridge. |All |* [[Product update] Release of Flutter module alternative](https://docs.byteplus.com/en/docs/apmplus/Flutter_module_replacement_solution_released)<br><br>* [Integrating APMPlus native SDKs with Flutter using the bridge](https://docs.byteplus.com/en/docs/apmplus/APMPlus_Flutter_bridge_native_SDK_integration_guide) |

## December 2025

|**Module** |Feature |**Description** |Regions |**Related document** |
|---|---|---|---|---|
|Server |Alert tasks support associating projects and tags |The alert task supports associating projects and tags. Resources can be grouped and managed by project or tag. In addition, resource bills can be viewed from the project or tag perspective, helping users calculate cloud resource usage costs. |All |[Creating alert tasks](https://docs.byteplus.com/en/docs/apmplus/Alert_tasks) |
|Server |Summary of integration\-related configuration information |Provides a detailed description of the methods to obtain the configurations required for application integration, including information about AppKey, annotation, and endpoint. |All |[How to use the Integration center](https://docs.byteplus.com/en/docs/apmplus/How_to_use_the_access_center) |

## November 2025

|**Module** |Feature |**Description** |Regions |**Related document** |
|---|---|---|---|---|
|Server |Data encryption |For data stored in TLS, two data encryption methods are provided: service key (SSE\-TLS) and user key (SSE\-KMS). You can select an appropriate method based on your business requirements to ensure data security. |All |[Storage configuration](https://docs.byteplus.com/en/docs/apmplus/parameter_management) |
|Server |Chart grouping by instance |For data integrated through the Skywalking monitoring system, the data charts in the service overview, API monitoring, downstream call, and upstream call modules support grouping by instance. |All |None |
|AI scenario |Span export |The span export feature is provided for AI\-related applications. You can export span information for other in\-depth analysis.<br><br>Two methods are available for exporting Span data: exporting Span data to a local file or to a CozeLoop evaluation set. |All |[Span export](https://docs.byteplus.com/en/docs/apmplus/Span_export) |
|Server |Trace performance analysis |View the list of aggregated traces of service interfaces that meet the filtering conditions within a specified time period. With collected duration\-related data of each node in the traces, the duration distribution is visually displayed with the trace duration list provided, helping users quickly locate performance bottlenecks. |All |[Trace analysis](https://docs.byteplus.com/en/docs/apmplus/Trace_analysis) |
|Server |Trace error propagation chain analysis |View the list of aggregated traces of service interfaces that meet the filtering conditions within a specified time period. With the obtained possible sources of propagation for error nodes and impacts on upstream and downstream nodes, error impact analysis and source analysis are visually displayed, helping users quickly analyze error propagation paths. |All |[Trace analysis](https://docs.byteplus.com/en/docs/apmplus/Trace_analysis) |
|Server |Customizing dashboards by using the Grafana add\-on |Server\-side Monitoring provides a Grafana add\-on for integrating with the data source of the open\-source software Grafana. Data can be displayed in a custom dashboard through the Grafana add\-on. |China (Beijing) |[Customizing dashboards by using the Grafana add-on](https://docs.byteplus.com/en/docs/apmplus/Customize_dashboards_using_the_Grafana_plugin) |
|Server |Alert management supports AI metrics |Metrics related to runtime and AI for the alert management module are added. You can create alert tasks for these metrics to monitor exceptions in the parameter metrics of the target service and promptly receive notifications. |All |[Creating alert tasks](https://docs.byteplus.com/en/docs/apmplus/Alert_tasks) |

## October 2025

|**Module** |Feature |**Description** |Regions |**Related document** |
|---|---|---|---|---|
|Client |Client IAM permission management |RUM uses IAM to control access permissions of different identities. |All |[Client IAM permission management](https://docs.byteplus.com/en/docs/apmplus/Client_IAM_permission_management) |
|Client |Project association |When you enable the RUM feature, you can specify custom associated projects. They can be used for bill splitting and other scenarios. |All |* [Creating client applications](https://docs.byteplus.com/en/docs/apmplus/Create_a_client_application)<br><br>* [Enabling RUM](https://docs.byteplus.com/en/docs/apmplus/Activate_client_monitoring) |
|Mini Pro Monitoring |Data export in data explore |The data explore module supports data export. This helps users export data for offline analysis. |All |[Data exploration](https://docs.byteplus.com/en/docs/apmplus/data_explore_minipro) |
|Observability dashboard |Custom observability dashboards support the TLS data source |Custom observability dashboards support integration, display, and analysis of TLS\-related data, helping users fully understand the system operating status and quickly locate issues. |All |[Data query](https://docs.byteplus.com/en/docs/apmplus/Data_queries) |

## September 2025

|**Module** |Feature |**Description** |Regions |**Related document** |
|---|---|---|---|---|
|General |Product release |APMPlus is available in BytePlus for the first time. |Asia Pacific (Johor) |None |
