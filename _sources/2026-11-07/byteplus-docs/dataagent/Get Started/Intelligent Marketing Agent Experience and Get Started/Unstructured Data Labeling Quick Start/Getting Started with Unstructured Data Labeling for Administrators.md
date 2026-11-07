---
title: "Getting Started with Unstructured Data Labeling for Administrators"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Getting_Started_with_Unstructured_Data_Labeling_for_Administrators"
---

Group administrators and project administrators can manage users within a project and license certain content to those users. When authorizing, the administrator needs to clarify the type and object of authorized users, and then select the specific authorization content to perform authorization operations to ensure the controllability of their usage rights. This article shows you how administrators can quickly set permissions related to marking unstructured data.

<span id="568b599b"></span>
# Overall process

Administrators can refer to the following steps to add users and grant users the corresponding permissions to quickly use the agent, for more permission information, please refer to [Manage by user ](https://www.volcengine.com/docs/6356/1154925)and [Authorization Configuration](https://docs.byteplus.com/docs/dataagent/Authorization_Configuration).


1. [New user](https://docs.byteplus.com/docs/dataagent/Getting_Started_with_Unstructured_Data_Labeling_for_Administrators#237110e2)The administrator creates a user sub\-account user.

2. [Select Authorized Objects](https://docs.byteplus.com/docs/dataagent/Getting_Started_with_Unstructured_Data_Labeling_for_Administrators#1c38c2c2)Add users/user groups to the platform's project.

3. [Grant project resource permissions](https://docs.byteplus.com/docs/dataagent/Getting_Started_with_Unstructured_Data_Labeling_for_Administrators#0649f55d)Grant users viewing and administrative permissions for the project.

4. [Grant feature module permissions](https://docs.byteplus.com/docs/dataagent/Getting_Started_with_Unstructured_Data_Labeling_for_Administrators#8f165d56)Grant users segmentation permissions for specific functional modules.

5. [grant resource permission](https://docs.byteplus.com/docs/dataagent/Getting_Started_with_Unstructured_Data_Labeling_for_Administrators#6ae7c123)Give users global authorization tags, grouping, and insight into these three resource types.

6. [grant data permission](https://docs.byteplus.com/docs/dataagent/Getting_Started_with_Unstructured_Data_Labeling_for_Administrators#24e5c99d): Grant users permission to use special data rules.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The priority of editing permissions for specific applications and knowledge bases is higher than that of functional modules.</div>


* <div data-tips="true" data-tips-type="tip">View permissions are basic permissions, edit permissions are sub\-basic permissions, and new permissions are advanced permissions. Turning on advanced permissions will synchronously turn on its basic permissions, and turning off basic permissions will synchronously turn off its advanced permissions. For example, when the view permission is turned off, the editing permission and the new permission are turned off synchronously; when the editing permission is turned off, the new permission is also turned off synchronously. Turning on the view permission does not affect the switch of editing and new permissions.</div>



All possible permission controls are described in the following table:


|**Function permission** |||**App and knowledge base permissions** ||**Fact Sheet** |
|---|---|---|---|---|---|
|view |edit |new build |view |edit ||
|√ |√ |√ |√ |√ |Allows viewing, editing, and new creation |
|√ |√ |× |√ |√ |New construction is not allowed |
|√ |× |× |√ |√ |New construction is not allowed<br><br>Allow viewing<br><br>Allows editing of knowledge base/AI apps with editing privileges |
|√ |√ |√ |√ |× |Do not allow editing Knowledge Base/AI apps without editing permissions |
|√ |√ |× |√ |× |New construction is not allowed<br><br>Do not allow editing Knowledge Base/AI apps without editing permissions |
|√ |× |× |√ |× |New construction is not allowed<br><br>Do not allow editing Knowledge Base/AI apps without editing permissions<br><br>Allows editing of other knowledge base/AI applications with editing privileges |


<span id="237110e2"></span>
# New user


1. Log in to Intelligent Marketing Agent , enter account number and password.

2. Clicking on the "Unstructured Data Marking" service card will take you to VeCDP's "Visual Modeling" page.

3. Create a new system user.

   1. The administrator clicks on the avatar in the upper right corner and selects "Access Control" **.** 

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/11e5524ead0d4060b988b7882bb02506~tplv-goo7wpa0wc-image.image) </span>

   2. Enter "User Management \> User", click "New User", fill in the user information and permission configuration to complete the creation, please refer to [User Management ](https://www.volcengine.com/docs/6257/64977)for specific operations.

      This article takes "Creating by Username" as an example, and the operation is as follows:

      1. Select "Create by username".

      2. Fill in the user's basic information.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">"Username" (must be English letters, cannot be entered in Chinese), such as test.         </div>
         

      3. Check "Programming Access \- Allow users to manage their own API keys" in the access method, and the system will automatically assign AK to the user; you can also check "Console Access"  **,**  select "Custom Generated Password" when accessing the password  **,**  and check "No need to reset the password" when resetting the password, click "Next".

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a9882b728da4e4e8adbbc4859dddf22~tplv-goo7wpa0wc-image.image) </span>

      4. On the Permissions Configuration page, after completing the required permissions check, click **Next**.

         Account types and permissions are described as follows:

         
         |**Role** |**Scope of authority** |
         |---|---|
         |Administrator (admin) |All resources under the group access + permission allocation permission |
         |normal user |Users who have been granted editing rights to Enterprise Knowledge Engine and AI applications |
         

      5. On the review page, check whether the configuration item created by the user is accurate. If it is inaccurate, you can return to the previous step to modify it. After confirming that it is correct, click "Next" and enter the verification code to complete the creation of the IAM sub\-account.


<span id="1c38c2c2"></span>
# **Select Authorized Objects**

On the Customer Data Platform page, select "Project Center", click "Rights Management" \- "Manage by User", and click "Add User".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/58208a4c691942f297f89b40e716dd57~tplv-goo7wpa0wc-image.image) </span>

To add a user group, click the "User Group" tab, and then click "Add User Group". Click the "Edit" icon of "Include Users" to add a member of the user group.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c3d589a651a47519b30e9733d023a8a~tplv-goo7wpa0wc-image.image) </span>

<span id="0649f55d"></span>
# Grant project resource permissions


1. Click "Project Center", select "Rights Management \> Manage by User", and select "Projects". Enter the project page, and the left side will display all the users/user groups created under the current project. Administrators can manage the rights of users/user groups.

2. Set user/user group viewing and administrative permissions for the project.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e789340a97fc4ce6998cda6bfb78b9d7~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">It is not recommended to authorize individual users one by one, which is inefficient and costly to maintain. It is recommended that:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the authority system is to be connected to the organizational structure, it is recommended to use the organizational structure as the main authorization object, supplemented by user groups that can make some flexible changes.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the permission system does not connect with the organizational structure, it is recommended to use "roles" or "user groups" as the main authorization object.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">"Roles": Roles are group\-granular and cross\-project. Once a role is created, it will be visible in the various projects under the group, and each project does not need to be created repeatedly. If the roles of each project are consistent, and there are roles for data development, operations, marketing, etc., the concept of "roles" is suitable.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">"User groups": A user group is project\-granular, and a user group created is only available within that project. If you only need to use it at the granularity of the project, such as a project data development group A, operation group B, etc., the concept of "user group" is suitable.   </div>
   


<span id="8f165d56"></span>
# Grant feature module permissions


1. Click "Project Center", select "Rights Management \> Manage by User", and select "Modules".

2. Click the "Edit" button on the right and check the permissions of model application, visual modeling and other modules.

3. Click "Save".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/72fbd2db59f546c2adab6b97974c0b96~tplv-goo7wpa0wc-image.image) </span>


<span id="6ae7c123"></span>
# Grant resource permission


1. Click "Project Center", select "Rights Management \> Manage by User", and select "Resources".

2. Click "Global Authorization" on the right side of the "Resource Page".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f47d4fe2e2ee4660aa5b5f9138080a81~tplv-goo7wpa0wc-image.image) </span>

3. In the expanded authorization box, click "Authorize to" on the right.

4. Check the type of resource that needs to be granted (label, grouping, insight), the scope of permissions (view, edit, manage), and the type of authorization object and the specific object that needs to be authorized, and click OK to complete the authorization.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3465820d0ea54a3384d11c4c23e3dd00~tplv-goo7wpa0wc-image.image) </span>


<span id="24e5c99d"></span>
# Grant data permission


1. Click "Project Center", select "Rights Management \> Manage by User", and select "Data".

2. To set a user's permissions on data permissions rules, you can view the specific permissions rules or remove the permissions.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">At present, only "tags" are supported for line permission control. For example, user A can only view users of "source channel = WeChat" on this platform, and user B can only view users of "source channel = Douyin" on this platform. For details, please refer to the document <a href="https://www.volcengine.com/docs/6356/1154926#_3-4-%E6%95%B0%E6%8D%AE%E6%8E%88%E6%9D%83">Data authorization </a>.   </div>
