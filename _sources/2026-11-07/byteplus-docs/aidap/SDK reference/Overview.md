---
title: "Overview"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/SDK_Overview"
---

To improve usability and scalability, and support more business scenarios, the AI Native Database Platform offers SDKs in Go and Python. After installing the SDK locally, you can develop based on the Open API provided by the AI Native Database Platform.

## SDK list

The download links for each version of the SDK for the AI Native Database Platform are shown in the following table.

|**Language** |**Version** |**Release time** |**Download address** |**User guide** |
|---|---|---|---|---|
|Python |v3.0.64 |2026\-10\-29 |[AIDAP Python SDK v3.0.64](https://github.com/byteplus-sdk/byteplus-python-sdk-v2/tree/v3.0.64/byteplussdkaidap) |[Using Python SDK](https://docs.byteplus.com/en/docs/aidap/Using_Python_SDK) |
||v3.0.60 |2026\-09\-03 |[AIDAP Python SDK v3.0.60](https://github.com/byteplus-sdk/byteplus-python-sdk-v2/tree/v3.0.60/byteplussdkaidap) ||
||v3.0.58 |2026\-08\-06 |[AIDAP Python SDK v3.0.58](https://github.com/byteplus-sdk/byteplus-python-sdk-v2/tree/v3.0.58/byteplussdkaidap) ||
|Go |v1.0.82 |2026\-10\-29 |[AIDAP Go SDK v1.0.82](https://github.com/byteplus-sdk/byteplus-go-sdk-v2/tree/v1.0.82) |[Using Go SDK](https://docs.byteplus.com/en/docs/aidap/Using_Go_SDK) |
||v1.0.78 |2026\-09\-03 |[AIDAP Go SDK v1.0.78](https://github.com/byteplus-sdk/byteplus-go-sdk-v2/tree/v1.0.78) ||
||v1.0.76 |2026\-08\-06 |[AIDAP Go SDK v1.0.76](https://github.com/byteplus-sdk/byteplus-go-sdk-v2/tree/v1.0.76) ||

## API overview

The Open APIs included in the SDK are listed in the following table.

|Category |API |Decscription |**Associated SDK** |
|---|---|---|---|
|Global management |[ListWorkspaceUsageTop](https://docs.byteplus.com/docs/aidap/ListWorkspaceUsageTop) |Call the ListWorkspaceUsageTop API to query resource usage of all Workspaces under the tenant account in descending order. |Python SDKs and Go SDKs released on or after August 6, 2026. |
|Workspace management<br><br> |[CreateWorkspace](https://docs.byteplus.com/docs/aidap/CreateWorkspace) |Call the CreateWorkspace API to create a workspace. ||
||[DescribeWorkspaces](https://docs.byteplus.com/docs/aidap/DescribeWorkspaces) |Call the DescribeWorkspaces API to query the list of Workspaces. ||
||[DescribeWorkspaceDetail](https://docs.byteplus.com/docs/aidap/DescribeWorkspaceDetail) |Call the DescribeWorkspaceDetail API to query Workspace details. ||
||[DescribeWorkspaceDetailList](https://docs.byteplus.com/docs/aidap/DescribeWorkspaceDetailList) |Call the DescribeWorkspaceDetailList API to query detailed information of multiple workspaces. ||
||[DescribeWorkspaceOverview](https://docs.byteplus.com/docs/aidap/DescribeWorkspaceOverview) |Call the DescribeWorkspaceOverview API to query workspace overview information. ||
||[ModifyComputeSettings](https://docs.byteplus.com/docs/aidap/ModifyComputeSettings) |Call the ModifyComputeSettings API to modify the initial compute settings of the workspace. ||
||[ModifyWorkspaceSettings](https://docs.byteplus.com/docs/aidap/ModifyWorkspaceSettings) |Call the ModifyWorkspaceSettings API to modify the workspace's basic configuration. ||
||[ModifyWorkspaceName](https://docs.byteplus.com/docs/aidap/ModifyWorkspaceName) |Call the ModifyWorkspaceName API to change the workspace name. ||
||[DeleteWorkspace](https://docs.byteplus.com/docs/aidap/DeleteWorkspace) |Call the DeleteWorkspace API to delete the Workspace. ||
||[ModifyWorkspaceDeletionProtectionPolicy](https://docs.byteplus.com/docs/aidap/ModifyWorkspaceDeletionProtectionPolicy) |Call the ModifyWorkspaceDeletionProtectionPolicy API to enable or disable deletion protection for the workspace. ||
||[AddTagsToWorkspaces](https://docs.byteplus.com/docs/aidap/AddTagsToWorkspaces) |Call the AddTagsToWorkspaces API to add tags to the workspace. ||
||[RemoveTagsFromWorkspaces](https://docs.byteplus.com/docs/aidap/RemoveTagsFromWorkspaces) |Call the RemoveTagsFromWorkspaces API to remove tags from the workspace. ||
||[StartWorkspace](https://docs.byteplus.com/docs/aidap/StartWorkspace) |Call the StartWorkspace API to start a stopped instance. ||
||[SuspendWorkspace](https://docs.byteplus.com/docs/aidap/SuspendWorkspace) |Call the SuspendWorkspace API to suspend a running instance. ||
||[StopWorkspace](https://docs.byteplus.com/docs/aidap/StopWorkspace) |Call the StopWorkspace API to pause a running instance. ||
||[DescribeChargeInfo](https://docs.byteplus.com/docs/aidap/DescribeChargeInfo) |Call DescribeChargeInfo API to query the billing information of the workspace. ||
||[CreateWorkspacesExportTask](https://docs.byteplus.com/docs/aidap/CreateWorkspacesExportTask) |Call the CreateWorkspacesExportTask API to create a workspace list export task, exporting workspace data to a jsonl.gz file. You can query the export progress and download link through the DescribeWorkspacesExportTask API. ||
||[DescribeWorkspacesExportTask](https://docs.byteplus.com/docs/aidap/DescribeWorkspacesExportTask) |Call the DescribeWorkspacesExportTask API to query the execution status, progress, and download link of the workspace list export task. Supports querying a specific task or the most recent export task of the current account. ||
||[RecoverDelayedDeleteWorkspace](https://docs.byteplus.com/en/docs/aidap/RecoverDelayedDeleteWorkspace) |Call the RecoverDelayedDeleteWorkspace API to recover the Workspace in **Latency deleting** status. |Python SDKs and Go SDKs released on or after October 29, 2026. |
|Branch management |[CreateBranch](https://docs.byteplus.com/docs/aidap/CreateBranch) |Call the CreateBranch API to create a branch for the workspace. |Python SDKs and Go SDKs released on or after August 6, 2026.<br><br> |
||[DescribeBranches](https://docs.byteplus.com/docs/aidap/DescribeBranches) |Call the DescribeBranches API to query the workspace's branch list. ||
||[DescribeBranchesList](https://docs.byteplus.com/docs/aidap/DescribeBranchesList) |Call the DescribeBranchesList API to query the branches list of multiple workspaces. ||
||[DescribeChildBranches](https://docs.byteplus.com/docs/aidap/DescribeChildBranches) |Call the DescribeChildBranches API to query the child branch list of a branch. ||
||[DescribeBranchDetail](https://docs.byteplus.com/docs/aidap/DescribeBranchDetail) |Call the DescribeBranchDetail API to query detailed information about the branch. ||
||[DescribeDefaultBranch](https://docs.byteplus.com/docs/aidap/DescribeDefaultBranch) |Call the DescribeDefaultBranch API to query the default branch of the workspace.<br><br> ||
||[DescribeDefaultBranchList](https://docs.byteplus.com/docs/aidap/DescribeDefaultBranchList) |Call the DescribeDefaultBranchList API to query the default branch of multiple workspaces. ||
||[UpdateBranch](https://docs.byteplus.com/docs/aidap/UpdateBranch) |Call the UpdateBranch API to modify the branch configuration. ||
||[SetAsDefaultBranch](https://docs.byteplus.com/docs/aidap/SetAsDefaultBranch) |Call the SetAsDefaultBranch API to set the branch as the default branch. ||
||[ResetBranch](https://docs.byteplus.com/docs/aidap/ResetBranch) |Call the ResetBranch API to reset the branch. ||
||[GetRestoreWindow](https://docs.byteplus.com/docs/aidap/GetRestoreWindow) |Call the GetRestoreWindow API to query the recoverable time period of a branch. ||
||[DescribeRestorableBranches](https://docs.byteplus.com/docs/aidap/DescribeRestorableBranches) |Call the DescribeRestorableBranches API to query the workspace's restorable branches at a specific time. ||
||[BranchRestore](https://docs.byteplus.com/docs/aidap/BranchRestore) |Call the BranchRestore API to restore branch data to a specific time. ||
||[DescribeAPIKeys](https://docs.byteplus.com/docs/aidap/DescribeAPIKeys) |Call the DescribeAPIKeys API to query the Workspace API keys. ||
||[RestartBranch](https://docs.byteplus.com/docs/aidap/RestartBranch) |call the RestartBranch API to restart a branch. ||
||[DeleteBranch](https://docs.byteplus.com/docs/aidap/DeleteBranch) |Call the DeleteBranch API to delete a branch. ||
||[DescribeBranchSchemaNames](https://docs.byteplus.com/docs/aidap/DescribeBranchSchemaNames) |Call the EnableBranchAIFunction API to enable the branch AI Functions. ||
||[CreateSchemaDiff](https://docs.byteplus.com/docs/aidap/CreateSchemaDiff) |Call the ModifyBranchAIFunctionSettings API to modify the branch's AI Function configuration. ||
||[DescribeSchemaDiffJobStatus](https://docs.byteplus.com/docs/aidap/DescribeSchemaDiffJobStatus) |Call the DescribeBranchAIFunction API to query the configuration details of the branch AI Function. ||
||[DescribeSchemaDiffResultMeta](https://docs.byteplus.com/docs/aidap/DescribeSchemaDiffResultMeta) |Call the DescribeBranchSchemaNames API to query the list of schemas for the branch. ||
||[DescribeSchemaDiffResultSQLText](https://docs.byteplus.com/docs/aidap/DescribeSchemaDiffResultSQLText) |Call CreateSchemaDiff API to create a branch compare task. ||
||[DescribeSchemaDiffResultSQLTextAll](https://docs.byteplus.com/docs/aidap/DescribeSchemaDiffResultSQLTextAll) |Call DescribeSchemaDiffJobStatus to query the status of the branch comparison task. ||
||[GetSchemaDiffResultDownloadLink](https://docs.byteplus.com/docs/aidap/GetSchemaDiffResultDownloadLink) |Call DescribeSchemaDiffResultMeta API to query detailed information of the Compare branch task. ||
|Compute management |[CreateCompute](https://docs.byteplus.com/docs/aidap/CreateCompute) |Call DescribeSchemaDiffResultSQLText API to query the SQL text of the branch compare result. ||
||[DescribeComputes](https://docs.byteplus.com/docs/aidap/DescribeComputes) |Call the DescribeSchemaDiffResultSQLTextAll API to query the complete migration SQL text for the branch comparison task. ||
||[DescribeComputeDetail](https://docs.byteplus.com/docs/aidap/DescribeComputeDetail) |Call GetSchemaDiffResultDownloadLink API to obtain the download link for the branch compare result. ||
||[ModifyComputeSpec](https://docs.byteplus.com/docs/aidap/ModifyComputeSpec) |Call the CreateCompute API to create a compute. ||
||[ModifyComputeName](https://docs.byteplus.com/docs/aidap/ModifyComputeName) |Call the DescribeComputes API to query the compute list of the branch. ||
||[ModifyComputeParameters](https://docs.byteplus.com/docs/aidap/ModifyComputeParameters) |Call the DescribeComputeDetail API to query compute details. ||
||[DeleteCompute](https://docs.byteplus.com/docs/aidap/DeleteCompute) |Call the ModifyComputeSpec API to modify the specification. ||
||[ModifyComputeAnalyticPolicy](https://docs.byteplus.com/docs/aidap/ModifyComputeAnalyticPolicy) |Call the ModifyComputeName API to modify the compute name. ||
||[CreateDataLakeSecretConnection](https://docs.byteplus.com/docs/aidap/CreateDataLakeSecretConnection) |Call ModifyComputeParameters API to change the running value of the parameters. ||
||[DeleteDataLakeSecretConnection](https://docs.byteplus.com/docs/aidap/DeleteDataLakeSecretConnection) |Call the DeleteDataLakeSecretConnection API to delete a data lake connection. ||
||[DescribeDataLakeSecretConnection](https://docs.byteplus.com/docs/aidap/DescribeDataLakeSecretConnection) |Call the DescribeDataLakeSecretConnection API to query the data lake connection. ||
||[CheckDataLakeSecretConnection](https://docs.byteplus.com/docs/aidap/CheckDataLakeSecretConnection) |Call the CheckDataLakeSecretConnection API to verify the connectivity of the data lake connection. ||
||[ListDatabasesDataLakeSecretConnection](https://docs.byteplus.com/docs/aidap/ListDatabasesDataLakeSecretConnection) |Call the ListDatabasesDataLakeSecretConnection API to query the databases created with data lake connection. ||
|Account management |[CreateDBAccount](https://docs.byteplus.com/docs/aidap/CreateDBAccount) |Call the CreateDBAccount API to create a database account for the branch. ||
||[DescribeDBAccounts](https://docs.byteplus.com/docs/aidap/DescribeDBAccounts) |Call the DescribeDBAccounts API to query the branch's database account list. ||
||[DescribeDBAccountConnection](https://docs.byteplus.com/docs/aidap/DescribeDBAccountConnection) |Call the DescribeDBAccountConnection API to query connection information of the database account. ||
||[ResetDBAccountPassword](https://docs.byteplus.com/docs/aidap/ResetDBAccountPassword) |Call the ResetAccountPassword API to reset the account password. ||
||[DeleteDBAccount](https://docs.byteplus.com/docs/aidap/DeleteDBAccount) |Call the DeleteDBAccount API to delete a database account. ||
||[CreateDatabase](https://docs.byteplus.com/docs/aidap/CreateDatabase) |Call the CreateDatabase API to create a database for a branch. ||
||[DescribeDatabases](https://docs.byteplus.com/docs/aidap/DescribeDatabases) |Call the DescribeDatabases API to query branch databases. ||
||[DropDatabase](https://docs.byteplus.com/docs/aidap/DropDatabase) |Call the DeleteDatabase API to delete a database. ||
|Connection management |[DescribeWorkspaceEndpoint](https://docs.byteplus.com/docs/aidap/DescribeWorkspaceEndpoint) |Call the DescribeWorkspaceEndpoint API to query connection endpoint information of a workspace. ||
||[DescribeWorkspaceEndpointList](https://docs.byteplus.com/docs/aidap/DescribeWorkspaceEndpointList) |Call the DescribeWorkspaceEndpointList API to query connection endpoint information of multiple workspaces. ||
||[ModifyVpcSettings](https://docs.byteplus.com/docs/aidap/ModifyVpcSettings) |Call the ModifyVpcSettings API to modify the workspace's network protocol type, Virtual Private Cloud, and subnet. ||
||[ModifyWorkspacePublicConnectionPolicy](https://docs.byteplus.com/docs/aidap/ModifyWorkspacePublicConnectionPolicy) |Call the ModifyWorkspacePublicConnectionPolicy API to enable or disable the workspace's shared public network. ||
||[CreateEndpointPublicAddress](https://docs.byteplus.com/docs/aidap/CreateEndpointPublicAddress) |Call the CreateEndpointPublicAddress API to enable public network access for the specified endpoint of the workspace. ||
||[DeleteEndpointPublicAddress](https://docs.byteplus.com/docs/aidap/DeleteEndpointPublicAddress) |Call the DeleteEndpointPublicAddress API to disable public network access for the specified workspace endpoint. ||
||[ModifyPrivateNetworkToSharedMode](https://docs.byteplus.com/docs/aidap/ModifyPrivateNetworkToSharedMode) |Call the ModifyPrivateNetworkToSharedMode API to set the workspace’s shared mode. ||
||[ResetWorkspaceAccountPassword](https://docs.byteplus.com/docs/aidap/ResetWorkspaceAccountPassword) |Use the ResetWorkspaceAccountPassword API to reset the account and password for logging in to the Supabase console. ||
||[ApplyPrivateDNSToPublic](https://docs.byteplus.com/docs/aidap/ApplyPrivateDNSToPublic) |Use the ApplyPrivateDNSToPublic API to enable or disable the public network resolution of private network domain names for the workspace. ||
|Access control |[CreateAccessControlList](https://docs.byteplus.com/docs/aidap/CreateAccessControlList) |Call the CreateAccessControlList API to create an IP allowlist for the workspace. ||
||[DescribeAccessControlList](https://docs.byteplus.com/docs/aidap/DescribeAccessControlList) |Call the DescribeAccessControlList API to query the IP allowlist bound to the workspace. ||
||[ModifyAccessControlList](https://docs.byteplus.com/docs/aidap/ModifyAccessControlList) |Call the ModifyAccessControlList API to modify the Workspace\-bound IP allowlist. ||
||[DeleteAccessControlList](https://docs.byteplus.com/docs/aidap/DeleteAccessControlList) |Call the DeleteAccessControlList API to remove the IP allowlist from the workspace. ||
|Managing tasks |[DescribeOperations](https://docs.byteplus.com/docs/aidap/DescribeOperations) |Call the DescribeOperations API to query operation records. ||
|Large model access management |[DescribeBaasAIModels](https://docs.byteplus.com/docs/aidap/DescribeBaasAIModels) |Call the DescribeBaasAIModels API to query the model list supported by the AI models access function. ||
||[DescribeBaasAIGlobalQuota](https://docs.byteplus.com/docs/aidap/DescribeBaasAIGlobalQuota) |Call the DescribeBaasAIGlobalQuota API to query the global quota for the AI models access function. ||
||[ModifyBaasAIGlobalQuota](https://docs.byteplus.com/docs/aidap/ModifyBaasAIGlobalQuota) |Call the ModifyBaasAIGlobalQuota API to modify the global model quota for users with AI models access function. ||
||[DescribeBaasAIUserSummaries](https://docs.byteplus.com/docs/aidap/DescribeBaasAIUserSummaries) |Call the DescribeBaasAIUserSummaries API to query the model usage summary of the AI models access function. ||
||[ModifyBaasAIUserQuotas](https://docs.byteplus.com/docs/aidap/ModifyBaasAIUserQuotas) |Call the ModifyBaasAIUserQuotas API to modify the model quota for users with AI models access function. ||
|SQL concurrency control |[CreateSQLConcurrencyControlRule](https://docs.byteplus.com/docs/aidap/CreateSQLConcurrencyControlRule) |Call the CreateSQLConcurrencyControlRule API to create SQL concurrency control rules. ||
||[ModifySQLConcurrencyControlRule](https://docs.byteplus.com/docs/aidap/ModifySQLConcurrencyControlRule) |Call the ModifySQLConcurrencyControlRule API to modify the SQL concurrency control rule. ||
||[DescribeSQLConcurrencyControlRules](https://docs.byteplus.com/docs/aidap/DescribeSQLConcurrencyControlRules) |Call the DescribeSQLConcurrencyControlRules API to query SQL concurrency control rules. ||
||[SwitchSQLConcurrencyControlRule](https://docs.byteplus.com/docs/aidap/SwitchSQLConcurrencyControlRule) |Call the SwitchSQLConcurrencyControlRule API to enable or disable the SQL concurrency control rule. ||
||[DeleteSQLConcurrencyControlRule](https://docs.byteplus.com/docs/aidap/DeleteSQLConcurrencyControlRule) |Call the DeleteSQLConcurrencyControlRule API to delete SQL concurrency control rules. ||

##
