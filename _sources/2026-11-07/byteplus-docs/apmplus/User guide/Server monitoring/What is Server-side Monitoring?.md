---
title: "What is Server-side Monitoring?"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/What_is_server_monitoring"
---

Server\-side Monitoring provides end\-to\-end backend monitoring capabilities, covering infrastructure resource performance, service/code\-layer observability, and application runtime health.

<span id=".5pyN5Yqh56uv55uR5o6n6K-05piO"></span>
## Introduction to Server\-side Monitoring

The Server\-side Monitoring module of APMPlus is an end\-to\-end backend monitoring service for server\-side applications. It provides unified monitoring from infrastructure resource performance to service and code layers and to the runtime health of online applications.

Server\-side Monitoring adopts a non\-intrusive instrumentation solution and requires only simple configuration on the server to complete integration.

<span id=".5LyY5Yq_"></span>
## Advantages


* **Low integration cost with non\-intrusive SDKs**

   * It provides non\-intrusive integration for common Java and Python frameworks to reduce costs.

   * SDK and agent resource consumption, as indicated by performance testing, is lower than that of open\-source alternatives.

   * Agents support multiple deployment and installation methods, including Yum and apt\-get, which further improves integration efficiency.

*  **‌Advanced anomaly tracing and analysis**

   Extensive anomaly tracing and analysis capabilities are available, including but not limited to stack tracing, log capture, scheduling analysis, tombstone analysis, and user interaction replay.

* **Flexible, cost\-saving sampling methods**

   You can use multiple sampling configurations (module\-specific or user\-based sampling configurations) to reduce event volume.

* **Custom error reporting**

   In addition to collecting common anomalies, custom errors can be reported, enabling a more comprehensive analysis of application anomalies.

* **Custom instrumentation support**

   Multiple custom instrumentation capabilities are provided to support flexible and in\-depth event tracking, as well as lightweight, simple front\-end custom instrumentation.

* **Technical optimization support**

   The expert team with extensive experience in optimizing applications with hundreds of millions of users are ready to deliver technical solutions that optimize your application quality and performance with platform\-provided capabilities.


<span id=".55uR5o6n6IO95Yqb5oC76KeI"></span>
## Overview of monitoring capabilities

Currently, Server\-side Monitoring provides the following monitoring capabilities.


|**Category** |**Feature** |**Description** |
|---|---|---|
|Dashboards |[Host performance](https://docs.byteplus.com/en/docs/apmplus/Performance_profiling) |Preset host performance dashboard. It displays trend charts for host machine load, CPU usage, and memory usage. |
||[Disks](https://docs.byteplus.com/en/docs/apmplus/Operating_system_dashboard) |Preset disk performance dashboard. It displays trend charts for iowait, IO latency, read/write throughput, and read/write QPS. |
||[Platform self-monitoring](https://docs.byteplus.com/en/docs/apmplus/Operating_system_dashboard) |Preset platform self\-monitoring dashboard. It displays trend charts for backend data receiving services and server agents. |
||[Custom dashboard](https://docs.byteplus.com/en/docs/apmplus/Custom_dashboard) |You can configure custom dashboards. |
|[Basic monitoring](https://docs.byteplus.com/en/docs/apmplus/Basic_monitoring) |Host monitoring |Displays a list of hosts and their operational status, CPU utilization, IO, and load information. |
||Docker monitoring |Displays a list of containers and their details, such as status, host name, image, CPU utilization, memory usage rate, startup time, and creation time. |
||Process monitoring |Displays a list of processes and their details such as startup user, host name, CPU utilization, memory usage rate, creation time, and end time. |
|[Logs](https://docs.byteplus.com/en/docs/apmplus/Log_monitoring) |Log queries |Provides log consumption capabilities and supports log clustering and log search. |
|[Service Overview](https://docs.byteplus.com/en/docs/apmplus/Service_monitoring) |Service list |Displays the complete list of services with their details including service type, operational status, error rate, QPS, latency, CPU utilization, memory usage, and last monitored time. |
||Service topology |Displays a global service topology map that reflects the cross\-service call relationships. It enables rapid analysis of overall service architecture and upstream/downstream call dependencies and provides real\-time monitoring of call success rates between services to help promptly identify faulty services. |
||Service integration |Provides instructions on integration using various programming languages. You can refer to the integration instructions to integrate monitoring capabilities. |
|[Middleware monitoring](https://docs.byteplus.com/en/docs/apmplus/Middleware_monitoring) |Middleware overview |Aggregates statistics of service access to middleware components, providing unified observability from the middleware perspective to streamline troubleshooting for middleware operators. |
|[Trace analysis](https://docs.byteplus.com/en/docs/apmplus/Trace_analysis) |Trace analysis |Enables real\-time retrieval of span information (such as service calls) with multi\-dimensional filtering and sorting for rapid error/slow query diagnosis. You can click a TraceID to view the complete request path. It is used to locate and troubleshoot single\-point issues. |
||Single trace query |Provides single\-point tracing and diagnosis capabilities. You can query the complete call trace of a single request by specifying its TraceID. Connecting to a log repository allows you to link all logs throughout the entire trace. You can use it to quickly locate and troubleshoot single\-point issues. |
|**Global analysis** |Custom Metrics |Displays reported custom metrics and their custom dimensions. You can search for and filter metrics and easily switch to the visual query interface. |
||Visual query |Visualizes the time trends for a given metric in a chart. It reflects metric changes over time. |
|[Error tracing](https://docs.byteplus.com/en/docs/apmplus/error_analytic) |Error analysis |Collects service anomlies and errors and aggregates and classifies them to help you analyze errors. |
|[Alert management](https://docs.byteplus.com/en/docs/apmplus/Alert_tasks) |Alert tasks |Adds and manages alert tasks. Alert tasks detect metric values or watchdog events, and when conditions are met, send alert notifications to O&M personnel so that they handle issues promptly. These tasks help O&M personnel quickly locate and troubleshoot issues. |
||Alert history |Records historical alerts. |
|**Platform setting** |Receiver group management |Manages alert receiver groups. |
||Parameter configuration |Allows you to adjust various platform parameter configurations. |


<span id=".5o6l5YWl5rWB56iL"></span>
## Integration workflow

You can refer to the following integration workflow diagram to preliminarily understand how to integrate Server\-side Monitoring. For detailed integration steps, see [Integrating Server-side Monitoring](https://docs.byteplus.com/en/docs/apmplus/How_to_integrate_server-side_monitoring).

<span id="API"></span>
## API

Server\-side Monitoring also provides OpenAPI interfaces for capabilities such as alert management, alert group management, and metric queries.
