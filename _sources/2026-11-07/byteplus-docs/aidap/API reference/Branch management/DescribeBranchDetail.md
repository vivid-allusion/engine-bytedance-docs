---
title: "DescribeBranchDetail"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/DescribeBranchDetail"
---

Call the DescribeBranchDetail API to query detailed information about the branch.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeBranchDetail&serviceCode=aidap&version=2025-10-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |noble\-heath\-3a48a1c7 |ID of the workspace. |
|BranchId |String |Yes |br\-merry\-scup\-42d3\*\*\*\* |Branch ID. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Branch |Object of [Branch](https://docs.byteplus.com/en/docs/330/84415#branch) |Refer to the sample response. |Details of the branch. |
|WorkspaceName |String |TestWorkspace |Name of the workspace. |


<span id="branch"></span>
### Branch


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Archived |Boolean |false |Whether the branch is archived. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|BranchId |String |br\-bloom\-duck\-61c7\*\*\*\* |Branch ID. |
|BranchName |String |childbranch |Name of the branch. |
|BranchStatus |String |Ready |Branch status. Values:<br><br><br>* `Unknown`: the branch state is unknown.<br><br>* `Init`: the branch is initializing.<br><br>* `Activating`: the branch is activating.<br><br>* `Ready`: the branch is ready.<br><br>* `Archived`: the branch is archived.<br><br>* `Deleted`: the branch is deleted.<br><br>* `Resetting`: the branch is resetting.<br><br>* `Deleting`: the branch is being deleted.<br><br>* `Stopping`: Stopping.<br><br>* `Stopped`: Stopped.<br><br>* `Suspending`: Suspending.<br><br>* `Suspended`: Suspended.<br><br>* `Replacing`: Replacing compute resources.<br><br>* `Restarting`: Restarting.<br><br>* `Updating`: Updating. |
|BranchUsage |Object of [BranchUsage](https://docs.byteplus.com/en/docs/330/84415#branchusage) |Refer to the sample response. |Resource usage information of the branch. |
|CreateTime |String |2025\-10\-08T10:51:06.000Z |Creation time of the branch (UTC time). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|CreationSource |String |Console |The branch's creation source. Value is `Console`. |
|Default |Boolean |false |The branch is default branch or not. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|InitSource |String |ParentData |Branch initialization source, default is `ParentData`.<br><br><br>* `ParentData`: Schema and data.<br><br>* `SchemaOnly`: Schema only. |
|LastResetTime |String |2025\-10\-07T08:57:21.000Z |Last reset time of the branch (UTC time). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If the branch has not been reset, returns empty.</div><br> |
|ParentBranch |Object of [ParentBranch](https://docs.byteplus.com/en/docs/330/84415#parentbranch) |Refer to the sample response. |Parent branch information of this branch.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If the branch has no parent branch, this field is not returned.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When the <a href="https://docs.byteplus.com/en/docs/330/84415#branch">Branch</a> data structure is used to describe ParentBranch, only the BranchId, BranchName, BranchStatus, and WorkspaceId fields are returned.</div><br> |
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
|VectorReadVCU |Double |19.22 |Resources consumed when performing retrieval, query, and other read operations on vector data in the vector bucket. Unit is vCU.<br><br><div data-tips="true" data-tips-type="default">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This field is returned only for workspaces using the Supabase engine.</div><br> |
|VectorWriteVCU |Double |7.3 |Resources consumed for writing, updating, or deleting vector data in the vector bucket. Unit is vCU.<br><br><div data-tips="true" data-tips-type="default">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This field is returned only for workspaces using the Supabase engine.</div><br> |
|VectorStorageSizeUsedBytes |Long |909805 |Storage space occupied by vector data stored in vector bucket. Unit is byte.<br><br><div data-tips="true" data-tips-type="default">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This field is returned only for workspaces using the Supabase engine.</div><br> |


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
POST /?Action=DescribeBranchDetail&Version=2025-10-01 HTTP/1.1
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "frank-melon-9dd3****",
    "BranchId": "br-witty-coot-3ccf****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2025102115353138042958D2259EDD320E-d9699b",
        "Action": "DescribeBranchDetail",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "Branch": {
            "Archived": false,
            "BranchId": "br-witty-coot-3ccf****",
            "BranchName": "branch-qozbqkt6",
            "BranchStatus": "Ready",
            "BranchUsage": {
                "BranchId": "br-witty-coot-3ccf****",
                "ComputeTimeSeconds": 2520,
                "DataSizeTotalBytes": -1,
                "DataSizeUsedBytes": 24576,
                "LastRunningTime": "2025-10-21 07:34:33 +0000 UTC",
                "StatTime": "2025-10-21 07:34:33 +0000 UTC",
                "WorkspaceId": "frank-melon-9dd3****"
            },
            "CreateTime": "2025-10-21T06:51:07.000Z",
            "CreationSource": "Console",
            "Default": false,
            "InitSource": "ParentData",
            "LastResetTime": "",
            "ParentBranch": {
                "BranchId": "br-sharp-ibis-3eea****",
                "BranchName": "main",
                "BranchStatus": "Ready",
                "WorkspaceId": "frank-melon-9dd3****"
            },
            "Protected": false,
            "StartParentLSN": "0/20984A8",
            "StartParentTime": "2025-10-21T06:51:06.000Z",
            "StatusChangedTime": "2025-10-21T06:51:22.000Z",
            "SupportAnalytic": false,
            "UpdateTime": "2025-10-21T06:51:22.000Z",
            "WorkspaceId": "frank-melon-9dd3****"
        },
        "WorkspaceName": "测试"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
