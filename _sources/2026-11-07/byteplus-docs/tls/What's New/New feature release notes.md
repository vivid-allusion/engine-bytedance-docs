---
title: "New feature release notes"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Release_notes"
---

This article describes the release updates for each feature version in TLS. New features will be released gradually in each region. Try them out.

<span id="D2IKMwiZ"></span>
## July 2026


|<div style="text-align: center"><br><strong>New features</strong></div><br> |<div style="text-align: center"><br><strong>Description</strong></div><br> |**Release date** |**Release region** |**Supporting documentation** |
|---|---|---|---|---|
|Query and analysis |The TIME_SERIES function now supports grouping and sorting by multiple fields. |2026\-07\-02 |All regions |[Date and time functions](https://docs.byteplus.com/en/docs/tls/Date-and-time-functions-2#time-series) |
|Query and analysis |* Added feature: adding description features for index fields. <br><br>* Added limit: the maximum number of auto\-indexed JSON subfields is 500. |2026\-07\-02 |All regions |[Configure index](https://docs.byteplus.com/en/docs/tls/Configure-indexes-2) |
|Data consumption and shipping |The consumption of JSON\-format data over the Kafka protocol now supports selecting specified preset fields for consumption. |2026\-07\-02 |All regions |[Use the Kafka protocol to consume logs](https://docs.byteplus.com/en/docs/tls/use_the_kafka_protocol_to_consume_logs) |


&nbsp;

<span id="HhvxKQFC"></span>
## May 2026


|<div style="text-align: center"><br><strong>New features</strong></div><br> |<div style="text-align: center"><br><strong>Description</strong></div><br> |**Release date** |**Release region** |**Supporting documentation** |
|---|---|---|---|---|
|Resource management |Added support for manually merging topic shards. |2026\-05\-26 |All regions |[Manage shards](https://docs.byteplus.com/en/docs/tls/Managing_shards) |
|Data processing |Added consumer processor, supporting rule\-based data consumption.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Notice</div><br><br><br><div data-tips="true" data-tips-type="default">This feature is in closed beta. If you have business needs, contact the client manager for allowlist.</div><br> |2026\-05\-26 |All regions |[Consumer processor overview](https://docs.byteplus.com/en/docs/tls/Consumer_processor_overview) |
|Log application |Added the following log applications:<br><br><br>* LLM Observability: CloudLens for CLB<br><br>* Basic Service Monitoring: CloudLens for ALB |2026\-05\-26 |All regions |* [CloudLens for CLB](https://docs.byteplus.com/en/docs/tls/CloudLens_for_CLB)<br><br>* [CloudLens for ALB](https://docs.byteplus.com/en/docs/tls/CloudLens_for_ALB) |
|Log application |Added monitoring and observability capabilities for CloudLens for TLS log applications. |2026\-05\-26 |All regions |[CloudLens for TLS](https://docs.byteplus.com/en/docs/tls/CloudLens_for_TLS) |


&nbsp;

<span id="M12ZQwZv"></span>
## April 2026


|<div style="text-align: center"><br><strong>New features</strong></div><br> |<div style="text-align: center"><br><strong>Description</strong></div><br> |**Release region** |**Supporting documentation** |
|---|---|---|---|
|Query and analysis |Added the phrase query feature for log index edition.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Notice</div><br><br><br><div data-tips="true" data-tips-type="default">It is in closed beta. If you have business needs, contact the client manager for allowlist.</div><br> |All regions |[Query logs via phrase query (Index edition)](https://docs.byteplus.com/en/docs/tls/Phrase_search_Index_edition) |
|Query and analysis |* Added support for directly saving query results on the current page locally.<br><br>* Added support for downloading fully accurate logs. |All regions |[Download logs](https://docs.byteplus.com/en/docs/tls/Download-logs-2) |
|Data collection |Added support for importing TOS archived and cold archived data. |All regions |[Import logs from TOS](https://docs.byteplus.com/en/docs/tls/Import_data_from_tos) |
|Data processing |Added the data processor, a tool that provides real\-time, lightweight data cleansing, transformation, and enrichment capabilities.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Notice</div><br><br><br><div data-tips="true" data-tips-type="default">It is in closed beta. If you have business needs, contact the client manager for allowlist.</div><br> |All regions |[Overview of the data processor](https://docs.byteplus.com/en/docs/tls/Overview_of_the_data_processor) |
|Data consumption and shipping |* Added support for delivering data to TOS in Parquet format.<br><br>* Added support for delivering data to TOS with partitioning by specified log fields. |All regions |[Overview of shipping logs to TOS](https://docs.byteplus.com/en/docs/tls/Ship_logs_to_tos_overview1) |
|Visualization |Added the preset WAF overview dashboard to display metrics related to WAF web attack logs. |All regions |[Quickly create a dashboard using a preset template](https://docs.byteplus.com/en/docs/tls/Quickly_create_dashboards_using_preset_templates) |
|Log application |Added log applications, providing out\-of\-the\-box scenario analysis applications for cloud product observation, LLM observation, basic service monitoring and more. |All regions |[Overview of log applications](https://docs.byteplus.com/en/docs/tls/Overview_of_log_applications) |


<span id="74dH8dEP"></span>
## December 2025


|**Feature** |**Description** |**Region** |Related Documents |
|---|---|---|---|
|Query and analysis |Optimizes index configuration of JSON type data; supports the automatic indexing or automatic indexing statistics for JSON subfields. |All regions |[Index data types](https://docs.byteplus.com/en/docs/tls/Index-data-types-2) |
|Data collection |The limit for the number of inotify monitored log directories in LogCollector 2.3.x and later versions are increased to 1000. |All regions |[LogCollector limits](https://docs.byteplus.com/en/docs/tls/logcollector_limits) |
|Data processing |Adds data backflow feature. This feature can return specified log fields to log topic and supports shipping data to TOS for long\-term storage. |All regions |[Data backflow overview](https://docs.byteplus.com/en/docs/tls/Log_backflow_overview?type=preview&lang=en) |


&nbsp;

<span id="WVnQaijQ"></span>
## November 2025


|**Feature** |**Description** |**Region** |Related Documents |
|---|---|---|---|
|Resource management |Supports batch splitting shards of log topics. |All regions |[Manage shards](https://docs.byteplus.com/en/docs/tls/Managing_shards) |
|Data collection |Copys existing data import tasks and creates new data import tasks as needed. |All regions |[Data import](https://docs.byteplus.com/en/docs/tls/data_import) |
|Query and analysis |* Adds download context query results.<br><br>* Adds download log export to JSONL format. |All regions |* [Context search](https://docs.byteplus.com/en/docs/tls/Context-search-2)<br><br>* [Download logs](https://docs.byteplus.com/en/docs/tls/Download-logs-2) |
|Data consumption and shipping |Ships logs to TOS in JSONL format. |All regions |[Overview](https://docs.byteplus.com/en/docs/tls/Ship_logs_to_tos_overview1) |


&nbsp;

<span id="7QJtDRmJ"></span>
## September 2025


|**Feature** |**Description** |**Region** |Related Documents |
|---|---|---|---|
|Resource management |Added the ability to modify the number of shards directly in the log topic list. |All regions |[Manually split shards](https://docs.byteplus.com/en/docs/tls/Managing_shards) |
|Query and analysis |* Added a feature to download logs of inaccurate query results.<br><br>* Added support for the `!=` query syntax to search for logs that do not contain the specified value. |All regions |* [Download logs](https://docs.byteplus.com/en/docs/tls/Download-logs-2)<br><br>* [Operator](https://docs.byteplus.com/en/docs/tls/Log-query-syntax-2) |
|Alert |Added alarm recovery notification feature. |All regions |[Create alarm policy](https://docs.byteplus.com/en/docs/tls/create_alarm_policies) |


<span id="mbpmKKor"></span>
## August 2025


|**Feature** |**Description** |**Region** |Related Documents |
|---|---|---|---|
|Resource management |Added LogCollector management features, separating upgrade and downgrade operations into a dedicated LogCollector management tab |All regions |[View host groups](https://docs.byteplus.com/en/docs/tls/View_a_host_group) |
|Data processing |Added the ability to convert analytics data from scheduled SQL tasks into metrics and store them in BytePlus Managed Prometheus (VMP) workspace. |All regions |[Create scheduled SQL analysis and store data in managed Prometheus](https://docs.byteplus.com/en/docs/tls/Create_scheduled_SQL_analysis_data_storage_to_managed_Prometheus) |


<span id="TEaSLNak"></span>
## July 2025


|**Feature** |**Description** |**Region** |Related Documents |
|---|---|---|---|
|Data consumption and shipping |Added capability to ship Syslog log data to Splunk.<br><br>After consuming data via the TLS API endpoint ConsumeLogs, the data is parsed into the corresponding Syslog format and then written to Splunk. |All regions |[Ship logs to Splunk](https://docs.byteplus.com/en/docs/tls/Ship_logs_to_Splunk) |
|Dashboard |Configure dashboard filters and variables when subscribing; set multiple message delivery periods; enable or disable dashboard subscriptions. |All regions |[Subscribe to dashboard notifications](https://docs.byteplus.com/en/docs/tls/Subscribing_to_a_dashboard) |
|Data processing |Added configuration for creating scheduled SQL analysis jobs with daily and monthly time window granularity. |All regions |[Create scheduled SQL analysis data and store it in the log topic](https://docs.byteplus.com/en/docs/tls/create_a_scheduled_sql_task) |
|Trace storage |Added the ability to set the maximum shard split count and log storage period when creating a Trace instance. |All regions |[Create a universal trace instance](https://docs.byteplus.com/en/docs/tls/create_a_trace_instance) |


<span id="Lda2ZREb"></span>
## June 2025


|**Feature** |**Description** |**Region** |Related Documents |
|---|---|---|---|
|Query and analysis |Enable automatic index update when adding a Key\-value index. When enabled, the system will automatically add newly discovered fields to the Key\-value index. |All regions |[Configure key-value indexes](https://docs.byteplus.com/en/docs/tls/Configure-indexes-2) |
|Data collection |* Added json_extract plugin, which extracts values from JSON using specified JSONPath expressions during LogCollector collection.<br><br>* Added split_select plugin, which splits and joins designated field values using a specified delimiter during LogCollector collection.<br><br>* Added url_parse plugin, which parses and extracts components of specified field URLs during LogCollector collection.<br><br>* Added keep_fields plugin, which keeps designated fields and discards all others during LogCollector collection. |All regions |* [JSON extraction plugin](https://docs.byteplus.com/en/docs/tls/JSON_extraction_plugin)<br><br>* [Field segmentation and recombination plugin](https://docs.byteplus.com/en/docs/tls/Field_split_and_reassembly_plugin)<br><br>* [URL parsing plugin](https://docs.byteplus.com/en/docs/tls/URL_parsing_plugin)<br><br>* [Field retention plugin](https://docs.byteplus.com/en/docs/tls/Reserved_fields_plugin) |
|Create host group |Add  ECS and quickly install LogCollector. When creating a host group, this feature lets you add  ECS instances to the group and automatically install LogCollector on the selected instances. |All regions |* [Create host group (IP address)](https://docs.byteplus.com/en/docs/tls/Create_an_IP_address-based_host_group)<br><br>* [Create host group (Host identification)](https://docs.byteplus.com/en/docs/tls/Create_a_label-based_host_group) |


<span id="RAH26SMf"></span>
## December 2024


|**Function** |**Description** |**Region** |**Related documents** |
|---|---|---|---|
|Data collection |LogCollector supports the setting of additional file identifiers, allowing log files or the standard output of containers to be matched and collected by multiple collection rules simultaneously. |Asia Pacific (Johor) |[File logs or standard output can be collected multiple times simultaneously](https://docs.byteplus.com/docs/tls/file-repeatedly-collected) |
|Query and analysis |New machine learning functions such as ts_density_cluster, ts_predicate_ar, ts_predicate_arima, ts_anomaly_filter, ts_predicate_simple are added. |Asia Pacific (Johor) |[Machine learning functions overview](https://docs.byteplus.com/docs/tls/Machine-learning-functions-overview) |
|Query and analysis |New SQL functions such as empty_approx_set, merge, cardinality are added. |Asia Pacific (Johor) |[Functions overview](https://docs.byteplus.com/docs/tls/Overview-of-functions-2) |
|Data consumption |Optimize the Kafka protocol consumption function to support the dashboard and alerting capabilities via TLS, and achieve real\-time monitoring and alerting for the backlog situation of Kafka protocol consumption. |Asia Pacific (Johor) |[Visualization of Kafka Protocol Consumption Metrics](https://docs.byteplus.com/docs/tls/Visualization-of-Kafka-Protocol-Consumption-Metrics) |
|Visualization |New data source variables are added, and it supports the flexible switching of data sources for statistical charts by specifying variable names and the scope of log topics. |Asia Pacific (Johor) |[Add data source variables](https://docs.byteplus.com/docs/tls/Adding_filters_to_a_dashboard#9d95ecde) |
|Visualization |The preset variables such as __from , __to are added, which can be directly used in text boxes like query and analysis statements on the dashboard, titles of statistical charts, and text graphs without the need for additional creation. |Asia Pacific (Johor) |[Use system preset variables](https://docs.byteplus.com/docs/tls/Adding_filters_to_a_dashboard#0d37c83f) |
|Visualization |A new data conversion\-classification function is added, which supports classifying the query and analysis results according to the specified fields. |Asia Pacific (Johor) |[Data conversion](https://docs.byteplus.com/docs/tls/Statistical-chart-related-operations#ec3e7867) |


<span id="bQPO5dkJ"></span>
## October 2024


|**Function** |**Description** |**Region** |**Related documents** |
|---|---|---|---|
|Data collection |Optimize the service logs of LogCollector, support the collection and recording of logs with duplicate paths, and provide corresponding best practices for monitoring. |All regions |[Monitore LogCollector](https://docs.byteplus.com/docs/tls/Monitore-LogCollector) |
|Query and analysis |New SQL functions such as INVERSE_NORMAL_CDF, CUME_DIST are added. |All regions |[Functions overview](https://docs.byteplus.com/docs/tls/Overview-of-functions-2) |
|Visualization |When configuring data sources in Grafana, a new method that only requires specifying the access key is added to obtain the data of all log topics under the current log service account. |All regions |[Import log data to Grafana](https://docs.byteplus.com/docs/tls/Importing_log_data_to_Grafana) |
|Timed SQL Analysis |Support setting the scheduling cycle through Cron expressions. |All regions |[Create a scheduled SQL task](https://docs.byteplus.com/docs/tls/create_a_scheduled_sql_task) |


<span id="LCtYIu11"></span>
## September 2024


|**Function** |**Description** |**Region** |**Related documents** |
|---|---|---|---|
|Query and analysis |Over 50 SQL functions such as CAST, TRY_CAST, ARRAY_POSITION, and DATE_TRUNC_SEC are newly added. |All regions |[Functions overview](https://docs.byteplus.com/docs/tls/Overview-of-functions-2) |
|Trace |Support the deployment of OpenTelemetry Collector in the container environment and forward data to TLS through OpenTelemetry Collector. |All regions |[Use OpenTelemetry Collector to forward data (Container Deployment)](https://docs.byteplus.com/docs/tls/Use-OpenTelemetry-Collector-to-forward-data-Container-Deployment) |
