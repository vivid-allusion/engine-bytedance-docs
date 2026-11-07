---
title: "DeleteData"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/DeleteData_V2"
---

<span id="8cb8d0a9"></span>
# Overview

To delete data from a specified collection, you can use this API to remove specific entries by their primary keys or clear all data within the collection. Please note that there is a delay in updating the index after deletion, which means the data may still be retrievable for a brief period.

<span id="be060813"></span>
# API Upgrade Notes


* The corresponding V1 API is: https://docs.byteplus.com/en/docs/VikingDB/del_data

* Usage differences:



| |V2 API |V1 API |
|---|---|---|
|Parameter name for specifying primary key |ids |primary_keys |


<span id="041f2915"></span>
# Request API

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you can use AK, SK to construct a signature. Please refer to the <a href="https://docs.byteplus.com/docs/VikingDB/Data_Plane_API_Calling_Process">Data Plane API Calling Process</a>, copy the calling example and fill in the necessary information.</div>



|URI |/api/vikingdb/data/delete |Uniform Resource Identifier |
|---|---|---|
|Method |POST |The type of operation the client requests from the vector database server |
|Request Headers |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="dc99e7bf"></span>
# Request Body Parameters


|Parameter Name |Type |Required |Remarks |
|---|---|---|---|
|resource_id |string |Choose 1 of 2 |Resource ID |
|collection_name |string ||Collection name |
|ids |list |Choose 1 of 2 |List of primary keys for data to be deleted. Maximum 100 entries.<br><br>Note:<br><br><br>* If the request parameters are invalid (4xx type), the entire operation will fail. |
|||||
|del_all |bool ||When set to true, deletes all data; defaults to false.<br><br>This API deletes all data, but this deletion is not immediately synchronized with the index. Therefore, for a period of time (about 5 minutes), the data can still be retrieved from the index. |


<span id="2bae2cc1"></span>
# Response Body Parameters

Refer to the[Data Plane API Calling Process](https://docs.byteplus.com/docs/VikingDB/Data_Plane_API_Calling_Process)

<span id="fc383d49"></span>
# Request Response Example


* Request parameters


```JSON
req_path = "/api/vikingdb/data/delete"
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
    "result": null
}
```
