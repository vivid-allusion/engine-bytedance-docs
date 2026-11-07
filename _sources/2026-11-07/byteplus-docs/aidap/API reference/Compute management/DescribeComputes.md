---
title: "DescribeComputes"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/DescribeComputes"
---

Call the DescribeComputes API to query the compute list of the branch.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |ideal\-fir\-9fc8\*\*\*\* |ID of the workspace. |
|BranchId |String |Yes |br\-merry\-scup\-42d3\*\*\*\* |Branch ID. |
|ServiceType |String |No |Database |Specify the compute type. Values:<br><br><br>* `Database`: Compute of database management service. Default value.<br><br>* `Supabase`: Compute of Supabase service. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Computes |Array of [Compute](https://docs.byteplus.com/en/docs/330/84431#compute) |Refer to the sample response. |List of computes for the branch. |
|Total |Integer |1 |Total compute of the branch. |


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
|ComputeStatus |String |Active |Status of the compute.<br><br><br>* `Active`: active, available for use.<br><br>* `Activating`: The branch is activating.<br><br>* `Idle`: Idle, stopped.<br><br>* `Init`: Initializing.<br><br>* `Modifying`: Changing.<br><br>* `Rebinding`: Rebinding.<br><br>* `Unknown`: The state is unknown.<br><br>* `Suspending`: Suspending.<br><br>* `Stopped`: Stopped.<br><br>* `Deleting`: Deleting.<br><br>* `Stopping`: Stopping.<br><br>* `Stopped`: Stopped.<br><br>* `Starting`: Starting.<br><br>* `Restarting`: Restarting. |
|CreateTime |String |2025\-10\-08T10:08:27Z |Creation time of the compute (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|CreationSource |String |Console |Source of compute creation. |
|Disabled |Boolean | false |Whether the compute is available. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|EnableAnalytics |String |Disabled |Status of the compute's AP acceleration function. Values:<br><br><br>* `Enabled`: enabled.<br><br>* `Disabled`: disabled. |
|LastActiveTime |String |2025\-10\-08T10:08:38Z |The most recent activation time of the compute (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|StatusChangedTime |String |2025\-10\-08T10:08:38Z |The last status change time of the compute (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|SuspendedTime |String |2025\-10\-08T10:08:27Z |Compute suspension time (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|UpdateTime |String |2025\-10\-08T10:08:38Z |Compute update time (UTC). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|ServiceType |String |Database |Compute type. Values:<br><br><br>* `Database`: Database management service compute.<br><br>* `Supabase`: Supabase service compute.<br><br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default">When the engine type used by the workspace is PostgreSQL, the return value is only <code>Database</code>.</div><br> |
|WorkspaceId |String |ideal\-fir\-9fc8\*\*\*\* |ID of the workspace. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=DescribeComputes&Version=2025-10-01 HTTP/1.1
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
        "RequestId": "202510161509365BA017521BC12FB90135-50ddef",
        "Action": "DescribeComputes",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "Computes": [
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
                "WorkspaceId": "noble-heath-3a48****",
                "LastActiveTime": "2025-10-08T06:55:06Z",
                "StatusChangedTime": "2025-10-08T06:55:06Z",
                "SuspendTimeoutSeconds": 300,
                "SuspendedTime": "",
                "UpdateTime": "2025-10-08T06:55:06Z"
            },
            {
                "AutoScalingLimitMaxCU": 2,
                "AutoScalingLimitMinCU": 0.25,
                "BranchId": "br-merry-scup-42d3****",
                "ComputeId": "cp-neat-pure-7ec8****",
                "ComputeName": "ReadReplica-1-8vzx",
                "ComputeRole": "ReadOnly"
                "ComputeStatus": "Active",
                "CreateTime": "2025-10-08T10:08:25Z",
                "CreationSource": "Console",
                "Disabled": false,
                "EnableAnalytics": "Enabled",
                "WorkspaceId": "noble-heath-3a48****",
                "LastActiveTime": "2025-10-08T10:08:38Z",
                "StatusChangedTime": "2025-10-08T10:08:38Z",
                "SuspendTimeoutSeconds": 0,
                "SuspendedTime": "2025-10-08T10:08:25Z",
                "UpdateTime": "2025-10-08T10:08:38Z"
            },
            {
                "AutoScalingLimitMaxCU": 2,
                "AutoScalingLimitMinCU": 0.25,
                "BranchId": "br-merry-scup-42d3****",
                "ComputeId": "cp-brave-hills-ad69****",
                "ComputeName": "ReadReplica-2-tucz",
                "ComputeRole": "ReadOnly"
                "ComputeStatus": "Active",
                "CreateTime": "2025-10-08T10:08:27Z",
                "CreationSource": "Console",
                "Disabled": false,
                "EnableAnalytics": "Disabled",
                "WorkspaceId": "noble-heath-3a48****",
                "LastActiveTime": "2025-10-08T10:08:40Z",
                "ServiceType": "Database",
                "StatusChangedTime": "2025-10-08T10:08:40Z",
                "SuspendTimeoutSeconds": 0,
                "SuspendedTime": "2025-10-08T10:08:27Z",
                "UpdateTime": "2025-10-08T10:08:40Z"
            }
        ],
        "Total": 3
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
