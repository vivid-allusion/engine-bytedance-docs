---
title: "Update Vikingdb Task"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Update_Task_V2"
---

<span id="ab396174"></span>
# Overview

This interface is used to update specified offline tasks.

<span id="6167e390"></span>
# Interface Upgrade Notes


* The corresponding V1 interface is:

* Usage differences:



| |V2 Interface |V1 Interface |
|---|---|---|
|Parameter Naming Style |Camel Case (TaskId) |Underscore (`index_name`) |


<span id="c456d7b5"></span>
# Request API

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you can use AK, SK to construct a signature. Please refer to the <a href="https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2">Control Plane API Calling Process</a>, copy the calling example and fill in the necessary information.</div>


<span id="b100ac5b"></span>
## Request Parameters

Request parameter Action value: UpdateVikingdbTask

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see[Control Plane API Calling Process](https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2).


|Parameter |Type |Required |Description |
|---|---|---|---|
|TaskId |String |Yes |Task ID |
|TaskStatus |String |Yes |Only tasks in a state that allows confirmation can be updated to 'confirmed'. |


<span id="3dcdd2ed"></span>
## Response Parameters

The table below lists only the specific response parameters for this interface. For more information, please see[Control Plane API Calling Process](https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2)


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|Message |String |success |A message indicating the result of the operation. |


<span id="97b30b99"></span>
## Request Example

```Plain
action = "UpdateVikingdbTask",
body = {
  "TaskId": "a7n44e7Y",
  "TaskStatus": "confirmed"
}
```


<span id="2f26b6a5"></span>
## Response Example

```Plain
{
  "ResponseMetadata": {
    "RequestId": "2025060910243616613011919613C0B7",
    "Action": "UpdateVikingdbTask",
    "Version": "2025-06-09",
    "Service": "vikingdb",
    "Region": "cn-beijing"
  },
  "Result": {
    "Message": "success"
  }
}
```


<span id="ebe11e14"></span>
## Error Codes

For common error codes, please refer to the [API V2 Error Codes and Troubleshooting Guide](https://docs.byteplus.com/docs/VikingDB/FAQnew)guide.
