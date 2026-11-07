---
title: "Use vector search with SQL"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/use-vector-search"
---

ByteHouse provides vector data management and similarity search features, supporting multiple common Approximate Nearest Neighbor (ANN) algorithms to improve search performance and handle unstructured data. This article explains how to perform vector search in ByteHouse using SQL statements with the HNSW, HNSW_SQ, or Faiss indices algorithm libraries.

<span id="0ac2e0d7"></span>
# Background information

ByteHouse currently supports two popular search algorithm libraries: [HNSW (hnswlib)](https://github.com/nmslib/hnswlib) and [Faiss](https://github.com/facebookresearch/faiss), including common indexes such as HNSW, FLAT, IVF_FLAT, and IVF_PQ.

The HNSW algorithm library uses a graph\-type index that maintains M nearest neighbor nodes for each node based on the small\-world graph concept. It also maintains a hierarchical graph structure, which becomes sparser toward the top. Queries begin at the top layer, find the closest point, then proceed to the next layer, continuing until the bottom layer to retrieve the k nearest neighbors for the query vector.

Faiss is Facebook’s open\-source ANN algorithm library featuring multiple types of indexes such as Inverted File (IVF), Product Quantization (PQ), and Scalar Quantization (SQ). Many index types can also be combined. ByteHouse mainly uses Faiss IVF indexes and supports vector compression methods like PQ and PQ_FS (Fast Scan) to reduce index memory usage.

For more details on ByteHouse’s high\-performance vector search, see [Overview](https://docs.byteplus.com/docs/bytehouse/vector-search-overview-ce).

<span id="43bff1da"></span>
# Prerequisites


* Ensure you use ByteHouse version v2.6 or above. You can log in to the ByteHouse console, enter the **Cluster list**, click the target cluster, and check the engine version on the **Basic information** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31ca108046f64d40b89d9e8c335325cd~tplv-goo7wpa0wc-image.image) </span>

* Ensure you have [Enable vector search](https://docs.byteplus.com/docs/bytehouse/start-vector-search-service).


<span id="abd0d02e"></span>
# Quick Start

The ANN algorithm library is accessed via indexes, supporting adding definitions by creating or altering tables. After defining the index, you can insert data and query using the index. This chapter uses the HNSW index type as an example to help you quickly get started with vector search functionality. For detailed descriptions of different indexes, see the [Use HNSW index](https://docs.byteplus.com/docs/bytehouse/use-vector-search#e5586cdc), [Using HNSW_SQ index](https://docs.byteplus.com/docs/bytehouse/use-vector-search#c201ba16), and [Use Faiss Indices index](https://docs.byteplus.com/docs/bytehouse/use-vector-search#e07e296e).

<span id="3f6d644f"></span>
## Build index

<span id="3f25620b"></span>
### Method 1: Create a new table

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
SETTINGS 
index_granularity = 1024, -- Alleviate read amplification issues
index_granularity_bytes = 0 -- Avoid generating adaptive marks
```


<span id="87b806bc"></span>
### Method 2: Modify an existing table

```SQL
ALTER TABLE test_ann ADD INDEX v1 vector TYPE HNSW('DIM=960, METRIC=COSINE')
```


**Parameter description**


|Parameter items |Required |Configuration description |
|---|---|---|
|`test_ann` |Yes |Custom table name. |
|``vector`Array(Float32)` |Yes |Define the `vector` column data type as `Array(Float32)`. It is typically used to store vector data. |
|`INDEX v1 vector` |Yes |Define the index. This article defines an index named `v1` based on the `vector` field to speed up queries on the vector field. |
|`TYPE HNSW('DIM=960, METRIC=COSINE')` |Yes |Define the index type used and configure the related internal parameters for the index type.<br><br><br>* Index types: currently supports HNSW, HNSW_SQ, FLAT, IVF_FLAT, IVF_PQ, IVF_PD_FS.<br><br>* Internal parameters: configure internal parameters in key\-value format, separating multiple parameters with commas, for example: DIM=960, METRIC=COSINE. Of which:<br><br>   * DIM: It defines the dimension information of the index vector and must match the actual vector dimension.<br><br>   * METRIC: It defines the metric method used when building the index. The METRIC parameter is optional; the default is L2. You can also manually set it to L2 or COSINE. Note that only the corresponding metric's distance function can perform index\-based query operations. For example, if the index metric is L2, subsequent queries must use the `L2Distance` function to utilize the index. Likewise, if the metric is COSINE, the `cosineDistance` function must be used for queries.<br><br><br>For detailed guidance on index types, please refer to [Use HNSW index](https://docs.byteplus.com/docs/bytehouse/use-vector-search#e5586cdc), [Using HNSW_SQ index](https://docs.byteplus.com/docs/bytehouse/use-vector-search#c201ba16), and [Use Faiss Indices index](https://docs.byteplus.com/docs/bytehouse/use-vector-search#e07e296e) sections. |
|`ENGINE` |specifies |The storage engine for the table. Configured as MergeTree. |
|`ORDER BY` |Yes |It specifies the data sorting in the table. |
|`SETTINGS` |No |* `index_granularity`: refers to the index granularity, that is, the number of rows each mark in the index corresponds to. Setting this parameter can reduce read amplification and improve query performance.<br><br>* `index_granularity_bytes`: refers to the index granularity in bytes. When set to 0, it prevents generating adaptive marks, so marks are created based only on row count, not data byte size.<br><br><br>For the complete list of configurable settings parameters supported by ByteHouse, see [Settings parameters](https://docs.byteplus.com/docs/bytehouse/use-vector-search#fc1ac31d). |


<span id="f27c8f6a"></span>
## Insert data

ByteHouse’s own insert statements and streaming imports such as Kafka are supported. For details, see the [data import](https://www.volcengine.com/docs/6464/152224) document. Examples are as follows:


* Import data through VALUES field.

   ```SQL
   INSERT INTO test_ann (id, vector) VALUES (1, [1.0, 1.0, 1.0]),(2, [2.0, 2.0, 2.0])
   ```
   

* Import data using CSV files.

   ```SQL
   INSERT INTO test_ann FORMAT CSV infile '/filename.csv'
   ```
   


<span id="180b0922"></span>
## Use index queries

This section explains how to query data using indexes, including regular queries and mixed queries with added `prewhere` conditions. Additionally, ByteHouse supports adding `where` conditions to filter search results, selecting records that meet criteria through similarity thresholds. For details, see [Distance filtering](https://docs.byteplus.com/docs/bytehouse/use-vector-search#3c59aa9e).

<span id="7e8205be"></span>
### Regular search

```Python
select 
    id， 
    label,
    dist 
from test_ann 
order by cosineDistance(vector, [query_vector]) as dist 
limit 100 
settings enable_new_ann=1
```



|Parameter items |Required |Configuration description |
|---|---|---|
|`cosineDistance(vector, [query_vector])` |Yes |Define the vector similarity calculation formula.<br><br><br>* The Distance function must match the metric defined in the index to use the index correctly. For example, if the metric is defined as cosine in the table creation syntax, the query syntax must also use cosine.<br><br>* `vector` is the defined vector field.<br><br>* `[query_vector]` is the query vector you need to input. |
|`order by ... as dist` |yes |Rename the calculated result as `dist` and sort in ascending order.<br><br>Currently, only queries with the `order by {metric}Distance limit k` mode use vector index calculation. |
|`limit` |yes |Set the number of records returned. |
|`settings` |yes |`enable_new_ann`: set to 1 to activate the new ANN query path implementation.<br><br>For the full list of configurable ByteHouse settings parameters, refer to [Settings parameters](https://docs.byteplus.com/docs/bytehouse/use-vector-search#fc1ac31d). |


<span id="d46377f8"></span>
### Hybrid search

ByteHouse supports hybrid searches with `prewhere`, such as the following example using `prewhere id > 1000` to add pre\-filtering conditions, processing only records where `id > 1000`.

```Python
select 
    id,
    label,
    dist 
from test_ann 
prewhere id > 1000
order by cosineDistance(vector, [query_vector]) as dist 
limit 100 
settings enable_new_ann=1
```


<span id="e5586cdc"></span>
# Use HNSW index

<span id="a66d2f2a"></span>
## Index construction syntax

When using the HNSW index, parameters `M` and `EF_CONSTRUCTION` can be defined to balance performance and accuracy. Generally, the larger the `M` and `EF_CONSTRUCTION`, the longer the index construction time, higher accuracy, and increased search latency. Examples are as follows:

```Python
CREATE TABLE test_ann
(
    `id` UInt64,
    `vector` Array(Float32),
    INDEX v1 vector TYPE HNSW('DIM=960, METRIC=COSINE, M=32, EF_CONSTRUCTION=512')
)
ENGINE = MergeTree
ORDER BY id
SETTINGS index_granularity = 1024
```


The configurable index parameters for the HNSW index are explained as follows. Please refer to [Index parameters](https://docs.byteplus.com/docs/bytehouse/use-vector-search#e7fa6486) for the complete index parameter table and usage suggestions.


|Parameter |Required |Configuration description |
|---|---|---|
|`M` |No |Defines the maximum number of connections (Max Connections) per node in the HNSW graph, with a default value of 16. When the M value is large (for example set to 32), search speed can be improved, but memory usage increases. When the M value is small (for example set between 4 and 16), memory usage can be reduced, but recall rate decreases. |
|`EF_CONSTRUCTION` |No |Defines the exploration factor used in index construction, with a default value of 200. The higher this value (e.g., 512), the better the search accuracy, but the construction time is longer. The lower this value (e.g., 100), the faster the construction speed, but the index quality may decrease. |


<span id="76d1d065"></span>
## Query syntax

You can use query statements to search data.

Additionally, ByteHouse supports adding `prewhere` clauses for pre\-filtering conditions; see [Hybrid search](https://docs.byteplus.com/docs/bytehouse/use-vector-search#d46377f8) for details. It also supports adding `where` clauses to filter search results and select records that meet similarity thresholds; see [Distance filtering](https://docs.byteplus.com/docs/bytehouse/use-vector-search#3c59aa9e) for details.

```Python
select 
    id， 
    dist 
from test_ann 
order by cosineDistance(vector, [query_vector]) as dist 
limit 100 
settings enable_new_ann=1, hnsw_ef_s=200
```


**Parameter description**


|Parameter Item |Required |Configuration Description |
|---|---|---|
|`settings` |Yes |`hnsw_ef_s`: This value controls accuracy and latency. The larger the parameter value, the higher the accuracy and the longer the latency; after exceeding the `EF_CONSTRUCTION` parameter, accuracy theoretically does not improve further.<br><br>For the full list of configurable settings parameters supported by ByteHouse, see [Settings parameters](https://docs.byteplus.com/docs/bytehouse/use-vector-search#fc1ac31d). |


<span id="c201ba16"></span>
# Using HNSW_SQ index

The HNSW SQ index supports SQ compression of vectors (compressed to Int8 by default), significantly reducing index size and slightly improving performance compared with the original HNSW algorithm.

<span id="e7ca5765"></span>
## Index construction syntax

```Python
CREATE TABLE test_ann
(
    `id` UInt64,
    `vector` Array(Float32),
    INDEX v1 vector TYPE HNSW_SQ('DIM=960', 'METRIC=COSINE', 'M=32', 'EF_CONSTRUCTION=512', 'SQ=8bit')
)
ENGINE = MergeTree
ORDER BY id
SETTINGS index_granularity = 1024
```


The HNSW_SQ index supports configuring the following index parameters. Please refer to [Index parameters](https://docs.byteplus.com/docs/bytehouse/use-vector-search#e7fa6486) for the complete index parameter table and usage suggestions.


|Parameter items |Required |Configuration description |
|---|---|---|
|`TYPE HNSW_SQ` |Yes |Defines the algorithm type to use; ByteHouse currently only supports setting one index type. This indicates that the HNSW_SQ algorithm is used to build the index. |
|`SQ` |Yes |Define the floating\-point number compression value to reduce memory usage and speed up calculations. The default compression is 8bit, that is, an 8\-digit integer. |


<span id="a4980c6a"></span>
## Query syntax

The query syntax of the HNSW_SQ algorithm library is consistent with HNSW, please refer to HNSW’s [Query syntax](https://docs.byteplus.com/docs/bytehouse/use-vector-search#76d1d065).

<span id="e07e296e"></span>
# Use Faiss Indices index

<span id="d24f139c"></span>
## Cautions

Faiss differs from HNSW in that it trains during index construction, which consumes significant CPU resources. When using, set the following parameters carefully:


* Set the index cache size based on memory capacity, configurable via the `vector_index_cache_size` parameter, defaulting to 200GB. This parameter is implemented based on the Least Recently Used (LRU) strategy.

* If sensitive to cold starts and memory allows, enable the `enable_vector_index_preload` parameter to load the constructed index into memory during write operations.

* During testing, monitor CPU usage. If CPU usage is too high, the following measures can be taken:

   * Limit merge concurrency by setting the parameter value for `max_replicated_merges_in_queue`.

   * Limit train index concurrency by setting the parameter value for `vector_index_build_threads`, with a default value of 8.


<span id="d56dfded"></span>
## Index\-building syntax

Faiss offers four common index types and corresponding tuning parameters for accuracy adjustment.

<span id="a967c8bd"></span>
### FLAT index

FLAT is the simplest index type in Faiss, based on brute\-force search. It stores all vectors in memory and calculates the distance between the query vector and all vectors to return the nearest neighbors. FLAT is simple to implement, requires no training, and is highly accurate, but its time complexity is O(n), making it unsuitable for very large\-scale databases. It is recommended to use it when the data volume is small, vector dimensions are low, query speed requirements are not high, but precise results are needed.

```SQL
CREATE TABLE tab_flat
(
    id Int32, 
    vector Array(Float32), 
    INDEX faiss_index vector TYPE FLAT('dim=4') GRANULARITY 1
) 
ENGINE = MergeTree 
ORDER BY id 
SETTINGS index_granularity = 128
```


The FLAT index supports configurable index parameters explained as follows. See [Index parameters](https://docs.byteplus.com/docs/bytehouse/use-vector-search#e7fa6486) for the full index parameter table and usage recommendations.


|Parameter items |Required |Configuration description |
|---|---|---|
|`dim` |Yes |Define the dimension of the corresponding vector. |
|`metric` |No |Define the metric used to build the index. The METRIC parameter is optional, defaulting to L2. You can also manually set it to L2 or COSINE. |
|`GRANULARITY` |No |Define the index granularity, indicating that an index is built for every data block (mark). |


<span id="c150156b"></span>
### IVF_FLAT index

The IVF_FLAT index combines the advantages of IVF and FLAT indexes, significantly improving query efficiency while maintaining high search accuracy. It is suitable for medium to large\-scale low\-dimensional vector retrieval tasks (e.g., 4\-128 dimensions).

```SQL
CREATE TABLE tab_ivf_flat
(
    id Int32, 
    vector Array(Float32), 
    INDEX faiss_index vector TYPE IVF_FLAT('dim=4') GRANULARITY 1
) 
ENGINE = MergeTree 
ORDER BY id 
SETTINGS index_granularity = 128
```


The supported configurable index parameters for IVF_FLAT are described below. See [Index parameters](https://docs.byteplus.com/docs/bytehouse/use-vector-search#e7fa6486) for the full index parameter table and usage recommendations.


|Parameter Items |Required |Configuration Description |
|---|---|---|
|`dim` |Yes |It defines the dimension of the corresponding vector. |
|`metric` |No |It defines the metric method used for indexing. The METRIC parameter is optional, with the default set to L2. You can manually configure it as L2 or COSINE. |
|`nlist` |No |It defines the number of cluster centers required for IVF index type; the higher the number, the slower the build. If not set, the engine will automatically infer it based on the following logic. You can specify the cap of `nlist` for each part when building an index using the `nlist` parameter during table creation.<br><br>```Java```<br>```static size_t decideIndexNlist(size_t n)```<br>```{```<br>```    if (n < ONE_MILLION)```<br>```        return std::min(int(n), int(4 * std::floor(std::sqrt(n))));```<br>```    else if (n >= ONE_MILLION && n < ONE_MILLION * 2)```<br>```        return 1024;```<br>```    else if (n >= ONE_MILLION * 2 && n < TEN_MILLION)```<br>```        return 4096;```<br>```    else if (n > TEN_MILLION)```<br>```        return 65536;```<br>```}```<br> |
|`GRANULARITY` |no |It defines the index granularity, indicating that an index is created for every 1 data block (mark). |


<span id="17927edb"></span>
### IVF_PQ index

The IVF_PQ index is an efficient vector compression and indexing method combining inverted file (IVF) and product quantization (PQ) techniques. It greatly reduces memory usage while maintaining high search accuracy, suitable for ultra\-large\-scale datasets (over hundreds of millions of vectors).

```SQL
CREATE TABLE tab_ivf_pq
(
    id Int32, 
    vector Array(Float32), 
    INDEX faiss_index vector TYPE IVF_PQ('dim=4','m=4','nbit=4') GRANULARITY 1
) 
ENGINE = MergeTree 
ORDER BY id 
SETTINGS index_granularity = 128
```


The supported configurable index parameters for IVF_PQ are described below. See [Index parameters](https://docs.byteplus.com/docs/bytehouse/use-vector-search#e7fa6486) for the full index parameter table and usage recommendations.


|Parameter items |Required |Vonfiguration description |
|---|---|---|
|`dim` |Yes |It defines the dimension of the corresponding vector. |
|`metric` |No |It defines the metric used when creating the index. The METRIC parameter is optional; the default value is L2. You can also manually set it to L2 or COSINE. |
|`m` |Yes |It defines the number of subvectors for product quantization. Recommended values are 64 or 32. The value must be a power of 2, ranging between 1 and std::min(dim, 64). |
|`nbit` |No |It defines the number of quantization bits per subvector. default value 8, usually no need to change, value is even number, typical range is [1, 16]. |
|`nlist` |Yes |It defines the number of cluster centers needed for IVF type index; the more centers, the slower the construction; if not set, the engine calculates automatically. |
|`GRANULARITY` |No |It defines index granularity, indicating one index built per data block (mark). |


<span id="fffd457c"></span>
### IVF_PQ_FS index

The IVF_PQ_FS index is an enhanced version of IVF_PQ, adding fast scan and refine functions. It improves retrieval accuracy while maintaining compression advantages, suitable for large\-scale vector data requiring high precision search.

```SQL
CREATE TABLE tab_ivf_pq_fs
(
    id Int32, 
    vector Array(Float32), 
    INDEX faiss_index vector TYPE IVF_PQ_FS('dim=4','m=4') GRANULARITY 1
) 
ENGINE = MergeTree 
ORDER BY id 
SETTINGS index_granularity = 128
```


The IVF_PQ_FS index supports configurable index parameters described as follows. For the full list of index parameters and usage recommendations, see [Index parameters](https://docs.byteplus.com/docs/bytehouse/use-vector-search#e7fa6486).


|Parameter items |Required or not |Configuration description |
|---|---|---|
|`dim` |Yes |It defines the dimension of the corresponding vector. |
|`metric` |No |It defines the metric method when building the index. The METRIC parameter is optional; the default value is L2. You can also manually set it to L2 or COSINE. |
|`m` |Yes |It defines the number of subvectors for product quantization. Commonly recommended values are 64 or 32, with a value range of 2 to the power of n, ranging between [1, std::min(dim, 64)]. |
|`refine` |No |It defines the quantization method used in the refinement stage. The default is RFlat, which offers the highest accuracy. Other scalar quantization methods such as SQ4, SQ6, SQ8, and SQfp16 can also be used. Accuracy ranking from high to low is RFlat \> SQfp16 \> SQ8 \> SQ6 \> SQ4, with memory usage decreasing accordingly. The following is an example using SQ8:<br><br>```SQL```<br>```CREATE TABLE tab_ivf_pq_fs_sq8```<br>```(```<br>```    id Int32,```<br>```    vector Array(Float32),```<br>```    INDEX faiss_index vector TYPE IVF_PQ_FS('dim=4','m=2', 'refine=SQ8') GRANULARITY 1```<br>```)```<br>```ENGINE = MergeTree```<br>```ORDER BY id```<br>```SETTINGS index_granularity = 128```<br> |
|`nlist` |No |It defines the number of cluster centers required for the IVF index type. The more centers, the slower the build. If not set, the engine will automatically estimate. |
|`GRANULARITY` |No |It defines the index granularity, indicating that the index is built every 1 data block (mark). |


<span id="7c61f355"></span>
## Query syntax

You can use basic query statements to search data or improve accuracy by setting the settings parameter.

In addition, ByteHouse supports adding `prewhere` statements for pre\-filtering conditions; see [Hybrid search](https://docs.byteplus.com/docs/bytehouse/use-vector-search#d46377f8) for details. It also supports adding `where` statements to filter search results by similarity threshold; see [Distance filtering](https://docs.byteplus.com/docs/bytehouse/use-vector-search#3c59aa9e) for details.

<span id="8c7fc5cd"></span>
### Basic query

```SQL
SELECT *, d
FROM xxx.yyy
ORDER BY L2Distance(vector, [...]) as d limit 3 
settings 
enable_new_ann=1;
```



|Parameter items |Required |Configuration description |
|---|---|---|
|`SELECT *, d` |Yes |It defines the query scope. This example returns all original fields in the table and the vector distance calculation result `d`.<br><br><br>* `d`: This value comes from the calculation result of `L2Distance(vector, [...]) as d` in `ORDER BY`, representing the Euclidean distance between the vector field and the query vector ([...]) **,**  used for sorting and displaying results. |
|`FROM xxx.yyy` |Yes |It defines the database name and table name to query. |
|`ORDER BY L2Distance(vector, [...]) as d limit 3` |Yes |It defines how to sort the query results.<br><br>This example means sorting the results by vector distance `d` in ascending order and selecting the top 3 records, which are the 3 vectors closest in distance.<br><br><br>* `L2Distance(vector, [...])`: defines the two vectors to query, calculating the Euclidean distance (L2 norm) between the vector field and the query vector ([...]).<br><br>* `as d`: renames the vector distance result to d for easier viewing of the results.<br><br>* `limit`: defines the limit on the number of records returned. This example returns the top 3 records with the shortest distance, meaning the 3 most similar vectors. |
|`settings` |yes |Set settings parameters.<br><br><br>* `enable_new_ann`: set to 1 to activate the newly implemented ANN query path.<br><br><br>For the full list of settings parameters supported by ByteHouse configuration, please refer to [Settings parameters](https://docs.byteplus.com/docs/bytehouse/use-vector-search#fc1ac31d). |


<span id="e60e7062"></span>
### Tune queries using the settings parameter

You can tune queries for IVF_FLAT, IVF_PQ, and IVF_PQ_FS indexes using the `nprobe` and `k_factor_rf` parameters to improve query accuracy. For the full list of configurable ByteHouse settings parameters, see [Settings parameters](https://docs.byteplus.com/docs/bytehouse/use-vector-search#fc1ac31d).

<span id="e5672d06"></span>
#### IVF_FLAT and IVF_PQ index tuning

IVF_FLAT and IVF_PQ indexes support setting the `nprobe` parameter. The `nprobe` parameter specifies the number of IVF cluster centers to access during retrieval. The default is 1. A larger value improves accuracy but reduces performance and query speed. Values are powers of 2, such as 32 or 64, within the range [1, std::min(nlist/2, top n in query)].

```SQL
SELECT *, d
FROM xxx.yyy
ORDER BY L2Distance(vector, [...]) as d limit 3 
settings 
enable_new_ann=1, nprobe=256;
```


<span id="f334f56e"></span>
#### IVF_PQ_FS index tuning

IVF_PQ_FS index supports setting `nprobe` and `k_factor_rf` parameters. The `k_factor_rf` parameter controls the candidate set expansion factor during re\-ranking. After the initial retrieval returns `k` results, the candidate set expands by `k_factor_rf` times (that is, `k×32`), and precise distances are recalculated for the expanded set to select the final `k` results.

```SQL
SELECT *, d
FROM xxx.yyy
ORDER BY L2Distance(vector, [...]) as d limit 3 
settings 
enable_new_ann=1, nprobe=256, k_factor_rf=32;
```


<span id="af23c2ba"></span>
# Related reference: tuning parameter configuration

<span id="3c59aa9e"></span>
## Distance filtering

ByteHouse optimized queries with single filter conditions like `where dist < max_score` and `where dist > min_score` to filter search results by similarity threshold and select matching records. Examples are as follows:

```SQL
select id, dist 
from test_ann 
where dist < 0.9 
order by cosineDistance(embedding_column, [query_vector]) as dist
limit 100
```


<span id="fc1ac31d"></span>
## Settings parameters

You can optimize vector search queries using the following settings parameters. Settings parameters configured in SQL statements only apply to the current statement.


|Param |**Description** |Configuration method |**Default value** |**Usage suggestions** |
|---|---|---|---|---|
|`index_granularity` |It represents the index granularity, that is, the number of rows each mark corresponds to in the index. Setting this parameter helps reduce read amplification and improve query performance. |Set in the create table statement. |8192 |It controls the number of rows each mark contains; reducing it lowers read amplification and improves vector filtering accuracy. recommended value is 128. |
|`index_granularity_bytes` |It represents the byte size of the index granularity; when set to 0, adaptive marks are avoided, so marks are generated based only on row count, not data byte size. |Set in the create table statement. |10485760 (approximately 10 MiB) |Disable adaptive mark, fix mark size to reduce mark positioning calculation overhead. Set to 0 recommended. |
|`enable_vector_index_preload` |Toggle for table\-level preload. |Set in the create table statement. |0 |Write acceleration. Vector index of the written part directly goes into cache, eliminating cache loading time. |
|`enable_new_ann` |Whether to use the new ANN execution path. |Set in the query statement. |0 |Set to 1 to activate. |
|`hnsw_ef_s` |It is the search parameter used when searching based on the HNSW index; the larger the value, the higher the accuracy. |Set in the query statement. |10 |For recall above 90, generally set above 128. |
|`nprobe` |Search parameter for Faiss IVF indexes (IVF_FLAT, IVF_PQ, IVF_PQ_FS) that indicates the number of cluster centers used in the search. In theory, a larger nprobe increases accuracy but also raises latency. |Set in the query statement. |0 (default 0 means not set; the default parameter in the index is 1) |For recall above 90, consider setting it to at least one\-fourth of nlist. |
|`k_factor_rf` |Search parameter for Faiss indexes with refine (IVF_PQ_FS). Larger k_factor_rf yields more results for sorting, higher accuracy, and higher latency. |Set in the query statement. |0 (same as above) |When using the refine index with low recall, try increasing the value. Start with setting it to 100 and fine\-tune as needed. |
|`vector_index_build_threads` |The number of build threads per part. |Set in the insert statement. |8 |Controls build threads for a single part. If concurrent import or merge concurrency is high, it is recommended to reduce this value. |


<span id="e7fa6486"></span>
## Index parameters


|Param |Description |Applicable index |Required |Default |
|---|---|---|---|---|
|`DIM` |Defines the dimension information of the vector corresponding to the index, which must match the actual vector dimension. |HNSW、HNSW_SQ、FLAT、IVF_FLAT、IVF_PQ、IVF_PQ_FS |Yes |960 |
|`METRIC` |Defines the metric used when building the index. Supports setting to L2 or COSINE.<br><br>It should be noted that only the distance function corresponding to the metric can execute index\-based query chains. For example, if the metric in the index is L2, subsequent queries must use the L2Distance function to query with the corresponding index. Similarly, if the metric is COSINE, the cosineDistance function must be used for querying. |HNSW、HNSW_SQ、FLAT、IVF_FLAT、IVF_PQ、IVF_PQ_FS |No |L2 |
|`M` |Defines the maximum number of connections (Max Connections) for each node in the HNSW graph. When the M value is large (for example, set to 32), search speed can increase, but memory usage will also grow. When the M value is small (for example, set between 4 and 16), memory usage can reduce, but recall rate will decrease. |HNSW、HNSW_SQ、IVF_PQ、IVF_PQ_FS |Yes |16 |
|`EF_CONSTRUCTION` |Defines the exploration factor during index construction. The larger this value (such as 512), the better the search accuracy, but the construction time is longer. The smaller this value (such as 100), the faster the construction speed, but the index quality may decrease. |HNSW、HNSW_SQ |Yes |200 |
|`SQ` |Defines the floating\-point compression value to reduce memory usage and speed up computation. |HNSW_SQ |is |8bit (representing 8\-digit integer) |
|`GRANULARITY` |Defines the index granularity, meaning the index is built for every 1 data block (mark). |FLAT、IVF_FLAT、IVF_PQ、IVF_PQ_FS |is | |
|`nbit` |Defines the quantization digits for each subvector. Default is 8, usually no need to change. The value is an even number, generally ranging from [1, 16]. |IVF_PQ |No |8 |
|`nlist` |Define the number of clustering centers required for IVF type indexes; the more centers, the slower the construction. If no value is set, the engine estimates it automatically according to the following logic. You can set the nlist parameter during table creation to specify the upper limit of nlist for each part when building the index.<br><br>```Java```<br>```static size_t decideIndexNlist(size_t n)```<br>```{```<br>```    if (n < ONE_MILLION)```<br>```        return std::min(int(n), int(4 * std::floor(std::sqrt(n))));```<br>```    else if (n >= ONE_MILLION && n < ONE_MILLION * 2)```<br>```        return 1024;```<br>```    else if (n >= ONE_MILLION * 2 && n < TEN_MILLION)```<br>```        return 4096;```<br>```    else if (n > TEN_MILLION)```<br>```        return 65536;```<br>```}```<br> |IVF_FLAT、IVF_PQ、IVF_PQ_FS |No |None |
|`refine` |Define the quantization method used in the fine\-tuning stage, configurable as scalar quantization methods such as RFlat, SQ4, SQ6, SQ8, SQfp16, and others. Accuracy ranking is RFlat \> SQfp16 \> SQ8 \> SQ6 \> SQ4, with memory resource usage decreasing accordingly. |IVF_PQ_FS |No |RFlat |


<span id="d0bb9b66"></span>
## System table parameters

ByteHouse provides a dedicated system table named `system.vector_indices` for vector_indices information. You can query this table for metadata related to constructed vectors.

<span id="b843f818"></span>
### Fields


|Parameter name |Description |
|---|---|
|`database` |Database name |
|`table` |Table name |
|`name` |Index name |
|`type` |Index type, supports setting to HNSW or Faiss. |
|`vector_column` |Name of the column for building the index |
|`params` |Index building parameters |
|`total_parts` |Total number of table parts |
|`index_built_parts` |Number of parts with built index |
|`total_rows` |Total number of data rows in the table |
|`estimate_memory_size` |Estimated index memory size |


<span id="4433edeb"></span>
### Example

```SQL
SELECT *
FROM system.vector_indices 
WHERE 
    database = 'xxx'    
    AND table = 'yyy';  
```


<span id="0dcf35e5"></span>
# Related reference: Best practice

You can refer to [Best practice for vector search](https://docs.byteplus.com/docs/bytehouse/best-practice-for-vector-search) to understand the configuration of vector search when using SQL statements to create tables, best practice.
