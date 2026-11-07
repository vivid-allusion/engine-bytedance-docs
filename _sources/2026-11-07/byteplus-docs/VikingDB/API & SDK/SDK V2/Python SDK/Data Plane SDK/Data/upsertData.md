---
title: "upsertData"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/upsertData_v2"
---

<span id="overview"></span>
# Overview

This interface is used to write data into a specified Collection. The data to be written is specified as a map, allowing insertion of one or multiple data entries at a time. A maximum of 100 data entries can be inserted in a single request. If the provided primary key already exists, the corresponding data will be updated; otherwise, new data will be inserted.

Adjustments have been made to the V2 version of the UpsertData interface (only affecting **datasets requiring vectorization** with **vectorize** configuration; datasets already with vector type fields are not affected). Key information is as follows:


* For dataset writes with **vectorize** configuration, embedding calculation will be changed from real\-time synchronous to background asynchronous execution, resulting in some latency for data to take effect;

* Write failure error messages can be viewed on the "Log Management" page of the Vector Database Console;

* The response body parameter no longer returns the `token_usage` field.


<span id="request-body-parameters"></span>
# Request Body Parameters


|Name |Type |Description |Required |
|---|---|---|---|
|collection_name |str |Name of the Collection, either this or resource_id must be provided. |Either one is required |
|resource_id |str |Resource ID of the Collection. | |
|data |List[Dict[str, Any]] |List of data to be written, maximum 100 entries per request, each must contain the primary key field. |Yes |
|ttl |int |Time\-to\-live of the data, in seconds. The system automatically deletes it after expiration. |No |
|async_write |bool |**For datasets "requiring vectorization":**  This parameter only distinguishes whether to perform streaming updates.<br><br><br>* async_write=false, triggers streaming index update after asynchronous write takes effect<br><br>* async_write=true, does not trigger streaming index update even after asynchronous write takes effect<br><br><br>**For datasets "with existing vector data":**  Asynchronous write switch.<br><br><br>* Asynchronous write rate limit threshold is 10 times that of synchronous write<br><br>* Asynchronously written data will not be synchronously written to the collection in real\-time, with latency at the minute level. Use the `FetchDataInCollection` interface to confirm whether data has been written to the collection<br><br>* Asynchronously written data will not trigger streaming index updates, index synchronization time is at the hour level. Use the `FetchDataInIndex` interface to confirm whether data has been synchronized to the index |No |


<span id="data-parameter-field-value-format"></span>
# data Parameter Field Value Format

Note: The primary key cannot be 0 when inserting data.


|Field Type |Format |Description |
|---|---|---|
|int64 |Integer value |Integer |
|float32 |Floating point value |Floating point number |
|string |String |String. Content limit is 256 bytes |
|bool |true/false |Boolean type |
|list |String array |String array |
|list |Integer array |Integer array |
|vector |* Vector (array of floats)<br><br>* Base64 encoding after float32/float64 compression to bytes |Dense vector |
|sparse_vector |List of dictionaries in input format, used to represent non\-zero subscripts of sparse vectors and their corresponding values, where token_id is of string type and token_weight is of float type |Sparse vector |
|text |String |If it's a vectorization field, the value cannot be empty. (Otherwise, it can be empty) |
|image |Object |If it's a vectorization field, the value cannot be empty. (Otherwise, it can be empty)<br><br><br>* Image TOS link `tos://{bucket}/{object}`<br><br>* http/https format link |
|video |Object |{<br><br>"value": `tos://{bucket}/{object}` or http/https format URL link (required)<br><br>"fps": 0.2 (value range 0.2\-5, optional)<br><br>} |
|date_time |string |Minute level:<br><br>`yyyy-MM-ddTHH:mmZ` or `yyyy-MM-ddTHH:mm±HH:mm`<br><br>Second level:<br><br>`yyyy-MM-ddTHH:mm:ssZ` or `yyyy-MM-ddTHH:mm:ss±HH:mm`<br><br>Millisecond level:<br><br>`yyyy-MM-ddTHH:mm:ss.SSSZ` or `yyyy-MM-ddTHH:mm:ss.SSS±HH:mm`<br><br>Example: "2025\-08\-12T11:33:56+08:00" |
|geoPoint |string |Geographic coordinates `longitude,latitude`, where `longitude` range is (\-180,180) and `latitude` range is (\-90,90)<br><br>Example: "116.408108,39.915023" |


<span id="created-time-type-field-date-time"></span>
## Created Time Type Field (date_time)

Only one of the following formats can be used, all following the RFC3339 standard (https://datatracker.ietf.org/doc/html/rfc3339)

Example: "2025\-08\-12T12:34:56+08:00"


| |Format(string) |Example |Description |
|---|---|---|---|
|Minute level |`yyyy-MM-ddTHH:mmZ` (UTC time) or<br><br>`yyyy-MM-ddTHH:mm±HH:mm` (specified time zone) |* `2025-08-12T04:34Z`<br><br>* `2025-08-12T12:34+08:00` |The examples on the left will both be parsed as Beijing time `2025-08-12` `12:34:00`. |
|Second level |`yyyy-MM-ddTHH:mm:ssZ` (UTC time) or<br><br>`yyyy-MM-ddTHH:mm:ss±HH:mm` (specified time zone) |* `2025-08-12T04:34:56Z`<br><br>* `2025-08-12T12:34:56+08:00` |The examples on the left will both be parsed as Beijing time `2025-08-12` `12:34:56`. |
|Millisecond level |`yyyy-MM-ddTHH:mm:ss.SSSZ` (UTC time) or<br><br>`yyyy-MM-ddTHH:mm:ss.SSS±HH:mm` (with time zone) |* `2025-08-12T04:34:56.147Z`<br><br>* `2025-08-12T12:34:56.147+08:00` |The examples on the left will both be parsed as Beijing time `2025-08-12` `12:34:56.147`. |


<span id="response-parameters"></span>
# Response Parameters

The response body contains common parameters (see "Response Body Common Parameters Description" below).

<span id="response-body-common-parameters-description"></span>
## Response Body Common Parameters Description


|Parameter Name |Type |Description |
|---|---|---|
|request_id |string |Request ID. |
|code |string |Operation status code. `Success` for success, otherwise an error code phrase. |
|message |string |Execution information. `The API call was executed successfully.` for success, otherwise an error message. |
|result |map |Operation result. If no data needs to be returned, `result = null`. |


<span id="request-example-code"></span>
# **Request Example Code**

```python
import os
import time

from vikingdb import IAM
from vikingdb.vector import UpsertDataRequest, VikingVector

auth = IAM(
    ak=os.environ["VIKINGDB_AK"],
    sk=os.environ["VIKINGDB_SK"],
)
client = VikingVector(
    host=os.environ["VIKINGDB_HOST"],
    region=os.environ["VIKINGDB_REGION"],
    auth=auth,
    scheme="https",
)

collection_client = client.collection(collection_name=os.environ["VIKINGDB_COLLECTION"])

payload = {
    "title": "Python upsert demo",
    "score": 42.5,
    "text": "示例负载，省略其余业务字段",
}
request = UpsertDataRequest(
    data=[payload],
    async_write=False,
)
response = collection_client.upsert(request)
print(f"request_id={response.request_id}")
if response.result:
    print(response.result.token_usage)
```
