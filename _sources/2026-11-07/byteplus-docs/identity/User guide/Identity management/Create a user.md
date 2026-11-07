---
title: "Create a user"
product: "Agent Identity"
product_code: "identity"
source: "https://docs.byteplus.com/en/docs/identity/Create_a_user"
---

A user is the core identity entity in a user pool. This document provides comprehensive instructions on user lifecycle management. You will learn how to create users individually, import them in bulk using a CSV template, edit their information, and manage their status within the Intelligent Identity and Access Management Platform.

<span id="ebfd21b6"></span>
## Precautions

Newly created users are enabled by default. You can disable a user on the user information editing page.

<span id="9fcdb176"></span>
## Prerequisites

You have created a user pool. For related operations, refer to [Create a user pool](https://docs.byteplus.com/docs/identity/89611).

<span id="93230557"></span>
## Create a single user


1. Log in to the BytePlus Agent Identity Console.

2. In the left navigation bar, select **Identity Management \> User Pool**.

3. Click the target user pool name to enter the specified user pool detail page.

4. Switch to the **User** tab and click **Create User**.

5. Configure the relevant user parameters.

   
   |**Configuration items** |**Note** |
   |---|---|
   |**Username** |Set the user's unique identifier.<br><br>Format requirements: [Comment: To be completed] |
   |**Email address** |* Set the user's email address, which can be used for login or receiving notifications.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The email address must conform to the standard email format (for example, xxx@example.com).</div><br><br><br>* <div data-tips="true" data-tips-type="default">Letters, numbers, <code>.</code> , <code>_</code>, <code>-</code>, and <code>@</code> are supported.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Length must be between 1 and 254 characters.</div><br><br><br>* Select **Email verified** to indicate that this email address has been verified and the user does not need to confirm it again. |
   |**Mobile number** |* Set the user's mobile number, which can be used for login or receiving verification codes.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The phone number must conform to the E.164 international format (for example, a Chinese mainland phone number consists of 11 digits, without spaces or special characters).</div><br><br><br>* <div data-tips="true" data-tips-type="default">The country code must be added before the number, for example, <code>+86 xxxxxxxx</code>.</div><br><br><br>* Select **Mobile number verified** to indicate that this mobile number has been verified and the user does not need to confirm it again. |
   |**Temporary password** |Set an initial password for the user. The user is usually required to change this password upon first login.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The password must contain numbers, special characters, and both uppercase and lowercase letters.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The length must be at least 8 characters.</div><br> |
   |**Additional attributes** |Add custom additional attributes for the user. For example: name, gender, date of birth, and more.<br><br>Click **Add key\-value pair** to add a new attribute. Each attribute consists of a **Key** and a **Value**. |
   |**User metadata** |A JSON\-formatted field for storing extended user information, supporting business\-specific customization. For example: `{"department":"Finance"}` |
   

6. Click **OK**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The default status for newly created users is <code>Enabled</code>.   </div>
   

<span id="0c8ce589"></span>
## Bulk import users

To create multiple users in bulk, you can use the bulk import feature.


1. Log in to the BytePlus Agent Identity Console.

2. In the left navigation bar, select **Identity Management \> User Pool**.

3. Click the target user pool name to enter the specified user pool detail page.

4. Switch to the **User** tab and click **Bulk Import**.

5. Click **Download Template** to download the CSV template file provided by the platform to your local device.

6. Open the downloaded template file and fill in the user information according to the column requirements of the template (`username`, `email`, `phone_number`, `password`, and so on).

7. Upload the completed CSV file to the console. The system will validate the file.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Caution   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">File size must not exceed 5 MB.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The number of users imported at one time must not exceed 500.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Common causes of import failure include: duplicate username, email address, or phone number; password does not meet the policy requirements; CSV file format error; and more. Please read the error report carefully, correct the issues, and re\-upload.   </div>
   


<span id="ea68859e"></span>
## Other operations

<span id="f74a05de"></span>
### Edit and delete users


* **Edit User**: In the operations column of the user list, click **Edit**. You can modify the user's email address, phone number, additional attributes, and user status (enabled/disabled). You can also manually mark the user's email address or phone number as "verified" here.

* **Delete User**: In the operations column of the user list, click **Delete**. This is an irreversible operation; the user's personal information and all associated sessions will be permanently deleted.


<span id="ecd77e27"></span>
### Update user status

Below is an explanation of the different user statuses:


* **Unconfirmed**: This status applies when a user registers directly (not through a third\-party IdP) but has not yet verified their email address or mobile number. This is the default status after a new user registers.

* **Confirmed**: The user has verified their email address or mobile number, or an administrator has manually confirmed the account. In this status, the user can log in directly without additional verification or password modification requirements.

* **Password change required**: This status applies to users imported by an administrator or developer, or when an administrator enforces a password change. In this status, the user must log in with a temporary password and set a new password.

* **External provider**: The user registers or logs in through a third\-party IDP, and the identity is managed by the third party.

* **Disabled**: The user is disabled by an administrator and cannot log in. In this status, the user can log in only after being manually enabled by an administrator.
