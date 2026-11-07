---
title: "Data collection overview"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/data_collection_overview"
---

BytePlus Torch Log Service (TLS) supports various log collection methods such as using LogCollector or an SDK to collecting log data from host machines, containers, mobile devices, and cloud services. This topic describes the collection methods and solutions supported by TLS.

<span id=".5Yqf6IO95qaC6L-w"></span>
## Feature overview

TLS offers log collection tools such as LogCollector and SDKs for multiple languages, and is compatible with multiple open\-source protocol frameworks including the Kafka and OpenTelemetry protocols. It can collects log data from various sources such as application servers, Kubernetes clusters, mobile clients, BytePlus cloud servers, and cloud services from other cloud vendors.

On the homepage of the TLS console, select a collection mode and complete the collection rule configuration for collecting log data and saving the collected log data to BytePlus TLS. After logs are written to the specified topic and indexed, you can preview the collected log data in real time on the page for querying log data. You can also run query statements that are created based on the query and analysis syntax supported by TLS to query and analyze log data for implementing data visualization and other advanced features.

<span id=".6YeH6ZuG5pa55byP"></span>
## Collection methods


|Collection methods |Description |
|---|---|
|Using LogCollector |Use LogCollector, a log collection tool offered by TLS, to collect application logs from servers or containers. LogCollector support various collection modes such as the single\-line full\-text mode and multiple collection plug\-ins such as the data masking plug\-in.<br><br>For more information on how to use LogCollector, refer to [Collecte logs](https://docs.byteplus.com/docs/tls/getting_started_collecte_logs). |
|Using the Kafka protocol |Torch Log Service (TLS) allows for uploading log data to the TLS server over the Kafka protocol. It means that you can collect log data using the Kafka Producer SDK and upload the collected log data to TLS over the Kafka protocol.<br><br>For more information, refer to [Use the Kafka protocol to upload logs](https://docs.byteplus.com/docs/tls/Use_the_Kafka_protocol_to_upload_logs). |
|Using the OpenTelemetry protocol |Trace is built on the native OpenTelemetry protocol and standards. It allows you to integrate, store, query, analyze, visualize, and perform other operations on trace data.<br><br>For more information, refer to [Trace Overview](https://docs.byteplus.com/docs/tls/trace_overview). |
|Using the TLS API |TLS offers an OpenAPI action for uploading structured log data to a specified topic.<br><br>For more information, refer to [PutLogs](https://docs.byteplus.com/docs/tls/api-putlogs). |
|Using SDKs |TLS offers SDKs in multiple languages. You can use the SDKs to call the OpenAPI interface [PutLogs](https://docs.byteplus.com/docs/tls/api-putlogs) to upload logs to a specified topic. |


<span id=".6YeH6ZuG5pa55qGI"></span>
## Collection solutions


|Data Source Type |The log source. |Description |Related documents |
|---|---|---|---|
|OS |Linux |Use LogCollector to collect log data from Linux OS\-based servers, such as BytePlus Elastic Compute Service (ECS) instances, servers in self\-managed data centers, and servers offered by other cloud vendors. |[Install LogCollector on a host](https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host) |
||Kubernetes cluster |Collect log data from self\-managed Kubernetes clusters, or Kubernetes clusters offered by other cloud vendors.<br><br>Supported log data types include:<br><br><br>* Text logs<br><br>* Standard outputs and standard errors |[Collect container logs overview](https://docs.byteplus.com/docs/tls/collect_container_logs_overview) |
||iOS |Use the SDK for iOS offered by TLS to collect log data. |/ |
||Android |Use the SDK for Android offered by TLS to collect log data. |/ |
|Application |Application log ouput |Use LogCollector to collect log data output by systems and applications. |[Install LogCollector on a host](https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host) |
||Web page |Use web tracking to collect log data from web applications. |[Use web tracking to collect logs](https://docs.byteplus.com/docs/tls/Use_web_tracking_to_collect_logs) |
||Trace |Trace is built on the native OpenTelemetry protocol and standards. It allows you to integrate, store, query, analyze, visualize, and perform other operations on trace data. |[Trace Overview](https://docs.byteplus.com/docs/tls/trace_overview) |
||Logstash |Modify the Logstash configuration file to use the built\-in Kafka output plug\-in logstash_output_kafka to upload log data to TLS. |[Use the Kafka protocol to upload logs](https://docs.byteplus.com/docs/tls/Use_the_Kafka_protocol_to_upload_logs) |
|Data import |BytePlus Torch Object Storage (TOS) |Import and structure log data from TOS to TLS. Only historical log data in TOS can be imported to TLS |[Import data from Torch Object Storage](https://docs.byteplus.com/docs/tls/Import_data_from_tos) |
||Alibaba Cloud Simple Log Service (SLS) |Import log data from Logstores in Alibaba Cloud SLS. SLS log collection rules can also be imported to TLS. |* [Import data from Simple Log Service](https://docs.byteplus.com/docs/tls/Importing_data_from_sls)<br><br>* [Import collection rules from Simple Log Service](https://docs.byteplus.com/docs/tls/Importing_collection_rules_from_sls) |
||Elasticsearch cluster |Import data from BytePlus Elasticsearch clusters, self\-managed Elasticsearch clusters, or Elasticsearch clusters offered by other cloud vendors. Only historical log data in TOS can be imported to TLS |[Import data from Elasticsearch](https://docs.byteplus.com/docs/tls/Importing_data_from_Elasticsearch) |


<span id=".6LS555So6K-05piO"></span>
## Cost information

Writing logs to TLS incurs storage fees, write traffic fees, and shard fees. If you use the API or SDKs to collect log data, you are also charged for resources fees calculated based on the number of requests.

TLS provides a certain free quota for logs collected from BytePlus services. For detailed billing policies, refer to the product documentation of the corresponding cloud service.

<span id=".6ZmQ5Yi26K-05piO"></span>
## Limits

When writing log data to TLS, be aware of the following limits. For limits such as the basic resource quota, read/write traffic limit, and query and analysis concurrency of TLS, refer to [Limits](https://docs.byteplus.com/docs/tls/Limits).
