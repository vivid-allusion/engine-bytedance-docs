---
title: "DescribeDatabases"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/DescribeDatabases"
---

Call the DescribeDatabases API to query branch databases.

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
|Offset |Integer |No |1 |Starting point for paginated query, an integer greater than or equal to 0, default value is 0. |
|Limit |Integer |No |5 |Pagination query count can be an integer greater than or equal to 1, with a default value of 10. |
|Search |String |No |Test |Search keywords. Supports fuzzy search by account name. |
|SortOrder |String |No |Asc |Sorting method.<br><br><br>* `Asc`: sort by update time in ascending order.<br><br>* `Desc`: sort by update time in descending order. Default value. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Databases |Array of [Database](https://docs.byteplus.com/en/docs/330/84439#database) |Refer to the sample response. |List of database matching query criteria. |
|Total |Integer |3 |Total number of databases matching the query criteria. |


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
POST /?Action=DescribeDatabases&Version=2025-10-01 HTTP/1.1
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "frank-melon-9dd3****",
    "BranchId": "br-bloom-ibex-56e0****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeDatabases",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "Databases": [
            {
                "BranchId": "br-bloom-ibex-56e0****",
                "CreateTime": "2025-10-21T08:06:52Z",
                "DatabaseDesc": "This is a description of a database."
                "DatabaseName": "test-db",
                "DatabaseOwner": "test-user",
                "UpdateTime": "2025-10-21T08:06:52Z",
                "WorkspaceId": "frank-melon-9dd3****"
            }
        ],
        "Total": 1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
