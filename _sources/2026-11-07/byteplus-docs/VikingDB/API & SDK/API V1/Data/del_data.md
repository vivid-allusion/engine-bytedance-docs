---
title: "del_data"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/del_data"
---

<span id="3929a1d7"></span>
# Overview

Use the /collection/del_data endpoint to delete data from a specified collection. This endpoint supports two deletion methods: you can delete one or more entries by their primary keys (up to 100 at a time), or you can delete all data within the collection entirely. Note that there may be a short delay before the deletion is reflected in the index.

Deleting data supports the following methods:


1. Delete one or more data entries in a specified collection by primary key. You can delete up to 100 entries at a time.

2. Delete all data in the specified collection.


<span id="d3fb581c"></span>
# **Request**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you need to construct a signature for authentication. For detailed OpenAPI signature calling methods, please refer to <a href="https://docs.byteplus.com/en/docs/VikingDB/Preparation">API Signature Call Guide</a>.</div>



|**URI** |/api/collection/del_data |Uniform Resource Identifier |
|---|---|---|
|**request method** |POST |The type of operation requested by the client on the vector database server. |
|**request header** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="0b43f8df"></span>
# **Request parameters**


|**parameter** |**type** |**Required** |**parameter description** |
|---|---|---|---|
|collection_name/collection_alias |String |Yes |Specifies the Collection name/alias for deleting data.<br><br><br>* Must contain only English letters, numbers, and underscores (_). It must begin with an English letter and cannot be empty.<br><br>* Length: 1–128 characters<br><br>* Collection names/aliases cannot be duplicated. |
|primary_keys |Int 64,<br><br>Array\ < int64 \>,<br><br>String,<br><br>Array\ < string \> |Conditionally required |Specify the primary keys of the data to delete. You can specify up to 100 keys at a time. Depending on the type of primary_keys, the data deletion logic is as follows:<br><br><br>* **int64 type**,**String type**: Deletes a single data entry.<br><br>* **Array< int64 \>** ,**Array< string \>** : Deletes multiple data entries. The number of entries is the length of the array, with a maximum of 100. |
|del_all |Bool ||If set to true, all data is deleted. The default value is false. |


<span id="7173cb67"></span>
# **Response**


|**parameter** |**parameter description** |
|---|---|
|Code |Status code |
|Message |Description |
|request_id |A unique identifier for the request. |


<span id="993d2f9f"></span>
## **Status code descriptions**


|**status code** |**HTTP status code** |**Return information** |**status code description** |
|---|---|---|---|
|0 |200 |Success |Data was deleted successfully from the specified collection. |
|1000005 |400 |Collection does not exist |Collection does not exist. |
|1000003 |400 |Invalid request:% s |Invalid parameter:<br><br><br>* Required parameters are missing.<br><br>* The primary key field value is missing. |
|1000001 |401 |Unauthorized |The request header lacks authentication information. |
|1000002 |403 |No permission |Insufficient permissions. |


<span id="8a4e5204"></span>
# Complete example

<span id="21b5dc21"></span>
## Request message

```Shell

curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-vikingdb.mlp.ap-mya.byteplus.com/api/collection/del_data \
  -d '{
    "collection_name": "test_name",
    "primary_keys": [                               
        123,     
        124    
    ]
}'
```


<span id="ae94e903"></span>
## Response message

A successful request returns the following:

```Shell
HTTP/1.1 200 OK
Content-Length: 43
Content-Type: application/json
 
{
    "code":0,
    "msg":"success",
    "request_id":"021695029736548fd001de66666000000000000000000029aa917"
}
```


A failed request returns the following:

```Shell
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1,"msg":"collection not exist","request_id":"021695029736548fd001de66666000000000000000000029aa917"}
```
