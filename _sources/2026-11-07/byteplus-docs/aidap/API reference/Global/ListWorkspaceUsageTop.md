---
title: "ListWorkspaceUsageTop"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/ListWorkspaceUsageTop"
---

Call the ListWorkspaceUsageTop API to query resource usage of all Workspaces under the tenant account in descending order.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListWorkspaceUsageTop&serviceCode=aidap&version=2025-10-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|ProjectName |String |No |default |Specify the items to query. |
|Limit |Integer |No |5 |The number of results returned. Range of values, default is 10. |
|SortBy |String |No | cpu |Sort basis. Values:<br><br><br>* `cpu`: sorted by compute consumption. Default value.<br><br>* `disk`: sorted by storage space consumption. |
|TimePastRange |Integer |No | 30 |The calculation range of resource usage is 30 days, specifying it is not supported yet. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|WorkspaceUsageList |Array of [WorkspaceUsageWithExtra](https://docs.byteplus.com/en/docs/330/84401#workspaceusagewithextra) |Refer to the sample response. |Resource usage information of the workspace under specific query conditions. |


<span id="workspaceusagewithextra"></span>
### WorkspaceUsageWithExtra


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|WorkspaceId |String |noble\-heath\-3a48\*\*\*\* |ID of the workspace. |
|WorkspaceName |String |TestWorkspace |Name of the workspace. |
|WorkspaceUsage |Object of [WorkspaceUsage](https://docs.byteplus.com/en/docs/330/84401#workspaceusage) |Refer to the sample response. |Resource usage information of the workspace. |


<span id="workspaceusage"></span>
### WorkspaceUsage


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|BranchComputeTimeSeconds |Long |4240159 |Compute duration used by the workspace branch. Unit is second. |
|BranchCreatedNum |Long |12 |The number of branches in the workspace.   |
|ComputeTimeSeconds |Long |4560259 |Compute duration used by the workspace. Unit is second. |
|DataSizeTotalBytes |Long |\-1 |Storage size. Unit is byte.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Return value <code>-1</code> indicates unlimited.</div><br> |
|DataSizeUsedBytes |Long |90980352 |Used storage space size of the workspace. Unit is byte. |
|FunctionCallNum |Long |45443 |Number of function calls.<br><br><div data-tips="true" data-tips-type="default">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This field is returned only for workspaces using the Supabase engine.</div><br> |
|ServiceTimeSeconds |Long |12 |Service usage duration.<br><br><div data-tips="true" data-tips-type="default">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This field is returned only for workspaces using the Supabase engine.</div><br> |
|StatTime |String |2025\-10\-20T03:46:01Z |Data statistics time (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|StorageSizeUsedBytes |Long |6944 |Size of data used by the storage service.<br><br><div data-tips="true" data-tips-type="default">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This field is returned only for workspaces using the Supabase engine.</div><br> |
|VectorReadVCU |Double |19.22 |Resources consumed when performing retrieval, query, and other read operations on vector data in the vector bucket. Unit is vCU.<br><br><div data-tips="true" data-tips-type="default">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This field is returned only for workspaces using the Supabase engine.</div><br> |
|VectorStorageSizeUsedBytes |Long |909805 |Storage space occupied by vector data stored in vector bucket. Unit is byte.<br><br><div data-tips="true" data-tips-type="default">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This field is returned only for workspaces using the Supabase engine.</div><br> |
|VectorWriteVCU |Double |7.3 |Resources consumed for writing, updating, or deleting vector data in the vector bucket. Unit is vCU.<br><br><div data-tips="true" data-tips-type="default">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This field is returned only for workspaces using the Supabase engine.</div><br> |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=ListWorkspaceUsageTop&Version=2025-10-01 HTTP/1.1
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "Limit": 5,
    "TimePastRange": 30,
    "SortBy": "cpu",
    "ProjectName": "default"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202512021223454E962EEB36ADD96E7021-8ae320",
        "Action": "ListWorkspaceUsageTop",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "WorkspaceUsageList": [
            {
                "WorkspaceId": "right-mint-f0e5b3ed",
                "WorkspaceName": "测试1",
                "WorkspaceUsage": {
                    "BranchComputeTimeSeconds": 749325,
                    "BranchCreatedNum": 5,
                    "ComputeTimeSeconds": 951600,
                    "DataSizeTotalBytes": -1,
                    "DataSizeUsedBytes": 54296576,
                    "StatTime": "2025-12-02T04:14:06Z"
                }
            },
            {
                "WorkspaceId": "peppy-moss-77fb77d1",
                "WorkspaceName": "测试2",
                "WorkspaceUsage": {
                    "BranchComputeTimeSeconds": 620400,
                    "BranchCreatedNum": 2,
                    "ComputeTimeSeconds": 778650,
                    "DataSizeTotalBytes": -1,
                    "DataSizeUsedBytes": 54149120,
                    "StatTime": "2025-12-02T04:15:20Z"
                }
            },
            {
                "WorkspaceId": "glad-aster-35fc5c7d",
                "WorkspaceName": "测试3",
                "WorkspaceUsage": {
                    "BranchComputeTimeSeconds": 309000,
                    "BranchCreatedNum": 2,
                    "ComputeTimeSeconds": 618600,
                    "DataSizeTotalBytes": -1,
                    "DataSizeUsedBytes": 2215917388,
                    "StatTime": "2025-12-02T04:20:14Z"
                }
            },
            {
                "WorkspaceId": "vocal-gourd-e4fd1611",
                "WorkspaceName": "测试4",
                "WorkspaceUsage": {
                    "BranchComputeTimeSeconds": 77850,
                    "BranchCreatedNum": 2,
                    "ComputeTimeSeconds": 471000,
                    "DataSizeTotalBytes": -1,
                    "DataSizeUsedBytes": 54140928,
                    "StatTime": "2025-12-02T04:18:01Z"
                }
            },
            {
                "WorkspaceId": "hip-thyme-30157643",
                "WorkspaceName": "测试5",
                "WorkspaceUsage": {
                    "BranchComputeTimeSeconds": 0,
                    "BranchCreatedNum": 1,
                    "ComputeTimeSeconds": 387540,
                    "DataSizeTotalBytes": -1,
                    "DataSizeUsedBytes": 39149568,
                    "StatTime": "2025-12-02T04:22:08Z"
                }
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
