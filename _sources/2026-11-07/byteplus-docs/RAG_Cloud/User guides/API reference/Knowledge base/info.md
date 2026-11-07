---
title: "info"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/collection_info"
---

This section describes how to view the information of an existing knowledge base.

<span id="e4fcbe8e"></span>
# Overview

The `/api/knowledge/collection/info` API is used to view the details of a knowledge base. It returns the description of the knowledge base and detailed information about the experimental versions configured for the knowledge base, based on the knowledge base name.

<span id="5fdc6b51"></span>
# **Prerequisites**

After completing account registration, real\-name authentication, AK/SK key acquisition, and signature acquisition on the "Signature Authentication Method" page, you can call the API to view knowledge base information.

<span id="4003ab4c"></span>
# **Request API**


|**URI** |/api/knowledge/collection/info |Uniform Resource Identifier |
|---|---|---|
|**Request method** |POST |Type of operation requested by the client to the vector database server |
|**Request header** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="597fbea7"></span>
# **Request parameters (applicable to both pro version and standard version)** 


|**Parameter** |**Type** |**Required** |**Default value** |**Parameter description** |
|---|---|---|---|---|
|name |string |No |\-\- |**Knowledge base name** |
|project |string |No |default |**Project to which the knowledge base belongs**<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">To operate the knowledge base under a specified project, this field must be configured correctly.</div><br> |
|resource_id |string |No |\-\- |**Unique knowledge base ID**<br><br>You can choose to pass resource_id directly, or pass both name and project as the unique identifier of the knowledge base |


&nbsp;

<span id="7b69f9d8"></span>
# **Response message**


|**Parameter** |**Parameter description** |
|---|---|
|code |Status code |
|message |Return message |
|request_id |Unique identifier for each request |
|data |Retrieved return content |


data return value


|Field |Subfield |Field type |Description |
|---|---|---|---|
|collection_name |\-\- |string |Knowledge base name |
|version |\-\- |int |2: standard version<br><br>4: pro version |
|description |\-\- |string |Knowledge base description |
|doc_num |\-\- |int |Number of documents in the knowledge base |
|create_time |\-\- |int |Time when the knowledge base was created |
|update_time |\-\- |int |Time when the knowledge base was updated |
|creator |\-\- |string |User who created the knowledge base |
|pipeline_list | |list |List of experimental versions (pipelines) under the knowledge base |
||pipeline_stat |json |Document import status under pipeline<br><br>```JSON```<br>```{```<br>```    "doc_num": 1, // Number of imported documents```<br>```    "finish_doc_num": 1, // Number of documents imported successfully```<br>```    "point_num": 1, // Number of slices```<br>```    "success_doc_num": 1 // Number of documents imported successfully (parsing of slices completed)```<br>```},```<br> |
||index_list |list |Knowledge base index details |
||preprocessing_list |list |Knowledge preprocessing configuration<br><br>```JSON```<br>```{```<br>```    "chunking_strategy": "custom_balance",// Slicing strategy```<br>```    "chunking_identifier": null, // Custom delimiter```<br>```    "chunk_length": 2000, // Maximum slice length```<br>```    "merge_small_chunks": true // Whether to merge short text slices```<br>```    ...```<br>``` }```<br> |
||table_config_list |list |Structured knowledge base table structure<br><br>```JSON```<br>```{```<br>```  "table_type": "row","col",```<br>```  // rowindicates parsing starts from rows, col indicates parsing starts from columns,```<br>```  "table_pos": "int",```<br>```  // The field is located in which row or column,```<br>```  "start_pos": "int",```<br>```  // Which row contains the starting data,```<br>```  "table_fields": [```<br>```      {```<br>```          "field_name": "xxx", // Field name```<br>```          "field_type": "int64", // Field type, supports string, int64, float32, bool, list<string>```<br>```          "if_embedding": true, // Whether to participate in indexing```<br>```          "default_value":"xxx", // Default value```<br>```          "if_filter": false // Whether this is a tag filtering field```<br>```    },```<br>```    .....```<br>```  ]```<br>```}```<br> |
||data_type |string |Data type in the knowledge base |
|resource_id |\-\- |string |Unique knowledge base ID |
|project |\-\- |sring |Project to which the knowledge base belongs |
|type | |list |Knowledge base type information |


index_list return value


|Field |Subfield |Field type |Description |
|---|---|---|---|
|index_type |\-\- |string |Index algorithm |
|index_config | |list |Index configuration details |
||vector_field |json |Dense vector field<br><br>```JSON```<br>```{```<br>```    "field_name": "_sys_auto_content_vector", // Field name```<br>```    "field_type": "vector", // Field type```<br>```    "dim": 2048 // Vector dimension```<br>```}```<br> |
||sparse_vector_field | |Sparse vector field<br><br>```JSON```<br>```{```<br>```    "field_name": "_sys_auto_content_vector", // Field name```<br>```    "field_type": "vector", // Field type```<br>```}```<br> |
||cpu_quota |int |CPU quota |
||distance |string |Distance type |
||quant |string |Quantization method |
||embedding_model |string |Embedding model |
||embedding_dimension |int |Embedding dimension |
||need_instruction |bool |Whether to concatenate instruction for retrieval |
||fields |list[object] |Dataset field details<br><br>```JSON```<br>```[```<br>```    {```<br>```    "field_name": "_sys_auto_id", // Field name```<br>```    "field_type": "string", // Field type```<br>```    },```<br>```    ......```<br>```]```<br> |
||field_enumerated_list |string |Tag list |
|primary_key |\-\- |sring |Primary key |
|status |\-\- |int |Index status<br><br>```Python```<br>```Status:```<br>```-1: Pending build```<br>```0 : Building```<br>```1 : Build completed```<br>```2 : Build failed```<br>```3 : In progress/Changing```<br> |


<span id="2c992e8e"></span>
## **Status code description**


|**Status code** |**HTTP status code** |**Return message** |**Status code description** |
|---|---|---|---|
|0 |200 |success |success |
|1000001 |401 |unauthorized |Authentication failed |
|1000002 |403 |no permission |Insufficient permissions |
|1000003 |400 |invalid request：%s |Invalid parameter |
|1000005 |400 |collection not exist |Collection does not exist |


<span id="b87caf6c"></span>
# Complete example

<span id="f6700990"></span>
## Request message

```Shell
curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-knowledgebase.mlp.cn-hongkong.bytepluses.com/api/knowledge/collection/info \
  -d '{
    "name": "test_collection_name",
    "project": ""
}'
```


<span id="2c2fb601"></span>
## Response message

Return on success:

```Shell
{
    "code": 0,
    "data": {
        "collection_name": "apiexample",
        "description": "test",
        "create_time": 1724747158,
        "update_time": 1724747158,
        "creator": "xxx",
        "pipeline_list": [
            {
                "pipeline_type": "user_define",
                "pipeline_stat": {
                    "doc_num": 0,
                    "finish_doc_num": 0,
                    "point_num": 0,
                    "success_doc_num": 0
                },
                "index_list": [
                    {
                        "index_type": "hnsw_hybrid",
                        "index_config": {
                            "vector_field": {
                                "field_name": "_sys_auto_content_vector",
                                "field_type": "vector",
                                "dim": 2048
                            },
                            "sparse_vector_field": {
                                "field_name": "_sys_auto_content_sparse_vector",
                                "field_type": "sparse_vector"
                            },
                            "cpu_quota": 1,
                            "distance": "ip",
                            "quant": "int8",
                            "embedding_model": "skylark-embedding-vision-and-m3",
                            "embedding_dimension": 2048,
                            "need_instruction": true,
                            "fields": [
                                {
                                    "field_name": "_sys_auto_id",
                                    "field_type": "string"
                                },
                                {
                                    "field_name": "_sys_auto_doc_id",
                                    "field_type": "string"
                                },
                                {
                                    "field_name": "_sys_auto_chunk_id",
                                    "field_type": "int64"
                                },
                                {
                                    "field_name": "_sys_auto_doc_type",
                                    "field_type": "string"
                                },
                                {
                                    "field_name": "_sys_auto_add_type",
                                    "field_type": "string"
                                }
                            ]
                        },
                        "primary_key": "",
                        "status": -1
                    }
                ],
                "preprocessing_list": [
                    {
                        "chunking_strategy": "default",
                        "chunking_identifier": null,
                        "chunk_length": 2000
                    }
                ],
                "table_config_list": [
                    {
                        "table_type": "row",
                        "table_pos": 1,
                        "start_pos": 2,
                        "table_fields": [
                            {
                                "field_name": "Explanation_Module",
                                "field_type": "string",
                                "if_embedding": true,
                                "if_filter": false
                            },
                            {
                                "field_name": "Sub_Module",
                                "field_type": "string",
                                "if_embedding": true,
                                "if_filter": false
                            },
                            {
                                "field_name": "Question_Example",
                                "field_type": "string",
                                "if_embedding": true,
                                "if_filter": false
                            },
                            {
                                "field_name": "Key_Explanation_Points",
                                "field_type": "string",
                                "if_embedding": true,
                                "if_filter": false
                            }
                        ]
                    }
                ],
                "data_type": "structured_data"
            }
        ],
        "resource_id": "kb-be6833502748aaef",
        "project": "default"
    },
    "message": "success",
    "request_id": "02172474937697900000000000000000000ffff0a00501d3f1d67"
}
```


Return on failure:

```Shell
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000003, "message":"invalid request：%s", "request_id": "021695029757920fd001de6666600000000000000000002569b8f"}
```
