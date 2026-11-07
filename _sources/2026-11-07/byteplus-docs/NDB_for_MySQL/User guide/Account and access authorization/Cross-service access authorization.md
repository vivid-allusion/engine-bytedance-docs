---
title: "Cross-service access authorization"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Cross-service_access_authorization"
---

Before using NDB for MySQL, cross\-service access authorization is needed to allow NDB for MySQL to access other services (such as VPC and EIP). This topic introduces you to the steps for granting cross\-service access authorization.

<span id="背景信息"></span>
## Background

Identity and Access Management (IAM) of BytePlus supports policy management. You can associate NDB for MySQL accounts with the `ServiceRoleForVeDBMySQL` role and associate the role with the `ServiceRoleForVeDBMySQL` policy to access other services.

The statements for defining the `ServiceRoleForVeDBMySQL` access policy are as follows:

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
                "vpc:DescribeEipAddressAttributes"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


For more information about IAM roles and policies, refer to [Managing roles](https://www.byteplus.com/en/docs/6257/64979) and [Managing policies](https://www.byteplus.com/en/docs/6257/65058).

<span id="操作步骤"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. On the **Cross\-service access requests** page, confirm the access roles and associated policies, and click **Authorize**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After service authorization is completed, the <strong>Instance list</strong> page of NDB for MySQL instances is automatically displayed.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you have performed the authorization, ignore it.   </div>
   


<span id="后续步骤"></span>
## Subsequent procedures

After service authorization is completed, you can continue other operations on NDB for MySQL instances.
