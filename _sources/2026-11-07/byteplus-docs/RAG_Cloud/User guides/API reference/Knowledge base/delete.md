---
title: "delete"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/collection_delete"
---

This section describes how to delete an existing knowledge base.

<span id="efea38b3"></span>
# Overview

The `/api/knowledge/collection/delete` endpoint is used to delete an existing knowledge base.

<span id="bd0e2a1a"></span>
# **Prerequisites**

After completing account registration, identity verification, AK/SK key acquisition, and signature generation on the 'Signature Authentication Method' page, you can call the API endpoint to delete a knowledge base.

<span id="3adee4bc"></span>
# **Request endpoint**


|**URI** |/api/knowledge/collection/delete |Uniform resource identifier |
|---|---|---|
|**Request method** |POST |Operation type requested by the client to the vector database server |
|**Request headers** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="05690202"></span>
# **Request parameters (applicable to both Pro version and Standard version)** 


|**Parameter** |**Type** |**Required** |**Default value** |**Parameter description** |
|---|---|---|---|---|
|name |string |No |\-\- |**Knowledge base name** |
|project |string |No |default |**Project to which the knowledge base belongs**<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If this field is not specified, the operation will be performed on the knowledge base under the default project.</div><br><br><br><div data-tips="true" data-tips-type="warning">To operate on a knowledge base under a specified project, this field must be configured correctly.</div><br> |
|resource_id |string |No |\-\- |**Unique knowledge base ID**<br><br>You can choose to pass resource_id directly, or pass both name and project as the unique identifier of the knowledge base. |


<span id="1158d1c7"></span>
# **Response message**


|**Parameter** |**Parameter description** |
|---|---|
|code |Status code |
|message |Return message |
|request_id |Unique identifier for each request |


<span id="10e1bfa9"></span>
## **Status code description**


|**Status code** |**HTTP status code** |**Return message** |**Status code description** |
|---|---|---|---|
|0 |200 |success |Success |
|1000001 |401 |unauthorized |Authentication failed |
|1000002 |403 |no permission |Insufficient permissions |
|1000003 |400 |invalid request: %s |Invalid parameter |
|1000005 |400 |collection not exist |Collection does not exist |


<span id="81af4114"></span>
# Complete example

<span id="735f1dfd"></span>
## Request message

```Shell
curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-knowledgebase.mlp.cn-hongkong.bytepluses.com/api/knowledge/collection/delete \
  -d '{
    "name": "test_collection_name",
    "project": ""
}'
```


<span id="17f6d465"></span>
## Response message

Successful execution returns:

```Shell
HTTP/1.1 200 OK
Content-Length: 43
Content-Type: application/json
 
{"code":0,"message":"success","request_id":"021695029537650fd001de666660000000000000000000230da93"}
```


Failed execution returns:

```Shell
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000003, "message":"invalid request: %s", "request_id": "021695029757920fd001de6666600000000000000000002569b8f"}
```
