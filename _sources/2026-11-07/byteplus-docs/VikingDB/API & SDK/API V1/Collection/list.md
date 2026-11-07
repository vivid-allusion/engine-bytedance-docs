---
title: "list"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/list1"
---

<span id="a8ef7886"></span>
# Overview

/collection/list interface is used to query the Collection list of datasets.

<span id="00a86c72"></span>
# **Request interface**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you need to construct a signature for authentication. For detailed OpenAPI signature calling methods, please refer to <a href="https://docs.byteplus.com/en/docs/VikingDB/Preparation">API Signature Call Guide</a>.</div>



|**URI** |/api/collection/list |Uniform Resource Identifier |
|---|---|---|
|**request method** |GET |The type of operation requested by the client side on the vector database server |
|**request header** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="c62e8351"></span>
# **request parameters**

None.

<span id="f77d87f0"></span>
# **response message**


|**parameter** |**parameter description** |
|---|---|
|Code |Status code |
|Message |Return information |
|request_id |A unique identifier for each request |
|Data |A list of collection details. For the fields in each collection, see the **Collection parameters section.**  |


<span id="c6560502"></span>
## Collection parameters


|**parameter** |**sub\-parameter** |**type** |**parameter description** |
|---|---|---|---|
|collection_name |*  |String |The name of the collection. |
|Description |*  |String |A description of the collection. |
|primary_key |*  |String |The name of the field designated as the primary key. The field type must be `int64` or `string`. |
|Fields |field_name |String |The name of a custom field. |
||field_type |String |Displays custom field types, optional values include int64, float32, string, bool, list< string \>, list< int64 \>, vector, sparse_vector, text. If you include a text field, you cannot also include a vector or sparse_vector field. |
||default_val |Consistent with field_type |The default value for the custom field. |
||dim |Int |Display custom field vector dimensions. |
||pipeline_name |*  |Plain text. |
|index_names |*  |Array |A list of index names associated with the collection. |
|index_num |*  |Int |The number of indexes associated with the collection. |
|create_time |*  |String |Collection creation time. |
|update_time |*  |String |Collection update time. |
|update_person |*  |String |Collection updater. |


<span id="70d4b39b"></span>
## **status code description**


|**status code** |**HTTP status code** |**Return information** |**status code description** |
|---|---|---|---|
|0 |200 |Success |Collection list was successfully queried. |
|1000001 |401 |Unauthorized |The request header lacks authentication information. |
|1000002 |403 |No permission |Insufficient permissions. |


<span id="4d74c08d"></span>
# Complete example

<span id="7ecd6f9d"></span>
## Request message

```Shell

curl -i -X GET \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-vikingdb.mlp.ap-mya.byteplus.com/api/collection/list \
```


<span id="c53ac6dc"></span>
## Response message

Successful execution returns:

```Shell
HTTP/1.1 200 OK
Content-Length: 43
Content-Type: application/json
 
{
    "code":0,
    "message":"success",
    "request_id":"021695029748777fd001de6666600000000000000000002887b8d",
    "data": [
        {
            "collection_name": "test_name",
            "description": "test dataset",
            "primary_key": "id", 
            "fields": [                               
                {
                    "field_name": "id",       
                    "field_type": "int64"
                },
                {
                    "field_name": "text",                     
                    "field_type": "string", 
                    "default_val": ""
                },
                {
                    "field_name": "vector_field",
                    "field_type": "vector",      
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
                "index1",
                "index2"
            ]
        "index_num": 2,            
        "create_time": "2023-11-21 12:22:57",
        "update_time": "2023-11-22 11:15:45",
        "update_person": "zhangsan"
        },
        {
            "collection_name": "test_name2",
            "descript": "test dataset 2",
            "primary_key": "id",
            "fields": [                               
                {
                    "field_name": "id",       
                    "field_type": "int64"
                }
                {
                    "field_name": "vector_field",
                    "field_type": "vector",      
                    "dim": 768
                }
            ]
            "index_names": [
                "index3",
                "index4"
            ]
        "index_num": 2,
        "create_time": "2023-11-21 10:22:57",
        "update_time": "2023-11-22 11:15:45",
        "update_person": "zhangsan"
        }
    ]
}
```


Example of a failed execution:

```Shell
HTTP/1.1 401 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000001,"message":"unauthorized","request_id":"021695029748777fd001de666660000000000000
```
