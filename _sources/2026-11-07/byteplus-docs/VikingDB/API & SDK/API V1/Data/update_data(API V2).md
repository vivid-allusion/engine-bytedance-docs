---
title: "update_data(API V2)"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/update_data"
---

<span id="e9f2879d"></span>
# Overview

To update specific fields of existing data in a collection, use the /collection/update_data interface. This API reference explains how to call this endpoint, which supports updates for text, scalar, and vector field types.

<span id="b7e439ad"></span>
# **Request interface**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you need to construct a signature for authentication. For detailed OpenAPI signature calling methods, please refer to <a href="https://docs.byteplus.com/en/docs/VikingDB/Preparation">API Signature Call Guide</a>.</div>



|**URI** |/api/collection/update_data |Uniform Resource Identifier |
|---|---|---|
|**request method** |POST |The type of operation requested by the client on the vector database server |
|**request header** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="f56746df"></span>
# **Request parameters**


|Parameter name |Type |Required |Note |
|---|---|---|---|
|collection_name/collection_alias |String |Yes |Collection name |
|Fields |Array < map \> |Yes |The number of data entries in a single write operation cannot exceed 100 (considering performance issues)<br><br>Each data entry is a map where the key is the field name and the value is the field value. The value formats for different field types are as follows:<br><br><br>* Int 64: The format is an integer value.<br><br>* Float: The format is a floating\-point value.<br><br>* String: The format is string.<br><br>* Bool: The format is true/false.<br><br>* List < string \>: The format is a string array.<br><br>* List < int64 \>: The format is an integer array.<br><br>* Vector: The format is vector (array of floating\-point numbers).<br><br>* sparse_vector: The format is a JSON object, where the key (k) is a string that represents the keyword literal, and the value (v) is a float that represents the keyword's weight.<br><br>* Text: The format is string.<br><br>* Image: Currently, only TOS paths are supported for image fields. The format is`tos://{bucket}/{object_key}`. |
|||||
|TTL |Int 64 |No |The Time\-to\-Live (TTL) for the updated data. |
|need_token_usage |Bool |No |Returns token consumption information |


<span id="65a0acfd"></span>
# **Response message**


|**parameter** |**parameter description** |
|---|---|
|Code |Status code |
|Message |Return information |


<span id="c734e0c4"></span>
## **Status code description**


|Code |Message |Note |HTTP status code |
|---|---|---|---|
|0 |Success |Success |200 |
|1000005 |Collection does not exist |Collection does not exist |400 |
|1000003 |Invalid request |Illegal parameter<br><br><br>* Missing required parameters<br><br>* Field value does not match field type |400 |
|1000001 |Unauthorized |Lack of authentication information |401 |
|1000002 |No permission |Insufficient permissions |403 |
|1000011 |Data not found |Data does not exist |400 |


<span id="f8fe28c1"></span>
# Complete example

<span id="e9c788d7"></span>
## Request message

```Shell
curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-vikingdb.mlp.ap-mya.byteplus.com/api/collection/update_data \
  -d '{
    "collection_name": "test_collection",
    "fields": [
        {
            "id": 1,
            "author": "Updated Author Name",
        },
    ],
}'
```


<span id="d5d8721d"></span>
## Response message

Successful execution returns:

```Shell
HTTP/1.1 200 OK
Content-Length: 43
Content-Type: application/json
 
{"code":0,"message":"success"}
```


A failed execution returns the following:

```Shell
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000011,"message":"primary key 2 data not exist","request_id":"02173469631705400000000000000000000ffff0a006429651395"}
```
