---
title: "drop"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/drop1"
---

<span id="3922736a"></span>
# Overview

The /index/drop API endpoint allows you to delete a specified index from a collection in your VikingDB instance.

<span id="320e4a50"></span>
# **request interface**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you need to construct a signature for authentication. For detailed OpenAPI signature calling methods, please refer to <a href="https://docs.byteplus.com/en/docs/VikingDB/Preparation">API Signature Call Guide</a>.</div>



|**URI** |/api/index/drop |Uniform Resource Identifier |
|---|---|---|
|**request method** |POST |The type of operation requested by the client on the vector database server |
|**request header** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="af8d0b90"></span>
# **request parameters**


|**parameter** |**type** |**Is it required?**  |**parameter description** |
|---|---|---|---|
|collection_name |String |Yes |The name of the collection containing the index to delete.<br><br><br>* Must begin with an English letter and can only contain English letters, numbers, and underscores (_).<br><br>* Length requirements: [1,128].<br><br>* Collection names must be unique. |
|index_name |String |Yes |The name of the index to delete.<br><br><br>* Must begin with an English letter and can only contain English letters, numbers, and underscores (_).<br><br>* Length requirements: [1,128].<br><br>* Index names must be unique. |


<span id="120c255f"></span>
# **response message**


|**parameter** |**parameter description** |
|---|---|
|Code |Status code |
|Message |Description |
|request_id |A unique identifier for the request. |


<span id="75ec5873"></span>
## **status code description**


|**status code** |**HTTP status code** |**Return information** |**status code description** |
|---|---|---|---|
|0 |200 |Drop index success |Deleted index successfully. |
|1000008 |400 |Index not exists |The specified index does not exist. |
|1000003 |400 |Invalid request:% s |Invalid parameter:<br><br><br>* Required parameters are missing. |
|1000001 |401 |Unauthorized |The request header lacks authentication information. |
|1000002 |403 |No permission |Insufficient permissions. |


<span id="38eeaace"></span>
# Complete example

<span id="039acbcd"></span>
## Request message

```Shell

curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-vikingdb.mlp.ap-mya.byteplus.com/api/index/drop \
  -d '{
    "collection_name": "test_name",
    "index_name": "index_test"
}'
```


<span id="c8ce70cf"></span>
## Response message

On success, the following response is returned:

```Shell
HTTP/1.1 200 OK
Content-Length: 43
Content-Type: application/json
 
{
    "code":0,
    "message":"success",
    "request_id":"021695029757920fd001de6666600000000000000000002569b8f" 
}
```


On failure, the following response is returned:

```Shell
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000008, "message":"index not exist", "request_id":"021695029757920fd001de6666600000000000000000002569b8f"}
```
