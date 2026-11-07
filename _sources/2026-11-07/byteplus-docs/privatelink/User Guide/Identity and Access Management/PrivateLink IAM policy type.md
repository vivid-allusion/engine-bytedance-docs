---
title: "PrivateLink IAM policy type"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/PrivateLink-IAM-Policy-Type"
---

This topic introduces the types of IAM policies and policies related to PrivateLink to help you quickly understand IAM policies. Identity and Access Management (IAM) policies support two types: System default policy and Custom policy. You can use system default policies to authorize IAM identities directly. If the system default policies cannot meet your needs, you can use custom policies for precise authorization and flexible resource management.

## System default policy

The IAM platform provides default PrivateLink\-related policies in advance. You can directly assign these system default policies to IAM entities (IAM users, user groups, or roles). **System default policies can only be used for authorization and cannot be edited or modified**.

### PrivateLink system default policy

> **tip**

* > When the service provider and service consumer belong to the same account, it is recommended that you grant the account either the `PrivateLinkFullAccess` or `PrivateLinkReadOnlyAccess` permission.

* > When the service provider and service consumer belong to different accounts, it is recommended that you grant the service consumer account the `PrivateLinkEndpointFullAccess` or `PrivateLinkEndpointReadOnlyAccess` policy. Grant the service provider account the `PrivateLinkEndpointServiceFullAccess` or `PrivateLinkEndpointServiceReadOnlyAccess` policy.

|System default policy name |Description |Policy type |
|---|---|---|
|PrivateLinkFullAccess |IAM identities (IAM users, user groups, or roles) granted this policy will obtain full administrative permissions for PrivateLink within the authorized scope, including create, view, and delete operations. |Policy |
|PrivateLinkReadOnlyAccess |An IAM identity (IAM user, user group, or role) granted this policy obtains read\-only access to all PrivateLink resources within the authorized scope. If an IAM identity is granted only this permission, it will have read\-only access to PrivateLink resources. It cannot perform any operations on PrivateLink resources and cannot access other unauthorized products. |Policy |
|PrivateLinkEndpointServiceFullAccess |IAM identities (IAM users, user groups, or roles) granted this policy will obtain full administrative permissions for endpoint service within the authorized scope, including create, view, and delete operations. |Policy |
|PrivateLinkEndpointServiceReadOnlyAccess |An IAM identity (IAM user, user group, or role) granted this policy obtains read\-only access to all endpoint service resources within the authorized scope. If an IAM identity is only granted this policy, it can only view endpoint service resources. It cannot perform any operations on them, and cannot view endpoint resources or other unauthorized products. |Policy |
|PrivateLinkEndpointFullAccess |IAM identities (IAM users, user groups, or roles) granted this policy will obtain full administrative permissions for endpoint within the authorized scope, including create, view, and delete operations. |Policy |
|PrivateLinkEndpointReadOnlyAccess |An IAM identity (IAM user, user group, or role) granted this policy obtains read\-only access to all endpoint resources within the authorized scope. If an IAM identity is only granted this policy, it can only view endpoint resources. It cannot perform any operations on them, and cannot view endpoint service resources or other unauthorized products. |Policy |

### Roles or policies required for PrivateLink console features​​

|Console feature |Required cloud service |Required role/policy |
|---|---|---|
|View PrivateLink monitoring details​​ |Cloud Monitor |After granting an IAM user the PrivateLinkFullAccess or PrivateLinkReadOnlyAccess policy, you must additionally grant CloudMonitorReadOnlyAccess to enable them to view monitoring information for PrivateLink resources. |

### PrivateLink system default policy details

### PrivateLinkFullAccess policy details

> **tip**

> After being granted this permission, the identity obtains full administrative permissions for all PrivateLink resources within the authorized scope, as well as read\-only access to Virtual Private Cloud (VPC) instances, subnets, security groups, and Classic Load Balancer (CLB) instances.

```json
{
    "Statement": [
        {
            "Effect": "Allow",  //Allow performing all the actions authorized by this policy on the specified resources
            "Action": [
                "privatelink:*",  //All actions for the PrivateLink service
                "vpc:DescribeVpcs", //view VPC Instances list
                "vpc:DescribeSubnets",  //view subnet list
                "vpc:DescribeSecurityGroups",  //View security group list
                "clb:DescribeLoadBalancers"  //View CLB instance list
            ],
            "Resource": [
                "*"  "*" //all resources
            ]
        }
    ]
}
```

### PrivateLinkReadOnlyAccess policy details

> **tip**

> After being granted this permission, the identity obtains read\-only access to all PrivateLink resources within the authorized scope, as well as read\-only access to Virtual Private Cloud (VPC) instances, subnets, security groups, and Classic Load Balancer (CLB) instances.

```json
{
    "Statement": [
        {
            "Effect": "Allow",  //Allow performing all the actions authorized by this policy on the specified resources
            "Action": [
                "privatelink:Describe*",  //All query actions for the PrivateLink service
                "vpc:DescribeVpcs",  //view VPC Instances list
                "vpc:DescribeSubnets",  //view subnet list
                "vpc:DescribeSecurityGroups",  //View security group list
                "clb:DescribeLoadBalancers"  //View CLB instance list
            ],
            "Resource": [
                "*"  "*" //all resources
            ]
        }
    ]
}
```

### PrivateLinkEndpointServiceFullAccess policy details

> **tip**

> After being granted this permission, the identity obtains full administrative permissions for all Endpoint Service resources within the authorized scope, as well as read\-only access to CLB instances.

```json
{
    "Statement": [
        {
            "Effect": "Allow", //Allow performing all the actions authorized by this policy on the specified resources
            "Action": [
                "privatelink:CreateUniqueResourceTypeVpcEndpointService",  //Create an endpoint service for RDS type service resource
                "privatelink:CreateVpcEndpointService",  //Create an endpoint service for CLB type service resource
                "privatelink:DescribeVpcEndpointServices",  //View endpoint service list
                "privatelink:ModifyUniqueResourceTypeVpcEndpointServiceAttributes",  //Modify information about the endpoint service of RDS type service resource
                "privatelink:ModifyVpcEndpointServiceAttributes",  //Modify information about the endpoint service of CLB type service resource
                "privatelink:DescribeVpcEndpointServiceAttributes",  //View interface endpoint service details
                "privatelink:AttachResourceToVpcEndpointService",  //Add service resources
                "privatelink:DescribeVpcEndpointServiceResources",  //View service resource list
                "privatelink:DetachResourceFromVpcEndpointService",  //Remove service resource
                "privatelink:DeleteVpcEndpointService",  //Delete endpoint service
                "privatelink:DescribeVpcEndpointConnections",  //View endpoint connection list
                "privatelink:EnableVpcEndpointConnection",  //Accept endpoint connection
                "privatelink:DisableVpcEndpointConnection",  //Reject endpoint
                "privatelink:AddPermissionToVpcEndpointService",  //Add service allowlist
                "privatelink:RemovePermissionFromVpcEndpointService",  //Remove service allowlist
                "privatelink:DescribeVpcEndpointServicePermissions",  //View the service allow list
                "privatelink:DescribePrivateLinkAvailableZones",  //View endpoint service supported Availability Zone list
                "clb:DescribeLoadBalancers"  //View CLB instance list
            ],
            "Resource": [
                "*"  "*" //all resources
            ]
        }
    ]
}
```

### PrivateLinkEndpointServiceReadOnlyAccess policy details

> **tip**

> After being granted this permission, the identity obtains read\-only access to all Endpoint Service resources within the authorized scope, as well as read\-only access to CLB instances.

```json
{
    "Statement": [
        {
            "Effect": "Allow",  //Allow performing all the actions authorized by this policy on the specified resources
            "Action": [
                "privatelink:DescribeVpcEndpointServices",  //View endpoint service list
                "privatelink:DescribeVpcEndpointServiceAttributes",  //View endpoint service details
                "privatelink:DescribeVpcEndpointServiceResources",  //View service resource list
                "privatelink:DescribeVpcEndpointConnections",  //View endpoint connection list
                "privatelink:DescribeVpcEndpointServicePermissions",  //View the service allow list
                "clb:DescribeLoadBalancers"  //View CLB instance list
            ],
            "Resource": [
                "*"  "*" //all resources
            ]
        }
    ]
}
```

### PrivateLinkEndpointFullAccess policy details

> **tip**

> After being granted this permission, the identity obtains full administrative permissions for all Endpoint resources within the authorized scope, as well as read\-only access to VPC instances, subnets, and security groups.

```json
{
    "Statement": [
        {
            "Effect": "Allow",  //Allow performing all the actions authorized by this policy on the specified resources
            "Action": [
                "privatelink:DescribeVpcEndpointServicesByEndUser",  //Query the list of endpoint services under this Account
                "privatelink:CreateVpcEndpoint",  //Create interface endpoint
                "privatelink:DescribeVpcEndpoints",  //View interface endpoint list
                "privatelink:ModifyVpcEndpointAttributes",  //Edit interface endpoint
                "privatelink:DescribeVpcEndpointAttributes",  //View interface endpoint details
                "privatelink:DescribeVpcEndpointSecurityGroups",  //View endpoint security group list
                "privatelink:AttachSecurityGroupToVpcEndpoint",  //Associate a security group with the interface endpoint
                "privatelink:DetachSecurityGroupFromVpcEndpoint",  //Disassociate a security group from the interface endpoint
                "privatelink:AddZoneToVpcEndpoint",  //Add an Availability Zone to the interface endpoint
                "privatelink:RemoveZoneFromVpcEndpoint",  //Delete an Availability Zone from the interface endpoint
                "privatelink:DescribeVpcEndpointZones",  //View the Availability Zone list of the interface endpoint
                "privatelink:DeleteVpcEndpoint",  //delete interface endpoint
                "vpc:DescribeVpcs", //view VPC Instances list
                "vpc:DescribeSubnets",  //view subnet list
                "vpc:DescribeSecurityGroups" //View security group list
            ],
            "Resource": [
                "*" "*" //all resources
            ]
        }
    ]
}
```

### PrivateLinkEndpointReadOnlyAccess policy details

> **tip**

> After being granted this permission, the identity obtains read\-only access to all Endpoint resources within the authorized scope, as well as read\-only access to VPC instances, subnets, and security groups.

```json
{
    "Statement": [
        {
            "Effect": "Allow",  //Allow performing all the actions authorized by this policy on the specified resources
            "Action": [
                "privatelink:DescribeVpcEndpoints",  //View interface endpoint list
                "privatelink:DescribeVpcEndpointAttributes",  //View interface endpoint details
                "privatelink:DescribeVpcEndpointSecurityGroups",  //View interface endpoint security group list
                "privatelink:DescribeVpcEndpointZones",  //View the list of availability zones for interface endpoints
                "vpc:DescribeVpcs",  //view VPC Instances list
                "vpc:DescribeSubnets",  //view subnet list
                "vpc:DescribeSecurityGroups" //View security group list
            ],
            "Resource": [
                "*"  "*" //all resources
            ]
        }
    ]
}
```

## Custom policy

|Topic |Explanation |
|---|---|
|Custom policy types |Custom policies are categorized based on the entity to which the policy can be bound: Identity\-based policies and Resource\-based policies. |
|Custom policy syntax |Custom policy syntax defines policy permissions through policy elements. When creating an **Identity\-based policy** or **Resource\-based policy**, the policy elements differ. |
|Create custom policy |When you use a BytePlus root user or an IAM user with IAM permissions to authorize, and the system default policy cannot meet your requirements, you can granularly define permissions through a custom policy. |
