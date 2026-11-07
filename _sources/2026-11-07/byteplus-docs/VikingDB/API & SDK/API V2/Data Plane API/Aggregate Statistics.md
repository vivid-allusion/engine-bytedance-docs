---
title: "Aggregate Statistics"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Aggregate_Statistics_V2"
---

<span id="cc192755"></span>
# Overview

Aggregate statistics can group and aggregate specified fields, and add filtering operations to finally obtain corresponding aggregate statistical results, assisting in understanding data distribution and other situations.

<span id="0ffeaac6"></span>
# Interface Upgrade Notes


* Corresponding V1 interface: https://docs.byteplus.com/en/docs/VikingDB/Aggregate

* Usage differences:



| |V2 Interface |V1 Interface |
|---|---|---|
|Sub\-index |Sharding with stronger performance and usability is under development. Please stay tuned. |The partition parameter is specified. |


<span id="4eb07c15"></span>
# Request API

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you can use AK, SK to construct a signature. Please refer to the <a href="https://docs.byteplus.com/docs/VikingDB/Data_Plane_API_Calling_Process">Data Plane API Calling Process</a>, copy the calling example and fill in the necessary information.</div>



|URI |/api/vikingdb/data/agg |Uniform Resource Identifier |
|---|---|---|
|Method |POST |The type of operation requested by the client. |
|Request Header |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="2008a598"></span>
# Request Body Parameters


|Parameter Name |Type |Required |Remarks |
|---|---|---|---|
|resource_id |string |Choose 1 of 2 |Resource ID |
|collection_name |string ||Collection name |
|index_name |string |Yes |Index name |
|filter |map |No |Filter conditions, format shown below. Defaults to empty, no filtering |
|op |string |Yes |Currently only supports count. When using the count operator, the index must contain at least one scalar index field of string, int64, or bool type. |
|field |string |No |The name of the field to aggregate on. The field must be a scalar index field of type string, int64, or bool. |
|cond |map |No |This is similar to a SQL GROUP BY...HAVING clause and is only effective when a 'field' is specified. For the 'count' operator, this parameter supports 'gt', which returns only result items with a count greater than the threshold. |


<span id="c0bbc6ae"></span>
# Response Body Parameters

For public response body parameters, see

[Data Plane API Calling Process](https://docs.byteplus.com/docs/VikingDB/Data_Plane_API_Calling_Process)


|Parameter Name |Type |Sub\-parameter | |Description |
|---|---|---|---|---|
|result |map |agg |map |Aggregate results |
|| |op |string |The operator. Currently, only 'count' is supported. |
|| |field |string |The field set in the request. If not specified, the value is "**NONE**". |


<span id="20e7bb92"></span>
# Request Response Examples

<span id="a8a7ffaf"></span>
## 1. View Total Data Count in Index


* Request Parameters


```JSON
req_path = "/api/vikingdb/data/agg"
req_body = {
    "collection_name": "test_coll",
    "index_name": "idx_1",
    "op": "count",
}
```



* Response Parameters


```JSON
{
    "code": "Success",
    "message": "The API call was executed successfully.",
    "request_id": "02175438839168500000000000000000000ffff0a003ee4fc3499",
    "result": {
        "op": "count",
        "field": "__NONE__",
        "agg": {
            "__TOTAL__": 4000000
        }
    }
}
```


<span id="c425df67"></span>
## 2. Aggregate Statistics by Field


* Request Parameters


```JSON
req_path = "/api/vikingdb/data/agg"
req_body = {
    "collection_name": "test_coll",
    "index_name": "idx_1",
    "op": "count",
    "field": "city",
    "cond": {
        "gt": 900
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
        "field": "city",
        "op": "count",
        "agg": {
            "beijing": 1001,
            "shanghai": 999,
        }
    }
}
```
