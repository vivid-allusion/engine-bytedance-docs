---
title: "drop"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/drop"
---

<span id="0867c2b4"></span>
# Overview

To permanently delete a collection, you can use the /collection/drop interface. This document provides the API reference for this operation. Please note that this action is irreversible and requires you to delete all associated indexes before the collection can be successfully dropped.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">This operation permanently deletes all data in the specified collection. Please proceed with caution.</div>


* <div data-tips="true" data-tips-type="warning">Before deleting a collection, you must delete all of its associated indexes.</div>



<span id="55b7428d"></span>
# **request interface**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you need to construct a signature for authentication. For detailed instructions on generating API signatures, refer to <a href="https://docs.byteplus.com/en/docs/VikingDB/Preparation">API Signature Call Guide</a>.</div>



|**URI** |/api/collection/drop |Uniform Resource Identifier |
|---|---|---|
|**request method** |POST |The type of operation requested by the client side on the vector database server |
|**request header** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="87256a9b"></span>
# **request parameters**


|**parameter** |**type** |**Required** |**Description** |
|---|---|---|---|
|collection_name |String |Yes |Specify the name of the Collection to delete.<br><br><br>* Must contain only English letters, numbers, and underscores (_), begin with an English letter, and not be empty.<br><br>* Length requirements: [1,128].<br><br>* Collection names must be unique. |


<span id="0006691a"></span>
# **response message**


|**parameter** |**Description** |
|---|---|
|Code |Status code |
|Message |Message |
|request_id |A unique identifier for the request |


<span id="e200af10"></span>
## **status code description**


|**status code** |**HTTP status code** |**Result message** |**status code description** |
|---|---|---|---|
|0 |200 |Success |The collection was deleted successfully. |
|1000006 |400 |Operation not allowed: associated indexes exist |The collection cannot be deleted because it still has associated indexes. |
|1000003 |400 |Invalid request:% s |Invalid parameter:<br><br><br>* Collection not specified. |
|1000001 |401 |Unauthorized |The request header lacks authentication information. |
|1000002 |403 |No permission |Insufficient permissions. |


<span id="92e1f314"></span>
# Complete example

<span id="04cd0a89"></span>
## Request message

```Shell

curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-vikingdb.mlp.ap-mya.byteplus.com/api/collection/drop \
  -d '{
    "collection_name": "test_name"
}'
```


<span id="b9db4e82"></span>
## Response message

Successful execution returns:

```Go
HTTP/1.1 200 OK
Content-Length: 43
Content-Type: application/json
 
{"code":0,"msg":"success","request_id":"021695029537650fd001de666660000000000000000000230da93"}
```


If execution fails, the response is:

```Go
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000006,"msg":"associated indexes exist","request_id":"021695029537650fd001de666660000000000000000000230da93"}
```
