---
title: "Disable Vikingdb Index"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/disable"
---

<span id="overview"></span>
# Overview

This API disables a specified index that is in Ready status. After the index is disabled, related memory resources will be released and the index cannot be used. If you want to use the index again, you must enable it. To enable an index, see Enable Vikingdb Index.

<span id="request-api"></span>
# Request API

When requesting the OpenAPI interface of the vector database VikingDB, you can use AK, SK to construct a signature. For details, refer to [Control Plane API Calling Process](https://docs.byteplus.com/en/docs/VikingDB/Control_Plane_API_V2,). Copy the calling example and fill in the required information.

<span id="request-parameters"></span>
## Request Parameters

Request parameter Action: DisableVikingdbIndex.

The table below lists the request parameters that are unique to this API, as well as some common parameters.


|Parameter |Type |Required |Description |
|---|---|---|---|
|ProjectName |String |No |Project name |
|CollectionName |String |Choose 1 of 2 |Collection name |
|ResourceId |String | |Collection resource ID. The request must specify either ResourceId or CollectionName. |
|IndexName |String |Yes |Index name |


<span id="response-parameters"></span>
## Response Structure

The table below lists only the unique response parameters for this API. For more information, see [Response Structure](https://docs.byteplus.com/en/docs/directconnect/Responses).


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|Message |String |success |Operation result message |


<span id="request-example"></span>
## Request Example

```Plain
action = "DisableVikingdbIndex"
body = {
  "CollectionName": "aa",
  "IndexName": "Zfg0D"
}
```


<span id="response-example"></span>
## Response Example

```Plain
{
  "ResponseMetadata": {
    "RequestId": "20251226143245108247224207F9BA68",
    "Action": "DisableVikingdbIndex",
    "Version": "2025-06-09",
    "Service": "vikingdb_stg",
    "Region": "cn-beijing"
  },
  "Result": {
    "Message": "success"
  }
}
```


<span id="error-codes"></span>
## Error Codes

For error codes, refer to [Common Error Codes](https://docs.byteplus.com/en/docs/VikingDB/FAQ_common)
