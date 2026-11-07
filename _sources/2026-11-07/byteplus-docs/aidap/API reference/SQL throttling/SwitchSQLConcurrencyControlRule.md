---
title: "SwitchSQLConcurrencyControlRule"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/SwitchSQLConcurrencyControlRule"
---

Call the SwitchSQLConcurrencyControlRule API to enable or disable the SQL concurrency control rule.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

This API only supports operations on workspaces using the PostgreSQL engine.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=SwitchSQLConcurrencyControlRule&serviceCode=aidap&version=2025-10-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |noble\-heath\-3a48\*\*\*\* |Workspace ID。 |
|BranchId |String |Yes |br\-merry\-scup\-42d3\*\*\*\* |Branch ID. |
|DatabaseName |String |Yes |test\-db |Name of the database. |
|RuleId |Long |Yes |136734987028564\*\*\*\* |ID of the rate limiting rule. |
|Enabled |Boolean |Yes |false |Whether to enable the rule. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|EffectType |String |No |NextWakeUp |Effective method. Values:<br><br><br>* `Immediate`: takes effect immediately if the Workspace is Running; if the Workspace is Suspending, it takes effect upon waking up. Default value.<br><br>* `NextWakeUp`: takes effect at the next wake\-up. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Code |Integer |0 |Return status code. 0 indicates succeeded. |
|Message |String |success |return message. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=SwitchSQLConcurrencyControlRule&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "noble-heath-3a48****",
    "BranchId": "br-merry-scup-42d3****",
    "DatabaseName": "test-db",
    "RuleId": 136734987028564,
    "Enabled": false,
    "EffectType": "NextWakeUp"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "SwitchSQLConcurrencyControlRule",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "Code": 0,
        "Message": "success"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
