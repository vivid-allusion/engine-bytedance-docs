---
title: "Id Search"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Id_Search_V2"
---

<span id="ce3da116"></span>
# Overview

To find items in your vector collection that are similar to a specific item, you can use the Search by ID API. This API takes a primary key ID, retrieves its corresponding vector, and uses that vector to perform a similarity search, returning a list of the most similar items.

<span id="9d21dbb3"></span>
# Request API

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you can use AK, SK to construct a signature. Please refer to the <a href="https://docs.byteplus.com/docs/VikingDB/Data_Plane_API_Calling_Process">Data Plane API Calling Process</a>, copy the code example and fill in the necessary information.</div>



|URI |/api/vikingdb/data/search/id |Uniform Resource Identifier |
|---|---|---|
|Method |POST |The type of operation the client performs on the vector database server |
|Headers |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="194c9574"></span>
# Request Body Parameters

Only parameters specific to this interface are listed. For more information, please refer to

[Data Plane API Calling Process](https://docs.byteplus.com/docs/VikingDB/Data_Plane_API_Calling_Process)


|Parameter |Required |Type |Description |
|---|---|---|---|
|id |Yes |int64/string<br><br>or list |Primary key ID. The vector associated with this primary key will be used as the search condition. |


<span id="92d6225c"></span>
# Request and Response Example


* Request Parameters


```JSON
req_path = "/api/vikingdb/data/search/id"
req_body = {
    "collection_name": "test_coll",
    "index_name": "idx_1",
    "id": "uid_001",
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
