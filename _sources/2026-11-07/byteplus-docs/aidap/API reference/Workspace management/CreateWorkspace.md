---
title: "CreateWorkspace"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/CreateWorkspace"
---

Call the CreateWorkspace API to create a workspace.

## Request type

Asynchronous request.

## Precautions

Each BytePlus main account can create up to 1,000 workspaces using the PostgreSQL engine or Supabase engine respectively.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateWorkspace&serviceCode=aidap&version=2025-10-01&groupName=)

## Request parameters

|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|ProjectName |String |No |default |Affiliate project name. |
|EngineVersion |String |Yes |PostgreSQL_17 |Engine version. Values:<br><br><br>* `PostgreSQL_17`: PostgreSQL 17.<br><br>* <br><br>* `Supabase_1_24`: Supabase 1.24. |
|EngineType |String |No |PostgreSQL |Engine type. Values:<br><br><br>* `PostgreSQL`: PostgreSQL engine.<br><br>* <br><br>* `Supabase`: Supabase engine. |
|WorkspaceName |String |No |TestWorkspace |Workspace name. The workspace name must meet the following rules:<br><br><br>* Can only contain Chinese characters, letters (a\-z and A\-Z), digits, hyphens (\-), and underscores (_).<br><br>* Must start with a Chinese character or letter (a\-z and A\-Z).<br><br>* Must be 2 to 128 characters in length.<br><br><br>> **tip**<br><br><br>> If not specified, the automatically generated workspace ID is used as the workspace name.<br> |
|WorkspaceSettings |Object of [DefaultWorkspaceSettings](https://docs.byteplus.com/en/docs/330/84447#defaultworkspacesettings) |No |Refer to the sample request. |Basic configuration of the workspace. |
|NetworkSettings |Object of [DefaultNetworkSettings](https://docs.byteplus.com/en/docs/330/84447#defaultnetworksettings) |No |Refer to the sample request. |Network configuration of the workspace.<br><br>> Tip<br><br><br>> When EngineVersion is<br><br><br>> `Supabase_1_24`, this parameter is required.<br> |
|BranchSettings |Object of [DefaultBranchSettings](https://docs.byteplus.com/en/docs/330/84447#defaultbranchsettings) |No |Refer to the sample request. |Branch configuration of the workspace. |
|ComputeSettings |Object of [DefaultComputeSettings](https://docs.byteplus.com/en/docs/330/84447#defaultcomputesettings) |No |Refer to the sample request. |Initial compute configuration of the workspace. |
|WorkspaceTags |Array of [TagOption](https://docs.byteplus.com/en/docs/330/84447#tagoption) |No |Refer to the sample request. |Tags for the workspace.<br><br>> **tip**<br><br><br><br>* > Up to 20 tag key\-value pairs can be passed simultaneously.<br><br><br>* > Up to 50 tags can be associated with a workspace.<br> |
|AgentPlanSettings |Object of [AgentPlanSettings](https://docs.byteplus.com/en/docs/330/84447#agentplansettings) |No |Refer to the sample request. |Agent plan configuration. |

### DefaultWorkspaceSettings

|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|DeletionProtection |String |No |Enabled |The status of the workspace deletion protection function. Values:<br><br><br>* `Enabled`: the function is enabled. Default value.<br><br>* `Disabled`: the function is disabled. |
|HistoryRetentionHours |Integer |No |48 |Traceability duration of the workspace. Value range is 1 to 720, default value is 48, unit is hour. |
|PublicConnection |String |No |Disabled |Status of workspace shared public network function. Values:<br><br><br>* `Enabled`: the function is enabled.<br><br>* `Disabled`: the function is disabled. Default value. |

### DefaultNetworkSettings

|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|EipId |String |No |eip\-mjl2a0ongirk5smt1byg\*\*\*\* |ID of the public network IP used by the workspace.<br><br>> Tip<br><br><br>> Only workspaces using the Supabase engine support specifying the public network IP during creation with this parameter.<br> |
|VpcId |String |Yes |vpc\-3ezxu117lv18g72200rro\*\*\*\* |ID of the Virtual Private Cloud used by the workspace.<br><br>> Tip<br><br><br><br>* > This parameter is optional when creating a workspace using the Supabase engine.<br><br><br>* > This parameter is not supported when creating a workspace using the PostgreSQL engine.<br> |
|SubnetId |String |Yes |subnet\-3rf442t6a54w016nf3pg9\*\*\*\* |The ID of the subnet used by the workspace.<br><br> |
|InternetProtocol |String |No |IPv4 |IP address protocol version used by the workspace.<br><br><br>* `DualStack`: IPv4 + IPv6.<br><br>* `IPv4`: IPv4. Default value. |
|SharedPrivateNetwork |Boolean |No |false |Whether to shared its private network. When enabled, use shared ENI; otherwise, each node is allocated an ENI. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. Default value.<br><br><br>> Tip<br><br><br>> Workspace using the veDB MySQL engine does not support this parameter.<br> |
|SharedPublicNetwork |Boolean |No |true |Enable shared public network for workspace? Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. Default value.<br><br><br>> Tip<br><br><br>> This field is valid only for workspaces using the Supabase engine.<br> |

### DefaultBranchSettings

|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|BranchName |String |No |main |Branch name, named `main` by default. The name must meet the following rules:<br><br><br>* The length must be between 1 and 128 characters.<br><br>* It can only contain letters (a~z and A~Z), numbers (0~9), hyphens (\-), and underscores (_).<br><br>* It must start with a letter (a~z and A~Z) and end with a letter (a~z and A~Z) or a number (0~9). |
|AccountName |String |No |user_admin |The account name is named `user_admin` by default. The name must meet the following rules:<br><br><br>* Unique within the branch.<br><br>* Must start with a letter and end with a letter or number.<br><br>* Can only contain letters, numbers, underscores (_), and hyphens (\-).<br><br>* Must be 2 to 63 characters in length.<br><br>* Cannot use certain reservation words. For details about reserved words, refer to [List of reserved keywords](https://docs.byteplus.com/en/docs/aidap/Reservation_word_list). |
|DatabaseName |String |No |testDB |The name defaults to `aidb`. The database name must follow these rules:<br><br><br>* Unique within the branch.<br><br>* Must start with a letter and end with a letter or number.<br><br>* Can only contain letters, numbers, underscores (_), and hyphens (\-).<br><br>* Must be 2 to 63 characters in length.<br><br>* Cannot use certain reservation words. For details about reserved words, refer to [List of reserved keywords](https://docs.byteplus.com/en/docs/aidap/Reservation_word_list). |

### DefaultComputeSettings

|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|AutoScalingLimitMaxCU |Double |No |4 |The upper limit of the workspace automatic compute expansion range. Valid values include [0.25\|0.5\|1\|2\|3\|4\|5\|6\|7\|8\|9\|10\|11\|12\|13\|14\|15\|16\|18\|20\|22\|24\|26\|28\|30\|32]. The default value is 2. The unit is CU.<br><br>> Tip<br><br><br><br>* > The valid ranges of AutoScalingLimitMaxCU and AutoScalingLimitMinCU are the same, but the value of AutoScalingLimitMaxCU must be greater than that of AutoScalingLimitMinCU.<br><br><br>* > The ratio of AutoScalingLimitMaxCU to AutoScalingLimitMinCU cannot exceed 8.<br> |
|AutoScalingLimitMinCU |Double |No |0.25 |The lower limit of the workspace automatic compute expansion range. Valid values are [0.25\|0.5\|1\|2\|3\|4\|5\|6\|7\|8\|9\|10\|11\|12\|13\|14\|15\|16\|18\|20\|22\|24\|26\|28\|30\|32]. The default value is 0.25. The unit is CU.<br><br>> Tip<br><br><br><br>* > The valid ranges of AutoScalingLimitMaxCU and AutoScalingLimitMinCU are the same, but the value of AutoScalingLimitMaxCU must be greater than that of AutoScalingLimitMinCU.<br><br><br>* > The ratio of AutoScalingLimitMaxCU to AutoScalingLimitMinCU cannot exceed 8.<br> |
|SuspendTimeoutSeconds |Integer |No |300 |Idle duration before suspend. The node is automatically suspended after the compute has no activity for the set time. A value of `-1` indicates that the node will never be suspended. |
|EnableAnalytic |String |No |Enabled |Workspace AP acceleration status. Values:<br><br><br>* `Enabled`: enabled.<br><br>* `Disabled`: disabled.<br><br><br>> **tip**<br><br><br><br>* > This field is valid only for workspaces using the PostgreSQL engine.<br><br><br>* > When used as a request parameter, the default value is `Disabled`.<br> |

### TagOption

|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |Tag_key |Key of the workspace tag. The rules for defining tag keys are as follows:<br><br><br>* In UTF\-8 encoded Unicode format.<br><br>* Cannot start with `volc:` or `sys` in any case. `volc:` and `sys` are system\-reserved tag keys and are forbidden to use.<br><br>* Can only contain language characters, digits, spaces, and English symbols `_`, `.`, `:`, `/`, `=`, `+`, `-`, and `@`.<br><br>* The length must be between 1 and 128 characters.<br><br><br>> **tip**<br><br><br><br>* > Tag keys are case\-sensitive**.**<br><br><br>* > The number of tags created at one time cannot exceed 20.<br><br><br>* > Tag keys within a single workspace cannot be duplicated.<br><br><br>* > A tag key can only have one tag value within a single workspace.<br> |
|Value |String |No |Tag_value |The value of the workspace tag. The rules for the tag value are as follows:<br><br><br>* In UTF\-8 encoded Unicode format.<br><br>* It can only contain language characters, numbers, spaces, and English symbols (`_`, `.`, `:`, `/`, `=`, `+`, `-`, and `@`).<br><br>* Allow empty, length limit between 0 and 256 characters.<br><br><br>> **tip**<br><br><br>> The tag value is case\-sensitive.<br> |

### AgentPlanSettings

|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|IsAgentPlan |Boolean |No |true |Whether the workspace is used for Agent Plan. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. Default value. |
|AgentPlanSeatId |String |No |seat\-20260615134321\-kjvvx |Seat ID of the Agent Plan.<br><br>> **tip**<br><br><br><br>* > If using the enterprise version of the Agent Plan, this parameter must be provided.<br><br><br>* > If using the personal version of the Agent Plan, this parameter is not required.<br> |

## Response parameters

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|WorkspaceId |String |ideal\-fir\-9fc8\*\*\*\* |ID of the workspace. |
|Workspace |Object of [Workspace](https://docs.byteplus.com/en/docs/330/84447#workspace) |Refer to the sample response. |Detailed information about the workspace. |

### Workspace

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|AccountId |String |210036\*\*\*\* |ID of the tenant to which the workspace belongs. |
|AgentPlanSeatId |String |seat\-20260615134321\-kjvvx |Seat ID of the Agent Plan.<br><br>> **tip**<br><br><br>> This parameter is returned only for the enterprise edition using the Agent Plan.<br> |
|BaasComputeSettings |Object of [DefaultComputeSettings](https://docs.byteplus.com/en/docs/330/84447#defaultcomputesettings) |Refer to the return example. |Configuration information for Supabase service compute.<br><br>> Tip<br><br><br>> This field is returned only for workspaces using the Supabase engine.<br> |
|ComputeSettings |Object of [DefaultComputeSettings](https://docs.byteplus.com/en/docs/330/84447#defaultcomputesettings) |Refer to the sample response. |Compute configuration information of the workspace |
|CreateTime |String |2025\-10\-20T06:47:49Z |Creation time of the workspace (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|CreationSource |String |Console |Creation source of the workspace. Values:<br><br><br>* `AIPA`: created via AIPA.<br><br>* `CLI`: created via CLI.<br><br>* `Console`: created via Console.<br><br>* `Coze`: created via Coze.<br><br>* `MCP`: created via MCP.<br><br>* `SDK`: created via SDK.<br><br>* `Terraform`: Created via Terraform.<br><br>* `Trae`: Created via Trae.<br><br>* `Unknown`: Unknown creation source. |
|DNSVisibility |Boolean |false |Whether the public network resolves private network domain names is enabled. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|DelayedDeleteExpiredAt |String |2026\-10\-09T08:03:17Z |Latency deletion end time (UTC). Format: `yyyy-MM-ddTHH:mm:ssZ`.<br><br>> **tip**<br><br><br>> Returned only when the value of `WorkspaceStatus` is `DelayedDelete`.<br> |
|DelayedDeleteStartedAt |String |2026\-09\-09T08:03:17Z |Latency deletion start time (UTC). Format: `yyyy-MM-ddTHH:mm:ssZ`.<br><br>> **tip**<br><br><br>> Returned only when the value of `WorkspaceStatus` is `DelayedDelete`.<br> |
|DeletionProtectionStatus |String |Enable |The status of the workspace deletion protection function. Values:<br><br><br>* `AllowDeletion`: deletion protection is disabled. The workspace can be deleted directly.<br><br>* `DeletionProtectionEnable`: deletion protection is enabled. The workspace cannot be deleted directly. |
|EngineType |String |PostgreSQL |Engine type. Values:<br><br><br>* `PostgreSQL`: PostgreSQL engine.<br><br>* <br><br>* `Supabase`: Supabase engine. |
|EngineVersion |String |PostgreSQL_17 |Engine version. Values:<br><br><br>* `PostgreSQL_17`: PostgreSQL 17.<br><br>* <br><br>* `Supabase_1_24`: Supabase 1.24. |
|InternetProtocol |String |IPv4 |IP address protocol version used by the workspace.<br><br><br>* `DualStack`: IPv4 + IPv6.<br><br>* `IPv4`: IPv4. |
|IsAgentPlan |Boolean |true |Whether the workspace is used for Agent Plan. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. Default value. |
|ProjectName |String |default |Name of the project to which the workspace belongs. |
|RegionId |String |cn\-beijing |The ID of the region where the workspace resides. |
|SharedPrivateNetwork |Boolean |true |Whether shared mode is enabled for the Virtual Private Cloud of the workspace. After enabling, the workspace supports wildcard domain access, and does not add new resolution records for each compute node. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no.<br><br><br>> Tip<br><br><br>> This field is not returned when not enabled.<br> |
|StatusChangedTime |String |2025\-10\-20T06:48:15Z |Workspace status change time (UTC). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|SubnetId |String |subnet\-3rf442t6a54w016nf3pg9\*\*\*\* |The ID of the subnet used by the workspace. |
|UpdateTime |String |2025\-10\-21T05:32:19Z |The update time of the workspace (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|VpcId |String |vpc\-3ezxu117lv18g72200rro\*\*\*\* |ID of the private network used by the workspace.<br><br>> Description<br><br><br>> Returns empty if the workspace does not use a virtual private cloud.<br> |
|WorkspaceId |String |ideal\-fir\-9fc8\*\*\*\* |ID of the workspace. |
|WorkspaceName |String |TestWorkspace |Name of the workspace. |
|WorkspaceSetting |Object of [DefaultWorkspaceSettings](https://docs.byteplus.com/en/docs/330/84447#defaultworkspacesettings) |Refer to the sample response. |Configuration information of the workspace. |
|WorkspaceStatus |String |Running |Running status of the workspace. Values:<br><br><br>* `Unknown`: Unknown status.<br><br>* `Creating`: Creating.<br><br>* `CreateFailed`: Failed to create.<br><br>* `Updating`: Modifying.<br><br>* `Running`: Running.<br><br>* `Deleted`: Deleted.<br><br>* `Error`: Abnormal.<br><br>* `NetworkChanging`: Network changing.<br><br>* `Closing`: Billing shutting down.<br><br>* `Closed`: Shutdown.<br><br>* `Resuming`: Restoring from billing shutdown.<br><br>* `Stopping`: Stopping.<br><br>* `Stopped`: Stopped.<br><br>* `Starting`: Starting.<br><br>* `Suspending`: Suspending.<br><br>* `Suspended`: Suspended.<br><br>* `DelayedDelete`: Latency deleting. |
|WorkspaceUsage |Object of [WorkspaceUsage](https://docs.byteplus.com/en/docs/330/84447#workspaceusage) |Refer to the sample response. |Workspace usage details: used storage space, used compute, etc. |
|WorkspaceTags |Array of [Tag](https://docs.byteplus.com/en/docs/330/84447#tag) |Refer to the sample response. |Tags for the workspace.<br><br>> Tip<br><br><br>> If no tags are bound to the workspace, it returns`null`。<br> |

### DefaultComputeSettings

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|AutoScalingLimitMaxCU |Double |4 |The upper limit of the workspace automatic compute expansion range. Valid values include [0.25\|0.5\|1\|2\|3\|4\|5\|6\|7\|8\|9\|10\|11\|12\|13\|14\|15\|16\|18\|20\|22\|24\|26\|28\|30\|32]. The default value is 2. The unit is CU.<br><br>> Tip<br><br><br><br>* > The valid ranges of AutoScalingLimitMaxCU and AutoScalingLimitMinCU are the same, but the value of AutoScalingLimitMaxCU must be greater than that of AutoScalingLimitMinCU.<br><br><br>* > The ratio of AutoScalingLimitMaxCU to AutoScalingLimitMinCU cannot exceed 8.<br> |
|AutoScalingLimitMinCU |Double |0.25 |The lower limit of the workspace automatic compute expansion range. Valid values are [0.25\|0.5\|1\|2\|3\|4\|5\|6\|7\|8\|9\|10\|11\|12\|13\|14\|15\|16\|18\|20\|22\|24\|26\|28\|30\|32]. The default value is 0.25. The unit is CU.<br><br>> Tip<br><br><br><br>* > The valid ranges of AutoScalingLimitMaxCU and AutoScalingLimitMinCU are the same, but the value of AutoScalingLimitMaxCU must be greater than that of AutoScalingLimitMinCU.<br><br><br>* > The ratio of AutoScalingLimitMaxCU to AutoScalingLimitMinCU cannot exceed 8.<br> |
|SuspendTimeoutSeconds |Integer |300 |Idle duration before suspend. The node is automatically suspended after the compute has no activity for the set time. A value of `-1` indicates that the node will never be suspended. |
|EnableAnalytic |String |Enabled |Workspace AP acceleration status. Values:<br><br><br>* `Enabled`: enabled.<br><br>* `Disabled`: disabled.<br><br><br>> **tip**<br><br><br><br>* > This field is valid only for workspaces using the PostgreSQL engine.<br><br><br>* > When used as a request parameter, the default value is `Disabled`.<br> |

### DefaultWorkspaceSettings

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|DeletionProtection |String |Enabled |The status of the workspace deletion protection function. Values:<br><br><br>* `Enabled`: the function is enabled. Default value.<br><br>* `Disabled`: the function is disabled. |
|HistoryRetentionHours |Integer |48 |Traceability duration of the workspace. Value range is 1 to 720, default value is 48, unit is hour. |
|PublicConnection |String |Enabled |Status of workspace shared public network function. Values:<br><br><br>* `Enabled`: the function is enabled.<br><br>* `Disabled`: the function is disabled. |

### WorkspaceUsage

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|BranchComputeTimeSeconds |Long |4240159 |Compute duration used by the workspace branch. Unit is second. |
|BranchCreatedNum |Long |12 |The number of branches in the workspace.   |
|ComputeTimeSeconds |Long |4560259 |Compute duration used by the workspace. Unit is second. |
|DataSizeTotalBytes |Long |\-1 |Storage size. Unit is byte.<br><br>> **tip**<br><br><br>> Return value `-1` indicates unlimited.<br> |
|DataSizeUsedBytes |Long |90980352 |Used storage space size of the workspace. Unit is byte. |
|FunctionCallNum |Long |45443 |Number of function calls.<br><br>> tip<br><br><br>> This field is returned only for workspaces using the Supabase engine.<br> |
|ServiceTimeSeconds |Long |12 |Service usage duration.<br><br>> tip<br><br><br>> This field is returned only for workspaces using the Supabase engine.<br> |
|StatTime |String |2025\-10\-20T03:46:01Z |Data statistics time (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|StorageSizeUsedBytes |Long |6944 |Size of data used by the storage service.<br><br>> tip<br><br><br>> This field is returned only for workspaces using the Supabase engine.<br> |
|VectorReadVCU |Double |19.22 |Resources consumed when performing retrieval, query, and other read operations on vector data in the vector bucket. Unit is vCU.<br><br>> tip<br><br><br>> This field is returned only for workspaces using the Supabase engine.<br> |
|VectorStorageSizeUsedBytes |Long |909805 |Storage space occupied by vector data stored in vector bucket. Unit is byte.<br><br>> tip<br><br><br>> This field is returned only for workspaces using the Supabase engine.<br> |
|VectorWriteVCU |Double |7.3 |Resources consumed for writing, updating, or deleting vector data in the vector bucket. Unit is vCU.<br><br>> tip<br><br><br>> This field is returned only for workspaces using the Supabase engine.<br> |

### Tag

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Key |String |key1 |Tag key. |
|Value |String |value1 |Value of tag. |
|System |Boolean |false |Whether it is a system tag. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |

## Sample

### Sample request

```JSON
POST /?Action=CreateWorkspace&Version=2025-10-01 HTTP/1.1
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "EngineVersion": "PostgreSQL_17",
"Tags": [
        {
            "Key": "Tag1_key",
            "Value": "Tag1_value"
        },
        {
            "Key": "Tag2_key",
            "Value": "Tag2_value"
        }
    ]
}
```

### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20251202124104819B0AB236CBE672E24E-b44436",
        "Action": "CreateWorkspace",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "Workspace": {
            "AccountId": "210036****",
            "ComputeSettings": {
                "AutoScalingLimitMaxCU": 2,
                "AutoScalingLimitMinCU": 0.25,
                "EnableAnalytics":"Enabled",
                "SuspendTimeoutSeconds": -1
            },
            "CreateTime": "2025-12-02T04:41:05Z",
            "CreationSource": "SDK",
            "DNSVisibility": false,
            "DeletionProtectionStatus": "DeletionProtectionEnable",
            "EngineType": "PostgreSQL",
            "EngineVersion": "PostgreSQL_17",
            "ProjectName": "default",
            "RegionId": "cn-beijing",
            "StatusChangedTime": "2025-12-02T04:41:05Z",
            "StorageSize": -1,
            "StorageType": "StoragePool",
            "UpdateTime": "2025-12-02T04:41:05Z",
            "WorkspaceId": "merry-aloe-b481****",
            "WorkspaceName": "merry-aloe-b481****",
            "WorkspaceSetting": {
                "DeletionProtection": "Enabled",
                "HistoryRetentionHours": 48,
                "PublicConnection": "Enabled"
            },
            "WorkspaceStatus": "Creating",
            "WorkspaceTags": null,
            "WorkspaceUsage": null
        },
        "WorkspaceId": "merry-aloe-b481****"
    }
}
```

## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
