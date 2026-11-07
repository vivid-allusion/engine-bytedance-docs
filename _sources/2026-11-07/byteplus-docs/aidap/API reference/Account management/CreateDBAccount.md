---
title: "CreateDBAccount"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/CreateDBAccount"
---

Call the CreateDBAccount API to create a database account for the branch.

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
|AccountName |String |Yes |test\-user |Account name. The name must meet the following rules:<br><br><br>* Unique within the branch.<br><br>* Must start with a letter and end with a letter or number.<br><br>* Can only contain letters, numbers, underscores (_), and hyphens (\-).<br><br>* Must be 2 to 63 characters in length.<br><br>* Cannot use certain reservation words. For details about reserved words, refer to [List of reserved keywords](https://docs.byteplus.com/en/docs/aidap/Reservation_word_list). |
|AccountPassword |String |Yes |password4test\-user |Password of the account. Account password must meet the following rules:<br><br><br>* Can only contain letters (a~z and A~Z), numbers (0~9), and the following special characters  `!#$%&()*+,-.=?@^_\|/`.<br><br>* The length must be between 8 and 32 characters.<br><br>* Must contain at least three of the following character types: uppercase letters (A~Z), lowercase letters (a~z), digits (0~9), and special characters.<br><br>* Using easily cracked weak passwords (such as Admin@123) is not allowed. |
|AccountDesc |String |No |This is a description of an account. |The description of the account, with a maximum length of 256 characters. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Account |Object of [Account](https://docs.byteplus.com/en/docs/330/84435#account) |Refer to the sample response. |Account details. |


<span id="account"></span>
### Account


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|AccountDesc |String |This is a description of an account. |Account description. |
|AccountName |String |test\-user |Account name. |
|BranchId |String |br\-merry\-scup\-42d3\*\*\*\* |Branch ID. |
|CreateTime |String |2025\-10\-21T08:00:58Z |Account creation time (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|UpdateTime |String |2025\-10\-21T08:00:58Z |Account update time (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|WorkspaceId |String |noble\-heath\-3a48\*\*\*\* |ID of the workspace. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=CreateDBAccount&Version=2025-10-01 HTTP/1.1
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "noble-heath-3a48****",
    "BranchId": "br-merry-scup-42d3****",
    "AccountName": "test-user",
    "AccountPassword": "password4test-user",
    "AccountDesc": "This is a description of an account."
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateDBAccount",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "Account": {
            "AccountDesc": "This is a description of an account.",
            "AccountName": "test-user",
            "BranchId": "br-bloom-ibex-56e0****",
            "CreateTime": "2025-10-21T08:00:58Z",
            "UpdateTime": "2025-10-21T08:00:58Z",
            "WorkspaceId": "frank-melon-9dd3c940"
        }
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
