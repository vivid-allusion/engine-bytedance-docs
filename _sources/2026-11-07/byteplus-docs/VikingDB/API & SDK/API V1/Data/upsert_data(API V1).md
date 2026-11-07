---
title: "upsert_data(API V1)"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/upsert_data"
---

<span id="c2e13e0e"></span>
# Overview

To add new data or update existing entries in a specified collection, you can use the `/collection/upsert_data` API. This interface allows you to efficiently perform batch operations, supporting up to 100 data entries in a single request.

<span id="537b628b"></span>
# **API Request**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you need to construct a signature for authentication. For detailed OpenAPI signature calling methods, please refer to <a href="https://docs.byteplus.com/en/docs/VikingDB/Preparation">API Signature Call Guide</a>.</div>



|**URI** |/api/collection/upsert_data |Uniform Resource Identifier |
|---|---|---|
|**request method** |POST |The type of operation requested by the client on the vector database server |
|**request header** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="6ef5d812"></span>
# **request parameters**


|**parameter name** |**type** |**Is it required?**  |**parameter description** |
|---|---|---|---|
|collection_name/collection_alias |String |Yes |Specifies the Collection name/alias for writing data.<br><br><br>* The name must begin with an English letter, cannot be empty, and can only contain English letters, numbers, and underscores (_).<br><br>* Length requirements: [1,128].<br><br>* Collection names/aliases cannot be duplicated. |
|Fields |Array |Yes |Specifies the data to be written.<br><br><br>* The number of data records written in a single request cannot exceed 100.<br><br>* Each data record is a map where the key is the field name and the value is the field value.<br><br>* The maximum size of the data in the fields array is 65535 bytes. When the limit is exceeded, an error will be returned: "fields data is too long, should be less than 65535".<br><br>* The format of field values for different field types is as follows:<br><br>   * Int 64: The format is an integer value.<br><br>   * Float: The format is a floating\-point value.<br><br>   * String: A string value.<br><br>   * Bool: The format is true/false.<br><br>   * List\ < string \>: The format is a string array.<br><br>   * List\ < int64 \>: The format is an integer array.<br><br>   * Vector: The format is vector (array of floating\-point numbers).<br><br>   * The format is a JSON object where the key (k) is a string representing the keyword literal, and the value (v) is a float representing the keyword's weight.<br><br>   * Text: A string value.<br><br>   * This field currently supports specifying images by their TOS paths. The format is tos://{bucket}/{object_key}. |
|TTL |Int |No |Data expiration time, in seconds.<br><br><br>* Format: 0 or a positive integer.<br><br>* The default value is 0, which means the data does not expire.<br><br>* When ttl is set to 86400, it means that the data will be automatically deleted after 1 day.<br><br>* Expired data is deleted, but this change may not be reflected in the index immediately. |
|Async |Bool |No |Specifies whether the request is asynchronous. Asynchronous requests are suitable for large\-scale data writing scenarios and can improve performance by up to 10 times.<br><br><br>* True: Indicates an asynchronous request for writing.<br><br>* The default is False, which indicates a synchronous request. |
|need_token_usage |Bool |No |Returns token consumption information |


<span id="919d162e"></span>
# **API Response**


|**parameter** |**parameter description** |
|---|---|
|Code |Status code |
|Message |Result message |
|request_id |A unique identifier for the request |


<span id="88815638"></span>
## **status code description**


|**status code** |**HTTP status code** |**Return information** |**status code description** |
|---|---|---|---|
|0 |200 |Success |Data was successfully written to the specified Collection. |
|1000005 |400 |Collection does not exist. |Collection does not exist. |
|1000003 |400 |Invalid request:% s |Illegal parameter:<br><br><br>* Required parameters are missing.<br><br>* The field value does not match the field type. |
|1000001 |401 |Unauthorized |The request header lacks authentication information. |
|1000002 |403 |No permission |Insufficient permissions. |


<span id="3ba7a273"></span>
# Complete example

<span id="e6b05c91"></span>
## Request message

Example of writing vector data synchronously:

```Shell

curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-vikingdb.mlp.ap-mya.byteplus.com/api/collection/upsert_data \
  -d '{
    "collection_name": "test_name",
    "fields": [
        {
            "id": 1000,
            "text": "hello world!",
            "vector_field": [0.10, 0.13.........0.52],
            "sparse_vector_field": {"hello": 0.34, "world": 0.03, "!": 0.11},
            "time": 1690529701,
            "author": "laoshe"
        },
        
        ...                              
    ]
}'
```


Example of writing text data synchronously:

```Shell
curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-vikingdb.volces.com/api/collection/upsert_data \
  -d '{
        "collection_name": "test_raw_data_collection",
        "fields": [{
                "id": 1001,  
                "gap": 1.1,
                "content": "hello world"
        }]
}'
```


<span id="46efb330"></span>
## Response message

Example of a successful response:

```Shell
HTTP/1.1 200 OK
Content-Length: 43
Content-Type: application/json
 
{"code":0,"msg":"success","request_id":"021695029757920fd001de6666600000000000000000002569b8f"}
```


Example of an error response:

```Shell
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000005, "msg":"collection not exist", "request_id":"021695029757920fd001de6666600000000000000000002569b8f"}
```
