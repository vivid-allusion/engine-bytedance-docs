---
title: "Perform vector search using SQL"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/perform-vector-search-using-SQL"
---

ByteHouse provides management and approximate query capabilities for vector data, enhancing retrieval performance through support of various popular Approximate Nearest Neighbor (ANN) algorithms, and offers processing capabilities for unstructured data. This article explains how to use SQL statements in ByteHouse to perform vector retrieval using HNSW or Faiss Indices libraries.

<span id="903bad8f"></span>
# Background information

ByteHouse currently supports the popular retrieval algorithm libraries [HNSW (hnswlib)](https://github.com/nmslib/hnswlib) and [Faiss](https://github.com/facebookresearch/faiss), supporting various common indices like HNSW, FLAT, IVF_FLAT, IVF_PQ, and IVF_PQ_FS.

The HNSW algorithm library is a graph\-type index, maintaining M nearest neighbors for each node through a minimal world construction approach. It also maintains a hierarchical graph structure, becoming sparser as it goes upward. The search begins from the top layer, continuing downwards layer by layer upon finding the nearest point, until the bottom layer is reached to identify the k nearest neighbors for the query vector.

Faiss, an open\-source ANN algorithm library by Facebook, includes types of indices such as Inverted File (IVF), Product Quantization (PQ), and Scalar Quantization (SQ), with abilities to combine multiple types of indices. ByteHouse primarily uses Faiss's IVF class indices and supports vector compression methods like PQ and PQ_FS (Fast Scan), to reduce memory usage of indices.

<span id="339e3412"></span>
# Prerequisites


* Please ensure that the ByteHouse you are using complies with version 2.2 or higher. You can log in to the ByteHouse console, click on **Tenant management** at the top, and check the engine version you are using on the **Basic Information** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c9c7749159774447ae90e4fe88549b56~tplv-goo7wpa0wc-image.image) </span>

* Please ensure that you [Enable vector search](https://docs.byteplus.com/docs/bytehouse/vector-retrieval).


<span id="1e6fc5b8"></span>
# Quick start

The ANN algorithm library is accessed via indexes, supporting the addition of definitions by creating or modifying tables. After defining the index, it supports inserting data and querying using the index. This chapter uses the HNSW index type as an example to help you get started quickly with vector retrieval features. For detailed explanations of different indexes, please see [Use HNSW index](https://docs.byteplus.com/docs/bytehouse/perform-vector-search-using-SQL#df67204f) and [Use Faiss Indices index](https://docs.byteplus.com/docs/bytehouse/perform-vector-search-using-SQL#42525594) chapters.

<span id="955daf73"></span>
## Define index

<span id="d78d58cb"></span>
### Method 1: Define when creating a new table

```SQL
CREATE TABLE test_ann
(
    `id` UInt64,
    `label` String,
    `vector` Array(Float32),
    INDEX v1 vector TYPE HNSW('DIM=960, METRIC=COSINE')
)
ENGINE = CnchMergeTree
ORDER BY id
SETTINGS 
index_granularity = 1024, -- Mitigate read amplification issues
index_granularity_bytes = 0 -- Prevent generating adaptive marks 
```


<span id="2efec24b"></span>
### Method 2: Modify existing table

```SQL
ALTER TABLE test_ann ADD INDEX v1 vector TYPE HNSW('DIM=960, METRIC=COSINE') 
```


**Parameter Description**


|Parameter items |Required |Configuration description |
|---|---|---|
|`test_ann` |Yes |Customize your table name. |
|`vector Array(Float32)` |Yes |Define the column data type `vector` as `Array(Float32)`, commonly used to store vector data. |
|`INDEX v1 vector` |Yes |Define an index. This article defines an index named v1 based on the vector fiel`v1 based on the vector` field to accelerate queries on the vector field. |
|`TYPE HNSW('DIM=960, METRIC=COSINE')` |Yes |Define the index type used and configure the relevant internal parameters for that index type.<br><br><br>* Index Types: Current support includes HNSW, FLAT, IVF_FLAT, IVF_PQ, IVF_PD_FS.<br><br>* Internal parameters: Configure internal parameters in a key\-value format, separate multiple parameters with commas, for example: DIM=960, METRIC=COSINE. Among these:<br><br>   * DIM: Defines the dimension information of the index corresponding to the vector, which must match the actual dimensions of the vector.<br><br>   * METRIC: Defines the measure used when building the index. The METRIC parameter is optional, with the default value being L2, but you can also manually configure it to L2 or COSINE. It should be noted that subsequent use of the corresponding metric's distance function is required to execute the query pipeline based on the index. For example, if the metric in the index is L2, subsequent queries must use the `L2Distance` function to access the corresponding index, similarly, when the metric is COSINE, you need to use the `cosineDistance` function to query.<br><br><br>For detailed guidance on using index types, see [Use HNSW index](https://docs.byteplus.com/docs/bytehouse/perform-vector-search-using-SQL#df67204f) and [Use Faiss Indices index](https://docs.byteplus.com/docs/bytehouse/perform-vector-search-using-SQL#42525594) chapters. |
|`ENGINE` |Yes |Specifies the storage engine of the table. Configured as CnchMergeTree. |
|`ORDER BY` |Yes |Specifies the sorting of data in the table. |
|`SETTINGS` |No |* `index_granularity`: Indicates the index granularity, i.e., the number of rows corresponding to each mark in the index. Setting this parameter can alleviate the problem of read amplification and improve query performance.<br><br>* `index_granularity_bytes`: Indicates the number of bytes for index granularity. When set to 0, it avoids generating an adaptive mark, meaning the index marks are generated based solely on the number of rows, not on the bytes of data.<br><br><br>Please refer to the full list of configurable settings for ByteHouse at [Settings parameters](https://docs.byteplus.com/docs/bytehouse/perform-vector-search-using-SQL#ec887126). |


<span id="a4dbe850"></span>
## Insert data

ByteHouse's insert statements are supported as well as streaming import methods like Kafka. For details, refer to [data import](https://docs.byteplus.com/en/docs/bytehouse/docs-data-import-e8caa19b). Examples are as follows:


* Import data through VALUES fieldsdata through VALUES fields.

   ```SQL
   INSERT INTO test_ann VALUES (1, [1.0, 1.0, 1.0]),(2, [2.0, 2.0, 2.0]) 
   ```
   

* Import data using CSV files.

   ```SQL
   INSERT INTO test_ann FORMAT CSV infile '/filename.csv' 
   ```
   


<span id="16a6fddc"></span>
## Query using indexes

This section explains how to query data using indexes, including basic queries and mixed queries with added `prewhere` conditions. Additionally, ByteHouse supports adding `where` conditions to filter search results, selecting records that meet similarity thresholds. For details, refer to [Distance filtering](https://docs.byteplus.com/docs/bytehouse/perform-vector-search-using-SQL#d7c5d74c).

<span id="9b5a52fd"></span>
### Basic query

```SQL
SELECT
    id， 
    label,
    dist 
FROM test_ann 
ORDER BY cosineDistance(vector, [query_vector]) AS dist 
LIMIT 100 
SETTINGS enable_new_ann=1 
```



|Parameter item |Required |Configuration description |
|---|---|---|
|`cosineDistance(vector, [query_vector])` |Yes |Define the vector similarity calculation formula.<br><br><br>* The Distance function must correspond to the metric defined by the index in order to use the index properly, for example, if the metric is defined as cosine in the table creation syntax example, cosine should also be used in the query syntax.<br><br>* `vector` is the defined vector field.<br><br>* `[query_vector]` is the query vector you need to input. |
|`order by ... as dist` |Yes |Rename the calculation result as `dist` and sort in ascending order.<br><br>Currently, only queries with the `order by {metric}Distance limit k` pattern will use the vector index for calculation. |
|`limit` |Yes |Set the number of records returned. |
|`settings` |Yes |`enable_new_ann`: Set to 1 to enable the newly implemented ANN search path.<br><br>Please refer to [Settings parameters](https://docs.byteplus.com/docs/bytehouse/perform-vector-search-using-SQL#ec887126) for the full list of configurable settings supported by ByteHouse. |


<span id="bc7daf65"></span>
### Mixed query

ByteHouse also supports mixed queries with `prewhere`, for example, the following example uses `prewhere id > 1000` to add a pre\-filter condition, processing only records with `id > 1000`.

```SQL
SELECT
    id,
    label,
    dist 
FROM test_ann 
PREWHERE id > 1000
ORDER BY cosineDistance(vector, [query_vector]) AS dist 
LIMIT 100 
SETTINGS enable_new_ann=1 
```


<span id="df67204f"></span>
# Use HNSW index

<span id="232420b4"></span>
## Index building syntax

When using the HNSW Index, you can define parameters `M` and `EF_CONSTRUCTION` to balance performance and accuracy. Generally, the larger the value of `M` and `EF_CONSTRUCTION`, the longer the index building time, the higher the accuracy, and the higher the search latency. Example as follows:

```SQL
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


Description of configurable index parameters for HNSW Index. For a complete table of index parameters and usage recommendations, please refer to [Index parameters](https://docs.byteplus.com/docs/bytehouse/perform-vector-search-using-SQL#91fa5d36).


|Parameter item |Mandatory |Configuration explanation |
|---|---|---|
|`M` |No |Defines the maximum number of connections for each node in the HNSW graph, with a default value of 16. When the M value is high (such as 32), it can increase search speed but will also increase memory usage. When the M value is low (such as 4\-16), it can reduce memory usage, but will decrease recall rate. |
|`EF_CONSTRUCTION` |No |Defines the exploration factor for index construction, with a default value of 200. When the value is high (such as 512), the search precision is better, but the construction time is longer. When the value is low (such as 100), construction speed is faster, but the quality of the index might decrease. |


<span id="56bd6890"></span>
## Query syntax

You can retrieve data using query statements.

In addition, ByteHouse also supports adding `prewhere` statements to add pre\-filtering conditions, see [Mixed query](https://docs.byteplus.com/docs/bytehouse/perform-vector-search-using-SQL#bc7daf65); it also supports adding `where` statements for filtering search results, selecting records that meet the similarity threshold, see [Distance filtering](https://docs.byteplus.com/docs/bytehouse/perform-vector-search-using-SQL#d7c5d74c).

```SQL
SELECT
    id， 
    dist 
FROM test_ann 
ORDER BY cosineDistance(vector, [query_vector]) AS dist 
LIMIT 100 
SETTINGS enable_new_ann=1, hnsw_ef_s=200 
```


**Parameter description**


|Parameter item |Required |Configuration description |
|---|---|---|
|`settings` |Yes |`hnsw_ef_s`: Set this value to control accuracy and latency. The larger the parameter value, the higher the accuracy and the longer the latency. Beyond the `EF_CONSTRUCTION` parameter, theoretically, there is no further increase in accuracy.<br><br>For a complete list of all configurable settings parameters supported by ByteHouse, refer to [Settings parameters](https://docs.byteplus.com/docs/bytehouse/perform-vector-search-using-SQL#ec887126). |


<span id="42525594"></span>
# Use Faiss Indices index

<span id="3c25556c"></span>
## Precautions

Faiss differs from HNSW in that it trains during index building, which consumes significant CPU resources. When using, please set the following parameters:


* Set the index cache size based on memory size using the `vector_index_cache_size` parameter, default 200GB. This parameter is implemented based on the Least Recently Used (LRU) strategy.

* During testing, pay attention to the CPU usage. If the CPU usage is too high, you can set the parameter value for `vector_index_build_threads`, which defaults to 8, to limit the concurrency of training indexes.


<span id="851a23ab"></span>
## Index building syntax

Faiss provides four common types of indexes and offers corresponding tuning parameters for adjusting accuracy.

<span id="dc078248"></span>
### FLAT index

FLAT is the simplest index type in Faiss, based on brute\-force search. It stores all vectors in memory, computes the distances between the query vector and all vectors during queries, and returns the nearest neighbors. FLAT is simple to implement, requires no training, offers high accuracy, but has a time complexity of O(n) and is not suitable for very large databases . It is recommended for situations with smaller data volumes, low vector dimensions, and low speed requirements but needs precise results .

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


The index parameters that can be set for FLAT index are as follows. For a complete index parameter list and usage recommendations, please refer to [Index parameters](https://docs.byteplus.com/docs/bytehouse/perform-vector-search-using-SQL#91fa5d36).


|Parameter Item |Required |Configuration Description |
|---|---|---|
|`dim` |Yes |Defines the dimension of the corresponding vector. |
|`metric` |No |Defines the metric used when building the index. The METRIC parameter can be unspecified; by default, it is L2, or you may manually configure it to L2 or COSINE. |
|`GRANULARITY` |No |Defines the index granularity, indicating that an index is built for every one data block (mark). |


<span id="2a47d08a"></span>
### IVF_FLAT index

The IVF_FLAT index combines the advantages of Inverted File (IVF) and FLAT indexes, significantly enhancing query efficiency while maintaining high retrieval accuracy, suitable for medium to large\-scale low\-dimensional vector retrieval tasks (such as 4\-128 dimensions).

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


Configuration parameters for the IVF_FLAT index are as follows. For a complete index parameter table and usage recommendations, please see [Index parameters](https://docs.byteplus.com/docs/bytehouse/perform-vector-search-using-SQL#91fa5d36).


|Parameter Item |Required |Configuration Description |
|---|---|---|
|`dim` |Yes |Defines the dimension of the corresponding vector. |
|`metric` |No |Defines the metric to use when building the index. The METRIC parameter can be unspecified by default, and you can manually configure it to L2 or COSINE. |
|`nlist` |No |Defining the quantity of cluster centers required for an IVF type index impacts build speed: more centers mean slower construction. If not set, the engine will automatically calculate, following this logic: when creating a table, you can use the `nlist` parameter to specify the `Cap` for each part during index building.<br><br>```Java```<br>```static size_t decideIndexNlist(size_t n)```<br>```{```<br>```    if (n < ONE_MILLION)```<br>```        return std::min(int(n), int(4 * std::floor(std::sqrt(n))));```<br>```    else if (n >= ONE_MILLION && n < ONE_MILLION * 2)```<br>```        return 1024;```<br>```    else if (n >= ONE_MILLION * 2 && n < TEN_MILLION)```<br>```        return 4096;```<br>```    else if (n > TEN_MILLION)```<br>```        return 65536;```<br>```}```<br> |
|`GRANULARITY` |No |Defines the index granularity, indicating an index is built for every 1 data block (mark). |


<span id="b7845315"></span>
### IVF_PQ index

The IVF_PQ index is an efficient vector compression and indexing method that combines the technologies of Inverted File (IVF) and Product Quantization (PQ). It dramatically reduces memory usage while maintaining high retrieval accuracy, suitable for ultra\-large datasets (100 million vectors and above).

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


Configuration parameters for the IVF_PQ index are as follows. For a complete index parameter table and usage recommendations, please see [Index parameters](https://docs.byteplus.com/docs/bytehouse/perform-vector-search-using-SQL#91fa5d36).


|Parameters |Required |Configuration Description |
|---|---|---|
|`dim` |Yes |Defines the metric used for indexing. |
|`metric` |No |Defines the method used for indexing. Param METRIC can be unspecified, Default is L2; you can also manually configure it to L2 or COSINE. |
|`m` |Yes |Defines the quantity of sub\-vectors for product quantization. Common values are either 64 or 32, the value should be a power of 2, ranging from [1, std::min(dim, 64)]. |
|`nbit` |No |Defines the quantization bit number for each sub\-vector. The default value is 8, usually no modification needed, value must be even, generally ranging from [1, 16]. |
|`nlist` |Yes |Defines the number of clustering centers required for the IVF type index. The more centers, the slower the build; if not set, the engine will automatically estimate. |
|`GRANULARITY` |No |Define the granularity of the index, indicating that an index is built for every 1 data block (mark). |


<span id="fcdca1bc"></span>
### IVF_PQ_FS index

The IVF_PQ_FS index is an enhanced version of IVF_PQ, adding Fast Scan and Refine features, which maintain compression benefits while improving retrieval accuracy, suitable for large\-scale vector data requiring high precision.

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


IVF_PQ_FS index configuration guide: Below are descriptions for the configurable index parameters. For a complete list of index parameters and usage recommendations, please see [Index parameters](https://docs.byteplus.com/docs/bytehouse/perform-vector-search-using-SQL#91fa5d36).


|Parameter items |Required |Configuration description |
|---|---|---|
|`dim` |Yes |Define the dimension of the corresponding vector. |
|`metric` |No |Define the metric used when building the index. The PARAM can be omitted by default, set to L2, or manually configured to L2 or COSINE. |
|`m` |Yes |Defines the number of subvectors for product quantization. Common values are 64 or 32, within a value range of powers of 2, ranging from [1, std::min(dim, 64)]. |
|`refine` |No |Defines the quantization method used in the reordering phase, using RFlat by default for the highest accuracy, or scalar quantization methods such as SQ4, SQ6, SQ8, SQfp16. Accuracy ranks as RFlat\>SQfp16\>SQ8\>SQ6\>SQ4, with memory resources used decreasing accordingly. Here is an example using SQ8:<br><br>```SQL```<br>```CREATE TABLE tab_ivf_pq_fs_sq8```<br>```(```<br>```    id Int32,```<br>```    vector Array(Float32),```<br>```    INDEX faiss_index vector TYPE IVF_PQ_FS('dim=4','m=2', 'refine=SQ8') GRANULARITY 1```<br>```)```<br>```ENGINE = MergeTree```<br>```ORDER BY id```<br>```SETTINGS index_granularity = 128```<br> |
|`nlist` |No |Define the number of clustering centers required for IVF type indexing. The more centers, the slower the construction. If not set, the engine will automatically estimate. |
|`GRANULARITY` |No |Define the index granularity, indicating that the index is built once per data block (mark). |


<span id="1e3e99fa"></span>
## Query syntax

You can use basic query statements to retrieve data or enhance accuracy by configuring the settings parameters.

In addition, ByteHouse also supports adding `prewhere` statements for pre\-filtering conditions. For more details, please see [Mixed query](https://docs.byteplus.com/docs/bytehouse/perform-vector-search-using-SQL#bc7daf65); It also supports adding `where` statements to filter search results and select records based on similarity thresholds. For more details, please see [Distance filtering](https://docs.byteplus.com/docs/bytehouse/perform-vector-search-using-SQL#d7c5d74c).

<span id="fb25759c"></span>
### Basic query

```SQL
SELECT *, d
FROM xxx.yyy
ORDER BY L2Distance(vector, [...]) as d limit 3 
settings 
enable_new_ann=1; 
```



|Parameter item |Required |Configuration description |
|---|---|---|
|`SELECT *, d` |Yes |Defines the scope of the query. This example indicates that all the original fields in the table will be returned, along with the vector distance calculation result `d`.<br><br><br>* `D`: This value is obtained from the calculation of L2Distance(vector, [...]) as d in ORDER BY, r`L2Distance(vector, [...]) as d in ORDER BY`, representing the Euclidean distance between the vector field and the query vector ([...]), **used for sorting and result display**. |
|`FROM xxx.yyy` |Yes |Defines the database name and table name that need to be queried. |
|`ORDER BY L2Distance(vector, [...]) as d limit 3` |Yes |Defines the sorting method for the query results.<br><br>This example shows the calculation results sorted in ascending order by vector distance and retrieves the first 3 records, i.e., the 3 vectors closest in distance.<br><br><br>* `L2Distance(vector, [...])`: Defines the two vectors to be queried and calculates the Euclidean distance (L2 norm) between the vector field and the query vector ([...]).<br><br>* `as d`: Renames the vector distance result to d for easy viewing of the results.<br><br>* `limit`: Defines the cap on the number of records returned. This example returns the records of the 3 closest vectors in distance, i.e., the 3 most similar vectors. |
|`settings` |Yes |Set the settings parameter.<br><br><br>* `enable_new_ann`: Should be set to 1 to activate the new ANN query path implementation.<br><br><br>For a complete list of configurable settings in ByteHouse, see [Settings parameters](https://docs.byteplus.com/docs/bytehouse/perform-vector-search-using-SQL#ec887126). |


<span id="e0e3b148"></span>
### Optimize queries using settings parameters

You can use the nprobe and k_factor_rf parameters to fine\-tune your queries for IVF_FLAT, IVF_PQ, and IVF_PQ_FS indexes to enhance query accuracy. For a comprehensive list of supported full settings parameters in ByteHouse, please see [Settings parameters](https://docs.byteplus.com/docs/bytehouse/perform-vector-search-using-SQL#ec887126).

<span id="924aa202"></span>
#### Optimization of IVF_FLAT and IVF_PQ indexes

IVF_FLAT and IVF_PQ indexes support setting the `nprobe` parameter. The `nprobe` parameter specifies the number of IVF cluster centers to visit during retrieval. The default value is 1. A larger value improves accuracy but reduces performance and query speed. The value is a power of 2, such as 32 or 64, within the range [1, std::min(nlist/2, top n in the query)].

```SQL
SELECT *, d
FROM xxx.yyy
ORDER BY L2Distance(vector, [...]) as d limit 3 
settings 
enable_new_ann=1, nprobe=256;
```


<span id="f1b94675"></span>
#### IVF_PQ_FS index tuning

The IVF_PQ_FS index supports setting the `nprobe` and `k_factor_rf` parameters. The `k_factor_rf` parameter controls the expansion factor of the candidate set during reranking. After the initial retrieval returns `k` results, the candidate set expands by `k_factor_rf` times (that is, `k×32`). The expanded candidate set is then recalculated for precise distances to select the final `k` results.

```SQL
SELECT *, d
FROM xxx.yyy
ORDER BY L2Distance(vector, [...]) as d limit 3 
SETTINGS
enable_new_ann=1, nprobe=256, k_factor_rf=32;
```


<span id="cf0cf476"></span>
# Reference: Tune parameters

<span id="d7c5d74c"></span>
## Distance filtering

ByteHouse optimizes single filter condition queries such as `where dist < max_score` and `where dist > min_score` to filter search results by similarity threshold and select matching records. Grammar examples are as follows:

```SQL
SELECT id, dist 
FROM test_ann 
WHERE dist < 0.9 
ORDER BY cosineDistance(embedding_column, [query_vector]) AS dist
LIMIT 100 
```


<span id="ec887126"></span>
## Settings parameters

You can use the following settings parameters to optimize vector search queries. If configured through the user.xml file, this parameter applies globally; if configured through an SQL statement, this parameter only applies to the current statement.


|Parameter |**Description** |Configuration method |**Default** |**Usage recommendation** |
|---|---|---|---|---|
|`index_granularity` |Indicates the granularity of the index, which is the number of rows each mark in the index corresponds to. Setting this parameter can alleviate read amplification issues and improve query performance. |Set in the table creation statement. |8192 |Control the number of rows per Mark. Reducing this value can decrease read amplification and improve vector filtering accuracy. It is recommended to set to `128`. |
|`index_granularity_bytes` |Indicates the byte granularity of the index. When set to 0, it avoids generating adaptive marks, so index mark generation is based solely on the number of rows and not on the number of bytes of data. |Set in the create table statement. |10485760 (approximately 10 MiB) |Disable adaptive marks to fix the mark size and reduce the computational overhead of mark positioning. It is recommended to set to `0`. |
|`enable_vector_index_preload` |Toggle for table level preload. |Set in the create table statement. |0 |Write acceleration. The vector index of the written part directly enters the cache, eliminating cache loading time. |
|`enable_new_ann` |Use the new ANN execution path. |Set in the query statement. |0 |Set to 1 to enable. |
|`hnsw_ef_s` |When searching based on the HNSW index, the search parameter used is higher in value for greater accuracy. |Set in the query statement. |10 |For scenarios with a recall above 90, it is generally necessary to set it to 128 or higher. |
|`nprobe` |The search parameters for using Faiss IVF index (IVF_FLAT, IVF_PQ, IVF_PQ_FS index), indicate the number of cluster centers used for the search. Theoretically, the larger the nprobe, the greater the accuracy and the higher the latency. |Set in the query statement. |0 (default is 0 which means it is not set, the default parameter used in the index is 1) |For scenarios with a recall above 90, consider setting it to more than 1/4 of nlist. |
|`k_factor_rf` |When using the Faiss index with refine (IVF_PQ_FS index), the higher the k_factor_rf, the more results are used for sorting, the higher the accuracy and the higher the latency. |Set in the query statement. |0 (as above) |If using an index that is refined, and recall is low, try increasing it. You could start by setting it to 100 and make fine adjustments as needed. |
|`vector_index_build_threads` |Number of build threads for each part. |Set in the insert statement. |8 |Control the build threads for each part. If concurrent imports or merge concurrency is high, it is advised to reduce it. |


<span id="91fa5d36"></span>
## Index parameters


|Parameter |Description |Applicable Index |Required Field |Default Value |
|---|---|---|---|---|
|`DIM` |Defines the dimension information for the index vector, which must match the actual dimensions of the vector. |HNSW、FLAT、IVF_FLAT、IVF_PQ、IVF_PQ_FS |Yes |960 |
|`METRIC` |Defines the metric used when building the index. Supports setting to L2 or COSINE.<br><br>It is worth noting that only by using the distance function for the corresponding metric can index\-based query chains be executed. For example, if the metric in the index is L2, subsequent queries need to use the L2Distance function to exploit the corresponding index; similarly, when the metric is COSINE, the cosineDistance function is required for querying. |HNSW、FLAT、IVF_FLAT、IVF_PQ、IVF_PQ_FS |No |L2 |
|`M` |Defines the maximum number of connections per node in the HNSW graph (Max Connections). When the value of M is large (such as set to 32), it can increase the search speed, but will increase memory usage. When the value of M is small (such as set to 4\-16), it can reduce memory usage, but will lower the recall rate . |HNSW、IVF_PQ、IVF_PQ_FS |is |16 |
|`EF_CONSTRUCTION` |Defines the exploration factor for index construction. When the value is high (such as 512), the search accuracy is better, but the construction time is longer. When the value is low (such as 100), the construction speed is faster, but the index quality may decrease. |HNSW |is |200 |
|`GRANULARITY` |Defines index granularity, indicating that an index is built for every 1 data block (mark). |FLAT、IVF_FLAT、IVF_PQ、IVF_PQ_FS |Yes | |
|`nbit` |Defines the quantization bits per sub\-vector. The default is 8, usually no modification is needed. The value must be even, typically within the range [1, 16]. |IVF_PQ |No |8 |
|`nlist` |Define the number of clustering centers required for the IVF type index; the more clustering centers, the slower the build. If no value is set, the engine will automatically estimate it. During table creation, you can use the nlist parameter to specify the upper limit of nlist for each part when building the index.<br><br>```Java```<br>```static size_t decideIndexNlist(size_t n)```<br>```{```<br>```    if (n < ONE_MILLION)```<br>```        return std::min(int(n), int(4 * std::floor(std::sqrt(n))));```<br>```    else if (n >= ONE_MILLION && n < ONE_MILLION * 2)```<br>```        return 1024;```<br>```    else if (n >= ONE_MILLION * 2 && n < TEN_MILLION)```<br>```        return 4096;```<br>```    else if (n > TEN_MILLION)```<br>```        return 65536;```<br>```}```<br> |IVF_FLAT、IVF_PQ、IVF_PQ_FS |No |None |
|`refine` |Define the quantization method used in the refinement stage, configurable to scalar quantization methods like RFlat, SQ4, SQ6, SQ8, SQfp16, etc. The precision ranking is RFlat \> SQfp16 \> SQ8 \> SQ6 \> SQ4, with memory resource usage decreasing accordingly. |IVF_PQ_FS |No |RFlat |
