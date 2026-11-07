---
title: "DeleteTrigger"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/DeleteTrigger"
---

Delete trigger

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the region where your resources are located. For details, see [Service address](https://docs.byteplus.com/en/docs/cp/Service_Addresses).


* Request method: POST

* Request URL: https://cp.ap\-southeast\-1.byteplusapi.com.cn?Action=DeleteTrigger&Version=2023\-05\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |DeleteTrigger |The API name. The name of the current API is `DeleteTrigger`. |
|Version |String |Yes |2023\-05\-01 |The API version. The current version of the API is `2023-05-01`. |
|WorkspaceId |String |Yes |7d496c3d189a311676\*\*\*\* |The workspace of the trigger. |
|PipelineId |String |Yes |0f7ca5e80f4c3cfd116\*\*\*\* |ID of the pipeline to which the trigger belongs. |
|Id |String |Yes |5281de81202023151c0c\*\*\*\* |Trigger ID. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cp.ap-southeast-1.byteplusapi.com.cn?Action=DeleteTrigger&Version=2023-05-01 HTTP/1.1
Content-Type: application/json
{
    "WorkspaceId": "7d496c3d189a311676****",
    "PipelineId": "0f7ca5e80f4c3cfd116****",
    "Id": "5281de81202023151c0c****"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This interface does not have any specific return parameters.

<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "202404071710430739950998FB2847****",
        "Action": "DeleteTrigger",
        "Version": "2023-05-01",
        "Service": "cp",
        "Region": "ap-southeast-1"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This API currently does not have independent error codes. If an error occurs during API invocation, refer to the [public error codes](https://docs.byteplus.com/en/docs/cp/Public_error_codes) for troubleshooting.
