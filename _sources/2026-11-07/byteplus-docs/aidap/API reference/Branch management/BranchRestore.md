---
title: "BranchRestore"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/BranchRestore"
---

Call the BranchRestore API to restore branch data to a specific time.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

This API can only be used to operate a workspace using the PostgreSQL engine or Supabase engine.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=BranchRestore&serviceCode=aidap&version=2025-10-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |noble\-heath\-3a48\*\*\*\* |ID of the workspace. |
|BranchId |String |Yes |br\-merry\-scup\-42d3\*\*\*\* |Branch ID. |
|RestoreSettings |Object of [RestoreSettings](https://docs.byteplus.com/en/docs/330/84422#restoresettings) |Yes |Refer to the sample request. |Data recovery configuration. |


<span id="restoresettings"></span>
### RestoreSettings


|**Name** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|Time |String |No |2025\-10\-08T15:03:01Z |Target time point for restore data (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|SourceBranchId |String |No |br\-blush\-seal\-09a7\*\*\*\* |Data source branch for restoration.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">if not provided, the branch specified by branch ID will be restored.</div><br> |
|SkipDBRolesAndCredentialsRollback |Boolean |No |true |Whether to skip database roles (DB Roles) and account password (Credentials). Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. Default value. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|BackupBranchID |String |br\-fleet\-cat\-2068\*\*\*\* |ID of the restored new branch. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=BranchRestore&Version=2025-10-01 HTTP/1.1
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "frank-melon-9dd3****",
    "BranchId": "br-sharp-ibis-3eea****",
    "RestoreSettings":{
        "Time":"2025-10-21T07:48:00Z",
        "SourceBranchId":"br-blush-seal-09a7****"
    }
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "BranchRestore",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "BackupBranchID": "br-deft-carp-3d43****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
