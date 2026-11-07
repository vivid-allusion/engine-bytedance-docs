---
title: "UpsertData"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/UpsertData_V2"
---

<span id="overview"></span>
# Overview

To write new data or update existing data in a VikingDB Collection, you can use the Upsert Data API. This endpoint allows you to process a single data entry or a batch of up to 100 entries in one request. It also supports advanced features like setting a time\-to\-live (TTL) for automatic data expiration and performing asynchronous writes for improved throughput.

<span id="api-upgrade-notes"></span>
# API Upgrade Notes


* The corresponding V1 API is: https://docs.byteplus.com/en/docs/VikingDB/upsert_data

* Usage differences:



| |V2 API |V1 API |
|---|---|---|
|Parameter for writing data |data |fields |
|Return of model token consumption |Automatically returned |Must be manually set |
|Limit on data volume per write operation |If the dataset has vectorize enabled, no more than 1; without vectorize, no more than 100. |No more than 100. |



* Note: QPS rate limiting is calculated based on the number of data entries, and the rate limiting behavior of V1 and V2 APIs is exactly the same.


<span id="request-api"></span>
# Request API

When requesting the OpenAPI interface of the vector database VikingDB, you can use AK, SK to construct a signature. Please refer to the [Data Plane API Calling Process](https://docs.byteplus.com/lwxm71ps/gk6oc6no), copy the calling example and fill in the necessary information.


|URI |/api/vikingdb/data/upsert |Uniform Resource Identifier |
|---|---|---|
|Method |POST |The type of operation the client requests from the vector database server |
|Request Headers |Content\-Type: application/json |Request message type |
| |Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="request-body-parameters"></span>
# Request Body Parameters


|Parameter Name |Type |Required |Default Value |Remarks |
|---|---|---|---|---|
|resource_id |string |Choose 1 of 2 |*  |Resource ID |
|collection_name |string | |*  |Collection name |
|data |array |Yes |*  |The number of data entries written per request cannot exceed 100.<br><br>Each data entry is represented as a map, where the key is the field name and the value is the field value. The format of field values for different field types is shown in the table below.<br><br>Note:<br><br><br>* Writing non\-existent field names is not allowed.<br><br>* If a field is missing, it will be filled with a default value. If the field type has no default value (such as text), the request will fail.<br><br>* If the request parameters are invalid (4xx type), the entire operation will fail. |
| | | | | |
|ttl |int |No |0 |Must be a positive integer.<br><br>Set to `0` for data that does not expire.<br><br>Data expiration time in seconds. Setting to 86400 will automatically delete the data after 1 day.<br><br>Data TTL deletion will not immediately update the index. |
|async |bool |No |false |Asynchronous write switch<br><br><br>* The rate limit threshold for asynchronous writes is 10 times that of synchronous writes<br><br>* Data written asynchronously will not be written to the collection in real\-time, with a lag of up to several minutes. You can use the FetchDataInCollection API to confirm whether the data has been written to the collection<br><br>* Data written asynchronously will not trigger streaming updates to the index, with index synchronization taking up to several hours. You can use the FetchDataInIndex API to confirm whether the data has been synchronized to the index |


<span id="data-parameter-field-value-format"></span>
# Data Parameter Field Value Format


|Field Type |Format |Description |
|---|---|---|
|int64 |Integer value |Integer |
|float32 |Floating point value |Floating point number |
|string |String |String. Content limit 256 bytes |
|bool |true/false |Boolean type |
|list |String array |String array |
|list |Integer array |Integer array |
|vector |* Vector (floating point array)<br><br>* Base64 encoding of float32/float64 compressed to bytes |Dense vector |
|sparse_vector |A list of dictionaries, where each dictionary represents a non\-zero element. Each dictionary must contain a `token_id` (string) and a `token_weight` (float). |Sparse vector |
|text |String |The value can be empty unless it is a vectorized field. |
|image |String |* Image TOS link. `tos://{bucket}/{object}`<br><br>* An HTTP or HTTPS URL |
|video |map |{<br><br>"value": A TOS link or an HTTP/HTTPS URL<br><br>"fps": 2.0 (0.2\-5 optional)<br><br>} |


<span id="response-body-parameters"></span>
# Response Body Parameters

For common response body parameters, see

[Data Plane API Calling Process](https://docs.byteplus.com/lwxm71ps/gk6oc6no)


|Parameter Name |Type |Sub\-parameters | |Description |
|---|---|---|---|---|
|result |map |token_usage |map |Includes `prompt_tokens`, `completion_tokens`, `image_tokens`, and `total_tokens`. |


<span id="request-response-example"></span>
# Request Response Example

<span id="_1-writing-to-a-dataset-with-direct-vector-fields"></span>
## 1. Writing to a Dataset with Direct Vector Fields


* Request parameters


```JSON
req_path = "/api/vikingdb/data/upsert"
req_body = {
    "collection_name": "test_coll",
    "data": [
        {
            "f_good_id": "000135",
            "f_vector": [0.1, 0.33, -0.88, 0.66],
            "f_city": "Beijing"
        }
    ]
}
```



* Response parameters


```JSON
{
    "code": "Success",
    "message": "The API call was executed successfully.",
    "request_id": "02175438839168500000000000000000000ffff0a003ee4fc3499",
    "result": null
}
```


<span id="_2-writing-a-dataset-with-vectorized-fields"></span>
## 2. Writing a dataset with vectorized fields

<span id="image-and-text-examples"></span>
### Image and Text Examples


* Request parameters


```JSON
req_path = "/api/vikingdb/data/upsert"
req_body = {
    "collection_name": "test_coll_with_vectorize",
    "data": [
        {
            "f_id": "000135",
            "f_city": "Beijing",
            "f_text": "This is a historical artifact with a history of 1,300 years",
            "f_image": "tos://my_bucket/good_000135.jpg"
        }
    ]
}
```



* Response parameters


```JSON
{
    "code": "Success",
    "message": "The API call was executed successfully.",
    "request_id": "02175438839168500000000000000000000ffff0a003ee4fc3499",
    "result": {
        "token_usage": {
            "Skylark-embedding-vision__250615": {
                "prompt_tokens": 1325,
                "completion_tokens": 0,
                "image_tokens": 1312,
                "total_tokens": 1325
            }
        }
    }
}
```


<span id="video-example"></span>
### Video Example


* Request parameters


```JSON
req_path = "/api/vikingdb/data/upsert"
req_body = {
    "collection_name": "test_coll_with_vectorize",
    "data": [
        {
            "f_id": "000135",
            "f_city": "Beijing",
            "f_text": "This is a historical artifact with a history of 1,300 years",
            "f_image": "tos://my_bucket/good_000135.jpg",
            "f_video": {
                "value": "tos://my_bucket/good_000135.mp4",
                "fps": 2.0,
             }
        }
    ]
}
```



* Response parameters


```JSON
{
    "code": "Success",
    "message": "The API call was executed successfully.",
    "request_id": "02175438839168500000000000000000000ffff0a003ee4fc3499",
    "result": {
        "token_usage": {
            "Skylark-embedding-vision__250615": {
                "prompt_tokens": 1325,
                "completion_tokens": 0,
                "image_tokens": 1312,
                "total_tokens": 1325
            }
        }
    }
}
```
