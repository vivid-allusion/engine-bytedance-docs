---
title: "re-process"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/re-process"
---

<span id="be5195e1"></span>
# Overview

The `api/knowledge/doc/re-process` endpoint is used to synchronize a specified document to an experimental version

<span id="6cc13a4c"></span>
# **Prerequisites**

After completing account registration, identity verification, AK/SK key acquisition, and signature acquisition on the "Signature authentication method" page, you can call the API to synchronize documents to the experimental version of the knowledge base.

<span id="85b1b7e6"></span>
# **Request endpoint**


|**URI** |/api/knowledge/doc/re\-process |Uniform resource identifier |
|---|---|---|
|**Request method** |POST |Operation type requested by the client to the vector database server |
|**Request header** |Content\-Type: application/json |Request message type |
||Authorization: token=\*\*\*\*\*\*\*\*\*\* |Authentication |


<span id="aebcf76c"></span>
# **Request parameters**


|Parameter |Type |Required |Default value |Remarks |
|---|---|---|---|---|
|collection_name |string |No |\-\- |**Knowledge base name** |
|project |string |No |default |**Project to which the knowledge base belongs**<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If this field is not specified, it will be created under the default project.</div><br><br><br><div data-tips="true" data-tips-type="warning">To operate on a knowledge base under a specified project, this field must be configured correctly.</div><br> |
|resource_id |string |No |\-\- |**Unique knowledge base ID**<br><br>You can choose to pass resource_id directly, or pass both collection_name and project as the unique identifier of the knowledge base |
|pipeline_name |string |Yes |\-\- |**Experimental version name** |
|doc_id |string |Yes |\-\- |**ID of the document to be imported** |
|auto_skip |bool |No |false |**Whether to deduplicate**<br><br>When enabled, document IDs that already exist in the experimental version will be automatically skipped |


<span id="07abe74b"></span>
# **Response message**


|**Parameter** |**Parameter description** |
|---|---|
|code |Status code |
|message |Return information |


<span id="4c804b58"></span>
## **Status code description**


|**Status code** |**HTTP status code** |**Return information** |**Status code description** |
|---|---|---|---|
|0 |200 |success |Successful |
|1000001 |403 |unauthorized |Authentication failed |
|1000002 |403 |no permission |Insufficient permissions |
|1000003 |400 |invalid request：%s |Invalid parameter<br><br><br>* Missing required parameter<br><br>* Collection name does not conform to specification<br><br>* Field type and related field attributes do not meet constraint conditions |


<span id="1339509c"></span>
# Complete example

<span id="9ffaa427"></span>
## Request message

```Shell
curl -i -X POST \
    -H 'Content-Type: application/json' \
    -H 'Authorization: token=****' \
    https://api-knowledgebase.mlp.cn-hongkong.bytepluses.com/api/knowledge/doc/re-process \
    -d '{
    "collection_name": "test_collection_name",
    "project": "default",
    "pipeline_name": "custom_pipeline",
    "doc_id": "test_doc_123",
    "auto_skip": true
}'
```


<span id="16020e28"></span>
## Response message

Return on successful execution:

```Shell
HTTP/1.1 200 OK
Content-Length: 78
Content-Type: application/json

{"code":0,"message":"success","request_id":"021695029537650fd001de666660000000000000000000230da93"}
```


Return on failed execution:

```JSON
HTTP/1.1 400 Bad Request
Content-Length: 95
Content-Type: application/json

{
"code": 1000003,
"message": "invalid request: missing required parameter doc_id",
"request_id": "021695029757920fd001de6666600000000000000000002569b8f"
}
```
