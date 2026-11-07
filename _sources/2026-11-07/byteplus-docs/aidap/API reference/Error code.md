---
title: "Error code"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/error_code"
---


|Error code |HTTP status code |Chinese description |
|---|---|---|
|ErrorCode.ServiceUnavailable |503 |The service is currently unavailable. |
|ErrorCode.InternalError |500 |The request processing has failed due to some unknown error, exception or failure. |
|ErrorCode.ServiceBusy |500 |The system is busy, please try again later. |
|ErrorCode.MissingParameter |400 |Missing the %s parameter. |
|ErrorCode.InvalidParameter |400 |The specified parameter %s is not valid. |
|ErrorCode.UnsupportedParameter |400 |The current value for the parameter %s is not supported. |
|ErrorCode.InvalidParameterFormat |400 |The request parameter format is incorrect. |
|ErrorCode.WorkspaceNotFound |404 |Workspace %s could not be found. |
|ErrorCode.WorkspaceSettingNotFound |404 |The %s configuration for workspace could not be found. |
|ErrorCode.InvalidWorkspaceName_Duplicate |400 |The specified workspace name already exists. |
|ErrorCode.WorkspaceNumExceedLimit |403 |The current account has reached its maximum number of workspaces. |
|ErrorCode.BranchNotFound |404 |The specified branch could not be found. |
|ErrorCode.OperationDenied_BranchNotReady |400 |The branch is not ready, please try again later. |
|ErrorCode.InvalidBranchName_Duplicate |400 |The specified branch name already exists. |
|ErrorCode.BranchNumExceedLimit |403 |The current workspace has reached its maximum number of branches. |
|ErrorCode.ComputeNumExceedLimit |403 |The compute of the current branch has reached its limit. |
|ErrorCode.PrimaryComputeNotFound |403 |The specified branch does not have primary compute. |
|ErrorCode.ComputeIsSuspended |403 |The specified branch's compute has been suspended. |
|ErrorCode.PrimaryComputeNumExceedLimit |400 |The current branch already has a primary compute. |
|ErrorCode.OperationDenied_BranchProtected |400 |This operation is not supported if the branch is a protected branch or the default branch. |
|ErrorCode.OperationDenied_SchemaOnlyBranch |400 |The branch is SchemaOnly, and this operation is not supported. |
|ErrorCode.OperationDenied_TimeTravelBranch |400 |The branch is TimeTravel branch, and this operation is not supported. |
|ErrorCode.ComputeNotFound |404 |The specified compute could not be found. |
|ErrorCode.InvalidComputeName_Duplicate |400 |The specified compute name already exists. |
|ErrorCode.OperationDenied_WorkspaceStatusNotRunning |400 |The operation is not permitted due to workspace state is not running. |
|ErrorCode.OperationDenied_InvalidWorkspaceStatus |400 |The operation is not supported in the current state of the workspace. |
|ErrorCode.OperationDenied_InvalidComputeStatus |400 |The operation is not supported in the current state of the compute. |
|ErrorCode.OperationDenied_InvalidBranchStatus |400 |The operation is not supported in the current state of the branch. |
|ErrorCode.OperationDenied_ComputeNumTooLess |400 |The compute of a workspace must not be less than %s. |
|ErrorCode.WorkspaceSameSubnetError |400 |The selected subnet is the same as the subnet currently being used by the workspace, so no network change is required. |
|ErrorCode.AccountResourceStatNotFound |400 |Unable to get resource statistics for account %s. |
|ErrorCode.AccountNotFound |400 |Account %s could not be found. |
|ErrorCode.AccountPermissionDenied |400 |Account %s does not have permission to operate on resource %s. |
|ErrorCode.AccountAlreadyExist |400 |The specified account name %s already exists. |
|ErrorCode.CreateWorkflowError |500 |Failed to create workflow %s. |
|ErrorCode.OperationDenied_WorkspaceHasResource |400 |The current workspace is still associated with the %s resource. Operation is denied. |
|ErrorCode.OperationUnsupported |400 |The operation is not supported. |
|ErrorCode.OperationUnsupported_SharedPrivateEniWorkspace |400 |The operation is unsupported for the specified workspace which use shared public network |
|ErrorCode.OperationDenied_HasChildBranch |400 |There are child branches. The operation is prohibited. |
|ErrorCode.OperationDenied_BranchNoParent |400 |The parent branch does not exist. The operation is prohibited. |
|ErrorCode.DatabaseAlreadyExist |400 |The specified database name %s already exists. |
|ErrorCode.DatabaseNotFound |400 |The specified database %s could not be found. |
|ErrorCode.DatabaseUnavailable |400 |Database %s is unavailable. |
|ErrorCode.EipNotAvailable |400 |EIP %s is unavailable. |
|ErrorCode.EipNotFound |404 |EIP %s could not be found. |
|ErrorCode.AnotherEipHasBeenAssociated |400 |The current workspace is already associated with another EIP. |
|ErrorCode.NoEipAssociated |400 |The current workspace is not associated with any EIP. |
|ErrorCode.EndpointNotFound |404 |Endpoint %s could not be found. |
|ErrorCode.PrivateEndpointNotFound |404 |There is no available private network, and public network access cannot be disabled. |
|ErrorCode.CmdCannotExecute |400 |Failed to execute the command %s. |
|ErrorCode.WorkspaceStatusNotMatch |400 |The specified workspace status does not match. |
|ErrorCode.BranchStatusNotMatch |400 |The specified branch status does not match. |
|ErrorCode.ComputeStatusNotMatch |400 |The specified compute status does not match. |
|ErrorCode.CanNotGetBranchInfo |400 |Unable to retrieve branch information. |
|ErrorCode.InvalidRestoreWindow |400 |Restore window is invalid |
|ErrorCode.ComputeCuCheckError |400 |The upper limit of the compute expansion range should not exceed the lower limit by more than 8 times. |
|ErrorCode.InvalidAccountInfo |400 |The request did not contain valid account information. |
|ErrorCode.OperationDenied_DeletionProtection |400 |The deletion protection function of the workspace is enabled， the workspace cannot be deleted. |
|ErrorCode.ResourceSoldOut |403 |The requested resource is sold out. |
|ErrorCode.AccessControlListNameNotFound |404 |The specified allowlist %s could not be found. |
|ErrorCode.TooManyAccessControlList |404 |Too many AccessControlList. max: %v |
|ErrorCode.InvalidAccessControlListName |400 |The specified allowlist name %s is invalid. |
|ErrorCode.InvalidIPList |400 |Invalid IPList: %s. |
|ErrorCode.AccessControlListTooMuchIP |400 |The specified allowlist contains too many IP addresses. The maximum number of IP addresses allowed is %v. |
|ErrorCode.OperationDenied_AccountNoPassword |400 |Account %s has not set a password. The operation is prohibited. |
|ErrorCode.InvalidTagKey |400 |The specified tag key [%s] is invalid. |
|ErrorCode.InvalidTagValue |400 |The specified tag value [%s] is invalid. |
|ErrorCode.TagsLimitExceeded |400 |Too many tags have been added. A maximum of %v tags can be added. |
|ErrorCode.OperationDenied_SystemTag |403 |operation denied. operation denied. system tag key is not allowed. |
|ErrorCode.DuplicateTagKey |400 |The specified tag key [%s] is duplicate. |
