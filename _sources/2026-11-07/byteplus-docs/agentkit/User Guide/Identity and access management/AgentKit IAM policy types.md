---
title: "AgentKit IAM policy types"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/AgentKit_IAM_policy_types"
---

This topic describes the types of AgentKit\-related IAM policies.

<span id="DOHiqzR3"></span>
## System default policies

<span id="veVARxUO"></span>
### AgentKit system default policies

The IAM platform provides default AgentKit\-related policies in advance, with details in the following table.

You can directly assign these system default policies to IAM entities (IAM users, user groups, or roles). **System default policies are for authorization only and can not be edited or modified**.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">AgentKitTosAccess and AgentKitToolAccess are internal policies dedicated to the AgentKit platform and do not need to be granted to IAM users.</div>



|System default policy name |Description |
|---|---|
|AgentKitFullAccess |Once granted this policy, IAM identities (IAM users, user groups, and roles) gain management permissions for AgentKit within the permission scope (global permission or project\-level permission). For example, IAM identities can create, change, delete, and view resources. |
|AgentKitReadOnlyAccess |Once granted this policy, IAM identities (IAM users, user groups, and roles) gain read\-only permissions for AgentKit within the permission scope (global permission or project\-level permission). An IAM identity granted with this policy can only view AgentKit\-related resources, but cannot manage them or view other unauthorized cloud products. |
|AgentKitDeveloperAcess |IAM entities (IAM users, user groups, or roles) assigned with this policy obtain full development permissions for AgentKit within the authorized scope (global or project permissions).<br><br>This permission level is higher than read\-only access but lower than full access:<br><br><br>* Compared with read\-only access: it supports creation, configuration, update, testing, and publishing of resources.<br><br>* Compared with full access: it only provides development and operational capabilities, and does not include high\-risk platform\-level management operations. |


<span id="5YWqXkDO"></span>
### AgentKit system default policy details

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For other system default policies, go to the <a href="https://console.byteplus.com/iam/policymanage?scope=System">Permission policy console</a>.</div>


<span id="HTDXnbGw"></span>
#### AgentKitFullAccess policy details

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Once this policy is assigned, management permissions for all AgentKit resources within the authorized scope, as well as read\-only permissions for IAM and related services are provided.</div>


```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "agentkit:*",
        "apmplus_server:Get*",
        "apmplus_server:List*",
        "Volc_Observe:Get*",
        "Volc_Observe:*Describe*",
        "Volc_Observe:*List*",
        "cloudmonitor:Get*",
        "cloudmonitor:*Describe*",
        "cloudmonitor:*List*",
        "tls:Get*",
        "tls:Describe*",
        "tls:List*",
        "apig:ConvertMcpConfig",
        "apmplus_server:CreateOrder",
        "ark:CreateApiKey",
        "ark:GetEndpoint",
        "ark:GetRawApiKey",
        "ark:InnerDescribeModelEndpoints",
        "ark:ListApiKeys",
        "ark:ListEndpoints",
        "ark:ListFoundationModelVersions",
        "ark:ListModelChargeItems",
        "ark:OpenModelChargeItem",
        "ark:ListFoundationModels",
        "content_customization:GetQuickOpenSearchInfo",
        "cp:CreatePipeline",
        "cp:CreateWorkspace",
        "cp:DeletePipeline",
        "cp:GetDefaultWorkspaceInner",
        "cp:GetInstance",
        "cp:GetTaskRunLog",
        "cp:GetTaskRunLogDownloadURI",
        "cp:ListPipelineRuns",
        "cp:ListPipelineRunStagesInner",
        "cp:ListPipelines",
        "cp:ListWorkspaces",
        "cp:RunPipeline",
        "cr:AddVpcEndpointLinkedVpc",
        "cr:CreateEndpointAclPolicies",
        "cr:CreateNamespace",
        "cr:CreateRegistry",
        "cr:CreateRepository",
        "cr:DeleteEndpointAclPolicies",
        "cr:DeleteNamespace",
        "cr:DeleteRegistry",
        "cr:DeleteTags",
        "cr:GetAuthorizationToken",
        "cr:GetPublicEndpoint",
        "cr:GetVpcEndpoint",
        "cr:ListDomains",
        "cr:ListNamespaces",
        "cr:ListRegistries",
        "cr:ListRepositories",
        "cr:ListTags",
        "cr:RemoveVpcEndpointLinkedVpc",
        "cr:StartRegistry",
        "cr:UpdateNamespace",
        "cr:UpdatePublicEndpoint",
        "cr:UpdateVpcEndpoint",
        "ESCloud:GetMLApiKey",
        "ESCloud:GetScene",
        "ESCloud:GetSceneInstance",
        "ESCloud:ListMLApiKeys",
        "iam:AttachRolePolicy",
        "iam:CheckServiceLinkedRole",
        "iam:CreateRole",
        "iam:CreateServiceLinkedRole",
        "iam:DeleteRole",
        "iam:DetachRolePolicy",
        "iam:GetPolicy",
        "iam:GetRole",
        "iam:GetServiceLinkedRoleTemplate",
        "iam:GetUser",
        "iam:ListProjects",
        "iam:ListRoles",
        "iam:ListUsers",
        "iam:UpdateRole",
        "iam:ListAttachedRolePolicies",
        "id:CreateApiKey",
        "id:CreateApiKeyCredentialProvider",
        "id:CreateInboundAuthConfig",
        "id:DeleteApiKey",
        "id:DeleteInboundAuthConfig",
        "id:GetCallerIdentity",
        "id:GetInboundAuthConfig",
        "id:GetResourceApiKey",
        "id:GetTenantServiceStatus",
        "id:GetUserPool",
        "id:GetUserPoolClient",
        "id:ListCredentialProviders",
        "id:ListNamespaces",
        "id:ListServices",
        "id:ListUserPoolClients",
        "id:ListUserPools",
        "id:UpdateInboundAuthConfig",
        "location:DescribeRegions",
        "mem0:CreateMemoryProject",
        "mem0:DeleteMemoryProject",
        "mem0:DescribeAPIKeyDetail",
        "mem0:DescribeMemoryProjectDetail",
        "mem0:DescribeMemoryProjects",
        "mem0:ModifyMemoryProjectLongTermStrategy",
        "mem0:SearchMemory",
        "mem0:SearchMemoryAllInfo",
        "ml_platform:GetKnowledgeBaseServiceInfo",
        "ml_platform:ListCollections",
        "sts:AssumeRole",
        "tls:ActiveTlsAccount",
        "tls:SearchLogs",
        "tos:CopyObject",
        "tos:CreateBucket",
        "tos:DeleteBucket",
        "tos:DeleteObject",
        "tos:GetAccountStatus",
        "tos:GetBucketInfo",
        "tos:HeadBucket",
        "tos:HeadObject",
        "tos:ListBuckets",
        "tos:ListObjectsV2",
        "tos:PostObject",
        "tos:PutObject",
        "vefaas:CreateFunction",
        "vefaas:CreateSandbox",
        "vefaas:DeleteFunction",
        "vefaas:DescribeSandbox",
        "vefaas:EnableUserCrVpcTunnel",
        "vefaas:GetAvailabilityZones",
        "vefaas:GetFunction",
        "vefaas:GetImageConfig",
        "vefaas:GetImageSyncStatus",
        "vefaas:GetReleaseStatus",
        "vefaas:KillSandbox",
        "vefaas:ListFunctions",
        "vefaas:ListRuntimes",
        "vefaas:ListSandboxes",
        "vefaas:QueryUserCrVpcTunnel",
        "vefaas:Release",
        "vefaas:SetSandboxTimeout",
        "vefaas:UpdateFunction",
        "vikingdb:GetKnowledgeBaseServiceInfo",
        "vikingdb:GetMemorydbInstanceDetail",
        "vikingdb:ListCollections",
        "vikingdb:MemoryCollectionInfo",
        "vikingdb:MemoryCollectionList",
        "vikingdb:MemorySearch",
        "vikingdb:MemorySearchUser",
        "vikingdb:GetCollectionInfo",
        "vikingdb:CreateCollection",
        "vikingdb:CreateKnowledgedbInstance",
        "vikingdb:GetKnowledgedbInstanceStatus",
        "vikingdb:AddDocument",
        "vikingdb:UpdateCollection",
        "vikingdb:DeleteCollection",
        "vikingdb:CreateMemorydbInstance",
        "vpc:DescribeSecurityGroups",
        "vpc:DescribeSubnets",
        "vpc:DescribeVpcAttributes",
        "vpc:DescribeVpcs",
        "vke:ListClusters",
        "vke:ForwardKubernetesApi",
        "vke:ListServices",
        "ecs:DescribeInstances"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```


<span id="UPWWUKxR"></span>
#### AgentKitReadOnlyAccess policy details

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Once this policy is assigned, all AgentKit resources within the authorized scope can be viewed.</div>


```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "agentkit:Get*",
        "agentkit:List*",
        "agentkit:*List*",
        "agentkit:*Get*",
        "apmplus_server:Get*",
        "apmplus_server:List*",
        "Volc_Observe:Get*",
        "Volc_Observe:*Describe*",
        "Volc_Observe:*List*",
        "cloudmonitor:Get*",
        "cloudmonitor:*Describe*",
        "cloudmonitor:*List*",
        "tls:Get*",
        "tls:Describe*",
        "tls:List*",
        "tls:SearchLogs",
        "apig:ConvertMcpConfig",
        "ark:GetEndpoint",
        "ark:GetRawApiKey",
        "ark:InnerDescribeModelEndpoints",
        "ark:ListApiKeys",
        "ark:ListEndpoints",
        "ark:ListFoundationModels",
        "ark:ListFoundationModelVersions",
        "ark:ListModelChargeItems",
        "content_customization:GetQuickOpenSearchInfo",
        "cp:GetDefaultWorkspaceInner",
        "cp:GetInstance",
        "cp:GetTaskRunLog",
        "cp:GetTaskRunLogDownloadURI",
        "cp:ListPipelineRuns",
        "cp:ListPipelineRunStagesInner",
        "cp:ListPipelines",
        "cp:ListWorkspaces",
        "cr:GetAuthorizationToken",
        "cr:GetPublicEndpoint",
        "cr:GetVpcEndpoint",
        "cr:ListDomains",
        "cr:ListNamespaces",
        "cr:ListRegistries",
        "cr:ListRepositories",
        "cr:ListTags",
        "escloud:ListScene",
        "iam:CheckServiceLinkedRole",
        "iam:GetPolicy",
        "iam:GetRole",
        "iam:GetServiceLinkedRoleTemplate",
        "iam:GetUser",
        "iam:ListProjects",
        "iam:ListRoles",
        "iam:ListUsers",
        "iam:ListAttachedRolePolicies",
        "id:GetCallerIdentity",
        "id:GetResourceApiKey",
        "id:GetTenantServiceStatus",
        "id:GetUserPool",
        "id:GetUserPoolClient",
        "id:ListCredentialProviders",
        "id:ListNamespaces",
        "id:ListServices",
        "id:ListUserPoolClients",
        "id:ListUserPools",
        "location:DescribeRegions",
        "mem0:DescribeMemoryProjects",
        "mem0:SearchMemory",
        "mem0:SearchMemoryAllInfo",
        "ml_platform:GetKnowledgeBaseServiceInfo",
        "ml_platform:ListCollections",
        "tos:GetAccountStatus",
        "tos:GetBucketInfo",
        "tos:HeadBucket",
        "tos:HeadObject",
        "tos:ListBuckets",
        "tos:ListObjectsV2",
        "vefaas:GetAvailabilityZones",
        "vefaas:ListFunctions",
        "vefaas:ListRuntimes",
        "vikingdb:GetKnowledgeBaseServiceInfo",
        "vikingdb:GetMemorydbInstanceDetail",
        "vikingdb:ListCollections",
        "vikingdb:MemoryCollectionInfo",
        "vikingdb:MemoryCollectionList",
        "vikingdb:MemorySearch",
        "vikingdb:MemorySearchUser",
        "vikingdb:GetCollectionInfo",
        "vikingdb:GetKnowledgedbInstanceStatus",
        "vpc:DescribeSecurityGroups",
        "vpc:DescribeSubnets",
        "vpc:DescribeVpcAttributes",
        "vpc:DescribeVpcs",
        "vke:ListClusters",
        "vke:ForwardKubernetesApi",
        "vke:ListServices",
        "ecs:DescribeInstances"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```


<span id="Y3DexF88"></span>
#### AgentKitDeveloperAccess policy details

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Once this policy is assigned, full development permissions for AgentKit within the authorized scope are provided.</div>


```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "agentkit:*",
        "apmplus_server:Get*",
        "apmplus_server:List*",
        "Volc_Observe:Get*",
        "Volc_Observe:*Describe*",
        "Volc_Observe:*List*",
        "cloudmonitor:Get*",
        "cloudmonitor:*Describe*",
        "cloudmonitor:*List*",
        "tls:Get*",
        "tls:Describe*",
        "tls:List*",
        "apig:ConvertMcpConfig",
        "ark:GetEndpoint",
        "ark:GetRawApiKey",
        "ark:InnerDescribeModelEndpoints",
        "ark:ListApiKeys",
        "ark:ListEndpoints",
        "ark:ListFoundationModelVersions",
        "ark:ListModelChargeItems",
        "ark:ListFoundationModels",
        "content_customization:GetQuickOpenSearchInfo",
        "cp:CreatePipeline",
        "cp:CreateWorkspace",
        "cp:GetDefaultWorkspaceInner",
        "cp:GetInstance",
        "cp:GetTaskRunLog",
        "cp:GetTaskRunLogDownloadURI",
        "cp:ListPipelineRuns",
        "cp:ListPipelineRunStagesInner",
        "cp:ListPipelines",
        "cp:ListWorkspaces",
        "cp:RunPipeline",
        "cr:CreateEndpointAclPolicies",
        "cr:CreateNamespace",
        "cr:CreateRegistry",
        "cr:CreateRepository",
        "cr:GetAuthorizationToken",
        "cr:GetPublicEndpoint",
        "cr:GetVpcEndpoint",
        "cr:ListDomains",
        "cr:ListNamespaces",
        "cr:ListRegistries",
        "cr:ListRepositories",
        "cr:ListTags",
        "cr:UpdatePublicEndpoint",
        "ESCloud:GetMLApiKey",
        "ESCloud:GetScene",
        "ESCloud:GetSceneInstance",
        "ESCloud:ListMLApiKeys",
        "iam:CheckServiceLinkedRole",
        "iam:GetPolicy",
        "iam:GetRole",
        "iam:GetServiceLinkedRoleTemplate",
        "iam:GetUser",
        "iam:ListProjects",
        "iam:ListRoles",
        "iam:ListUsers",
        "iam:ListAttachedRolePolicies",
        "id:GetCallerIdentity",
        "id:GetInboundAuthConfig",
        "id:GetResourceApiKey",
        "id:GetTenantServiceStatus",
        "id:GetUserPool",
        "id:GetUserPoolClient",
        "id:ListCredentialProviders",
        "id:ListNamespaces",
        "id:ListServices",
        "id:ListUserPoolClients",
        "id:ListUserPools",
        "location:DescribeRegions",
        "mem0:CreateMemoryProject",
        "mem0:DeleteMemoryProject",
        "mem0:DescribeAPIKeyDetail",
        "mem0:DescribeMemoryProjectDetail",
        "mem0:DescribeMemoryProjects",
        "mem0:ModifyMemoryProjectLongTermStrategy",
        "mem0:SearchMemory",
        "mem0:SearchMemoryAllInfo",
        "ml_platform:GetKnowledgeBaseServiceInfo",
        "ml_platform:ListCollections",
        "tls:SearchLogs",
        "tos:CreateBucket",
        "tos:GetAccountStatus",
        "tos:GetBucketInfo",
        "tos:HeadBucket",
        "tos:HeadObject",
        "tos:ListBuckets",
        "tos:ListObjectsV2",
        "tos:PostObject",
        "tos:PutObject",
        "vikingdb:GetKnowledgeBaseServiceInfo",
        "vikingdb:GetMemorydbInstanceDetail",
        "vikingdb:ListCollections",
        "vikingdb:MemoryCollectionInfo",
        "vikingdb:MemoryCollectionList",
        "vikingdb:MemorySearch",
        "vikingdb:MemorySearchUser",
        "vikingdb:GetCollectionInfo",
        "vikingdb:CreateCollection",
        "vikingdb:CreateKnowledgedbInstance",
        "vikingdb:GetKnowledgedbInstanceStatus",
        "vikingdb:AddDocument",
        "vikingdb:UpdateCollection",
        "vikingdb:DeleteCollection",
        "vikingdb:CreateMemorydbInstance",
        "vpc:DescribeSecurityGroups",
        "vpc:DescribeSubnets",
        "vpc:DescribeVpcAttributes",
        "vpc:DescribeVpcs",
        "vke:ListClusters",
        "vke:ForwardKubernetesApi",
        "vke:ListServices",
        "ecs:DescribeInstances",
        "llmshield:ListInstances",
        "llmshield:ListApps",
        "llmshield:CreateOuterApp",
        "ark:ListSubscribeTrade",
        "ark:EstimateSubscribePrice",
        "ark:GetCodingPlanUsage",
        "rds_mysql:DescribeDBInstances",
        "rds_mysql:DescribeDBInstanceEndpoints",
        "rds_mysql:DescribeDBAccounts",
        "rds_mysql:DescribeDatabases",
        "rds_postgresql:DescribeDBInstances",
        "rds_postgresql:DescribeDBAccounts",
        "rds_postgresql:DescribeDatabases",
        "aidap:DescribeWorkspaces",
        "aidap:DescribeBranches",
        "aidap:DescribeComputes",
        "aidap:DescribeDBAccounts",
        "aidap:DescribeDatabases"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```
