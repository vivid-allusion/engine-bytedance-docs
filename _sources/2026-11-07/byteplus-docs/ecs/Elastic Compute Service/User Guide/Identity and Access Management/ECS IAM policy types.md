---
title: "ECS IAM policy types"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Accessing-resources-with-Identity-and-Access-Management"
---

This topic describes the types of Identity and Access Management (IAM) policies and the policies related to ECS instances to help you quickly understand IAM policies. IAM policies support two types: the system default policy and the custom policy. You can directly grant permissions to IAM identities by using system default policies. If the system default policies cannot meet your needs, you can use custom policies to grant permissions in a fine\-grained way and manage account resources flexibly.

<span id=".57O757uf6aKE6K6-562W55Wl"></span>
## System default policies

<span id=".RUNT57O757uf6aKE6K6-562W55Wl"></span>
### ECS\-related system default policies

The IAM platform provides default ECS\-related policies, as described in the following table.

You can directly assign these system default policies to IAM identities (IAM users, user groups, or roles). **System default policies can be used for authorization only, and cannot be edited or modified.** 


|System default policy name |Description |
|---|---|
|ECSFullAccess |Once granted this policy, IAM identities (IAM users, user groups, and roles) gain management permissions for ECS instances within the permission scope (global or project\-level permissions), including creating, modifying, deleting, and viewing resources. |
|ECSReadOnlyAccess |Once granted this policy, IAM identities (IAM users, user groups, and roles) gain read\-only permissions for ECS instances within the permission scope (global permission or project\-level permission). An IAM identity granted with this policy can only view ECS resources, but not perform any management on them or view other unauthorized cloud products. |


<span id=".RUNT5Yqf6IO95L6d6LWW55qE6KeS6Imy5oiW562W55Wl"></span>
### Roles or policies required for ECS features


|Feature |Required cloud service |Required role/policy |
|---|---|---|
|Manage security enhancement for ECS instances |Security Center |After IAM users are granted the ECSFullAccess or ECSReadOnlyAccess permission, SecCenterFullAccess or SecCenterReadOnlyAccess is also required to view or manage security enhancement statuses of ECS instances. |
|View monitoring details of ECS instances |Cloud Monitor |After IAM users are granted the ECSFullAccess or ECSReadOnlyAccess permission, CloudMonitorReadOnlyAccess is also required to view the monitoring data of ECS instances. |
|Receive event notifications |Message Center |After IAM users are granted the ECSFullAccess or ECSReadOnlyAccess permission, MessageCenterFullAccess or SiteMessageReadOnlyAccess is also required to configure message reception methods (such as SMS, email, or internal messages) or view the internal messages only. |


<span id=".RUNT57O757uf6aKE6K6-562W55Wl6K-m5oOF"></span>
### Details of the ECS\-related system default policies

<span id=".RUNTRnVsbEFjY2VzcyDnrZbnlaXor6bmg4U="></span>
#### Details of the ECSFullAccess policy

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Once this permission is granted, you can obtain management permissions for all resources within the permission scope, including ECS, Classic Load Balancer (CLB), NAT Gateway, tag service (TAG), Virtual Private Cloud (VPC), VPN connection, Elastic Block Storage (EBS), along with view permission for IAM.</div>


```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ecs:*",
                "clb:*",
                "nat:*",
                "tag:*",
                "iam:Get*",
                "iam:List*",
                "iam:MoveProjectResource",
                "vpc:*",
                "vpn:*",
                "storage_ebs:*",
                "Volc_CLB:*"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id=".RUNTUmVhZE9ubHlBY2Nlc3Mg562W55Wl6K-m5oOF"></span>
#### Details of the ECSReadOnlyAccess policy

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Once this permission is granted, all ECS instances and their associated resources within the permission scope can be viewed, such as network and storage.</div>


```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ecs:Get*",
                "ecs:*Describe*",
                "ecs:*List*",
                "clb:Get*",
                "tag:Query*",
                "tag:Get*",
                "iam:Get*",
                "iam:List*",
                "vpc:Get*",
                "vpc:Check*",
                "vpc:*Describe*",
                "vpn:Get*",
                "storage_ebs:*Get*",
                "storage_ebs:*Describe*",
                "storage_ebs:*List*",
                "storage_ebs:Check*",
                "Volc_CLB:Get*",
                "Volc_CLB:List*",
                "Volc_CLB:Describe*"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id=".6Ieq5a6a5LmJ562W55Wl"></span>
## Custom policies

For details, refer to [Creating custom policies](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-3).
