---
title: "AS IAM policy types"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/AS_IAM_policy_types"
---

This topic describes the types of IAM policies and those related to Auto Scaling (AS) to help you quickly understand IAM policies. IAM policies support two types: the system default policy and the custom policy. You can use system default policies to grant IAM identities directly. If the system default policies can not meet your needs, you can use custom policies to grant permissions precisely and manage resources flexibly.

<span id=".57O757uf6aKE6K6-562W55Wl"></span>
## System default policies

The IAM platform provides default AS\-related policies in advance. You can directly assign related system default policies to IAM entities (IAM users, user groups, or roles). **System default policies are for authorization only and can not be edited or modified**.

<span id=".5by55oCn5Ly457yp57O757uf6aKE6K6-562W55Wl"></span>
### System default policies related to AS


|System default policy name |Description |
|---|---|
|AutoScalingFullAccess |Once granted this policy, IAM identities (IAM users, user groups, and roles) gain **management** permissions for Auto Scaling features within the scope of permissions. This applies to scenarios where Auto Scaling features are used via APIs. |
|AutoScalingReadOnlyAccess |Once granted this policy, IAM identities (IAM users, user groups, and roles) gain **read\-only** permissions for Auto Scaling features within the scope of permissions. This applies to scenarios where Auto Scaling features are used via APIs. |
|AutoScalingConsoleFullAccess |Once granted this policy, IAM identities (IAM users, user groups, and roles) gain **management** permissions for Auto Scaling features within the scope of permissions, as well as **read\-only** permissions for related cloud products in the Auto Scaling console. This applies to scenarios where Auto Scaling features are used via the console. |
|AutoScalingConsoleReadOnlyAccess |Once granted this policy, IAM identities (IAM users, user groups, and roles) gain **read\-only** permissions for Auto Scaling features within the scope of permissions, as well as **read\-only** permissions for related cloud products in the Auto Scaling console. This applies to scenarios where Auto Scaling features are used via the console. |


<span id=".5by55oCn5Ly457yp5bi455So5pON5L2c5LiO57O757uf562W55Wl55qE5YWz57O7"></span>
### Relationship between common AS operations and system policies

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">An IAM identity granted only <strong>read\-only</strong> permissions is restricted to viewing configuration details (for example, querying scaling groups or scaling configuration source details) and can not perform any operations.</div>



|Operation |AutoScalingFullAccess |AutoScalingReadOnlyAccess |AutoScalingConsoleFullAccess |AutoScalingConsoleReadOnlyAccess |
|---|---|---|---|---|
|Manage scaling group |√ |× |√ |× |
|Query scaling group |√ |√ |√ |√ |
|Query Load Balancer/launch template |× |× |√ |√ |
|Manage scaling configuration source |√ |× |√ |× |
|Query scaling configuration source |√ |√ |√ |√ |
|Query cloud product (such as VPC) required for scaling configuration |× |× |√ |√ |
|Set instance scale\-in protection |√ |× |√ |× |
|Add/remove/delete instance |√ |× |√ |× |
|Query instance |× |× |√ |√ |
|Manage scaling rule |√ |× |√ |× |
|Query scaling rule |√ |√ |√ |√ |
|Manage lifecycle hook |√ |× |√ |× |
|Query lifecycle hook |√ |√ |√ |√ |
|Manage message notifications |√ |× |√ |× |
|Configure message reception |× |× |× |× |
|Query scaling log |√ |√ |√ |√ |
|Manage vertical scaling |√ |× |√ |× |
|Query vertical scaling |√ |√ |√ |√ |
|Query instance type required for vertical scaling |× |× |√ |√ |


<span id=".5by55oCn5Ly457yp5Yqf6IO95L6d6LWW55qE6KeS6Imy5oiW562W55Wl"></span>
### Roles and policies required for AS features


|Feature |Required cloud service |Required role |Required policy |
|---|---|---|---|
|Associate scaling group with other cloud products |Classic Load Balancer (CLB) |When you use the Auto Scaling service for the first time, the platform guides you to complete the ["Cross-service access authorization"-ServiceRoleForAutoScaling](https://docs.byteplus.com/en/docs/as/Quick-start#.5YmN5o-Q5p2h5Lu2) (For API operations, the platform [performs the authorization automatically](https://docs.byteplus.com/en/docs/as/CreateScalingGroup)). Once authorization succeeds, the Auto Scaling service is authorized to perform cloud product\-related operations, such as adding or removing ECS instances/EIPs, and obtaining Load Balancer information. |After an IAM user is granted management permissions, it can use all Auto Scaling features. To manage other cloud products, you also need to have management permissions for the corresponding cloud products. For example, the CLBFullAccess policy is needed for creating a Classic Load Balancer (CLB). |
||Application Load Balancer (ALB) |||
|Scaling configuration source |ECS |||
||EIP |||
|Receive message notification ||None |After an IAM user is granted management permission, MessageCenterFullAccess is also required to configure message reception methods and recipients. |


<span id=".5by55oCn5Ly457yp5Lqn5ZOB57O757uf6aKE6K6-562W55Wl6K-m5oOF"></span>
### Details of system default policies related to AS

<span id="AutoScalingFullAccess"></span>
#### AutoScalingFullAccess

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "auto_scaling:*"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id="AutoScalingReadOnlyAccess"></span>
#### AutoScalingReadOnlyAccess

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "auto_scaling:Get*",
                "auto_scaling:*Describe*",
                "auto_scaling:*List*"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id="AutoScalingConsoleFullAccess"></span>
#### AutoScalingConsoleFullAccess

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ecs:Get*",
                "ecs:*Describe*",
                "ecs:*List*",
                "clb:Get*",
                "clb:*Describe*",
                "clb:*List*",
                "vpc:Get*",
                "vpc:*Describe*",
                "vpc:*List*",
                "storage_ebs:Get*",
                "storage_ebs:*Describe*",
                "storage_ebs:*List*",
                "rds_mysql:Get*",
                "rds_mysql:*Describe*",
                "rds_mysql:*List*",
                "volc_observe:Get*",
                "volc_observe:*Describe*",
                "volc_observe:*List*",
                "auto_scaling:*"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id="AutoScalingConsoleReadOnlyAccess"></span>
#### AutoScalingConsoleReadOnlyAccess

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ecs:Get*",
                "ecs:*Describe*",
                "ecs:*List*",
                "clb:Get*",
                "clb:*Describe*",
                "clb:*List*",
                "vpc:Get*",
                "vpc:*Describe*",
                "vpc:*List*",
                "storage_ebs:Get*",
                "storage_ebs:*Describe*",
                "storage_ebs:*List*",
                "rds_mysql:Get*",
                "rds_mysql:*Describe*",
                "rds_mysql:*List*",
                "volc_observe:Get*",
                "volc_observe:*Describe*",
                "volc_observe:*List*",
                "auto_scaling:Get*",
                "auto_scaling:*Describe*",
                "auto_scaling:*List*"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id=".5by55oCn5Ly457yp5Lqn5ZOB6Leo5pyN5Yqh5o6I5p2D562W55Wl6K-m5oOF"></span>
### Details of cross\-service authorization policies related to AS

<span id="ServiceRoleForAutoScaling"></span>
#### ServiceRoleForAutoScaling

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ecs:DescribeInstances",
                "ecs:GetInstance",
                "ecs:CreateInstances",
                "ecs:DeleteInstance",
                "ecs:DeleteInstances",
                "ecs:DescribeInstanceTypes",
                "ecs:DescribeKeyPair",
                "ecs:DescribeImages",
                "ecs:DescribeZones",
                "ecs:BindAssumeRole",
                "ecs:ModifyInstanceSpec",
                "ecs:StopInstance",
                "ecs:StartInstance",
                "ecs:DescribeAvailableResource",
                "ecs:DescribeHpcCluster",
                "ecs:CreateTags",
                "ecs:DeleteTags",
                "ecs:DescribeCommands",
                "ecs:InvokeCommand",
                "ecs:DescribeInvocations",
                "ecs:DescribeLaunchTemplateVersions",
                "ecs:CreateScheduledInstances",
                "ecs:DescribeScheduledInstances",
                "ecs:DescribeScheduledInstanceStock",
                "vpc:AllocateEipAddress",
                "vpc:AssociateEipAddress",
                "vpc:DisassociateEipAddress",
                "vpc:ReleaseEipAddress",
                "vpc:DescribeVpcs",
                "vpc:DescribeEipAddresses",
                "vpc:DescribeSubnetAttributes",
                "vpc:InnerGetLimitFromKeys",
                "vpc:DescribeSubnets",
                "vpc:DescribeBandwidthPackages",
                "vpc:RemoveBandwidthPackageIp",
                "clb:DescribeLoadBalancers",
                "clb:DescribeServerGroups",
                "clb:DescribeListenerHealth",
                "clb:DescribeListeners",
                "clb:AddServerGroupBackendServers",
                "clb:RemoveServerGroupBackendServers",
                "clb:DescribeServerGroupAttributes",
                "alb:DescribeLoadBalancers",
                "alb:DescribeServerGroups",
                "alb:AddServerGroupBackendServers",
                "alb:RemoveServerGroupBackendServers",
                "alb:DescribeServerGroupAttributes",
                "alb:DescribeListenerAttributes",
                "alb:DescribeListeners",
                "alb:DescribeListenerHealth",
                "volc_observe:GetMetricData",
                "rds_mysql:ListDBInstances",
                "rds_mysql:DescribeDBInstance",
                "rds_mysql:CreateDBInstanceIPList",
                "rds_mysql:ListDBInstanceIPLists",
                "rds_mysql:ModifyDBInstanceIPList",
                "rds_mysql:DeleteDBInstanceIPList",
                "rds_mysql:DescribeAllowLists",
                "rds_mysql:DescribeAllowListDetail",
                "rds_mysql:DeleteAllowList",
                "rds_mysql:ModifyAllowList",
                "rds_mysql:AssociateAllowList",
                "rds_mysql:DisassociateAllowList",
                "rds_mysql:CreateAllowList",
                "volc_observe:CreateRule",
                "volc_observe:DeleteRulesByIds",
                "volc_observe:UpdateRule",
                "volc_observe:ListRulesByIds",
                "storage_ebs:DescribeVolumes"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id=".6Ieq5a6a5LmJ562W55Wl"></span>
## Custom policies


|Type |Description |
|---|---|
|Custom policy type |Custom policies are divided into identity\-based policies and resource\-based policies, depending on the entity to which they are associated. |
|Custom policy syntax |Custom policy syntax defines policy permissions through policy elements. When creating an identity\-based policy and a resource\-based policy, the policy elements differ. |
|Create a custom policy |When you use a BytePlus root account or an IAM user with IAM management permissions to grant authorizations, and system default policies cannot meet your requirements, you can use custom policies to define fine\-grained permissions. |
