---
title: "Cross-service access authorization"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Cross-service_access_authorization"
---

Milvus for VectorDB uses other Volcengine services, such as VPCs, subnets, and CloudMonitor. To use all features of Milvus for VectorDB, you must first complete cross\-service access authorization to allow Milvus for VectorDB to access other services. This topic describes how to complete cross\-service access authorization.

## Background

Volcengine Identity and Access Management (IAM) supports policy management. You can associate the `ServiceRoleForMilvus` role with the Milvus for VectorDB service account and link the `ServicePolicyForMilvus` policy to this role to access other services.

The definition statement of the `ServicePolicyForMilvus` access policy is as follows:

```SQL
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "vpc:DescribeVpcs",
                "vpc:DescribeVpcAttributes",
                "vpc:DescribeSubnets",
                "vpc:DescribeSecurityGroups",
                "vpc:CreateNetworkInterface",
                "vpc:DeleteNetworkInterface",
                "vpc:DescribeNetworkInterfaces",
                "vpc:CreateNetworkInterfacePermission",
                "vpc:DeleteNetworkInterfacePermission",
                "vpc:DescribeNetworkInterfacePermissions",
                "vpc:AssociateEipAddress",
                "vpc:DisassociateEipAddress",
                "vpc:DescribeEipAddressAttributes",
                "vpc:CreateSecurityGroup",
                "vpc:DescribeSecurityGroupAttributes",
                "vpc:DescribeNetworkInterfaceAttributes",
                "vpc:DescribeSubnetAttributes",
                "vpc:AttachNetworkInterface",
                "vpc:DetachNetworkInterface",
                "vpc:AssociateTrunkInterface",
                "vpc:DisassociateTrunkInterface",
                "vpc:DescribeTrunkAssociations",
                "vpc:AssignIpv6Addresses",
                "iam:ListUsers"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "private_zone:SearchGlobalZone",
                "private_zone:CreatePrivateZone",
                "private_zone:UpdatePrivateZone",
                "private_zone:DeletePrivateZone",
                "private_zone:IncBindVPC",
                "private_zone:UpdateBindVPC",
                "private_zone:ListBindVPC",
                "private_zone:ListPrivateZones",
                "private_zone:QueryPrivateZone",
                "private_zone:CreateRecord",
                "private_zone:UpdateRecord",
                "private_zone:DeleteRecord",
                "private_zone:ListRecords",
                "private_zone:QueryRecord",
                "private_zone:CreateAuthorizedUser",
                "private_zone:DeleteAuthorizedUser",
                "private_zone:ListAuthorizedUsers"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "Volc_Observe:CreateObjectGroup",
                "Volc_Observe:GetMetricData",
                "Volc_Observe:ListObjectGroups",
                "Volc_Observe:ListPresetAlertTemplates",
                "Volc_Observe:ListContactGroups",
                "Volc_Observe:CreateContactGroup",
                "Volc_Observe:UpdateContactGroupWithContacts",
                "Volc_Observe:ListContacts",
                "Volc_Observe:CreateContacts",
                "Volc_Observe:ListRules",
                "Volc_Observe:CreateRule"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```

For more information on access control roles and policies, see [Role Management](https://docs.byteplus.com/en/docs/6257/64979) and [Policy Overview](https://docs.byteplus.com/en/docs/6257/65058).

## Precautions

If you want to perform cross\-service access authorization as an IAM user, the IAM user must have the `IAMFullAccess` permission. Otherwise, corresponding operations will be required during authorization. For the specific steps to authorize IAM users, see [User management](https://docs.byteplus.com/en/docs/6257/64977#%E7%AE%A1%E7%90%86%E7%94%A8%E6%88%B7).

## Authorize using the console

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. On the popup **Cross\-service access request** page, confirm the access role and association policy, then click **Authorize**.

> **tip**

* > After authorization, you can log in to the [Access control console](https://console.byteplus.com/iam/). If the `ServiceRoleForMilvus` role exists, the authorization is successful.

* > If you have authorized previously, you do not need to authorize again.

## Authorize using API

You can call the Access control [CreateServiceLinkedRole](https://docs.byteplus.com/en/docs/6257/71624) API to complete cross\-service authorization, setting `ServiceName` as `milvus`.

## What's next

[Create an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance)
