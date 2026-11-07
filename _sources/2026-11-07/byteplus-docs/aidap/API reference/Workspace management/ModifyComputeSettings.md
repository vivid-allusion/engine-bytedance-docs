---
title: "ModifyComputeSettings"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/ModifyComputeSettings"
---

Call the ModifyComputeSettings API to modify the initial compute settings of the workspace.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

This API can only be used to operate a workspace using the PostgreSQL engine or Supabase engine.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyComputeSettings&serviceCode=aidap&version=2025-10-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |ideal\-fir\-9fc8\*\*\*\* |ID of the workspace. |
|AutoScalingLimitMaxCU |Double |Yes |2 |The upper limit of the compute automatic expansion range. The unit is CU.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">AutoScalingLimitMaxCU and AutoScalingLimitMinCU share the same value range.</div><br><br><br>   * <div data-tips="true" data-tips-type="default">When the compute specified by ComputeId is the database management service compute, the valid values are [0.25\|0.5\|1\|2\|3\|4\|5\|6\|7\|8\|9\|10\|11\|12\|13\|14\|15\|16\|18\|20\|22\|24\|26\|28\|30\|32].</div><br><br><br>   * <div data-tips="true" data-tips-type="default">When the compute specified by ComputeId is the Supabase service compute, the valid values are [0.5\|1\|2\|3\|4\|5\|6\|7\|8\|9\|10\|11\|12\|13\|14\|15\|16\|18\|20\|22\|24\|26\|28\|30\|32].</div><br><br><br>* <div data-tips="true" data-tips-type="default">The value of AutoScalingLimitMaxCU must be greater than that of AutoScalingLimitMinCU, but the ratio of AutoScalingLimitMaxCU to AutoScalingLimitMinCU cannot exceed 8.</div><br> |
|AutoScalingLimitMinCU |Double |Yes |0.25 |The lower limit of the compute expansion range. The unit is CU.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">AutoScalingLimitMaxCU and AutoScalingLimitMinCU share the same value range.</div><br><br><br>   * <div data-tips="true" data-tips-type="default">When the compute specified by ComputeId is the database management service compute, the valid values are [0.25\|0.5\|1\|2\|3\|4\|5\|6\|7\|8\|9\|10\|11\|12\|13\|14\|15\|16\|18\|20\|22\|24\|26\|28\|30\|32].</div><br><br><br>   * <div data-tips="true" data-tips-type="default">When the compute specified by ComputeId is the Supabase service compute, the valid values are [0.5\|1\|2\|3\|4\|5\|6\|7\|8\|9\|10\|11\|12\|13\|14\|15\|16\|18\|20\|22\|24\|26\|28\|30\|32].</div><br><br><br>* <div data-tips="true" data-tips-type="default">The value of AutoScalingLimitMaxCU must be greater than that of AutoScalingLimitMinCU, but the ratio of AutoScalingLimitMaxCU to AutoScalingLimitMinCU cannot exceed 8.</div><br> |
|SuspendTimeoutSeconds |Integer |No |600 |Idle duration before suspend. The node is automatically suspended after the compute has no activity for the set time. The value range is an integer between `-1` or `300` and `604,800`. The default value is 300 seconds. The unit is second.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">A value of <code>-1</code> means the compute never suspends.</div><br> |
|ServiceType |String |No |Database |Specify the compute type. Values:<br><br><br>* `Database`: Compute of database management service. Default value.<br><br>* `Supabase`: Compute of Supabase service.<br><br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This field is valid only for workspaces using the Supabase engine.</div><br><br><br>* <div data-tips="true" data-tips-type="default">In workspaces using the Supabase engine, this field specifies the target for the compute expansion range parameters (AutoScalingLimitMaxCU and AutoScalingLimitMinCU). The idle duration before suspend parameter (SuspendTimeoutSeconds) targets the workspace and is not affected by this field.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|WorkspaceId |String |ideal\-fir\-9fc8\*\*\*\* |ID of the workspace. |
|Workspace |Object of [Workspace](https://docs.byteplus.com/en/docs/330/84403#workspace) |Refer to the sample response. |Detailed information about the workspace. |


<span id="workspace"></span>
### Workspace


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|AccountId |String |210036\*\*\*\* |ID of the tenant to which the workspace belongs. |
|AgentPlanSeatId |String |seat\-20260615134321\-kjvvx |Seat ID of the Agent Plan.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is returned only for the enterprise edition using the Agent Plan.</div><br> |
|BaasComputeSettings |Object of [DefaultComputeSettings](https://docs.byteplus.com/en/docs/330/84403#defaultcomputesettings) |Refer to the Sample response. |Configuration information for Supabase service compute.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default">This field is returned only for workspaces using the Supabase engine.</div><br> |
|ComputeSettings |Object of [DefaultComputeSettings](https://docs.byteplus.com/en/docs/330/84403#defaultcomputesettings) |Refer to the sample response. |Compute configuration information of the workspace |
|CreateTime |String |2025\-10\-20T06:47:49Z |Creation time of the workspace (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|CreationSource |String |Console |Creation source of the workspace. Values:<br><br><br>* `AIPA`: created via AIPA.<br><br>* `CLI`: created via CLI.<br><br>* `Console`: created via Console.<br><br>* `Coze`: created via Coze.<br><br>* `MCP`: created via MCP.<br><br>* `SDK`: created via SDK.<br><br>* `Terraform`: Created via Terraform.<br><br>* `Trae`: Created via Trae.<br><br>* `Unknown`: Unknown creation source. |
|DeletionProtectionStatus |String |Enable |The status of the workspace deletion protection function. Values:<br><br><br>* `AllowDeletion`: deletion protection is disabled. The workspace can be deleted directly.<br><br>* `DeletionProtectionEnable`: deletion protection is enabled. The workspace cannot be deleted directly. |
|DNSVisibility |Boolean |false |Whether the public network resolves private network domain names is enabled. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|EngineType |String |PostgreSQL |Engine type. Values:<br><br><br>* `PostgreSQL`: PostgreSQL engine.<br><br>* <br><br>* `Supabase`: Supabase engine. |
|EngineVersion |String |PostgreSQL_17 |Engine version. Values:<br><br><br>* `PostgreSQL_17`: PostgreSQL 17.<br><br>* <br><br>* `Supabase_1_24`: Supabase 1.24. |
|InternetProtocol |String |IPv4 |IP address protocol version used by the workspace.<br><br><br>* `DualStack`: IPv4 + IPv6.<br><br>* `IPv4`: IPv4. |
|IsAgentPlan |Boolean |true |Whether the workspace is used for Agent Plan. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. Default value. |
|ProjectName |String |default |Name of the project to which the workspace belongs. |
|RegionId |String |cn\-beijing |The ID of the region where the workspace resides. |
|SharedPrivateNetwork |Boolean |true |Whether shared mode is enabled for the Virtual Private Cloud of the workspace. After enabling, the workspace supports wildcard domain access, and does not add new resolution records for each compute node. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no.<br><br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default">This field is not returned when not enabled.</div><br> |
|StatusChangedTime |String |2025\-10\-20T06:48:15Z |Workspace status change time (UTC). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|SubnetId |String |subnet\-3rf442t6a54w016nf3pg9\*\*\*\* |The ID of the subnet used by the workspace. |
|UpdateTime |String |2025\-10\-21T05:32:19Z |The update time of the workspace (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|VpcId |String |vpc\-3ezxu117lv18g72200rro\*\*\*\* |ID of the private network used by the workspace.<br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">Returns empty if the workspace does not use a virtual private cloud.</div><br> |
|WorkspaceId |String |ideal\-fir\-9fc8\*\*\*\* |ID of the workspace. |
|WorkspaceName |String |TestWorkspace |Name of the workspace. |
|WorkspaceSetting |Object of [DefaultWorkspaceSettings](https://docs.byteplus.com/en/docs/330/84403#defaultworkspacesettings) |Refer to the sample response. |Configuration information of the workspace. |
|WorkspaceStatus |String |Running |Running status of the workspace. Values:<br><br><br>* `Unknown`: Unknown status.<br><br>* `Creating`: Creating.<br><br>* `CreateFailed`: Failed to create.<br><br>* `Updating`: Modifying.<br><br>* `Running`: Running.<br><br>* `Deleted`: Deleted.<br><br>* `Error`: Abnormal.<br><br>* `NetworkChanging`: Network changing.<br><br>* `Closing`: Billing shutting down.<br><br>* `Closed`: Shutdown.<br><br>* `Resuming`: Restoring from billing shutdown.<br><br>* `Stopping`: Stopping.<br><br>* `Stopped`: Stopped.<br><br>* `Starting`: Starting.<br><br>* `Suspending`: Suspending.<br><br>* `Suspended`: Suspended. |
|WorkspaceUsage |Object of [WorkspaceUsage](https://docs.byteplus.com/en/docs/330/84403#workspaceusage) |Refer to the return example. |Workspace usage details: used storage space, used compute, etc. |
|WorkspaceTags |Array of [Tag](https://docs.byteplus.com/en/docs/330/84403#tag) |Refer to the sample response. |Tags for the workspace.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default">If no tags are bound to the workspace, it returns<code>null</code>。</div><br> |


<span id="defaultcomputesettings"></span>
### DefaultComputeSettings


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|AutoScalingLimitMaxCU |Double |4 |The upper limit of the workspace automatic compute expansion range. Valid values include [0.25\|0.5\|1\|2\|3\|4\|5\|6\|7\|8\|9\|10\|11\|12\|13\|14\|15\|16\|18\|20\|22\|24\|26\|28\|30\|32]. The default value is 2. The unit is CU.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The valid ranges of AutoScalingLimitMaxCU and AutoScalingLimitMinCU are the same, but the value of AutoScalingLimitMaxCU must be greater than that of AutoScalingLimitMinCU.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The ratio of AutoScalingLimitMaxCU to AutoScalingLimitMinCU cannot exceed 8.</div><br> |
|AutoScalingLimitMinCU |Double |0.25 |The lower limit of the workspace automatic compute expansion range. Valid values are [0.25\|0.5\|1\|2\|3\|4\|5\|6\|7\|8\|9\|10\|11\|12\|13\|14\|15\|16\|18\|20\|22\|24\|26\|28\|30\|32]. The default value is 0.25. The unit is CU.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The valid ranges of AutoScalingLimitMaxCU and AutoScalingLimitMinCU are the same, but the value of AutoScalingLimitMaxCU must be greater than that of AutoScalingLimitMinCU.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The ratio of AutoScalingLimitMaxCU to AutoScalingLimitMinCU cannot exceed 8.</div><br> |
|SuspendTimeoutSeconds |Integer |300 |Idle duration before suspend. The node is automatically suspended after the compute has no activity for the set time. A value of `-1` indicates that the node will never be suspended. |
|EnableAnalytic |String |Enabled |Workspace AP acceleration status. Values:<br><br><br>* `Enabled`: enabled.<br><br>* `Disabled`: disabled.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This field is valid only for workspaces using the PostgreSQL engine.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When used as a request parameter, the default value is <code>Disabled</code>.</div><br> |


<span id="defaultworkspacesettings"></span>
### DefaultWorkspaceSettings


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|DeletionProtection |String |Enabled |The status of the workspace deletion protection function. Values:<br><br><br>* `Enabled`: the function is enabled. Default value.<br><br>* `Disabled`: the function is disabled. |
|HistoryRetentionHours |Integer |48 |Traceability duration of the workspace. Value range is 1 to 720, default value is 48, unit is hour. |
|PublicConnection |String |Enabled |Status of workspace shared public network function. Values:<br><br><br>* `Enabled`: the function is enabled.<br><br>* `Disabled`: the function is disabled. |


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


<span id="tag"></span>
### Tag


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Key |String |key1 |Tag key. |
|Value |String |value1 |Value of tag. |
|System |Boolean |false |Whether it is a system tag. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=ModifyComputeSettings&Version=2025-10-01 HTTP/1.1
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "witty-senna-6d08****",
    "AutoScalingLimitMaxCU": 3,
    "AutoScalingLimitMinCU": 1
    }
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyComputeSettings",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "Workspace": {
            "AccountId": "210000****",
            "ComputeSettings": {
                "AutoScalingLimitMaxCU": 3,
                "AutoScalingLimitMinCU": 1,
                "EnableAnalytics":"Enabled",
                "SuspendTimeoutSeconds": -1
            },
            "CreateTime": "2025-10-20T06:47:49Z",
            "CreationSource": "Console",
            "DNSVisibility": false,
            "DeletionProtectionStatus": "AllowDeletion",
            "EngineType": "PostgreSQL",
            "EngineVersion": "PostgreSQL_17",
            "InternetProtocol": "IPv4",
            "ProjectName": "default",
            "RegionId": "cn-beijing",
            "StatusChangedTime": "2025-10-20T06:48:15Z",
            "StorageSize": -1,
            "StorageType": "StoragePool",
            "SubnetId": "",
            "UpdateTime": "2025-10-20T14:01:28Z",
            "VpcId": "",
            "WorkspaceId": "witty-senna-6d08****",
            "WorkspaceName": "测试Workspace",
            "WorkspaceSetting": {
                "DeletionProtection": "Disabled",
                "HistoryRetentionHours": 48,
                "PublicConnection": "Disabled"
            },
            "WorkspaceStatus": "Running",
            "WorkspaceUsage": null
        },
        "WorkspaceId": "witty-senna-6d08****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
