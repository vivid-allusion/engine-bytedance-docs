---
title: "DeletePipeline"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/DeletePipeline"
---

Delete the specified pipeline under the specified workspace.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, we recommend that you select the service address that corresponds to the Region where your resources are located. For details, see [service address](https://docs.byteplus.com/en/docs/cp/Service_Addresses).


* Request method: POST

* Request URL: https://cp.cn\-beijing.byteplusapi.com.cn?Action=DeletePipeline&Version=2023\-05\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |DeletePipeline |The API name. The name of the current API is `DeletePipeline`. |
|Version |String |Yes |2023\-05\-01 |The API version. The current version of the API is `2023-05-01`. |
|WorkspaceId |String |Yes |3f5f09a059124d6898a8543e678f\*\*\*\* |Workspace ID. |
|Id |String |Yes |016254aba6f14bdcb69e32022b48\*\*\*\* |Pipeline ID. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cp.cn-beijing.byteplusapi.com.cn?Action=DeletePipeline&Version=2023-05-01 HTTP/1.1
Content-Type: application/json
{
    "WorkspaceId": "3f5f09a059124d6898a8543e678f****",
    "Id": "016254aba6f14bdcb69e32022b48****"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This interface has no specific return parameters.

<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "202404031138595E5D8BD124299EB9****",
        "Action": "DeletePipeline",
        "Version": "2023-05-01",
        "Service": "cp",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This API does not have independent error codes. If an exception occurs during an API call, refer to [common error codes](https://docs.byteplus.com/en/docs/cp/Public_error_codes) for troubleshooting.
