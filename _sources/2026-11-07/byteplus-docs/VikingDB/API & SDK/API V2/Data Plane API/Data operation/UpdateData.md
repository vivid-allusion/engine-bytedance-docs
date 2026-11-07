---
title: "UpdateData"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/UpdateData_V2"
---

<span id="28cfff14"></span>
# Overview

To modify existing data entries in your collection, you can use this API to update specific fields. It supports partial updates for text, scalar, and vector field types.

<span id="5afc9656"></span>
# API Upgrade Notes


* The corresponding V1 API is: https://docs.byteplus.com/en/docs/VikingDB/update_data

* Usage differences:



| |V2 API |V1 API |
|---|---|---|
|Parameter for writing data |data |fields |
|Model token consumption handling |Automatically returned |Must be manually set |
|Limit on data volume per write operation |If vectorization is enabled for the dataset, the limit is 1 data entry per request for lower latency. If vectorization is not enabled, the limit is 100 data entries. |No more than 100. |



* Note: QPS rate limiting is calculated based on the number of data entries, and the rate limiting behavior of V1 and V2 APIs is exactly the same.


<span id="901343e5"></span>
# Request API

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you can use AK, SK to construct a signature. Please refer to the <a href="https://docs.byteplus.com/docs/VikingDB/Data_Plane_API_Calling_Process">Data Plane API Calling Process</a>, copy the calling example and fill in the necessary information.</div>


<span id="8c1d2309"></span>
# Request API


|URI |/api/vikingdb/data/update |Uniform Resource Identifier |
|---|---|---|
|Method |POST |The type of operation the client requests from the vector database server |
|Request Headers |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="35e97e10"></span>
# Request Body Parameters


|Parameter Name |Type |Required |Default Value |Remarks |
|---|---|---|---|---|
|resource_id |string |One of these two parameters is required. |*  |Resource ID |
|collection_name |string ||*  |Collection name |
|data |array |Yes |*  |The number of data entries written per request cannot exceed 100.<br><br>Each data entry is represented as a map, where the key is the field name and the value is the field value. The format of field values for different field types is shown in the table below.<br><br>Note:<br><br><br>* Writing non\-existent field names is not allowed.<br><br>* If a field is missing, it will be filled with a default value. If the field type has no default value (such as text), the request will fail.<br><br>* If the request parameters are invalid (4xx type), the entire operation will fail. |
||||||
|ttl |int |No |0 |Must be a non\-negative integer.<br><br>A value of 0, which is the default, indicates that the data does not expire.<br><br>For example, a value of 86400 deletes the data after one day.<br><br>Data TTL deletion will not immediately update the index. |


Note:


* Data can include a subset of fields, but it must include the primary key.

* Asynchronous writing is not currently supported


<span id="1978d160"></span>
# Response Body Parameters

For common response body parameters, see

[Data Plane API Calling Process](https://docs.byteplus.com/docs/VikingDB/Data_Plane_API_Calling_Process)
