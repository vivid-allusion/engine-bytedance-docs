---
title: "Search feature"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/Search_feature"
---

This topic introduces the search feature of Document Database for MongoDB.

<span id="yQTOvlgu"></span>
## Feature introduction

When building search capabilities in applications, traditional solutions often require introducing independent search engines like Elasticsearch, which can lead to increased architectural complexity, fragile data synchronization links, and higher operation and maintenance costs. The search feature of Document Database for MongoDB achieves native integration of search capabilities with the database by deploying dedicated search nodes (`mongot`) within the database instance. You can use MongoDB's standard aggregation query syntax to complete search tasks, without needing to maintain an external search system.

The search feature provides the following two search methods.


|**Search type** |**Functional positioning** |**Corresponding aggregation stage** |**Main features** |**Application scenarios** |
|---|---|---|---|---|
|Full\-text search |Keyword\-based text matching<br><br> |`$search` |Accelerate keyword queries on text fields by creating Search indexes, supporting tokenization and relevance ranking. |Product review retrieval, document content search, system log queries<br><br> |
|Vector search |Similarity search based on data semantics or intrinsic meaning |`$vectorSearch`<br><br> |Searches for vectors similar to the query vector in a multi\-dimensional space, where closer distances indicate more similar semantics; can be used with embedding and generative models |Semantic retrieval, image similarity search, recommendation systems, RAG applications, AI Agents |


<span id="xELD56LV"></span>
## System architecture and working principle

Regardless of the search type used, it is underpinned by a unified search architecture. Document Database for MongoDB supports two architectures: replica set and sharding cluster. Building upon this architecture, the search feature expands search capabilities by adding independent `mongot` nodes. `mongot` is an indexing and query execution engine built on Apache Lucene, specifically designed to support MongoDB Search and Vector Search.


* **Architecture diagram**<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_81170dbbe903845a9b7d929cf933f0c6.jpeg) </span>**Core components and responsibilities**

   
   |**Core components** |**Responsibilities** |
   |---|---|
   |mongod node |Responsible for business data storage and regular read/write operations. Forwards retrieval requests to the mongot node for execution when `$search`, `$searchMeta`, or `$vectorSearch` queries are received. |
   |mongot node |Independent search compute resources, hosting all Search indexes, dedicated to processing retrieval requests. Each `mongot` process has its own persistent storage, not shared with databases or other search nodes. `mongot `is responsible for managing index definitions, continuously retrieving data from the database to update indexes in real time, and processing search queries. |
   

* **Data synchronization mechanism**

   `mongot` asynchronously subscribes to data changes from `mongod` via Change Stream (MongoDB's change stream mechanism), updating indexes in real\-time to ensure eventual consistency. Retrieval workloads run on independent `mongot` nodes and do not impact the transaction processing performance of the core database.

* **Request processing path**

   You initiate retrieval aggregation queries through mongosh or other official MongoDB drivers. After `mongos` (sharding cluster) or `mongod` (replica set) receives the query, it forwards the search stage to the mongot node for execution. After `mongot` completes the search, it returns the IDs and relevance scores of the matching documents to the proxy node that received the request. This node then completes reading the full documents, merges them with the results of regular queries, and finally returns a unified result set to you. The entire routing and execution process is completely transparent to the application. You only need to write retrieval statements using standard aggregation syntax, without needing to concern yourself with internal details such as how requests are distributed or how data is merged, nor do you need to maintain additional connections or APIs for the retrieval feature.


<span id="3WcxI9Y8"></span>
## Limits

Before using the search feature, note the following constraints.


|**Limits** |**Description** |
|---|---|
|Version requirements |MongoDB 8.3 and later. |
|Instance type |Replica set instance or sharding cluster instance |
|Vector field type |Vector fields must be numeric arrays of `int32`, `int64`, or `double` data types. |
|Index isolation |`mongot` component is tightly coupled with a single replica set and cannot be shared across multiple databases or replica sets. |
|Sharding cluster |Each shard maintains an independent group of `mongot` nodes, which are not shared between shards. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For sharding cluster instances, if a collection with an existing Search index is sharded, temporary incomplete search results may occur during the sharded index building. When adding new shards to a sharded collection with an existing Search index, search queries may return incomplete results until the new shard completes initial synchronization.</div>


<span id="rzsuMPMO"></span>
## Usage process

The search feature relies on Search indexes, so you must create the indexes beforehand. The following outlines the complete steps for index creation and retrieval execution, categorized by task type.

<span id="EckxD9E3"></span>
### Create vector index

Vector indexes are used to support semantic similarity search. We recommend searching after confirming the index status changes to `READY`.

Before using the vector search feature, you need to determine how vectors are generated:


* Auto: When creating an index, specify the text fields and models for embedding. MongoDB automatically generates, stores, and updates vectors, and automatically generates vectors for query text when querying. You do not need to write vector generation code or maintain synchronization between vectors and source data. For specific steps, refer to [Creating auto-embedding vector index](https://docs.byteplus.com/en/docs/mongodb/create-auto-embedding-vector-index?lang=en).

* Manual: Manually call an embedding model to generate vectors, which are then written alongside the original data. When querying, you generate the query vectors yourself.


This section uses the manual method as an example to introduce the complete workflow from vector preparation to search.


1. Prepare vector data

   Your business code must import the LLM Embedding model to convert the data to be retrieved into a vector array for storage. Vector dimensions must not exceed 8192 and must be consistent with `numDimensions` in subsequent index definitions.

2. Create index

   Use the `createSearchIndexes()` method to create vector indexes, with the core definition structure as follows.

   ```JSON
   {
     "fields": [{
       "type": "vector",
       "path": "<向量字段路径>",
       "numDimensions": <维度数>,
       "similarity": "euclidean | cosine | dotProduct",
       "quantization": "none | scalar | binary"
     }]
   }
   ```
   

   **Parameter description**

   
   |**Parameter** |**Required** |**Description** |
   |---|---|---|
   |`path` |Yes |Path of the vector field For nested fields, use dot notation to specify the path of embedded fields, e.g. `info.vector`. |
   |`numDimensions` |Yes |Number of vector dimensions, with a value range of 1 to 8192.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The value must exactly match the vector data dimension stored in mongod.</div><br> |
   |`similarity`<br><br> |Yes |Similarity calculation method. The value range is as follows:<br><br><br>* `dotProduct` (default): Dot product, which measures similarity based on the angle and magnitude between vectors.<br><br>* `euclidean`: Euclidean distance, which measures the distance between vector endpoints and can be used to measure similarity across different dimensions.<br><br>* `cosine`: Cosine similarity, which measures similarity based on the angle between vectors and can be used to measure similarity unaffected by magnitude scaling. |
   |`quantization` |No |Quantization method, which reduces the precision of vector data to decrease the storage and memory footprint of the index. Options:<br><br><br>* `none`: No quantization, which ensures no loss of vector data integrity.<br><br>* `scalar`: Scalar quantization, which independently quantizes each dimension of the vector, offers higher precision, and is the recommended option for most scenarios.<br><br>* `binary`: Binary quantization, which binarizes the numerical information of the vector. If your business requires high search speed and low cost, you can choose this method.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When using binary quantization, <code>similarity</code> must be <code>euclidean</code>, and <code>numDimensions</code> must be a multiple of 8.</div><br> |
   

3. Search

   Use the `$vectorSearch` stage in an aggregation pipeline.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Vector search supports two search modes: Approximate Nearest Neighbor (ANN) and Exact Nearest Neighbor (ENN). ANN search is fast and suitable for large datasets, while ENN search is highly accurate but involves high computational overhead. You can control the search mode using the <code>exact</code> parameter.   </div>
   

   ```Bash
   {
     "$vectorSearch": {
       "path": "<向量字段路径>",
       "queryVector": [<数字数组>],
       "numCandidates": <候选数量>,
       "limit": <返回数量>,
       "filter": { <预过滤条件> },
       "index": "<索引名称>"
     }
   }
   ```
   

   **Parameter description**

   
   |**Parameter** |**Required** |**Description** |
   |---|---|---|
   |`path` |Yes |Vector field path, which must match the index definition. |
   |`queryVector` |Yes |Query vector array. Its dimensions must match `numDimensions`. |
   |`numCandidates` |Yes |The number of candidates for ANN search. The recommended value is ≥ `limit` × 20 to improve recall. |
   |`limit` |Yes |Number of returned documents. |
   |`filter` |No |Pre\-filtering conditions, supporting MQL expressions. |
   |`index` |No |Index name, defaults to `\"default\"`. |
   |`exact` |No |Control search mode: `false` (default, ANN approximate search) or `true` (ENN exact search). |
   

   You can also achieve this using the `vectorSearch` operator of the `$search` stage.


<span id="KfFaf8H4"></span>
### Create full\-text index

Full\-text indexes are used for keyword retrieval on content in text fields stored within a collection.


1. Create index

   Use the `createSearchIndexes()` method to create a Search index. The following example creates an index named `full_text_index` and allows MongoDB to automatically index all fields in the collection using `mappings.dynamic: true`.

   ```JSON
   // Create a Search index named 'full_text_index' on the collection
   db.<集合>.createSearchIndex({
     name: "full_text_index",
     definition: {
       "mappings": {
         "dynamic": true      // Automatically index all fields in the collection, making any field retrievable by $search
       }
     }
   });
   ```
   

   **Parameter description**

   
   |**Parameter** |**Required** |**Description** |
   |---|---|---|
   |`name` |Yes |Index name, used to specify when executing `$search`. |
   |`definition.mappings.dynamic` |No |Automatically index all fields. `true` indicates automatically indexing all indexable fields without needing to declare each one in `fields`. Defaults to `false`. |
   

2. Search

   Use the text operator of the `$search` stage in an aggregation pipeline.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The <code>$search</code> stage must be the first stage in its aggregation pipeline.   </div>
   

   ```JSON
   {
     "$search": {
       "index": "full_text_index",
       "text": {
         "query": "<搜索字符串>",
         "path": "<字段名>",
         "fuzzy": {
           "maxEdits": 1 | 2,
           "prefixLength": <字符数>,
           "maxExpansions": <数量>
         },
         "matchCriteria": "any" | "all"
       }
     }
   }
   {
     "$search": {
       "index": "full_text_index",
       "text": {
         "query": "<搜索字符串>",
         "path": "<字段名>",
         "fuzzy": {
           "maxEdits": 1 | 2,
           "prefixLength": <字符数>,
           "maxExpansions": <数量>
         },
         "matchCriteria": "any" | "all"
       }
     }
   }
   ```
   

   **Parameter description**

   
   |**Parameter** |**Required** |**Description** |
   |---|---|---|
   |`index` |No |The name of the Search index to use, defaults to `"default"`. |
   |`text.query` |Yes |Text string to search Supports multiple keywords. |
   |`text.path` |Yes |The field path to search, supporting arrays to specify multiple fields. |
   |`text.fuzzy` |No |Fuzzy matching configuration. `maxEdits ` is the maximum edit distance (default 2), `prefixLength ` is the prefix exact match length (default 0), and `maxExpansions ` is the maximum number of variations (default 50). |
   |`text.matchCriteria` |No<br><br> |Match condition: `\"any\"` (any term matches) or `\"all\"` (all terms match), default `\"any\"`. |
   


<span id="GB5gYuSd"></span>
### Example

The following JSON code snippet demonstrates the complete process from connecting to a database and creating a vector index to executing a vector search (taking the Node.js driver as an example). You can replace the placeholders in the example (such as `<connection string>`) with actual values.

```Bash
[
  {
    "//": "步骤1: 连接数据库并获取集合",
    "connect": {
      "driver": "Node.js (mongodb)",
      "uri": "<您的MongoDB连接字符串>",
      "database": "<数据库名>",
      "collection": "<集合名>"
    }
  },
  {
    "//": "步骤2: 创建向量索引（如果尚未创建）",
    "createSearchIndex": {
      "name": "vector_index_example",
      "definition": {
        "fields": [
          {
            "type": "vector",
            "path": "plot_embedding",
            "numDimensions": 384,
            "similarity": "cosine"
          }
        ]
      }
    }
  },
  {
    "//": "步骤3: 执行向量搜索",
    "aggregate": {
      "pipeline": [
        {
          "$vectorSearch": {
            "index": "vector_index_example",
            "path": "plot_embedding",
            "queryVector": [0.1, -0.2, 0.3 /* ... 请替换为您的384维向量 */],
            "numCandidates": 100,
            "limit": 5
          }
        },
        {
          "$project": {
            "_id": 0,
            "title": 1,
            "plot": 1
          }
        }
      ]
    }
  }
]
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Index creation is an asynchronous operation and takes some time to complete. It is recommended to search only after confirming the index status becomes <strong>Running</strong>.</div>


<span id="hIsYGJ7j"></span>
## Relevant APIs


|**API** |**Description** |
|---|---|
|[CreateDBInstance](https://docs.byteplus.com/en/docs/mongodb/createdbinstance) |Call the CreateDBInstance API to create a MongoDB instance. |
|[DescribeNodeSpecs](https://docs.byteplus.com/en/docs/mongodb/describenodespecs) |Call the DescribeNodeSpecs API to query the list of node specifications supported by MongoDB. |
|[DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) |Call the DescribeDBInstances API to query the basic information of the MongoDB instance. |
|[DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/mongodb/describedbinstancedetail) |Call the DescribeDBInstanceDetail API to query the detailed information of the target MongoDB instance. |
