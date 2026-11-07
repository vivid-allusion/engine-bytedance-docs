---
title: "Cross-service access authorization"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/cross-service_access_authorization"
---

Before using RDS for MySQL, cross\-service access authorization is needed to allow MySQL to access other services (such as VPC and EIP). This topic describes the procedure for authorizing cross\-service access.

<span id="background"></span>
## Background

Identity and Access Management (IAM) of BytePlus supports policy management. You can associate MySQL accounts with the `ServiceRoleForRDSMySQL` role and associate the role with the `ServiceRoleForRDSMySQL` policy to access other services.

The statements for defining the `ServiceRoleForRDSMySQL` access policy are as follows:

```Plain Text
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "vpc:DescribeVpcs",
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
                "vpc:AssociateEipAddress",
                "vpc:DisassociateEipAddress",
                "vpc:DescribeEipAddressAttributes",
                "vpc:DescribeSecurityGroupAttributes",
                "kms:CreateKeyring",
                "kms:CreateKey",
                "kms:GenerateDataKey"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}

```


For more information about IAM roles and policies, refer to [Role Management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-roles-management) and [Managing policies](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-policies).

<span id="procedure"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. On the **Cross\-service access requests** page, confirm the access roles and associated policies, and click **Authorize**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">说明   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After service authorization is completed, the <strong>Instance list</strong> page of MySQL instances is automatically displayed. Please wait.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you have performed the authorization, ignore it.   </div>
   


<span id="subsequent-procedures"></span>
## Subsequent procedures

After service authorization is completed, you can continue other operations on MySQL instances.
