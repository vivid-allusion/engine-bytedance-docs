---
title: "DeleteWorkspace"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/DeleteWorkspace"
---

Delete a workspace.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the appropriate service address based on the region where your resources are deployed. For details, see [Service addresses](https://docs.byteplus.com/en/docs/cp/Service_Addresses).


* Request method: POST

* Request URL: https://cp.ap\-southeast\-1.byteplusapi.com.cn?Action=DeleteWorkspace&Version=2023\-05\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |DeleteWorkspace |The API name. The name of the current API is `DeleteWorkspace`. |
|Version |String |Yes |2023\-05\-01 |The API version. The current version of the API is `2023-05-01`. |
|Id |String |Yes |2c7a85e4ac034eb790b096705694\*\*\*\* |Workspace ID. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cp.ap-southeast-1.byteplusapi.com.cn?Action=DeleteWorkspace&Version=2023-05-01 HTTP/1.1
Content-Type: application/json
{
    "Id": "2c7a85e4ac034eb790b096705694****"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This interface does not have any unique return parameters.

<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "202404031138595E5D8BD124299EB9****",
        "Action": "DeleteWorkspace",
        "Version": "2023-05-01",
        "Service": "cp",
        "Region": "ap-southeast-1"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This API currently does not have dedicated error codes. If an exception occurs when calling the API, refer to [public error codes](https://docs.byteplus.com/en/docs/cp/Public_error_codes) for troubleshooting.
