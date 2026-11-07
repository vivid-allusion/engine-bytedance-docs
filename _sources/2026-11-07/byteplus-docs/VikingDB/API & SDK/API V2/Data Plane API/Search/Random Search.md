---
title: "Random Search"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Random_Search_V2"
---

<span id="578f3ca1"></span>
# Overview

Random search is a search method that randomly returns several records from a dataset without specifying query content. Random search also supports filtering and post\-processing of search results, which can be used for scenarios such as comparing recall effectiveness and data filtering.

<span id="bb4b8363"></span>
# Request API

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When making requests to the VikingDB vector database's OpenAPI, you can use AK, SK to construct a signature. Please refer to the <a href="https://docs.byteplus.com/docs/VikingDB/Data_Plane_API_Calling_Process">Data Plane API Calling Process</a>, copy the calling example and fill in the necessary information.</div>



* 



|URI |/api/vikingdb/data/search/random |Uniform Resource Identifier |
|---|---|---|
|Method |POST |The HTTP method for the request. |
|Headers |Content\-Type: application/json |The media type of the request body. |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="45b41c86"></span>
# Request Body Parameters

No special parameters. For more information, please refer to

[Data Plane API Calling Process](https://docs.byteplus.com/docs/VikingDB/Data_Plane_API_Calling_Process)

<span id="3388a9cd"></span>
# Request and Response Example


* Request Parameters


```JSON
req_path = "/api/vikingdb/data/search/random"
req_body = {
    "collection_name": "test_coll",
    "index_name": "idx_1",
    "limit": 2
}
```



* Response Parameters


```JSON
{
    "code": "Success",
    "message": "The API call was executed successfully.",
    "request_id": "02175438839168500000000000000000000ffff0a003ee4fc3499",
    "result": {
        "data": [
            {
                "id": "uid_001",
                "fields": {
                    "f_good_id": "uid_001", "f_price": 999000
                },
                "score": 1.000000,
                "ann_score": 1.000000
            },
            {
                "id": "uid_002",
                "fields": {
                    "f_good_id": "uid_002", "f_price": 309000
                },
                "score": 0.88232,
                "ann_score": 0.88232,
            }
        ],
        "total_return_count": 2
    }
}
```
