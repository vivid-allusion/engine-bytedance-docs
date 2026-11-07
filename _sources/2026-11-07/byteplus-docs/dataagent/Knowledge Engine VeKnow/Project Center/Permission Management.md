---
title: "Permission Management"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Authorization_Management__"
---

The permission management function of the enterprise knowledge engine console is a management tool for refined knowledge management, data access, project center, one customer, one policy engine and marketing interaction assistant. This function can help enterprise administrators configure permissions efficiently and in batches, avoid unauthorized operations, and ensure the security and control of marketing data and resources. It is suitable for typical scenarios such as multi\-department marketing team collaboration and permission isolation of personnel at different levels. This article describes how to manage users and user permissions.

# Manage users

1. Log into the Marketing Agent console and select **Enterprise Knowledge Engine** in the left navigation bar.

2. In the left navigation bar of the Enterprise Knowledge Engine, select **Project Center** \> **Permission Management** \> **User Management**.

   In user management, the following operations are supported:

   * **Manage** **new user default configurations**

      Whether to grant new users access to all features by default.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/72f416792ed74d038e5e84e73794b03e~tplv-goo7wpa0wc-image.image)

   * **Add user**

      * In the upper right corner of the page, click **Add user**, in the pop\-up add box, support add users by user, by department, and by role in batches.

      * Support entering and searching by keywords of user, department, and role.

      * Choose to authorize project administrator status according to the actual situation.

      * If the user is not found, you can click **New User** to enter the management center to create a new user.

      > **注意**

      * > Adding users in the user management of the project center is essentially adding the IAM sub\-users you added in the BytePlus access control and binding their permissions.

      * > The maximum number of users is 1000 (subject to adjustment to comply with product deployment requirements).

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/efb1dc6aea7f4450b4cc909d63039808~tplv-goo7wpa0wc-image.image)

   * **Edit user information, deactivate or activate user accounts, remove users**

      In the **operation** column of the user list, it supports editing, deactivating, and removing users.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e4ef30a133024cd9895320b4607e0e37~tplv-goo7wpa0wc-image.image)

   * **Configure user permissions**

      Click **Authorize** in the **operation** column of the user list to redirect to the **per\-user management** page to configure **module permissions** or **resource permissions** for the current user.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ca4826a999149d194a6c253e0bbd927~tplv-goo7wpa0wc-image.image)

# Manage permissions by user

Per\-user management refers to user\-centric authorization of specific content resource permissions to each user object.

> **注意**

> The SaaS version does not currently support roles and department management permission.

## Add user

1. Log into the Marketing Agent console and select **Enterprise Knowledge Engine** in the left navigation bar.

2. In the left navigation bar of the Enterprise Knowledge Engine, select **Project Center** \> **Permission Management** \> **Manage by User**.

3. In the upper left corner of the **Users** tab, click **Add User**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b2bf8fd3f4f49508824b1aef6cd476e~tplv-goo7wpa0wc-image.image)

4. In the pop\-up add box, batch addition of users is supported.

   * Support for entering user keywords for search.

   * Choose to authorize project administrator status according to the actual situation.

   * If the user is not found, you can click **New User** to enter the management center to create a new user.

   > **说明**

   > It should be noted that adding users in the user management of the project center is essentially adding the IAM sub\-users you added in the BytePlus access control and binding their permissions.

5. At the bottom of the **Users** tab, click **Manage all users** to access the User Management page.

   For related operations, see [Manage users](https://docs.byteplus.com/docs/dataagent/Authorization_Management__#23237170).

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6d920b16959249a5b150d1e0530b053b~tplv-goo7wpa0wc-image.image)

## Authorize users

When authorizing, the administrator needs to clarify the type and object of authorized users, and then select the specific authorization content to perform authorization operations to ensure the controllability of their usage permission.

Go to the **Users** tab and select the specified user to configure **module permissions** or **resource permissions** on the page.

* **Module permissions: view**, **edit** and **manage** permissions for each functional module.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8a37eace86014ab08a42bf2e2eea4dee~tplv-goo7wpa0wc-image.image)

* **Resource permissions: view**, **edit**, or **manage** resources such as knowledge bases, retrieval applications, documents, data source metadata, datasets, visual modeling tasks, and Knowledge Graph.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c0ca555dd29a4cd299a65a3f3122fdfa~tplv-goo7wpa0wc-image.image)

# Manage permissions by content

Content\-based management refers to content\-centric, assigning specific users to each content object (module, resource).

## Manage module permissions

1. Log into the Marketing Agent console and select **Enterprise Knowledge Engine** in the left navigation bar.

2. In the left navigation bar of the Enterprise Knowledge Engine, select **Project Center** \> **Permission Management** \> **Manage by Content**.

3. On the **Module Permissions** tab, select Specify Module, and in the **operation** column, click **Add Authorization**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/30f9429f9ce84b7f91868c76aefd3926~tplv-goo7wpa0wc-image.image)

4. In the **Add Authorization** interface that pops up on the right, configure the following information and click **Save**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a8e7ef61be864590b046075997edf74a~tplv-goo7wpa0wc-image.image)

   * **Authorize permissions:**  single selection, you can choose to **view**, **edit**, **manage** permissions.

   * **Authorized object** :

      1. Select the **user** object type.

      2. After selection, select one or more objects in the list.

5. Return to the module permissions list and click **Manage Authorized** in the **operation** column.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c86df907581481585c89c425484f9c5~tplv-goo7wpa0wc-image.image)

   Authorized list information can be viewed according to the **user** 's dimension.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/70acc3b18d17447dbc883f4603891d58~tplv-goo7wpa0wc-image.image)

   * In the list, support real\-time adjustment of the corresponding user's **viewing**, **editing**, **managing** permissions.

   * Click **Authorize** in the top right corner of the list to continue adding authorization information.

## Manage resource permissions

1. Log into the Marketing Agent console and select **Enterprise Knowledge Engine** in the left navigation bar.

2. In the left navigation bar of the Enterprise Knowledge Engine, select **Project Center** \> **permission management** \> **Manage by Content**.

3. On the **Resource Permissions** tab, select Specify Resource Type and in the **operation** column click **Add Authorization**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dd6e3b0ae6df467cb94c90868d4747a2~tplv-goo7wpa0wc-image.image)

4. In the **Add Authorization** interface that pops up on the right, configure the following information and click **Save**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/120b013e8f644853a5741fdac917822f~tplv-goo7wpa0wc-image.image)

   * **Grant permissions**: \*\*\*\* single selection, you can choose to **view**, **edit**, **manage** permissions.

   * **Authorized object**:

      1. Select the **user** object type.

      2. After selection, select one or more objects in the list.

5. To return to the list of resource permissions, click **Manage Authorized** in the **operation** column.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b7ef19093664a8d8ca47bc8cf0a5d1e~tplv-goo7wpa0wc-image.image)

   Authorized list information can be viewed by **user** dimension.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/30bdfa3d6d794325a48021d4f7e6ecb3~tplv-goo7wpa0wc-image.image)

   * In the list, support real\-time adjustment of the corresponding user's **viewing**, **editing**, **managing** permissions.

   * Click **Authorize** in the top right corner of the list to continue adding authorization information.
