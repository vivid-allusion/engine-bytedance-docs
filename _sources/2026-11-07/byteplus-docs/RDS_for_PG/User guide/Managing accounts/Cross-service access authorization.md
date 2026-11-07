---
title: "Cross-service access authorization"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/cross-service_access_authorization"
---

Before using RDS for PostgreSQL, you need to authorize cross\-service access to allow RDS for PostgreSQL instances to access other services (such as VPC and EIP). This topic describes the procedure for cross\-service access authorization.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

BytePlus access control (IAM) supports policy management. You can associate the `ServiceRoleForRDSPG` role with the RDS for PostgreSQL account and attach the `ServiceRoleForRDSPG` policy to this role to access other services.

The definition statement of the `ServiceRoleForRDSPG` access policy is as follows:

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


The trust relationship of the `ServiceRoleForRDSPG` role is as follows:

```Plain Text
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "sts:AssumeRole"
      ],
      "Principal": {
        "Service": [
          "rds_postgresql"
        ]
      }
    }
  ]
}

```


For more information about access control roles and policies, refer to [Managing roles](https://docs.byteplus.com/en/docs/byteplus-platform/docs-roles-management) and [Managing policies](https://docs.byteplus.com/en/docs/byteplus-platform/docs-policy-management).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. Go to the **Cross\-service access requests** pop\-up page, confirm the trust relationships of the associated role and policy, and then click **Authorize**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <strong>Instances</strong> page of the PostgreSQL instance is automatically returned once service authorization is completed.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you have performed the authorization, ignore it.   </div>
   


<span id=".5ZCO57ut5q2l6aqk"></span>
## Next steps

After service authorization is completed, you can continue other operations on PostgreSQL instances.
