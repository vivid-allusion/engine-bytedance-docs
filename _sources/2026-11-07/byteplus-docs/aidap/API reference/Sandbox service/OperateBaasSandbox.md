---
title: "OperateBaasSandbox"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/operatebaassandbox"
---

Call the OperateBaasSandbox API to stop the Sandbox compute.

## Request type

Synchronous request.

## Precautions

This API can only be used to operate the workspace using the Supabase engine.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=OperateBaasSandbox&serviceCode=aidap&version=2025-10-01&groupName=)

## Request parameters

|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |noble\-heath\-3a48\*\*\*\* |ID of the workspace. |
|BranchId |String |Yes |br\-merry\-scup\-42d3\*\*\*\* |Branch ID。 |
|SandboxId |String |Yes |35q6spfjixq54bxba4gadn\*\*\*\* |ID of the sandbox. |
|Operation |String |Yes |STOP |Operation type. Currently only supports the value `STOP` to stop and reclaim the Sandbox compute. |

## Response parameters

null

## Sample

Sample request

```JSON
POST /?Action=OperateBaasSandbox&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "noble-heath-3a48****",
    "BranchId": "br-merry-scup-42d3****",
    "SandboxId": "35q6spfjixq54bxba4gadn****",
    "Operation": "STOP"
}
```

Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202610261225326E20583AA10470CEBE5F-0191bc",
        "Action": "OperateBaasSandbox",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```

## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
