---
title: "Cross-service authorization"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/Cross-service-authorization"
---

Before using PFS, you need to perform cross\-service access authorization to allow PFS to access other services, such as VPC and TOS. This topic describes the relevant steps for cross\-service access authorization.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background Information

Identity and Access Management (IAM)supports policy management functionality. You can associate the PFS account with the ServiceRoleForVEPFS role and associate that role with the ServiceRoleForVEPFS policy to access other services. The definition statement of the ServiceRoleForVEPFS access policy is as follows:

```Plain
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "vpc:Describe*",
                "vpc:CreateNetworkInterface",
                "vpc:DeleteNetworkInterface",
                "vpc:ModifyNetworkInterfaceAttributes",
                "vpc:AttachNetworkInterface",
                "vpc:DetachNetworkInterface",
                "vpc:CreateNetworkInterfacePermission",
                "vpc:DeleteNetworkInterfacePermission",
                "vpc:DescribeNetworkInterfacePermissions",
                "vpc:CreateSecurityGroup",
                "vpc:AuthorizeSecurityGroupIngress",
                "vpc:AuthorizeSecurityGroupEgress",
                "vpc:RevokeSecurityGroupIngress",
                "vpc:RevokeSecurityGroupEgress",
                "vpc:ModifySecurityGroupAttributes",
                "vpc:DeleteSecurityGroup",
                "ecs:Describe*",
                "ecs:RunInstances",
                "ecs:CreateInstances",
                "ecs:DeleteInstance",
                "tos:List*",
                "tos:Get*",
                "tos:HeadBucket",
                "tos:PutBucketPolicy",
                "tos:DeleteBucketPolicy",
                "tos:CopyObject",
                "tos:DeleteObject",
                "tos:DeleteMultiObjects",
                "tos:HeadObject",
                "tos:AppendObject",
                "tos:PutObject",
                "tos:PutObjectAcl",
                "tos:SetObjectMeta",
                "tos:CreateMultipartUpload",
                "tos:UploadPart",
                "tos:CompleteMultipartUpload",
                "tos:AbortMultipartUpload",
                "tos:UploadPartCopy"
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
## Note

If you need to use a sub\-account for cross\-service authorization, the sub\-account must have IAMFullAccess permission. Otherwise, there will be corresponding errors during authorization.

<span id=".5o6I5p2D5pa55byP"></span>
## Authorization Method


1. Log on to the [PFS console](https://console.byteplus.com/pfs).

2. On the pop\-up **Cross\-service access request** page, Confirm access roles and associated policy information, click **Authorize Now**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After authorization is completed, you can log in to the <a href="https://console.byteplus.com/auth/login/">Access Control Console</a>. If the role ServiceRoleForVEPFS exists in the role, it indicates that the authorization is successful.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you have already authorized before, there is no need to authorize again.   </div>
   


<span id=".5ZCO57ut5q2l6aqk"></span>
## Follow\-up steps

After completing the service authorization, you can proceed to perform other operations on PFS.
