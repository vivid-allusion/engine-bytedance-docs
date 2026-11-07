---
title: "Vector Search"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Vector_Search_V2"
---

<span id="overview"></span>
# Overview

To find the most relevant items in your dataset, you can use the Vector Search API. This document details the /api/vikingdb/data/search/vector endpoint, which supports searching with dense vectors, sparse vectors, or a hybrid approach. You will also learn how to apply tensor reranking to further refine your search results.

<span id="request-api"></span>
# Request API

When requesting the OpenAPI interface of the vector database VikingDB, you can use AK, SK to construct a signature. Please refer to the [Data Plane API Calling Process](https://docs.byteplus.com/en/docs/VikingDB/Data_Plane_API_Calling_Process), copy the request example and fill in the necessary information.


|URI |/api/vikingdb/data/search/vector |Uniform Resource Identifier |
|---|---|---|
|Method |POST |The HTTP method used to send the request |
|Headers |Content\-Type: application/json |Request message type |
| |Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="request-body-parameters"></span>
# Request Body Parameters

Only parameters specific to this interface are listed. For more information, please refer to

[Data Plane API Calling Process](https://docs.byteplus.com/en/docs/VikingDB/Data_Plane_API_Calling_Process)


|Parameter |Required |Type |Description |
|---|---|---|---|
|dense_vector |Yes |list |Dense vector for search. |
|sparse_vector |No |map |Sparse vector for search. |
|tensor_rerank |No |map |Tensor rerank structure. See [Tensor Rerank structure](https://docs.byteplus.com/en/docs/VikingDB/Common_Search_Parameters_V2#post-processing-structure:~:text=5%20%3Cbr%3E%20%7D%20%3Cbr%3E-,Tensor%20Rerank%20structure,-Note%3A%20This%20parameter) in Common Search Parameters. |


<span id="request-response-example"></span>
### Request and Response Example

<span id="_1-dense-vector-search"></span>
#### 1. Dense Vector Search


* Request Parameters


```JSON
req_path = "/api/vikingdb/data/search/vector"
req_body = {
    "collection_name": "test_coll",
    "index_name": "idx_1",
    "dense_vector": [0.1243, -0.344345, 0.43232, ......],
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
                "score": 9.899999618530273,
                "ann_score": 9.899999618530273
            },
            {
                "id": "uid_002",
                "fields": {
                    "f_good_id": "uid_002", "f_price": 309000
                },
                "score": 8.324234999961,
                "ann_score": 8.324234999961,
            }
        ],
        "total_return_count": 2
    }
}
```


<span id="_2-dense-sparse-vector-search"></span>
#### 2. Dense + Sparse Vector Search


* Request Parameters


```JSON
req_path = "/api/vikingdb/data/search/vector"
req_body = {
    "collection_name": "test_coll",
    "index_name": "idx_1",
    "dense_vector": [0.1243, -0.344345, 0.43232, ......],
    "sparse_vector": {"Song": 0.1, "Official Kiln": 0.5}
    "limit": 2
}
```


<span id="_3-dense-vector-search-tensor-rerank"></span>
#### 3. Dense Vector Search + Tensor Rerank


* Request Parameters


```Plain
req_path = "/api/vikingdb/data/search/vector"
req_body = {
    "collection_name": collection_name,
    "index_name": index_name,
    "dense_vector": [0.1243, -0.344345, 0.43232, ......],
    "limit": 5,
    "output_fields": ["id", "name"],
    "tensor_rerank": {
        "tensor": [
            [0.1, 0.2, ...],
            [0.3, 0.4, ...],
            ...
            [0.8, 0.9, ...]
        ],
        "input_limit": 50
    }
}
```



* Response Parameters


```JSON
{
  "code": "Success",
  "message": "The API call was executed successfully.",
  "request_id": "02176373685223400000000000000000000ffff0a00730a97ec44",
  "result": {
    "data": [
      {
        "id": 35,
        "fields": {
          "id": 35,
          "name": "PGKgzIpXyr"
        },
        "score": 142.28414916992188,
        "ann_score": 0.7548813819885254
      }
    ]
  }
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
                "score": 10.899999618530273,
                "ann_score": 10.899999618530273
            },
            {
                "id": "uid_002",
                "fields": {
                    "f_good_id": "uid_002", "f_price": 309000
                },
                "score": 4.324234999961,
                "ann_score": 4.324234999961,
            }
        ],
        "total_return_count": 2
    }
}
```
