---
title: "Adding IAM users, organizations, or roles"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-managing-iam-users-and-roles"
---

This document describes how to add an IAM user, organization, or role, including assigning organizations and roles to users, which makes IAM user permission management more fine\-grained and flexible.

<span id="25abd8c1"></span>
## Prerequisite

A BytePlus account or an IAM user with **Account Overview** \> **Edit** permission. For more information, see [Signing up for a BytePlus account](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account).

<span id="b0edeff3"></span>
## Steps

<span id="241e6b39"></span>
### Adding a user


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. On BytePlus Live's menu bar, click **Authorization**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1055d6b0ea5d4435a6b7c2e8aa636081~tplv-goo7wpa0wc-image.image) </span>

3. On the **Users** page, click **Add user**.

4. In the **Add user** dialog box that appears, click **Add user**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e52312be7bc475780d3566fb9d77214~tplv-goo7wpa0wc-image.image) </span>

5. Complete the following configurations and click **OK**. Then, a user will be added both on the **Authorization** \> **Users** page of BytePlus Live and the [IAM > Identity management > User](https://console.byteplus.com/iam/identitymanage/user) page of BytePlus.

   
   |**Configuration** |**Description** |**Notes** |
   |---|---|---|
   |User type |Select **Email**. Currently, you can only add users by using email. |You cannot change the email address after the user is added. Make sure that you enter the correct one. |
   |User account |Enter the user's email address, which is used as the **Sub\-account username** to log in to the BytePlus Live console on the [IAM user sign in](https://console.byteplus.com/auth/login/user/?redirectURI=%2Flivesaas%2FaccountManagement%2FroleManage) page. |None |
   |User nickname |Enter the user's nickname. |The nickname cannot exceed 16 characters and can only contain English letters, digits, and Chinese characters. |
   |Affiliated organization |Select the organization where the user belongs. For more information on how to add organizations, see [Adding an organization](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles#442b626b). |None |
   |Role |Select one or more roles to assign to this user. For more information on how to create roles, see [Adding a role](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles#08751041). |If no role is selected, the default role is assigned to the user and the user can only view and edit live rooms created by themselves. |
   

   After a user is added, they will receive an email and can log in to the BytePlus Live console by using the login URL, email address, and password contained in that email.

6. You can also perform the following operations:

   * Search for users by nickname or email address. Fuzzy search is supported.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">English letters are case insensitive.      </div>
      

   * Click **Edit** in the **Actions** column and change the nickname, organization, and roles of a user as needed in the **Edit user** dialog box that appears.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/706bfdd557344c66900d996200aee63c~tplv-goo7wpa0wc-image.image) </span>

   * Click **Reset password** in the **Actions** column to reset a user's password used to log in to the console. The system will send an email containing a random new password to the user. Currently, only the main BytePlus account can customize an IAM user's password. For more information, see [How to customize the password of an IAM user?](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles#fd3d4ba8).

   * Click **Delete** in the **Actions** column to delete a user.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">After being deleted here, the user can still log in to the BytePlus console to use other services. You can also use the same email address to add the user again on this page.      </div>
      

<span id="08751041"></span>
### Adding a role


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. On BytePlus Live's menu bar, click **Authorization**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1055d6b0ea5d4435a6b7c2e8aa636081~tplv-goo7wpa0wc-image.image) </span>

3. On the left navigation pane, click **Subaccount** \> **Roles**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f47f09a1251e4b0a87b2e7be022e013d~tplv-goo7wpa0wc-image.image) </span>

4. On the **Roles** page, click **Create role**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/81d081d61dab4f389b1380316980afdf~tplv-goo7wpa0wc-image.image) </span>

5. In the **New role** dialog box that appears, complete the following configurations and click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To clip a video, start a live stream, and export data, a user must have edit permission to the page where these features are.   </div>
   

   
   |**Configuration item** |**Description** |
   |---|---|
   |Role name |Enter the role name. The role name cannot exceed 16 characters and can only contain English letters, digits, and Chinese characters. |
   |Permission assignment |Configure the permissions and visible scope for users assigned this role.<br><br><br>* **Live room permissions:**  Configure the live room permissions and visible scope.<br><br>   Users assigned this role have specific permissions to live rooms within the visible scope. For example, select organization A as the visible scope, and select **Live control** \> **Edit**, **Producer** \> **View only**, and **Insight** \> **No permission** as the live room permissions. Then, users assigned this role have edit permission to the **Live control** page, view only permission to all pages of the **Producer** module, and no permission to any pages of the **Insight** module in all live rooms created by users in organization A.<br><br>   * Select the live room permissions.<br><br>   * Select the visible scope.<br><br>      * **Self**: Users assigned this role can only access or edit all the live rooms created by themselves. This option is selected by default and cannot be deselected.<br><br>      * **All users**: Selecting this checkbox allows users with this role to access or edit all live rooms created by other users (including the main BytePlus account and its IAM users).<br><br>      * **Designated users**: Select this checkbox and select users from the corresponding drop\-down list. Users assigned this role can only access or edit live rooms created by the selected users.<br><br>         You can search for users by nickname or email address. Fuzzy search is supported and English letters are case insensitive.<br><br>      * **Designated organizations**: Select this checkbox and select organizations from the corresponding drop\-down list. Users assigned this role can only access or edit live rooms created by users within the selected organizations.<br><br>         You can search for organizations by name. Fuzzy search is supported and English letters are case insensitive.<br><br>      * **Designated live rooms**: Select this checkbox and select live rooms from the corresponding drop\-down list. Users assigned this role can only access or edit the selected live rooms.<br><br>         You can search for live rooms by name. Fuzzy search is supported and English letters are case insensitive.<br><br>* Account permissions: Select the account permissions.<br><br>   Users assigned this role have specific permissions to specific pages on the BytePlus Live console. For example, select **Media library** \> **Video library** \> **Edit**, **Data center** \> **User portrait** \> **View only**, and **Account center** \> **Account overview** \> **No permission** as the account permissions. Then, users assigned this role have edit permission to the **Video library** page, view only permission to the **User portrait** page, and no permission to the **Account overview** page.<br><br>   When selecting **Media library** \> **Video library** \> **View only** or **Edit**, you can select the user range and classification range. If both the user range and classification range are selected, the final visible range will be the intersection of the two.<br><br>   Select the user range after selecting **Media library** \> **Live temporary** \> **View only** or **Edit**, **Media library** \> **Cloud clips** \> **View only** or **Edit**, and **Media library** \> **Prize library** \> **View only** or **Edit**.<br><br>   * User range: Defines the range of videos, cloud clip projects, or prizes users with this role can access or edit.<br><br>      * **Self**: Users assigned this role can only access or edit videos and cloud clip projects they have uploaded or created. Videos and cloud clip projects uploaded or created by the user are also subject to the selected account permissions. This option is selected by default and cannot be deselected.<br><br>      * **All users**: Select this checkbox and then users assigned this role can access or edit videos and cloud clip projects uploaded or created by other users, including the BytePlus account and its IAM users, except themselves.<br><br>      * **Designated users**: Select this checkbox and select users from the corresponding drop\-down list. Users assigned this role can only access or edit videos and cloud clip projects uploaded or created by the selected users.<br><br>         You can search for users by nickname or email address. Fuzzy search is supported and English letters are case insensitive.<br><br>      * **Designated organizations**: Select this checkbox and select organizations from the corresponding drop\-down list. Users assigned this role can only access or edit videos and cloud clip projects uploaded or created by users within the selected organizations.<br><br>         You can search for organizations by name. Fuzzy search is supported and English letters are case insensitive.<br><br>   * **Category scope**: Users assigned this role can only access or edit videos under the selected categories and their subcategories. You can search for categories by name. Fuzzy search is supported and English letters are case insensitive. If no category scope is configured, users with this role can access or edit videos from all categories by default. All users can access or edit videos under the default category. |
   

6. You can also perform the following operations:

   * Search for roles by role name. Fuzzy search is supported and English letters are case insensitive.

   * Click **Edit** in the **Actions** column. Change the name, permissions, and visible scope of a role as needed in the **Edit role** dialog box that appears.

   * Click **Delete** in the **Actions** column to delete a role.


<span id="08ecb0ea"></span>
#### Built\-in roles

Besides the roles you create, BytePlus Live provides the following built\-in roles:


* Super administrators: This is a role with edit permission to live rooms and all pages on the BytePlus Live console. This role cannot be modified or deleted.

* Default role: This is a role generally used to view and edit live rooms and the media library. This role cannot be deleted.

* Operation: This is a role generally used to view live rooms and pages on the BytePlus Live console.

* Data: This is a role generally used to view and export data.

* Assistant: This is a role generally used to send interaction tools such as questionnaires, votes, and lucky draws during the live stream.


<span id="c86a1f31"></span>
### Adding an organization


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. On BytePlus Live's menu bar, click **Authorization**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1055d6b0ea5d4435a6b7c2e8aa636081~tplv-goo7wpa0wc-image.image) </span>

3. On the left navigation pane, click **Subaccount** \> **Organizations**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9f0c9309bbd4940912b8d32c38b7299~tplv-goo7wpa0wc-image.image) </span>

4. On the **Organizations** page, click **Add organization**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/94bb4d99d2b44b57aa3046722a35a284~tplv-goo7wpa0wc-image.image) </span>

5. In the **Add organization** dialog box that appears, enter the organization name and click **OK**.

   The organization name cannot exceed 20 characters and can only contain English letters, digits, and Chinese characters.

6. You can also perform the following operations:

* Search for organizations by organization name. Fuzzy search is supported and English letters are case insensitive.

* Click **Edit** in the **Actions** column. Change the name of an organization as needed and view users added to this organization in the **Edit organization** dialog box that appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5bde8ea9fcbe43b4ab7e95208a69b003~tplv-goo7wpa0wc-image.image) </span>

* Click **Delete** in the **Actions** column to delete an organization.


<span id="5f820fa0"></span>
## FAQ

<span id="fd3d4ba8"></span>
### How to customize the password of an IAM user?

Currently, only the BytePlus account can customize the password of an IAM user.


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/) as a BytePlus account.

2. Click your portrait in the upper\-right corner of the console and select **IAM**.

3. On the **Identity management** \> **User** page, click the username of the IAM user or click **View details** in the **Actions** column.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0ff2952462984a2b9942285d42bbb43d~tplv-goo7wpa0wc-image.image) </span>

4. On the **User details** page, click the **Console login** tab and then click **Reset password**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6756ecc6c58f4d0eaf379eae4b0c9b7d~tplv-goo7wpa0wc-image.image) </span>

5. In the **Reset password** dialog box that appears, enter the new password and click **OK**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9e6ec608b379427abe1bc655e598f7ff~tplv-goo7wpa0wc-image.image) </span>
