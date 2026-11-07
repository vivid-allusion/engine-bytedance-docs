---
title: "ModifyBaasAIUserQuotas"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/ModifyBaasAIUserQuotas"
---

Call the ModifyBaasAIUserQuotas API to modify the model quota for users with AI models access functions.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

This API can only be used to operate the workspace using the Supabase engine.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyBaasAIUserQuotas&serviceCode=aidap&version=2025-10-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |vivid\-onion\-1122\*\*\*\* |ID of the workspace. |
|BranchId |String |Yes |br\-dandy\-cusk\-d7b1\*\*\*\* |Branch ID. |
|UserQuotaItems |Array of [BaasAIUserQuotaItem](https://docs.byteplus.com/en/docs/330/114169#baasaiuserquotaitem) |Yes |Refer to the sample request. |Model quota list for multiple users. |


<span id="baasaiuserquotaitem"></span>
### BaasAIUserQuotaItem


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|UserId |String |Yes |61559718\-fce5\-4fdb\-bf2e\-26e33f06\*\*\*\* |User ID, corresponds to `auth.users.id`. |
|CustomQuota |Object of [BaasAIModelQuota](https://docs.byteplus.com/en/docs/330/114169#baasaimodelquota) |No |Refer to the sample request. |User\-customized limit. |
|QuotaCustomized |Boolean |Yes |true |Whether there is a customize quota. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If the value is <code>false</code>, the CustomQuota parameter is ignored.</div><br> |


<span id="baasaimodelquota"></span>
### BaasAIModelQuota


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|DailyImageLimit |Long |No |300 |Daily image generation quota.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default"><code>-1</code> indicates unlimited.</div><br> |
|DailyTokenLimit |Long |No |10000 |Daily token quota.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default"><code>-1</code> indicates unlimited.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

None.

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=ModifyBaasAIUserQuotas&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "adept-lotus-1dbb****",
    "BranchId": "br-slick-scup-b8c0****",
    "UserQuotaItems": [
        {
            "UserId": "61559718-fce5-4fdb-bf2e-26e33f06****",
            "QuotaCustomized": true,
            "CustomQuota": {
                "DailyTokenLimit": 10000
            }
        }
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyBaasAIUserQuotas",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
