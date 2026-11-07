---
title: "What is Cloud Search"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/what-is-cloudsearch"
---

Cloud Search is a fully managed, one\-stop information retrieval and analysis platform provided by BytePlus. It is compatible with Elasticsearch, OpenSearch, Kibana, Dashboards, Cerebro, and common open\-source plugins. It can be used for full\-text search, vector search, hybrid search,  spatiotemporal retrieval, and other scenarios. Using BytePlus Cloud Search, you can deploy with one click, scale elastically, simplify maintenance, and quickly build solutions for log analysis, information retrieval, and other business scenarios.

<span id=".5Lqn5ZOB57uE5Lu2"></span>
## Product components

<span id="Elasticsearch"></span>
### Elasticsearch & OpenSearch

BytePlus Cloud Search is based on the open\-source Elasticsearch and OpenSearch projects. It provides easy\-to\-use RESTful APIs and powerful near real\-time capabilities to search and analyze large datasets. It is widely applied in log analysis, enterprise search, big data analytics, vector search, hybrid search, spatiotemporal retrieval, and more.

The following is core architectures diagram of Elasticsearch and OpenSearch.

<span id="YVJzr84E"></span>
#### Elasticsearch

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b477f721ae002d082aadece0071a38b6.png) </span>

<span id="aUYlM0TH"></span>
#### OpenSearch

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ca1f176134ef62355eef335dc07ef541.png) </span>

<span id="Kibana"></span>
### Kibana & Dashboards

A data visualization tool. When you create a Cloud Search instance, the system deploys Kibana/Dashboards nodes simultaneously. These nodes allow you to view and interact with index data and visualize and analyze data through charts.

<span id="yprs2ehC"></span>
## Product features

<span id="tHKq8Ard"></span>
### Data storage


* BytePlus Cloud Search offers a variety of node specifications and high\-performance volumes to ensure your data read and write performance.

* Supports elastic scaling, allowing you to adjust the number of nodes, node volume size, and computing specifications based on your actual business needs to meet various evolving scenarios.

* Supports instance monitoring to reduce operation and maintenance costs and ensure instance availability.


<span id="rcbjJBUL"></span>
### Data retrieval and analysis


* Provides real\-time search with stable and reliable service, supporting full\-text search, analysis, aggregation, highlight display, and SQL analysis capability through plugins. It effectively handles complex combinations, conditions, and fuzzy queries, easily meeting text, numeric, date, IP, and geographic data query and analysis scenarios.

* Offers RESTful API and multiple language clients to find matching information in PB\-level data within milliseconds, facilitating efficient construction of search services.


<span id="8GbaZ7ps"></span>
### Data visualization

Integrate Kibana services to help you build visual operation and maintenance panels with Kibana dashboards, enabling business data classification and dashboard creation. This allows efficient statistics and analysis of massive data to deeply explore the business data value.

<span id="jBN4U3Cb"></span>
### Vector retrieval

Cloud Search supports k\-NN, offering vector search, vector storage, and embedding capabilities. Based on the Cloud Search cluster, the k\-NN vector database provides large\-scale distributed capabilities, delivering scalable vector search. Additionally, Cloud Search supports hybrid "text + vector" search to better meet search scenario needs.

<span id="EDGn4tlJ"></span>
## Product advantages

<span id="EDGn4tlJ"></span>
### Vector search advantages

Cloud Search provides industry\-leading vector and full\-text search capabilities, including:


* **Multiple engines and architecture evolution**

   Supports multiple algorithm engines such as DiskANN, Lucene, Faiss, and NMSLIB. Various configurations including capacity\-oriented DiskANN, performance\-oriented DiskANN + RaBitQ, and Hybrid DiskANN cover a unified algorithm engine form from full memory to full disk. It suits application scenarios ranging from hundreds of thousands to hundreds of billions in scale. Users do not need to switch indexing algorithm engines due to business scenarios or stages; the same architecture seamlessly supports different business development stages.

* **Unified retrieval and feature inheritance**

   Supports combined vector and text retrieval with normalized scoring within the same engine, combining text search precision with vector search semantic capability. It also supports sparse vectors, multi\-vector joint queries, and diverse tuning methods while fully inheriting Elasticsearch/OpenSearch features, including filtering, nested relations, RRF, synonyms, time range filtering, keyword point queries, full/fuzzy matching, and geolocation filtering.

* **AI capabilities compatible with ecosystems**

   Supports multiple embedding modes, built\-in inference and rerank models, integrates with large models like Doubao and DeepSeek, and also supports customer\-built inference; fully compatible with mainstream AI ecosystems such as LangChain, MCP, and Hugging Face.

* **Openness and migration friendliness**

   Fully leverages open\-source ecosystems with no technology lock\-in risk; users migrating to self\-built systems can directly reuse existing application interfaces without modification.

* **Query and optimization capabilities**

   Offers 30+ query capabilities, including query DSL, complex query construction, multiple matching modes, nested and combined field queries, fuzzy matching, weighted retrieval, and highlighting; also supports data enhancement, intent understanding, DSL generation, vector + scalar + full\-text hybrid search, rerank and fine ranking, and large model generation for optimization. Improves performance and reduces computational overhead by simplifying coarse ranking and reranking only the Top N data.


<span id="TlJH4RLL"></span>
### Fully managed advantages


* **One\-click deployment**

   You only need to click Create instance in the BytePlus Cloud Search service console, select the required specification configuration and network configuration, and create it within minutes, eliminating the process of hardware and software deployment and debugging, greatly saving deployment time.

* **elastic scaling**

   Cloud Search service instances support elastic scaling. You can flexibly adjust node specifications, quantity, and disk size according to your actual business needs to meet the changing demands of your growing business. Advanced features such as Security, SQL, and Alerting are provided via the Open Distro plugin, effectively ensuring instance security and improving operation and maintenance efficiency.

* **High security**

   Deploy instances through the VPC network, provide HTTPS access protocol to ensure data transmission security, and offer multi\-tenant capability based on the Security plugin to guarantee the security of your resources.

* **high reliability**

   Supports multi\-AZ deployment and fast automatic/manual backup snapshots integrated with Volcano TOS. Supports out\-of\-the\-box log search, monitoring, and alerting functions, including ES\-level operational monitoring. It also monitors and alerts on all metrics from underlying resources to ES.
