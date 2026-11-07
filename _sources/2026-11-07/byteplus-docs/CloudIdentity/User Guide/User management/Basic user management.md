---
title: "Basic user management"
product: "BytePlus Cloud Identity"
product_code: "CloudIdentity"
source: "https://docs.byteplus.com/en/docs/CloudIdentity/Basic-user-management"
---

<span id="scenarios"></span>
## Scenarios

When you initialize the cloud identities of your enterprise, you must use your identity management platform as the "identity source" of your cloud identities to import employee identities into Cloud Identity.

If the number of employees that need to log in is small, you can create users with the same names on Cloud Identity and perform manual management operations such as addition, deletion, update, and query through the approaches described in this topic.

If the number of employees that need to log in is large, you can refer to [User synchronization settings](https://docs.byteplus.com/en/docs/CloudIdentity/Overview-of-SCIM-based-user-synchronization) to directly synchronize all users of your enterprise identity source.

<span id="prerequisites"></span>
## Prerequisites


1. You have activated [Cloud Identity](https://docs.byteplus.com/en/docs/CloudIdentity/Activate-Cloud-Identity).

2. You are an organization master account, such as the root user or an authorized IAM user.


<span id="procedure"></span>
## Procedure

<span id="create-a-user"></span>
### Create a user


1. Log in to the BytePlus console, and go to the [User management](https://console.byteplus.com/cloudidentity/region:ap-southeast-1/user/) page.

2. Click **Create user**.

3. On the Create user page, enter basic information of the user.

   1. The username is required, and must have the same name as the employee for SSO logins. It consists of letters, digits, underscores (_), periods (.), hyphens (\-), and at signs (@) and is 1 to 64 characters in length.

   2. The display name is optional, which is used to identify the identity of an employee. It can be the Chinese name, English name, or alias of the employee.

   3. The description, mobile phone number, and email address are optional. They are additional information for identifying an employee.

   4. If username and password\-based login is enabled on Cloud Identity, you can set a password. You can use a unified custom or random password, and specify whether to reset the password during the next login.

4. After entering information, click OK. If you have created a login password in the previous step, download and save the login information on the result page, and notify the user.


<span id="view-a-user"></span>
### View a user


1. Log in to the BytePlus console, and go to the [User management](https://console.byteplus.com/cloudidentity/region:ap-southeast-1/user/) page.

2. Click a username in the user list.

3. On the page that appears, you can view the basic information of the user. The user information includes the user ID, username, display name, description, creation method (how the user is created, such as synchronization from the identity source or manual creation), identity source (the identity source type of a synchronized user, such as SCIM), creation time, update time, email address, mobile phone number, and department.


<span id="modify-the-basic-information-of-a-user"></span>
### Modify the basic information of a user


1. Log in to the BytePlus console, and go to the [User management](https://console.byteplus.com/cloudidentity/region:ap-southeast-1/user/) page.

2. Click edit or a username in the user list.

3. On the page that appears, you can view and modify the basic information of the user.

   1. For a user synchronized from an identity source, you can modify its description. The rest of the user information changes with the user information in the identity source.

   2. For a manually created user, you can modify its username, display name, description, email address, and mobile phone number.

   3. After clicking on the username to enter the user details page, you can edit the user's basic information.

      In the **Security Settings** module, you can modify the user's security email address, which is used for identity verification when the user logs in to the cloud identity portal. Please note that after modification, remind the user to check their email and complete verification promptly via the verification link (with a validity period of *24 Hours* for the link). The modification will take effect only after verification. During the verification period, if you need to modify the email address again, please withdraw the previous change before proceeding.


<span id="reset-a-login-password"></span>
### Reset a login password


1. Log in to the BytePlus console, and go to the [User management](https://console.byteplus.com/cloudidentity/region:ap-southeast-1/user/) page.

2. If username and password\-based login is enabled on Cloud Identity, you can reset a password in the editing column of the user list. You can also require the user to reset its password upon the next login.


<span id="delete-a-user"></span>
### Delete a user


1. Log in to the BytePlus console, and go to the [User management](https://console.byteplus.com/cloudidentity/region:ap-southeast-1/user/) page.

2. In the editing column of the user list, you can delete users that are manually created. Users synchronized from an identity source cannot be manually deleted. If an employee in the identity source resigns from the company or is removed, the corresponding user in Cloud Identity is automatically deleted upon synchronization.


<span id="what-to-do-next"></span>
## What to do next

After you create a user, you can [configure user login settings](https://docs.byteplus.com/en/docs/CloudIdentity/User-login-settings).
