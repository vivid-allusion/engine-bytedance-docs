---
title: "Cross-service Authorization"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/cross-service-authorization"
---

Before you use Cloud Search, authorize cross\-service access to allow Cloud Search to access other BytePlus services such as Virtual Private Cloud (VPC) and Elastic IP Address (EIP). This topic describes how to authorize cross\-service access.

<span id="f3d5accb"></span>
## Background Information

Identity and Access Management (IAM) supports policy management. To enable Cloud Search to access other BytePlus services, assign the `ServiceRoleForESCloud` role to your Cloud Search account and attach the `ServiceRoleForESCloud` policy to the role.

The `ServiceRoleForESCloud` policy is defined as follows:

```SQL
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "tos:*",
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


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precaution

If you want to use an IAM user for cross\-service authorization, make sure that the IAM user has the `IAMFullAccess` permissions. Otherwise, an error occurs upon authorization.

<span id=".5L2_55So5o6n5Yi25Y-w5o6I5p2D"></span>
## Procedure


1. Log into the [BytePlus Cloud Search console](https://console.byteplus.com/es).

2. For a first\-time user, the **Cross\-service access request** page will pop up. Please confirm the role and attached policy, and then click **Authorize**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can go to <a href="https://console.byteplus.com/iam/identitymanage/role">BytePlus IAM Role</a> page to check whether <code>ServiceRoleForESCloud</code> is successfully created.</div>


* <div data-tips="true" data-tips-type="tip">Cross\-service authorization confirmation is only required for the first time.</div>
