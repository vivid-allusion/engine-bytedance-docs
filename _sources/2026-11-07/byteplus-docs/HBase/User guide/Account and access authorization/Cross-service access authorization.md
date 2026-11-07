---
title: "Cross-service access authorization"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Cross-service_access_authorization"
---

Before using Table Storage for HBase, cross\-service access authorization is needed to allow HBase to access other services (such as VPC and EIP). This topic introduces you to the steps for granting cross\-service access authorization.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

Identity and Access Management (IAM) of BytePlus supports policy management. You can associate Table Storage for HBase accounts with the `ServiceRoleForHBase` role and associate the role with the `ServiceRoleForHBase` policy to access other services.

The statements for defining the `ServiceRoleForHBase` access policy are as follows:

```json
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
        "vpc:DescribeEipAddresses"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```


For more information about IAM roles and policies, refer to [Managing roles](https://docs.byteplus.com/en/docs/byteplus-platform/docs-roles-management) and [Managing policies](https://docs.byteplus.com/en/docs/byteplus-platform/docs-policy-management).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

If you use a sub\-account for cross\-service authorization, the sub\-account must have `IAMFullAccess` permissions. Otherwise, an error will occur during authorization. For detailed steps on granting permissions to a sub\-account, see [Managing users](https://docs.byteplus.com/en/docs/byteplus-platform/docs-user-management).

<span id=".6YCa6L-H5o6n5Yi25Y-w5o6I5p2D"></span>
## Procedure


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. On the **Cross\-service access requests** page, confirm the access roles and associated policies, and click **Authorize**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After service authorization is completed, the <strong>Instance</strong> list page of HBase instances is automatically displayed.</div>


* <div data-tips="true" data-tips-type="tip">If you have performed the authorization, ignore it.</div>



<span id=".5ZCO57ut5q2l6aqk"></span>
## Subsequent procedures

After service authorization is completed, you can continue other operations on HBase instances.
