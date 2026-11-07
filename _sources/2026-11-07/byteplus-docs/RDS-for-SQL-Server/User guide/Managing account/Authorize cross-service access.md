---
title: "Authorize cross-service access"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/Authorize_cross-service_access"
---

Before using RDS for SQL Server, you must authorize cross\-service access to allow SQL Server to access other services (such as VPC, EIP, and TOS). This topic describes the steps for cross\-service access authorization.

<span id="3lslbx7i"></span>
## Description

BytePlus Identity and Access Management (IAM) supports policy management. You can associate the `ServiceRoleForRDSMSSQL` role with your RDS for SQL Server account, and then associate the role with the `ServicePolicyForRDSMSSQL` policy to access other services.

The following is an example of the definition statement for the `ServicePolicyForRDSMSSQL` access policy:

```JSON
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
        "vpc:DescribeEipAddressAttributes"，
        "tos:ListBuckets",
        "tos:HeadBucket",
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```


<span id="xUeU6Z7E"></span>
## Precautions

If you need to use a sub\-user to authorize cross\-service access, the sub\-user must have the `IAMFullAccess` permission. Otherwise, an error will be reported during authorization. For the specific steps to grant permissions to a sub\-user, see [About users](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-users).

<span id="sB5WsvV3"></span>
## Authorize through the console


1. Log on to the [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. On the **Cross\-Service Access Request** page, confirm the access role and associated policy information, and click **Authorize**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After service authorization is complete, you will be automatically returned to the <strong>Instances</strong> page.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you have previously granted authorization, you do not need to grant it again.   </div>
   


<span id="RelAH7a1"></span>
## Authorize through an API

You can call the [CreateServiceLinkedRole](https://docs.byteplus.com/en/docs/byteplus-platform/reference-createservicelinkedrole) API of Access Control to grant cross\-service access. When authorizing, `ServiceName` is `rds_mssql`.

<span id="PvyS3Mch"></span>
## Next steps

After the service authorization is complete, you can proceed with other operations for the SQL Server instance.
