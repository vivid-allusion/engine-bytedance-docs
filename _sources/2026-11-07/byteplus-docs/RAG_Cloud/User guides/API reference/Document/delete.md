---
title: "delete"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/doc_delete"
---

<span id="6e6c3725"></span>
# Overview

The `/api/knowledge/doc/delete` endpoint is used to delete documents from the knowledge base or from a specific experimental version.

> You can delete documents only under a specific experimental version by specifying the pipeline_name parameter.


<span id="c6757c31"></span>
# **Prerequisites**

After completing account registration, identity verification, AK/SK key acquisition, and signature retrieval on the "Signature Authentication Method" page, you can call the API endpoint to delete documents from the knowledge base.

<span id="a6f69046"></span>
# **Request endpoint**


|**URI** |/api/knowledge/doc/delete |Uniform resource identifier |
|---|---|---|
|**Request method** |POST |Type of operation requested by the client from the vector database server |
|**Request headers** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="1795a5d3"></span>
# **Request parameters**


|**Parameter** |**Type** |**Required** |**Default value** |**Parameter description** |
|---|---|---|---|---|
|collection_name |string |No |\-\- |**Knowledge base name** |
|project |string |No |default |**Project to which the knowledge base belongs**<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If this field is not specified, the knowledge base will be created in the default project.</div><br><br><br><div data-tips="true" data-tips-type="warning">To operate on a knowledge base in a specified project, you must configure this field correctly.</div><br> |
|resource_id |string |No |\-\- |**Unique knowledge base ID**<br><br>You can choose to pass resource_id directly, or pass both collection_name and project together to uniquely identify the knowledge base. |
|doc_id |string |Yes |\-\- |**ID of the document to be deleted** |
|pipeline_name |string |No |\-\- |**Experimental version name**<br><br><br>* If not specified, by default, documents in the current knowledge base and all its associated experimental versions will be deleted.<br><br>* If specified, only documents under that experimental version will be deleted, without affecting documents in the knowledge base or other versions. |


<span id="516e13f5"></span>
# **Response message**


|**Parameter** |**Parameter description** |
|---|---|
|code |Status code |
|message |Return message |
|request_id |Unique identifier for each request |


<span id="56234951"></span>
## **Status code description**


|**Status code** |**HTTP status code** |**Return message** |**Status code description** |
|---|---|---|---|
|0 |200 |success |Success |
|1000001 |401 |unauthorized |Authentication failed |
|1000002 |403 |no permission |Insufficient permissions |
|1000003 |400 |invalid request：%s |Invalid parameter |
|1000005 |400 |collection not exist |Collection does not exist |
|1001001 |400 |doc not exist |Document does not exist |


<span id="bb888a2c"></span>
# Complete example

<span id="2e4a5e79"></span>
## Request message

```Shell
curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-knowledgebase.mlp.cn-hongkong.bytepluses.com/api/knowledge/doc/delete  \
  -d '{
    "collection_name": "test_collection_name",
    "project": "",
    "doc_id": "test123"
}'
```


<span id="e241b1fa"></span>
## Response message

Return on successful execution:

```Shell
HTTP/1.1 200 OK
Content-Length: 43
Content-Type: application/json
 
{"code":0,"message":"success","request_id":"021695029537650fd001de666660000000000000000000230da93"}
```


Return on failed execution:

```Shell
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000003, "message":"invalid request：%s", "request_id": "021695029757920fd001de6666600000000000000000002569b8f"}
```
