---
title: "Overview"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/vector-search-overview-ce"
---

ByteHouse provides high\-performance vector search capabilities, allowing vector search via SQL statements and Python API, supporting multiple vector search algorithms, including vector similarity calculation, vector clustering, and vector similarity queries. This article introduces ByteHouse's vector search capabilities.

<span id="7ca4d892"></span>
# **Introduction**

ByteHouse is based on ClickHouse, but ClickHouse has issues such as repeated vector index reads and redundant similarity calculations. This leads to lower availability for vector search scenarios that require low latency and high concurrency. ByteHouse innovates comprehensively in vector search capabilities and has the following features:


* It offers comprehensive SQL syntax support and provides numerous functions to help users construct complex queries mixing structured and unstructured data, enhancing flexibility and usability.

* It supports OLAP mixed scenarios, handling both structured and unstructured data, offering broader application scenarios than current dedicated vector databases.

* It reduces component dependencies in mixed scenarios involving text, vectors, and OLAP, lowering engineering complexity.

* The storage\-compute separation architecture more easily resolves the heavy index construction tasks of vector databases without affecting normal read and write operations.

* ByteHouse is a high\-performance query engine that provides an efficient execution foundation for vector search\-related queries, optimizing query performance.

* Support project for the query optimizer allows selecting the optimal plan based on cost in hybrid queries, further improving performance.

* Support project real\-time data updates and real\-time queries.

* Lower cost, with performance improvements several times higher than ES, saving 80% of machine resources in the same scenario.


<span id="d581bf2d"></span>
# Architecture

The overall architecture of ByteHouse’s vector retrieval function is shown in the figure below:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9373c54828a941b48fef2175247f0191~tplv-goo7wpa0wc-image.image" width="1280px" /></div>


For vector indexing, ByteHouse integrates two popular retrieval algorithm libraries: [HNSW (hnswlib)](https://github.com/nmslib/hnswlib) and [Faiss](https://github.com/facebookresearch/faiss), supporting commonly used indexes such as HNSW, FLAT, IVF_FLAT, IVF_PQ, and IVF_PQ_FS. Additionally, considering vector retrieval must run in memory, ByteHouse introduces a vector index caching mechanism to ensure data part indexes involved in queries remain resident in memory for low\-latency vector retrieval.

Moreover, based on the existing skip index logic, ByteHouse adds support for building corresponding index statements, specifying that each data part builds only one index.

To address high resource consumption in index building, ByteHouse adds CPU resource control during the index building process and offers on\-disk building logic for large memory usage scenarios (training methods of IVF\-type indexes).

In query execution, ByteHouse identifies patterns and rewrites queries related to vector search at various levels. Currently, it mainly recognizes queries with order by L2Distance/cosineDistance + limit topK. Based on the calculation characteristics of vector search, it implements a new SelectWithSearch operator to perform actual vector search and other attribute read operations.

Comparison between old and new execution pipelines is as follows:


* Skip Index Based Pipeline

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a1d1777060cf4b31942da8e60b37db16~tplv-goo7wpa0wc-image.image" width="1284px" />   </div>
   

* New Pipeline

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eca6cbb41cb74926aa14ccae93eee1a9~tplv-goo7wpa0wc-image.image" width="1272px" />   </div>
   


Example query construction statements are as follows:

```SQL
CREATE TABLE test_ann 
(
    `id` UInt64,
    `label` String,
    `vector` Array(Float32),
    INDEX v1 vector TYPE HNSW('DIM=960, METRIC=COSINE')
)
ENGINE = MergeTree
ORDER BY id
```


Example query statements are as follows:

```SQL
select  
    id， 
    label,
    dist 
from test_ann 
prewhere label = '...'
order by cosineDistance(vector, [query_vector]) as dist 
limit 100 
```


<span id="c290521c"></span>
# Performance evaluation

The ByteHouse team tested using the industry’s latest VectorDBBench tool on a machine configured with 80 cores and 376 GB memory. On the cohere 1M standard dataset, at 98 recall, QPS can exceed twice that of the open\-source vector database Milvus (2.3.0). With recall above 95, QPS can reach over 4200, and p99 latency stays below 15 ms, demonstrating industry\-leading performance.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0721a73e74014df6b5f6cfd320db8445~tplv-goo7wpa0wc-image.image" width="1436px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1260e51f7b8c425da24c09449aefaefc~tplv-goo7wpa0wc-image.image" width="1328px" /></div>


<span id="f9021e79"></span>
# Application scenarios

The core function of vector search is to retrieve the similarity of any data objects, such as the similarity of texts, images, videos, sounds, and all other digital content. Therefore, application scenarios focused on text similarity search, question\-and\-answer retrieval, image, audio, and video search, face recognition, and intelligent recommendation can all be built based on vector search capabilities.

The core application scenarios are shown in the table below:


|Industry |Application scenarios |
|---|---|
|E\-commerce |Goods image search |
|Social media |Image deduplication, video originality verification, risk control review, related recommendations, public opinion monitoring |
|Government agencies |Face recognition, video search, fingerprint search, human body image search, vehicle search, content deduplication |
|Finance |Face recognition, text search, intelligent customer service |
|Retail |Face recognition, product recognition, vending machine |


<span id="79543318"></span>
## Large model applications

Large model applications mainly include enterprise knowledge bases, intelligent Q&A, large model\-assisted systems, and creative assistants (content creation field). These involve segmenting, organizing, and entering deeply relevant enterprise industry content into a database for downstream use. This includes search and access by enterprise employees, internal enterprise Q&A access, and cooperating with large models to answer questions more intelligently and logically.

Taking an enterprise\-exclusive Q&A knowledge base as an example, the implementation plan can vectorize document fragments (using language models like BERT) and store them in ByteHouse. After the user asks a question, the system vectorizes the query sentence and calculates the top k document fragments most similar to the question vector in the vector database using metrics such as cosine similarity or dot product. The large model then organizes the context to package the query results into a standard answer returned to the application system.

This scenario features a large data volume and requires logical segmentation management; performance demands range from tens to over one hundred milliseconds, with a high recall rate requirement. ByteHouse offers high performance, strong scalability, supports massive datasets, and provides good SQL usability, making it well suited for this type of scenario.

<span id="932abdcf"></span>
## Product search and recommendation

In e\-commerce scenarios, use a combination of scalar data condition search and image search to help users easily find interested products; you can also use vector similarity search to recommend similar products.

For example, users can search for clothes shipped from Shanghai, priced between 200 and 1000 yuan, in Korean style, that closely match an uploaded picture. ByteHouse enables searching both scalar and vector data with a single SQL query, making it simple to use and highly efficient.

<span id="2958b257"></span>
## Image and video search

As shown below, you can upload an image and specify conditions like time, similarity, and source to search for videos across the web that resemble the target image. This scenario uses ByteHouse’s mixed scalar and vector data search capability with the following SQL query for fast retrieval:

```SQL
SELECT　unique_id,create_time,image_url,platform,update_time,post_category,post_id,　    post_publish_time,dist　
FROM qian.photo_vec7 
WHERE (post_publish_time >= '2023-11-22 11:00:00') AND (post_publish_time <= '2023-11-24 11:00:00') WHERE (post_category = 1)　
ORDER BY cosineDistance(vector, [10, 5, 23, 17, 9, 9, 3, 12, 32, 40, 32, 3, 8, 26, 26, 54, 93, 91, 8, 7, 41, 22, 19, 119, 5, 8, 77, 33, 61, 55,, 56]) AS dist ASC　LIMIT 100;
```


<span id="d9690579"></span>
# Vector Search Guide

ByteHouse’s vector search is an advanced feature you can activate and use as needed.


* General operation guide: [Enable vector search](https://docs.byteplus.com/docs/bytehouse/start-vector-search-service), [Use vector search with SQL](https://docs.byteplus.com/docs/bytehouse/use-vector-search), [Use vector search with Python API](https://docs.byteplus.com/docs/bytehouse/python-api).

* Best practice: [Best practice for vector search](https://docs.byteplus.com/docs/bytehouse/best-practice-for-vector-search).


<span id="cfeb17ad"></span>
# Related reference: ByteHouse high\-performance vector search technical guide

For more ByteHouse vector search features, see [ByteHouse high-performance vector retrieval technology guide](https://docs.byteplus.com/docs/bytehouse/bytehouse-high-performance-vector-retrieval-technology-guide).
