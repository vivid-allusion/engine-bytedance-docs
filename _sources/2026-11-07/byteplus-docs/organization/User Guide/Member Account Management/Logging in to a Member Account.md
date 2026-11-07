---
title: "Logging in to a Member Account"
product: "BytePlus Organization"
product_code: "organization"
source: "https://docs.byteplus.com/en/docs/organization/LoggingintoaMemberAccount"
---

<span id="method-1-logging-in-with-account-credentials"></span>
## Method 1: Logging in with Account Credentials

<span id="procedure"></span>
### Procedure

Once console login is enabled for a Member Account, you can log in to the console as the Root User by using account credentials.

<span id="method-2-logging-in-by-assuming-the-default-role"></span>
## Method 2: Logging in by Assuming the Default Role

When a Member Account is created or invited to join an Organization, the system automatically creates a role named OrganizationAccessControlRole under the Member Account. This role is granted full IAM management permissions (AdministratorAccess). The Master Account can assume the role to log in to the Member Account and manage resources within the Member Account.

<span id="procedure"></span>
### Procedure


1. Assign a role to a IAM user of the Master Account. The IAM user must be assigned the preset STSAssumeRoleAccess policy.

2. Log in to BytePlus as the IAM user. From the profile menu, select Switch Role.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_9c297e99b11d55b79431c1f0e0295360.png) </span>


3. On the Switch Role page, enter the Member Account ID, Member Account role, and display name for the current role. Click Switch Role to log in to the Member Account with the assigned role.


When a Member Account is created or invited to join an Organization, the system automatically generates the OrganizationAccessControlRole for that account. By default, this role is assigned the preset AdministratorAccess policy. You can adjust the role permissions based on your requirements.
