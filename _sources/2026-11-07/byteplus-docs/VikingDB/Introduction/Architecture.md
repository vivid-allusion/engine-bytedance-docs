---
title: "Architecture"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Architecture"
---

<span id="Architecture"></span>
# Architecture

VikingDB is a vector database system built on the cloud infrastructure of BytePlus. It integrates a layer of comprehensively optimized engines, and provides a comprehensive suite of capabilities, from text embedding to collection management, index management, data search, elastic resource scheduling, and monitoring and alerting. These capabilities can be applied in products such as intelligent Q&A, intelligent search, recommendation, and data deduplication systems, and are used in scenarios supported by large language models (LLMs), such as intelligent customer service, domain\-specific knowledge Q&A, text retrieval, cross\-modal and multimodal retrieval of AI\-generated content (AIGC), hybrid search, recommendation and detection of similar and related data, data deduplication, relevance ranking, shuffling, cluster analysis, and data mining.

Capabilities of VikingDB are described as follows:

**Text embedding**: After unstructured text data is imported, VikingDB uses deep neural networks to extract the content and semantics from the text, converts it into feature vectors, and automatically writes them into the vector database to support subsequent retrieval and analysis.

**Collection management**: VikingDB stores raw data in collections. You can create multiple collections, and store the vector data of different business applications in different collections for easy management. Collections support real\-time data writes, queries, and analysis, making data management efficient and accurate.

**Index management**: You can create indexes for collections to accelerate vector similarity search. Before indexes are activated, VikingDB supports automatic tuning of vector index parameters to ensure higher retrieval accuracy with minimal computing overhead. After indexes are activated, VikingDB supports streaming updates of indexes to ensure the timeliness of data retrieval.

**Data retrieval**: VikingDB supports vector retrieval, scalar retrieval, hybrid retrieval, and unstructured data retrieval. Essentially, hybrid retrieval is vector retrieval with attribute filters.

**Elastic scheduling**: When handling an increasing number of retrieval requests, VikingDB automatically schedules more computing resources to ensure service stability.

**Monitoring and alerting**: VikingDB supports end\-to\-end service monitoring and alerting, which ensures the stability of online data retrieval and the efficiency of troubleshooting.
