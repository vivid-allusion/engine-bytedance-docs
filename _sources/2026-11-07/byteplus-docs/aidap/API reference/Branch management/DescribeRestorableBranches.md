---
title: "DescribeRestorableBranches"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/DescribeRestorableBranches"
---

Call the DescribeRestorableBranches API to query the workspace's restorable branches at a specific time.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeRestorableBranches&serviceCode=aidap&version=2025-10-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |ideal\-fir\-9fc8\*\*\*\* |ID of the workspace. |
|Time |String |Yes |2026\-02\-26T10:35:12Z |Target time point (UTC time). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|Offset |Integer |No |1 |The starting page for paginated queries, the default value is `0`. |
|Limit |Integer |No |10 |Page size for paginated query, default value is `10`. |
|Search |String |No |br\-bloom\-duck\-61c7\*\*\*\* |Search by branch ID or branch name prefix. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Branches |Array of [Branch](https://docs.byteplus.com/en/docs/330/106714#branch) |Refer to the sample response. |Branch list under the specified query conditions. |
|RestoreWindow |Array of [RestoreWindow](https://docs.byteplus.com/en/docs/330/106714#restorewindow) |Refer to the sample response. |Available window time list. |
|Total |Integer |2 |Total number of branches that meet the query criteria. |
|WorkspaceName |String |TestWorkspace |Name of the workspace. |


<span id="branch"></span>
### Branch


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Archived |Boolean |false |Whether the branch is archived. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|BranchId |String |br\-bloom\-duck\-61c7\*\*\*\* |Branch ID. |
|BranchName |String |childbranch |Name of the branch. |
|BranchStatus |String |Ready |Branch status. Values:<br><br><br>* `Unknown`: the branch state is unknown.<br><br>* `Init`: the branch is initializing.<br><br>* `Activating`: the branch is activating.<br><br>* `Ready`: the branch is ready.<br><br>* `Archived`: the branch is archived.<br><br>* `Deleted`: the branch is deleted.<br><br>* `Resetting`: the branch is resetting.<br><br>* `Deleting`: the branch is being deleted.<br><br>* `Stopping`: Stopping.<br><br>* `Stopped`: Stopped.<br><br>* `Suspending`: Suspending.<br><br>* `Suspended`: Suspended.<br><br>* `Replacing`: Replacing compute resources.<br><br>* `Restarting`: Restarting.<br><br>* `Updating`: Updating. |
|BranchUsage |Object of [BranchUsage](https://docs.byteplus.com/en/docs/330/106714#branchusage) |Refer to the sample response. |Resource usage information of the branch.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This interface does not return resource usage information of the branch, only returns<code>null</code>。</div><br> |
|CreateTime |String |2025\-10\-08T10:51:06.000Z |Creation time of the branch (UTC time). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|CreationSource |String |Console |The branch's creation source. Value is `Console`. |
|Default |Boolean |false |The branch is default branch or not. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|InitSource |String |ParentData |Source of branch initialization.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default">This interface does not return the initialization source of the branch, only returning <code>None</code>.</div><br> |
|LastResetTime |String |2025\-10\-07T08:57:21.000Z |Last reset time of the branch (UTC time). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If the branch has not been reset, returns empty.</div><br> |
|Protected |Boolean |true |Whether branch protection is set on the branch. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|StatusChangedTime |String |2025\-10\-08T10:16:45.000Z |Branch status change time (UTC time). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|SupportAnalytic |Boolean |true |Whether the compute under the branch supports AP acceleration. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|UpdateTime |String |2025\-10\-09T08:46:27.000Z |The branch's last updated time (UTC time). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|WorkspaceId |String |ideal\-fir\-9fc8\*\*\*\* |ID of the workspace. |


<span id="restorewindow"></span>
### RestoreWindow


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|BranchCreateTime |String |2025\-10\-08T06:54:51.000Z |Creation time of the branch (UTC time). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|BranchId |String |br\-bloom\-duck\-61c7\*\*\*\* |Branch ID. |
|EndTime |String |2025\-10\-09T09:21:28.013Z |End time of the recoverable time period (UTC time). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|StartTime |String |2025\-10\-08T06:54:51.000Z |Start time of the recoverable time period (UTC time). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|WindowSizeSeconds |Long |86400 |Duration of the recoverable time period, in seconds. |


<span id="branchusage"></span>
### BranchUsage


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|BranchId |String |br\-bloom\-duck\-61c7\*\*\*\* |Branch ID. |
|ComputeTimeSeconds |Long |0 |Compute usage of all compute in the branch, unit is second. |
|DataSizeTotalBytes |Long |\-1 |Storage space occupied by branch data. Unit is byte.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Return value <code>-1</code> indicates unlimited.</div><br> |
|DataSizeUsedBytes |Long |24576 |Data size used by the branch, unit is byte. |
|FunctionCallNum |Long |3562 |Number of function calls of the branch.<br><br><div data-tips="true" data-tips-type="default">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This field is returned only for workspaces using the Supabase engine.</div><br> |
|LastRunningTime |String |2025\-10\-21 06:46:33 +0000 UTC |Last running time of the branch (UTC). Format: `yyyy-MM-dd HH:mm:ss +0000 UTC`. |
|ServiceTimeSeconds |Long |365 |The branch has used service duration.<br><br> |
|StatTime |String |2025\-10\-21 06:46:33 +0000 UTC |Statistics time of branch resource usage information (UTC). Format: `yyyy-MM-dd HH:mm:ss +0000 UTC`. |
|StorageSizeUsedBytes |Long |24576 |The storage service data size used by the branch, in bytes.<br><br> |
|WorkspaceId |String |ideal\-fir\-9fc8\*\*\*\* |ID of the workspace. |
|VectorReadVCU |Double |19.22 |Resources consumed when performing retrieval, query, and other read operations on vector data in the vector bucket. Unit is vCU.<br><br><div data-tips="true" data-tips-type="default">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This field is returned only for workspaces using the Supabase engine.</div><br> |
|VectorWriteVCU |Double |7.3 |Resources consumed for writing, updating, or deleting vector data in the vector bucket. Unit is vCU.<br><br><div data-tips="true" data-tips-type="default">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This field is returned only for workspaces using the Supabase engine.</div><br> |
|VectorStorageSizeUsedBytes |Long |909805 |Storage space occupied by vector data stored in vector bucket. Unit is byte.<br><br><div data-tips="true" data-tips-type="default">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This field is returned only for workspaces using the Supabase engine.</div><br> |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=DescribeRestorableBranches&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "ideal-fir-9fc8****",
    "Time": "2026-02-26T10:35:12Z",
    "Search": "br-bloom-duck-61c7****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeRestorableBranches",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "Branches": [
            {
                "Archived": false,
                "BranchId": "br-stoic-ibex-e642****",
                "BranchName": "main",
                "BranchStatus": "Stopped",
                "BranchUsage": null,
                "CreateTime": "2026-02-13T03:50:22Z",
                "CreationSource": "Console",
                "Default": true,
                "InitSource": "None",
                "LastResetTime": "",
                "Protected": false,
                "StatusChangedTime": "2026-02-26T10:27:15Z",
                "SupportAnalytic": false,
                "UpdateTime": "2026-02-26T10:27:15Z",
                "WorkspaceId": "ideal-fir-9fc8****"
            }
        ],
        "RestoreWindow": [
            {
                "BranchCreateTime": "2026-02-13T03:50:22Z",
                "BranchId": "br-stoic-ibex-e642****",
                "EndTime": "2026-02-26T12:07:35Z",
                "StartTime": "2026-02-25T12:07:35Z",
                "WindowSizeSeconds": 86400
            }
        ],
        "Total": 1,
        "WorkspaceName": "TestWorkspace"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
