---
title: "ResetWorkspaceAccountPassword"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/ResetWorkspaceAccountPassword"
---

Use the ResetWorkspaceAccountPassword API to reset the account and password for logging in to the Supabase console.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

This API can only be used to operate the workspace using the Supabase engine.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |noble\-heath\-3a48\*\*\* |ID of the workspace. |
|BranchId |String |Yes |br\-merry\-scup\-42d3\*\*\*\* |Branch ID. |
|AccountName |String |Yes |testuser |Account name to be reset. The name must meet the following rules:<br><br><br>* Can only contain Chinese characters, letters (a~z and A~Z), digits (0~9), hyphens (\-), and underscores (_).<br><br>* Must be 2 to 63 characters in length.<br><br>* Must start with a letter (a\-z and A\-Z).<br><br>* Must end with a letter (a\-z and A\-Z) or digit (0\-9).<br><br>* Cannot use certain reservation words. For details about reserved words, refer to [List of reserved keywords](https://docs.byteplus.com/en/docs/aidap/Reservation_word_list). |
|AccountPassword |String |Yes |Test@user |Account password to be reset. Account password must meet the following rules:<br><br><br>* Can only contain letters (a~z and A~Z), numbers (0~9), and the following special characters ` !#$%&()*+,-.=?@^_\|/`.<br><br>* The length must be between 8 and 32 characters.<br><br>* Must contain at least three of the following character types: uppercase letters (A~Z), lowercase letters (a~z), digits (0~9), and special characters.<br><br>* Using easily cracked weak passwords (such as Admin@123) is not allowed. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

None.

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=ResetWorkspaceAccountPassword&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "noble-heath-3a48***",
    "BranchId": "br-merry-scup-42d3****",
    "AccountName": "testuser",
    "AccountPassword": "Test@user"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ResetWorkspaceAccountPassword",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
