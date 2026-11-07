---
title: "Cross-Service Authorization"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Cross-Service-authorization"
---

Before mounting FileNAS, you need to perform cross\-service access authorization to allow FileNAS to access other services such as VPC, EIP, etc. This article introduces the relevant operation steps for cross\-service access authorization.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background Information

The BytePlus Identity and Access Management (IAM) supports policy management functions. You can associate the FileNAS account with the`ServiceRoleForFileNAS` role and associate that role with the `ServiceRoleForFileNAS` policy to access other services. The definition statement of the `ServiceRoleForFileNAS` access policy is as follows:

```Plain
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
                "vpc:Describe*",
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


For more information about access control roles and policies, please refer to [About roles](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-roles) and [About policies](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-policies).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

If you need to use a sub\-account for cross\-service authorization, the sub\-account must have IAMFullAccess permission. Otherwise, there will be corresponding errors during authorization.

<span id=".5L2_55So5o6n5Yi25Y-w5o6I5p2D"></span>
## Granting Authorization via Console


1. Log on to the [FileNAS console](https://console.byteplus.com/filenas).

2. On the pop\-up **Cross\-service access request** page, Confirm access roles and associated policy information, click **Authorize Now**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After authorization is completed, you can log in to the <a href="https://console.byteplus.com/auth/login/">Access Control Console</a>. If the role ServiceRoleForVEPFS exists in the role, it indicates that the authorization is successful.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you have already authorized before, there is no need to authorize again.   </div>
   


<span id=".5L2_55SoLWFwaS3mjojmnYM="></span>
## API authorization

You can use the **CreateServiceLinkedRole** interface of access control to complete cross\-service authorization. When authorizing, the `ServiceName`should be set as `FileNAS`.

<span id=".5ZCO57ut5q2l6aqk"></span>
## Follow\-up steps

After completing the service authorization, you can proceed with other operations of FileNAS.
