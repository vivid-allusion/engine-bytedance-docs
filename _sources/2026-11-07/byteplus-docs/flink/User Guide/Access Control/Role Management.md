---
title: "Role Management"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Role_Management"
---

In the BytePlus Flink project, a role represents a set of permission policies and can also be considered a user group with the same role. When authorizing project members, it is done by associating roles.

<span id="14968da5"></span>
## Background Information

The system in the project has predefined roles such as Project_Admin, Project_Dev, Project_OPS, and Project_Member, which are generally suitable for everyday project activities.

If your project requires more finely divided roles, in addition to system roles, you can also add custom roles. Custom roles need to be bound to permission policies, and members associated with the roles can have corresponding permissions.


|**Role** |**Permissions** |
|---|---|
|Project_Admin |Project administrator.<br><br>Primarily responsible for managing project members, roles, strategies, and full permissions for resource pool management. |
|Project_Dev |Project developer.<br><br>Has the necessary permissions for development tasks, such as creating, debugging, and deleting tasks. |
|Project_OPS |Project operations personnel.<br><br>Has the authority to start, stop, and manage tasks online and offline. |
|Project_Member |Ordinary project member.<br><br>Has the authority to only view project resources such as resource pools and tasks. |
|Custom Role |Managed independently by users, with the authority to bind policies. |


<span id="adb930ba"></span>
## Prerequisites

When performing project role\-related operations, please ensure that you have completed the following tasks:


* You must be the project leader or a project administrator (Project_Admin). To add members and associate roles, please refer to [添加项目成员](https://docs.byteplus.com/docs/undefined/655468147c29cc0301edef1f#a45bfca3)。

* If you need to associate a custom permission policy with roles, first create a custom policy, please refer to [创建自定义策略](https://docs.byteplus.com/docs/flink/45783#394a75d4)。

* When associating project members with roles, make sure to add the target users to the project in advance, please refer to [添加项目成员](https://docs.byteplus.com/docs/undefined/655468147c29cc0301edef1f#a45bfca3)。


<span id="221edba3"></span>
## Create a custom role


1. Log in to the [BytePlus Flink](https://console.volcengine.com/flink) console.

2. Select the target region in the top menu bar.

3. In the left navigation bar, select **Project Management**, use the search box to perform a fuzzy search by project name, then click the project block to enter the project.

4. In the project's left navigation bar, select **Access Management**, click on the **Roles** tab, and then click **Create Role**.

5. In the **Create Role** dialog box, set the role name and description statement, then click **Confirm**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e7ffff6b0fa9302c131d00d8b83be169.png) </span>


<span id="e021cf89"></span>
## Associate policies with the role

You can associate policies with roles to ensure that members linked to that role have the necessary permissions.


1. On the **Access Management** page, click the **Roles** tab.

2. In the roles list, click on **Associated Policies** next to a custom role or click on the role name.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c7452b192d2c0e06b20dbfe337c796b9.png) </span>

3. Under the **Associated Policies** tab, click **Add Policy**.

4. In the **Add Policy** dialog, check the target policy and then click **Confirm**.

   You can choose either system preset policies or custom policies. For how to customize a policy, please refer to [创建自定义策略](https://docs.byteplus.com/docs/flink/45783#394a75d4).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dfdd09585d144852b60302fcb5432162~tplv-goo7wpa0wc-image.image) </span>


<span id="f860d964"></span>
## Remove policy from role


1. In the roles list, click on **Associated Policies** next to a custom role or click on the role name.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c7452b192d2c0e06b20dbfe337c796b9.png) </span>

2. Under the **Associated Policies** tab, click on the **Remove** button next to the target policy.

3. In the Remove Policy dialog, click **Delete**.


<span id="8b6571ec"></span>
## Associate members with roles

You can associate members with roles, granting these members the corresponding permissions of the roles.


1. On the **Access Management** page, click the **Roles** tab.

2. In the roles list, click **Associate Members** next to a role or click on the role name.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d4cbc5c2ea4d6f1590184f8da467ef10.png) </span>

3. Under the **Associate Members** tab, click **Add Members**.

4. In the **Add Members** dialog, select members and then click **Confirm**.

   Supports simultaneously checking multiple members, thereby associating all the selected members with the current role, granting them the permissions corresponding to that role.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_925b1bdf176b460fbf883ed4d581a8cc.png) </span>


<span id="a59e64a9"></span>
## Remove associated members from a role


1. In the roles list, click **Associate Members** next to a role or click on the role name.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/13aceddf98a64483a7f4424aa2372b68~tplv-goo7wpa0wc-image.image) </span>

2. In the **Associated Members** tab, click **Remove** next to the target member.

3. In the confirm member removal dialog box, click **Delete**.


<span id="a98a738c"></span>
## Edit Role

You can edit the role to modify its description.


1. In the role list, click the **actions** column for the target role and select Edit from the ... button.``**Edit from the ...**  button.

2. In the **Edit Role** dialog box, modify the role description, then click **Confirm**.


<span id="ce5fd4c0"></span>
## Delete Role

You can delete custom roles; system\-generated roles cannot be deleted.


1. In the role list, click the **actions** column for the target role and select `Delete`.

2. In the delete confirmation dialog box, click **Delete**.
