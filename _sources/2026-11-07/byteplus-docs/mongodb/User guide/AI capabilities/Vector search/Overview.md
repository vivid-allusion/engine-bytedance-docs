---
title: "Overview"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/vector_index_overview"
---

This topic introduces the vector search feature of Document Database for MongoDB.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To use vector search feature, <a href="https://console.byteplus.com/workorder/create/">submit a ticket</a> to contact technical support for applying.</div>


<span id="hRsLOXIO"></span>
## Feature introduction

Vector search is a search method that returns search results based on data semantics or intrinsic meaning. Unlike traditional full\-text search (which is implemented by finding text matches), vector search looks for vectors similar to the search query in a multi\-dimensional space. The closer the distance between the vector and the query, the more similar their meanings. By analyzing the meaning of search queries and data, vector search can consider the searcher's intent and search context, thereby retrieving more relevant results. For more details, refer to [Vector search](https://www.mongodb.com/docs/atlas/atlas-vector-search/vector-search-overview/#what-is-vector-search-).

Document Database for MongoDB provides Vector Search capability. You can combine Vector Search with other embedding models and generative models to meet your needs such as implementing vector search, RAG, and AI Agent in applications. Additionally, Document Database for MongoDB also offers auto\-embedding capability. This, combined with Ark's Embedding model, eliminates the need to maintain vector generation processes in your application.

<span id="2uvdrm3f"></span>
## Common vector search scenarios

Document Database for MongoDB's Vector Search is commonly used in the following vector search scenarios.


* **Semantic search**

   Use ANN or KNN search algorithms to query vector embeddings based on semantic similarity. For more details, refer to [Vector search queries](https://www.mongodb.com/zh-cn/docs/atlas/atlas-vector-search/vector-search-stage/#run-vector-search-queries).

* **Generative search**

   Use MongoDB as a vector database and MongoDB Vector Search to provide retrieval data support for natural language processing (NLP), machine learning (ML), and generative AI applications. For more details, refer to [Use MongoDB for retrieval augmented generation (RAG)](https://www.mongodb.com/zh-cn/docs/atlas/atlas-vector-search/rag/#std-label-avs-rag).


<span id="FVH6vFrC"></span>
## Basic usage procedure

Before using the vector search feature, you need to determine how vectors are generated:


* Auto: When creating an index, specify the text fields and models for embedding. MongoDB automatically generates, stores, and updates vectors, and automatically generates vectors for query text when querying. You do not need to write vector generation code or maintain synchronization between vectors and source data. For specific steps, refer to [Creating auto-embedding vector index](https://docs.byteplus.com/en/docs/mongodb/create-auto-embedding-vector-index?lang=en).

* Manual: Manually call an embedding model to generate vectors, which are then written alongside the original data. When querying, you generate the query vectors yourself.


This second uses the manual method as an example to introduce the specific procedure.


1. Prepare and generate vectors

   Use suitable embedding models (e.g., models provided by BytePlus Ark Platform) to convert raw data (e.g., text, images) into vectors (i.e., arrays of floating\-point numbers). You need to generate this vector data by writing an independent program or script that calls the network interface of the chosen model or loads a local model. Built\-in vector generation is not currently supported.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For specific code implementations on generating vectors using different models and programming languages (e.g., Python examples), refer to <a href="https://www.mongodb.com/zh-cn/docs/vector-search/crud-embeddings/create-embeddings-manual/">How to manually create vector embeddings</a>. This guide provides complete script examples, from loading data and calling models to storing vectors.   </div>
   

2. Store Data and Vectors

   Write raw data and generated vector fields into the collection. Vector fields are stored as an array type (e.g., [0.1, 0.2, ...]).

3. Creating a vector index

   To ensure efficient retrieval performance, create a `vector` type index on the vector field. When creating, focus on these parameters:

   * `type`: Must be set to `\"vector\"`, indicating this is a vector search index.

   * `dimensions`: The vector dimension must be exactly consistent with the vector dimensions output by your embedding model; otherwise, index creation will fail.

   * `similarity`: Vector similarity calculation method. Options include `cosine` (cosine similarity), `euclidean` (Euclidean distance), or `dotProduct` (dot product).

   * `quantization`: Vector quantization type, used to compress vectors to reduce storage and memory overhead. Available values are as follows:

      * `"none"` (default): No quantization, uses full\-precision 32\-bit floating\-point vectors.

      * `\"scalar\"`: Scalar quantization, converts vectors from floating\-point numbers to integers (`int8`), with storage and memory overhead approximately 1/4 of full precision.

      * `\"binary\"`: Binary quantization, converts vectors to a 1\-bit (0 or 1) representation. This method significantly reduces memory overhead.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For information on the index creation process and configuration item descriptions, see <a href="https://docs.byteplus.com/en/docs/mongodb/create_vector_index?lang=en">Creating index</a>.   </div>
   

4. Perform vector search

   Use the `$vectorSearch` aggregation stage to perform vector similarity queries. Specify core parameters such as the query vector (`queryVector`), target index (`index`), and the number of results to return (`limit`). Additionally, it supports pre\-filtering using the `filter` parameter, or balancing query latency and recall by adjusting the `numCandidates` parameter.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For the complete syntax of <code>$vectorSearch</code>, descriptions of all parameters, pre\-filtering details, and performance tuning recommendations, see <a href="https://www.mongodb.com/zh-cn/docs/vector-search/query/aggregation-stages/vector-search-stage/">running vector search queries</a>.   </div>
