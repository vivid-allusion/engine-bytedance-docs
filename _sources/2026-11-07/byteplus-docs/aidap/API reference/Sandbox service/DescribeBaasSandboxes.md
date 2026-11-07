---
title: "DescribeBaasSandboxes"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/describebaassandboxes"
---

Call the DescribeBaasSandboxes API to query the Sandbox compute running on the specified Branch of the specified workspace.

## Request type

Synchronous request.

## Precautions

This API can only be used to operate the workspace using the Supabase engine.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeBaasSandboxes&serviceCode=aidap&version=2025-10-01&groupName=)

## Request parameters

|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |noble\-heath\-3a48\*\*\*\* |ID of the workspace. |
|BranchId |String |Yes |br\-merry\-scup\-42d3\*\*\*\* |Branch ID。 |
|SandboxId |String |No |35q6spfjixq54bxba4gadn\*\*\*\* |Match exactly by sandbox ID. |
|OwnerUserId |String |No |System Admin |Match exactly by user ID who actually started the sandbox compute. |
|Status |String |No | <br><br>RUNNING |Sandbox compute status. Values:<br><br><br>* `CREATING`: Creating.<br><br>* `STARTING`: Starting.<br><br>* `RUNNING`: Running.<br><br>* `PAUSING`: Pausing.<br><br>* `Paused`: Paused.<br><br>* `Restoring`: Restoring.<br><br>* `Stopping`: Stopping.<br><br>* `Stopped`: Stopped.<br><br>* `Killed`: Reclaimed.<br><br>* `Failed`: Failed. |
|Offset |Integer |No |0 |Starting point for paginated query, an integer greater than or equal to 0, default value is 0. |
|Limit |Integer |No | <br><br>20 |Page size for paginated query, range 1 to 100, default value is 10, input 0 to use the default value. |
|TemplateName |String |No |opencode |Exact match by source template Name. Values:<br><br><br>* `opencode`<br><br>* `codex`<br><br>* `code-interpreter`<br><br>* `base` |

## Response parameters

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Total |Long | <br><br>1 |Total number of instances meeting full filter conditions. |
|Sandboxes |Array of [Sandbox](https://docs.byteplus.com/en/docs/330/124109#sandbox) |Refer to the sample response. |Sandbox list. |

### Sandbox

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|CpuMilli |Integer |2000 |CPU specifications, unit is milli\-core. |
|CreatedAt |String |2026\-10\-26T03:48:29Z |Creation time (UTC). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|EndedAt |String | |End time (UTC). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|FailReason |String | |Failure reason. Return is omitted when the sandbox status is not `Failed` or there is no failure reason. |
|MemMb |Integer |4096 |Memory specifications, unit: MB. |
|OwnerUserId |String |System Admin |User ID who actually started this sandbox compute. |
|RemainingTtlSeconds |Long |562 |Remaining TTL seconds; returns 0 if expired, not returned if TTL is not set. |
|SandboxId |String |35q6spfjixq54bxba4gadn\*\*\*\* |ID of the sandbox. |
|Status |String |RUNNING |Sandbox compute status. Values:<br><br><br>* `CREATING`: Creating.<br><br>* `STARTING`: Starting.<br><br>* `RUNNING`: Running.<br><br>* `PAUSING`: Pausing.<br><br>* `Paused`: Paused.<br><br>* `Restoring`: Restoring.<br><br>* `Stopping`: Stopping.<br><br>* `Stopped`: Stopped.<br><br>* `Killed`: Reclaimed.<br><br>* `Failed`: Failed. |
|TemplateName |String |opencode |Name of source template. |
|TimeoutAt |String |2026\-10\-26T04:03:30Z |Estimated timeout (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`. Not returned if TTL is not set. |
|UpdatedAt |String |2026\-10\-26T03:48:30Z |Last update time (UTC). Format: `yyyy-MM-ddTHH:mm:ssZ`. |

## Sample

### Sample request

```JSON
POST /?Action=DescribeBaasSandboxes&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "noble-heath-3a48****",
    "BranchId": "br-merry-scup-42d3****",
    "SandboxId": "35q6spfjixq54bxba4gadn****",
    "OwnerUserId": "System Admin",
    "Status": "RUNNING",
    "Offset": 0,
    "Limit": 20,
    "TemplateName": "opencode"
}
```

### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeBaasSandboxes",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "Sandboxes": [
            {
                "MemMb": 4096,
                "Status": "RUNNING",
                "EndedAt": "",
                "CpuMilli": 2000,
                "CreatedAt": "2026-10-26T03:48:29Z",
                "SandboxId": "35q6spfjixq54bxba4gadn****",
                "TimeoutAt": "2026-10-26T04:03:30Z",
                "UpdatedAt": "2026-10-26T03:48:30Z",
                "FailReason": "",
                "OwnerUserId": "System Admin",
                "TemplateName": "opencode",
                "RemainingTtlSeconds": 562
            }
        ],
        "Total": 1
    }
}
```

## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
