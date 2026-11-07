---
title: "info"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/info"
---

<span id="cf0239f0"></span>
# Overview

To retrieve the complete configuration and status of a specific collection, you can use the /api/collection/info endpoint. This API returns comprehensive details, including the collection's schema, primary key, field definitions, associated indexes, and statistics like data count and storage size.

<span id="c1616cf7"></span>
# **request interface**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you need to construct a signature for authentication. For detailed information on how to use API signatures, please refer to <a href="https://docs.byteplus.com/en/docs/VikingDB/Preparation">API Signature Call Guide</a>.</div>



|**URI** |/api/collection/info |Uniform Resource Identifier |
|---|---|---|
|**method** |GET |The type of operation requested by the client side on the vector database server |
|**request header** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="96abbbf1"></span>
# **request parameters**


|**parameter** |**type** |**Required** |**parameter description** |
|---|---|---|---|
|collection_name/collection_alias |String |Yes |Specifies the Collection name/alias for the query.<br><br><br>* Must start with an English letter and can only contain English letters, numbers, and underscores (_). The value cannot be empty.<br><br>* Length requirements: [1,128]. |


<span id="635e6040"></span>
# **response message**


|**parameter** |**parameter description** |
|---|---|
|Code |Status code |
|Message |Message |
|request_id |A unique identifier for each request |
|Data |Collection details. For more information, see the "Collection parameters" section. |


<span id="d0d3fc94"></span>
## Collection parameters


|**parameter** |**sub\-parameter** |**type** |**parameter description** |
|---|---|---|---|
|collection_name |\-\- |String |The name of the queried Collection. |
|Description |\-\- |String |The description of the queried Collection. |
|collection_aliases |\-\- |Array |A list of aliases for the Collection. |
|primary_key |\-\- |String |The name of the primary key field. This must correspond to a `field_name` in the `Fields` array. The field type of the primary key must be of type int64/string. |
|Fields |field_name |String |Displays the name of the custom field. |
||field_type |String |Displays the type of the custom field. Valid values are `int64`, `float32`, `string`, `bool`, `list<string>`, `list<int64>`, `vector`, `sparse_vector`, and `text`. If `text` is used, the field is bound to a text processing pipeline, and the Collection cannot contain `vector` or `sparse_vector` fields. |
||default_val |Consistent with field_type |Displays the default value for the custom field. |
||dim |Int |Displays the dimension of the vector field. |
||pipeline_name |\-\- |The name of the pipeline to use for a field of type `text`. |
|Stat |data_number |Number |The number of records, note:<br><br><br>* Non\-real\-time statistics.<br><br>* This value is updated only after data is written and the corresponding index is created. |
||data_storage |Number |Data storage size (in bytes), note:<br><br><br>* Non\-real\-time statistics.<br><br>* This value is updated only after data is written and the corresponding index is created. |
|index_names |\-\- |Array |Displays a list of index names associated with the Collection. |
|index_num |\-\- |Int |Displays the number of indexes associated with the Collection. |
|create_time |\-\- |String |Collection creation time. |
|update_time |\-\- |String |Collection update time. |
|update_person |\-\- |String |The user who last updated the Collection. |


<span id="03d9ad05"></span>
## **status code description**


|**status code** |**HTTP status code** |**Message** |**status code description** |
|---|---|---|---|
|0 |200 |Get collection success |The request was successful. |
|1000005 |404 |Collection does not exist |Collection does not exist. |
|1000003 |400 |Invalid request: %s |Invalid parameter:<br><br><br>* Required parameters are missing. |
|1000001 |401 |Unauthorized |The request header lacks authentication information. |
|1000002 |403 |No permission |Insufficient permissions. |


<span id="c2ad4637"></span>
# Complete example

<span id="b3c5d39a"></span>
## Request message

```Shell

curl -i -X GET \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-vikingdb.mlp.ap-mya.byteplus.com/api/collection/info \
  -d '{
    "collection_name": "test_name",
}'
```


<span id="d05caf12"></span>
## Response message

Successful execution returns:

```Shell
HTTP/1.1 200 OK
Content-Length: 43
Content-Type: application/json
 
{
    "code":0,
    "message":"success",
    "request_id":"021695029537650fd001de666660000000000000000000230da93",
    "data": {
        "collection_name": "test_name",
        "description": "test dataset",
        "primary_key": "id", 
        "fields": [                               
            {
                "field_name": "id",       
                "field_type": "int64"
            },
            {
                "field_name":"text",                     
                "field_type": "string", 
                "default_val": ""
            },
            {
                "field_name": "vector_field",
                "field_type": "dense_vector",      
                "dim": 768
            },
            {
                "field_name": "sparse_vector_field",
                "field_type": "sparse_vector"
            },
            {
                "field_name": "time",
                "field_type": "int64",       
                "default_val": 0
            },
            {
                "field_name": "author",
                "field_type": "string",      
                "default_val": "null"
            }
        ]
        "index_names": [
            "test_index",
            "test_index_1"
        ],
        "index_num": 2,
        "stat":{"data_number":20,"data_storage":2440}
        "create_time": "2023-11-21 12:22:57",
        "update_time": "2023-11-22 11:15:45",
        "update_person": "zhangsan"        
    }
}
```


Example failure response:

```Shell
HTTP/1.1 404 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000005, "msg":"collection not exist", "request_id":"021695029537650fd001de666660000000000000000000230da93"}
```
