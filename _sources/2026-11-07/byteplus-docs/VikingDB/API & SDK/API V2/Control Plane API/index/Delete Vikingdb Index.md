---
title: "Delete Vikingdb Index"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Delete_Index_V2"
---

<span id="f6304bb3"></span>
# Overview

To delete a specified index from a collection in VikingDB, you can call the `DeleteVikingdbIndex` API. This reference provides the required request parameters, response details, and request examples to guide your implementation.

<span id="5a2c62df"></span>
# Interface Upgrade Notes


* The corresponding V1 interface is: https://docs.byteplus.com/en/docs/VikingDB/drop1

* Usage differences:



| |V2 Interface |V1 Interface |
|---|---|---|
|Parameter naming style |CamelCase (`IndexName`) |Underscore (`index_name`) |



* Note: QPS rate limiting is calculated based on the number of data entries, and the rate limiting behavior of V1 and V2 interfaces is identical.


<span id="78e2ee8c"></span>
# Request API

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you can use AK, SK to construct a signature. Refer to the Control Plane API Calling Process, copy the calling example, and fill in the necessary information.</div>


<span id="3f577f5e"></span>
## Request Parameters

The value of the Action request parameter is DeleteVikingdbIndex.

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see the  Control Plane API Calling Process.


|Parameter |Type |Required |Description |
|---|---|---|---|
|ProjectName |String |No |Project name |
|CollectionName |String |Conditional |Dataset name |
|ResourceId |String ||Dataset resource ID. The request must specify either ResourceId or CollectionName. |
|IndexName |String |Yes |Index name |


<span id="b66b619c"></span>
## Response Parameters

The table below only lists the response parameters specific to this interface. For more information, please see [Control Plane API Calling Process](https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2).


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|Message |String |success |A message indicating the operation result |


<span id="7e874be9"></span>
## Request Example

```Plain
action = "DeleteVikingdbIndex"
body = {
  "CollectionName": "test_coll",
  "IndexName": "test_coll_index"
}
```


<span id="aa67307d"></span>
## Response Example

```Plain
{
  "ResponseMetadata": {
    "RequestId": "20250527175218115212119089A5D56A",
    "Action": "DeleteVikingdbIndex",
    "Version": "2025-06-09",
    "Service": "vikingdb",
    "Region": "cn-beijing"
  },
  "Result": {
    "Message": "success"
  }
}
```


<span id="d4acf88e"></span>
## Error Codes

For error codes, please refer to the  Common Error Codes.
