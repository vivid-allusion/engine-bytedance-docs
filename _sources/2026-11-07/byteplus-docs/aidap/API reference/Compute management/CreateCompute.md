---
title: "CreateCompute"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/CreateCompute"
---

Call the CreateCompute API to create a compute.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* This API can only operate workspaces using the PostgreSQL engine and veDB MySQL engine.

* For workspaces using the PostgreSQL engine, each branch can have up to 20 computes. The primary compute can have up to 1, with a minimum of 0; read\-only compute and DuckDB read\-only compute can have up to 20 each, with a minimum of 0. You can call the [DescribeComputes](https://docs.byteplus.com/en/docs/aidap/DescribeComputes) API to query the existing compute information of a branch.

* 

   * 

   * 


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |ideal\-fir\-9fc8\*\*\*\* |ID of the workspace. |
|BranchId |String |Yes |br\-merry\-scup\-42d3\*\*\*\* |Branch ID. |
|ComputeSettings |Object of [ComputeSettings](https://docs.byteplus.com/en/docs/330/84425#computesettings) |Yes |Refer to the sample request. |Compute configuration. |
|ComputeName |String |No |test\-compute |Name of the compute. The compute name must meet the following rules:<br><br><br>* Must be 2 to 64 characters in length.<br><br>* It can only contain letters (a~z and A~Z), numbers (0~9), hyphens (\-), and underscores (_).<br><br>* It must start with a letter (a~z and A~Z) and end with a letter (a~z and A~Z) or a number (0~9). |


<span id="computesettings"></span>
### ComputeSettings


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|AutoScalingLimitMaxCU |Double |No |4 |The upper limit of the workspace automatic compute expansion range. Valid values include [0.25\|0.5\|1\|2\|3\|4\|5\|6\|7\|8\|9\|10\|11\|12\|13\|14\|15\|16\|18\|20\|22\|24\|26\|28\|30\|32]. The default value is 2. The unit is CU.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The valid ranges of AutoScalingLimitMaxCU and AutoScalingLimitMinCU are the same, but the value of AutoScalingLimitMaxCU must be greater than that of AutoScalingLimitMinCU.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The ratio of AutoScalingLimitMaxCU to AutoScalingLimitMinCU cannot exceed 8.</div><br> |
|AutoScalingLimitMinCU |Double |No | 1 |The lower limit of the workspace compute expansion range. Valid values are [0.25\|0.5\|1\|2\|3\|4\|5\|6\|7\|8\|9\|10\|11\|12\|13\|14\|15\|16\|18\|20\|22\|24\|26\|28\|30\|32]. The default value is 0.25. The unit is CU.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The valid ranges of AutoScalingLimitMaxCU and AutoScalingLimitMinCU are the same, but the value of AutoScalingLimitMaxCU must be greater than that of AutoScalingLimitMinCU.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The ratio of AutoScalingLimitMaxCU to AutoScalingLimitMinCU cannot exceed 8.</div><br> |
|ComputeRole |String |Yes |Primary |Role of the compute. Values:<br><br><br>* `Primary`: primary compute.<br><br>* `ReadOnly`: read\-only compute.<br><br>* `Analytic`: DuckDB read\-only compute.<br><br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If the branch already has a main compute, this parameter can only be <code>ReadOnly</code>. If the branch has no main compute, this parameter can be <code>Primary</code> or <code>ReadOnly</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">In the CreateBranch API, this parameter can only be <code>Primary</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If the branch currently has no primary compute, only primary compute or read\-only compute can be created, that is, the value can only be <code>Primary</code> or <code>ReadOnly</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If the AP acceleration function of the primary compute is enabled, DuckDB read\-only compute cannot be created, that is, the value cannot be <code>Analytic</code>.</div><br> |
|EnableAnalytic |String |No |Enabled |Status of the AP acceleration function. Values:<br><br><br>* `Enabled`: enabled.<br><br>* `Disabled`: disabled.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This field is valid only for workspaces using the PostgreSQL engine.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When used as a request parameter, the default value is <code>Disabled</code>.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|BranchId |String |br\-merry\-scup\-42d3\*\*\*\* |Branch ID. |
|ComputeId |String |cp\-cute\-fresh\-0e7d\*\*\*\* |Compute ID. |
|Compute |Object of [Compute](https://docs.byteplus.com/en/docs/330/84425#compute) |Refer to the sample response. |Details of the compute. |
|WorkspaceId |String |ideal\-fir\-9fc8\*\*\*\* |ID of the workspace. |


<span id="compute"></span>
### Compute


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|AutoScalingLimitMaxCU |Double |2 |The upper limit of the compute expansion range. |
|AutoScalingLimitMinCU |Double |0.25 |The lower limit of the compute expansion range. |
|BranchId |String |br\-merry\-scup\-42d3\*\*\*\* |Branch ID. |
|ComputeId |String |cp\-cute\-fresh\-0e7d\*\*\*\* |Compute ID. |
|ComputeName |String |cp\-cute\-fresh\-0e7d\*\*\*\* |Compute name. |
|ComputeRole |String |Primary |Role of the compute. Values:<br><br><br>* `Primary`: primary compute.<br><br>* `ReadOnly`: read\-only compute. |
|ComputeStatus |String |Active |Status of the compute.<br><br><br>* `Active`: Active, available for use.<br><br>* `Activating`: The branch is activating.<br><br>* `Idle`: Idle, stopped.<br><br>* `Init`: Initializing.<br><br>* `Modifying`: Changing.<br><br>* `Rebinding`: Rebinding.<br><br>* `Unknown`: The state is unknown.<br><br>* `Suspending`: Suspending.<br><br>* `Stopped`: Stopped.<br><br>* `Deleting`: Deleting.<br><br>* `Stopping`: Stopping.<br><br>* `Stopped`: Stopped.<br><br>* `Starting`: Starting.<br><br>* `Restarting`: Restarting. |
|CreateTime |String |2025\-10\-08T10:08:27Z |Creation time of the compute (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|CreationSource |String |Console |Source of compute creation. |
|Disabled |Boolean | false |Whether the compute is available. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|LastActiveTime |String |2025\-10\-08T10:08:38Z |The most recent activation time of the compute (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|StatusChangedTime |String |2025\-10\-08T10:08:38Z |The last status change time of the compute (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|SuspendedTime |String |2025\-10\-08T10:08:27Z |Compute suspension time (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|UpdateTime |String |2025\-10\-08T10:08:38Z |Compute update time (UTC). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|ServiceType |String |Database |Compute type. Values:<br><br><br>* `Database`: Database management service compute.<br><br>* `Supabase`: Supabase service compute.<br><br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default">When the engine type used by workspace is PostgreSQL, the return value is only <code>Database</code>.</div><br> |
|WorkspaceId |String |ideal\-fir\-9fc8\*\*\*\* |ID of the workspace. |
|EnableAnalytic |String |Enabled |Workspace AP acceleration status. Currently only supports the value `Enabled`, which means enabling AP acceleration.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default">Currently, only enabling AP acceleration is supported, and disabling it after enabling is not supported.</div><br> |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=CreateCompute&Version=2025-10-01 HTTP/1.1
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "ideal-fir-9fc8****",
    "BranchId": "br-merry-scup-42d3****",
    "ComputeName": "test-computenode",
    "ComputeSettings": {
        "AutoScalingLimitMaxCU": 2,
        "AutoScalingLimitMinCU": 0.25,
        "ComputeRole": "ReadOnly"
    }
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateCompute",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "WorkspaceId": "ideal-fir-9fc8****",
        "BranchId": "br-merry-scup-42d3****",
        "ComputeId": "cp-cute-fresh-0e7d****",
        "Compute": 
            {
                "AutoScalingLimitMaxCU": 2,
                "AutoScalingLimitMinCU": 0.25,
                "BranchId": "br-merry-scup-42d3****",
                "ComputeId": "cp-cute-fresh-0e7d****",
                "ComputeName": "cp-cute-fresh-0e7d****",
                "ComputeRole": "Primary",
                "ComputeStatus": "Active",
                "CreateTime": "2025-10-08T06:54:51Z",
                "CreationSource": "Console",
                "Disabled": false,
                "EnableAnalytics": "Enabled",
                "WorkspaceId": "ideal-fir-9fc8****",
                "LastActiveTime": "2025-10-08T06:55:06Z",
                "ServiceType": "Database",
                "StatusChangedTime": "2025-10-08T06:55:06Z",
                "SuspendTimeoutSeconds": 300,
                "SuspendedTime": "",
                "UpdateTime": "2025-10-08T06:55:06Z"
            }
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
