---
title: "create"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/pipeline_create"
---

To compare different data processing methods without affecting the official version, you can use the `api/knowledge/pipeline/create` endpoint. This API allows you to create an experimental version (a pipeline) with an independent offline data processing workflow, enabling you to test and publish the best\-performing configuration.

> A pipeline corresponds to the "experimental version" feature in the knowledge base console. Each pipeline has an independent offline data processing workflow. Multiple pipelines can be used to compare different processing methods for the same batch of data, and the best pipeline can be published as the official version.

> Note:

> * A single knowledge base **can create up to 10 pipelines.** 

> * Only Pro version knowledge bases support the experimental version API.


<span id="07c64bc3"></span>
# **Prerequisites**

After completing account registration, identity verification, AK/SK key acquisition, and signature generation on the "Signature Authentication Method" page, you can call the API to create a new experimental version from the knowledge base.

<span id="cabd36cc"></span>
# **Request endpoint**


|**URI** |api/knowledge/pipeline/create |Uniform resource identifier |
|---|---|---|
|**Request method** |POST |Operation type requested by the client to the vector database server |
|**Request headers** |Content\-Type: application/json |Request message type |
||Authorization: token=\*\*\*\*\*\*\*\*\*\* |Authentication |


<span id="17f80b8f"></span>
# **Request parameters**


|Parameter |Sub\-parameter |Type |Required |Default value |Description |
|---|---|---|---|---|---|
|collection_name |*  |string |No |*  |**Knowledge base name** |
|project |*  |string |No |default |**Project name** |
|resource_id |*  |string |No |*  |**Unique knowledge base ID**<br><br><br>* You can choose to pass resource_id directly, or pass both name and project as the unique identifier for the knowledge base. |
|name |*  |string |Yes |*  |**Experimental version name**<br><br><br>* You cannot use the existing system default value "default".<br><br>* The experimental version name must consist of letters, numbers, and underscores, and must start with a letter.<br><br>* The length must not exceed 32 characters. |
|index | |object |No | |**Index configuration** |
| |index_config |object |No |*  |```JSON```<br>```{```<br>```    "fields": [```<br>```        {```<br>```            "field_name": "type",```<br>```            // Tag name```<br>```            "field_type": "string",```<br>```            // Tag type```<br>```            "default_val": "instruction"```<br>```            // Tag default value```<br>```         },```<br>```         {...}```<br>```    ],```<br>```    "cpu_quota": 1,```<br>```    // CPU quota, integer type, greater than 0, default value is 1```<br>```    "embedding_model": "base-multilingual-rerank",```<br>```    // Specify vectorization model```<br>```    "embedding_dimension": 2048,```<br>```    // Vector dimension```<br>```    "quant": "int8"```<br>```    // Vector quantization method```<br>```    // For the optional ranges for "embedding_model", "embedding_dimension", and "quant", refer to the relevant documentation.```<br>```}```<br><br><br>Note:<br><br><br>* Fields are used as "tags", with a limit of 180. Names must not be duplicated, and they can be used to filter documents during retrieval.<br><br>* The name of fields must not start with "_sys_auto"; otherwise, creation will fail.<br><br>* For fields, if not provided or if the value is empty, no filter fields will be added.<br><br>* If the field is set to "doc_id" and the field type is "string", the system will write the doc_id value of subsequently uploaded documents. |
| |index_type |string |No |hnsw_hybrid |**Specify index algorithm**<br><br>Supports hnsw_hybrid, hnsw, and flat<br><br>It is recommended to select "hnsw_hybrid", which combines keyword and semantic understanding to improve overall retrieval accuracy.<br><br>For compatibility between the embedding model and index algorithm, refer to [Embedding model and index algorithm comparison table](https://docs.byteplus.com/docs/209/collection_create#3d008a9c) |
|preprocessing | |object |No | |**Unstructured document processing strategy**<br><br><br>* Effective when data_type is "unstructured_data"; not applicable when it is "structured_data". |
| |chunking_strategy |string |No |*  |**Selected chunking strategy**, enumerated values: ["custom_balance", "custom"]<br><br><br>* "custom_balance" is the latest default document processing strategy provided by the Ark Knowledge Base system. This strategy:<br><br>   1. This strategy enhances parsing and understanding for complex documents like PDF and DOCX, significantly improving the analysis of complex document layouts and semantic structures. It specifically optimizes the processing of image content and its context, supports mixed arrangements of image and text chunks to enhance contextual consistency, and optimizes the processing of table content for parsing long tables. It also integrates VikingDB semantic and keyword fusion retrieval algorithms to improve multimodal content retrieval and recall. Finally, this strategy increases the signal\-to\-noise ratio of the chunking algorithm, resulting in less irrelevant information and reduced semantic loss.<br><br>   2. After selecting this strategy, the effective document processing strategy sub\-parameters include:<br><br>   * "chunk_length" (effective only when "chunking_identifier" is empty)<br><br>   * "merge_small_chunks" (effective only when "chunking_identifier" is empty)<br><br>   * "multi_mode" (effective only when "chunking_identifier" is empty)<br><br>* "custom" is a document processing strategy that uses custom delimiters. After selecting this strategy, the effective document processing strategy sub\-parameters include:<br><br>   * “chunking_identifier"<br><br>   * "chunk_length" (effective only when "chunking_identifier" is empty)<br><br>   * "merge_small_chunks" (effective only when "chunking_identifier" is empty)<br><br>   * "multi_mode" (effective only when "chunking_identifier" is empty)<br><br>* Please note that the original "default" strategy is currently only used for compatibility with existing knowledge bases and is no longer maintained. **It is recommended to use "custom_balance" for new knowledge bases.**  |
| |chunking_identifier |list |No |*  |**Custom delimiter** |
| |chunk_length |int |No |500 |**Maximum chunk length**<br><br>For value range, see [Embedding model and index algorithm comparison table](https://docs.byteplus.com/docs/209/collection_create#3d008a9c) |
| |merge_small_chunks |bool |No |true |**Whether to merge short text chunks**<br><br>Configure whether to merge short text chunks. The merged text chunks will not exceed the maximum chunk length. |
| |multi_modal |*  |No |*  |**Image recall strategy**<br><br>Enumerated values:<br><br><br>* "image_ocr": image OCR<br><br><br>Parameter passing example:<br><br><br>* When `"multi_modal": ["image_ocr"]`, image OCR is enabled. If no value is passed, image OCR is not enabled.<br><br><br>Knowledge bases created using the old parameter name "multi_mode" will retain the original naming, but it is not recommended for new knowledge bases. |
|data_type |*  |string |Yes |*  |**Data type in the knowledge base**<br><br><br>* unstructured_data: Unstructured data<br><br>* structured_data: Structured data |
|table_config |*  |object |No |*  |**Structured knowledge base table field definition**<br><br>Effective when data_type is "structured_data"<br><br>```JSON```<br>```{```<br>```  "table_type": "row","col",```<br>```  // "row" means parse from rows, and "col" means parse from columns.```<br>```  "table_pos": "int",```<br>```  // Specifies which row or column the field is located in.```<br>```  "start_pos": "int",```<br>```  // Specifies which row the data starts in.```<br>```  "table_fields": [```<br>```      { "field_name": "xxx", // Field name```<br>```          "field_type": "int64", // Field type, supports string, int64, float32, bool```<br>```          "if_embedding": true, // Specifies whether to include the field in the index.```<br>```          "default_value":"xxx", // Default value```<br>```          "if_filter": false // Specifies whether to set the field as a filter field.```<br>```    },```<br>```    .....```<br>```  ]```<br>```}```<br> |
|auto_sync_doc |*  |bool |No |*  |**Whether to automatically synchronize newly added documents**<br><br>When enabled, documents uploaded to the knowledge base via the add_doc interface are automatically synchronized to the current experimental version |


<span id="5e28bbb3"></span>
# **Response message**


|**Parameter** |**Parameter description** |
|---|---|
|code |Status code |
|message |Return information |


<span id="29bead65"></span>
## **Status code description**


|**Status code** |**HTTP status code** |**Return information** |**Status code description** |
|---|---|---|---|
|0 |200 |success |Success |
|1000001 |403 |unauthorized |Authentication failed |
|1000002 |403 |no permission |Insufficient permissions |
|1000003 |400 |invalid request：%s |Invalid parameter<br><br><br>* Missing required parameter<br><br>* The collection name is invalid or does not follow the naming conventions.<br><br>* The field type or related field attributes do not meet the constraints. |


<span id="2d8fa248"></span>
# Complete example

<span id="07c740f0"></span>
## Request message

```Shell
curl -i -X POST \
-H 'Content-Type: application/json' \
-H 'Authorization: token=****' \
https://api-knowledgebase.mlp.cn-hongkong.bytepluses.com/api/knowledge/pipeline/create \
-d '{
  "collection_name": "test_collection_name",
  "project": "default",
  "name": "custom_pipeline_01",
  "data_type": "unstructured_data",
  "index_type": "hnsw_hybrid",
  "index_config": {
    "embedding_dimension": 2048,
    "quant": "int8",
    "cpu_quota": 1,
    "fields": [
      {
        "field_name": "type",
        "field_type": "string",
        "default_val": "instruction"
      }
    ]
  },
  "preprocessing": {
    "chunking_strategy": "custom_balance",
    "chunk_length": 800,
    "merge_small_chunks": true,
    "multi_modal": ["image_ocr"]
  },
  "auto_sync_doc": true
}'
```


<span id="67363b70"></span>
## Response message

Return on success:

```Shell
HTTP/1.1 200 OK
Content-Length: 78
Content-Type: application/json

{"code":0,"message":"success","request_id":"021695029537650fd001de666660000000000000000000230da93"}
```


Return on failure:

```JSON
HTTP/1.1 400 Bad Request
Content-Length: 105
Content-Type: application/json

{
"code": 1000003,
"message": "invalid request: pipeline name cannot be 'default'",
"request_id": "021695029757920fd001de6666600000000000000000002569b8f"
}
```
