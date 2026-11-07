---
title: "DescribeOperations"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/DescribeOperations"
---

Call the DescribeOperations API to query operation records.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

&nbsp;


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Offset |Integer |No |1 |Starting point for paginated query, an integer greater than or equal to 0, default value is 0. |
|Limit |Integer |No |5 |Pagination query count can be an integer greater than or equal to 1, with a default value of 10. |
|Filters |Array of [QueryFilter](https://docs.byteplus.com/en/docs/330/106709#queryfilter) |No |Refer to the sample request. |Filter conditions for the query. |
|CreateTimeStart |String |No |2026\-03\-12T12:06:25Z |When querying by the operation start time, the starting point of the time period (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default">The maximum query period is 7 days.</div><br> |
|CreateTimeEnd |String |No |2026\-03\-11T16:00:00Z |When querying by operations start time, the end of the time range (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The maximum query period is 7 days.</div><br> |


<span id="queryfilter"></span>
### QueryFilter


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Name |String |Yes |WorkspaceId |Filter options for querying. Values:<br><br><br>* `WorkspaceId`: Query by workspace ID.<br><br>* `BranchId`: Query by branch ID.<br><br>* `ComputeId`: Query by compute ID.<br><br>* `ActionName`: Query by operation name. |
|Value |String |Yes |"frank\-reed\-56a1\*\*\*\*,regal\-lemon\-9ee5\*\*\*\*" |Specify the filter value for the filter option.<br><br><br>* When the parameter Name takes the value `WorkspaceId`, `BranchId`, or `ComputeId`, the parameter Value takes the ID of the resource specified by the parameter Name.<br><br>* When the parameter Name takes the value `ActionName`, the parameter Value takes the operation of create, delete, or update operations listed in the [API list](https://docs.byteplus.com/en/docs/aidap/API_overview). |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

&nbsp;


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Operations |Array of [OperationSummary](https://docs.byteplus.com/en/docs/330/106709#operationsummary) |Refer to the sample response. |Operation list under specified query conditions. |
|Total |Integer |10 |Total number of operations matching the specified query conditions. |


<span id="operationsummary"></span>
### OperationSummary


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|ActionName |String |CreateWorkspace |Name of the operations. Refer to the [API list](https://docs.byteplus.com/en/docs/aidap/API_overview) document for more details on operations. |
|ActionStatus |String |Success |Status of the operation. Values:<br><br><br>* `Running`: Running.<br><br>* `Succeeded`: succeeded.<br><br>* `Failed`: failed. |
|BranchId |String |br\-smart\-tody\-d5a1\*\*\*\* |ID of the branch associated with the operations.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default">If the operations are unrelated to the branch, return empty.</div><br> |
|ComputeId |String |cp\-deft\-whirl\-c769\*\*\*\* |ID of the Compute associated with the operation.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default">If the operation is unrelated to Compute, returns empty.</div><br> |
|CreateTime |String |2026\-03\-12T12:20:03Z |operation start time. |
|DurationTime |String |17s |Duration of the operation. |
|FinishTime |String |2026\-03\-12T08:30:17Z |Operation end time. |
|OperationId |String |2026031216295953DDC35B8C8410AC\*\*\*\*\-5c48ca |ID of the operations. |
|WorkspaceId |String |quiet\-dill\-9136\*\*\*\* |ID of the Workspace associated with the operations. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=DescribeOperations&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "Filters": [
        {
            "Name":"WorkspaceId",
            "Value":"brisk-birch-32f0****"
        },
        {
            "Name":"BranchId",
            "Value":"br-grand-emu-4d22****"
        }
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeOperations",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "Operations": [
            {
                "ActionName": "CreateBranch",
                "ActionStatus": "Success",
                "BranchId": "br-grand-emu-4d22****",
                "ComputeId": "",
                "CreateTime": "2026-03-12T12:42:19Z",
                "DurationTime": "31s",
                "FinishTime": "2026-03-12T12:42:50Z",
                "OperationId": "20260312204218449C6A572D73781A****-b528a5",
                "WorkspaceId": "brisk-birch-32f0****"
            },
        "Total": 1
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
