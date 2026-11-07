---
title: "Marketing Interaction Assistant Administrator Getting Started Guide"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Marketing_Interaction_Assistant_Administrator_Getting_Started_Guide"
---

The permissions of the enterprise knowledge engine and AI application in the intelligent conversation assistant are owned by the creator by default, and the creator is the administrator, which can be flexibly authorized in the permission management. This article shows you how administrators can create more sub\-account users and grant them corresponding permissions.

<span id="07567731"></span>
# Overall process

Administrators can refer to the following steps to add users and grant users the corresponding permissions to quickly use the agent, more permission information please refer to [Authorization Management](https://docs.byteplus.com/docs/dataagent/Authorization_Management__).


1. [New user](https://docs.byteplus.com/docs/dataagent/Marketing_Interaction_Assistant_Administrator_Getting_Started_Guide#38299684)The administrator creates a user sub\-account user.

2. [Add user](https://docs.byteplus.com/docs/dataagent/Marketing_Interaction_Assistant_Administrator_Getting_Started_Guide#25419e89)Add users to the platform's project.

3. [Grant feature module permissions](https://docs.byteplus.com/docs/dataagent/Marketing_Interaction_Assistant_Administrator_Getting_Started_Guide#0bc0933c)Grant users the ability to view, edit, or create new content for knowledge bases and AI applications.

4. [Grant Knowledge Base Permissions](https://docs.byteplus.com/docs/dataagent/Marketing_Interaction_Assistant_Administrator_Getting_Started_Guide#eacde8cf)Grant users access to view and edit specific knowledge bases.

5. [Grant app permissions](https://docs.byteplus.com/docs/dataagent/Marketing_Interaction_Assistant_Administrator_Getting_Started_Guide#44d5cd20)Grant users viewing and editing permissions for specific AI applications.

6. [Grant content permissions](https://docs.byteplus.com/docs/dataagent/Marketing_Interaction_Assistant_Administrator_Getting_Started_Guide#401c7044)Grant users access to view and edit specific knowledge files.


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


<span id="38299684"></span>
# New user


1. Log in to Intelligent Marketing Agent , enter account number and password.

2. Find the "Intelligent Conversation Assistant" service card, click "Experience Now", and enter the enterprise knowledge engine page.

3. Create a new system user.

   1. The administrator clicks on the avatar in the upper right corner and selects "Access Control" **.** 

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab6c441afb3c430780f84ab0a15f15bc~tplv-goo7wpa0wc-image.image) </span>

   2. Enter "User Management \> User", click "New User", fill in the user information and permission configuration to complete the creation, please refer to [User Management ](https://www.volcengine.com/docs/6257/64977)for specific operations.

      This article takes "Creating by Username" as an example, and the operation is as follows:

      1. Select "Create by username".

      2. Fill in the user's basic information.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">"Username" (must be English letters, cannot be entered in Chinese), such as test.         </div>
         

      3. Check "Programming Access \- Allow users to manage their own API keys" in the access method, and the system will automatically assign AK to the user; you can also check "Console Access"  **,**  select "Custom Generated Password" when accessing the password  **,**  and check "No need to reset the password" when resetting the password, click "Next".

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/76ca58abd5af4089a4c81411471d14b1~tplv-goo7wpa0wc-image.image) </span>

      4. On the Permissions Configuration page, after completing the required permissions check, click **Next**.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d69e81c3a0944e13a2af826358b2c7ad~tplv-goo7wpa0wc-image.image) </span>

         Account types and permissions are described as follows:

         
         |**role** |**scope of authority** |
         |---|---|
         |Administrator (admin) |All resources under the group access + permission allocation permission |
         |normal user |Users who have been granted editing rights to Enterprise Knowledge Engine and AI applications |
         

      5. On the review page, check whether the configuration item created by the user is accurate. If it is inaccurate, you can return to the previous step to modify it. After confirming that it is correct, click "Next" and enter the verification code to complete the creation of the IAM sub\-account.


<span id="25419e89"></span>
# Add user

On the Enterprise Knowledge Engine page, select "Project Center", click "Rights Management" \- "Manage by User", and click "Add User".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fca64b565ed34c58ab6bf9861cdac8d6~tplv-goo7wpa0wc-image.image) </span>

<span id="0bc0933c"></span>
# Grant feature module permissions


1. Click "Project Center", select "Rights Management \> Manage by User", and select "Function Module". Enter the user rights configuration page, and the left side will display all the users created under the current project. Administrators can manage user rights.

2. Set a user's view, edit, and create permissions for knowledge bases and AI applications.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">To grant editing permissions to the user\-specified knowledge base and applications, you need to first open the editing permissions of the function modules for the user.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/932118ff43a84c0a8c7b94625db92701~tplv-goo7wpa0wc-image.image) </span>


<span id="eacde8cf"></span>
# Grant Knowledge Base Permissions


1. Click "Project Center", select "Rights Management \> Manage by User", and select "Knowledge Base". Enter the user rights configuration page, and the left side will display all the users created under the current project. Administrators can manage user rights.

2. Sets the view and edit permissions for a user on a specific knowledge base.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fdb8b4f59aee4ea0b42f6afa5a15009c~tplv-goo7wpa0wc-image.image) </span>


<span id="44d5cd20"></span>
# Grant app permissions


1. Click "Project Center", select "Rights Management \> Manage by User", and select "Applications". Enter the user rights configuration page, and the left side will display all the users created under the current project. Administrators can manage user rights.

2. Set a user's view and edit permissions for a specific AI application.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a34df2943d1d433f94090a9b1a7f0978~tplv-goo7wpa0wc-image.image) </span>


<span id="401c7044"></span>
# Grant content permissions


1. Click "Project Center" and select "Rights Management \> Manage by Content".

2. Click "Rights Management" in the operation bar of a certain knowledge data name to set up the viewing and editing of the content of a specific knowledge document by a user. If you need to add a user, you can click "Authorize to" to add it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ce164bc0b5c74414b64656f4d08d2542~tplv-goo7wpa0wc-image.image) </span>
