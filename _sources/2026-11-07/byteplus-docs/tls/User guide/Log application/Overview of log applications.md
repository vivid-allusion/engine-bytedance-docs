---
title: "Overview of log applications"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Overview_of_log_applications"
---

This section introduces the concept of log applications in TLS.

<span id="c22fcb12"></span>
## Overview

TLS provides out\-of\-the\-box multi\-scenario analysis applications, delivering a complete solution for rapid reuse and collaborative development. Users do not need to configure log collection, visualization, or tracing rules from scratch. By clicking an application card, users can quickly reuse mature solutions. Once the application is added, a data dashboard can be quickly built for efficient log analysis and insights.

Log applications provide professional data visualization dashboards, covering scenarios such as cloud product observability, large model observability, and basic service monitoring.

<span id="bed3943b"></span>
## Usage limits

Each account can create up to 200 applications by default.

<span id="4c997844"></span>
## Billing information

The log application feature itself does not incur any charges. However, log topics and related data storage, read traffic, data transformation, and log shipping generated through log applications will incur charges. For details, see [Billing overview](https://docs.byteplus.com/docs/tls/billable_items).

<span id="2c299091"></span>
## Feature description

Log applications provide out\-of\-the\-box analysis applications for cloud product observability, large model observability, and basic service monitoring scenarios. Users can easily access multiple monitoring templates, supporting core capabilities such as usage monitoring, performance monitoring, trace analysis, and call chain analysis. Applicable to various data analysis and application scenarios for traces, logs, and more.


|Core advantages |Description |
|---|---|
|Out\-of\-the\-box analysis applications |Resource configuration templates are provided, including data access configuration (enabling cloud product logs/log collection and so on), log topic configuration, index configuration, alert configuration, and more. Users can select and customize applications as needed. |
|Visualization chart capabilities |Provides multiple chart types. Chart data source mappings, axes, legends, and other configurations are preconfigured in the application template, so users only need to associate their own log fields to generate visualizations. |
|Link tracing capability |For distributed systems, preset link topology diagrams, Span duration analysis, and Exception node location rules are provided. You can associate TraceID and SpanID in logs to enable Auto generation of tracing link visualizations. |


Build unified cloud product observability capabilities based on TLS. By correlating logs, metrics, and configuration and measurement data, TLS provides services such as usage analysis, performance monitoring, and access analysis for cloud products, helping to quickly build cloud product observability. Supported applications are as follows:


|Application type |Application name |
|---|---|
|Cloud product observation log application |* [CloudLens for TLS](https://docs.byteplus.com/docs/tls/CloudLens_for_TLS)<br><br>* [CloudLens for EBS](https://docs.byteplus.com/docs/tls/CloudLens_for_EBS)<br><br>* [CloudLens for TOS](https://docs.byteplus.com/docs/tls/CloudLens_for_TOS)<br><br>* [CloudLens for VKE](https://docs.byteplus.com/docs/tls/CloudLens_for_VKE) |
|Large model observation log application |* [OpenClaw Observability](https://docs.byteplus.com/docs/tls/OpenClaw_Observability)<br><br>* [VeADK observability](https://docs.byteplus.com/docs/tls/VeADK_observability) |
|Basic service monitoring log application |* [Trace call chain analysis](https://docs.byteplus.com/docs/tls/Trace_call_chain_analysis)<br><br>* [NGINX access monitoring](https://docs.byteplus.com/docs/tls/NGINX_access_monitoring)<br><br>* [JuiceFS access analysis](https://docs.byteplus.com/docs/tls/JuiceFS_access_analysis)<br><br>* [MQTT monitoring](https://docs.byteplus.com/docs/tls/MQTT_monitoring) |
