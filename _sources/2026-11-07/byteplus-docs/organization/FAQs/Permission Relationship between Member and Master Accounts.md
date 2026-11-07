---
title: "Permission Relationship between Member and Master Accounts"
product: "BytePlus Organization"
product_code: "organization"
source: "https://docs.byteplus.com/en/docs/organization/PermissionRelationship"
---

In organization, the permission management relationship between member accounts and master account is controlled and maintained in the following ways:

&nbsp;

<span id="_1-the-master-account-controls-the-permission-scope-of-member-accounts"></span>
## 1.The master account controls the permission scope of member accounts

The master account is able to specify the service access scope of member accounts.

The services here refer to basic platform services such as the Identity and Access Management (IAM) service, ECS, and so on.

Examples:


* Prevent a certain account from making certain changes to the IAM users and roles under that account.

* Prevent a member account from leaving the organization.

* Control the instance type of an ECS.


<span id="_1-1-the-master-account-sets-the-permission-scope-of-member-accounts-through-control-policies"></span>
### 1.1 The master account sets the permission scope of member accounts through control policies

Through control policies, the scope of operations that member accounts are allowed to perform on their own account resources is defined, limiting the maximum permission scope of member accounts. The permission scope defined by the control policies cannot be changed by the member accounts themselves, and the IAM policies set within the account cannot exceed the permission scope of the management policies either.

<span id="_1-2-the-permissions-of-member-accounts-over-the-master-account"></span>
### 1.2 The permissions of member accounts over the master account

By default, member accounts have no permission to access or operate on the resources of the master account or other member accounts.

&nbsp;

<span id="_2-the-permission-scope-of-the-master-account-within-member-accounts"></span>
## 2. The permission scope of the master account within member accounts

The master account accesses member accounts through role\-playing. It can be understood as automatically creating a "steward" position under the member account, with corresponding stewardship authorities. The master account acts as the "steward" to access the member account and exercise management authorities.

&nbsp;

<span id="_2-1-the-default-permissions-of-the-master-account"></span>
### 2.1 The default permissions of the master account

By default, the master account can have all the permissions to manage the resources of member accounts. After successfully inviting and creating a member account, a role (OrganizationAccessControlRole) trusted by the master account will be automatically created under the IAM of the member account, and full management permissions (AdministratorAccess) will be granted, which is equivalent to the permissions of the root user of the member account: managing all users within the account and their permissions, financial\-related information, and the permissions of service assets. The master account can use this role to log in and manage the resources related to the member account.

&nbsp;

<span id="_2-2-member-accounts-modifying-the-default-permissions"></span>
### 2.2 Member accounts modifying the default permissions

Member accounts can modify or delete the permissions of the master account. After logging in to the member account, within IAM \- Identity Management \- Roles, the OrganizationAccessControlRole can be modified, and the option to delete this role is available. There are two implementation effects for these operations:

<span id="_2-2-1-prohibit-the-master-account-from-accessing-the-member-account"></span>
#### 2.2.1 Prohibit the master account from accessing the member account

The role 'OrganizationAccessControlRole' can be deleted by logging in to the member account and deleting the role in IAM console.

<span id="_2-2-2-restrict-the-master-account-s-access-to-the-member-account"></span>
#### 2.2.2 Restrict the master account's access to the member account

If the master account is allowed to access but its access permissions need to be restricted, then the permission policies attached to the OrganizationAccessControlRole need to be adjusted. In IAM console, click to edit the role and edit the attached permission policies.

You can delete the AdministratorAccess policy, add system managed policies, or add and modify custom policies within policy management.
