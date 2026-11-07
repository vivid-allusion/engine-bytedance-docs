---
title: "NLB IAM policy types"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-IAM-Policy-Type"
---

This topic introduces the types of IAM policies and the policies related to Network Load Balancer (NLB) to help you quickly understand IAM policies. Identity and Access Management (IAM) policies support two types: System default policy and Custom policy. You can use system default policies to authorize IAM identities directly. If the system default policies cannot meet your needs, you can use custom policies for precise authorization and flexible resource management.

## System default policy

The IAM console has pre\-configured default policies for NLB, which you can directly authorize for IAM identities (IAM users, user groups, or roles). **System default policies can only be used for authorization and cannot be edited or modified**.

### NLB system default policies

|System default policy name |Description |
|---|---|
|[NLBFullAccess](https://console.byteplus.com/iam/policymanage/System/NLBFullAccess?tab=content) |IAM identities (IAM users, user groups, roles) authorized with this policy can manage all NLB resources within the permission scope. |
|[NLBReadOnlyAccess](https://console.byteplus.com/iam/policymanage/System/NLBReadOnlyAccess?tab=content) |After being authorized this policy, IAM identities (IAM users, user groups, roles) can obtain view permissions for all NLB resources within the permission scope. If the IAM identity is granted only this permission, it can only view NLB resources without performing any operations on them or viewing other unauthorized products. |
|[ServiceRoleForNLBLogDelivery](https://console.byteplus.com/iam/policymanage/System/ServiceRoleForNLBLogDelivery?tab=content) |This role authorizes the service\-associated role for NLB log delivery. NLB uses this role to access your resources in Torch Log Service (TLS) for log delivery. |

Details are as follows:

**NLBFullAccess**

After being authorized this policy, you gain full management permissions for all NLB resources within the permission scope and view permissions for Virtual Private Cloud (VPC), subnet, and Elastic Compute Service (ECS).

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "clb:*NLB*",
        "clb:*NetworkLoadBalancer*",
        "vpc:DescribeVpcs",
        "vpc:DescribeSubnets",
        "vpc:DescribeNetworkInterfaces",
        "vpc:DescribeSecurityGroups",
        "ecs:DescribeInstances",
        "vpc:DescribeEipAddresses",
        "vpc:DescribeBandwidthPackages",
        "Volc_Observe:GetMetricsData",
        "cloudmonitor:GetMetricsData"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```

**NLBReadOnlyAccess**

After authorizing this policy, all NLB resources within the permission scope can be viewed.

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "clb:DescribeNLB*",
        "clb:DescribeNetworkLoadBalancer*",
        "clb:ListNLBTagsForResources",
        "Volc_Observe:GetMetricsData",
        "cloudmonitor:GetMetricsData"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```

**ServiceRoleForNLBLogDelivery**

This policy supports authorizing only the service\-associated role for NLB log delivery. After authorization, NLB can create and query related resources in the log service through this role.

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "tls:CreateProject",
        "tls:ModifyProject",
        "tls:DescribeProject",
        "tls:DescribeProjects",
        "tls:CreateTopic",
        "tls:ModifyTopic",
        "tls:DescribeTopics",
        "tls:DescribeTopic",
        "tls:CreateIndex",
        "tls:ModifyIndex",
        "tls:DescribeIndex",
        "tls:PutLogs"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```

### Roles or policies required by the NLB console features

|Feature |Required cloud service |Required role/policy |
|---|---|---|
|Create an NLB instance |VPC |After granting the NLBFullAccess permission to an IAM user:<br><br><br>* If the IAM user’s main account already has VPC instances, no additional permissions are needed to create NLB instances.<br><br>* If there are no VPC instances in the IAM user's root user account, either use the root user account to create VPC instances or add permissions for the IAM user. The following two solutions are available for granting permissions to IAM users:<br><br>   * Solution 1: Add VPCFullAccess permission for the IAM user.<br><br>   * Solution 2: Add a custom policy for the IAM user that grants permissions to create VPC instances and subnets. The policy content is as follows:<br><br>      ```Plain Text```<br>```      {```<br>```          "Statement":[```<br>```              {```<br>```                  "Effect":"Allow",```<br>```                  "Action":[```<br>```                      "vpc:CreateVpc",```<br>```                      "vpc:CreateSubnet"```<br>```                  ],```<br>```                  "Resource":[```<br>```                      "*"```<br>```                  ]```<br>```              }```<br>```          ]```<br>```      }```<br>```      ```<br>       |
|Add backend servers to server groups |Elastic Compute Service |After granting the IAM user the NLBFullAccess permission:<br><br><br>* If the IAM user's associated root account contains ECS instances, no additional permissions are needed to add backend servers to the server group.<br><br>* If the root user associated with the IAM user does not have ECS instances, please create ECS instances using the root user or add permissions for the IAM user. The following two solutions are available for granting permissions to IAM users:<br><br>   * Solution 1: Add ECSFullAccess permission for the IAM user.<br><br>   * Solution 2: Add a custom policy for the IAM user that grants permission to create ECS instances. The policy content is as follows:<br><br>      ```Plain Text```<br>```      {```<br>```          "Statement":[```<br>```              {```<br>```                  "Effect":"Allow",```<br>```                  "Action":[```<br>```                      "ecs:RunInstances"```<br>```                  ],```<br>```                  "Resource":[```<br>```                      "*"```<br>```                  ]```<br>```              }```<br>```          ]```<br>```      }```<br>```      ```<br>       |

## Custom policy

|Topic |Explanation |
|---|---|
|Custom policy types |Custom policies are categorized based on the entity to which the policy can be bound: Identity\-based policies and Resource\-based policies. |
|Custom policy syntax |Custom policy syntax defines policy permissions through policy elements. When creating an identity\-based policy and a resource\-based policy, the policy elements differ. |
|Create custom policy |When you use a BytePlus main account or an IAM user with IAM permissions to authorize, and the system default policy cannot meet your requirements, you can granularly define permissions through a custom policy. |

##
