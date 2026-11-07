---
title: "IAM user permission management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/managing-permissions-of-an-sub-account"
---

After successfully creating an IAM user, you need to grant the sub\-account permission to access Database Workshop (DBW) when the IAM user needs to access the DBW. This topic describes how to grant permissions to an IAM user to access Database Workshop (DBW).

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The created user is an IAM user.  

* The root user to which the IAM user belongs has been granted permission from Database Workshop (DBW) to access other cloud service resources. For more information, see [Grant root account access to other clouds as a service resource](https://docs.byteplus.com/en/docs/DBW/managing-permissions-of-a-main-account).


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background


* IAM: Identity and Access Management (IAM) is a permission management system used to control the access rights of different identities to cloud resources.  

* Account: Also known as the root user, the owner of cloud service resources and the subject of resource metering and billing. The root user has all permissions under the account by default.

* User: Also known as an IAM user, an identity in access control, created by an account or a user with permissions. After a user is granted permissions (Policy), they can log in to the console or use an Access Key to call an API to access cloud resources.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [Access control ](https://console.byteplus.com/iam/identitymanage/user) using the root user.

2. On the left navigation bar, click **User**.

3. On the **User** page, select the IAM user.

4. On the **User details** page, click **Permissions**.

5. In the **Permissions** tab, under **Directly Attached Permissions**, click **Add Permission**.

6. On the **Add Authorization** page, add the following permission policies as needed.

   * `DbwFullAccess`: Indicates all access permissions of Database Workshop (DBW).

   * `DBWDASFullAccess`: Indicates administrator permissions for O/M and management of Database Workshop (DBW).

   * `DBWDASReadOnlyAccess`: Indicates permissions for viewing O/M and management capabilities of Database Workshop (DBW).

   * `IAMReadOnlyAccess`: Indicates read\-only permissions for IAM.

   * `TLSReadOnlyAccess`: Indicates read\-only permissions for Torch Log Service (TLS).

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You also need to grant IAM users the <code>IAMReadOnlyAccess</code> and <code>TLSReadOnlyAccess</code> permissions, as the database audit logs are provided and billed by Torch Log Service (TLS), when they need to use the audit log feature of the Database Workshop (DBW).      </div>
      

7. Click **OK**.


After an IAM user is granted the corresponding DBW permissions, to manage instance data in the DBW console, the following conditions must also be met: Become an administrator or normal user of DBW, and apply for access permissions to the corresponding instance. For details, see [Personal user management](https://docs.byteplus.com/en/docs/DBW/Personal_user_management?lang=zh).
