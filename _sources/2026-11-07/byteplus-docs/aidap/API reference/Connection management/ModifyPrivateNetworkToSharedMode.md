---
title: "ModifyPrivateNetworkToSharedMode"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/ModifyPrivateNetworkToSharedMode"
---

Call the ModifyPrivateNetworkToSharedMode API to set the workspace’s shared mode.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* You need to set up a Virtual Private Cloud for your Workspace first; otherwise, switching is not supported. Call the [DescribeWorkspaceDetail](https://docs.byteplus.com/en/docs/aidap/DescribeWorkspaceDetail) API to view the workspace’s Virtual Private Cloud configuration.

* Switching again is not supported after changing to shared mode. You can call the [DescribeWorkspaceDetail](https://docs.byteplus.com/en/docs/aidap/DescribeWorkspaceDetail) API to check the shared mode of the workspace’s Virtual Private Cloud.

* This feature is an invited test feature. If you need to use them, [submit a ticket](https://console.byteplus.com/workorder/create) to apply.


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |noble\-heath\-3a48\*\*\* |ID of the workspace. |
|SharedPrivateWildcardDomain |String |No |Disabled |Whether to enable Virtual Private Cloud sharing mode for workspace. After enabling, the workspace supports wildcard domain access, and does not add new resolution records for each compute node. Values:<br><br><br>* `Enabled`: enabled.<br><br>* `Disabled`: disabled. Default value. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=ModifyPrivateNetworkToSharedMode&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "noble-heath-3a48***",
    "SharedPrivateWildcardDomain": "Disabled"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyPrivateNetworkToSharedMode",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": null
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
