---
title: "create"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/collection_create"
---

<span id="223d9ec2"></span>
# Overview

The `/api/knowledge/collection/create` endpoint is used to create a new knowledge base. After successful creation, data can be imported.

<span id="e589343b"></span>
# **Prerequisites**

After you complete account registration, identity verification, and AK/SK key acquisition, and acquire a signature as described on the 'Signature Authentication Method' page, you can call the API endpoint to create a knowledge base.

<span id="1a6138e1"></span>
# **Request endpoint**


|**URI** |/api/knowledge/collection/create |Uniform resource identifier |
|---|---|---|
|**Request method** |POST |The operation type that the client requests from the vector database server. |
|**Request header** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="504a7df6"></span>
# **Request parameters (pro version)** 


|**Parameter** |**Sub\-parameter** |**Type** |**Required** |**Default value** |**Parameter description** |
|---|---|---|---|---|---|
|name |\-\- |string |Yes |\-\- |**Knowledge base name**<br><br><br>* Can contain only English letters, numbers, and underscores (_). It must start with an English letter and cannot be empty<br><br>* Length requirement: [1\-64]<br><br>* Knowledge base names must not be duplicated |
|project |\-\- |string |No |default |**The project to which the knowledge base belongs**<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If this field is not specified, the knowledge base will be created under the default project.</div><br><br><br><div data-tips="true" data-tips-type="warning">To create a knowledge base under a specified project, this field must be configured correctly.</div><br> |
|description |\-\- |string |No |"" |**Description of the knowledge base**<br><br><br>* Length requirement: [1, 65535] |
|version |\-\- |int |No |4 |2: standard version<br><br>4: pro version<br><br>For the current version, this value is 4 |
|data_type | |string |No |unstructured_data |**Data type in the knowledge base**<br><br><br>* unstructured_data: multi\-modal data (also supports uploading structured documents, such as pdf, doc, csv, xlsx, png, and more)<br><br>* structured_data: structured data (only supports uploading structured documents, such as csv, xlsx, jsonl) |
|**preprocessing** | |object |No | |**Unstructured document processing strategy**<br><br>Effective when data_type is "unstructured_data"; not applicable when it is "structured_data". |
| |chunking_strategy |string |No |\-\- |**Document chunking strategy**, enumeration values: ["custom_balance"]<br><br><br>* "custom_balance" is the latest default document processing strategy provided by the knowledge base system. This strategy:<br><br>   1. This strategy enhances parsing and understanding for complex documents like PDF and DOCX, with significant improvements in analyzing layout and semantic structures. It optimizes the processing of image content and its context, supports mixed arrangements of images and text to improve contextual consistency, and provides advantages in parsing long tables. Combined with the VikingDB semantic and keyword fusion retrieval algorithm, it improves multimodal content retrieval, increases recall of relevant information, and improves the signal\-to\-noise ratio of the slicing algorithm, resulting in less irrelevant information and reduced semantic loss.<br><br>   2. After selecting this strategy, the effective document processing strategy sub\-parameters include:<br><br>   * "chunk_length" (effective only when "chunking_identifier" is empty)<br><br>   * "merge_small_chunks" (effective only when "chunking_identifier" is empty)<br><br>   * "multi_mode" (effective only when "chunking_identifier" is empty)<br><br>* Please note that the original "default" strategy is currently only used for compatibility with existing knowledge bases and is no longer maintained. **It is recommended to use "custom_balance" for new knowledge bases** |
| |chunk_length |int |No |500 |**Maximum length of document type slices**<br><br>For value range, see [Embedding model and index algorithm comparison table](https://docs.byteplus.com/docs/209/collection_create#3d008a9c) |
| |merge_small_chunks |bool |No |true |**Whether to merge short slices**<br><br>The merged text chunk will not exceed the configured maximum slice length. |
| |multi_modal |\-\- |No |\-\- |**Image understanding strategy**<br><br>Enumeration values:<br><br><br>* "image_ocr": image OCR<br><br><br>Parameter passing example:<br><br><br>* When "multi_modal": ["image_ocr"], image OCR is enabled. If no value is passed, image OCR is not enabled. If not enabled, images will not be processed.<br><br><br>Knowledge bases created using the old parameter name "multi_mode" will retain the original naming. However, it is not recommended to continue using this parameter name for new knowledge bases. |
|table_config |\-\- |object |No |\-\- |**Structured knowledge base table field configuration**<br><br>Effective when data_type == "structured_data"<br><br>```JSON```<br>```{```<br>```  "table_type": "row","col",```<br>```  // row indicates parsing starts from the row, col indicates parsing starts from the column,```<br>```  "table_pos": "int",```<br>```  // The field is located in which row or column,```<br>```  "start_pos": "int",```<br>```  // Starting data is in which row or column,```<br>```  "table_fields": [```<br>```      { "field_name": "xxx", //Field name```<br>```          "field_type": "int64", //Field type, supports string, int64, float32, bool, list<string>```<br>```          "if_embedding": true, //Whether to participate in vector indexing```<br>```          "default_value": "xxx", //Default value```<br>```          "if_filter": false //Whether it is a tag filtering field```<br>```    },```<br>```    .....```<br>```  ]```<br>```}```<br> |
|**index** | |object |No |\-\- |**Index configuration** |
||index_config |object |No |\-\- |Knowledge base index configuration<br><br>```JSON```<br>```{```<br>```    "fields": [```<br>```        {```<br>```            "field_name": "type",```<br>```            //Tag name```<br>```            "field_type": "string",```<br>```            //Tag type```<br>```            "default_val": "instruction"```<br>```            //Tag default value```<br>```         },```<br>```         {...}```<br>```    ],```<br>```    "cpu_quota": 1,```<br>```    // CPU quota, integer [1, 100], default value is 1```<br>```    "embedding_model": "base-multilingual-rerank",```<br>```    // Specify the embedding model; the type of knowledge base created is determined by the selected model```<br>```    "embedding_model_version": 240715,```<br>```    // Specify the embedding model version. Optional; if not specified, the default version will be used.```<br>```    "embedding_dimension": 2048,```<br>```    // Embedding dimension```<br>```    "quant": "int8"```<br>```    // Quantization method for the vector```<br>``````<br>```    // Refer to the available options for "embedding_model", "embedding_model_version", "embedding_dimension", and "quant"```<br>```}```<br><br><br>Note:<br><br><br>* The `fields` array defines tags. There is a limit of 180 tags, and their names must be unique. They can be used to filter documents during retrieval.<br><br>* The name of a field cannot start with "_sys_auto"; otherwise, creation will fail.<br><br>* For fields, if not provided or if the value is empty, no tags will be added for filtering.<br><br>* If field_name is set to "doc_id" and the field type is "string", the system will automatically write the doc_id value into the field for subsequently uploaded documents.<br><br>* To create a knowledge base, only the tag fields need to be defined. When you upload documents, you can assign tags to them using the `doc/add` endpoint. |
| |index_type |string |No |hnsw_hybrid |**Specify the indexing algorithm**, supports hnsw_hybrid, hnsw, and flat<br><br>It is recommended to select "hnsw_hybrid", which combines keyword and semantic search to comprehensively improve retrieval accuracy<br><br>For the correspondence between embedding model and indexing algorithm, refer to [Embedding model and index algorithm comparison table](https://docs.byteplus.com/docs/209/collection_create#3d008a9c) |
|**doc_summary_config** | |object |No |\-\- |**Knowledge base summary configuration** |
| |enabled |bool |No |false |**Whether to enable the document AI summary feature**<br><br>Enables or disables the AI\-generated document summary feature for the knowledge base. When enabled, the knowledge base will automatically generate a summary for each document and save the result in the document metadata.<br><br>Note: This feature is only effective when the knowledge base type is unstructured, that is, when data_type is "unstructured_data" |


<span id="b54e69c6"></span>
# Request parameters (standard version)


|**Parameter** |**Sub\-parameter** |**Type** |**Required** |**Default value** |**Parameter description** |
|---|---|---|---|---|---|
|name |\-\- |string |Yes |\-\- |**Knowledge base name**<br><br><br>* Can contain only English letters, numbers, and underscores (_). It must start with an English letter and cannot be empty<br><br>* Length requirement: [1\-64]<br><br>* Knowledge base name must be unique |
|project |\-\- |string |No |default |**Project to which the knowledge base belongs**<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If this field is not specified, it will be created under the default project.</div><br><br><br><div data-tips="true" data-tips-type="warning">To create a knowledge base under a specified project, this field must be configured correctly.</div><br> |
|description |\-\- |string |No |"" |**Knowledge base description**<br><br><br>* Length requirement: [1, 65535] |
|version |\-\- |int |No |4 |2: standard version<br><br>4: pro version<br><br>For the current version, this value is 2 |
|**preprocessing** | |object |No | |**Unstructured document processing strategy**<br><br>Effective when data_type is "unstructured_data"; This parameter is ignored when data_type is "structured_data". |
| |chunking_strategy |string |No |\-\- |**Document chunking strategy**, enumerated values: ["custom_balance"]<br><br><br>* "custom_balance" is the latest default document processing strategy provided by the knowledge base system. This strategy:<br><br>   1. This strategy provides upgraded parsing and understanding for complex documents like PDF and DOCX, with significant improvements in analyzing layout and semantic structures. It optimizes the processing of image content and context, supports mixed arrangements of images and text for better contextual consistency, and improves the parsing of long tables. By integrating the VikingDB semantic and keyword fusion retrieval algorithm, it enhances multimodal content retrieval, increases the recall of relevant information, and improves the signal\-to\-noise ratio of the slicing algorithm, resulting in less irrelevant information and lower semantic loss.<br><br>   2. After selecting this strategy, the effective document processing sub\-parameters include:<br><br>   * "chunk_length" (effective only when "chunking_identifier" is empty)<br><br>   * "merge_small_chunks" (effective only when "chunking_identifier" is empty)<br><br>   * "multi_mode" (effective only when "chunking_identifier" is empty)<br><br>* Please note that the original "default" strategy is currently only used for compatibility with existing knowledge bases and is no longer maintained. **For new knowledge bases, it is recommended to use "custom_balance"**  |
| |chunk_length |int |No |500 |**Maximum length of slices for each document type**<br><br>For value range, see [Embedding model and index algorithm comparison table](https://docs.byteplus.com/docs/209/collection_create#3d008a9c) |
| |merge_small_chunks |bool |No |true |**Whether to merge short text chunks**<br><br>Specifies whether to merge short text chunks. The merged chunk will not exceed the maximum slice length |
| |multi_modal |\-\- |No |\-\- |**Image understanding strategy**<br><br>Enumeration values:<br><br><br>* "image_ocr": image OCR<br><br><br>Parameter passing example:<br><br><br>* When "multi_modal": ["image_ocr"], image OCR is enabled; if no value is passed, image OCR is not enabled<br><br><br>Knowledge bases created using the old parameter name "multi_mode" will retain the original naming, but using this parameter is not recommended for new knowledge bases. |
|**doc_summary_config** | |object |No |\-\- |**Knowledge base summary configuration** |
| |enabled |bool |No |false |**Whether to enable the document AI summary feature**<br><br>Configure whether to enable the document AI\-generated summary feature for the knowledge base. Once enabled, this knowledge base will automatically generate a summary for each document and save the result in the document metadata. |


<span id="3d008a9c"></span>
# Embedding model and index algorithm comparison table


|**Create a knowledge base type** |**Embedding model** |**Model version** |**Output type** |**Index type** |**Vector dimension** |**Quantization method** |**chunk_length value** |**Retrieval type** |
|---|---|---|---|---|---|---|---|---|
|Image/rich text knowledge base |skylark\-embedding\-vision\-and\-m3 |250328 |Dense vectors and sparse vectors |hnsw_hybrid |1024, 2048<br><br>Default 2048 |int8, float, fix16<br><br>Default int8 |[100, 8000]<br><br>Default 2000 |Hybrid retrieval (combines semantic retrieval and keyword matching) |
||skylark\-embedding\-vision |250328 |Dense vectors |hnsw、flat |1024, 2048<br><br>Default 2048 |int8, float, fix16<br><br>Default int8 |[100, 8000]<br><br>Default 2000 |Semantic retrieval (ByteDance proprietary model) |
|Plain text knowledge base |bge\-large\-zh |\-\- |Dense vectors |hnsw, flat |1024 |int8, float, fix16 |[100, 500] |Semantic retrieval |
||bge\-m3 |\-\- |Dense vectors and sparse vectors |hnsw_hybrid |1024 |int8, float, fix16 |[100, 8000] |Hybrid retrieval (combines semantic retrieval and keyword matching) |
|||\-\- ||hnsw、flat |1024 |int8, float, fix16 |[100, 8000] |Semantic retrieval (in this case, sparse vectors are ignored; suitable for pure semantic retrieval scenarios that require long\-text processing capabilities and multilingual retrieval) |
||bge\-large\-zh\-and\-m3 |\-\- |Dense vectors and sparse vectors |hnsw_hybrid |1024 |int8, float, fix16 |[100, 500] |Hybrid retrieval (combines semantic retrieval and keyword matching) |


<span id="dde8863a"></span>
# **Response message**


|**Parameter** |**Parameter description** |
|---|---|
|code |Status code |
|message |Return information |
|data |Returned detailed information<br><br>{<br><br>"resource_id": The ID of the knowledge base.<br><br>} |
|request_id |Unique identifier for each request |


<span id="8e2a6eee"></span>
## **Status code description**


|**Status code** |**HTTP status code** |**Return information** |**Status code description** |
|---|---|---|---|
|0 |200 |success |Success |
|1000001 |403 |unauthorized |Authentication failed |
|1000002 |403 |no permission |Insufficient permissions |
|1000003 |400 |invalid request：%s |Invalid parameter<br><br><br>* Missing required parameter<br><br>* The collection name does not meet the requirements.<br><br>* The field type or its attributes do not meet the constraints. |
|1000004 |400 |collection exists |Collection already exists |


<span id="baea7251"></span>
# Complete example

<span id="d011c07c"></span>
## Request message

Create a structured knowledge base

```Shell
curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-knowledgebase.mlp.cn-hongkong.bytepluses.com/api/knowledge/collection/create \
  -d '{
    "name": "apiexample",
    "description": "test",
    "index": {
        "index_type": "hnsw_hybrid",
        "index_config": {
            "fields": [],
            "quant": "int8",
            "cpu_quota": 1,
            "embedding_model": "skylark-embedding-vision-and-m3",
            "embedding_dimension": 2048
        }
    },
    "table_config": {
        "table_type": "row",
        "table_pos": 1,
        "start_pos": 2,
        "table_fields": [
            {
                "field_type": "string",
                "field_name": "Explanation_Module",
                "if_embedding": true,
                "if_filter": false
            },
            {
                "field_type": "string",
                "field_name": "Sub_Module",
                "if_embedding": true,
                "if_filter": false
            },
            {
                "field_type": "string",
                "field_name": "Question_Example",
                "if_embedding": true,
                "if_filter": false
            },
            {
                "field_type": "string",
                "field_name": "Memoization_Key_Points",
                "if_embedding": true,
                "if_filter": false
            }
        ]
    },
    "data_type": "structured_data",
    "project": "default"
  }'
```


<span id="8046a603"></span>
## Response message

Return on successful execution:

```Shell
HTTP/1.1 200 OK
Content-Length: 43
Content-Type: application/json
 
{
    "code":0,
    "message":"success",
    "data": {
        "resource_id": "kb-8349ef57441ab57"
    },
    "request_id":"021695029537650fd001de666660000000000000000000230da93"
}
```


Return on failed execution:

```Shell
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000003, "message":"invalid request：%s", "request_id": "021695029757920fd001de6666600000000000000000002569b8f"}
```
