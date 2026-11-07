---
title: "Identity and access management"
product: "Bandwidth Package"
product_code: "bandwidthpackage"
source: "https://docs.byteplus.com/en/docs/bandwidthpackage/Identity-and-access-management"
---

Identity and Access Management (IAM) is a permission management system provided by BytePlus and is used to manage access permissions of different identities on cloud resources. For example, it can grant permissions on multiple cloud resources to different IAM users, grant the same permissions to multiple cloud resources, and grant different permissions to different IAM users. This facilitates decentralized resource management, improves management efficiency, and reduces information leakage risks.

For more information on IAM, refer to [What is IAM?](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-3)

<span id="basic-concepts"></span>
## Basic concepts


|**Concept** |**Description** |
|---|---|
|BytePlus account |An account, or a primary account, is an entity within BytePlus for which resources are allocated, measured, and billed. Before you use BytePlus services, you must create a BytePlus account. In most cases, a username is used as the login identity of an account.<br><br>A BytePlus account is the owner of all service resources within the BytePlus account. The BytePlus account has full access permissions for all resources within the BytePlus account. You can use the BytePlus account to perform operations such as purchasing, renewing, and upgrading resources. Resource usage is calculated and billed to the BytePlus account. Service resources within the BytePlus account can be operated on and accessed with the BytePlus account. |
|IAM user |An IAM user, or an Identity and Access Management (IAM) user, is an authorized entity of the primary account and also a resource belonging to the primary account. After an IAM user is created, the IAM user belongs to a BytePlus account. The IAM user is not an independent BytePlus Cloud account. An IAM account does not own any service resources and is not independently billed. An IAM account is only authorized by the primary account to manage the resources of the primary account. Resources managed by an IAM account are owned and paid for by the primary account.<br><br>When an authorized IAM user is granted a password and an AccessKey, the user can log on to the console and use open APIs to manage the resources of the primary account. |
|User group |A set of users. A user can belong to one or more user groups. After a user group is attached to a policy, the users in the user group have the permissions on the policy. |
|Role |A role cannot directly access cloud services, but must be entrusted to another identity first. Then, the trusted identity assumes the role to obtain temporary security credentials to access cloud resources. Roles are classified into the following types based on trusted identities:<br><br><br>* Account: Roles can be assigned to the current account or other account so that this account can access your cloud resources.<br><br>* User: The user can be a real user or a back\-end service. After a role is assigned to a user, the user obtains a temporary security credential to access cloud resources as the role. This ensures access security.<br><br>* Cloud service: Roles can be assigned to BytePlus services to give them access to your cloud resources.<br><br>   Cloud services refer to BytePlus cloud services. Some cloud products may rely on your other cloud product resources to provide services. In this case, the cloud products become the IAM identities. You can manage the permissions of product service identities to ensure reasonable and secure resource access. |


<span id="scenarios"></span>
## Scenarios

IAM policies are applicable to the following authorization scenarios:


* Users are granted permissions for multiple cloud resources.

* The same permissions are set for multiple cloud resources.

* Different users are granted different permissions.


<span id="iam-policies"></span>
## IAM policies

By default, a newly created user, user group, or role has no permissions. Before a user or user group has operation permissions on cloud resources, you must attach the user or user group to policies with your BytePlus account.

IAM supports the following types of policies: System default policies and custom policies.


* System default policies: The IAM console is configured with default Bandwidth Package policies. If you want to grant permissions to IAM users, user groups, or roles, attach the IAM users, user groups, or roles to preset policies. The following table describes the policies and supported operations.

   
   |**Policy Name** |**Description** |**Supported Operations** |
   |---|---|---|
   |BandwidthPackageFullAccess |Bandwidth Package read and write policy |Manage Bandwidth Packages, including creating, viewing, and deleting resources. |
   |BandwidthPackageReadOnlyAccess |Bandwidth Package read\-only policy |View resources of a Bandwidth Package. |
   

* Custom policies: If default policies configured in the IAM console cannot meet your business requirements, create custom IAM policies as needed. For more information, refer to [Policy management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-policies).
