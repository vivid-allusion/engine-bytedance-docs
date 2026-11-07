---
title: "list"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/collection_list"
---

This section describes how to query all knowledge base information under an account.

<span id="736b2ad1"></span>
# Overview

The `/knowledge/collection/list` API is used to query all knowledge base information under an account, and by default, the results are sorted by the creation time of the knowledge base from newest to oldest.

<span id="fb6e2af0"></span>
# **Prerequisites**

After completing account registration, real\-name authentication, AK/SK key acquisition, and signature acquisition on the "Signature Authentication Method" page, the API can be called to view the knowledge base list.

<span id="bbaad420"></span>
# **Request API**


|**URI** |/api/knowledge/collection/list |Uniform resource identifier |
|---|---|---|
|**Request method** |POST |Operation type of the client request to the vector database server |
|**Request header** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="df878baa"></span>
# **Request parameters (applicable to both pro version and standard version)** 


|**Parameter** |**Type** |**Required** |**Default value** |**Parameter description** |
|---|---|---|---|---|
|project |string |No |\-\- |**Project to which the knowledge base belongs**<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If not specified, all knowledge bases under all projects will be returned</div><br><br><br><div data-tips="true" data-tips-type="warning">To operate on the knowledge base under a specified project, this field must be configured correctly.</div><br> |
|brief |bool |No |false |**Whether to query and return the index status**<br><br>false means to query and return the index status<br><br>true means not to query and return the index status |


&nbsp;

<span id="b0c4b214"></span>
# **Response message**


|**Parameter** |**Parameter description** |
|---|---|
|code |Status code |
|message |Return message |
|request_id |Unique identifier for each request |
|data |* total_num: Total number of knowledge bases in the list<br><br>* collection_list: Detailed information list of knowledge bases, array type, each element is the detailed information of a knowledge base, for specific parameter format see the info documentation<br><br>* collection: Knowledge base name<br><br>* version: Knowledge base version, the value is 2 for the standard version; the value is 4 for the pro version |


<span id="cbba52d5"></span>
## **Status code description**


|**Status code** |**HTTP status code** |**Return message** |**Status code description** |
|---|---|---|---|
|0 |200 |success |Success |
|1000001 |401 |unauthorized |Authentication failed |
|1000002 |403 |no permission |Insufficient permissions |
|1000003 |400 |invalid request：%s |Invalid parameter |
|1000005 |400 |collection not exist |Collection does not exist |


<span id="1b79b9de"></span>
# Complete example

<span id="cc816a82"></span>
## Request message

```Shell
curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-knowledgebase.mlp.cn-hongkong.bytepluses.com/api/knowledge/collection/list \
  -d '{
    "project": "abc",
    "brief": false
}'
```


<span id="9116ae07"></span>
## Response message

Return on successful execution:

```Shell
HTTP/1.1 200 OK
Content-Length: 43
Content-Type: application/json
 
{
    "code": 0,
    "data": {
        "total_num": 200,
        "collection_list": [
            {
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
                                    "embedding_model": "skylark-embedding-vision",
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
                                        "field_name": "Explanation Module",
                                        "field_type": "string",
                                        "if_embedding": true,
                                        "if_filter": false
                                    },
                                    {
                                        "field_name": "Sub-module",
                                        "field_type": "string",
                                        "if_embedding": true,
                                        "if_filter": false
                                    },
                                    {
                                        "field_name": "Question Example",
                                        "field_type": "string",
                                        "if_embedding": true,
                                        "if_filter": false
                                    },
                                    {
                                        "field_name": "Memorization - Key Points",
                                        "field_type": "string",
                                        "if_embedding": true,
                                        "if_filter": false
                                    }
                                ]
                            }
                        ]
                    }
                ],
                "data_type": "structured_data",
                "resource_id": "kb-be6833502748aaef",
                "project": "default"
            }
        ]
    },
    "message": "success",
    "request_id": "02172474869381600000000000000000000ffff0a005049697e42"
}
```


Return on failed execution:

```Shell
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000003, "message":"invalid request：%s", "request_id": "021695029757920fd001de6666600000000000000000002569b8f"}
```
