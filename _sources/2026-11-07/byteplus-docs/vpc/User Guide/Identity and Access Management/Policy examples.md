---
title: "Policy examples"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Example-of-custom-policy"
---

## System default policy

The IAM platform provides default VPC\-related policies in advance. You can directly assign these system default policies to IAM entities (IAM users, user groups, or roles). **System default policies can only be used for authorization and cannot be edited or modified**.

|System default policy name |Description |
|---|---|
|VPCFullAccess |After being granted this policy, the IAM entity (IAM user, user group, or role) will obtain **management** permission for VPC features within the scope of permission. |
|VPCReadOnlyAccess |After being granted this policy, the IAM entity (IAM user, user group, or role) will obtain **read\-only** access to VPC features within the scope of permissions. |

> **tip**

> Wildcard\*: Match zero, one, or multiple characters.

### VPCFullAccess

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "vpc:*Vpc*",
        "vpc:*Subnet*",
        "vpc:*NetworkInterface*",
        "vpc:*Route*",
        "vpc:*SecurityGroup*",
        "vpc:*HaVip*",
        "vpc:*NetworkAcl*",
        "vpc:*PrivateIpAddresses",
        "vpc:*Ipv6Addresses",
        "vpc:*FlowLog*",
        "vpc:*PrefixList*",
        "vpc:*TrafficMirror*",
        "vpc:TagResources",
        "vpc:UntagResources",
        "vpc:ListTagsForResources",
        "cen:GrantInstanceToCen",
        "cen:RevokeInstanceFromCen",
        "cen:DescribeInstanceGrantedRules",
        "quota:GetServiceQuota",
        "ecs:DescribeZones"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```

### VPCReadOnlyAccess

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "vpc:*DescribeVpc*",
        "vpc:*DescribeSubnet*",
        "vpc:*DescribeNetworkInterface*",
        "vpc:*DescribeRoute*",
        "vpc:*DescribeSecurityGroup*",
        "vpc:*DescribeHaVip*",
        "cen:DescribeInstanceGrantedRules",
        "vpc:*DescribeNetworkAcl*",
        "vpc:*DescribeFlowLog*",
        "vpc:*DescribePrefixList*",
        "vpc:*DescribeTrafficMirror*",
        "vpc:ListTagsForResources"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```

## Custom policy

Deny takes precedence over Allow. If an entity is denied permissions for certain operations, granting Allow permissions for those operations will not take effect.

### Example 1: Deny VPC and subnet deletion

After granting the VPCFullAccess policy to an IAM user, you can assign the following additional permissions to explicitly deny VPC and subnet deletion operations.

```JSON
{
  "Statement": [
    {
      "Effect": "Deny",
      "Action": [
        "vpc:DeleteVpc",
        "vpc:DeleteSubnet"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```

### Example 2: Grant permissions for managing a specific subnet

After assigning the VPCReadOnlyAccess policy to an IAM user, you can grant them additional permissions for a specific subnet (e.g., subnet\-2yyxafgve001), enabling them to manage that subnet.

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "vpc:*Subnet*"
      ],
      "Resource": [
        "trn:vpc:*:*:subnet/subnet-2yyxafgve001"
      ]
    }
  ]
}
```

### Example 3: Grant permissions to modify routes in a specific route table

Allow an IAM user to modify route entries only in a specified route table (e.g., vtb\-2fdzao4h726f45). Add vtb\-2fdzao4h726f45 to a project, and grant the IAM user the following permissions within that project.

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "vpc:DescribeRouteTable*",
        "vpc:*RouteEntry*"
      ],
      "Resource": [
        "*"
      ]
    },
    {
      "Effect": "Allow",
      "Action": [
        "vpc:Describe*",
        "ecs:Describe*",
        "vpn:Describe*",
        "natgateway:Describe*", 
        "transitrouter:Describe*" 
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```

### Example 4: Grant permissions to use VPC tagging functionality

```JSON
{
    "Statement":[
        {
            "Effect":"Allow",
            "Action":[
                "vpc:TagResources",
                "vpc:UntagResources",
                "vpc:ListTagsForResources"
            ],
            "Resource":[
                "*"
            ]
        }
    ]
}
```
