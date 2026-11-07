---
title: "Scalar Sort Search"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Scalar_Sort_Search_V2"
---

<span id="0e320055"></span>
# Overview

To retrieve and sort data based on specific numeric attributes in your vector database, you can use the Scalar Search API. This API allows you to query indexed int64 or float32 fields, such as price or age, and order the results in ascending or descending order.

<span id="841e110a"></span>
# Request API

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you can use AK, SK to construct a signature. Please refer to the [Data Plane API Calling Process]. Copy the calling example and fill in the necessary information.</div>



|URI |/api/vikingdb/data/search/scalar |Uniform Resource Identifier |
|---|---|---|
|Method |POST |Client operation type for the vector database server |
|Headers |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="680273b1"></span>
# Request Body

Only parameters specific to this interface are listed. For more information, please refer to

[Data Plane API Calling Process](https://docs.byteplus.com/docs/VikingDB/Data_Plane_API_Calling_Process)


|Parameter |Required |Type |Description |
|---|---|---|---|
|field |Yes |string |Field name. Prerequisites: 1. The field must be int64 or float32. 2. A scalar index must be created for this field. |
|order |No |string |asc/desc. The default is `desc` for descending order; use `asc` for ascending order. |


<span id="19a59807"></span>
# Example Request and Response


* Request Body


```JSON
req_path = "/api/vikingdb/data/search/scalar"
req_body = {
    "collection_name": "test_coll",
    "index_name": "idx_1",
    "limit": 2,
    "field": "f_price",
    "order": "desc"
}
```



* Response Body


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
                "score": 999000
            },
            {
                "id": "uid_002",
                "fields": {
                    "f_good_id": "uid_002", "f_price": 309000
                },
                "score": 309000
            }
        ],
        "total_return_count": 2
    }
}
```
