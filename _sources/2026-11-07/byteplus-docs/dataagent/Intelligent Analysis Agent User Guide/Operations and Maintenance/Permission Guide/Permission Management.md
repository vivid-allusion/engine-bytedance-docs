---
title: "Permission Management"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Permission_Management"
---

Data Agent provides users with flexible permission management capabilities. Combined with the BytePlus access control (IAM) product, it enables permission management for users at both the system and product levels. This article introduces the permission management capabilities of Data Agent.

<span id="aafd921f"></span>
# Permission management overview

Typically, the BytePlus **primary account** that activates Data Agent serves as the **system administrator** account with the highest permissions. The system administrator can create multiple IAM sub\-accounts based on the team's business needs, add them as Data Agent users, and grant more granular Data Agent resource permissions (including project resource permissions and agent permissions) through Data Agent's permission management.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6d0ded02c72a4615bb45c8af0a29961f~tplv-goo7wpa0wc-image.image) </span>

<span id="0ecf885a"></span>
## Permission management granularity

Data Agent includes product\-level management, project resource permission management, and agent permission management. The scope of each level of permission management is described as follows.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Agents and projects are independent of each other. When granting permissions, users must be assigned both project\-related permissions and agent\-related permissions separately.</div>


<div data-tips="true" data-tips-type="warning">For example, to configure datasets sourced from multiple projects for an agent, a user must obtain agent management permissions and viewing permissions for multiple datasets separately.</div>



|Permission management granularity |Permission scope description |
|---|---|
|Product\-level control |* Used to control whether a user has permission to access the Data Agent product interface. Only Data Agent product members can access the product page; non\-product members do not have permission to access. |
|Project resource permission management |* Used to control whether a user has permission for a specific project or resources within a project in Data Agent.<br><br>* Project resource permissions can be further divided into datasets, visual modeling, and data connection resources within a project. Resource operation permissions can be categorized as view, edit, manage, and more.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In addition, for data permissions within project resources, Data Agent provides a more fine\-grained row and column permission control mechanism to fully ensure the security of user data and the compliance of data operations. For details, see <a href="https://docs.byteplus.com/docs/dataagent/Permission_Management#7e46920b">Practical scenarios: Fine\-grained data permission control</a>.   </div><br>    |
|Agent permission management |* Used to control whether a user has permission to use (such as querying, in\-depth research, and more) or manage (such as creating and configuring agents) agents. |


<span id="fd8395a9"></span>
## Key points for user authorization

When Data Agent assigns user permissions for products, projects, and agents, users can be categorized as administrators and regular users.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/54ee5bdeb0b64075b966c71bb3ef0952~tplv-goo7wpa0wc-image.image" width="520px" /></div>



|User categories |System and product |Project |Agent |
|---|---|---|---|
|Administrators |System administrator:<br><br>The default primary account is the system administrator and has all permissions for the product. For example, performing system configuration, adding IAM users as Data Agent product users, managing all project\-related permissions, and managing all agent\-related permissions. |Project administrator:<br><br>Has all permissions related to the project, such as configuring basic project information, adding project members, and granting resource permissions to project members. |Agent administrator:<br><br>Has all permissions related to the agent, such as creating, configuring, authorizing, publishing, deactivating, and deleting agents. |
|Regular users |System members and product members:<br><br><br>* Permission requirements: System administrators have permissions related to managing system members and product members.<br><br>* Permission management: By default, sub\-accounts are system members. They must be added as Data Agent members by the system administrator before becoming product members. Only after becoming product members can they be added as project members and agent members.<br><br>* Permission scope: System members and product members do not yet have project or agent\-related permissions. |Project members:<br><br><br>* Permission requirements: System administrators and project administrators have permissions related to managing project members.<br><br>* Permission management: Product members can be authorized as project members and granted permissions related to project resources (datasets, data connections, visual modeling).<br><br>* Permission scope: Once authorized, project members can access the project list and perform corresponding view, edit, and manage operations on project resources. |Agent members:<br><br><br>* Permission requirements: System administrators and agent administrators have permissions related to agent member management.<br><br>* Permission management: Product members can be authorized as agent members and granted permissions related to agent usage.<br><br>* Permission scope: Once authorized, agent members can access the agent usage interface and conduct intelligent analysis (such as data queries, in\-depth research, and more). |


<span id="109548c6"></span>
## Viewing permission details

Users can view permission details, obtain permission\-related information, and determine whether permissions are effective.


* Project\-related permissions can be viewed on the "Project Center" \- "User Authorization" page.

* Agent\-related permissions can be viewed on the "Agent Configuration" \- "Basic Information" page.


<span id="5ca6032a"></span>
# Permission management practices

<span id="2d4bf1c4"></span>
## General authorization operations

<span id="2fae946f"></span>
### Authorization methods

Data Agent provides users with multiple authorization methods for different resources:


* Project resource authorization methods

   * [User Management](https://docs.byteplus.com/docs/dataagent/User_Management): Add a single user and grant initial permissions to the user.

   * [User-Based Authorization](https://docs.byteplus.com/docs/dataagent/User-Based_Authorization): Suitable for single\-point authorization for individual users.

   * [User Group Management](https://docs.byteplus.com/docs/dataagent/User_Group_Management): Suitable for granting the same operational permissions to multiple users.

   * [Resource-Based Authorization](https://docs.byteplus.com/docs/dataagent/Resource-Based_Authorization): Suitable for authorizing users or user groups based on resources.

* Agent resource authorization methods

   * [Agent permissions](https://docs.byteplus.com/docs/dataagent/Detailed_Explanation_of_User_Permissions#4efb3f5c): Suitable for adding administrators or members to an agent.


<span id="1b094d0f"></span>
### Authorization operations

For detailed permission information and authorization steps for each resource, see [Detailed Explanation of User Permissions](https://docs.byteplus.com/docs/dataagent/Detailed_Explanation_of_User_Permissions).

<span id="c9141fef"></span>
## Practical scenarios: Authorization link recommendations


* Link 1: Grant users operational permissions on the target object


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e648a4efe334872b2a7a777f9120aeb~tplv-goo7wpa0wc-image.image" width="767px" /></div>



1. Create IAM sub\-accounts. The system administrator (primary account) logs in to BytePlus and creates a sub\-account on the [IAM Access Control page](https://console.volcengine.com/iam/identitymanage/user), which is a BytePlus system user. When creating a sub\-account, the DataAgentFullAccess permission must be granted to the sub\-user in the permission settings. For details, see [User Management](https://docs.byteplus.com/docs/dataagent/User_Management).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ae6ec91265d429580c4dbe0c8bbeea8~tplv-goo7wpa0wc-image.image) </span>

```Plain Text
  :::warning
  After the system administrator creates a sub-account, there is no need to authorize the sub-account on the IAM access control page.
  :::
```



2. Add the system user to the Data Agent product. The system administrator (primary account) goes to the Data Agent "System Management" \- "User Management" page, searches for the IAM sub\-account (system user), and adds it as a Data Agent product user.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe29148fe2c149d9a4c6f15659e68517~tplv-goo7wpa0wc-image.image) </span>


3. Grant project and agent\-related permissions. The project administrator grants project resource\-related permissions (project, dataset, visual modeling, data connection) to the product user, and the agent administrator grants agent resource\-related permissions (agent only) to the product user.

   * To quickly use an agent, the user must at least have both agent usage permission and view permission for the dataset configured for that agent (this is the minimum permission requirement). For specific instructions, see the details.

   * To view, edit, or manage a project or datasets, visual modeling, data connections within a project, or to perform advanced operations such as configuring an agent, the user must have the corresponding project and agent permissions. For specific instructions, see [Detailed Explanation of User Permissions](https://docs.byteplus.com/docs/dataagent/Detailed_Explanation_of_User_Permissions).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/78edbc90f2384769a55dfe9c7fee1ecd~tplv-goo7wpa0wc-image.image) </span>


* Link 2: When authorizing project resource objects, use user groups to batch authorize users.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc96fd18a4154bfdbc963d09bde34e75~tplv-goo7wpa0wc-image.image" width="753px" />   </div>
   

   1. Create a user group. The system administrator creates a user group on the [IAM Access Control page](https://console.volcengine.com/iam/identitymanage/user), which is a system\-level user group. For details, see [User management](https://www.volcengine.com/docs/6257/64977).

   2. Add users to the user group. The system administrator adds users to the user group on the [IAM Access Control page](https://console.volcengine.com/iam/identitymanage/user).

   3. Associate the user group. The project administrator creates a new user group in the product by associating a system\-level user group in the "User Group List" on the "Project Center" \- "User Group Management" page.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Here, <strong>project administrators</strong> can only create user groups in Data Agent by associating system\-level user groups. System\-level user groups are user groups set in <a href="https://console.volcengine.com/iam/identitymanage/user">BytePlus access control</a>.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">To adjust system\-level user group members, <strong>system administrators</strong> must add or remove users on the <a href="https://console.volcengine.com/iam/identitymanage/user">IAM access control page</a>.      </div>
      

   4. Authorize the user group. Project administrators grant project or dataset permissions to user groups in the "Project Center" \- "User Group Management" page under "Permission Management". For details, refer to [User Group Management](https://docs.byteplus.com/docs/dataagent/User_Group_Management).


<span id="7e46920b"></span>
## Practical scenarios: Fine\-grained data permission control

In addition, for data permissions in Data Agent datasets, the product also provides a more granular control method—row and column permission control, which allows you to manage user viewing permissions for specific rows or columns in a dataset. For details, refer to [Row and column permissions](https://docs.byteplus.com/docs/dataagent/Detailed_Explanation_of_User_Permissions#f3ed5cd6).


|**Comparison dimensions** |**Asset permissions** |**Data permissions** |
|---|---|---|
|**Core objects** |Assets such as projects, datasets, visual modeling, data connections, agents, and other assets |Specific rows or columns of a dataset |
|**Permission scope** |Operations such as creating, viewing, editing, and managing assets (for example, creating a project, editing a dataset, managing an agent) |Viewing restrictions for data rows or columns, such as being able to view only data rows of a certain department or specific field columns |
|**Key role** |Controls operational permissions for assets and determines whether resources can be used or managed |Controls the visible scope of data content and restricts access to specific data rows or columns |
|**Acquisition method** |Authorization is granted by the corresponding asset administrator; after authorization, users can obtain the corresponding asset permissions. |Project administrators or users with dataset management permissions configure row and column permissions on the dataset management page.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/97a7be923ce34d4bb3a20411b5a033bb~tplv-goo7wpa0wc-image.image) </span> |
|**Dependency relationship** |* When a user has dataset viewing permissions, if row and column permissions for the dataset are not enabled, the user can view all data.<br><br>* When a user has dataset viewing permissions, if row and column permissions for the dataset are enabled, the data content the user can view is restricted by row and column permissions, and the user may also need to apply for row and column permissions. |* When row and column permission restrictions are enabled for a dataset, having dataset permissions does not necessarily mean the user can view the data; row and column permissions must also be applied for.<br><br>* Even if row and column permissions are granted, to access the visual modeling page for free analysis, dataset permissions must also be applied for. |


In real business scenarios, data permissions (referring to row and column permissions) play a crucial role. They precisely define the boundaries of user access to data content, ensuring that data is used appropriately under secure and controllable conditions. The specific scenario\-based functions are as follows:


* Enterprise department collaboration: For datasets associated with the Sales department's agent, row permissions restrict Sales representatives to viewing only sales data rows for their assigned regions or customers, while column permissions grant access only to relevant columns such as sales amount and hide sensitive financial columns such as cost, ensuring compliant data usage.

* Financial risk control: For customer information datasets of banking agents, row permissions allow loan officers to view only application data rows for their assigned customers, while column permissions grant ordinary loan officers access only to basic information columns. Sensitive columns such as asset details are restricted to senior risk control personnel, ensuring data security.

* Medical data applications: For medical record datasets of hospital agents, row permissions are divided by department, so doctors can view only medical record rows for patients in their own department. Sensitive columns such as genetic test results are accessible only to specific teams through column permissions, balancing privacy protection and research needs.
