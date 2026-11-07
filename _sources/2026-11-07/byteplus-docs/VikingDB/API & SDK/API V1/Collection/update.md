---
title: "update"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/update"
---

<span id="1cb243a9"></span>
# Overview

Use the /api/collection/update interface to modify an existing Collection. You can add new scalar fields, update the collection's description, or change its aliases. Please note that this interface does not support adding new vector fields or modifying the properties of existing fields.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Collection supports new field fields, not new Vector field types; defined field fields do not support modification, only support modifying dataset descriptions.</div>


<span id="379ca915"></span>
# **Request**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you need to construct a signature for authentication. For detailed OpenAPI signature calling methods, please refer to <a href="https://docs.byteplus.com/en/docs/VikingDB/Preparation">API Signature Call Guide</a>.</div>



|**URI** |/api/collection/update |Uniform Resource Identifier |
|---|---|---|
|**request method** |POST |The type of operation requested by the client on the vector database server |
|**request header** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="f97acdeb"></span>
# **request parameters**


|**parameter** |**sub\-parameter** |**type** |**Is it required?**  |**default value** |**parameter description** |
|---|---|---|---|---|---|
|collection_name |*  |String |Yes |*  |The name of the collection to modify.<br><br><br>* Must contain only English letters, numbers, and underscores (_), and must begin with an English letter. It cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Collection names cannot be repeated. |
|collection_aliases |*  |Array |No |*  |Modify the alias of the dataset.<br><br><br>* You can set multiple aliases.<br><br>* The same dataset alias cannot be repeated.<br><br>* If an alias is already mapped to another collection, setting it here will release it from the original collection and map it to the current one<br><br>* Must contain only English letters, numbers, and underscores (_), and must start with an English letter.<br><br>* Length requirements: [1,128]. |
|Description |*  |String |No |" |Modify the description of the Collection.<br><br><br>* Length requirement: [0,65535]. |
|Fields<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The maximum number of fields in a Collection is 200.</div><br> |field_name |String |Yes |*  |The name of the new field to add.<br><br><br>* Must contain only English letters, numbers, and underscores (_), and must begin with an English letter. It cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Field names cannot be repeated. |
||field_type |String |Yes |*  |The type of the new field. For details, see the "field_type optional values" section. |
||default_val |Consistent with field_type |No |*  |The default value for the new field. For details, see the "field_type optional values" section.<br><br><br>* When the field is a primary key, `default_val` has no effect and is not validated. |
||Dimension |Int |Required when field_type is a vector |*  |Specifies the dimension of the vector field.<br><br><br>* Value range: [4, 2048], and must be a multiple of 4.<br><br>* Vector dimension refers to the number of elements contained in a vector. |
||pipeline_name |String |Optional when field_type is text |*  |Text. A plain text preprocessing pipeline is a process where the vector database automates text slicing, vectorization, and storage. Support writing to the original data source in string form.<br><br>pipeline_name enumeration values are as follows:<br><br><br>* text_split_bge_large_zh: The vector database uses a slicer to split long text into short text, and calls the embedding model to vectorize short text.<br><br>* text_bge_large_zh: The vector database does not split the text, and directly calls the embedding model to vectorize the text.<br><br>* text_split_bge_m3: The vector database uses the slicer to divide the long text into short text, calls the bge m3 model to extract the sparse features and dense features of the short text, and stores them in the dense and sparse vector fields preset by the system.<br><br>* text_bge_m3: The vector database does not divide the text, directly calls bge m3 to extract the sparse features and dense features of the short text, and stores them in the dense and sparse vector fields preset by the system.<br><br>* text_split_bge_large_and_m3: The vector database uses the slicer to divide the long text into short texts, calls the bge v1.5 model to extract the dense features of the short text and stores them in the dense vector field preset by the system; calls the bge m3 model to extract the sparse features of the short text and stores them in the sparse vector field preset by the system.<br><br>* text_bge_large_and_m3: The vector database does not divide the text, calls the bge v1.5 model to extract the dense features of the short text and stores them in the dense vector field preset by the system; calls the bge m3 model to extract the sparse features of the short text and stores them in the sparse vector field preset by the system. |


<span id="7a7da3a5"></span>
## field_type optional values


|**field type** |**Available index types** |**default_val default** |**When data is written**<br><br>**value range** |**default_val**<br><br>**value range** |**Can be the primary key** |**explain** |
|---|---|---|---|---|---|---|
|Int64 |Enumeration |0 |Int64 range |Int64 range |Yes |Integer |
|Float32 |Range |0.0 |Float32 range |Float32 range |No |Floating point number |
|String |Enumeration |"Default" |*  |Length <= 128 |Yes |String |
|Bool |Enumeration |False |True/false |True/false |No |Boolean type |
|List |Enumeration |["Default"] |List length <= 32 |List length <= 32 |No |String array |
|List |Enumeration |[0] |List length <= 32 |List length <= 32 |No |Integer array |
|Vector |Vector |*  |Dimension 4\-2048 |*  |No |Dense vector.<br><br><br>* The `dim` parameter is required when `field_type` is `Vector`. |
|sparse_vector |Sparse vector |*  |Number of non\-zero elements: Unlimited<br><br>Non\-zero values are in the float32 range |*  |No |Sparse vector.<br><br><br>* sparse_vector cannot be set separately, it must be set in combination with the vector field.<br><br>* Receives a JSON object of index\-value pairs representing the non\-zero elements of the sparse vector and their corresponding weights.<br><br>> Example:<br><br>> sparse_vector = |
|Text |*  |*  |*  |*  |No |Text, note:<br><br><br>* The `pipeline_name` parameter is optional when `field_type` is `Text`.<br><br>* When adding a `Text` field with a `pipeline_name`, you cannot also add `Vector` or `sparse_vector` fields, and only one such `Text` field is permitted. When adding a `Text` field without a `pipeline_name`, you can add `Vector` and `sparse_vector` fields, and multiple such `Text` fields are allowed (up to 200). |


<span id="3e6217d8"></span>
# **Response**


|**parameter** |**parameter description** |
|---|---|
|Code |Status code |
|Message |Description |
|request_id |A unique identifier for each request |


<span id="ddf6b23a"></span>
## **status code description**


|**status code** |**HTTP status code** |**Return information** |**status code description** |
|---|---|---|---|
|0 |200 |Success |The specified Collection was successfully modified. |
|1000003 |400 |Invalid request:% s |Invalid parameter<br><br><br>* Required parameters are missing.<br><br>* Unexpected parameters, such as primary_key.<br><br>* An attempt was made to modify an existing field (for example, by deleting it or changing its properties).<br><br>* Field types and related field properties do not satisfy constraints. |
|1000001 |401 |Unauthorized |The request header lacks authentication information. |
|1000002 |403 |No permission |Insufficient permissions. |


<span id="e00817f6"></span>
# Complete example

<span id="e8e54fac"></span>
## Request message

```Shell

curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256***' \
  https://api-vikingdb.mlp.ap-mya.byteplus.com/api/collection/update \
  -d '{
    "collection_name": "test_name",
    "description": "test dataset",
    "fields": [
        {
            "field_name": "city",
            "field_type": "int64",       
            "default_val": 0
        },
        {
            "field_name": "author",
            "field_type": "string",      
            "default_val": "null"
        }
    ]
}'
```


<span id="13e454eb"></span>
## Response message

Successful execution returns:

```Shell
HTTP/1.1 200 OK
Content-Length: 43
Content-Type: application/json
 
{"code":0,"msg":"success","request_id":"021695029537650fd001de666660000000000000000000230da93"}
```


If execution fails, the response is:

```Shell
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000003,"msg":"invalid request: collect miss","request_id":"021695029537650fd001de666660000000000000000000230da93"}
```
