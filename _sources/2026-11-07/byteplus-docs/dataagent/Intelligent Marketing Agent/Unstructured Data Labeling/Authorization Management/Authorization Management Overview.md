---
title: "Authorization Management Overview"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Authorization_Management_Overview"
---

Each functional module of the platform involves multiple permissions, such as account, user, label, and other permissions. In this module, users can centrally manage various permissions and authorizations, and use enterprise data more securely and in compliance. This article introduces you to rights management in the unstructured data marking function.

<span id="8bf211a5"></span>
# Function introduction

Rights management is divided into two parts:


| |Module |Function introduction |Operation document |
|---|---|---|---|
|Part 1 |Volcano Engine \- Access Control |For creating projects, user accounts, roles, etc.<br><br>You can directly associate and use created users and roles. |[access control document](https://www.volcengine.com/docs/6257/64959) |
|Part 2 |Project Center |Used to manage users, user groups, and authorize various permissions. |[Manage by user](https://www.volcengine.com/docs/6356/1154925)<br><br>[Manage by content](https://www.volcengine.com/docs/6356/1154926) |


<span id="63caac3f"></span>
# Manager Role Types

Currently has three management roles, namely **group administrator \> project administrator \> resource manager** :


| |Job Description |Scope of authority |
|---|---|---|
|Group administrator |The single group administrator is an Admin account ( **does not support flexible configuration** ), which **has the highest authority of the group** , and can manage, edit, and view the functions, resources, and data line permissions of all projects under the group. |**Id\-mapping** is configured **exclusively for** group administrators and can only be configured by group administrators. Group administrators can configure project administrators and resource managers. |
|Project Manager |**With the highest project authority** , you can manage, edit, and view the functions, resources, and data line permissions of the corresponding project. Project administrators can set it up flexibly. |Project administrators can configure permissions within their **project permissions** . |
|Resource Manager |The resource manager grants resource permissions to other users in **each business module** (tag module, grouping module), and the resource manager can set it flexibly. |Resource permissions can be configured within the **resource permissions** they have. |


<span id="9d6dd7e1"></span>
# Authorized object

There are four types of authorization objects, including users, roles, user groups, and departments. Their concepts and relationships are as follows:


|**Concept** |**Paraphrase** |
|---|---|
|User |Users are the subjects corresponding to a single independent account, and users can belong to roles, user groups, and departments. |
|Role |A role is a collection of users, which is group\-granular (after a role is created, it will be displayed in different projects under the same group, and the users are the same). |
|User group |A user group is also a collection of users and is project\-specific (projects within the same group can have different user groups). |
|Department |A department is an organizational structure with a hierarchical relationship and a collection of users, which is platform\-granular (there can only be one set of departments present on all major platforms, and departments in different groups are the same). |


<span id="01652391"></span>
# Licensed content

There are four types of authorized content, including project, function (module), resource, and data line permissions.


|**Concept** |**Paraphrase** |
|---|---|
|Project |Refers to the project space, which contains all authorized content under the project, such as functions, resources, and data line permissions. |
|Function (module) |Page menu and button permissions, such as data management module, label module view, edit, management permissions. |
|Resource |Resources are the assets produced by the system, such as data sets, data files, tags, grouping, etc. Resources have viewing, editing, and management rights. |
|Data rules |It is the permission of a certain line under the resource, such as the sales channel label. Some users can only view the label of "Channel = Douyin", and some users can only view the label of "Channel = JD.com, Tmall". |


<span id="1ad9256d"></span>
# Authorization rules


* **Authorization mechanism:**  Based on the administrator authorization mechanism, permission application is not supported, and group administrators and project administrators can grant permissions to ordinary users.

* **Authorization model:**  Authorization logic is based on the "ABAC + RBAC" model, which is very flexible, and can grant project, function, resource, and data line permissions to users, user groups, roles, and departments.

* **Authority inheritance:** 

   * Users inherit project, function, resource, and data line permissions for user groups, roles, and departments.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Example: User A has permission to resource 1, user A belongs to role F, and role F has permission to resource 2, then user A will also have permission to resource 2 at the same time      </div>
      

   * Project, function, resource permissions, according to the type of authorization to determine the intersection or union. If it is "authorization" logic, the final merge is taken; if it is "disabled" logic, the final "intersection" is taken.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Projects, functions, tags, and other resources follow the authorization logic. When user A belongs to role F (with the permission of resource 2) and role H (with the permission of resource 3) at the same time, then user A will have the permission of resource 2 + resource 3;      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Indicator resources and main resources follow the disabling logic. When user A disables resource 1 and resource 2, neither of them has resource permissions.      </div>
      

   * Data row permissions intersect.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The authorized users of the data line permission rule 1 (only access to "channel = Douyin" data) and the data line permission rule 2 (only access to "gender = male" data) have user A, and user A can access the data of "channel = Douyin" and "gender = male", narrowing the data scope.      </div>
