---
title: "Member Management"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Member_Management"
---

Project members are generally managed by the project leader or the project administrator (Project_Admin), supporting the addition of multiple project members and associating relevant roles. Once members are associated with a role, they will have the permissions of that role.

<span id="a970e8e1"></span>
## Prerequisites

When adding members and associating roles in a project, please complete the following work in advance:


* The users to be added must be sub\-users created by the master account on the access control platform (IAM user), and must be granted `FlinkFullAccess` permission. For related documentation, please see [Creating Users and Granting Permissions](https://www.volcengine.com/docs/6257/94013).

* When managing members in a project, you must be the project leader or the project administrator (Project_Admin).

* If the role associated with project members is a custom role, it is necessary to first create a custom role and bind related permission policies, please see [项目角色管理](https://docs.byteplus.com/docs/flink/45786).


<span id="a45bfca3"></span>
## Add project members


1. Log in to [BytePlus Flink console](https://console.volcengine.com/flink).

2. Select the target region from the top menu bar.

3. In the left navigation bar, select **Project Management**, perform a fuzzy search in the search box based on the project name, and then click on the project block to enter the project.

4. In the project’s left navigation bar, select **Access Management**, click on the **Members** tab, and then click on **Add Members**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Users who need to be added must be sub\-users created by the main account on the access control platform and must be granted <code>FlinkFullAccess</code> rights. For related documentation, please see <a href="https://www.volcengine.com/docs/6257/94013">create users and authorize</a>.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/213c6bd78d984b64bf8493cdd6719422~tplv-goo7wpa0wc-image.image) </span>

5. In the **Add Members** dialog, enter the IAM user name keywords to perform a fuzzy search, select a member and set the associated role, then click **Confirm**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7d47b8a793cd40c0b02d8d1bee5db258~tplv-goo7wpa0wc-image.image) </span>

   
   |**Configuration** |**Description** |
   |---|---|
   |Member Name |Enter the IAM user name for fuzzy search to add users as project members. |
   |Role |Select the role to be associated with project members from the dropdown list to have the permissions of that role.<br><br>The project has four preset roles: Project_Admin, Project_Dev, Project_OPS, and Project_Member, which can be directly chosen for association; if the existing roles do not meet the requirements, you can choose to create a custom role and bind related permission policies, see [角色管理](https://docs.byteplus.com/docs/flink/45786).<br><br><br>* Project_Admin: Project Administrator. Mainly responsible for managing project members, roles, policies, and all permissions related to resource pool management.<br><br>* Project_Dev: Task Developer. Possess the necessary permissions for development tasks, such as creation, debugging, and deletion of tasks.<br><br>* Project_OPS: Task operation personnel. Possess permissions to start, stop, and manage the online status of tasks.<br><br>* Project_Member: Regular project user. Only has permission to view tasks, resource pools, and other project resources. |
   |Description |Fill in the descriptive language for project members. |
   


<span id="b2174503"></span>
## Associate roles with members


1. In the member list, click on the **Operation** column's **Associate Role**, or click on the member’s name.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4145d5e772db4b07ba38700dda62a9cf~tplv-goo7wpa0wc-image.image) </span>

2. In the **Associate Role** panel, click **Add Role**.

3. In the **Add Role** dialog, check the target role, then click **Confirm**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fca08e918c4c7fa946d8f67ee7803392.png) </span>


<span id="cd477007"></span>
## Remove associated roles for members


1. In the member list, click **Actions** in the **Associated Roles** column or click the member name.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4145d5e772db4b07ba38700dda62a9cf~tplv-goo7wpa0wc-image.image) </span>

2. In the **Associated Roles** panel, click **Remove** next to the target role.

3. In the confirm removal of associated roles dialog, click **Delete**.


<span id="e9b77d70"></span>
## Associate policies for members


1. In the member list, click **Actions** in the **Associated Policies** column or click the member name.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac4915b00d21489bba1efc19cb893503~tplv-goo7wpa0wc-image.image) </span>

2. In the **Associated Policies** tab, click **Add Policy**.

3. In the **Add Policy** dialog, check the target policy, then click **Confirm**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dfdd09585d144852b60302fcb5432162~tplv-goo7wpa0wc-image.image) </span>


<span id="a50ceef8"></span>
## Remove policies for members


1. In the member list, click **Actions** in the **Associated Policies** column or click the member name.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac4915b00d21489bba1efc19cb893503~tplv-goo7wpa0wc-image.image) </span>

2. In the **Associated Strategy** tab, click **Remove** behind the target strategy.

3. In the confirm strategy removal dialog, click **Delete**.


<span id="b1900d5b"></span>
## Set project manager

The project manager is appointed by the main account when creating the project, and can transfer management rights to other project members. Once set, the member will have all the permissions of the project, please proceed with caution.


1. On the **Access Management** page, click the **Members** tab.

2. In the member list, filter the target member by name, then click on the **Operation** column `...` icon and select **Set as Project Manager**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/97d184a7eed74092ae7a0db22be1e9f1~tplv-goo7wpa0wc-image.image) </span>

3. In the confirm manager transfer dialog, click **Confirm**.


<span id="e61ad72e"></span>
## Edit project members


1. On the **Access Management** page, click the **Members** tab.

2. In the member list, filter for the target member by their name, then click on the **operation** column's `...` icon and select **edit**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/69c8185cba7c4c6eaef87a5413d03e1a~tplv-goo7wpa0wc-image.image) </span>

3. In the **edit member** dialog, you can add or remove associated roles, modify the member's description, and click **confirm** after editing.


<span id="317d38e7"></span>
## Remove a project member

If a member no longer needs to be in the project, they should be removed promptly. Removed members will not be able to perform any operations in the project, so please proceed with caution.


1. On the **access management** page, click on the **members** tab.

2. In the member list, filter for the target member by their name, then click on the **operation** column's `...` icon and select **edit**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f156abf00bf40b39fd32a0b7364f949~tplv-goo7wpa0wc-image.image) </span>

3. In the confirmation dialog for removing a member, click **confirm**.
