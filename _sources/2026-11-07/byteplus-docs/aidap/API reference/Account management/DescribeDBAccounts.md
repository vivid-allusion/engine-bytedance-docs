---
title: "DescribeDBAccounts"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/DescribeDBAccounts"
---

Call the DescribeDBAccounts API to query the branch's database account list.

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
|Limit |Integer |No |5 |Pagination query count can be an integer greater than or equal to 1, with a default value of 10. |
|Offset |Integer |No |1 |Starting point for paginated query, an integer greater than or equal to 0, default value is 0. |
|Search |String |No |test |Search keywords. Supports fuzzy search by account name. |
|SortOrder |String |No |Asc |Sorting method.<br><br><br>* `Asc`: sort by update time in ascending order.<br><br>* `Desc`: sort by update time in descending order. Default value. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Accounts |Array of [Account](https://docs.byteplus.com/en/docs/330/84433#account) |Refer to the sample response. |Account list matching the query criteria. |
|Total |Integer |3 |Total number of results matching the query criteria. |


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
POST /?Action=DescribeDBAccounts&Version=2025-10-01 HTTP/1.1
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "noble-heath-3a48****",
    "BranchId": "br-merry-scup-42d3****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeDBAccounts",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "Accounts": [
            {
                "AccountDesc": "This is a description of an account.",
                "AccountName": "test-user",
                "BranchId": "br-merry-scup-42d3****",
                "CreateTime": "2025-10-09T18:32:12Z",
                "UpdateTime": "2025-10-09T18:32:12Z",
                "WorkspaceId": "noble-heath-3a48a1c7"
            }
        ],
        "Total": 1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
