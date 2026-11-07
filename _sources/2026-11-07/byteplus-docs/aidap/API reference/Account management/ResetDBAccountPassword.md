---
title: "ResetDBAccountPassword"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/ResetDBAccountPassword"
---

Call the ResetAccountPassword API to reset the account password.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

This API can only operate workspaces using the PostgreSQL engine.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |noble\-heath\-3a48\*\*\*\* |ID of the workspace. |
|BranchId |String |Yes |br\-merry\-scup\-42d3\*\*\*\* |Branch ID. |
|AccountName |String |Yes |test\-user |Name of the account that requires password reset. |
|AccountPassword |String |Yes |R6RX3PmCs\u0026$Q\*\*\*\* |New account password. Account password must meet the following rules:<br><br><br>* Can only contain letters (a~z and A~Z), numbers (0~9), and the following special characters  `!#$%&()*+,-.=?@^_\|/`.<br><br>* The length must be between 8 and 32 characters.<br><br>* Must contain at least three of the following character types: uppercase letters (A~Z), lowercase letters (a~z), digits (0~9), and special characters.<br><br>* Using easily cracked weak passwords (such as Admin@123) is not allowed. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Success |Boolean |true |Whether resetting the account password succeeded. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=ResetDBAccountPassword&Version=2025-10-01 HTTP/1.1
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "noble-heath-3a48****",
    "BranchId": "br-merry-scup-42d3****",
    "AccountName": "test-user",
    "AccountPassword": "R6RX3PmCs\\u0026$Q****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ResetDBAccountPassword",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "Success": true
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
