---
title: "DescribeWorkspaces"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/DescribeWorkspaces"
---

Call the DescribeWorkspaces API to query the list of Workspaces.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeWorkspaces&serviceCode=aidap&version=2025-10-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|ProjectName |String |No |default |Specify the items to query. |
|Limit |Integer |No |5 |Pagination query count can be an integer greater than or equal to 1, with a default value of 10. |
|Offset |Integer |No |1 |Starting point for paginated query, an integer greater than or equal to 0, default value is 0. |
|Search |String |No |Test |Search keywords. Supports fuzzy search by workspace ID or workspace name. |
|SortBy |String |No |create_time |Sort fields, values:<br><br><br>* `update_time`: Update time. Default value.<br><br>* `create_time`: Creation time.<br><br>* `workspace_name`: Name of the workspace. |
|SortOrder |String |No |Asc |Sorting method.<br><br><br>* `Asc`: ascending order.<br><br>* `Desc`: descending order. Default value. |
|Filters |Array of [QueryFilter](https://docs.byteplus.com/en/docs/330/84448#queryfilter) |No |Refer to the sample request. |Filter conditions for the query. |
|WorkspaceTags |Array of [TagOption](https://docs.byteplus.com/en/docs/330/84448#tagoption) |No |See the request example. |Query array objects by tag.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">It supports querying and filtering up to 10 tag key\-value pairs simultaneously per request.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If multiple tags are specified for query, the relationship between multiple tag keys is "and," and different tag values for the same tag key are in an "or" relationship.</div><br> |
|NextToken |String |No | |Used for cursor pagination query.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Pass a valid value to NextToken to use cursor pagination query. If not passed, pagination query will continue.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For the first cursor pagination query, pass <code>None</code>.</div><br> |


<span id="queryfilter"></span>
### QueryFilter


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Name |String |Yes |WorkspaceStatus |Filter options for querying. Values:<br><br><br>* `WorkspaceStatus`: Query by workspace status.<br><br>* `DBEngineVersion`: Query by engine type. |
|Value |String |Yes |"CreateFailed,Error" |Specify the filter value for the filter option.<br><br><br>* When the parameter Name is set to `WorkspaceStatus`, the possible values for Value are:<br><br>   * `Unknown`: Unknown status.<br><br>   * `Creating`: Creating.<br><br>   * `CreateFailed`: Failed to create.<br><br>   * `Updating`: Modifying.<br><br>   * `Running`: Running.<br><br>   * `Deleted`: Deleted.<br><br>   * `Error`: Abnormal.<br><br>   * `NetworkChanging`: Network changing.<br><br>   * `Closing`: Billing shutting down.<br><br>   * `Closed`: Shutdown.<br><br>   * `Resuming`: Restoring from billing shutdown.<br><br>   * `Stopping`: Stopping.<br><br>   * `Stopped`: Stopped.<br><br>   * `Starting`: Starting.<br><br>   * `Suspending`: Suspending.<br><br>   * `Suspended`: Suspended.<br><br>* When the parameter Name is set to `DBEngineVersion`, the value of parameter Value can be:<br><br>   * `PostgreSQL_17`: PostgreSQL engine.<br><br>   * `Supabase_1_24`: Supabase engine.<br><br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default">Multiple values are supported, separated by commas (,).</div><br> |


<span id="tagoption"></span>
### TagOption


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |Tag_key |Key of the workspace tag. The rules for defining tag keys are as follows:<br><br><br>* In UTF\-8 encoded Unicode format.<br><br>* Cannot start with `volc:` or `sys` in any case. `volc:` and `sys` are system\-reserved tag keys and are forbidden to use.<br><br>* Can only contain language characters, digits, spaces, and English symbols `_`, `.`, `:`, `/`, `=`, `+`, `-`, and `@`.<br><br>* The length must be between 1 and 128 characters.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Tag keys are case\-sensitive<strong>.</strong></div><br><br><br>* <div data-tips="true" data-tips-type="default">The number of tags created at one time cannot exceed 20.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Tag keys within a single workspace cannot be duplicated.</div><br><br><br>* <div data-tips="true" data-tips-type="default">A tag key can only have one tag value within a single workspace.</div><br> |
|Value |String |No |Tag_value |The value of the workspace tag. The rules for the tag value are as follows:<br><br><br>* In UTF\-8 encoded Unicode format.<br><br>* It can only contain language characters, numbers, spaces, and English symbols (`_`, `.`, `:`, `/`, `=`, `+`, `-`, and `@`).<br><br>* Allow empty, length limit between 0 and 256 characters.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The tag value is case\-sensitive.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|HasMore |Boolean |true |Returned in cursor pagination, indicating whether there is more data on the next page. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|NextToken |String |eyJzb3J0X2J5IjoidXBkYXRlX3RpbWUiLCJzb3J0X2Rlc2MiOnRydWUsImxhc3Rfc29ydCI6MTc4NzIxOTY1NjAwMDAwMDAwMCwibGFzdF9pZCI6OTQ0Mj\*\*\*\*== |Returned when using cursor pagination to query the next page of data. |
|Total |Integer |29 |Total number of results matching the query criteria. |
|Workspaces |Array of [Workspace](https://docs.byteplus.com/en/docs/330/84448#workspace) |Refer to the sample response. |List of workspaces matching the query criteria. |


<span id="workspace"></span>
### Workspace


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|AccountId |String |210036\*\*\*\* |ID of the tenant to which the workspace belongs. |
|AgentPlanSeatId |String |seat\-20260615134321\-kjvvx |Seat ID of the Agent Plan.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is returned only for the enterprise edition using the Agent Plan.</div><br> |
|BaasComputeSettings |Object of [DefaultComputeSettings](https://docs.byteplus.com/en/docs/330/84448#defaultcomputesettings) |Refer to the sample response. |Configuration information for Supabase service compute.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default">This field is returned only for workspaces using the Supabase engine.</div><br> |
|ComputeSettings |Object of [DefaultComputeSettings](https://docs.byteplus.com/en/docs/330/84448#defaultcomputesettings) |Refer to the sample response. |Compute configuration information of the workspace |
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
|WorkspaceSetting |Object of [DefaultWorkspaceSettings](https://docs.byteplus.com/en/docs/330/84448#defaultworkspacesettings) |Refer to the sample response. |Configuration information of the workspace. |
|WorkspaceStatus |String |Running |Running status of the workspace. Values:<br><br><br>* `Unknown`: Unknown status.<br><br>* `Creating`: Creating.<br><br>* `CreateFailed`: Failed to create.<br><br>* `Updating`: Modifying.<br><br>* `Running`: Running.<br><br>* `Deleted`: Deleted.<br><br>* `Error`: Abnormal.<br><br>* `NetworkChanging`: Network changing.<br><br>* `Closing`: Billing shutting down.<br><br>* `Closed`: Shutdown.<br><br>* `Resuming`: Restoring from billing shutdown.<br><br>* `Stopping`: Stopping.<br><br>* `Stopped`: Stopped.<br><br>* `Starting`: Starting.<br><br>* `Suspending`: Suspending.<br><br>* `Suspended`: Suspended. |
|WorkspaceUsage |Object of [WorkspaceUsage](https://docs.byteplus.com/en/docs/330/84448#workspaceusage) |Refer to the sample response. |Workspace usage details: used storage space, used compute, etc. |
|WorkspaceTags |Array of [Tag](https://docs.byteplus.com/en/docs/330/84448#tag) |Refer to the sample response. |Tags for the workspace.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default">If no tags are bound to the workspace, it returns<code>null</code>。</div><br> |


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
POST /?Action=DescribeWorkspaces&Version=2025-10-01 HTTP/1.1
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "Search": "测试",
    "Filters": [
        {
            "Name": "WorkspaceStatus",
            "Value": "CreateFailed,Error"
        },
        {
            "Name": "DBEngineVersion",
            "Value": "PostgreSQL_17"
        }
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20251202140319A7D36E3017BE59792A9C-2311a7",
        "Action": "DescribeWorkspaces",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "Total": 1,
        "Workspaces": [
            {
                "AccountId": "2100365180",
                "ComputeSettings": {
                    "AutoScalingLimitMaxCU": 2,
                    "AutoScalingLimitMinCU": 0.25,
                    "EnableAnalytics":"Enabled",
                    "SuspendTimeoutSeconds": -1
                },
                "CreateTime": "2025-12-02T06:02:54Z",
                "CreationSource": "Console",
               "DNSVisibility": false,
                "DeletionProtectionStatus": "DeletionProtectionEnable",
                "EngineType": "PostgreSQL",
                "EngineVersion": "PostgreSQL_17",
                "InternetProtocol": "IPv4",
                "ProjectName": "default",
                "RegionId": "cn-beijing",
                "StatusChangedTime": "2025-12-02T06:02:54Z",
                "StorageSize": -1,
                "StorageType": "StoragePool",
                "SubnetId": "subnet-1jopkal6uri0w1n7amqfa****",
                "UpdateTime": "2025-12-02T06:02:54Z",
                "VpcId": "vpc-1jop7f4t8bxfk1n7amp60****",
                "WorkspaceId": "alive-palm-e2bb****",
                "WorkspaceName": "测试",
                "WorkspaceSetting": {
                    "DeletionProtection": "Enabled",
                    "HistoryRetentionHours": 0,
                    "PublicConnection": "Enabled"
                },
                "WorkspaceStatus": "CreateFailed",
                "WorkspaceTags": [],
                "WorkspaceUsage": {
                    "BranchComputeTimeSeconds": 0,
                    "BranchCreatedNum": 1,
                    "ComputeTimeSeconds": 0,
                    "DataSizeTotalBytes": -1,
                    "DataSizeUsedBytes": 0,
                    "ServiceTimeSeconds": 0,
                    "StatTime": "2025-12-02T06:03:19Z",
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
