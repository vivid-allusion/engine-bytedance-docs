---
title: "How to Add a New User?"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/How_to_Add_a_New_User"
---

> "How to add a new user to DataWind?"

> "How to grant a specific user permissions for a particular project?"


Adding users is the first step in permission management and is also one of the most common daily operations for system administrators.

Today, we will discuss the steps for adding users under different permission integration methods.

<span id="_1-如何将用户新增至-datawind-内"></span>
# 1. How to add a user to DataWind?

<span id="_1-1-自有账号体系"></span>
## 1.1 Native account system

For environments managed using DataWind's native account system, system administrators need to enter the user's basic information into the system to complete account creation. The number of users added to DataWind will consume an equivalent number of user License units.

<span id="_1-2-操作示例"></span>
## 1.2 Operation example

**Step 1:**  Click the profile icon in the upper right corner to enter the [Enterprise Domain Management] page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c8adbcfdc9a94246a153b570c02b686d~tplv-goo7wpa0wc-image.image) </span>

**Step 2:**  Click [Add User] or [Batch New] to fill in or upload user information.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e567d5c12cd44f20b8dc337102f9cad1~tplv-goo7wpa0wc-image.image) </span>

**Step 3:**  In the [Add User] window, fill in the username, name, email, and other information, then click Confirm to complete adding the user.

The initial password for a newly added user is the username itself. Upon first login, please follow the system prompts to reset the password.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/87d14d830c9447c4a75fbc4088b43855~tplv-goo7wpa0wc-image.image) </span>

**Step 4**: On the [Batch Import] page, download the template, fill it out completely, and then click Upload.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a5e304db2cb343dc927f72d5ce9efc3a~tplv-goo7wpa0wc-image.image) </span>

Note the following when filling out the template:

(1) Please fill in the users to be imported according to the template format without modifying the template format.

(2) Username, name, and email are required fields. Username, mobile, number, and email must not be duplicated; otherwise, the operation will fail.

The initial password for users added via batch upload is the username itself. Upon first login, please follow the system prompts to reset the password.

<span id="_1-3-集成企业单点登录-sso"></span>
## 1.3 Integrate enterprise single sign\-on SSO

If the enterprise has completed integration between the product and enterprise single sign\-on (SSO) when deploying DataWind, system administrators only need to search for users and add them to the system. The number of users added to DataWind will consume an equivalent number of user License units.

<span id="_1-4-操作示例"></span>
## 1.4 Operation example

**Step 1:**  Click the profile icon in the upper right corner to enter the Enterprise Domain Management page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c8adbcfdc9a94246a153b570c02b686d~tplv-goo7wpa0wc-image.image) </span>

**Step 2:**  On the Enterprise Domain Management page, click [Add user].

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4fe8e2eb44be491499165d3f0835ebce~tplv-goo7wpa0wc-image.image) </span>

**Step 3:**  In the pop\-up Add user window, enter one or more users, then click [Confirm] to complete the addition.

Because integrated enterprise single sign\-on is used for permission control, the username and password for new users are consistent with the enterprise SSO.

<span id="_2-如何为用户授予某项目的特定权限"></span>
# 2. How to grant specific permissions for a project to a user?

To access a project, a user must have view or higher permissions for the project. For details on project permission control, see [A Complete Guide to the of System Permission Framework](https://docs.byteplus.com/docs/DataWind/A_Complete_Guide_to_the_of_System_Permission_Framework).

<span id="_2-1-操作示例"></span>
## 2.1 Operation example

**Step 1:**  Enter the project to be authorized, then click Project Center \- User Management.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e594fd2861c944a7af55e5104871a29a~tplv-goo7wpa0wc-image.image) </span>

**Step 2: Click [Add user], search for the user in the pop\-up window, select the project permissions to grant, and click Confirm to save.** 

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da855cdff57642d7ad5607a629f40d49~tplv-goo7wpa0wc-image.image" width="610px" /></div>


The system defines four types of permissions: view, edit, global view, and manage. Details are as follows.


|**Permission categories** |**View permission** |**Edit permission** |**Global view permission** |**Manage permission** |
|---|---|---|---|---|
|**Application scenarios** |This permission is generally granted to users who view resources. |This permission is generally granted to users who collaboratively edit resources. |This permission is generally granted to project business leaders who do not participate in permission approval. |This permission is generally for resource creators or users granted collaborative management of resources. Caution: You cannot grant others management permissions for personal dashboards. |
|**Project** |Having permission to access and enter the project allows viewing resources within the project for which permission is granted, as well as performing operations such as creating personal dashboards or folders. |In addition to project viewing permissions, operations such as creating public dashboards, datasets, or folders can also be performed in the root directory of the public directory. |Having permission to view all public dashboards, public dashboard folders, and datasets within the project allows viewing all data. |Having management permissions for resources within the project allows performing permission management, project deletion, and other operations, representing the highest level of resource permissions. |


Caution: When directly granting dashboard or dataset permissions within a project to a user, the user will be added to the system and granted view permissions for the project as well as the corresponding dashboard or dataset permissions. There is no need to add them step by step from System \- Project.

In summary, you have successfully added the user to the project. Go ahead and contact them to visit DataWind and start their data exploration journey!
