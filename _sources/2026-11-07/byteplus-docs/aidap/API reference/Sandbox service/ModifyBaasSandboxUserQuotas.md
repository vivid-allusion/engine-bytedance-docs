---
title: "ModifyBaasSandboxUserQuotas"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/modifybaassandboxuserquotas"
---

Call the ModifyBaasSandboxUserQuotas API to modify the user's sandbox quota and usage.

## Request type

Synchronous request.

## Precautions

This API can only be used to operate the workspace using the Supabase engine.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyBaasSandboxUserQuotas&serviceCode=aidap&version=2025-10-01&groupName=)

## Request parameters

|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |noble\-heath\-3a48\*\*\*\* |ID of the workspace. |
|BranchId |String |Yes |br\-merry\-scup\-42d3\*\*\*\* |Branch ID。 |
|UserQuotaItems |Array of [BaasSandboxUserQuotaItem](https://docs.byteplus.com/en/docs/330/124115#baassandboxuserquotaitem) |Yes |Refer to the sample request. |List of user quota items to be modified, containing at least one item, fields are detailed in the structure below. |

### BaasSandboxUserQuotaItem

|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|UserId |String |Yes |7b973f0e\-\*\*\*\* |Unique identifier of the User to be modified. Not empty, and cannot be a System account. |
|CustomQuota |Object of [BaasSandboxQuota](https://docs.byteplus.com/en/docs/330/124115#baassandboxquota) |No |Refer to the sample request. |Customize quota configuration. Only required when QuotaCustomized is `true`; must not be provided when QuotaCustomized is `false`. |
|QuotaCustomized |Boolean |Yes |true |Whether to set a customized quota. Values:<br><br><br>* `true`: Yes.<br><br>* `false`: No. Indicates restoring to follow the global default value. |

### BaasSandboxQuota

|**Parameter** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|DailySandboxLimit |Long |Yes |100 |Default daily create quota, `-1` means no limit, `0` means creation is prohibited, positive integers indicate the daily limit. |

## Response parameters

null

## Sample

Sample request

```JSON
POST /?Action=ModifyBaasSandboxUserQuotas&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
  "WorkspaceId": "ideal-fir-9fc8****",
  "BranchId": "br-2f4c****",
  "UserQuotaItems": [
    {
      "UserId": "7b973f0e-****",
      "QuotaCustomized": true,
      "CustomQuota": {
        "DailySandboxLimit": 20
      }
    },
    {
      "UserId": "1e2d3c4b-****",
      "QuotaCustomized": false
    }
  ]
}
```

Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyBaasSandboxUserQuotas",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    }
}
```

## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
