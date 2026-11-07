---
title: "Product specifications"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Product_specifications"
---

This topic describes the specifications of Milvus for VectorDB Dedicated instances to help you select the appropriate instance specifications when creating a Dedicated instance.

## Instance version

Milvus for VectorDB currently supports Milvus engine versions 2.5, 2.6, and 3.0.

> **tip**

> Milvus 3.0 version instances currently require whitelist access. To use it, [submit a ticket](https://console.byteplus.com/workorder/create/?step=2&SubProductID=P00000255) for approval.

## Instance specification

Dedicated instances consist of service nodes, index nodes, and compute nodes.

* **Service nodes**

   Service nodes include metadata service, Proxy, and Data Node types. The specifications supported by each type of service node are shown in the following table.

   |**Node type** |**vCPU** |**Memory** |
   |---|---|---|
   |Metadata service |2 cores |4 GiB |
   ||2 cores |8 GiB |
   ||2 cores |16 GiB |
   ||4 cores |8 GiB |
   ||4 cores |16 GiB |
   ||4 cores |32 GiB |
   ||8 cores |16 GiB |
   ||8 cores |32 GiB |
   ||8 cores |64 GiB |
   |Proxy |2 cores |4 GiB |
   ||2 cores |8 GiB |
   ||2 cores |16 GiB |
   ||4 cores |8 GiB |
   ||4 cores |16 GiB |
   ||4 cores |32 GiB |
   ||8 cores |16 GiB |
   ||8 cores |32 GiB |
   ||8 cores |64 GiB |
   ||16 cores |32 GiB |
   ||16 cores |64 GiB |
   ||16 cores |128 GiB |
   |Data node |2 cores |4 GiB |
   ||2 cores |8 GiB |
   ||2 cores |16 GiB |
   ||4 cores |8 GiB |
   ||4 cores |16 GiB |
   ||4 cores |32 GiB |
   ||8 cores |16 GiB |
   ||8 cores |32 GiB |
   ||8 cores |64 GiB |
   ||16 cores |32 GiB |
   ||16 cores |64 GiB |
   ||16 cores |128 GiB |

* **Index node and compute node**

   Milvus for VectorDB currently offers Capacity and Performance specifications for index nodes and compute nodes. Version 2.5 instances include Index Node and Data Node, while versions 2.6 and later include Data Node and Query Node.

   * The Capacity index types are DiskANN and HNSW, designed for ultra\-large vector scales where memory is the main bottleneck. They support massive vector retrieval with acceptable millisecond\-level latency while ensuring high recall rates. For applications with huge vector counts, low update frequency, and sensitivity to memory cost, Capacity nodes are suitable, e.g., search engine base, ad and recommend recall layers, knowledge bases and document\-level RAG, massive image and video similarity search scenarios.

   * The index type used for Performance is HNSW, suitable for scenarios requiring high query QPS and low query latency. Performance nodes suit high concurrency, large traffic, and low latency scenarios, e.g., search, recommendation systems, generative AI, and chatbots.

   |**CU type** |**vCPU** |**Memory** |
   |---|---|---|
   |Capacity |4 cores |8 GiB |
   ||4 cores |16 GiB |
   ||4 cores |32 GiB |
   ||8 cores |16 GiB |
   ||8 cores |32 GiB |
   ||8 cores |64 GiB |
   ||16 cores |32 GiB |
   ||16 cores |64 GiB |
   ||16 cores |128 GiB |
   ||32 cores |64 GiB |
   ||32 cores |128 GiB |
   ||32 cores |256 GiB |
   |Performance |4 cores |8 GiB |
   ||4 cores |16 GiB |
   ||4 cores |32 GiB |
   ||8 cores |16 GiB |
   ||8 cores |32 GiB |
   ||8 cores |64 GiB |
   ||16 cores |32 GiB |
   ||16 cores |64 GiB |
   ||16 cores |128 GiB |
   ||32 cores |64 GiB |
   ||32 cores |128 GiB |
   ||32 cores |256 GiB |

## Storage specifications

When you create an instance, the system automatically creates a bucket in [TOS](https://docs.byteplus.com/en/docs/tos/docs-what-is-tos) to store data. You are billed for actual storage space used hourly.
