---
title: "Vector Search"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Vector_Search"
---

<span id="fbbd21af"></span>
## Overview

To find the K\-nearest neighbors for a target vector within your dataset, you can use the `/api/index/search` endpoint. This API reference provides detailed information on how to perform vector searches, including request parameters, body structure, and complete examples.

Vector Nearest Neighbor Retrieval is a retrieval method based on vector space model, which searches by calculating the similarity between vectors. In a given vector dataset, vector nearest neighbor search uses a time\- and space\-efficient data structure built from vectors according to certain metrics (such as inner product, Euclidean distance), which can efficiently retrieve K vectors similar to the target vector.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After data in a collection is written or deleted, there can be a lag of up to 20 seconds for the index to update. Consequently, changes may not be immediately reflected in search results.</div>


<span id="c669f8db"></span>
# **Prerequisites**


* When the collection is created, the vector field must be included in the field definitions.

* When Collection data is written, the field name and field value of the vector type have been written.

* When the index is created, a vector index must also be created.


<span id="7301d6ec"></span>
# **request interface**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you need to construct a signature for authentication. For details on how to use API signatures, refer to <a href="https://docs.byteplus.com/en/docs/VikingDB/Preparation">API Signature Call Guide</a>.</div>



|**URI** |/api/index/search |Uniform Resource Identifier |
|---|---|---|
|**request method** |POST |The type of operation requested by the client on the server |
|**request header** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="e5d82798"></span>
# **request parameters**


|**parameter** |**sub\-parameter** |**type** |**Is it required?**  |**default value** |**parameter description** |
|---|---|---|---|---|---|
|collection_name/collection_alias |*  |String |Yes |*  |Specifies the Collection name/alias to which the retrieved Index belongs.<br><br><br>* Must contain only English letters, numbers, and underscores (_), begin with an English letter, and cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Collection names/aliases cannot be duplicated. |
|index_name |*  |String |Yes |*  |Specifies the Index name to retrieve.<br><br><br>* Must contain only English letters, numbers, and underscores (_), begin with an English letter, and cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Index names cannot be repeated. |
|Search |order_by_vector |Map |Yes |*  |Searches based on vector distance. You must specify either `vectors` or `primary_keys`:<br><br><br>* Vectors: List of vectors to retrieve, up to 10.<br><br>* primary_keys: List of data primary keys used for retrieval, up to 10. The system first finds the corresponding vector using the primary key, and then performs an approximate search using that vector. Supports `int` and `string` types.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Indexes of type hnsw_hybrid do not support primary_keys retrieval.</div><br> |
||Partition |String/int |No |"Default" |The subindex name, the type is consistent with the field_type of the partition_by, and the field value corresponds to the field_value of the partition_by.<br><br><br>* field_type is int64 and list\ < int64 \>, the partition input type is int64.<br><br>* If `field_type` is `string` or `list<string>`, the partition input type is `string` and must match the format `^[a-zA-Z0-9._]+$`.\* n |
||Limit |Int |No |10 |Number of search results, up to 5000. |
||output_fields |List\ < string \> |No |*  |Filter fields, specifying a list of scalar or vector fields to return.<br><br><br>* If `output_fields` is not specified, all scalar fields are returned, but vector fields are not.<br><br>* output_fields an empty list, the fields field is not returned.<br><br>* output_fields formatting error or the filter field is not a field in the collection, the interface returns an error.<br><br><br>If the indexed distance mode is cosine, the vector returned by the vector field is a normalized vector. |


<span id="e5621a0d"></span>
# **response message**


|**parameter** |**parameter description** |
|---|---|
|Code |Status code |
|Message |Return information |
|request_id |A unique identifier for each request. |
|Data |Search results, vector search will return the retrieved primary key, score, fields. |


<span id="56e56a56"></span>
## **status code description**


|**status code** |**HTTP status code** |**Return information** |**status code description** |
|---|---|---|---|
|0 |200 |Vector search successful |Vector search successful. |
|1000008 |400 |Index does not exist |The specified Index does not exist. |
|1000003 |400 |Invalid request |Illegal parameter:<br><br><br>* Required parameters are missing.<br><br>* Lack of search input.<br><br>* Constraint not satisfied. |
|1000001 |401 |Unauthorized |The request header lacks authentication information. |
|1000002 |403 |No permission |Insufficient permissions. |
|1000016 |400 |Invalid vectors for index_recall |The input vector format is invalid. |
|1000029 |429 |The request has reached the upper limit, please adjust the number of CPU cores |The `cpu_quota` needs to be increased. |


<span id="1cbf8c60"></span>
# Complete example

<span id="847e1eae"></span>
## Request message

The following is an example of a dense vector retrieval request using the `vectors` parameter within `order_by_vector`:

```Shell
curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-vikingdb.mlp.ap-mya.byteplus.com/api/index/search \
  -d '{
    "collection_name": "test_name",    // The name of the collection.
    "index_name": "index_test",    // The name of the index. 
    "search": {
        "order_by_vector": {   // The list of query vectors. 
            "vectors": [
                [0.1, 0.2, 0.3......0.9], 
                [0.01, 0.02, 0.03......0.09],
            ],         
        }, 
        "limit": 2,    // The maximum number of search results to return
        }
}
}'
```


<span id="f159f630"></span>
## Response message

Successful execution returns:

```Shell
HTTP/1.1 200 OK
Content-Length: 43
Content-Type: application/json
 
{
    "code":0,
    "msg":"search success",
    "request_id":"021695029537650fd001de666660000000000000000000230da93",
    "data": [
        [
            {
                "id": 1,
                "score": 0.99,
                "fields": {
                    "time": 1690529704,
                    "author": "zhangsan"
                } 
            },
            {
                "id": 2,
                "score": 0.98,
                "fields": {
                    "time": 1690529701,
                    "author": "lisi"
                } 
            }
        ],
        [
            {
                "id": 9,
                "score": 0.95,
                "fields": {
                    "time": 1690529708,
                    "author": "wangwu"
                } 
            },
            {
                "id": 8,
                "score": 0.84,
                "fields": {
                    "time": 1690529710,
                    "author": "zhaoliu"
                } 
            }            
        ]
    ]
}
```


If execution fails, the following response is returned:

```Shell
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000008, "msg":"index not exist","request_id":"021695029537650fd001de666660000000000000000000230da93"}
```
