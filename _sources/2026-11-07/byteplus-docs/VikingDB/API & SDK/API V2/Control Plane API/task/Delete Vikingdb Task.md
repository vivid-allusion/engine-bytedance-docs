---
title: "Delete Vikingdb Task"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Delete_Task_V2"
---

<span id="edc17365"></span>
# Overview

This interface is used to delete specified offline tasks.

<span id="112a2c30"></span>
# Interface Upgrade Notes


* The corresponding V1 interface is:

* Usage differences:



| |V2 Interface |V1 Interface |
|---|---|---|
|Parameter Naming Style |Camel Case (TaskId) |Underscore (task_id) |


<span id="b610d803"></span>
# Request API

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you can use AK, SK to construct a signature. Please refer to the <a href="https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2">Control Plane API Calling Process</a>, copy the calling example, and fill in the necessary information.</div>


<span id="1e6f1486"></span>
## Request Parameters

Request parameter Action value: DeleteVikingdbTask

For more information, please see [Control Plane API Calling Process](https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2).


|Parameter |Type |Required |Description |
|---|---|---|---|
|TaskId |String |Yes |Task ID |


<span id="ab5ef9c5"></span>
## Response Parameters

For more information, please see [Control Plane API Calling Process](https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2)


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|Message |String |success |Information about the result of the operation |


<span id="1a8ce0c1"></span>
## Request Example

```Plain
action = "DeleteVikingdbTask",
body = {
  "TaskId": "7d8e122b-7870-5ff4-9be4-86a099cb7f64"
}
```


<span id="1e1708d6"></span>
## Response Example

```Plain
{
  "ResponseMetadata": {
    "RequestId": "2025060910180919118203304068EA18",
    "Action": "DeleteVikingdbTask",
    "Version": "2025-06-09",
    "Service": "vikingdb",
    "Region": "cn-beijing"
  },
  "Result": {
    "Message": "success"
  }
}
```


<span id="b4ad3e9c"></span>
## Error Codes

For common error codes, please refer to the [API V2 Error Codes and Troubleshooting Guide](https://docs.byteplus.com/docs/VikingDB/FAQnew).
