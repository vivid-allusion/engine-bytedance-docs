---
title: "Overview"
product: "IPv6 Gateway"
product_code: "IPv6"
source: "https://docs.byteplus.com/en/docs/IPv6/IAM_Overview"
---

Identity and Access Management (IAM) is a permission management system supplied by BytePlus to control access to cloud resources for different identities. For example, with IAM, you can grant permissions on multiple cloud resources to different IAM users, set the same permissions for multiple cloud resources, and assign different permissions to different IAM users. This approach enables decentralized resource management, improves management efficiency, and reduces the risk of information leakage.

<span id="basic-concepts"></span>
## Basic concepts


|**Name** |**Description** |
|---|---|
|BytePlus account |An account, or a primary account, is an entity within BytePlus for which resources are allocated, measured, and billed. To use BytePlus services, you need to register a BytePlus account. Generally, the username is used as the login identifier of an account.<br><br>A BytePlus account is the owner of all service resources within the BytePlus account. The BytePlus account has full access permissions on all resources within the BytePlus account. You can use the BytePlus account to perform operations such as purchasing, renewing, and upgrading resources, and the BytePlus account has resource orders and bills. Service resources within the BytePlus account can be operated and accessed with the BytePlus account. |
|IAM user |A sub\-account. It is created by a BytePlus Cloud account. After an IAM user is created, the IAM user belongs to a BytePlus account. The IAM user is not an independent BytePlus Cloud account. The IAM user does not own service resources. The resource usage of the RAM user is not calculated or billed to the RAM user. Before you manage resources as the IAM user, the IAM user must be granted the required permissions. The resources managed by the IAM user belong to the BytePlus account, and you can use the BytePlus account to pay the bills of the IAM user. The IAM user has no independent bills.<br><br>When an authorized IAM user is granted a password and an Access Key, the user can log on to the authorized consoles and call open APIs to manage the resources of the account. |
|User group |A set of users. A user can belong to one or more user groups. After a user group is attached to a policy, the users in the user group have the permissions on the policy. |
|Role |A role cannot directly access cloud services. Before a role accesses cloud services, the role must be entrusted to another identity. After the role is assumed by a trusted identity, the trusted identity obtains a temporary security credential to access the cloud resources as the role. Roles are classified into the following types based on trusted identities:<br><br><br>* Account: Assign the current account or other account to a role. The current account or other account accesses your cloud resources as a role.<br><br>* User: The user can be a real user or a back\-end service. After a role is entrusted to a user, the user obtains a temporary security credential to access cloud resources as the role. This ensures access security.<br><br>* Cloud service: Assign a BytePlus service to a role. The BytePlus service accesses your cloud resource as a role.<br><br>   Cloud services refer to BytePlus cloud services. Some cloud products may rely on your other cloud product resources to provide services. In this case, the cloud products become the IAM identities. You can manage the permissions of product service identities to protect reasonable and secure resource access. |


<span id="use-scenarios-of-iam-policies"></span>
## Use scenarios of IAM policies

Policies describe permissions. Associate policies with IAM users, user groups, or roles to grant permissions. In a policy, you can define the scope of operations, resource range, and conditions for permissions to take effect.

&nbsp;

IAM policies apply to the following authorization scenarios: Granting users permissions on multiple cloud resources, setting the same permissions for multiple cloud resources, and granting different permissions to different users.

<span id="iam-policies"></span>
## IAM policies

By default, a newly created user, user group, or role has no permissions. Before a user or user group has operation permissions on cloud resources, you must attach the user or user group to policies with your BytePlus account.

&nbsp;

IAM supports the following types of policies: System default policies and custom policies.


* System default policies: The IAM console is configured with default EIP policies. If you want to grant permissions to IAM users, user groups, or roles, attach the IAM users, user groups, or roles to preset policies. The following table describes the policies and supported operations.

   
   |**Policy Name** |**Supported Operations** |
   |---|---|
   |IPv6GatewayFullAccess |The IAM identities (IAM users, user groups, roles) authorized with this policy can obtain **management** permission within the scope of IPv6 gateway features. |
   |IPv6GatewayReadOnlyAccess |IAM identities (IAM users, user groups, roles) authorized with this policy can obtain **read\-only** permission within the scope of IPv6 gateway features. |
   

* Custom policies: If default policies configured in the IAM console cannot meet your business requirements, create custom IAM policies as needed. For more information, refer to [Manage custom policies](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-policies).
