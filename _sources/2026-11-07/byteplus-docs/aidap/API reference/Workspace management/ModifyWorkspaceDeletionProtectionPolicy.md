---
title: "ModifyWorkspaceDeletionProtectionPolicy"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/ModifyWorkspaceDeletionProtectionPolicy"
---

Call the ModifyWorkspaceDeletionProtectionPolicy API to enable or disable deletion protection for the workspace.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |noble\-heath\-3a48\*\*\*\* |ID of the workspace. |
|DeletionProtection |String |Yes |Enabled |Workspace AP acceleration status. Currently only supports the value `Enabled`, which means enabling AP acceleration.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default">Currently, only enabling AP acceleration is supported, and disabling it after enabling is not supported.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=ModifyWorkspaceDeletionProtectionPolicy&Version=2025-10-01 HTTP/1.1
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "noble-heath-3a48****",
    "DeletionProtection": "Disabled"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyWorkspaceDeletionProtectionPolicy",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
