---
title: "RecoverDelayedDeleteWorkspace"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/RecoverDelayedDeleteWorkspace"
---

Call the RecoverDelayedDeleteWorkspace API to recover the Workspace in **Latency deleting** status.

## Request type

Asynchronous request.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=RecoverDelayedDeleteWorkspace&serviceCode=aidap&version=2025-10-01&groupName=)

## Request parameters

|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |noble\-heath\-3a48\*\*\*\* |ID of the workspace. |

## Response parameters

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|WorkspaceId |String |noble\-heath\-3a48\*\*\*\* |ID of the workspace. |

## Sample

### Sample request

```JSON
POST /?Action=RecoverDelayedDeleteWorkspace&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "noble-heath-3a48****"
}
```

### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteWorkspace",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "WorkspaceId": "noble-heath-3a48****"
    }
}
```

## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
