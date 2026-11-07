---
title: "DescribeBaasSandboxGlobalQuota"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/describebaassandboxglobalquota"
---

Call the DescribeBaasSandboxGlobalQuota API to query the user's daily create sandbox compute quota, which is the global default value used when the user\-level customize quota is not set.

## Request type

Synchronous request.

## Precautions

This API can only be used to operate the workspace using the Supabase engine.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeBaasSandboxGlobalQuota&serviceCode=aidap&version=2025-10-01&groupName=)

## Request parameters

|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |noble\-heath\-3a48\*\*\*\* |ID of the workspace. |
|BranchId |String |Yes |br\-merry\-scup\-42d3\*\*\*\* |Branch ID。 |

## Response parameters

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|UserDefaultQuota |Object of [BaasSandboxQuota](https://docs.byteplus.com/en/docs/330/124112#baassandboxquota) |Refer to the sample response. |Default user quota configuration. |

### BaasSandboxQuota

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|DailySandboxLimit |Long |100 |Default daily create quota, `-1` means no limit, `0` means creation is prohibited, positive integers indicate the daily limit. |

## Sample

Sample request

```JSON
POST /?Action=DescribeBaasSandboxGlobalQuota&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "noble-heath-3a48****",
    "BranchId": "br-merry-scup-42d3****"
}
```

Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2026102612244438BF5547B7586E327A65-f1e1c8",
        "Action": "DescribeBaasSandboxGlobalQuota",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "UserDefaultQuota": {
            "DailySandboxLimit": 0
        }
    }
}
```

## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
