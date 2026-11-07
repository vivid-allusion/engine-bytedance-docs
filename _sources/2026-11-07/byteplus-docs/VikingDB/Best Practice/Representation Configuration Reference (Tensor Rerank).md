---
title: "Representation Configuration Reference (Tensor Rerank)"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/representation"
---

<span id="representation-configuration-reference"></span>
# Representation Configuration Reference

In vector retrieval, representation types are the data structures—such as dense vectors, sparse vectors, or tensors—that define how content is matched and indexed. This document explains the benefits and typical use cases for each type. It provides best practices to help you choose and configure the right representation for your needs, whether you want to balance semantic relevance with keyword precision or implement low\-latency reranking.

<span id="what-are-representation-types"></span>
# What Are Representation Types?

In vector retrieval scenarios, a representation type refers to the data structure used to represent a piece of content (text, image, or a multimodal segment). It determines the matching logic and index organization used during retrieval.

VikingDB currently supports the following representation types:


|Representation Type |Description |Benefits |Typical Scenarios |
|---|---|---|---|
|Dense vector |A high\-dimensional vector where most dimensions are non\-zero, typically extracted from text, images, or other data as semantic features. Example: `v = [1.2, 3.4, 5.6, -0.5]` |* Strong semantic recall: retrieves content that is semantically similar even if wording differs<br><br>* Naturally supports multimodality: text, images, and audio can be mapped into a shared space<br><br>* Enables unified TopK retrieval |Use cases that require strong semantic relevance or unified cross\-modal retrieval. Examples:<br><br><br>1. Semantic recall for knowledge bases / Q&A systems (different phrasing, same intent)<br><br>2. Multimodal similarity search<br><br>* Image\-to\-image search: upload an image and retrieve visually similar images<br><br>* Text\-image retrieval: query with text (e.g., “a rose with red petals”) to retrieve images, or upload a photo to retrieve matching textual descriptions<br><br>* Video retrieval: query with text or an image to retrieve semantically similar videos |
|Sparse vector |A high\-dimensional vector where most dimensions are zero, represented explicitly as keyword–weight pairs. Example: `{"what": 0.34, "is": 0.76, "sparse vector": 0.98}`<br><br>Sparse vectors are closer to a keyword\-based representation: only a small number of content\-related terms are activated with weights. |* Strong exact matching: stable for entities, proper nouns, code, numbers, medicines, etc. |Use cases that need keyword precision alongside semantic retrieval, typically combined with dense vectors with adjustable weights. Examples:<br><br><br>1. Domain\-specific search that depends on exact terms (medical, legal/government, code/technical docs)<br><br>2. Weight tuning in hybrid retrieval to balance semantic relevance and keyword precision |
|Tensor |A 2D array of vectors used in retrieval to carry richer, fine\-grained information than a single vector. Example: `[[0.1, 0.2, 0.3], ... , [0.4, 0.5, 0.6]]` |* Richer semantics: captures more fine\-grained semantic or multimodal features<br><br>* Better fine\-grained alignment: more suitable for long\-form content and detail\-level Q&A |Use cases that require fine\-grained matching, low\-latency reranking, or cost control under high concurrency by reducing rerank model token usage. Typically applied as a reranking stage after semantic retrieval. Examples:<br><br><br>1. Fine\-grained text retrieval: long\-document QA, evidence matching in regulations/medical guidelines, multi\-constraint queries with fewer false positives<br><br>2. Local feature alignment for multimodality: align image regions with short text phrases (e.g., locate an object in a specific region)<br><br>3. Low\-latency image/video reranking: performance\-sensitive image/video retrieval where both quality and latency matter<br><br>4. Cost reduction in high\-concurrency text retrieval: replace per\-request model rerank with one\-time offline processing to reduce long\-term costs |


<span id="best-practices-for-representation-types"></span>
# Best Practices for Representation Types

Based on the representation types above, this section summarizes common best\-practice configurations.

<span id="_1-hybrid-dense-sparse-vector-search"></span>
## 1 Hybrid Dense + Sparse Vector Search

<span id="_1-1-applicable-scenarios"></span>
### 1.1 Applicable Scenarios

Hybrid dense + sparse vector search is best suited for scenarios that require both semantic relevance and keyword precision—where a single vector representation is not sufficient. Examples:


1. **Domain\-specific retrieval that depends on keywords**: medical, legal/government, code/technical docs, product/material models, etc., where specific terms must be matched.

2. **Topic\-driven content retrieval**: a user query can be a semantic description of an event or a key entity in the event. Hybrid retrieval can recall semantically relevant content while also ensuring exact\-entity matches, improving coverage and relevance.


<span id="_1-2-workflow-and-principle"></span>
### 1.2 Workflow and Principle

Hybrid nearest\-neighbor retrieval combines dense and sparse vectors to leverage both the semantic matching capability of dense vectors and the exact keyword matching capability of sparse vectors. Dense vectors capture implicit semantic relationships but are weaker at strict keyword/phrase matching, while sparse vectors are more interpretable and precise for explicit terms but do not capture semantics well.

By combining them and tuning their weights, you can balance semantic relevance and keyword precision to improve overall accuracy and coverage.

<span id="_1-3-how-to-configure-hybrid-dense-sparse-retrieval"></span>
### 1.3 How to Configure Hybrid Dense + Sparse Retrieval


1. **Collection setup**

   1. **If you have existing vector data:**  configure a sparse vector field.

   2. **If you start from vectorization:**  choose fields that require keyword/phrase constraints and configure sparse vector representation for those fields.

2. **Retrieval test**

   * In result configuration, adjust **Dense Weight** to specify the relative weight between dense and sparse vectors. A larger value places more emphasis on dense vector retrieval. For details, see [Getting started with vector databases - API V2](https://docs.byteplus.com/en/docs/VikingDB/Getting_started_with_vector_databases_V2).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a0359287225448288a897cc1873b74ac~tplv-goo7wpa0wc-image.image) </span>


3. **API reference**

   1. **If you have existing vector data:**  [Vector Search](https://docs.byteplus.com/en/docs/VikingDB/Vector_Search_V2)

   2. **If you start with vectorization:**  [Multimodal Search](https://docs.byteplus.com/en/docs/VikingDB/Multimodal_Search_V2)


<span id="_2-vector-search-tensor-rerank"></span>
## 2 Vector Search + Tensor Rerank

<span id="_2-1-applicable-scenarios"></span>
### 2.1 Applicable Scenarios

Tensor rerank is suitable for retrieval scenarios that require fine\-grained matching, low\-latency responses, and cost control under high concurrency, for example:


* **Low\-latency image/video search (response time under 300 ms)** : Tensor rerank is recommended for such scenarios. Compared with a rerank model, it can provide quality improvements with much lower latency.

* **High\-concurrency text search (token cost sensitive)** : In high\-concurrency scenarios, model rerank can incur high costs due to token consumption. Tensor rerank is a more economical choice. Although it adds some compute overhead, it is typically cheaper than model token costs.


<span id="_2-2-workflow-and-principle"></span>
### 2.2 Workflow and Principle

Tensor rerank performs a second\-stage ranking after the initial vector recall, balancing effectiveness and efficiency. Its core idea is to shift the “query–document token\-level interaction” earlier by encoding content into token\-level multi\-vectors, and compute maxsim between the query and stored tensors only at search time. This achieves a trade\-off between quality and latency, sitting between full interaction and no interaction.

Tensor representation introduces upfront compute and storage costs, but reduces search\-time overhead. It typically requires only one vectorization and interaction computation offline. Combined with optimizations such as quantization, clustering, and recall\-size tuning, it can outperform rerank models with lower latency.

<span id="_2-3-how-to-enable-tensor-rerank"></span>
### 2.3 How to Enable Tensor Rerank


1. **Collection setup**

   1. **If you have existing vector data:**  configure **Tensor**.

   2. **If you start from vectorization:**  configure **Tensor** representation. The tensor representation field and model must be consistent with the dense vector representation field and model.

2. **Retrieval test**

   * After enabling **Rerank in the console, choose Tensor rerank and configure the number of candidates to be reranked. For details, see **  ** ** **Getting started with vector databases \- API V2.** 


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f963e4a453b646b8876260b1c7631369~tplv-goo7wpa0wc-image.image) </span>


3. **API reference**

   1. **If you have existing vector data:**  [Vector Search](https://docs.byteplus.com/en/docs/VikingDB/Vector_Search_V2)

   2. **If you start with vectorization:**  [Multimodal Search](https://docs.byteplus.com/en/docs/VikingDB/Multimodal_Search_V2)
