---
title: "Cross-service authorization"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Cross-service_authorization"
---

Before using an ECS instance, you need to complete cross\-service access authorization first to enable your instance to access other services (such as VPC and TOS). This topic describes the steps for cross\-service access authorization.

<span id="fILk52Ch"></span>
## **Background**

BytePlus IAM supports policy management. You can authorize ECS instances to access other services by attaching the `ServiceRoleForECS` role to your ECS service account and then attaching the `ServicePolicyForECS` policy to that role. The definition of the `ServicePolicyForECS` policy is as follows:

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "tos:GetObject",
        "tos:HeadObject",
        "tos:PutObject",
        "tos:HeadBucket",
        "tos:CreateMultipartUpload",
        "tos:CompleteMultipartUpload",
        "vpc:DescribeNetworkInterfaces",
        "vpc:DescribeNetworkInterfaceAttributes",
        "vpc:DeleteNetworkInterface",
        "vpc:DescribeVpcAttributes",
        "vpc:DescribeSubnetAttributes",
        "vpc:DescribeSecurityGroupAttributes",
        "vpc:DescribeEipAddresses",
        "vpc:AllocateEipAddress",
        "vpc:AssociateEipAddress",
        "vpc:ModifyEipAddressAttributes",
        "vpc:DisassociateEipAddress",
        "vpc:ReleaseEipAddress",
        "vpc:DescribeVpcs",
        "vpc:CreateVpc",
        "vpc:DescribeSubnets",
        "vpc:CreateSubnet",
        "vpc:ModifyNetworkInterfaceAttributes",
        "vpc:CreateSecurityGroup",
        "vpc:DescribeSecurityGroups",
        "vpc:AuthorizeSecurityGroupEgress",
        "vpc:DescribeEipAddressAttributes"
      ],
      "Resource": [
        "*"
      ]
    },
    {
      "Effect": "Allow",
      "Action": [
        "Volc_InfluxDB_Proxy:Write",
        "cloudmonitor:Write"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For more information about IAM roles and policies, see Role management and Policy management.</div>


<span id="Q3nhhOXA"></span>
## **Usage notes**

If you need to perform cross\-service authorization using an IAM user, the user must have `IAMFullAccess` permission. Otherwise, errors will occur during authorization. For steps to grant permissions to an IAM user, see User management.

<span id="R28gpcx5"></span>
## Authorization methods

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">After authorization, you can log in to the <a href="https://console.byteplus.com/iam/">IAM console</a>. If the <code>ServiceRoleForECS</code> role exists in the role list, the authorization succeeds.</div>


<div data-tips="true" data-tips-type="default">If you have authorized previously, you do not need to authorize again.</div>


<span id="DoIFogw3"></span>
### **Authorize via the console**


1. Log in to the[ ECS console](https://console.byteplus.com/ecs/region:ecs+cn-guangzhou/dashboard?projectName=default).

2. On the "Cross\-service access request" page that appears, confirm the access role and associated policy information, then click the "Authorize now" button to complete authorization.


<span id="ppv5hcg2"></span>
### Authorize via an authorization link


1. Log in to the [ECS console](https://console.byteplus.com/ecs/region:ecs+cn-guangzhou/dashboard?projectName=default).

2. Click the [ServiceRoleForECS](https://console.byteplus.com/iam/service/attach_role/?ServiceName=ecs) link, and then click the "Authorize now" button to complete authorization.


<span id="Ifxsf553"></span>
### **Authorize via API**

You can call the IAM CreateServiceLinkedRole API to complete cross\-service authorization. During authorization, specify `ServiceName` as `ecs`.
