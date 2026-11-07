---
title: "What is Torch Log Service"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/What_is_TLS"
---

Torch Log Service (TLS) is an all\-in\-one service platform for managing logs and trace data. The platform offers features such as data collection, storage, query and analysis, transformation, consumption, shipping, monitoring and alarming, and visualization. TLS is applicable to scenarios such as O&M monitoring and statistical analysis.

<span id="adea55ac"></span>
## Overview

As a fully\-managed data service platform, TLS helps enterprises and organizations manage logs and trace data in cloud\-native architectures. TLS offers various data access methods, secure data storage, powerful data query and analysis, abundant transformation functions and charts, flexible consumption and shipping mechanisms, and all\-in\-one alarm features. TLS can connect to dozens of data sources, store data securely with low costs, wrangle and mask data, and connect to downstream systems such as big data platforms, and report alarms in seconds if data exceptions occur. With the preceding capabilities, TLS is applicable to the following scenarios:


* O&M monitoring: Enterprises can build log platforms based on TLS to implement business monitoring, O&M, and operations.

* Statistical analysis: TLS can display the status and trend of key business metrics in real time, so decision makers are informed of updates.

* Data lake and stream computing: TLS can seamlessly connect to various real\-time computing services and stream computing engines.

* Monitoring of cloud service logs: TLS offers out\-of\-the\-box visualized applications of log analysis and best practices in cloud product log scenarios.

* Classified protection compliance: TLS can help your enterprise meet classified protection compliance requirements.


<span id="Features"></span>
## Features

TLS offers the following features:


|Feature |Description |
|---|---|
|Data collection |Connects to dozens of data sources through methods such as LogCollector, API, and SDK. The data sources include host logs, container logs, BytePlus product logs, data stored in Kafka, Torch Object Storage (TOS), Simple Log Service (SLS), and Elasticsearch, and mobile app data. |
|Data storage |Supports permanent storage. |
|Data query and analysis |Offers built\-in log query syntax and SQL functions to query and analyze massive data. |
|Visualization |Offers abundant charts to visualize query and analysis results and interactive dashboards to help you build data analysis dashboards. |
|Data transformation |Offers dozens of domain\-specific language (DSL) transformation functions to copy, filter, mask, split, and wrangle data. |
|Scheduled SQL |Queries and analyzes data collected in a specific time range as scheduled, and outputs the analysis results to the specified topic in data analysis, aggregation, and filtering scenarios. |
|Data consumption and shipping |Allows you to consume data in real time using an SDK, the Kafka protocol, or other methods, and ship data to cloud products such as TOS and Kafka in real time. |
|Alarm |Offers an all\-in\-one alarm feature, including data monitoring, alarm notifications, and alarm management, to report alarms in seconds if data exceptions occur. |
|Trace |Offers a distributed tracing feature based on the native OpenTelemetry protocol and specification, and supports end\-to\-end observability of trace data. |


<span id="25790589"></span>
## Terms

Before you use TLS, read and understand the following terms.


|Terms |Description |
|---|---|
|Log |Logs are records of events that occur during the runtime of a system or a program. The events include user operation events, API access events, and runtime error events. All types of logs have a unified structure and format. |
|Trace data |Trace data records information about the entire trace of calling services, including the call relationship, latency, and result. |
|Project |A project is a unit of data management. It isolates the resources of different tenants and controls access to resources. Normally, one project corresponds to one application, business, or product. |
|Topic |A topic is a unit of data collection and storage. A project consists of one or more topics. Each topic belongs to one project. For one topic, you can configure different data sources and collection rules. |
|Shard |A shard is a basic unit of data reads and writes. All data is stored in shards. Each shard has a certain read and write capability. We recommend that you plan the number of shards based on your business needs. |


<span id="3a25847c"></span>
## Fees

The fees depend on your actual usage of resources each day.

<span id="937338df"></span>
## Use method

Use TLS through the console, API, or SDK.


|**Method** |**Description** |
|---|---|
|Console |Log on to the [TLS console](https://console.byteplus.com/tls) to use your TLS resources. |
|API |Call API actions of TLS to use your TLS resources. |
