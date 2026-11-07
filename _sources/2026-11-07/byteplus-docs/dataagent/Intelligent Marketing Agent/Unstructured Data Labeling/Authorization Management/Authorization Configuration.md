---
title: "Authorization Configuration"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Authorization_Configuration"
---

This article provides you with a detailed introduction to the permissions configuration methods for each project, module, resource, and data.

<span id="15b90519"></span>
# Prerequisite

Before configuring permissions, identify the administrator and create projects, role accounts, roles, etc. in the Volcano Engine console. Operational documentation reference: [Identity Configuration](https://www.volcengine.com/docs/6257/64959).

According to the division logic of the group and the project, determine the group and the project administrator. The group administrator has the authority of all the projects under the group by default, and the project administrator needs the project creator to manually grant "project management permission spot".

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The group administrator of a single group is admin, and other people are not supported. Administrators of multiple groups can flexibly set up multiple people.</div>



* **Privatization:**  When the privatization environment is deployed, the Volcano Engine operation and maintenance personnel will provide the login link of the privatization environment and the administrator account password to the administrator. You need to record the relevant information and log in to the privatization environment with the administrator account.

* **SaaS version**

   1. Enter the Volcano Engine console.

   2. Select Management Center.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/179e07e8ff99484f85b19604ecfdc5d1~tplv-goo7wpa0wc-image.image) </span>

   3. Click the Modify button of the group administrator to set the group administrator.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/38e5270a9d254956bad7db06fc91fe98~tplv-goo7wpa0wc-image.image) </span>


<span id="038a35a1"></span>
# Add User

<span id="b3a547e8"></span>
## Privatized version


1. Create a new system user.

   1. The administrator clicks on the avatar in the upper right corner and selects "System Configuration".

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b1b1ee6210d243f0841a70221836abce~tplv-goo7wpa0wc-image.image) </span>

   2. Enter the system configuration page, select "Account Management", click "New Account" \- "Manually New" or "Batch Import", and fill in the basic information of the account. Click "OK".

2. Add a user. On the Enterprise Knowledge Engine page, select "Project Center", click "Rights Management" \- "Manage by User", and click "Add User".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca11ebf624d04df29fd5737850fbb384~tplv-goo7wpa0wc-image.image) </span>


<span id="0ced87f6"></span>
## SaaS version


1. Create a new system user.

   1. The administrator clicks on the avatar in the upper right corner and selects "Access Control" **.** 

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b8b5cad9e70b4ccc98ccd51d58231ed6~tplv-goo7wpa0wc-image.image) </span>

   2. Enter "User Management \> User", click "New User", fill in the user information and permission configuration to complete the creation, please refer to [User Management ](https://www.volcengine.com/docs/6257/64977)for specific operations.

      This article takes "Creating by Username" as an example, and the operation is as follows:

      1. Select "Create by username".

      2. Fill in the user's basic information.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">"Username" (must be English letters, cannot be entered in Chinese), such as test.         </div>
         

      3. Check "Programming Access \- Allow users to manage their own API keys" in the access method, and the system will automatically assign AK to the user; you can also check "Console Access"  **,**  select "Custom Generated Password" when accessing the password  **,**  and check "No need to reset the password" when resetting the password, click "Next".

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/49247d8d9afe43c4a45314c5c86acf3c~tplv-goo7wpa0wc-image.image) </span>

      4. On the Permissions Configuration page, after completing the required permissions check, click **Next**.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f66adcce0404516b14546142a4ecfd8~tplv-goo7wpa0wc-image.image) </span>

         Account types and permissions are described as follows:

         
         |**role** |**scope of authority** |
         |---|---|
         |Administrator (admin) |All resources under the group access + permission allocation permission |
         |normal user |Users who have been granted editing rights to Enterprise Knowledge Engine and AI applications |
         

      5. On the review page, check whether the configuration item created by the user is accurate. If it is inaccurate, you can return to the previous step to modify it. After confirming that it is correct, click "Next" and enter the verification code to complete the creation of the IAM sub\-account.

2. Add a user. On the Customer Data Platform page, select "Project Center", click "Rights Management" \- "Manage by User", and click "Add User".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8bfd7c13985f4f5c9b4372df0881f509~tplv-goo7wpa0wc-image.image) </span>


<span id="6e204a25"></span>
# Determine the Authorized Object

On the Customer Data Platform page, select **Project Center \- Permissions \- Manage by User** to enable or disable View and Manage permissions for users or user groups.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/074815d7658743ceb6c5ba7326429093~tplv-goo7wpa0wc-image.image) </span>

It is not recommended to authorize individual users one by one, which is inefficient and costly to maintain. It is recommended that:


1. If the authority system is to be connected to the organizational structure, it is recommended to use the organizational structure as the main authorization object, supplemented by user groups that can make some flexible changes.

2. If the permission system does not connect with the organizational structure, it is recommended to use "roles" or "user groups" as the main authorization object.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">"Roles": Roles are group\-granular and cross\-project. Once a role is created, it will be visible in the various projects under the group, and each project does not need to be created repeatedly. If the roles of each project are consistent, and there are roles for data development, operations, marketing, etc., the concept of "roles" is suitable.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">"User groups": A user group is project\-granular, and a user group created is only available within that project. If you only need to use it at the granularity of the project, such as a project data development group A, operation group B, etc., the concept of "user group" is suitable.   </div>
   

<span id="d7689d94"></span>
# Grant Feature Module Permissions

Permissions support function module according to the content or granted by the user. For the specific operation method, see [by user management ](https://www.volcengine.com/docs/6356/1154925), [by content management](https://www.volcengine.com/docs/6356/1154926#_3-2-%E6%A8%A1%E5%9D%97%E6%8E%88%E6%9D%83%EF%BC%88%E4%BA%A7%E5%93%81%E6%A8%A1%E5%9D%97%EF%BC%89).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b13542c1bb641a2817855d582b15f33~tplv-goo7wpa0wc-image.image) </span>

<span id="bed25d61"></span>
# Grant Resource Permission

Batch grant resource permissions for visual modeling tasks, datasets, labels, clusters, etc. for departments/roles/user groups. The resource supports global authorization, and can grant all label, grouping, and insight report viewing, editing, and management permissions to corresponding objects. The permission of the resource module supports granting according to the content or the user. For specific operation methods, please refer to [management by user ](https://www.volcengine.com/docs/6356/1154925)and [management by content](https://www.volcengine.com/docs/6356/1154926#_3-2-%E6%A8%A1%E5%9D%97%E6%8E%88%E6%9D%83%EF%BC%88%E4%BA%A7%E5%93%81%E6%A8%A1%E5%9D%97%EF%BC%89).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d1ec33638504aa28e835867e7a90eff~tplv-goo7wpa0wc-image.image) </span>

<span id="00d5717b"></span>
# Grant Data Rule Permissions

At present, only "tags" are supported for line permission control. For example, user A can only view users of "source channel = WeChat" on this platform, and user B can only view users of "source channel = Douyin" on this platform. For details, please refer to the document [Data authorization](https://www.volcengine.com/docs/6356/1154926#_3-4-%E6%95%B0%E6%8D%AE%E6%8E%88%E6%9D%83).

**For example** , the bank has built a customer label system, which can view the labels and label values of each customer. However, the customers managed by each account manager in a bank are different. Each account manager can only view the label value of his own customers, so he needs to perform line\-level authority control on customers.

Solution (dynamic row\-level permissions):


1. A new column of labels has been processed, called "Customer Manager".


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/63beb3e0e6d94167a89bee2ed8b2a435~tplv-goo7wpa0wc-image.image" width="650px" /></div>



2. In "User Management" (the account manager is the logged\-in user of the platform), there is a column in the user attributes column that can be the same as the value of the above "Affiliated Account Manager", if not, you can add a column through the "Extended User Identity" function.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cb2fa1f5d9c748b994c3f8e858c4cfd1~tplv-goo7wpa0wc-image.image" width="650px" /></div>



3. Configure "Dynamic Row Level Permissions" in Row Level Permissions

   Rules: Label (account manager) = user name **or** label (sales department) = sales department to which the account manager belongs.

   When querying later, the SQL statement will dynamically replace the user name according to the current logged in user to achieve data permission control.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/717a4ba511cf4ebbbd826f2966f37c2e~tplv-goo7wpa0wc-image.image) </span>
