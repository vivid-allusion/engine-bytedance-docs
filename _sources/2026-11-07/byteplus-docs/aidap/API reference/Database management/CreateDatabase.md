---
title: "CreateDatabase"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/CreateDatabase"
---

Call the CreateDatabase API to create a database for a branch.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

This API can only operate workspaces using the PostgreSQL engine.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |noble\-heath\-3a48\*\*\*\* |ID of the workspace. |
|BranchId |String |Yes |br\-merry\-scup\-42d3\*\*\*\* |Branch ID. |
|DatabaseName |String |Yes |test\-db |Name of the database. The database name must follow these rules:<br><br><br>* Unique within the branch.<br><br>* Must start with a letter and end with a letter or number.<br><br>* Can only contain letters, numbers, underscores (_), and hyphens (\-).<br><br>* Must be 2 to 63 characters in length.<br><br>* Cannot use certain reservation words. For details about reserved words, refer to [List of reserved keywords](https://docs.byteplus.com/en/docs/aidap/Reservation_word_list). |
|DatabaseOwner |String |No |test\-user |The account to which the database belongs<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default">The optionality of the DatabaseOwner parameter differs depending on the engine used by the workspace specified by the WorkspaceId parameter:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">when the workspace uses the <code>PostgreSQL</code> engine, DatabaseOwner is required.</div><br> |
|DatabaseDesc |String |No |This is a description of a database. |The database description cannot exceed 256 characters. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Database |Object of [Database](https://docs.byteplus.com/en/docs/330/84437#database) |Refer to the sample response. |Details of the database. |


<span id="database"></span>
### Database


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|BranchId |String |br\-merry\-scup\-42d3\*\*\*\* |Branch ID. |
|CreateTime |String |2025\-10\-21T08:06:52Z |Database creation time (UTC). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|DatabaseDesc |String |This is a description of a database. |The description of the database. |
|DatabaseName |String |test\-db |Name of the database. |
|DatabaseOwner |String |test\-user |The account to which the database belongs. |
|UpdateTime |String |2025\-10\-21T08:06:52Z |Update time of the database (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|WorkspaceId |String |noble\-heath\-3a48\*\*\*\* |ID of the workspace. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=CreateDatabase&Version=2025-10-01 HTTP/1.1
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "frank-melon-9dd3****",
    "BranchId": "br-bloom-ibex-56e0****",
    "DatabaseName": "test-db",
    "DatabaseOwner": "test-user",
    "DatabaseDesc": "This is a description of a database."
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateDatabase",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "Database": {
            "BranchId": "br-bloom-ibex-56e0****",
            "CreateTime": "2025-10-21T08:06:52Z",
            "DatabaseDesc": "This is a description of a database.",
            "DatabaseName": "test-db",
            "DatabaseOwner": "test-user",
            "UpdateTime": "2025-10-21T08:06:52Z",
            "WorkspaceId": "frank-melon-9dd3****"
        }
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
