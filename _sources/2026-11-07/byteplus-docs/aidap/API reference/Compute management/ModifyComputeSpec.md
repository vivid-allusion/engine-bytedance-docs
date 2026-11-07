---
title: "ModifyComputeSpec"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/ModifyComputeSpec"
---

Call the ModifyComputeSpec API to modify the specification.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

This API can only be used to operate a workspace using the PostgreSQL engine or Supabase engine.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyComputeSpec&serviceCode=aidap&version=2025-10-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |ideal\-fir\-9fc8\*\*\*\* |ID of the workspace. |
|ComputeId |String |Yes |cp\-brave\-hills\-ad69\*\*\*\* |Compute ID. |
|AutoScalingLimitMaxCU |Double |Yes |4 |The upper limit of the compute automatic expansion range. The unit is CU.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">AutoScalingLimitMaxCU and AutoScalingLimitMinCU share the same value range.</div><br><br><br>   * <div data-tips="true" data-tips-type="default">When the compute specified by ComputeId is the database management service compute, the valid values are [0.25\|0.5\|1\|2\|3\|4\|5\|6\|7\|8\|9\|10\|11\|12\|13\|14\|15\|16\|18\|20\|22\|24\|26\|28\|30\|32].</div><br><br><br>   * <div data-tips="true" data-tips-type="default">When the compute specified by ComputeId is the Supabase service compute, the valid values are [0.5\|1\|2\|3\|4\|5\|6\|7\|8\|9\|10\|11\|12\|13\|14\|15\|16\|18\|20\|22\|24\|26\|28\|30\|32].</div><br><br><br>* <div data-tips="true" data-tips-type="default">The value of AutoScalingLimitMaxCU must be greater than that of AutoScalingLimitMinCU, but the ratio of AutoScalingLimitMaxCU to AutoScalingLimitMinCU cannot exceed 8.</div><br> |
|AutoScalingLimitMinCU |Double |Yes |1 |The lower limit of the compute expansion range. The unit is CU.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">AutoScalingLimitMaxCU and AutoScalingLimitMinCU share the same value range.</div><br><br><br>   * <div data-tips="true" data-tips-type="default">When the compute specified by ComputeId is the database management service compute, the valid values are [0.25\|0.5\|1\|2\|3\|4\|5\|6\|7\|8\|9\|10\|11\|12\|13\|14\|15\|16\|18\|20\|22\|24\|26\|28\|30\|32].</div><br><br><br>   * <div data-tips="true" data-tips-type="default">When the compute specified by ComputeId is the Supabase service compute, the valid values are [0.5\|1\|2\|3\|4\|5\|6\|7\|8\|9\|10\|11\|12\|13\|14\|15\|16\|18\|20\|22\|24\|26\|28\|30\|32].</div><br><br><br>* <div data-tips="true" data-tips-type="default">The value of AutoScalingLimitMaxCU must be greater than that of AutoScalingLimitMinCU, but the ratio of AutoScalingLimitMaxCU to AutoScalingLimitMinCU cannot exceed 8.</div><br> |
|EffectType |String |No |NextWakeUp |Effective time for the compute specification modification. Values:<br><br><br>* `Immediate`: If the workspace is running, the specification will be modified immediately after the request is sent. Default value.<br><br>* `NextWakeUp`: If the workspace is running, the request will not change the specifications but will take effect after the next suspend wake\-up. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|ComputeId |String |cp\-brave\-hills\-ad69\*\*\*\* |Compute ID. |
|Compute |Object of [Compute](https://docs.byteplus.com/en/docs/330/84429#compute) |Refer to the return example. |Details of the compute. |
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
|ComputeStatus |String |Active |Status of the compute.<br><br><br>* `Active`: active, available for use.<br><br>* `Activating`: The branch is activating.<br><br>* `Idle`: Idle, stopped.<br><br>* `Init`: Initializing.<br><br>* `Modifying`: Changing.<br><br>* `Rebinding`: Rebinding.<br><br>* `Unknown`: The state is unknown.<br><br>* `Suspending`: Suspending.<br><br>* `Stopped`: Stopped.<br><br>* `Deleting`: Deleting.<br><br>* `Stopping`: Stopping.<br><br>* `Stopped`: Stopped.<br><br>* `Starting`: Starting.<br><br>* `Restarting`: Restarting. |
|CreateTime |String |2025\-10\-08T10:08:27Z |Creation time of the compute (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|CreationSource |String |Console |Source of compute creation. |
|Disabled |Boolean | false |Whether the compute is available. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|LastActiveTime |String |2025\-10\-08T10:08:38Z |The most recent activation time of the compute (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|StatusChangedTime |String |2025\-10\-08T10:08:38Z |The last status change time of the compute (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|SuspendedTime |String |2025\-10\-08T10:08:27Z |Compute suspension time (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|UpdateTime |String |2025\-10\-08T10:08:38Z |Compute update time (UTC). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|ServiceType |String |Database |Compute type. Values:<br><br><br>* `Database`: Database management service compute.<br><br>* `Supabase`: Supabase service compute.<br><br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default">When the engine type used by the workspace is PostgreSQL, the return value is only <code>Database</code>.</div><br> |
|WorkspaceId |String |ideal\-fir\-9fc8\*\*\*\* |ID of the workspace. |
|EnableAnalytic |String |Enabled |Workspace AP acceleration status. Currently only supports the value `Enabled`, which means enabling AP acceleration.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default">Currently, only enabling AP acceleration is supported, and disabling it after enabling is not supported.</div><br> |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=ModifyComputeSpec&Version=2025-10-01 HTTP/1.1
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "ideal-fir-9fc8****",
    "ComputeId": "cp-brave-hills-ad69****",
    "AutoScalingLimitMinCU": 1,
    "AutoScalingLimitMaxCU": 4
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyComputeSpec",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "ComputeId": "cp-brave-hills-ad69****",
        "Compute": {
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
            "EnableAnalytics": "Enabled",
            "WorkspaceId": "ideal-fir-9fc8****",
            "LastActiveTime": "2025-10-08T10:08:40Z",
             "ServiceType": "Database",
            "StatusChangedTime": "2025-10-08T10:08:40Z",
            "SuspendTimeoutSeconds": -1,
            "SuspendedTime": "2025-10-08T10:08:27Z",
            "UpdateTime": "2025-10-08T10:08:40Z"
        },
        "WorkspaceId": "ideal-fir-9fc8****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
