---
title: "GetRestoreWindow"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/GetRestoreWindow"
---

Call the GetRestoreWindow API to query the recoverable time period of a branch.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

This API can only be used to operate a workspace using the PostgreSQL engine or Supabase engine.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |noble\-heath\-3a48\*\*\*\* |ID of the workspace. |
|BranchId |String |Yes |br\-merry\-scup\-42d3\*\*\*\* |Branch ID. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|BranchCreateTime |String |2025\-10\-08T06:54:51.000Z |Creation time of the branch (UTC time). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|BranchId |String |br\-merry\-scup\-42d3\*\*\*\* |Branch ID. |
|EndTime |String |2025\-10\-09T09:21:28.013Z |End time of the recoverable time period (UTC time). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|StartTime |String |2025\-10\-08T06:54:51.000Z |Start time of the recoverable time period (UTC time). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|WindowSizeSeconds |Long |172800 |Duration of the recoverable time period, in seconds. |
|WorkspaceId |String |noble\-heath\-3a48\*\*\*\* |ID of the workspace. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=GetRestoreWindow&Version=2025-10-01 HTTP/1.1
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
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
        "RequestId": "202510091721270A6C1C4DA9ACFE36A0A3-1abad3",
        "Action": "GetRestoreWindow",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "BranchCreateTime": "2025-10-08T06:54:51.000Z",
        "BranchId": "br-merry-scup-42d3****",
        "EndTime": "2025-10-09T09:21:28.013Z",
        "WorkspaceId": "noble-heath-3a48****",
        "StartTime": "2025-10-08T06:54:51.000Z",
        "WindowSizeSeconds": 172800
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
