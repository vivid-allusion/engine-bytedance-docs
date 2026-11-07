---
title: "IAM authorization best practices"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/IAM-based-authorization-best-practices"
---

VKE supports two user authorization methods: Identity and Access Management (IAM) and role\-based access control (RBAC). This topic describes the best practices of authorizing IAM users.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">IAM user custom policies do not automatically update with product API changes. When the service adds, modifies, or deprecates APIs or Actions, you need to evaluate and update custom policies manually. Otherwise, the following issues may occur:</div>



* <div data-tips="true" data-tips-type="warning">Feature unavailability (new Actions are not added to the policy, resulting in authorization failure)</div>


* <div data-tips="true" data-tips-type="warning">Permission redundancy (deprecated Actions are not removed promptly, resulting in unnecessary permissions)</div>



<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An IAM users has been created.  For detailed steps, see [User management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-user-management).

<span id=".5Zy65pmv5LiA77ya5Li6LWlhbS3nlKjmiLfmjojmnYPmjIflrprnmoTpm4bnvqQ="></span>
## Scenario 1: Grant permissions on a specified cluster to an IAM user

<span id=".5Zy65pmv5LuL57uN"></span>
### Scenario introduction

Grant access and operation permissions on a specified cluster to an IAM user. In this way, the user can create, delete, query, and modify resources only within the specified VKE cluster.

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the [IAM console](https://console.byteplus.com/iam) by using the BytePlus root user or an IAM user with related permissions.

2. In the left navigation bar, select **Permission policy**, and search for **VKEReadOnlyAccess**.

3. Click **VKEReadOnlyAccess** to go to the policy details page. Click the **Syntax** tab, and copy the **VKEReadOnlyAccess** policy syntax.

4. Modify the copied **VKEReadOnlyAccess** policy syntax based on the following description, and save it as a new custom policy, such as **Access\-Cluster\-A**.

   1. Replace the content in the VKE\-related **Action** with `vke:*`, and replace the content in **Resource** with the required constraints.

      ```json
      {
          "Effect": "Allow",
          "Action": [
              "vke:*"
          ],
          "Resource": [
              "trn:vke:{Region_ID}:{Account_ID}:cluster/{Cluster_ID}",
              "trn:iam:{Account_ID}:project/*",
              "trn:vpc:{Region_ID}:{Account_ID}:securitygroup/*",
              "trn:vpc:{Region_ID}:{Account_ID}:subnet/*"
          ]
      }
      ```
      

      The variable descriptions are as follows:

      * `{Region_ID}`: Replace the value with the ID of the region where the target VKE cluster is located, such as `cn-shanghai`.

      * `{Account_ID}`: Replace the value with the ID of your BytePlus root user, such as `210001****`.

      * `{Cluster_ID}`: Replace the value with the ID of the target VKE cluster, such as `ccm0i61o93a9te2k8****`.

      The complete example is as follows:

      ```json
      {
          "Effect": "Allow",
          "Action": [
              "vke:*"
          ],
          "Resource": [
              "trn:vke:cn-shanghai:210001****:cluster/ccm0i61o93a9te2k8****",
              "trn:iam::210001****:project/*",
              "trn:vpc:cn-shanghai:210001****:securitygroup/*",
              "trn:vpc:cn-shanghai:210001****:subnet/*"
          ]
      }
      ```
      

   2. Add the following EBS\-related **Action** and **Resource**.

      ```json
      {
          "Effect": "Allow",
          "Action": [
              "storage_ebs:Describe*",
              "storage_ebs:CalculatePrice"
          ],
          "Resource": [
              "*"
          ]
      }
      ```
      

5. Create a custom policy **Access\-Cluster\-A**. For detailed operations, see [Creating policies](https://docs.byteplus.com/en/docs/IAM/creating-a-user-custom-policy).

6. Attach the **Access\-Cluster\-A** policy to the IAM user. For detailed operations, see [Managing users](https://docs.byteplus.com/en/docs/IAM/about-users).


<span id=".5Zy65pmv5LqM77ya5Yib5bu66aG555uu6IyD5Zu05L2_55So55qE6Ieq5a6a5LmJ5p2D6ZmQ5bm25o6I5p2D"></span>
## Scenario 2: Create and grant custom permissions on specific projects

<span id=".5Zy65pmv5LuL57uN"></span>
### Scenario introduction

In VKE, some operations and resources are categorized by project. This achieves permission management at the project granularity. To grant permissions on such operations and resources to IAM users, permissions must be granted in the form of project permissions.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Some operations and resources in VKE cannot be categorized by project. Therefore, when you grant permissions on projects to IAM users, you also need to grant permissions on operations and resources that cannot be categorized by project as global permissions to the IAM users. Otherwise, the IAM users may not be able to manage and use VKE resources.</div>


For descriptions of operations and resources related to the VKE services, see [User-defined policy](https://docs.byteplus.com/en/docs/vke/Authorization-overview#.55So5oi36Ieq5a6a5LmJ562W55Wl).

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the [IAM console](https://console.byteplus.com/iam) by using the BytePlus root user or an IAM user with related permissions. 

2. Create a custom policy, such as **vke\-project**. The sample JSON content of the policy is shown as follows. Add or remove specific actions or resources based on your business requirements. For access permissions on cloud service resources required by VKE, see [Introduction to the VKE service-linked role](https://docs.byteplus.com/en/docs/vke/Service-linked-roles-for-Vital-Kubernetes-Engine).

   ```json
   {
     "Statement": [
       {
         "Effect": "Allow",
         "Action": [
           "vke:CreateCluster",
           "vke:ListClusters",
           "vke:UpdateClusterConfig",
           "vke:DeleteCluster",
           "vke:CreateKubeconfig",
           "vke:DeleteKubeconfigs",
           "vke:CreateNodePool",
           "vke:CreateDefaultNodePool",
           "vke:UpdateNodePoolConfig",
           "vke:DeleteNodePool",
           "vke:CreateNodes",
           "vke:DeleteNodes",
           "vke:CreateAddon",
           "vke:UpdateAddonConfig",
           "vke:UpdateAddonVersion",
           "vke:DeleteAddon",
           "vke:ForwardKubernetesApi",
           "vke:ForwardKubernetesReadApi",
           "vke:ForwardKubernetesWriteApi",
           "vke:CreateScalingPolicy",
           "vke:UpdateScalingPolicy",
           "vke:DeleteScalingPolicies",
           "vke:ListKubeconfigs",
           "vke:ListNodePools",
           "vke:ListNodes",
           "vke:ListAddons",
           "vke:SetGlobalDefaultDeleteOption",
           "vke:ListScalingPolicies",
           "vke:ListScalingEvents",
           "vke:UpdateClusterVersion",
           "vke:UpdateImageCache",
           "alb:DescribeLoadBalancers",
           "clb:DescribeLoadBalancers",
           "FileNAS:DescribeFileSystems",
           "storage_ebs:DescribeVolumes",
           "FileNAS:DescribeMountPoints",
           "tls:DescribeTopics",
           "tls:DescribeProject",
           "tls:DescribeTopic",
           "TLS:DescribeTopic",
           "vpc:DescribeSubnets",
           "vpc:DescribeSecurityGroups",
           "vpc:DescribeVpcs",
           "vpc:DescribeBandwidthPackages",
           "vpc:DescribeSecurityGroupAttributes",
           "clb:DescribeListeners",
           "alb:DescribeListeners",
           "natgateway:DescribeNatGateways",
           "ecs:DescribeImages",
           "ecs:DescribeKeyPairs",
           "ecs:DescribeInstances",
           "alb:DescribeCertificates",
           "clb:DescribeCertificates",
           "vepfs:DescribeFileSystems",
           "vepfs:DescribeMountServices",
           "auto_scaling:DescribeScalingGroups",
           "auto_scaling:DescribeScalingActivities",
           "certificate_service:CertificateGetInstance",
           "artifacts:ListRepositories",
           "artifacts:ListInstances",
           "artifacts:GetPackageInfo",
           "apig:ListGateways",
           "cr:ListNamespaces"
         ],
         "Resource": [
           "*"
         ]
       }
     ]
   }
   ```
   

3. Add authorization for the created **vke\-project** policy.

4. Select the target IAM user and add project permissions for the **vke\-project** policy.  For detailed operations, see [Managing users](https://docs.byteplus.com/en/docs/byteplus-platform/docs-editing-a-user).

5. Create a custom policy for operations and resources that are not project\-specific, and attach the policy to the target IAM user.

   1. For example, name the policy **vke\-global**. The sample JSON content of the policy is shown as follows. Add or remove specific actions or resources based on your business requirements. For access permissions on cloud service resources required by VKE, see [Introduction to the VKE service-linked role](https://docs.byteplus.com/en/docs/vke/Service-linked-roles-for-Vital-Kubernetes-Engine).

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If you have created a custom policy for non\-project\-specific operations and resources, you can directly attach it to the target IAM user without creating another one.      </div>
      

      ```json
      {
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "vke:AddClusterNode",
              "vke:AddVciSubnets",
              "vke:CheckClusterCidrConflict",
              "vke:CheckNameConflict",
              "vke:CreateAddonInner",
              "vke:CreateConfigMap",
              "vke:CreateCronHorizontalPodAutoscaler",
              "vke:CreateCronJob",
              "vke:CreateDaemonSet",
              "vke:CreateDefaultNodePoolInner",
              "vke:CreateDeployment",
              "vke:CreateHorizontalPodAutoscaler",
              "vke:CreateIHPA",
              "vke:CreateIngress",
              "vke:CreateJob",
              "vke:CreateLogCollectRule",
              "vke:CreateLogConfig",
              "vke:CreateNamespace",
              "vke:CreateNodePoolInner",
              "vke:CreateNodesInner",
              "vke:CreatePersistentVolume",
              "vke:CreatePersistentVolumeClaim",
              "vke:CreateRelease",
              "vke:CreateResourceByYaml",
              "vke:CreateResourcePackages",
              "vke:CreateSecret",
              "vke:CreateService",
              "vke:CreateStatefulSet",
              "vke:CreateStorageClass",
              "vke:CreateUserRbac",
              "vke:CreateVirtualNode",
              "vke:DeleteCRD",
              "vke:DeleteConfigMap",
              "vke:DeleteCronHorizontalPodAutoscaler",
              "vke:DeleteCronJob",
              "vke:DeleteDaemonSet",
              "vke:DeleteDeployment",
              "vke:DeleteHorizontalPodAutoscaler",
              "vke:DeleteIHPA",
              "vke:DeleteImageCache",
              "vke:DeleteIngress",
              "vke:DeleteJob",
              "vke:DeleteLogCollectRule",
              "vke:DeleteLogConfig",
              "vke:DeleteNamespace",
              "vke:DeletePersistentVolume",
              "vke:DeletePersistentVolumeClaim",
              "vke:DeletePod",
              "vke:DeleteRelease",
              "vke:DeleteResource",
              "vke:DeleteSecret",
              "vke:DeleteService",
              "vke:DeleteStatefulSet",
              "vke:DeleteStorageClass",
              "vke:DeleteUserRbac",
              "vke:GetAPIGroup",
              "vke:GetAccountQuotaUsages",
              "vke:GetApplicationCronInspection",
              "vke:GetApplicationInspection",
              "vke:GetApplicationInspectionItem",
              "vke:GetApplicationInspectionStatus",
              "vke:GetChart",
              "vke:GetCheckItem",
              "vke:GetClusterDeployProgress",
              "vke:GetClusterOverview",
              "vke:GetClusterResources",
              "vke:GetConfigMap",
              "vke:GetContainerLogs",
              "vke:GetCronJob",
              "vke:GetCronScan",
              "vke:GetDaemonSet",
              "vke:GetDeployment",
              "vke:GetEventTopic",
              "vke:GetHorizontalPodAutoscaler",
              "vke:GetIHPA",
              "vke:GetIngress",
              "vke:GetJob",
              "vke:GetListeners",
              "vke:GetLogCollectRule",
              "vke:GetLogProjectID",
              "vke:GetLogTopicID",
              "vke:GetNamespace",
              "vke:GetNamespaceResource",
              "vke:GetNodePoolNodeStatistics",
              "vke:GetPersistentVolume",
              "vke:GetPersistentVolumeClaim",
              "vke:GetPod",
              "vke:GetRelease",
              "vke:GetResource",
              "vke:GetResourceYaml",
              "vke:GetSecret",
              "vke:GetSecretDomains",
              "vke:GetService",
              "vke:GetStatefulSet",
              "vke:GetStorageClass",
              "vke:GetTerminal",
              "vke:InnerReconcileVCIQuotaUsage",
              "vke:InnerSyncVCIQuota",
              "vke:IsAffectedByVci",
              "vke:ListAPIGroups",
              "vke:ListAddonFeatureSchemas",
              "vke:ListAddonNotRefactoredVersions",
              "vke:ListAiSuiteStatus",
              "vke:ListAllAddons",
              "vke:ListAllSupportedAddons",
              "vke:ListApplicationInspectionItems",
              "vke:ListApplicationInspectionReports",
              "vke:ListBatchSuiteStatus",
              "vke:ListBenchmarks",
              "vke:ListCRDs",
              "vke:ListChartCategories",
              "vke:ListCharts",
              "vke:ListCheckItems",
              "vke:ListClusterNode",
              "vke:ListConfigMaps",
              "vke:ListContainerInstances",
              "vke:ListCronHorizontalPodAutoscalers",
              "vke:ListCronJobs",
              "vke:ListCustomRoles",
              "vke:ListDaemonSets",
              "vke:ListDeployments",
              "vke:ListEvent",
              "vke:ListHorizontalPodAutoscalers",
              "vke:ListIHPAs",
              "vke:ListImageCaches",
              "vke:ListIngress",
              "vke:ListInstanceTypes",
              "vke:ListJobs",
              "vke:ListJobsFromCronJob",
              "vke:ListKubernetesObservability",
              "vke:ListKubernetesObservabilityComponentConfigs",
              "vke:ListLogCollectRules",
              "vke:ListLogConfigs",
              "vke:ListLogProjects",
              "vke:ListLogTopics",
              "vke:ListNamespace",
              "vke:ListNodePoolNodes",
              "vke:ListNodePoolScalingRecords",
              "vke:ListNodeReports",
              "vke:ListNodeZones",
              "vke:ListNodesInner",
              "vke:ListObjectEvents",
              "vke:ListOperationEvents",
              "vke:ListPersistentVolume",
              "vke:ListPersistentVolumeClaim",
              "vke:ListPods",
              "vke:ListReleases",
              "vke:ListReservedContainerInstanceGroups",
              "vke:ListResourcePackageSpecs",
              "vke:ListResources",
              "vke:ListSecrets",
              "vke:ListServices",
              "vke:ListStatefulSets",
              "vke:ListStorageClass",
              "vke:ListTagsForResources",
              "vke:ListTasks",
              "vke:ListUpdateRecords",
              "vke:ListUserRbacs",
              "vke:ListVirtualNodes",
              "vke:ListWorkloadHistories",
              "vke:ListWorkloadHorizontalPodAutoscalers",
              "vke:ListWorkloadPods",
              "vke:ListWorkloadServices",
              "vke:PatchCronJobSuspend",
              "vke:PatchWorkloadImage",
              "vke:PatchWorkloadParallelism",
              "vke:PatchWorkloadReplicas",
              "vke:RestartWorkload",
              "vke:RollbackRelease",
              "vke:RollbackWorkload",
              "vke:SetApplicationCronInspection",
              "vke:SetApplicationInspection",
              "vke:StartApplicationInspection",
              "vke:StartNodeScan",
              "vke:StartScan",
              "vke:TagResources",
              "vke:UntagResources",
              "vke:UpdateAiSuiteStatus",
              "vke:UpdateConfigMap",
              "vke:UpdateCronHorizontalPodAutoscaler",
              "vke:UpdateCronJob",
              "vke:UpdateCronScan",
              "vke:UpdateDaemonSet",
              "vke:UpdateDeployment",
              "vke:UpdateHorizontalPodAutoscaler",
              "vke:UpdateIHPA",
              "vke:UpdateIngress",
              "vke:UpdateJob",
              "vke:UpdateLogCollectRule",
              "vke:UpdateNamespace",
              "vke:UpdateNamespaceResource",
              "vke:UpdateNodePoolForCA",
              "vke:UpdateNodesSystemConfigInner",
              "vke:UpdateNodesVersion",
              "vke:UpdateRelease",
              "vke:UpdateResourceByYaml",
              "vke:UpdateSecret",
              "vke:UpdateService",
              "vke:UpdateStatefulSet",
              "vke:UpdateUserRbac",
              "vmp:CreateAlertingRuleGroup",
              "vmp:DeleteAlertingRuleGroup",
              "vmp:ListAlertingRuleGroups",
              "vmp:ListAlertingRuleTemplates",
              "vmp:ListAlertingRules",
              "vmp:ListDashboards",
              "vmp:ListDatasources",
              "vmp:ListNotifyGroupPolicies",
              "vmp:ListNotifyPolicies",
              "vmp:ListWorkspaceInstanceTypes",
              "vmp:ListWorkspaces",
              "vmp:UpdateAlertingRuleGroup",
              "vpc:DescribeIpv6AddressBandwidths",
              "vpc:InnerGetLimitFromKeys",
              "vpc:ListTagsForResources",
              "alb:DescribeRules",
              "apig:CheckGatewayExist",
              "cfs:ListFs",
              "cfs:ListNs",
              "clb:DescribeCertificates",
              "clb:DescribeLoadBalancerAttributes",
              "clb:ListTagsForResources",
              "cr:GetVpcEndpoint",
              "cr:ListRegistries",
              "cr:ListRepositories",
              "ecs:DescribeDeploymentSetSupportedInstanceTypeFamily",
              "ecs:DescribeDeploymentSets",
              "ecs:DescribeTags",
              "iam:AttachRolePolicy",
              "iam:CreateRole",
              "iam:ListAttachedRolePolicies",
              "iam:ListPolicies",
              "iam:ListRoles",
              "tls:DescribeProjects",
              "tos:ListBuckets",
              "vepfs:DescribeFileSystemStatistics",
              "vepfs:DescribeMountServices"
            ],
            "Resource": [
              "*"
            ]
          }
        ]
      }
      ```
      

   2. Add authorization for the created **vke\-global** policy.

   3. Select the target IAM user and add global permissions for the **vke\-global** policy.  For detailed operations, see [Managing users](https://docs.byteplus.com/en/docs/byteplus-platform/docs-editing-a-user).
