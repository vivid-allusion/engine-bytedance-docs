---
title: "Multimodal Retrieval"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Multimodal_Retrieval"
---

<span id="e11f515f"></span>
# Overview

To perform multimodal data retrieval using text or images, you can call the `/index/search` API endpoint. This reference provides the required request parameters, such as `order_by_raw`, and includes complete `curl` examples for text search and image search to help you implement this feature.

Multimodal data retrieval means that the vector database supports direct retrieval through multi\-modal data types such as images and text, and supports modal combinations, such as text search, image search, and text + image search.

<span id="bfeb15b9"></span>
# **prerequisite**


* From the console, select a database type that supports vectorization and configure the vectorization field when creating the dataset. Alternatively, when using the create_collection interface, configure vectorization for the Collection by setting the vectorize parameter.

* Using the upsert_data interface, you have written field names and values for fields of type text or image.

* When an index is created, a vector index is also created.


<span id="afd76b24"></span>
# **request interface**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you need to construct a signature for authentication. For detailed OpenAPI signature calling methods, please refer to <a href="https://docs.byteplus.com/en/docs/VikingDB/Preparation">API Signature Call Guide</a>.</div>



|**URI** |/api/index/search |Uniform Resource Identifier |
|---|---|---|
|**request method** |POST |The type of operation requested by the client on the vector database server |
|**request header** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="f4589716"></span>
# **request parameters**

For multimodal data retrieval, use the `order_by_raw` and `need_instruction` sub\-parameters in addition to the basic vector retrieval parameters.


|**parameter** |**sub\-parameter** |**type** |**Is it required?**  |**default value** |**parameter description** |
|---|---|---|---|---|---|
|Search |order_by_raw |Map |Yes |*  |Multimodal data retrieval, currently supports text and image retrieval, the fields are as follows:<br><br><br>* Text: The input text retrieved.<br><br>* Image: Currently supports 2 ways:<br><br>   * Image tos link.`tos://{bucket}/{object_key}`.<br><br>   * Base64 string.`base64://{Base64Encoding}`. |
||need_instruction |Bool |Yes |The default value is determined by the model. For “bean bag” series models, the default is true; for other models, the default is false. |Specifies whether to add instructions before the query during vectorization. |


<span id="286a9c37"></span>
## **response message**


|**parameter** |**parameter description** |
|---|---|
|Code |Status code |
|Message |Return information |
|request_id |A unique identifier for each request |
|Data |The search results. For example, a search can return the retrieved primary key, score, text, and other fields for each item. |


<span id="1ecdcd7a"></span>
## **status code description**


|**status code** |**HTTP status code** |**Return information** |**status code description** |
|---|---|---|---|
|0 |200 |Search successful. |Index retrieved successfully. |
|1000008 |400 |Index does not exist |The specified index does not exist. |
|1000003 |400 |Invalid request |Invalid parameter:<br><br><br>* Required parameters are missing.<br><br>* Search input is missing.<br><br>* A constraint is not satisfied. |
|1000001 |401 |Unauthorized |The request header lacks authentication information. |
|1000002 |403 |No permission |Insufficient permissions. |
|1000029 |429 |The request rate has reached the limit. Please adjust the number of CPU cores. |The cpu_quota needs to be increased. |


<span id="9117a994"></span>
# Complete example


* ## Text search   <span id="text-search"></span>


<span id="b5181614"></span>
### Request message

```Shell
curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-vikingdb.mlp.ap-mya.byteplus.com/api/index/search \
  -d '{
    "collection_name": "test_name",
    "index_name": "index_test",
    "search": {
        "order_by_raw":{
            "text":"hello" 
        },
        "dense_weight": 0.5, 
        "limit": 3
    }
}
}'
```


<span id="a91eb812"></span>
### Response message

A successful execution returns the following:

```Shell
HTTP/1.1 200 OK
Content-Length: 43
Content-Type: application/json
 
{
        "message": "success",
        "code": 0,
        "request_id":"021695029736548fd001de66666000000000000000000029aa917",
        "data": [
                [{
                        "score": 0.9027934670448303,
                        "text": "hello world1",
                        "id": 1001,
                        "fields": {
                                "time": 1690529704,
                                "author": "zhangsan"
                }
                },
                {
                        "score": 0.8901656270027161,
                        "text": "hello world3",
                        "id": 1003,
                         "fields": {
                                "time": 1690529701,
                                "author": "lisi"
                }
                },
                {
                        "score": 0.8855509757995605,
                        "text": "hello world2",
                        "id": 1002,
                        "fields": {
                                "time": 1690529708,
                                "author": "wangwu"
                }
                }]
        ]
}
```


A failed execution returns the following:

```Plain
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000008, "msg":"index not exist", "request_id":"021695029736548fd001de66666000000000000000000029aa917"}
```



* ## Image search   <span id="image-search"></span>


<span id="31eaf86b"></span>
### Request message

```Plain
curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-vikingdb.mlp.ap-mya.byteplus.com/api/index/search \
  -d '{
    "collection_name": "test_name",
    "index_name": "index_test",
    "search": {
        "order_by_raw":{
            "image":"tos://best-practice-pic-search-tos/pic_search_1000_images/003bd60fa9.jpg}" 
        },
        "dense_weight": 0.5, 
        "limit": 3
    }
}
}'
```


<span id="ed3b069f"></span>
### Response message

A successful execution returns the following:

```Plain
HTTP / 1.1 200 OK Content - Length: 43 Content - Type: application / json

{
        "message": "success",
        "code": 0,
        "request_id": "02174064805694700000000000000000000ffff0a00449f914fac",
        "data": [[{
                "fields": {
                        "id": 3,
                        "img_field": "tos://best-practice-pic-search-tos/pic_search_1000_images/000ef44b56.jpg"
                },
                "id": 3,
                "score": 0.125640869140625
        },
        {
                "fields": {
                        "id": 2,
                        "img_field": "tos://best-practice-pic-search-tos/pic_search_1000_images/000d3a9260.jpg"
                },
                "id": 2,
                "score": 0.03074061870574951
        },
        {
                "fields": {
                        "id": 1,
                        "img_field": "tos://best-practice-pic-search-tos/pic_search_1000_images/0009fc27d9.jpg"
                },
                "id": 1,
                "score": 0.02828240394592285
        }]]
}
```


A failed execution returns the following:

```Shell
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000008, "msg":"index not exist", "request_id":"02174064805694700000000000000000000ffff0a00449f914fac"}
```
