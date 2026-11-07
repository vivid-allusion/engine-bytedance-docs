---
title: "DescribeWorkspaceOverview"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/DescribeWorkspaceOverview"
---

Call the DescribeWorkspaceOverview API to query workspace overview information.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|ProjectName |String |No |default |Affiliate project name. |
|EngineType |String |No |PostgreSQL |Engine type. Values:<br><br><br>* `PostgreSQL`: PostgreSQL engine.<br><br>* `Supabase`: Supabase engine. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|WorkspaceOverviews |Array of [WorkspaceOverview](https://docs.byteplus.com/en/docs/330/84449#workspaceoverview) |Refer to the sample response. |Overview information about the workspace. |


<span id="workspaceoverview"></span>
### WorkspaceOverview


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|ClosedTotal |Integer |0 |Total number of workspaces in the "Closed" status under the specified database engine type. |
|CreatingTotal |Integer |2 |Total number of workspaces in "Creating" status under the specified database engine type. |
|EngineType |String |PostgreSQL |Engine type. Values:<br><br><br>* `PostgreSQL`: PostgreSQL engine.<br><br>* `Supabase`: Supabase engine. |
|ErrorTotal |Integer |0 |total number of workspaces in the "Creation failed" and "Abnormal" status under the specified database engine type. |
|RunningTotal |Integer |11 |total number of workspaces in the "Running" status under the specified database engine type. |
|StoppedTotal |Integer |1 |Total number of workspaces in the "Stopped" status under the specified database engine type. |
|SuspendedTotal |Integer |1 |Total number of workspaces in the "Suspended" status under the specified database engine type. |
|UpdatingTotal |Integer |0 |Total workspace count with database engine type in "Changing" and "Network changing" status. |
|WorkspaceTotal |Integer |13 |Total number of workspaces under the specified database engine type. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=DescribeWorkspaceOverview&Version=2025-10-01 HTTP/1.1
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "EngineType": "PostgreSQL",
    "ProjectName": "default"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeWorkspaceOverview",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "WorkspaceOverviews": [
            {
                "ClosedTotal": 0,
                "CreatingTotal": 0,
                "EngineType": "PostgreSQL",
                "ErrorTotal": 0,
                "RunningTotal": 37,
                "StoppedTotal": 4,
                "SuspendedTotal": 1,
                "UpdatingTotal": 0,
                "WorkspaceTotal": 42
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
