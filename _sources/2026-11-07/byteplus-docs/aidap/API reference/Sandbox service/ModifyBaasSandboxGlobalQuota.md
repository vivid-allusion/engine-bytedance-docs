---
title: "ModifyBaasSandboxGlobalQuota"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/modifybaassandboxglobalquota"
---

Call the ModifyBaasSandboxGlobalQuota API to modify the daily create sandbox quota for users. After modification, all users without customized quotas immediately follow the new default values.

## Request type

Synchronous request.

## Precautions

This API can only be used to operate the workspace using the Supabase engine.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyBaasSandboxGlobalQuota&serviceCode=aidap&version=2025-10-01&groupName=)

## Request parameters

|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |noble\-heath\-3a48\*\*\*\* |ID of the workspace. |
|BranchId |String |Yes |br\-merry\-scup\-42d3\*\*\*\* |Branch ID。 |
|UserDefaultQuota |Object of [BaasSandboxQuota](https://docs.byteplus.com/en/docs/330/124113#baassandboxquota) |Yes |Refer to the sample request. |Default user\-level quota configuration pending update. |

### BaasSandboxQuota

|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|DailySandboxLimit |Long |Yes |100 |Default daily creation limit, `-1` means no limit, `0` means creation is forbidden, positive integers represent the daily maximum. |

## Response parameters

null

## Sample

Sample request

```JSON
POST /?Action=ModifyBaasSandboxGlobalQuota&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "noble-heath-3a48****",
    "BranchId": "br-merry-scup-42d3****",
    "UserDefaultQuota": {
"DailySandboxLimit":1000
    }
}
```

Sample response

```JSON
{
  "ResponseMetadata": {
    "RequestId": "your-request-id",
    "Action": "ModifyBaasSandboxGlobalQuota",
    "Version": "2025-10-01",
    "Service": "aidap",
    "Region": "cn-beijing"
  },
  "Result": {}
}
```

## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
