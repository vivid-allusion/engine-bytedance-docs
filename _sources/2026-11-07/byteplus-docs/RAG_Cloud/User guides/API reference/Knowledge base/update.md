---
title: "update"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/collection_update"
---

The `/api/knowledge/collection/update` endpoint allows you to programmatically modify an existing knowledge base. This API supports updating the description, CPU quota, and document tags (fields), though available parameters may differ by subscription plan. Note that any update to document tags will overwrite the entire existing set.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Currently, only updating the description, cpu_quota, and fields (document tags) of the knowledge base is supported.</div>


   * <div data-tips="true" data-tips-type="tip">The pro version supports modifying description, cpu_quota, and fields (document tags).</div>


   * <div data-tips="true" data-tips-type="tip">The standard version only supports modifying description.</div>


* <div data-tips="true" data-tips-type="tip">After you update the fields (document tags) using the collection/update API, the frontend automatically synchronizes with the updated content, overwriting the existing tags.</div>



<span id="d1c25fa4"></span>
# Overview

The `/api/knowledge/collection/update` API is used to update knowledge base information.

<span id="356f86ef"></span>
# **Prerequisites**

To call this API, you must first complete account registration, real\-name authentication, AK/SK key acquisition, and signature acquisition on the "Signature Authentication Method" page.

<span id="43f31085"></span>
# **Request API**


|**URI** |/api/knowledge/collection/update |Uniform resource identifier |
|---|---|---|
|**Request method** |POST |Type of operation requested by the client to the vector database server |
|**Request header** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="65721e04"></span>
# **Request parameters (pro version)** 


|**Parameter** |**Type** |**Required** |**Default value** |**Parameter description** |
|---|---|---|---|---|
|name |string |No |\-\- |**Knowledge base name** |
|project |string |No |default |**Project to which the knowledge base belongs**<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If this field is not specified, it will be created under the default project.</div><br><br><br><div data-tips="true" data-tips-type="warning">To perform operations on a knowledge base in a specific project, specify the project name in this parameter.</div><br> |
|resource_id |string |No |\-\- |**Knowledge base ID**<br><br>You can identify the knowledge base by providing either the resource_id or a combination of the name and project. |
|description |string |No |\-\- |**Knowledge base description**<br><br><br>* Length requirement: [1, 65535] |
|cpu_quota |int |No |\-\- |**CPU quota** |
|fields |list |No |\-\- |**Document tags**<br><br>This operation overwrites all existing tags. For example, if a knowledge base has tags A,B, and C: \* To add tag D, you must provide A,B,C, and D in the update request. \* To delete tag A, you must provide B and C in the update request.<br><br><br>* To add document tag D, update should include A, B, C, and D.<br><br>* To delete document tag A, update should include B, C, and D.<br><br><br>```Plain```<br>```[```<br>```  {```<br>```    "field_name": "xxx" //Document tag name```<br>```    "field_type": "xxx" //Document tag type```<br>```    "default_val": xxxx //Document tag value```<br>```  },```<br>```]```<br> |


<span id="ecc0bd4d"></span>
# Request parameters (standard version)


|**Parameter** |**Type** |**Required** |**Default value** |**Parameter description** |
|---|---|---|---|---|
|name |string |No |\-\- |**Knowledge base name** |
|project |string |No |default |**Project to which the knowledge base belongs**<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If this field is not specified, it will be created under the default project.</div><br><br><br><div data-tips="true" data-tips-type="warning">To perform operations on a knowledge base in a specific project, specify the project name in this parameter.</div><br> |
|resource_id |string |No |\-\- |**Knowledge base ID**<br><br>You can identify the knowledge base by providing either the resource_id or a combination of the name and project. |
|description |string |No |\-\- |**Knowledge base description**<br><br><br>* Length requirement: [1, 65535] |


<span id="8945c08f"></span>
# **Response message**


|**Parameter** |**Parameter description** |
|---|---|
|code |Status code |
|message |Return message |
|request_id |Unique identifier for each request |


<span id="828f6bf7"></span>
## **Status code description**


|**Status code** |**HTTP status code** |**Return message** |**Status code description** |
|---|---|---|---|
|0 |200 |success |Success |
|1000001 |401 |unauthorized |Authentication failed |
|1000002 |403 |no permission |Insufficient permissions |
|1000003 |400 |invalid request: %s |Invalid parameter |
|1000005 |400 |Collection does not exist |Collection does not exist |


<span id="36dc6145"></span>
# Complete example

<span id="5befe250"></span>
## Request message

```Shell
curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-knowledgebase.mlp.cn-hongkong.bytepluses.com/api/knowledge/collection/update \
  -d '{
    "name": "test_collection_name",
    "project": "",
    "description": "This is a test knowledge base",
    "cpu_quota": 1
}'
```


<span id="91d1171a"></span>
## Response message

Return on success:

```Shell
HTTP/1.1 200 OK
Content-Length: 43
Content-Type: application/json
 
{"code":0,"message":"success","request_id":"021695029537650fd001de666660000000000000000000230da93"}
```


Return on failure:

```Shell
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000003, "message":"invalid request: %s", "request_id": "021695029757920fd001de6666600000000000000000002569b8f"}
```
