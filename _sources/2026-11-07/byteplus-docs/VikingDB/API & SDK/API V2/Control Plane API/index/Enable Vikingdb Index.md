---
title: "Enable Vikingdb Index"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/enable"
---

<span id="overview"></span>
# Overview

To enable a specified VikingDB index that is in a 'Disabled' status, you can use this API. After the index is enabled, it will be rebuilt and consume compute resources. Once the rebuilding is complete, the index can be used normally. To perform the opposite action, see Disable Vikingdb Index.

<span id="request-api"></span>
# Request API

When requesting the OpenAPI interface of the vector database VikingDB, you can use AK, SK to construct a signature. For details, refer to [Control Plane API Calling Process](https://docs.byteplus.com/en/docs/VikingDB/Control_Plane_API_V2,). Copy the calling example and fill in the required information.

<span id="request-parameters"></span>
## Request Parameters

Request parameter Action: EnableVikingdbIndex.

The table below lists only the unique request parameters for this API and some common parameters. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/directconnect/Public-parameters.)


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
action = "EnableVikingdbIndex"
body = {
  "CollectionName": "aaa"
  "IndexName": "5J"
}
```


<span id="response-example"></span>
## Response Example

```Plain
{
  "ResponseMetadata": {
    "RequestId": "202512261424270210401601790C2F23",
    "Action": "EnableVikingdbIndex",
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

For error codes, refer to [Common Error Codes](https://docs.byteplus.com/en/docs/VikingDB/FAQ_common).
