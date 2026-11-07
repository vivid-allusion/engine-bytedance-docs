---
title: "batch-to-pipeline"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/batch-to-pipeline"
---

<span id="1b090312"></span>
# Overview

The `api/knowledge/doc/batch-to-pipeline` endpoint is used to synchronize all existing documents in the knowledge base to an experimental version.

Based on the timestamp when the interface receives the request, all historical documents created before that timestamp are imported. To automatically synchronize newly added documents to the current experimental version, enable the `/api/knowledge/pipeline/update/auto_sync_doc` interface.

<span id="9ae21e44"></span>
# **Prerequisites**

After completing account registration, real\-name authentication, acquisition of AK/SK keys, and signature acquisition on the "Signature Authentication Method" page, you can call the API to delete documents from the knowledge base.

<span id="1e328236"></span>
# **Request interface**


|**URI** |/api/knowledge/doc/batch\-to\-pipeline |Uniform resource identifier |
|---|---|---|
|**Request method** |POST |Type of operation requested by the client to the vector database server |
|**Request header** |Content\-Type: application/json |Request message type |
||Authorization: token=\*\*\*\*\*\*\*\*\*\* |Authentication |


<span id="79fce31d"></span>
# **Request parameters**


|Parameter |Type |Required |Default value |Remarks |
|---|---|---|---|---|
|collection_name |string |No |\-\- |**Knowledge base name** |
|project |string |No |default |**Project to which the knowledge base belongs**<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If this field is not specified, it will be created under the default project.</div><br><br><br><div data-tips="true" data-tips-type="warning">To operate on a knowledge base under a specified project, this field must be configured correctly.</div><br> |
|resource_id |string |No |\-\- |**Unique knowledge base ID**<br><br>You can choose to pass resource_id directly, or pass both collection_name and project as the unique identifier of the knowledge base. |
|pipeline_name |string |Yes |\-\- |**Experimental version name** |
|timestamp |int |No |\-\- |**Timestamp in seconds**<br><br><br>* Specify the import of all documents created before a certain point in time |


<span id="1791c4d5"></span>
# **Response message**


|**Parameter** |**Parameter description** |
|---|---|
|code |Status code |
|message |Return information |


<span id="50eb566b"></span>
## **Status code description**


|**Status code** |**HTTP status code** |**Return information** |**Status code description** |
|---|---|---|---|
|0 |200 |success |Success |
|1000001 |403 |unauthorized |Authentication failed |
|1000002 |403 |no permission |Insufficient permissions |
|1000003 |400 |invalid request：%s |Invalid parameter<br><br><br>* Missing required parameter<br><br>* Collection name does not conform to the specification<br><br>* Field type and related field attributes do not meet constraint conditions |


<span id="14a14718"></span>
# Complete example

<span id="6be1c56f"></span>
## Request message

```Shell
curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: token=****' \
  https://api-knowledgebase.mlp.cn-hongkong.bytepluses.com/api/knowledge/doc/batch-to-pipeline \
  -d '{
    "collection_name": "test_collection_name",
    "project": "default",
    "pipeline_name": "custom_pipeline",
    "timestamp": 1703923200
}'
```


<span id="95c67da5"></span>
## Response message

Return on successful execution:

```Shell
HTTP/1.1 200 OK
Content-Length: 78
Content-Type: application/json

{"code":0,"message":"success","request_id":"021695029537650fd001de666660000000000000000000230da93"}
```


Return on failed execution:

```Shell
HTTP/1.1 400 Bad Request
Content-Length: 95
Content-Type: application/json

{
  "code": 1000003,
  "message": "invalid request: missing required parameter pipeline_name",
  "request_id": "021695029757920fd001de6666600000000000000000002569b8f"
}
```
