---
title: "DescribeBaasAIUserSummaries"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/DescribeBaasAIUserSummaries"
---

Call DescribeBaasAIUserSummaries to query the model usage summary of AI models access functionality.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

This API can only be used to operate the workspace using the Supabase engine.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeBaasAIUserSummaries&serviceCode=aidap&version=2025-10-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |vivid\-onion\-1122\*\*\*\* |ID of the workspace. |
|BranchId |String |Yes |br\-dandy\-cusk\-d7b1\*\*\*\* |Branch ID. |
|Offset |Integer |No |2 |Starting point for paginated query, an integer greater than or equal to 0, default value is 0. |
|Limit |Integer |No |5 |Pagination query count can be an integer greater than or equal to 1, with a default value of 10. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Total |Integer |4 |Total number of users matching the query criteria. |
|UserSummaryItems |Array of [BaasAIUserSummaryItem](https://docs.byteplus.com/en/docs/330/114167#baasaiusersummaryitem) |Refer to the sample response. |A list summarizing model usage for multiple users. |


<span id="baasaiusersummaryitem"></span>
### BaasAIUserSummaryItem


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|CreateTime |String |2026\-05\-20T06:48:15Z |User creation time (UTC). Format: `yyyy-MM-ddTHH:mm:ssZ`. Corresponds to `auth.users.create_at`. |
|CustomQuota |Object of [BaasAIModelQuota](https://docs.byteplus.com/en/docs/330/114167#baasaimodelquota) |Refer to the sample response. |User\-customized limit. |
|Email |String |test1@test.com |User email, corresponding to `auth.users.email`. |
|LastSignInTime |String |2026\-07\-20T18:48:15Z |User last sign\-in time, user creation time (UTC). Format: `yyyy-MM-ddTHH:mm:ssZ`. Corresponds to `auth.users.last_sign_in_at`. |
|Phone |String |12345678910 |User phone, corresponding to `auth.users.phone`.<br><br> |
|QuotaCustomized |Boolean |true |whether the limit is customized Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|Usage |Object of [BaasAIModelUsage](https://docs.byteplus.com/en/docs/330/114167#baasaimodelusage) |Refer to the sample response. |User's model usage statistics. |
|UserId |String |e0021ade\-c4f4\-43a8\-9678\-dc99a6b5\*\*\*\* |User ID, corresponding to `auth.users.id`. |
|UserName |String |TestUser |User name, which may be an email or phone number.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default">Returns empty if not set.</div><br> |


<span id="baasaimodelquota"></span>
### BaasAIModelQuota


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|DailyImageLimit |Long |300 |Daily image generation quota.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default"><code>-1</code> indicates unlimited.</div><br> |
|DailyTokenLimit |Long |10000 |Daily token quota.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default"><code>-1</code> indicates unlimited.</div><br> |


<span id="baasaimodelusage"></span>
### BaasAIModelUsage


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|TotalImages |Long |1000 |Total number of generated images. |
|TotalTokens |Long |12341245245 |Cumulative token usage. |
|LastDailyImages |Long | |Image usage in the most recent day |
|LastDailyTokens |Long |4338 |Token usage for the last day. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=DescribeBaasAIUserSummaries&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "vivid-onion-1122****",
    "BranchId": "br-dandy-cusk-d7b1****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20260707142930C97D74BE690D08749574-e73fe6",
        "Action": "DescribeBaasAIUserSummaries",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "Total": 2,
        "UserSummaryItems": [
            {
                "CreateTime": "",
                "CustomQuota": {
                    "DailyTokenLimit": -1
                },
                "Email": "",
                "Phone": "",
                "QuotaCustomized": true,
                "Usage": {
                    "LastDailyTokens": 0,
                    "TotalTokens": 0
                },
                "UserId": "service_role:system",
                "UserName": "系统管理员"
            },
            {
                "CreateTime": "2026-05-20T06:48:15Z",
                "Email": "test1@test.com",
                "Phone": "",
                "QuotaCustomized": false,
                "Usage": {
                    "LastDailyTokens": 0,
                    "TotalTokens": 0
                },
                "UserId": "61559718-fce5-4fdb-bf2e-26e33f06****",
                "UserName": ""
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
