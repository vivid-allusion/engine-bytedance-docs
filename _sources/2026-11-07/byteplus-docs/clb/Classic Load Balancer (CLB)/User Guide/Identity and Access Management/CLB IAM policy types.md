---
title: "CLB IAM policy types"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/CLB-IAM-Policy-Type"
---

This topic introduces the types of IAM policies and the policies related to Classic Load Balancer (CLB) to help you quickly understand IAM policies. IAM policies support two types: System default policies and custom policies. You can directly use system default policies to authorize IAM identities. If the system default policy cannot meet your needs, you can use a custom policy for precise authorization to flexibly manage account resources.

## System default policy

The IAM console has pre\-configured default policies for CLB. You can directly authorize system default policies to IAM identities (IAM users, user groups, or roles). **System default policies can only be used for authorization and cannot be edited or modified**.

### CLB system default policies

|**System default policy name** |**Description** |**Policy type** |
|---|---|---|
|[CLBFullAccess](https://console.byteplus.com/iam/policymanage/System/CLBFullAccess?tab=content) |The IAM identities (IAM users, user groups, roles) authorized with this policy obtain full management permissions for all CLB resources within the permitted scope, including all create, view, modify, and delete operations. |Strategy |
|[CLBReadOnlyAccess](https://console.byteplus.com/iam/policymanage/System/CLBReadOnlyAccess?tab=content) |An IAM identity (IAM user, user group, or role) granted this policy obtains read\-only access to all CLB resources within the permission scope. If an IAM identity is only granted this permission, it can only view CLB resources, cannot perform any actions on CLB resources, nor view other unauthorized products. |Strategy |
|[ServiceRolePolicyForClbLogDelivery](https://console.byteplus.com/iam/policymanage/System/ServiceRolePolicyForClbLogDelivery?tab=content) |This is a service\-associated role authorized for CLB log delivery. CLB uses this role to access your resources in other cloud products for log delivery. |Strategy |

Details are as follows:

**CLBFullAccess**

After being granted this policy, you can manage all CLB resources within the permission scope and view Virtual Private Cloud (VPC), subnet, and Elastic Compute Service (ECS) permissions.

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "clb:*",
        "clblogdelivery:*",
        "vpc:DescribeEip*",
        "vpc:DisassociateEipAddress",
        "vpc:AssociateEipAddress",
        "vpc:ModifyEipAddressAttributes",
        "vpc:ReleaseEipAddress",
        "vpc:AllocateEipAddress",
        "vpc:DescribeVpc*",
        "vpc:DescribeSubnet*",
        "vpc:DescribeNetworkInterfaces",
        "ecs:DescribeInstances",
        "Volc_Observe:List*",
        "Volc_Observe:Get*",
        "cloudmonitor:List*",
        "cloudmonitor:Get*"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```

**CLBReadOnlyAccess**

After being authorized with this policy, you can view all CLB resources within the permission scope, as well as view Virtual Private Cloud (VPC), subnet, and Elastic Compute Service instance

**ServiceRolePolicyForClbLogDelivery**

This policy only supports authorizing service\-associated roles for CLB log delivery. After authorization, CLB can create and query resources related to Torch Log Service (TLS) and Torch Object Storage (TOS) through this role.

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "tos:HeadBucket",
        "tos:PutObject",
        "tos:GetObject",
        "tos:DeleteObject",
        "tls:PutLogs",
        "tls:CreateProject",
        "tls:DeleteProject",
        "tls:DescribeProject",
        "tls:DescribeProjects",
        "tls:CreateTopic",
        "tls:DeleteTopic",
        "tls:DescribeTopics",
        "tls:GetTopic",
        "tls:DescribeTopic",
        "tls:DescribeIndex",
        "tls:CreateIndex",
        "tls:ModifyIndex",
        "tls:ModifyProject"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```

### Roles or policies required for CLB features

|**Feature** |**Required cloud service** |**Required role/policy** |
|---|---|---|
|Creating a CLB instance |VPC |After granting CLBFullAccess permission to an IAM user:<br><br><br>* If there are VPC instances in the IAM user's root user, no additional permissions are needed to create CLB instances.<br><br>* If there are no VPC instances in the IAM user's root user account, either use the root user account to create VPC instances or add permissions for the IAM user. The following two solutions are available for granting permissions to IAM users:<br><br>   * Solution 1: Add VPCFullAccess permission for the IAM user.<br><br>   * Solution 2: Add a custom policy for the IAM user that grants permissions to create VPC instances and subnets. The policy content is as follows:<br><br><br>```Plain Text```<br>```{```<br>```    "Statement":[```<br>```        {```<br>```            "Effect":"Allow",```<br>```            "Action":[```<br>```                "vpc:CreateVpc",```<br>```                "vpc:CreateSubnet"```<br>```            ],```<br>```            "Resource":[```<br>```                "*"```<br>```            ]```<br>```        }```<br>```    ]```<br>```}```<br> |
|Add backend servers to the Server Group |Elastic Compute Service |After granting ECSFullAccess permission to an IAM user:<br><br><br>* If the root user associated with the IAM user already has ECS instances, no additional permissions are required to add backend servers to the Server Group.<br><br>* If the root user associated with the IAM user does not have ECS instances, please create ECS instances using the root user or add permissions for the IAM user. The following two solutions are available for granting permissions to IAM users:<br><br>   * Solution 1: Add ECSFullAccess permission for the IAM user.<br><br>   * Solution 2: Add a custom policy granting ECS instance creation permission for the IAM user. The policy content is as follows:<br><br><br>```Plain Text```<br>```{```<br>```    "Statement":[```<br>```        {```<br>```            "Effect":"Allow",```<br>```            "Action":[```<br>```                "ecs:RunInstances"```<br>```            ],```<br>```            "Resource":[```<br>```                "*"```<br>```            ]```<br>```        }```<br>```    ]```<br>```}```<br><br><br> |

|**Topic** |**Explanation** |**Related documents** |
|---|---|---|
|Custom policy types |Custom policies are categorized based on the entity to which the policy can be bound: Identity\-based policies and Resource\-based policies. |* [Identity-based policy](https://docs.byteplus.com/en/docs/6257/65059)<br><br>* [Resource-based policy](https://docs.byteplus.com/en/docs/6257/65059) |
|Custom policy syntax |Custom policy syntax defines policy permissions through policy elements. When creating an identity\-based policy and a resource\-based policy, the policy elements differ. |* [General custom policy syntax examples](https://docs.byteplus.com/en/docs/6257/1253728)<br><br>* [CLB custom policy syntax examples](https://docs.byteplus.com/en/docs/clb/Example-of-custom-policy) |
|Create custom policy |When you use a BytePlus main account or an IAM user with IAM permissions to authorize, and the system default policy cannot meet your requirements, you can granularly define permissions through a custom policy. |[Create custom policy](https://docs.byteplus.com/en/docs/6257/1158323) |
