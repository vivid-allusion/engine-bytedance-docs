---
title: "Permission Management"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Authorization_Management"
---

The permission management function of the intelligent marketing Agent console is a management tool for fine allocation of one customer, one policy engine, marketing interactive assistant and other related modules and resource operation permission. This function can help administrators efficiently configure permissions in batches, avoid unauthorized operations, and ensure the security and control of marketing data and resources. It is suitable for typical scenarios such as multi\-department marketing team collaboration and permission isolation of personnel at different levels. This article introduces the specific operation process of configuring permissions by user and by content.

# Manage permissions by user

Per\-user management refers to user\-centric authorization of specific content resource permissions for each user object(user, user group, role).

## Add user

1. Log in to the Smart Marketing Agent console and select **Project Center** \> **Permission Management** in the left navigation bar.

2. On the **Permission Management** page, select **Manage by User** \> **Users** and click **Add User**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dfe29865bb1e44ed87b405ace447c06e~tplv-goo7wpa0wc-image.image)

3. In the add box that pops up, enter the username you want to add to select and grant specific project permissions (view/manage). If the user is not found, please click **New User** to enter the management center to create a new user.

   > **说明**

   > It should be noted that adding users to the user management of the project center is essentially adding the IAM sub\-users you added to the BytePlus access control and binding their permissions.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6626ee4cddab4ed9a26487bf7177e462~tplv-goo7wpa0wc-image.image)

4. At the bottom of the **Users** tab, click **Manage All Users** to search and view all users under this item, add new users and manage them.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d9fe863f5443422bb96aa148a4f6156a~tplv-goo7wpa0wc-image.image)

## Add user group

1. Log in to the Intelligent Marketing Agent console and select **Project Center** \> **Permission Management** in the left navigation bar.

2. On the **Permission Management** page, select **Manage by User** \> **User Groups** and click **Add User Group**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/94a41706c1bf4bc59e2d7adc7936a398~tplv-goo7wpa0wc-image.image)

3. In the **New User Group** pop\-up window, fill in the **user group name**, **description,**  and click **OK**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/168193d776594d93bb31ef1f11c483dd~tplv-goo7wpa0wc-image.image)

4. Click the **Edit** button containing the user and select Add the user to the group.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2777f0695a54894bbb10cfb7f41403c~tplv-goo7wpa0wc-image.image)

## Add role

1. Log in to the Smart Marketing Agent console and select **Project Center** \> **Permission Management** in the left navigation bar.

2. On the **Permission Management** page, select **Manage by User** \> **Roles** and click **Add Role**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f4661294c34a4b0ea5587474a12d3c00~tplv-goo7wpa0wc-image.image)

3. On the **New Role** page, complete the following configuration and click **Create**.

   1. Fill in **basic information** , including name, description, and role owner.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d7a6aca22bea4b47ac9601c43829a5a7~tplv-goo7wpa0wc-image.image)

   2. Fill in the **permission settings** and select the projects and products for which the current role is open.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9cb5c2ba9d8b424d8b81e757461ac57a~tplv-goo7wpa0wc-image.image)

   3. Configure **role members** , including member maintainers and member scopes.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/462d46e0c1c04873857d6e548861bfeb~tplv-goo7wpa0wc-image.image)

## Authorize users/user groups/roles

When authorizing, the administrator needs to specify the type and object of authorized users, and then select the specific authorization content to perform authorization operations to ensure the controllability of their usage permission.

![](data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI1MDZweCIgaGVpZ2h0PSI2NnB4IiB2aWV3Qm94PSItMC41IC0wLjUgNTA2IDY2Ij48ZGVmcy8+PGc+PHBhdGggZD0iTSAxNDMgMzMgTCAxNzQuNzYgMzMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzY2NjZmZiIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDE4MC43NiAzMyBMIDE3Mi43NiAzNyBMIDE3NC43NiAzMyBMIDE3Mi43NiAyOSBaIiBmaWxsPSIjNjY2NmZmIiBzdHJva2U9IiM2NjY2ZmYiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMyIgeT0iMyIgd2lkdGg9IjE0MCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjY2NjY2ZmIiBzdHJva2U9IiM2NjY2ZmYiIHN0cm9rZS13aWR0aD0iMiIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMzcHg7IG1hcmdpbi1sZWZ0OiA0cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTRweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlNwZWNpZnkgdXNlciB0eXBlKHVzZXIsIHVzZXIgZ3JvdXApPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDMyMyAzMyBMIDM1NC43NiAzMyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjNjY2NmZmIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMzYwLjc2IDMzIEwgMzUyLjc2IDM3IEwgMzU0Ljc2IDMzIEwgMzUyLjc2IDI5IFoiIGZpbGw9IiM2NjY2ZmYiIHN0cm9rZT0iIzY2NjZmZiIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIxODMiIHk9IjMiIHdpZHRoPSIxNDAiIGhlaWdodD0iNjAiIHJ4PSI5IiByeT0iOSIgZmlsbD0iI2NjY2NmZiIgc3Ryb2tlPSIjNjY2NmZmIiBzdHJva2Utd2lkdGg9IjIiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzM3B4OyBtYXJnaW4tbGVmdDogMTg0cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTRweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlNwZWNpZnkgdXNlciBvYmplY3Q8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjM2MyIgeT0iMyIgd2lkdGg9IjE0MCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjY2NjY2ZmIiBzdHJva2U9IiM2NjY2ZmYiIHN0cm9rZS13aWR0aD0iMiIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMzcHg7IG1hcmdpbi1sZWZ0OiAzNjRweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxNHB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+U3BlY2lmeSBhdXRob3JpemF0aW9uIGNvbnRlbnQ8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjwvZz48L3N2Zz4=)

> **说明**

> If a user is simultaneously granted different types of permissions for a user/user group/role/department, the user's permissions are a combination of those types of permissions.

Click on a user/user group/role, select the specific authorized content category, and support the selected authorized content: projects, modules, and resources.

* Manage project permissions: Set project permissions for specified users, user groups, and roles, including view permissions and administrative permissions.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d325c53c51a54234a1421c83b60e7931~tplv-goo7wpa0wc-image.image)

* Management module permissions: Set a customer\-policy engine for designated users, user groups, and roles, and the permissions of each module in the marketing interaction assistant, including viewing permissions, editing permissions, and management permissions.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d88b264190c41beb9fe0420f24557ed~tplv-goo7wpa0wc-image.image)

* Manage resource permissions: Set resource permissions such as memory, profile assistant, and query tool for designated users, user groups, and roles, including viewing permissions, editing permissions, and administrative permissions.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/731b1c23b4e641b6b1f0e78c2a51f545~tplv-goo7wpa0wc-image.image)

# Manage permissions by content

Content\-based management refers to content\-centric, assigning specific users/user groups/roles to each content object(project, module, resource).

## Project authorization

Project\-centric, manage project view permission and administrative permission for designated users, user groups, and roles.

1. Log in to the Smart Marketing Agent console and select **Project Center** \> **Permission Management** in the left navigation bar.

2. On the **Permission Management** page, select **Manage by Content** \> **Projects**.

   The following two authorization methods are supported:

   |**Authorization method** |**Operating instructions** |
   |---|---|
   |Batch authorization |1. Click **Permission Management** in the **Actions** column for the specified project.<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c7de89131e5748bfbf8bededce9e517e~tplv-goo7wpa0wc-image.image)<br><br>2. In the pop\-up interface on the right, click **Authorize to**.<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9edffef8e3154e5499d1fda9a157c4af~tplv-goo7wpa0wc-image.image)<br><br>3. Select the Authorization Object Type and Object, and then click **Save**.<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7c350c6a46aa4b938ec4319f15005145~tplv-goo7wpa0wc-image.image) |
   |Single authorization |In the list of users, user groups, and roles, you can grant view or administrative permissions to the specified object.<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e9f030260d234638a85a96424559a115~tplv-goo7wpa0wc-image.image) |

## Module authorization

Module authorization is centered on functional modules, and specific permissions can be authorized.

1. Log in to the Smart Marketing Agent console and select **Project Center** \> **Permission Management** in the left navigation bar.

2. On the **Permission Management** page, select **Manage by Content** \> **Modules**.

   The following two authorization methods are supported:

   |**Authorization method** |**Operating instructions** |
   |---|---|
   |Batch authorization |1. In the upper right corner of the **Modules** tab, click **Batch Authorization**.<br><br>2. In the **Batch Authorization** interface, select the modules and permissions that need to be authorized (support all selection).<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c96f791d16484d62b051532ff578346f~tplv-goo7wpa0wc-image.image)<br><br>3. Select the Authorization Object Type and Object, and then click **Save**.<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88a34ff3affa428cb08669cde6ac373e~tplv-goo7wpa0wc-image.image) |
   |Single authorization |1. In the module list, hover the mouse to the right of the permission column corresponding to the target module and click the **Settings** icon.<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/418fe9ea60a949cb9991d5912209de57~tplv-goo7wpa0wc-image.image)<br><br>2. (Optional) Click **Authorize to** in the upper right corner of the page, and specify the authorization object in batches for authorization.<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6cad42af34084b2da7332f8e0d5d0919~tplv-goo7wpa0wc-image.image)<br><br>3. (Optional) Authorize the specified user, user group, or role.<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fd819d70e329462aa23a1b3f66109194~tplv-goo7wpa0wc-image.image) |

## Resource authorization

Resource authorization is data\-centric and can authorize specific agents, intents, memory banks, profiling assistants, or profiling tasks.

> **说明**

> The user who creates a resource is the default owner of that resource.

1. Log in to the Smart Marketing Agent console and select **Project Center** \> **Permission Management** in the left navigation bar.

2. On the **Permission Management** page, select **Manage by Content** \> **Resources**, and in the **Type** drop\-down list, select Specify Resource Type.

   You can also search by entering the resource name directly in the search box.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c426ca3c5d494d7e82064d79915616b5~tplv-goo7wpa0wc-image.image)

3. In the **Actions** column for the specified resource, click **Permission Management**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99a36180ac9c423d9bf45a52b42ef4a6~tplv-goo7wpa0wc-image.image)

4. On the resource details page, authorize the user in one of the following ways.

   |**Authorization method** |**Operating instructions** |
   |---|---|
   |Batch authorization |1. In the pop\-up interface on the right, click **Authorize to**.<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f37bc7e3f5d94956ba11775d5a507903~tplv-goo7wpa0wc-image.image)<br><br>2. Select the Authorization Object Type and Object, and then click **Save**.<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/60c6144f1afe4076af9af278c5598034~tplv-goo7wpa0wc-image.image) |
   |Single authorization |In the list of users, user groups, and roles, you can grant view or administrative permissions to the specified object.<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cfde59c10a874bd49f9df184f2309036~tplv-goo7wpa0wc-image.image) |
