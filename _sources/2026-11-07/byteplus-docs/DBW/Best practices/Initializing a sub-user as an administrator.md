---
title: "Initializing a sub-user as an administrator"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Initializing_a_sub-user_as_an_administrator"
---

This topic describes the operation steps for initializing the sub\-user created by the primary account as an administrator when logging on to the DBW console user management for the first time.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A BytePlus account has been registered and completed verification. For the detailed method, refer to [Sign up and verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* As per the regulations in the Chinese mainland, you must have completed real name registration before you can activate and use cloud services on regions in the Chinese mainland through BytePlus. For more details, refer to [Real name registration](https://docs.byteplus.com/en/docs/byteplus-platform/docs-real-name-registration).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The sub\-user who logs in to user management for the first time can be initialized as an administrator.

* If a sub\-user who is added as an administrator or normal user is removed, the sub\-user will not be initialized as an administrator even if logging in to user management again. To become an administrator, you need to [apply to become an administrator](https://docs.byteplus.com/en/docs/DBW/role-permission-request) or [contact the administrator to add](https://docs.byteplus.com/en/docs/DBW/user-management-for-mysql).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. The primary account creates a sub\-user and grants the sub\-user the `AdministratorAccess` permission policy.

   * Create a sub\-user

      1. Log on to the [Access control](https://console.byteplus.com/iam/identitymanage/user) console using the primary account.

      2. On the left navigation bar, click **User**.

      3. On the **User** page, click **Create user**.

         On the Create user page, configure the relevant parameters. For details, refer to [User management](https://docs.byteplus.com/en/docs/DBW/user-management-for-mysql).

   * Authorize the sub\-user

      1. Log on to the [Access control](https://console.byteplus.com/iam/identitymanage/user) console using the primary account.

      2. On the left navigation bar, click **User**.

      3. On the **User** page, click **Add permissions** in the **Actions** column of the target user.

      4. On the **Authorization policy** pane, select the `AdministratorAccess` permission policy.

      5. Click **Submit**.

2. The sub\-user is initialized as an administrator

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When a sub\-account logs on to DBW User management for the first time, you must first allow DBW to access IAM configurations on BytePlus.   </div>
   

   1. Log on to the [DBW console](https://console.byteplus.com/dbw).

   2. On the left navigation bar, select **Data management** \> **User management**.

   3. On the top menu bar of the **User management** page, select the region.

   4. On the **User management** page, click **Authorize**.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fe35ca75a67de88a7eeccbc9dca3297c.png) </span>

   5. In the **Are you sure to authorize?**  dialog box, click **OK**.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2c83382867cf3044619e42dc622823f8.png) </span>

   After authorization, your sub\-user account will be initialized as an administrator for DBW.
