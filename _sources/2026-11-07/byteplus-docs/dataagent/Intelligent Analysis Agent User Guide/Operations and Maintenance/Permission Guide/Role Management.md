---
title: "Role Management"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Role_Management"
---

A role is a collection of permissions. Role\-based authorization can simplify the authorization process and reduce the cost of authorization management. This document introduces the types of roles supported by DataAgent and role authorization operations.

<span id="15b5cc70"></span>
# Role types


| |System & project |Agent |
|---|---|---|
|Role definition | | |
|Preset administrator roles<br><br>(Modification and customization are not supported) |* System administrator:<br><br>   * The default primary account is the system administrator and has all operation permissions, such as system configuration, adding IAM users as DataAgent product users, and so on.<br><br>* Project administrator:<br><br>   * Has project configuration permissions, such as configuring basic project information, adding project members, and granting resource permissions to project members. |* Agent administrator:<br><br>   * On the **Agent configuration** page, perform operations such as creating, configuring, authorizing, publishing, taking offline, and deleting agents. |
|Regular users and user permissions |Project members and permission management:<br><br><br>* Permission requirements: System administrators and project administrators have permission to operate.<br><br>* Permission scope: Add and manage DataAgent product users as project members, and grant permissions to members (for example, grant dataset management permissions, xxxx). After being authorized, project members can access the project list and perform operations such as dataset integration. |Agent members and permission management:<br><br><br>* Permission requirements: Agent administrators have permission to operate.<br><br>* Permission scope: Add and manage members of the intelligent agent, and grant permissions to members. Once authorized, intelligent agent members can access the intelligent agent to perform intelligent analysis (such as data queries, in\-depth research, and more). |
|Permission management recommendations |New users are advised to refer to the process below for permission management: ||


DataAgent role types include admin roles and resource roles.

Admin roles: Admin roles can be directly granted to users, enabling users to have all permissions associated with the admin role. However, admin roles do not support granting additional resource permissions.

Resource roles: Resource roles can first be granted to users, and then the corresponding resource permissions can be assigned to these resource roles. This ensures that users under the same resource role have identical permissions. Subsequent adjustments to the scope of resource permissions or user scope are also supported.

<span id="5c86b9a4"></span>
# Role overview


|Role category |Role name |Permission description |
|---|---|---|
|Management\-type role |System administrator |* Add IAM users and more on the **Access Control** page.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c8847a2b8eaf47d9875b06a0027f42c7~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Manage DataAgent users, office platform integration, office platform account binding, and more on the **System Management** page.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c5d2e419051e45c7bdd1beb9b664bad6~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Configure basic project information, manage project members, and grant permissions for all resources within the project on the **Project Center** page.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b01f99bb0a344586bc9f9950a3cea7a3~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Visit the **Intelligent Agent Configuration** page to create, configure, authorize, publish, deactivate, and delete intelligent agents.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/19d8cfe64e1e4f3abf5d566cb89b768e~tplv-goo7wpa0wc-image.image) </span> |
||Project administrator |* Access the dataset page and the project center page.<br><br>* Configure basic project information, manage project members, and grant permissions for all resources within the project in the project center.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f203543bf0824bd98ad78da99c3759c5~tplv-goo7wpa0wc-image.image) </span> |
||Intelligent agent administrator |* Visit the **Intelligent Agent Configuration** page to create, configure, authorize, publish, deactivate, and delete intelligent agents.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/940b42abe7d5427bb9521f8f29e17c84~tplv-goo7wpa0wc-image.image) </span> |
|Resource\-type role |User group administrator |* Configure resource permissions and members of the user group.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7c68130307f348dc810cdbdb25383b31~tplv-goo7wpa0wc-image.image) </span> |


<span id="4f35629a"></span>
# Role authorization

<span id="a2af4294"></span>
## Admin roles

Admin roles can only be granted to users, and the scope of permissions for the role cannot be adjusted further.

<span id="7a359952"></span>
### System administrator

In most cases, the Volcano Engine **primary account** that activates DataAgent is the account with the highest permissions, serving as the **system administrator** account. Other sub\-account users created by the primary account cannot become system administrators.

<span id="6c796ddc"></span>
### Project administrator

Typically, the user who creates a project is the project administrator. System administrators or project administrators can grant project administrator permissions to other users.


* Authorize by user:

   * New user: On the "Project Center" \- "User Management" page, click "Add User", select the user, and grant "Admin" permissions.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/39c34b599d344c42badff24ca56e0cff~tplv-goo7wpa0wc-image.image) </span>


* Existing user: On the "Project Center" \- "Authorize by User" page, select the user, click "Project", and grant "Admin" permissions.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f78b30288eb4cbab9a375c13c3abadf~tplv-goo7wpa0wc-image.image) </span>


* Authorize by user group: On the "Project Center" \- "User Group Management" page, select the user group, click "Permission Management", and grant "Admin" permissions.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When the project "Management" permission is enabled, other permissions (View, Edit, Global View) are also enabled. However, when the "Management" permission is disabled, the other permissions will not be disabled simultaneously.   </div>
   

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/455071531a24410eb749473e1b1af840~tplv-goo7wpa0wc-image.image) </span>

<span id="b71bcfe5"></span>
### Agent administrator

In most cases, the user who creates the agent is also the agent administrator. System administrators or agent administrators can grant agent administrator permissions to other users.


* Go to the "Agent configuration" \- "Basic information" page, click "Edit", add members in the "Agent administrator" section, and then save.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d84764019a474682b9e0b1ae6a1b3471~tplv-goo7wpa0wc-image.image) </span>

<span id="6fb588be"></span>
## Resource\-type roles

After a resource\-type role is granted to a user, the scope of permissions for the role can also be adjusted.

<span id="70e07e2b"></span>
### User group administrator

User group management refers to the functionality for grouping and maintaining users. System administrators or project administrators are user group administrators.


* Go to the "Project center" \- "User group management" page to manage members (adjust the scope of user groups) or manage permissions (adjust the scope of permissions). For more information about user group administrators, see [User Group Management](https://docs.byteplus.com/docs/dataagent/User_Group_Management).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/230de1726f654c8991db84478abd29a5~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Currently, only "system\-level" user groups are supported. Therefore, to manage user group members, go to Volcano Engine navigation avatar \- Access Control \- User Group to view user group members.</div>
