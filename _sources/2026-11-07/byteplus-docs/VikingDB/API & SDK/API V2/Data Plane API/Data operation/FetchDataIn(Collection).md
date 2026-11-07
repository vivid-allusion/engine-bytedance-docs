---
title: "FetchDataIn(Collection)"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/FetchDataIn_Collection_V2"
---

<span id="4792cf6d"></span>
# Overview

This API fetches one or more data entries from a specified collection by their primary keys. You can retrieve up to 100 entries in a single request.

<span id="05ca1861"></span>
# API Upgrade Notes


* The corresponding V1 API is: https://docs.byteplus.com/en/docs/VikingDB/fetch_data_collection

* Usage differences:



| |V2 API |V1 API |
|---|---|---|
|Parameter name for specifying primary key |ids |primary_keys |
|Response fields |Primary key values are listed separately for easier data location. |All fields are at the same level in the response |


<span id="f4b9fec3"></span>
# Request API

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you can use AK, SK to construct a signature. Please refer to the <a href="https://docs.byteplus.com/docs/VikingDB/Data_Plane_API_Calling_Process">Data Plane API Calling Process</a>, copy the request example and fill in the necessary information.</div>



* 



|URI |/api/vikingdb/data/fetch_in_collection |Uniform Resource Identifier |
|---|---|---|
|Method |POST |The type of operation the client requests from the vector database server |
|Request Headers |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="4fd4cf67"></span>
# Request Body Parameters


|Parameter Name |Type |Required |Default Value |Remarks |
|---|---|---|---|---|
|resource_id |string |Conditional |*  |Resource ID |
|collection_name |string ||*  |Collection name |
|ids |list<br><br>list |Yes |*  |* List of primary keys for data lookup. Maximum 100 entries |
||||*  ||


<span id="e9315842"></span>
# Response Body Parameters

For common response body parameters, see

[Data Plane API Calling Process](https://docs.byteplus.com/docs/VikingDB/Data_Plane_API_Calling_Process)


|Parameter Name |Type |Sub\-parameters | |Description |
|---|---|---|---|---|
|result |map |fetch |list |List of queried data, FetchResult structure is shown below. |
|||ids_not_exist |list |List of non\-existent primary keys |


<span id="c798137b"></span>
## FetchResult


|Parameter Name |Type |Remarks |
|---|---|---|
|id |string/int64 |Primary key value |
|fields |map |Key is field name, value is field value |


<span id="afd1ef36"></span>
# Request Response Example


* Request parameters


```JSON
req_path = "/api/vikingdb/data/fetch_in_collection"
req_body = {
    "collection_name": "test_coll",
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
                }
            },
            {
                "id": "uid_002",
                "fields": {
                    "f_good_id": "uid_002", "f_text": "This is a cultural relic from the Qing Dynasty, dating back 300 years."
                }
            },
        ],
        "ids_not_exist": [
            "uid_005"
        ]
    }
}
```
