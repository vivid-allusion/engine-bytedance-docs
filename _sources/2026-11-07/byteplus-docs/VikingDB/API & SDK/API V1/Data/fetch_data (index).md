---
title: "fetch_data (index)"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/fetch_data_index"
---

<span id="bb5f3ce8"></span>
# Function introduction

To retrieve specific data entries from a vector index, you can use the `/index/fetch_data` interface. This allows you to query for single or multiple data points by their primary keys, with a limit of 100 entries per request.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Please note that there may be a data update latency of up to 20 seconds after a write or delete operation.</div>


<span id="21cee722"></span>
# **API request**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you need to construct a signature for authentication. For detailed instructions on signing OpenAPI requests, please refer to <a href="https://docs.byteplus.com/en/docs/VikingDB/Preparation">API Signature Call Guide</a>.</div>



|**URI** |/api/index/fetch_data |Uniform Resource Identifier |
|---|---|---|
|**request method** |GET |The type of operation requested by the client on the vector database server |
|**request header** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="94e10a5b"></span>
# **request parameters**


|**parameter** |**type** |**Required?**  |**parameter description** |
|---|---|---|---|
|collection_name/collection_alias |String |Yes |The name or alias of the collection to query.<br><br><br>* Can contain only English letters, numbers, and underscores (_). Must begin with an English letter and cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Collection names and aliases must be unique. |
|index_name |String |Yes |The name of the index to query.<br><br><br>* Can contain only English letters, numbers, and underscores (_). Must begin with an English letter and cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Index names must be unique. |
|primary_keys |Int 64,<br><br>Array\ < int64 \>,<br><br>String,<br><br>Array\ < string \> |Yes |The primary key value(s) of the records to query. You can query up to 100 records at a time. The query logic differs based on the type of the primary_keys parameter:<br><br><br>* **Int 64 type, string type**: For a single record query.<br><br>* **Array< int64 \>, array\ < string \>** : For multiple record queries. The number of records is the length of the array, with a maximum of 100. |
|Partition |Int64/string |No |The partition name. The type of this parameter must match the type of the partition key field, and its value must match a value of the partition key field.<br><br><br>* If the partition key's field_type is int64 or list, the partition input type is int64.<br><br>* field_type string, list\ < string \>, partition input type is string, format requirements "^[a\-zA\-Z0\-9_\-]+$"<br><br><br>If this parameter is not set, it defaults to "default". |
|output_fields |List\ < string \> |No |A list of scalar fields to return. This filters the fields in the response.<br><br><br>* If output_fields is not passed, all scalar fields are returned.<br><br>* If output_fields is an empty list, the fields field is not returned.<br><br>* If output_fields has a formatting error or contains a field that is not in the collection, the interface returns an error. |


<span id="cc81f3f0"></span>
# **Response body**


|**parameter** |**parameter description** |
|---|---|
|Code |Status code |
|Message |A message describing the result of the request. |
|request_id |A unique identifier for each request |
|Data |Returns the data for the query.<br><br><br>* If a single record is queried, the type is a map. If multiple records are queried in a batch, the type is an array of maps. If a record cannot be found, only its primary key value and a message are returned.<br><br>* Each record is represented as a map, where the keys are field names and the values are the corresponding field values. |


<span id="b69251f0"></span>
## **status code description**


|**status code** |**HTTP status code** |**Return information** |**status code description** |
|---|---|---|---|
|0 |200 |Success |Successfully queried data from the specified index. |
|1000008 |400 |Index does not exist |Index does not exist. |
|1000003 |400 |Invalid request:% s |Invalid parameter:<br><br><br>* Required parameters are missing. |
|1000001 |401 |Unauthorized |The request header lacks authentication information. |
|1000002 |403 |No permission |Insufficient permissions. |


<span id="322fda0e"></span>
# Complete example

<span id="f4f77ebe"></span>
## Request message

```Shell

curl -i -X GET \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-vikingdb.mlp.ap-mya.byteplus.com/api/index/fetch_data \
  -d '{
    "collection_name": "test_name",
    "primary_keys": [123,456],    
    "output_fields": ["time", "author", "vector_field"]
}'
```


<span id="c65115a0"></span>
## Response message

Successful execution returns:

```Shell
HTTP/1.1 200 OK
Content-Length: 43
Content-Type: application/json
 
{
    "code":0,
    "msg":"fetch data success",
    "request_id":"021695029537650fd001de666660000000000000000000230da93",
    "data": [
        {
            "id": "123",
            "vector": [0.10, 0.13.........0.52],
            "dimension": 768,
            "fields": [
                "time": 1690529701,
                "author": "zhangsan",
                "vector_field": [0.10, 0.13.........0.52]
            ]
        },
        {
            "id": "456",
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
 
{"code": 1000008, "msg": "index not exist", "request_id":"021695029537650fd001de666660000000000000000000230da93"}
```
