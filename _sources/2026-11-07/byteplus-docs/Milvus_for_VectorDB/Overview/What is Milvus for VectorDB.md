---
title: "What is Milvus for VectorDB"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/What_is_Milvus_for_VectorDB"
---

Milvus for VectorDB (hereafter Milvus) is a fully managed Milvus database service built by BytePlus based on the open\-source Milvus. It provides efficient unstructured data retrieval, supports instance lifecycle management, parameter configuration, and alerts and monitoring. It suits diverse AI scenarios, such as AI\-generated content retrieval and multimodal search.

## Product architecture

Milvus nodes are divided into service nodes and compute nodes. Service nodes include metadata service nodes, Proxy nodes, Index nodes, Streaming nodes, and Data nodes. Compute nodes include Query nodes. Milvus uses a shared storage architecture. Its compute nodes support storage and compute separation as well as horizontal scaling.

* Metadata service node: manages cluster components, coordinates cluster tasks, and supports primary\-backup mechanisms.

* Proxy node: receives user requests and routes them to the corresponding backend components, designed stateless to support horizontal scaling.

* Index node: builds, updates, and maintains data indexes. Indexing efficiency depends on computing power and it supports horizontal scaling. Only version 2.5 instances support Index nodes.

* Streaming node: receives, processes, and distributes real\-time data streams. It handles data ingestion and streaming processing on the write path to ensure high\-throughput write and data reliability, supporting horizontal scaling. Streaming node is supported only in version 2.6 and above instances.

* Data node: handles data writing. Writing efficiency depends on computing power and it supports horizontal scaling.

* Query node: handles data queries and retrievals. Its memory must accommodate all indexes and it supports horizontal scaling.

Milvus supports selecting whether to enable high availability multi\-node deployment. After enabling high availability multi\-node deployment, Mix Coordinator nodes, Proxy nodes, Index nodes, Streaming nodes, Data nodes, and Query nodes each require at least 2 instances. Proxy nodes, Index nodes, Streaming nodes, Data nodes, and Query nodes can scale further. In practical business scenarios, enabling high availability deployment is recommended to ensure continuous service availability.

**Milvus 2.5**

Released in December 2024, it builds upon the full vector search capabilities of Milvus and introduces powerful new features, including keyword search, cluster merge compression for query optimization, and comprehensive support for both sparse and dense vector search methods. At the same time, it enhances cluster management, index construction, and data processing capabilities. It is the mainstream version used for current RAG vector knowledge bases and vector search business.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0de84e0a75cefdbf58bb3c4eaa350f9a.png)

**Milvus 2.6**

Released in August 2025, it includes all core features of Milvus 2.5.0, rebuilds the stream node architecture, rewrites the streaming ingestion pipeline, and introduces a unified Tensor/StructList data type supporting multi\-vector embedding structures. It also enables hierarchical storage through automatic hot and cold data separation and intelligent scheduling. Fully compatible with new production scenarios such as AI Agent, large\-scale high\-dimensional vector search, and privacy\-compliant RAG.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bcbb0faf8bcca6030ac5688389aaa334.png)

**Milvus 3.0**

Released in September 2026, besides core capabilities from Milvus 2.6 such as streaming ingestion reconstruction and tiered storage, it further strengthens open lakehouse collaboration and AI\-native data foundation capabilities. Version 3.0 introduces capabilities like External Collection and Snapshot, which allow direct referencing of files in external data lakes, further decoupling query execution, index management, and underlying data storage. It also keeps enhancing sorting and aggregation, text analysis, near\-duplicate detection, entity\-level TTL, multi\-vector organization, and low\-cost storage optimization. Based on AI Agent, enterprise\-level RAG, and multimodal search scenarios, it further adapts to lakehouse integrated search and ultra\-large\-scale vector services in next\-generation production scenarios.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f033f9671dd08a7d330897407406700f.png)

> **tip**

> Milvus 3.0 instances currently require whitelist access. To use this feature, please [submit a ticket](https://console.byteplus.com/workorder/create/?step=2&SubProductID=P00000255) for application.

## Product advantages

Milvus for VectorDB offers the following product advantages:

* Enterprise\-grade operation and ease of use

   Milvus for VectorDB provides fully managed cloud database services with alerts and monitoring, parameter templates, and a series of streamlined actions, greatly reducing daily cluster operation and maintenance costs.

* High availability

   Milvus for VectorDB supports high availability multi\-node deployment to effectively ensure continuous business operation.

* Compatibility with the open\-source Milvus ecosystem

   Built on open\-source Milvus and fully compatible with open\-source Milvus, ensuring no compatibility issues in self\-built migration scenarios.
