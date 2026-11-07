---
title: "User group management"
product: "BytePlus Cloud Identity"
product_code: "CloudIdentity"
source: "https://docs.byteplus.com/en/docs/CloudIdentity/user-group-management"
---

<span id="user-group-management"></span>
# User group management

<span id="scenarios"></span>
## Scenarios

When you need to perform batch SSO authorization for Cloud Identity users, you can use the user group management feature to manage multiple users at a time.

<span id="prerequisites"></span>
## Prerequisites


1. You have completed Cloud Identity user synchronization. Otherwise, you must go to [configure user synchronization settings](https://console.byteplus.com/cloudidentity/region:ap-southeast-1/userSync/).

2. You are an organization master account, such as the root user or an authorized IAM user.


<span id="procedure"></span>
## Procedure


1. Log in to the BytePlus console and go to the [User groups](https://console.byteplus.com/cloudidentity/region:ap-southeast-1/userGroup/) page.

2. You can view all created user groups on this page. The user groups on this page are Cloud Identity user groups, which serve only for configuring multi\-account access in subsequent steps and have no direct relationship with IAM user groups.

3. You can create user groups on this page. To create a user group, you need to enter the user group name, display name, and description as well as select the method to add users.

   1. If you select **Custom**, manually add users to the user group in the next step.

   2. If you select **Automatically add all users**, Cloud Identity will automatically add all users to the user group and add or delete users along with the employee onboarding and offboarding situations.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">For the second user adding method, only one user group can be available, which can be integrated with user group\-based multi\-account access configuration to meet the requirement of automatically granting all employees access permissions on BytePlus.</div>


2. <div data-tips="true" data-tips-type="tip">A user group can contain up to 1,000 users. If this limit is exceeded, users can no longer be automatically added to the user group. <strong>For enterprise system security and stability, we recommend that you only grant login and access permissions to necessary employees.</strong> If you cannot restrict the number of Cloud Identity employees, we recommend that you adopt the custom user adding method for subsequent login permission authorization to avoid permission leakage. Submit a ticket and contact us if you want to increase the user number quota.</div>


4. After creating a user group, you can click the user group name to view details. If you select **Custom** as the user adding method in Step 3, you can add users to the user group on the user group details page. You can also view users in or remove users from the user group. Removing a user from the user group will revoke the associated access permissions if you have configured user access for the user group. For more information, refer to Configure user access based on user group.


<span id="what-to-do-next"></span>
## What to do next

After creating the user group, refer to [Configure user access based on user group](https://docs.byteplus.com/en/docs/CloudIdentity/Configure-multi-account-access-based-on-user-group) for subsequent operations.
