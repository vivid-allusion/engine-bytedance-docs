---
title: "fetch_data (collection)"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/fetch_data_collection"
---

<span id="d170497e"></span>
# Overview

To query single or multiple data entries from a specified collection, use the /collection/fetch_data interface. You can retrieve up to 100 entries at a time by providing their primary keys.

After data in a collection is written or deleted, it can be queried in real time.

<span id="b2a5827f"></span>
# **Request interface**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you need to construct a signature for authentication. For details on how to generate API signatures, refer to <a href="https://docs.byteplus.com/en/docs/VikingDB/Preparation">API Signature Call Guide</a>.</div>



|**URI** |/api/collection/fetch_data |Uniform Resource Identifier |
|---|---|---|
|**request method** |GET |The type of operation requested by the client on the vector database server |
|**request header** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="262641ab"></span>
# **request parameters**


|**parameter** |**type** |**Required?**  |**Description** |
|---|---|---|---|
|collection_name/collection_alias |String |Yes |Specifies the Collection name/alias for the query data.<br><br><br>* Must begin with an English letter and contain only English letters, numbers, and underscores (_). It cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Collection names/aliases cannot be duplicated. |
|primary_keys |Int 64,<br><br>Array\ < int64 \>,<br><br>String,<br><br>Array\ < string \>, |Yes |Specify the primary key field value to query up to 100 pieces of data at a time. The query logic varies depending on the type of primary_keys:<br><br><br>* **int64 type**,**String type**: Single data query, also supports multiple text slice data queries corresponding to the primary key.<br><br>* **Array\ < int64 \>** ,**Array\ < string \>** : Multiple data queries, the number of data bars is the length of the outer array, the maximum is 100. |


<span id="4be1ae96"></span>
# **Response message**


|**parameter** |**parameter description** |
|---|---|
|Code |Status code |
|Message |Message |
|request_id |A unique identifier for the request. |
|Data |Returns the data for the query.<br><br><br>* If a single item is queried, the type is a map. If multiple items are queried in a batch, the type is an array of maps. If an item cannot be found, only its primary key and a message are returned.<br><br>* Each data item is a map where the key is the field name and the value is the field value. |


<span id="33cd6bf3"></span>
## **Status code description**


|**status code** |**HTTP status code** |**Message** |**status code description** |
|---|---|---|---|
|0 |200 |Success |The data query for the specified Collection was successful. |
|1000005 |400 |Collection does not exist |Collection does not exist. |
|1000003 |400 |Invalid request:% s |Illegal parameter<br><br><br>* Required parameters are missing. |
|1000001 |401 |Unauthorized |The request header lacks authentication information. |
|1000002 |403 |No permission |Insufficient permissions. |


<span id="d377acd5"></span>
# Complete example

<span id="0f6994a3"></span>
## Request message

```Shell

curl -i -X GET \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-vikingdb.mlp.ap-mya.byteplus.com/api/collection/fetch_data \
  -d '{
    "collection": "test_name",
    "primary_keys": [123,124]                              
}'
```


<span id="d5ddec86"></span>
## Response message

Successful execution returns:

```Shell
HTTP/1.1 200 OK
Content-Length: 43
Content-Type: application/json
 
{
    "code":0,
    "msg":"fetch data success",
    "request_id":"021695029748777fd001de6666600000000000000000002887b8d",
    "data": [
        {
            "id": "123",
            "text": "hello world!",
            "vector_field": [0.10, 0.13.........0.52],
            "sparse_vector_field": {"hello": 0.34, "world": 0.03, "!": 0.11},
            "time": "1690529701",
            "author": "zhangsan"
        },
        {
        "id": "124",
          // If no data is queried, no vector but a message will be returned. 
            "message": "no data found"
        }  
    ]
}
```


Sample error response:

```Shell
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code": 1000005, "msg": "collection not exist", "request_id":"021695029748777fd001de6666600000000000000000002887b8d"}
```
