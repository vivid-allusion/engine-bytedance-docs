---
title: "DescribeBaasSandboxUserSummaries"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/describebaassandboxusersummaries"
---

Call the DescribeBaasSandboxUserSummaries API to query the user's sandbox compute quota and usage.

## Request type

Synchronous request.

## Precautions

This API can only be used to operate the workspace using the Supabase engine.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeBaasSandboxUserSummaries&serviceCode=aidap&version=2025-10-01&groupName=)

## Request parameters

|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |noble\-heath\-3a48\*\*\*\* |ID of the workspace. |
|BranchId |String |Yes |br\-merry\-scup\-42d3\*\*\*\* |Branch ID。 |
|Offset |Integer |No |0 |Starting point for paginated query, an integer greater than or equal to 0, default value is 0. |
|Limit |Integer |No |20 |Number of returned items per page for paged queries. Range: 1–100. Default: 10. Passing 0 uses the default value. |
|Search |String |No |alice |User search keywords support fuzzy matching for User ID, User name, Email, or Phone number. |

## Response parameters

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Total |Long | <br><br>1 |Total number of users matching the query criteria. |
|UserSummaryItems |Array of [BaasSandboxUserSummaryItem](https://docs.byteplus.com/en/docs/330/124114#baassandboxusersummaryitem) |Refer to the sample response. |User quota and usage list. |

### BaasSandboxUserSummaryItem

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|CreateTime |String |2026\-07\-01T08:00:00Z |User creation time (UTC). Format: `yyyy-MM-ddTHH:mm:ssZ`. System account might be empty. |
|CustomQuota |Object of [BaasSandboxQuota](https://docs.byteplus.com/en/docs/330/124114#baassandboxquota) |Refer to the Sample response. |Customize quota. Returned only when QuotaCustomized equals `true`. |
|Email |String |alice@example.com |User email, may be empty. |
|QuotaCustomized |Boolean |true |Whether to set a customized quota. Values:<br><br><br>* `true`: Yes.<br><br>* `false`: No. Indicates restoring to follow the global default value. |
|ReadOnly |Boolean |false |Indicates whether it is a read\-only system account. |
|Usage |Object of [BaasSandboxUsage](https://docs.byteplus.com/en/docs/330/124114#baassandboxusage) |Refer to the sample response. |User creation usage statistics. |
|UserId |String |7b973f0e\-\*\*\*\* |User ID. |
|UserName |String |Alice |User name. The System account shows uniformly as `System Admin`. |

### BaasSandboxQuota

|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|DailySandboxLimit |Long |100 |Default daily create quota, `-1` indicates no limit, `0` means creation is prohibited, positive integers represent the daily limit. |

### BaasSandboxUsage

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|TodayCreatedSandboxes |Long | <br><br>3 | <br><br>Number of sandboxes created on the same day in UTC+8. |
|TotalCreatedSandboxes |Long | <br><br>36 | <br><br>Historical total of created Sandbox computes. |

## Sample

Sample request

```JSON
POST /?Action=DescribeBaasSandboxUserSummaries&Version=2025-10-01
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
        "RequestId": "202610261234292B249EA29B2345EFF44C-194611",
        "Action": "DescribeBaasSandboxUserSummaries",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "Total": 1,
        "UserSummaryItems": [
            {
                "CreateTime": "",
                "CustomQuota": {
                    "DailySandboxLimit": -1
                },
                "Email": "",
                "QuotaCustomized": true,
                "ReadOnly": true,
                "Usage": {
                    "TodayCreatedSandboxes": 6,
                    "TotalCreatedSandboxes": 6
                },
                "UserId": "service_role:system",
                "UserName": "System Admin"
            }
        ]
    }
}
```

## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
