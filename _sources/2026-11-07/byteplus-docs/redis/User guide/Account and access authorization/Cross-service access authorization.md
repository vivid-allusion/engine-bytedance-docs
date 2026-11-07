---
title: "Cross-service access authorization"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/cross-service-access-authorization"
---

Before using Cache for Redis, you need to authorize cross\-service access to allow Redis instances to access other services (such as VPC and EIP). This topic describes the procedure for cross\-service access authorization.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Identity and Access Management (IAM) supports policy management. You can associate the `ServiceRoleForRedis` role with your Cache for Redis account and then associate this role with the `ServiceRoleForRedis` policy to access other services.

The statements for defining the access policy `ServiceRoleForRedis` are as follows:

```JSON
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


For more information about access control roles and policies, refer to [About roles](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-roles) and [About policies](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-policies).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

If you need to authorize cross\-service access for IAM users, the IAM users must have the `IAMFullAccess` permissions, otherwise an error will occur during authorization. For more information on how to authorize IAM users, refer to [About users](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-users).

<span id=".6YCa6L-H5o6n5Yi25Y-w5o6I5p2D"></span>
## Authorize via console


1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. On the **Cross\-service access requests** page, confirm the access roles and associated policies, and click **Authorize**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After service authorization is completed, the <strong>Instances</strong> page of Redis instances is automatically displayed.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you have authorized before, you do not need to authorize again.   </div>
   


<span id=".6YCa6L-HLWFwaS3mjojmnYM="></span>
## Authorize via API

You can call the [CreateServiceLinkedRole](https://docs.byteplus.com/en/docs/byteplus-platform/reference-createservicelinkedrole) API to complete the authorization for cross\-service access with `ServiceName` as `Redis`.

<span id=".5ZCO57ut5q2l6aqk"></span>
## Subsequent operations

After completing service authorization, you can proceed with other operations for the Redis instance.
