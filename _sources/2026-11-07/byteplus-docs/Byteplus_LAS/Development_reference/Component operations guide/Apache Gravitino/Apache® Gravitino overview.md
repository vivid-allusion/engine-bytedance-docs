---
title: "Apache® Gravitino overview"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Gravitino_overview"
---

In today's enterprise data environments, complexity is increasing, with data scattered across various databases, data lakes, message queues, and even AI platforms, resulting in "metadata islands." Traditional solutions typically require large\-scale data migration, which is not only costly but also highly risky.

The emergence of Apache® Gravitino is intended to address this challenge. Its core objective is not to move data, but to unify metadata, aiming to become a "**catalog of catalogs**"  **(Catalog of Catalogs)** . It is designed to build a high\-performance, geographically distributed federated metadata lake, providing a unified entry point for discovery, management, and governance of all enterprise data and AI assets, and serving as the single source of truth for multi\-cloud and multi\-region data architectures. This article provides a comprehensive overview of Apache® Gravitino's core concepts, main features, and architectural design.

> "Apache Gravitino, the names of other Apache projects, and the ASF logo are either registered trademarks or trademarks of the Apache Software Foundation in the United States and/or other countries."


<span id="4855af52"></span>
## Main features and characteristics

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d0bda00d8de54c1d98f6bfbfa847c795~tplv-goo7wpa0wc-image.image" width="1376px" /></div>


<div style="text-align: center">
<strong>Figure 1 Gravitino unified management of multiple data sources</strong></div>


The core features of Gravitino can be summarized as follows:


* **Unified metadata management**: By leveraging an abstract metadata model, it supports unified management of heterogeneous data sources, including relational databases (such as MySQL and PostgreSQL), data lakes (such as Hive and Iceberg), file systems (such as HDFS and S3), message queues (such as Kafka), and AI/ML models.

* **Direct management and real\-time synchronization**: Unlike traditional metadata systems that passively collect metadata through pull or push methods, Gravitino directly manages underlying data sources via connectors. Any metadata changes made in Gravitino are instantly reflected in the underlying systems.

* **End\-to\-end data governance**: Provides a unified governance layer that centralizes access control (RBAC), audit logs, data tagging, and discovery, ensuring consistent policy enforcement across all connected systems.

* **Multi\-engine support**: Compute engines (such as Trino, Spark, and Flink) can access all managed data through Gravitino's connectors without modifying existing SQL dialects or code.

* **Geographical distribution support**: The architecture is designed to support cross\-region and cross\-cloud deployment. Gravitino instances in different regions can interconnect, providing a globally unified metadata view.

* **Metadata\-driven action system**: This is the core highlight of version 1.0, marking Gravitino's evolution from a passive metadata store to an active "data brain" capable of executing automated tasks.


<span id="a064e727"></span>
## Core architecture and design

<span id="1de00eaf"></span>
### Overall architecture

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c1e16cb0cd14b88bccd7245df98775f~tplv-goo7wpa0wc-image.image" width="2731px" /></div>


<div style="text-align: center">
<strong>Figure 2 Gravitino layered overall architecture design</strong></div>


Gravitino adopts a clear layered architecture design to ensure high scalability and flexibility:


* **Interface layer (Interface Layer)** : Primarily provides standard REST API interfaces for users and applications. Future plans include support for interfaces such as Thrift and JDBC.

* **Functionality layer (Functionality Layer)** : Provides core APIs for metadata management (CRUD) and metadata governance (access control, auditing, discovery, and more).

* **Core object model (Core Object Model)** : Defines a universal metadata object model to shield underlying differences, mainly including the following levels:

   * **Metalake**: The metadata lake, which is the top\-level container managed by Gravitino, used to isolate different businesses or environments.

   * **Catalog**: The data catalog, corresponding to an external data source, such as a Hive Metastore or a PostgreSQL database.

   * **Schema**: The database or schema, which is a collection of tables and provides a namespace within the Catalog.

   * **Table**: The table, which defines a structured view of the data.

   * **Fileset**: The fileset, used to manage unstructured data, such as collections of files on HDFS or S3.

   * **Model**: The model, used to manage metadata for machine learning models.

   * **Topic**: The topic, used to manage metadata for message queues (such as Kafka).

* **Connection layer (Connection Layer)** : Contains a series of pluggable connectors responsible for communicating with specific external data sources (such as Hive Metastore (HMS), PostgreSQL) and performing metadata operations.


<span id="47271025"></span>
### Enterprise\-grade Iceberg REST Catalog implementation

Gravitino not only follows the open specification of the Iceberg REST Catalog, but also provides an enhanced implementation designed for enterprise production environments.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/23344b09dec045b3831f8eefa62c53f3~tplv-goo7wpa0wc-image.image" width="820px" /></div>


**Gravitino Iceberg REST Catalog architecture**


* **Performance and reliability**: Built\-in intelligent caching, connection pool, and failover mechanisms ensure stability and high availability for large\-scale production environments.

* **Enterprise\-grade observability and governance**: Natively integrates Prometheus and Grafana for comprehensive monitoring, provides a complete audit log and event framework, and allows enterprises to inject custom business logic.

* **Unified and robust security model**: Reuses the platform's unified security framework, supports enterprise\-grade authentication such as OAuth 2.0 and Kerberos, and securely applies for temporary tokens to access cloud storage for clients through the **Credential Vending** mechanism, greatly enhancing the security of cloud data access.

* **Extensive backend compatibility**: Any Catalog supported by Gravitino (such as Hive Metastore or JDBC Catalog) can be used as backend storage, and is uniformly exposed through standard REST interfaces, enabling all the advantages of a modern **REST Catalog** without modifying existing metadata infrastructure.


<span id="8646e7f5"></span>
## BytePlus ecosystem integration

As an open metadata management core, Gravitino is deeply integrated with BytePlus LAS Catalog, providing enterprises with one\-stop data and AI asset management capabilities.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8caee7df27364cb3aca9322f610734bc~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<strong>Figure 3 Gravitino and BytePlus LAS Catalog integration</strong></div>


Gravitino and BytePlus LAS Catalog integration aims to deliver the following core values to users:


* **Openness and standards**: Based on compatibility with existing **Hive Metastore (HMS)** , introduces the industry\-leading Gravitino as the metadata management core, offering an open experience based on open\-source standards.

* **Modern data lake capabilities**: Natively supports mainstream data lake formats such as Iceberg and Paimon, provides standard **Iceberg REST Catalog** services, as well as unified access control and audit capabilities.

* **Multimodal metadata**: Extends support for metadata management of unstructured and AI assets, including **Fileset** (file sets) and **Model** (AI models).


<span id="9355d197"></span>
## Limitations

Currently, integration between Gravitino and the BytePlus ecosystem is only supported in North China 2 (Beijing) and East China 2 (Shanghai) regions.

<span id="0c90bcbc"></span>
## Related documentation

For detailed usage and API specifications of the Gravitino Server API, please refer to [Gravitino Server OpenAPI usage guide](https://docs.byteplus.com/docs/Byteplus_LAS/Gravitino_Server_OpenAPI_usage_guide).

For detailed usage and API specifications of the Gravitino Iceberg REST Catalog, please refer to [Gravitino Iceberg REST Catalog user guide](https://docs.byteplus.com/docs/Byteplus_LAS/Gravitino_Iceberg_REST_Catalog_user_guide).
