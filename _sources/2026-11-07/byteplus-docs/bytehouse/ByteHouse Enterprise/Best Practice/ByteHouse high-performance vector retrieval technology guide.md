---
title: "ByteHouse high-performance vector retrieval technology guide"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/bytehouse-high-performance-vector-retrieval-technology-guide"
---

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Content summary:</strong> The ByteHouse team provides insights into frontier vector databases, challenges in OLAP+ vector retrieval technologies, high\-performance implementation solutions, and related application scenarios\*\*.\*\*</div>


<div data-tips="true" data-tips-type="tip"><strong>Use scenario:</strong> Used in vector retrieval\-related external communications, such as external presentations, content dissemination; vector retrieval\-related in\-client scenarios, etc.</div>


<span id="c6d6a298"></span>
# Introduction

With the application and implementation of LLM (Large Language Models) technology, databases need to enhance vector analytics and AI support capabilities. Vector databases and vector retrieval are increasingly getting attention from the industry. Simply put, vector retrieval technology and vector databases can provide LLM with external memory units, assisting LLM in returning more accurate answers by providing content associated with the problems and historical answers.

It's not just LLMs; vector retrieval and the OLAP engine also have a long history. As software used for data analysis, OLAP can process large amounts of data quickly and efficiently and provide multi\-dimensional analysis functions, while vector retrieval can help enhance the OLAP engine's ability to analyze and retrieve unstructured data.

ByteHouse is a cloud\-native data warehouse launched by the BytePlus engine, which is also an OLAP engine. By adding vector index maintenance and query logic to existing data management mechanisms and query execution pathways, ByteHouse has recently expanded its high\-performance retrieval capabilities. It now supports various vector retrieval algorithms and efficient execution pathways, enabling large\-scale vector retrieval scenarios and achieving millisecond\-level query latency.

"ByteHouse High\-Performance Vector Retrieval Technology Guide V1.0" will integrate the ByteHouse team's cutting\-edge observations on the vector database industry and technology, interpreting how OLAP can build high\-performance vector retrieval capabilities and related real\-world scenarios. Using the open\-source software VectorDBBench testing tool on the cohere 1M standard test dataset, with a recall of 98, ByteHouse's QPS performance can now surpass that of dedicated vector databases.

<span id="5290c0f3"></span>
# Intro to vector search

<span id="2c01573e"></span>
## Concept analysis

The core implementation principle of a vector database is vectorized storage and indexing technology. Vectorized storage refers to converting vector data into a binary format for storage to enhance storage efficiency and search speed. Vector indexing involves indexing vector data to facilitate fast similarity matching and clustering operations.

Vectors in a vector database consist of multiple dimensions, each representing a feature of the vector. For example, a document can simply be represented as a vector comprised of word frequencies. Vectors in a vector database can be either dense or sparse, with dense vectors having values in most dimensions and sparse vectors having values in only a few.

<span id="cd007427"></span>
## Principle introduction

Vector databases can quickly retrieve objects similar to the query because they have pre\-calculated these similarities. One fundamental concept is called Approximate Nearest Neighbor (ANN) search, which utilizes various algorithms for indexing and similarity calculations.

When you have millions of embeddings, calculating the similarity between a query and each embedding you have using a simple k\-Nearest Neighbors (kNN) algorithm becomes time\-consuming. By using Approximate Nearest Neighbor search, you can sacrifice a bit of accuracy for speed and retrieve objects that are approximately the most similar to the query. Indexing \- for this, vector databases index vector embeddings. This step maps the vectors into a data structure for faster search.

<span id="0e17074f"></span>
### Data preprocessing

Before vectorizing storage, the original data needs to be preprocessed, including steps such as data cleaning, feature extraction, and feature normalization. For example, in text vectorization, texts need to be tokenized, stopwords removed, and stems extracted; then, texts are converted into vectors using either the bag\-of\-words model or word vector model.

<span id="e210cb6d"></span>
### Vector encoding

Encode vector data into binary format for storage on disk or in memory. Common vector encoding methods include binary encoding, hash encoding, and compression encoding. Hash encoding maps vectors to a hash table for fast similarity matching. Compression encoding compresses redundant information in vectors to reduce storage space.

<span id="84de24fe"></span>
### Storage management

After encoding the vector data, it is stored on disk or in memory, requiring storage management, including data segmentation, data compression, and data indexing. Data segmentation divides vector data into multiple chunks for distributed storage and querying. Data compression compresses vector data to reduce storage space. Data indexing indexes vector data for fast similarity matching and cluster analysis.

<span id="4394ecad"></span>
### Data query

After vector\-based storage, data queries are required, including similarity matching and cluster analysis. Similarity matching refers to searching a vector database for vectors most similar to the query vector, with common similarity metrics including cosine similarity and Euclidean distance. Cluster analysis involves dividing vector data into multiple clusters to facilitate data analysis and mining.

<span id="a341e056"></span>
## Model selection analysis

The development of current vector databases mainly follows two approaches. One approach constructs a dedicated vector database based on a Vector\-centric design for storing vector data and indexing resources and strategies, offering simple query patterns and limited data type support. The other approach extends the vector search capabilities of existing databases by adding vector index maintenance and query execution logic to existing data management mechanisms and query execution pipelines.

<span id="0cbbd716"></span>
### Dedicated vector database

Dedicated vector databases, such as Milvus and Pinecone, generally support fewer data types and lack enterprise\-level features like multi\-environment deployment options (Local, hybrid, and cloud), disaster recovery, ACID, data security, and governance. This is effective for smaller projects and prototypes, as they can launch very quickly and be used to search PDFs or other unstructured data files.

<span id="36aef3e7"></span>
### Database plus vector extension

Currently in the industry, more databases are expanding their vector capabilities, including Elasticsearch, PostgreSQL, MongoDB, ByteHouse, and others, offering the following advantages:


* **Broader data processing**. Provides vector processing functions as well as traditional database features, such as SQL support and JSON data. This makes the data architecture more complex and typically means that no additional database purchase is necessary, achieving cost savings.

* **The versatility of RAG**. The combination of structured and vector data retrieval can provide richer context for large models, resulting in more accurate context\-awareness.


<span id="482092e1"></span>
# **II. ByteHouse high\-performance vector retrieval**

<span id="5da3d321"></span>
## ByteHouse introduction

ByteHouse is a cloud\-native data warehouse product independently developed by ByteDance Data Platform, built on top of the open\-source ClickHouse Engine with a reconstructed technical architecture. It has achieved cloud\-native deployment and operations management, storage\-computation separation, multi\-tenant management, among other features, and is provided externally through BytePlus. In terms of scalability, stability, maintainability, performance, and resource utilization, ByteHouse has made tremendous improvements.

As of Feb 2022, ByteHouse has been deployed internally within ByteDance at a scale of over 18,000 devices, with individual clusters exceeding 2,400 devices. After intense refining across hundreds of internal application scenarios and tens of thousands of users, it has been promoted and applied among multiple external enterprise customers.

<span id="8383799c"></span>
### Product features

ByteHouse has optimized design and engineering to aim for higher performance, better resource utilization, higher stability, and lower operational costs. The product features and advantages are as follows:


* Separation of storage and computation: It solves challenges such as global metadata management and poor performance due to excessive small files. Separate storage and computation layers with minimal performance loss, allowing independent scaling.

* New generation MPP architecture: Combines a shared\-nothing computational layer and a shared\-everything storage layer, effectively preventing the re\-sharding issues found in traditional MPP architectures while retaining MPP parallel processing capabilities.

* Data consistency and transaction support.

* Computational resource isolation, read and write separation: Flexible division and allocation of host hardware resources through the concept of computational Groups (VW), allowing for scaling as needed. Effective resource isolation, managing read and write operations separately to prevent tasks from affecting each other, and eliminating big queries using up all resources and impacting the cluster.

* ANSI\-SQL: Complete enhancement in SQL compatibility, supporting the ANSI\-SQL 2011 standard with a 100% pass rate on the TPC\-DS test set.

* UDF: Supports the creation and management of Python UDF/UDAF, complementing the extensibility of functions. Java UDF/UDAF is currently under development

* Proprietary Optimizer: Our self\-developed Cost\-Based Optimizer enhances the performance of complex queries, such as multi\-table JOINs, by several folds.


In terms of product capabilities, we provide an array of enterprise\-level features and visual management interfaces beyond the engine.


* Library Table Asset Management: Console creates libraries and tables, managing metadata.

* Multi\-Tenant Management: Supports a multi\-tenant model with isolation between tenants and independent billing.

* RBAC Permission Management: Supports permissions at the library, table, and column levels, including read, write, and resource management. Management is conducted through roles.

* Automatic VW startup and shutdown, elastic scaling: Compute resources are allocated on\-demand, and turned off during idle times. Reduces total cost and improves resource utilization.

* Performance Diagnosis: Provides Query History and Query Profiler functions to help users independently investigate the causes of slow queries.


<span id="2d0b142a"></span>
### Application scenarios

ByteHouse is positioned as a data warehouse product, mainly used for OLAP queries and computations. In scenarios such as real\-time data access, large wide\-table aggregation queries, complex analysis and calculations with massive data, and multi\-table associated queries, it performs exceptionally well.

The main application scenarios are as follows:


|Scene Classification |Scene |Description |Characteristics |
|---|---|---|---|
|Interactive Query |Custom SQL Query |Data App Supporting Multidimensional Query Analysis |Free Dimensions, Multi\-Table Associations, Quick Response |
||Self\-Service Reports |Supporting Tools Like Tableau |Flexible dimensions, multiple table associations, quick response |
||User portrait analysis |Supports DMP and other profile platform |Flexible dimensions, multiple table associations, quick response |
||Marketing effect analysis |Supports traffic effect funnel analysis |Multi\-table association, real\-time |
||Behavior log analysis |Supports log exploration analysis |Log retrieval, large data volume |
|Real\-time Data Dashboard |Real\-time Business Monitoring Screen |Supports DataV and Other Visualization Screens |Real\-time |
||Live Data Statistics Dashboard |Supports Real\-time Reports |Real\-time |
||Business Dashboard |Supports Reporting Tools |Statistics, Quick Response |
||System Link Monitoring |Support real\-time app monitoring |Real\-time |
|Real\-time data warehouse |Real\-time data integration |Support real\-time data writing and updating |Real\-time data writing, immediately visible |
||Near real\-time ETL calculations |Support complex computations and data cleaning |Mixed workload |


<span id="0541da88"></span>
## ByteHouse vector retrieval intro

ByteHouse originates from ClickHouse Engine, but the ClickHouse Engine has problems such as repeated vector index reads and redundant similarity calculations. For vector retrieval scenarios with low latency requirements and high concurrency needs, its usability is weak. ByteHouse has innovated comprehensively in vector retrieval capabilities and has the following features:


* It supports a wide range of SQL syntax and provides numerous functions to help users construct complex queries for both structured and unstructured data, enhancing flexibility and usability.

* Supports OLAP mixed scenarios, supports both structured and unstructured data, and has a broader range of application scenarios compared with dedicated vector databases.

* It reduces the dependency on components in mixed scenarios of text, vector, and OLAP, lowering engineering complexity.

* Decoupling storage and computation architectures makes it easier to address the problem of normal read and write operations being heavily impacted by the construction of index tasks in vector databases.

* The high\-performance query engine of ByteHouse provides a powerful platform for executing vector search\-related queries, enhancing the query performance.

* The system supports query optimizers, which under mixed queries can select the optimal plan according to cost, further enhancing performance.

* It supports real\-time data updates and queries.

* The cost is lower, performance is improved several times compared to ES, and machine resources are saved by 80% in the same scenarios.


<span id="3f541128"></span>
# III. **Technical interpretation**

<span id="9fa6c553"></span>
## Challenges and difficulties

The goal of vector search is to find the k most similar results to a given vector, widely used in scenarios such as image\-based searching and recommendation systems. In the last two years, with the popularization of large models, vector search\-based enhancement of large model retrieval has significantly improved the low accuracy problem of large model results, attracting widespread attention. Therefore, the technology related to vector search as well as the concept of vector databases based on vector search are gradually becoming popular, turning into a hot topic in the database realm.

In practical use scenarios, vector retrieval usually targets datasets ranging from millions to billions in size, and the expected query latency is within a few milliseconds to hundreds of milliseconds. Therefore, brute force computation is typically avoided, and instead, vector retrieval indexes with special structures are used. Popular vector index algorithms include HNSW, Faiss IVF, etc.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a16769fe4be149faa44e9d307d4a1063~tplv-goo7wpa0wc-image.image" width="2664px" /></div>


Vector retrieval workloads based on vector indexes generally have the following characteristics:


* Long build times, high resource consumption: The time taken to build indexes is usually much longer than the time taken for data insertion. For example, various types of indexes for the commonly used gist1M dataset take tens to hundreds of seconds to build. Additionally, building indexes typically consumes significant CPU and memory resources. Therefore, when implementing vector retrieval functions, it is necessary to consider how to efficiently manage the resources needed for index building tasks to ensure quick construction without affecting other tasks.

* In\-memory computation: Indexes like HNSW and Faiss IVF need to load the entire index structure into memory, which usually contains all original vector data and some additional structure\-related data; therefore, the size is generally larger than the total vector data. Due to the large structure, loading indexes takes longer, demanding persistent memory for low latency and high QPS query scenarios. Thus, vector retrieval functions need to consider how to support in\-memory computation and efficient management of memory resources.

* Fusion queries: Users typically need to query many other attribute info of similar vectors, usually combining some scalar Filters to achieve more expected results. Therefore, vector retrieval functions need to consider how to reduce the extra overhead from vector retrieval to other attribute info reading, and how to integrate with filter statements.


Currently, ByteHouse has implemented a skip index solution. Vector indices can be used as a new type of skip index.

However, the original skip index system does not efficiently support calculations related to vector search mainly for the following three reasons:


* ByteHouse lacks a caching mechanism for skip indexes, which cannot ensure that vector indices are always kept in memory.

* Skip indexes are only used for mark level filtering before query plan execution; the results need additional distance calculations to achieve topK results, not solely relying on the results from skip index calculations, which leads to computational redundancy.

* Skip indexes can only be built based on mark granularity (mark \* granule), which for data parts with large volumes, results in multiple skip indexes and thus higher IO and computational overhead.


Considering these factors, the ByteHouse team believes that the existing skip index architecture cannot support high\-performance vector search calculations, therefore a new architecture specifically designed for vector search scenarios has been developed.

<span id="83202e86"></span>
## Architecture design

The overall architecture of ByteHouse's vector search capabilities is shown in the following diagram:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a4c48e81ff8b4078ac963fdf02c83522~tplv-goo7wpa0wc-image.image) </span>

In terms of vector indexing, ByteHouse has integrated popular search algorithm libraries such as hnswlib and faiss, supporting various common indices like HNSW, IVF_PQ, and IVF_PQ_FS. Additionally, considering that vector search needs to be executed in memory, ByteHouse has also implemented a vector index caching mechanism to ensure the indices of the data parts involved in the queries are always kept in memory, achieving low\-latency vector search.

Additionally, ByteHouse has enhanced the existing skip index logic by adding support for index\-building statements, specifying that each data part builds only one index.

To address the issue of high resource consumption during building, ByteHouse has introduced a resource (CPU) control mechanism in the index\-building process and provided on\-disk construction logic for scenarios with substantial memory usage (IVF type index's train method).

In query execution, ByteHouse has implemented pattern recognition and query rewriting targeting vector retrieval\-related queries across different levels, primarily identifying queries related to order by L2Distance/cosineDistance + limit topK. It also introduced a new SelectWithSearch operator, designed for performing actual vector retrieval and reading other attributes.

Comparison of the old and new execution pipelines is as follows:


* Skip Index Based Pipeline


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/089b7a707a5e4ac1b77678f211deeb64~tplv-goo7wpa0wc-image.image" width="1284px" /></div>



* New Pipeline


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84e6c3a5081e4f33b4f967b6513debcd~tplv-goo7wpa0wc-image.image" width="1272px" /></div>


For example, the build statement is as follows:

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


For example, the query statement is as follows:

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


<span id="e70c720b"></span>
## Optimization plan

<span id="62f8af6b"></span>
### Elimination of vector column read operations

Identify whether vector columns are only necessary in vector retrieval operations. If so, omit the vector columns in the final read operation to minimize unnecessary reads.

<span id="106f02af"></span>
### Vector retrieval calculation setup

By default in the execution process, we create a SelectWithSearch Operator for each data part. The process involves performing vector retrieval and reading other attributes for each part. Since the smallest reading unit is a mark, the total number of rows read can be as high as (part_num \* mark_size \* topK) rows. As a result, performance deteriorates as the number of parts increases. To optimize query performance in multi\-part scenarios, we propose a pre\-processing optimization for vector retrieval. Before actually executing the plan, we compute vector retrieval for all parts to get global topK results. Subsequent reads of other attributes for each part are then reduced, with the maximum number of rows read being (mark_size \* topK). In real scenario tests, latency has improved by more than 2x.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/30b54a09dad145ebb5a92efeedd00ade~tplv-goo7wpa0wc-image.image" width="5228px" /></div>


<span id="493ab76b"></span>
### Cache preload

The currently supported vector indexes need to be loaded into memory for high\-performance vector retrieval calculations. During vector retrieval operations, if the vector index for the pending calculation data part is not found in the vector index cache, a load operation must be initiated to load the index into memory. The query will then have to wait until the load operation is complete before continuing. The vector index load operation significantly increases the latency of query execution, especially in scenarios of new data part entries or server restarts.

To address this issue, ByteHouse has added a cache preload mechanism. During data part generation and server startup processes, indexes are automatically loaded into memory. Specific settings to support table\-level and global cache preload configurations are also added.

The mechanism has added support for currently supported engines such as HaMergeTree and HaUniqueMergeTree.

<span id="3aae6bf2"></span>
# IV. Performance evaluation

The ByteHouse team conducts tests using the industry's latest VectorDBBench test tool, with test machine configurations of 80 cores and 376 GB memory. In the cohere 1M standard test dataset, with a recall of 98, QPS can reach more than twice that of the open\-source vector database Milvus (2.3.0). With recall over 95, the highest QPS can reach more than 4200, with p99 latency within 15ms, demonstrating a leading advantage in the industry.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fbdc1fd9577b41f69d8269587add245e~tplv-goo7wpa0wc-image.image" width="1436px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3c893d7f368c45e48d2043789c881584~tplv-goo7wpa0wc-image.image" width="1328px" /></div>


<span id="77db9442"></span>
# V. Application scenarios

The core functionality of vector retrieval is to retrieve the similarity of any data object, such as text, images, videos, sounds, and other digitized content. Thus, application scenarios centered on functionalities like text similarity retrieval, question\-answer retrieval, image sound video retrieval, face recognition, and smart recommendations can be built based on vector retrieval capabilities.

The core application scenarios are as shown in the table below:


|Industry |Application Scenarios |
|---|---|
|Internet E\-commerce |Goods Image Search |
|Internet \- Social |Image deduplication, original video verification, risk control audit, related recommendations, public opinion monitoring |
|Goverment Agencies |Face recognition, video retrieval, fingerprint search, human body image retrieval, vehicle search, content duplicated check |
|Finance |Face recognition, text retrieval, intelligent customer service |
|Retail |Facial recognition, product identification, automatic vending machines |


<span id="7f16dac0"></span>
## Large model applications

Large model applications primarily include corporate knowledge bases, intelligent Q&A, large model assistance systems, and creation assistants (in the content creation field). Enterprises divide industry\-specific content, organize, and enter it into databases for downstream use. Includes searching access for enterprise staff, internal Q&A access within the enterprise, and answering questions more intelligently and logically with the help of large models.

For example, using an exclusive enterprise Q&A knowledge base, the implementation can involve vectorizing document fragments (through language models like BERT) and storing them in ByteHouse. After users pose questions, the system vectorizes the problem statement and computes the top k document fragments most similar to the problem vector in the vector database, using metrics such as cosine similarity or dot product. It then packages the query results into standard answers returned to the application system through the contextual organizing capability of large models.

This scenario is characterized by large data volumes and requires logical segmentation management. The performance requirements range from tens to hundreds of ms, with a high demand for recall rate. ByteHouse is highly performant, scalable, supports massive datasets, and offers good usability support for SQL, making it well\-suited for such scenarios.

<span id="0e079568"></span>
## Product search and recommendation

In the e\-commerce scene, a method that combines scalar data condition retrieval and image retrieval is employed to search for products, allowing users to visually find products of interest more directly; it also enables similar product recommendation functions through vector similarity retrieval features.

For instance, a user wants to search for clothes shipped from Shanghai, priced between 200\-1000 yuan, styled in Korean fashion, and highly similar to an uploaded image. ByteHouse enables a single SQL to carry out retrieval on both scalar and vector data simultaneously, which is simple to use and provides high retrieval performance.

<span id="7e4952ca"></span>
## Image and video search

As shown in the figure below, you can upload an image and enter conditions such as time, similarity, and source of information to retrieve videos similar to the target image from the entire network. This scenario utilizes ByteHouse's capability to mix scalar and vector data in search. The following SQL statement can be used to conduct a quick search:

```SQL
SELECT　unique_id,create_time,image_url,platform,update_time,post_category,post_id,　    post_publish_time,dist　
FROM qian.photo_vec7 
WHERE (post_publish_time >= '2023-11-22 11:00:00') AND (post_publish_time <= '2023-11-24 11:00:00') WHERE (post_category = 1)　
ORDER BY cosineDistance(vector, [10, 5, 23, 17, 9, 9, 3, 12, 32, 40, 32, 3, 8, 26, 26, 54, 93, 91, 8, 7, 41, 22, 19, 119, 5, 8, 77, 33, 61, 55,, 56]) AS dist ASC　LIMIT 100;
```


<span id="3e6a0301"></span>
# Landing case studies

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In today's rapidly digitizing world, sentiment monitoring has become an indispensable tool for every organization and brand. Effective sentiment monitoring helps brands quickly respond to potential negative news in an era of rapidly changing information, reducing the risk of reputation damage, and allows companies to adjust their marketing strategies based on sentiment data, enhancing consumer satisfaction and gaining a competitive edge in the industry.</div>


<div data-tips="true" data-tips-type="tip">A content social integration marketing company aims to use big data systems to provide valuable KOL public/private domain traffic management solutions for corporate clients, and offer social media listening, industry insight, SCRM system management and other comprehensive digital marketing and management services, building an all\-encompassing content ecosystem for advertisers that covers communication, placement, monitoring, and evaluation, creating more valuable marketing services.</div>


<span id="6798b41f"></span>
## Scenario 1: Public opinion monitoring

**Background:** 

Public opinion monitoring requires high real\-time performance of data. In existing technology plans, the enterprise uses its self\-built Elasticsearch to provide capability for similarity searches in public opinion, but from the perspectives of performance and cost, it cannot fully meet the business needs. In terms of performance, the system is required to support tens of thousands of QPS for real\-time search, and the Elasticsearch solution struggles to achieve such high concurrency metrics. Cost\-wise, the use of the Elasticsearch solution comes with high machine resource costs. As data volume continues to grow, the cost of machine resources becomes increasingly uncontrollable; moreover, the data writing and querying process is quite complex, resulting in high application development costs.

**Problems and requirements:** 

The enterprise has tens of billions of public opinion data, with QPS peaks reaching tens of thousands. For all analytical type databases, not only must they have the ability to handle complex OLAP analysis scenarios, but they also need to support ultra\-high QPS online pinpoint services, achieving high throughput, low latency, and high stability, which are significant challenges.

**Solution:** 


* ByteHouse employs a multi\-copy mechanism, writes total data to the primary node, automatically syncs to multiple copies in real\-time, and achieves automatic load balancing and multi\-read via gateway queries, thereby linearly enhancing concurrency capability.

* ByteHouse also supports executing business logic through SQL write and query operations, further simplifying the data processing workflow and enhancing development efficiency. In terms of resource efficiency, ByteHouse adopts a flexible resource model that supports any number of nodes and replicas adjustments. Initially, users only need to purchase the minimum resources, which can be scaled up instantly as the business grows, making costs more controllable.


**Application effects:** 

Under 1 billion data records, single node QPS peak exceeds 3000. With 2 billion data records, single node QPS peak reaches 1000+, which is several times higher than ES performance; machine resources reduced from 32C*10 nodes in ES to 32C*3 nodes in ByteHouse.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/794a1fcf59ff419698b2316820053d84~tplv-goo7wpa0wc-image.image" width="582px" /></div>


<span id="866870ae"></span>
## Scenario 2: **Image search by image**

**Background:** 

ByteHouse supports converting unstructured data such as images, videos, and articles into vectors, storing them in ByteHouse, and then querying for similar images based on conditions and vector similarity using SQL.

**Background and requirements:** 

In the public opinion monitoring scenario of the business, users need to input a photo, select a time range and a target platform (Douyin, Kuaishou, Weibo, etc.), and then retrieve similar images and videos. Currently built on ES, the retrieval response is slow, requires more resources, and fails to meet business needs.

**Application effectiveness:** 

Under the same data and application conditions, using ByteHouse as the query engine reduces the required machine resources by 60%, while image retrieval performance increases eightfold.

<span id="210df89f"></span>
# Method of use

<span id="49f9c551"></span>
## Create table

Create a table using the 'create table' statement, storing vector feature data in Array type fields. An index can be added to the vector feature field. The index can either be added during table creation or after the table is created.

Create index as defined when creating the table:

```SQL
CREATE TABLE test_vector
(
    `id` UInt64,
    `label` String,
    `vector` Array(Float32),
    INDEX v1 vector TYPE HNSW('DIM=960, METRIC=COSINE'),
    CONSTRAINT cons_vec_len CHECK length(vector) = 960 -- Used for data insertion check
)
ENGINE = MergeTree
ORDER BY id
SETTINGS 
index_granularity = 1024, -- Alleviate the read amplification problem
index_granularity_bytes = 0 -- Avoid generating adaptive marks
```


Add index using alter add index as follows:

```SQL
ALTER TABLE test_vector ADD INDEX v1 vector TYPE HNSW('DIM=960, METRIC=COSINE')
```


<span id="caf8cd27"></span>
## vQuery

Retrieve scalar and vector data using the following statements:

```SQL
select 
    id， 
    label,
    dist 
from test_vector 
where id>100 and label='a' 
order by cosineDistance(vector, [query_vector]) as dist 
limit 100 
settings enable_new_ann=1
```


<span id="cc62603a"></span>
# VIII. Summary and outlook

As a routine technology in the database field, more traditional databases will support vector retrieval technologies in the future, along with more user\-friendly, high\-performance vector retrieval algorithms and libraries.

Looking at industry developments, currently, we can see two directions for innovation: one is the innovation in retrieval algorithms and indices, including adaptive parameter tuning, early termination, integration with filters, vector compression, distributed retrieval structures, etc.; the other is system\-level innovations, including real\-time vector retrieval, embedded vector retrieval modules, index recommendation, data privacy protection, etc.

Currently, ByteHouse has implemented a high\-performance vector database framework. In the future, it will explore and optimize areas such as low resource consumption vector indexing, query performance optimization, user\-friendliness, and large model ecosystems.
