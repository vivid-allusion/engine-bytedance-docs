---
title: "list"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/pipeline_list"
---

To programmatically retrieve the configurations of all pipelines within a specific knowledge base, you can use the `api/knowledge/pipeline/list` endpoint. This API reference provides the necessary details, including request parameters for identifying the knowledge base, response structures that outline each pipeline's configuration, and complete curl examples for successful and failed requests.

<span id="3131c45e"></span>
# **Prerequisites**

After completing account registration, identity verification, and obtaining your AK/SK keys and signature as described on the "Signature Authentication Method" page, you can call the API to view all pipelines in a knowledge base.

<span id="795350a2"></span>
# **Request Format**


|**URI** |api/knowledge/pipeline/list |Uniform resource identifier |
|---|---|---|
|**Request method** |POST |Operation type of the client request to the vector database server |
|**Request header** |Content\-Type: application/json |Request message type |
||Authorization: token=\*\*\*\*\*\*\*\*\*\* |Authentication |


<span id="41c941a9"></span>
# **Request parameters**


|Parameter |Type |Required |Default value |Remarks |
|---|---|---|---|---|
|collection_name |string |No |*  |**Knowledge base name** |
|project |string |No |default |**Project name** |
|resource_id |string |No |*  |**Unique knowledge base ID**<br><br><br>* You can either pass the resource_id directly, or pass both the name and project parameters to uniquely identify the knowledge base. |


<span id="9e892742"></span>
# **Response Body**


|**Parameter** |**Parameter description** |
|---|---|
|code |Status code |
|message |A detailed message about the response status. |
|data |// Returns the configuration information of the pipeline<br><br>{<br><br>collection_name: Knowledge base name<br><br>pipeline_list:<br><br>[ { // The content of this object is the same as the content returned by the pipeline/info endpoint<br><br>},<br><br>]<br><br>} |


<span id="5dd25d7c"></span>
## **Description**


|**Status code** |**HTTP status code** |**Message** |**Status code description** |
|---|---|---|---|
|0 |200 |success |Success |
|1000001 |403 |unauthorized |Authentication failed |
|1000002 |403 |no permission |Insufficient permissions |
|1000003 |400 |invalid request: %s |Invalid parameter<br><br><br>* Missing required parameter<br><br>* Collection name does not conform to the naming convention<br><br>* The field type or its attributes do not meet the constraints. |


<span id="539fd6e8"></span>
# Complete example

<span id="bf434998"></span>
## Sample Request

```Shell
curl -i -X POST \
-H 'Content-Type: application/json' \
-H 'Authorization: token=****' \
https://api-knowledgebase.mlp.cn-hongkong.bytepluses.com/api/knowledge/pipeline/list \
-d '{
"collection_name": "test_collection_name",
"project": "default"
}'
```


<span id="ebd2c69a"></span>
## Sample Response

Successful response:

```Shell
HTTP/1.1 200 OK
Content-Length: 1024
Content-Type: application/json

{
  "code": 0,
  "message": "success",
  "request_id": "021695029537650fd001de666660000000000000000000230da93",
  "data": {
    "collection_name": "test_collection_name",
    "pipeline_list": [
      {
        "pipeline_name": "default",
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
        "create_time": "2024-11-01T10:30:00Z",
        "update_time": "2024-11-01T10:31:00Z"
      },
      {
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
            "chunk_size": 1000,
            "chunk_overlap": 200
          }
        },
        "auto_sync_doc": false,
        "create_time": "2024-12-01T15:20:00Z",
        "update_time": "2024-12-01T15:21:00Z"
      }
    ]
  }
}
```


Failed response:

```JSON
HTTP/1.1 400 Bad Request
Content-Length: 95
Content-Type: application/json

{
"code": 1000003,
"message": "invalid request: collection not found",
"request_id": "021695029757920fd001de6666600000000000000000002569b8f"
}
```
