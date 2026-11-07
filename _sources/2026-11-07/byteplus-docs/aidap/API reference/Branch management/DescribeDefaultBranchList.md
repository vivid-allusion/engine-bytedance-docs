---
title: "DescribeDefaultBranchList"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/DescribeDefaultBranchList"
---

Call the DescribeDefaultBranchList API to query the default branch of multiple workspaces.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

&nbsp;


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceIds |Array of String |Yes |["noble\-heath\-3a48\*\*\*\*","stoic\-chili\-ab80\*\*\*\*"] |List of workspace IDs. |
|Offset |Integer |No |1 |Pagination query count can be an integer greater than or equal to 1, with a default value of 10. |
|Limit |Integer |No |20 |Pagination query count can be an integer greater than or equal to 1, with a default value of 10. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

&nbsp;


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Total |Integer |20 |The quantity of results that meet the query conditions. |
|BranchList |Array of [WorkspaceDefaultBranch](https://docs.byteplus.com/en/docs/330/106699#workspacedefaultbranch) |Refer to the Sample response. |List of default branches for the specified workspaces. |


<span id="workspacedefaultbranch"></span>
### WorkspaceDefaultBranch


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Branch |Object of [Branch](https://docs.byteplus.com/en/docs/330/106699#branch) |Refer to the sample response. |Details of the workspace's default branch. |
|WorkspaceId |String |"noble\-heath\-3a48\*\*\*\* |ID of the workspace. |


<span id="branch"></span>
### Branch


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Archived |Boolean |false |Whether the branch is archived. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|BranchId |String |br\-bloom\-duck\-61c7\*\*\*\* |Branch ID. |
|BranchName |String |childbranch |Name of the branch. |
|BranchStatus |String |Ready |Branch status. Values:<br><br><br>* `Unknown`: the branch state is unknown.<br><br>* `Init`: the branch is initializing.<br><br>* `Activating`: the branch is activating.<br><br>* `Ready`: the branch is ready.<br><br>* `Archived`: the branch is archived.<br><br>* `Deleted`: the branch is deleted.<br><br>* `Resetting`: the branch is resetting.<br><br>* `Deleting`: the branch is being deleted.<br><br>* `Stopping`: Stopping.<br><br>* `Stopped`: Stopped.<br><br>* `Suspending`: Suspending.<br><br>* `Suspended`: Suspended.<br><br>* `Replacing`: Replacing compute resources.<br><br>* `Restarting`: Restarting.<br><br>* `Updating`: Updating. |
|BranchUsage |Object of [BranchUsage](https://docs.byteplus.com/en/docs/330/106699#branchusage) |Refer to the sample response. |Resource usage information of the branch. |
|CreateTime |String |2025\-10\-08T10:51:06.000Z |Creation time of the branch (UTC time). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|CreationSource |String |Console |The branch's creation source. Value is `Console`. |
|Default |Boolean |false |The branch is default branch or not. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|InitSource |String |ParentData |Branch initialization source, default is `ParentData`.<br><br><br>* `ParentData`: Schema and data.<br><br>* `SchemaOnly`: Schema only. |
|LastResetTime |String |2025\-10\-07T08:57:21.000Z |Last reset time of the branch (UTC time). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If the branch has not been reset, returns empty.</div><br> |
|ParentBranch |Object of [ParentBranch](https://docs.byteplus.com/en/docs/330/106699#parentbranch) |Refer to the Sample response. |Parent branch information of this branch.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If the branch has no parent branch, this field is not returned.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When the <a href="https://docs.byteplus.com/en/docs/330/106699#branch">Branch</a> data structure is used to describe ParentBranch, only the BranchId, BranchName, BranchStatus, and WorkspaceId fields are returned.</div><br> |
|Protected |Boolean |true |Whether branch protection is set on the branch. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|StartParentLSN |String |0/3522648 |The parent branch LSN corresponding to this branch when created. |
|StartParentTime |String |2025\-10\-08T08:57:21.000Z |Data synchronization time point (UTC time) selected when the branch is created from the parent branch. Format: `yyyy-MM-ddTHH:mm:ss.sssZ`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If the branch has no parent branch, it returns <code>1970-01-01T00:00:00.000Z</code>.</div><br> |
|StatusChangedTime |String |2025\-10\-08T10:16:45.000Z |Branch status change time (UTC time). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|SupportAnalytic |Boolean |true |Whether the compute under the branch supports AP acceleration. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|UpdateTime |String |2025\-10\-09T08:46:27.000Z |The branch's last updated time (UTC time). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|WorkspaceId |String |ideal\-fir\-9fc8\*\*\*\* |ID of the workspace. |


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


<span id="parentbranch"></span>
### ParentBranch


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|BranchId |String |br\-bloom\-duck\-61c7\*\*\*\* |Branch ID. |
|BranchName |String |main |Name of the branch. |
|WorkspaceId |String |ideal\-fir\-9fc8\*\*\*\* |ID of the workspace. |
|BranchStatus |String |Ready |Branch status. Values:<br><br><br>* `Unknown`: the branch state is unknown.<br><br>* `Init`: the branch is initializing.<br><br>* `Activating`: the branch is activating.<br><br>* `Ready`: the branch is ready.<br><br>* `Archived`: the branch is archived.<br><br>* `Deleted`: the branch is deleted.<br><br>* `Resetting`: the branch is resetting.<br><br>* `Deleting`: the branch is being deleted.<br><br>* `Stopping`: Stopping.<br><br>* `Stopped`: Stopped.<br><br>* `Suspending`: Suspending.<br><br>* `Suspended`: Suspended.<br><br>* `Replacing`: Replacing compute resources.<br><br>* `Restarting`: Restarting.<br><br>* `Updating`: Updating. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=DescribeDefaultBranchList&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceIds": ["perky-bluet-7508****","zappy-fern-1756****"]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20260507182951C01645DFD0C95FC3253D-ca795a",
        "Action": "DescribeDefaultBranchList",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "BranchList": [
            {
                "Branch": {
                    "Archived": false,
                    "BranchId": "br-happy-pike-80d1****",
                    "BranchName": "main",
                    "BranchStatus": "Ready",
                    "BranchUsage": {
                        "BranchId": "br-happy-pike-80d1****",
                        "ComputeTimeSeconds": 1950,
                        "DataSizeTotalBytes": -1,
                        "DataSizeUsedBytes": 73777152,
                        "LastRunningTime": "2026-05-07T10:24:39Z",
                        "ServiceTimeSeconds": 352,
                        "StatTime": "2026-05-07T10:24:39Z",
                        "StorageSizeUsedBytes": 0,
                        "TotalTokens": 0,
                        "WorkspaceId": ""
                    },
                    "CreateTime": "2026-05-07T08:18:55.000Z",
                    "CreationSource": "SDK",
                    "Default": true,
                    "InitSource": "None",
                    "LastResetTime": "",
                    "Protected": false,
                    "StatusChangedTime": "2026-05-07T08:19:01.000Z",
                    "SupportAnalytic": false,
                    "UpdateTime": "2026-05-07T08:19:01.000Z",
                    "WorkspaceId": "perky-bluet-7508****"
                },
                "WorkspaceId": "perky-bluet-7508****"
            },
            {
                "Branch": {
                    "Archived": false,
                    "BranchId": "br-dear-tern-753b****",
                    "BranchName": "main",
                    "BranchStatus": "Ready",
                    "BranchUsage": {
                        "BranchId": "br-dear-tern-753b****",
                        "ComputeTimeSeconds": 270,
                        "DataSizeTotalBytes": -1,
                        "DataSizeUsedBytes": 67141632,
                        "LastRunningTime": "2026-05-07T10:22:55Z",
                        "ServiceTimeSeconds": 33,
                        "StatTime": "2026-05-07T10:22:55Z",
                        "StorageSizeUsedBytes": 0,
                        "WorkspaceId": ""
                    },
                    "CreateTime": "2026-05-07T10:09:56.000Z",
                    "CreationSource": "SDK",
                    "Default": true,
                    "InitSource": "None",
                    "LastResetTime": "",
                    "Protected": false,
                    "StatusChangedTime": "2026-05-07T10:10:04.000Z",
                    "SupportAnalytic": false,
                    "UpdateTime": "2026-05-07T10:10:04.000Z",
                    "WorkspaceId": "zappy-fern-1756****"
                },
                "WorkspaceId": "zappy-fern-1756****"
            }
        ],
        "Total": 2
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
