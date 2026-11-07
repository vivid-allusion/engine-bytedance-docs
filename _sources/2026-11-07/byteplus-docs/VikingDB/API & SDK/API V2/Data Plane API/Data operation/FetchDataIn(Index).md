---
title: "FetchDataIn(Index)"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/FetchDataIn_Index_V2"
---

<span id="f9706475"></span>
# Overview

To query one or more data entries from a specified index by their primary keys, use this API. You can retrieve up to 100 entries in a single request.

<span id="7db0a0bb"></span>
# API Upgrade Notes


* The corresponding V1 API is: https://docs.byteplus.com/en/docs/VikingDB/fetch_data_index

* Usage differences:



| |V2 API |V1 API |
|---|---|---|
|Parameter name for specifying primary key |ids |primary_keys |
|Sub\-index |Performance and usability improvements with sharding are under development, please stay tuned. |Specified by partition parameter |
|Response fields |Primary key values are listed separately for easier data location. |All fields are at the same level in the response |


<span id="9bd5e9a7"></span>
# Request API

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you can use AK, SK to construct a signature. Please refer to the <a href="https://docs.byteplus.com/docs/VikingDB/Data_Plane_API_Calling_Process">Data Plane API Calling Process</a>, copy the calling example and fill in the necessary information.</div>



|URI |/api/vikingdb/data/fetch_in_index |Uniform Resource Identifier |
|---|---|---|
|Method |POST |The type of operation the client requests from the vector database server |
|Request Headers |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="f67dacd6"></span>
# Request Body Parameters


|Parameter Name |Type |Required |Remarks |
|---|---|---|---|
|resource_id |string |Choose 1 of 2 |Resource ID |
|collection_name |string ||Collection name |
|index_name |string |Yes |Index name |
|ids |list of single\-column or dual\-column primary keys<br><br>list<br><br>or listdual\-column primary key |Yes |* List of primary keys for data lookup. Maximum 100 entries |
|||||
|output_fields |list |No |List of scalar fields to return.<br><br><br>1. If this parameter is not provided, all scalar fields are returned<br><br>2. If an empty list is provided, no scalar fields are returned<br><br>3. If the format of output_fields is incorrect or if the specified fields are not in the collection, the API returns an error |


<span id="673536c1"></span>
# Response Body Parameters

For common response body parameters, see

[Data Plane API Calling Process](https://docs.byteplus.com/docs/VikingDB/Data_Plane_API_Calling_Process)


|Parameter Name |Type |Sub\-parameters | |Description |
|---|---|---|---|---|
|result |map |fetch |list |A list of the queried data. The structure of each item is described in the FetchResult section below. |
|||ids_not_exist |list<br><br>or list |List of non\-existent primary keys |


<span id="c4f8a258"></span>
## FetchResult


|Parameter Name |Type |Remarks |
|---|---|---|
|id |string/int64<br><br>list (for a dual\-column primary key) |Primary key value |
|fields |map |The key is the field name, and the value is the field value. |
|dense_vector |list |Dense vector |
|dense_dim |int |Dense vector dimension |


<span id="be3f3e14"></span>
# Request Response Example


* Request parameters


```JSON
req_path = "/api/vikingdb/data/fetch_in_index"
req_body = {
    "collection_name": "test_coll",
    "index_name", "idx_1",
    "ids": [
        "uid_001",
        "uid_002",
        "uid_005"
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
        "fetch":[
            {
                "id": "uid_001",
                "fields": {
                    "f_good_id": "uid_001", "f_text": "This is a cultural relic from the Tang Dynasty, dating back 1,300 years."
                },
                "dense_dim": 1024,
                "dense_vector": [0.05674682557582855, 0.001147925853729248, ......]
            },
            {
                "id": "uid_002",
                "fields": {
                    "f_good_id": "uid_002", "f_text": "This is a cultural relic from the Qing Dynasty, dating back 300 years."
                },
                "dense_dim": 1024,
                "dense_vector": [0.001147925853729248, 0.0011479258, ......]
            },
        ],
        "ids_not_exist": [
            "uid_005"
        ]
    }
}
```
