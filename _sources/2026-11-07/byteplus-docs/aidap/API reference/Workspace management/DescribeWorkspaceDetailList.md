---
title: "DescribeWorkspaceDetailList"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/DescribeWorkspaceDetailList"
---

Call the DescribeWorkspaceDetailList API to query detailed information for multiple workspaces.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeWorkspaceDetailList&serviceCode=aidap&version=2025-10-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceIds |Array of String |Yes |["noble\-heath\-3a48\*\*\*\*","stoic\-chili\-ab80\*\*\*\*"] |List of workspace IDs.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default">Up to 20 workspace IDs can be input.</div><br> |
|Offset |Integer |No |1 |Starting point for paginated query, an integer greater than or equal to 0, default value is 0. |
|Limit |Integer |No |20 |Pagination query count can be an integer greater than or equal to 1, with a default value of 10. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Total |Integer |20 |The quantity of results that meet the query conditions. |
|Workspaces |Array of [Workspace](https://docs.byteplus.com/en/docs/330/106698#workspace) |Refer to the sample response. |Details of the specified workspace. |


<span id="workspace"></span>
### Workspace


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|AccountId |String |210036\*\*\*\* |ID of the tenant to which the workspace belongs. |
|AgentPlanSeatId |String |seat\-20260615134321\-kjvvx |Seat ID of the Agent Plan.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is returned only for the enterprise edition using the Agent Plan.</div><br> |
|BaasComputeSettings |Object of [DefaultComputeSettings](https://docs.byteplus.com/en/docs/330/106698#defaultcomputesettings) |Refer to the sample response. |Supabase service compute configuration information.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default">This field is returned only for workspaces using the Supabase engine.</div><br> |
|ComputeSettings |Object of [DefaultComputeSettings](https://docs.byteplus.com/en/docs/330/106698#defaultcomputesettings) |Refer to the sample response. |Compute configuration information of the workspace |
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
|WorkspaceSetting |Object of [DefaultWorkspaceSettings](https://docs.byteplus.com/en/docs/330/106698#defaultworkspacesettings) |Refer to the sample response. |Configuration information of the workspace. |
|WorkspaceStatus |String |Running |Running status of the workspace. Values:<br><br><br>* `Unknown`: Unknown status.<br><br>* `Creating`: Creating.<br><br>* `CreateFailed`: Failed to create.<br><br>* `Updating`: Modifying.<br><br>* `Running`: Running.<br><br>* `Deleted`: Deleted.<br><br>* `Error`: Abnormal.<br><br>* `NetworkChanging`: Network changing.<br><br>* `Closing`: Billing shutting down.<br><br>* `Closed`: Shutdown.<br><br>* `Resuming`: Restoring from billing shutdown.<br><br>* `Stopping`: Stopping.<br><br>* `Stopped`: Stopped.<br><br>* `Starting`: Starting.<br><br>* `Suspending`: Suspending.<br><br>* `Suspended`: Suspended. |
|WorkspaceUsage |Object of [WorkspaceUsage](https://docs.byteplus.com/en/docs/330/106698#workspaceusage) |Refer to the sample response. |Workspace usage details: used storage space, used compute, etc. |
|WorkspaceTags |Array of [Tag](https://docs.byteplus.com/en/docs/330/106698#tag) |Refer to the sample response. |Tags for the workspace.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default">If no tags are bound to the workspace, it returns<code>null</code>。</div><br> |


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
POST /?Action=DescribeWorkspaceDetailList&Version=2025-10-01
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
        "RequestId": "20260507181603903392A08CAB48E99ED0-61e03d",
        "Action": "DescribeWorkspaceDetailList",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "Total": 2,
        "Workspaces": [
            {
                "AccountId": "210000****",
                "BaasComputeSettings": {
                    "AutoScalingLimitMaxCU": 2,
                    "AutoScalingLimitMinCU": 0.5,
                    "SuspendTimeoutSeconds": -1
                },
                "ComputeSettings": {
                    "AutoScalingLimitMaxCU": 2,
                    "AutoScalingLimitMinCU": 0.25
                },
                "CreateTime": "2026-05-07T08:18:51Z",
                "CreationSource": "Console",
                "DNSVisibility": false,
                "DeletionProtectionStatus": "DeletionProtectionEnable",
                "EngineType": "Supabase",
                "EngineVersion": "Supabase_1_24",
                "ProjectName": "default",
                "RegionId": "cn-beijing",
                "StatusChangedTime": "2026-05-07T08:20:07Z",
                "StorageSize": -1,
                "StorageType": "StoragePool",
                "UpdateTime": "2026-05-07T08:20:07Z",
                "WorkspaceId": "perky-bluet-750****",
                "WorkspaceName": "测试1",
                "WorkspaceSetting": {
                    "DeletionProtection": "Enabled",
                    "HistoryRetentionHours": 48,
                    "PublicConnection": "Disabled"
                },
                "WorkspaceStatus": "Running",
                "WorkspaceTags": null,
                "WorkspaceUsage": {
                    "BranchComputeTimeSeconds": 3930,
                    "BranchCreatedNum": 4,
                    "ComputeTimeSeconds": 5400,
                    "DataSizeTotalBytes": -1,
                    "DataSizeUsedBytes": 87965696,
                    "ServiceTimeSeconds": 967,
                    "StatTime": "2026-05-07T09:57:06Z",
                    "StorageSizeUsedBytes": 0
                }
            },
            {
                "AccountId": "210000****",
                "BaasComputeSettings": {
                    "AutoScalingLimitMaxCU": 2,
                    "AutoScalingLimitMinCU": 0.5,
                    "SuspendTimeoutSeconds": -1
                },
                "ComputeSettings": {
                    "AutoScalingLimitMaxCU": 2,
                    "AutoScalingLimitMinCU": 0.25
                },
                "CreateTime": "2026-05-07T10:09:49Z",
                "CreationSource": "Console",
                "DNSVisibility": false,
                "DeletionProtectionStatus": "DeletionProtectionEnable",
                "EngineType": "Supabase",
                "EngineVersion": "Supabase_1_24",
                "ProjectName": "default",
                "RegionId": "cn-beijing",
                "StatusChangedTime": "2026-05-07T10:11:13Z",
                "StorageSize": -1,
                "StorageType": "StoragePool",
                "UpdateTime": "2026-05-07T10:11:14Z",
                "WorkspaceId": "zappy-fern-1756****",
                "WorkspaceName": "测试2",
                "WorkspaceSetting": {
                    "DeletionProtection": "Enabled",
                    "HistoryRetentionHours": 48,
                    "PublicConnection": "Disabled"
                },
                "WorkspaceStatus": "Running",
                "WorkspaceTags": null,
                "WorkspaceUsage": {
                    "BranchComputeTimeSeconds": 0,
                    "BranchCreatedNum": 0,
                    "ComputeTimeSeconds": 0,
                    "DataSizeTotalBytes": -1,
                    "DataSizeUsedBytes": 0,
                    "FunctionCallNum": 0,
                    "ServiceTimeSeconds": 0,
                    "StatTime": "2026-05-07T10:09:49Z",
                    "StorageSizeUsedBytes": 0
                }
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
