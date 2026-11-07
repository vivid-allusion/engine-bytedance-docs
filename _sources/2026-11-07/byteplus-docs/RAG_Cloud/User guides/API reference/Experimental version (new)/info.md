---
title: "info"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/pipeline_info"
---

The `api/knowledge/pipeline/info` endpoint is used to view information about the experimental version of a specific knowledge base

<span id="90dc4a2a"></span>
# **Prerequisites**

After completing account registration, identity verification, AK/SK key acquisition, and signature retrieval on the 'Signature Authentication Method' page, you can call the API endpoint to view information about an experimental version in a knowledge base

<span id="e9451e6b"></span>
# **Request endpoint**


|**URI** |api/knowledge/pipeline/info |Uniform resource identifier |
|---|---|---|
|**Request method** |POST |Type of operation requested by the client to the vector database server |
|**Request headers** |Content\-Type: application/json |Request message type |
||Authorization: token=\*\*\*\*\*\*\*\*\*\* |Authentication |


<span id="6eb56b60"></span>
# **Request parameters**


|Parameter |Type |Required |Default value |Remarks |
|---|---|---|---|---|
|collection_name |string |No |*  |**Knowledge base name** |
|project |string |No |default |**Project name** |
|resource_id |string |No |*  |**Unique knowledge base ID**<br><br>You can choose to pass resource_id directly, or pass both name and project as the unique identifier of the knowledge base |
|name |string |Yes |*  |**Experimental version name**<br><br><br>* Cannot use the existing system default value "default"<br><br>* The experimental version name must consist of letters, numbers, and underscores, and must begin with a letter<br><br>* Length must not exceed 32 characters |


<span id="e7e4095d"></span>
# **Response message**


|**Parameter** |**Parameter description** |
|---|---|
|code |Status code |
|message |Return information |
|data |// Returns the pipeline configuration information<br><br>{<br><br>collection_name: Name of the knowledge base to which the current pipeline belongs<br><br>pipeline_info: Complete configuration information of the pipeline (including parsing strategy, index configuration, storage, and more)<br><br>pipeline_name: Name of the experimental version<br><br>auto_sync_doc: Indicates whether the pipeline automatically synchronizes newly imported documents<br><br>} |


<span id="45daf402"></span>
## **Status code description**


|**Status code** |**HTTP status code** |**Return information** |**Status code description** |
|---|---|---|---|
|0 |200 |success |Success |
|1000001 |403 |unauthorized |Authentication failed |
|1000002 |403 |no permission |Insufficient permissions |
|1000003 |400 |invalid request：%s |Invalid parameter<br><br><br>* Missing required parameter<br><br>* The collection name does not conform to specifications<br><br>* The field type and related field attributes do not meet the constraints |


<span id="aa8b6caa"></span>
# Complete example

<span id="8c1203f1"></span>
## Request message

```Shell
curl -i -X POST \
-H 'Content-Type: application/json' \
-H 'Authorization: token=****' \
https://api-knowledgebase.mlp.cn-hongkong.bytepluses.com/api/knowledge/pipeline/info \
-d '{
"collection_name": "test_collection_name",
"project": "default",
"name": "custom_pipeline_01"
}'
```


<span id="af5548ac"></span>
## Response message

Successful execution returns:

```Shell
HTTP/1.1 200 OK
Content-Length: 486
Content-Type: application/json

{
  "code": 0,
  "message": "success",
  "request_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "data": {
    "collection_name": "test_collection_name",
    "pipeline_info": {
      "pipeline_name": "custom_pipeline_01",
      "data_type": "unstructured_data",
      "index": {
        "vector_index": {
          "dimension": 1536,
          "metric": "cosine"
        }
      },
      "preprocessing": {
        "chunk_strategy": {
          "chunk_type": "fixed_size",
          "chunk_size": 800,
          "chunk_overlap": 400
        }
      },
      "auto_sync_doc": true,
      "create_time": "2024-12-01T10:30:00Z",
      "update_time": "2024-12-01T10:30:00Z"
    }
  }
}
```


Failed execution returns:

```JSON
HTTP/1.1 400 Bad Request
Content-Length: 95
Content-Type: application/json

{
"code": 1000003,
"message": "invalid request: pipeline not found",
"request_id": "021695029757920fd001de6666600000000000000000002569b8f"
}
```
