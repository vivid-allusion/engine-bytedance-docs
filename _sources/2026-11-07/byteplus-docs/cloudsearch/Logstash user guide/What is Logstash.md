---
title: "What is Logstash"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/What_is_Logstash"
---

Cloud Search Logstash is a server\-side data processing pipeline developed by BytePlus based on the open\-source data collection engine Logstash. It dynamically collects data from multiple sources, transforms the format, and then stores the data in the specified location. Logstash is often used together with Elasticsearch and Kibana to form the ELK ecosystem. In the ELK ecosystem, Elasticsearch serves as a real\-time distributed search and analytics engine; Logstash provides data collection, transformation, optimization, and output capabilities; and Kibana offers a powerful visualization interface. This ecosystem is widely applied in real\-time log processing, full\-text search, and data analytics. This article introduces the definition, working principle, product features, advantages, compatibility, and supported plugins of Cloud Search Logstash.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Cloud Search Logstash features are currently not available to individual users.</div>


* <div data-tips="true" data-tips-type="default">Cloud Search Logstash does not support data from pushed data sources, such as HTTP, Beats, TCP, UDP, Syslog, etc.</div>



<span id="boeA9qli"></span>
## Working principle


* Data collection and input: Logstash supports various input options, capturing events simultaneously from different common sources. It can easily collect data in a continuous streaming manner from logs, metrics, web applications, and data storage.

* Data filtering, parsing, and transformation: During data transfer from source to repository, Logstash filters parse each event, identify named fields to build structures, and transform them into a standard format for more efficient analysis.

* Data output and storage: Logstash supports various output options and can transfer data to specified locations through output plugins, such as Elasticsearch, OpenSearch, MySQL, Redis, etc., for further analysis and processing.


<span id="i6RdNHFR"></span>
## Product features


* Scalable: Logstash uses a pluggable framework supporting more than 200 plugins. You can mix and match different input options, filters, and output options in a pipeline.

* Secure and reliable: When a Logstash node fails, Logstash ensures at least once delivery of running events through persistent queues. Unhandled messages can be sent to a dead letter queue for further processing.


<span id="D9TC18xv"></span>
## Product advantages

Based on full support for open\-source Logstash features, BytePlus Logstash offers the following special functions:


* Built\-in OpenSearch\-related plugins support . For detailed information, see [logstash-input-opensearch](https://github.com/opensearch-project/logstash-input-opensearch) and [logstash-output-opensearch](https://github.com/opensearch-project/logstash-output-opensearch).

* Considering the close relationship between Logstash and Elasticsearch/OpenSearch, Cloud Search provides a customized metadata migration pipeline that supports migrating metadata (including index and index templates) from one ES/OS instance to another, improving data migration support between ES/OS instances.

* Supports monitoring and log query, allowing you to view Logstash node status and log details at any time.
