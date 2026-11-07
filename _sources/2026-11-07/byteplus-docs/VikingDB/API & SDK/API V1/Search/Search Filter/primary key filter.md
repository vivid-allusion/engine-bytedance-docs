---
title: "primary key filter"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/primary_key_filter"
---

To refine your vector search results, you can filter them based on a list of primary keys. This guide provides the API reference for the `/api/index/search` endpoint, detailing how to use the `primary_key_in` and `primary_key_not_in` parameters to precisely include or exclude specific documents from your search.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Primary key filtering is a general\-purpose search capability that you can apply to<strong>basic vector search</strong> and<strong>dense\-sparse hybrid retrieval</strong></div>


<span id="89c399f6"></span>
# **Request Interface**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you need to construct a signature for authentication. For detailed OpenAPI signature calling methods, please refer to <a href="https://docs.byteplus.com/en/docs/VikingDB/Preparation">API Signature Call Guide</a>.</div>



|**URI** |/api/index/search |Uniform Resource Identifier |
|---|---|---|
|**Request Method** |POST |The type of operation requested by the client on the vector database server. |
|**Request Header** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="1bcc2f4e"></span>
# **Request Parameters**

Based on the vector retrieval interface, you can use primary_key_in, primary_key_not_in subparameters for filtering.


|**parameter** |**sub\-parameter** |**type** |**Required** |**default value** |**Parameter Description** |
|---|---|---|---|---|---|
|Search |primary_key_in |List< int64 \> or list\ < string \> |No |*  |Setting this parameter restricts retrieval to the primary key list.<br><br>Passing an empty list has the same effect as omitting this parameter. |
||primary_key_not_in |List< int64 \> or list\ < string \> |No |*  |Setting this parameter excludes data with primary keys in the specified list from the search results. |


<span id="e54f0897"></span>
# **response message**


|**parameter** |**parameter description** |
|---|---|
|Code |Status code |
|Message |Description |
|request_id |A unique identifier for each request. |
|Data |The search results. For a successful search, the response includes the primary key, score, and fields for each retrieved item. |


<span id="6fe51a0f"></span>
## **Status Code Description**


|**status code** |**HTTP status code** |**Description** |**Status Code Description** |
|---|---|---|---|
|0 |200 |Search success |Index retrieved successfully. |
|1000008 |400 |Index does not exist |The specified index does not exist. |
|1000003 |400 |Invalid request |Illegal parameter:<br><br><br>* Required parameters are missing.<br><br>* Search input is missing.<br><br>* Constraint not satisfied. |
|1000001 |401 |Unauthorized |The request header lacks authentication information. |
|1000002 |403 |No permission |Insufficient permissions. |
|1000016 |400 |Invalid vectors for index_recall |The input vector format is invalid. |
|1000029 |429 |The request has reached the upper limit. Please adjust the number of CPU cores |The cpu_quota needs to be increased. |


<span id="bc905ad5"></span>
# Complete example

<span id="f502ea99"></span>
## Request message

```Shell
curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-vikingdb.mlp.ap-mya.byteplus.com/api/index/search \
  -d '{
    "collection_name": "test_name",
    "index_name": "index_test",
    "search": {
        "order_by_vector": {
            "vectors": [
                [0.1, 0.2, 0.3......0.9], 
            ], 
        }, 
        "limit": 2,   
        "primary_key_in":[1,2,3，4，5，6]， // Search within the the list of primary keys. 
        "primary_key_not_in":[7,8]，  // Search outside the list of primary keys. 
        "partition": "default"     // The name of the subindex matches the field value. 
    }
}'
```


<span id="3f1ffdbf"></span>
## Response message

Successful execution returns:

```Shell
HTTP/1.1 200 OK
Content-Length: 43
Content-Type: application/json
 
{
    "code":0,
    "msg":"search success",
    "request_id":"021695029757920fd001de6666600000000000000000002569b8f",
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
        ]
    ]
}
```


A failed execution returns:

```Shell
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000008, "msg":"index not exist", "request_id":"021695029757920fd001de6666600000000000000000002569b8f"}
```
