---
title: "Delete Vikingdb Collection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Delete_Collection_V2"
---

<span id="2a2d6ef5"></span>
# Overview

This interface is used to delete a specified collection

<span id="b936f63a"></span>
# Interface Upgrade Notes


* Corresponding V1 interface: https://docs.byteplus.com/en/docs/VikingDB/drop

* Usage differences:



| |V2 Interface |V1 Interface |
|---|---|---|
|Parameter Naming Style |CamelCase (`CollectionName`) |Underscore (`collection_name`) |


<span id="ab26a756"></span>
# Request API

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you can use AK, SK to construct a signature. Please refer to the <a href="https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2">Control Plane API Calling Process</a>, copy the calling example and fill in the necessary information.</div>


<span id="547159a2"></span>
## Request Parameters

Request parameter Action value: DeleteVikingdbCollection

The table below lists only the unique request parameters for this interface and some common parameters. For more information, see [Control Plane API Calling Process](https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2).


|Parameter |Type |Required |Description |
|---|---|---|---|
|ProjectName |String |No |Project name |
|CollectionName |String |Conditional |Collection name |
|ResourceId |String ||Collection resource ID. The request must specify either ResourceId or CollectionName. |


<span id="9eacd241"></span>
## Response Parameters

The table below lists only the unique response parameters for this interface. For more information, see [Control Plane API Calling Process](https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2).


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|Message |String |success |Operation result information |


<span id="ca0530a4"></span>
## Request Examples

```Plain
action = "DeleteVikingdbCollection",
body = {
    "ProjectName": "default",
    "CollectionName": "my_test_coll_1",
}
```


<span id="308482aa"></span>
## Response Examples

```Plain
{
  "ResponseMetadata": {
    "RequestId": "20250331204634101189204179056F1E",
    "Action": "DeleteVikingdbCollection",
    "Version": "2025-06-09",
    "Service": "vikingdb",
    "Region": "cn-beijing"
  },
  "Result": {
    "Message": "success"
  }
}
```


<span id="2211a3c8"></span>
## Error Codes

For common error codes, please refer to the [Common Error Codes](https://docs.byteplus.com/lwxm71ps/exr2na84) and [API V2 Error Codes and Troubleshooting Guide](https://docs.byteplus.com/lwxm71ps/odf7hlr6) documentation.
