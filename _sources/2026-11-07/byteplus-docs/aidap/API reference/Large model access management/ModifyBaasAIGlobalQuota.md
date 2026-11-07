---
title: "ModifyBaasAIGlobalQuota"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/ModifyBaasAIGlobalQuota"
---

Use the ModifyBaasAIGlobalQuota API to change the global model quota for users with AI models access functionality.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

This API can only be used to operate the workspace using the Supabase engine.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyBaasAIGlobalQuota&serviceCode=aidap&version=2025-10-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |vivid\-onion\-1122\*\*\*\* |ID of the workspace. |
|BranchId |String |Yes |br\-dandy\-cusk\-d7b1\*\*\*\* |Branch ID. |
|UserDefaultQuota |Object of [BaasAIModelQuota](https://docs.byteplus.com/en/docs/330/114171#baasaimodelquota) |Yes |Refer to the sample request. |Default quota for every user. |


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
POST /?Action=ModifyBaasAIGlobalQuota&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "vivid-onion-1122****",
    "BranchId": "br-dandy-cusk-d7b1****",
    "UserDefaultQuota": {
        "DailyTokenLimit": 10000
    }
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyBaasAIGlobalQuota",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
