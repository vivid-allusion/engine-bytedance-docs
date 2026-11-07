---
title: "Features"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Features"
---

This topic describes the features of Torch Log Service (TLS).

<span id="Log collection"></span>
## Data collection

TLS allows you to collect log data by using various methods such as LogCollector, API, and data import from open\-source components and data cloud products, and to connect to dozens of data sources.


* You can use LogCollector to collect logs such as host text logs, container text logs, and container standard output.

* You can connect to BytePlus products such as Application Load Balancer (ALB).

* You can import data from channels such as Kafka, TOS, Simple Log Service (SLS), and Elasticsearch.

* You can collect data from mobile apps.


<span id="12e15cb3"></span>
## Data storage

TLS offers efficient and reliable data storage solutions.

Supports persistent storage of massive data, featuring stable performance and convenient read and write access.

<span id="Query and analysis"></span>
## Data query and analysis

TLS offers the data query and analysis feature to facilitate the query and analysis of massive logs.


* Supports SQL\-92 syntax.

* Supports query methods such as exact search, fuzzy search, full\-text search, field search, and phrase search.

* Supports features such as quick analysis, context search, and download logs.


<span id="2176c60d"></span>
## Visualization

TLS offers various types of charts and interactive dashboards.


* Offers more than 20 types of charts to visualize query and analysis results and meet multidimensional analytical requirements.

* Offers interactive dashboards to help you build data analysis dashboards.

* Supports connecting to third\-party visualization tools such as Grafana.


<span id="571f8d7b"></span>
## Data transformation

TLS offers dozens of domain\-specific language (DSL) data transformation functions to meet different data processing requirements.


* Data wrangling: extracts field content in mixed formats from logs and converts the log formats to get structured data.

* Data transferring: transfers data to multiple downstream systems for storage or computing. The data can be consumed by various business systems.

* Data masking: masks sensitive information in data.

* Data filtering: filters complex and diverse log data, retaining core information that requires your focus.


<span id="a35e0d10"></span>
## Scheduled SQL

Scheduled SQL can periodically execute query and analysis statements and save the analysis results.


* Scheduled query and analysis of logs: executes query and analysis statements periodically based on the specified time window and scheduling cycle, and saves the analysis results to the specified topic.

* Log aggregation: aggregates detailed raw logs into logs with appropriate precision to reduce storage costs.

* Log filtering: filters raw logs and retains only key fields that require your focus.


<span id="a1953f40"></span>
## Data consumption and shipping

TLS offers the real\-time data consumption and shipping features.


* Supports the Kafka protocol feature to connect to downstream ecosystems.

* Supports dumping data to multiple heterogeneous storage systems such as TOS in real time.


<span id="f04b1d2b"></span>
## Alarm

TLS offers an all\-in\-one alarm feature, including data monitoring, alarm notifications, and alarm management.


* Monitors query and analysis results as scheduled based on alarm policies and reports alarms in seconds if data exceptions occur.

* Sends service status notifications in real time through email.

* Supports designing the custom notification content based on the content syntax, content functions, and content variables.


<span id="a33aaacc"></span>
## Trace

TLS offers a distributed tracing feature based on the [OpenTelemetry](https://opentelemetry.io/docs/what-is-opentelemetry/) protocol and specification.


* Allows you to access, store, query, and analyze various types of trace data.

* Supports connecting to open\-source systems using an SDK or LogCollector.
