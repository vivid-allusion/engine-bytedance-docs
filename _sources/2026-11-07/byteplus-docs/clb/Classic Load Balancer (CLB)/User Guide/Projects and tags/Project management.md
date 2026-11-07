---
title: "Project management"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Project-management"
---

<span id=".566A5LuL"></span>
## Introduction​

Project management is a resource management approach provided by the platform, allowing you to group and manage cloud resources used by different businesses or projects. IAM authorization based on projects (i.e., a group of resources) helps maintain resource independence and data security. It also enables viewing resource consumption bills from a project perspective, facilitating the calculation of cloud resource usage costs. 

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Resources that support project management in Classic Load Balancer (CLB) include CLB instances, access control list groups, and certificates.

* Listeners and backend server groups, as sub\-resources of CLB instances, do not support specifying projects during creation; their project defaults to that of the CLB instance. When a CLB instance moves into or out of a project, the related listeners and backend server groups also synchronize their project assignments. Moving listeners or backend server groups independently is not supported.

* When a public CLB instance moves into or out of a project, its associated Elastic IP address (EIP)'s project changes accordingly (it is recommended to wait a few seconds after the move before checking if the CLB instance and its associated EIP share the same project). The project of the EIP bound to a private CLB instance does not change with the CLB instance.

* A resource can belong to only one project.

* Associations between resources do not change due to project assignments.

* To associate resources from multiple projects, you must have permissions for all projects involved. For example, to associate an EIP from Project B with an instance in Project A, you must have permissions for both Project A and Project B. For authorization, see Adding project permissionAdding project permission.


<span id=".5L2_55So5rWB56iL"></span>
## Usage process

The general workflow for project management is as follows:


|No. |Actions |Explanation |
|---|---|---|
|1 |Create project |Create a project to manage CLB resources. |
|2 |Add project permissions for an IAM user |Authorize project permissions for IAM users. |
|3 |Create CLB resource |Create CLB resources using IAM users, here using creating a CLB instance as an example. |
|4 |(Optional) Move CLB resources into or out of projects |When the related project of a CLB resource changes, you can move it in or out of the project. |
|5 |(Optional) View bills by project |You can filter bills by project. |


<span id="2TyAtSQX"></span>
## Search for instances by project


1. Log in to the CLB console.

2. In the top navigation bar, select Region, then select the project according to the instructions below.

   * Select All resources to view all resources under the current account.

   * Select a specific project to view all resources associated with that project.

   * Click Manage projects to redirect to the project list for project management.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When logging in with a main account or an IAM user, the system will display all resources under the account by default.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If your IAM user has not been granted global permissions, selecting <strong>All Resources</strong> will not display the complete resource list. Please switch projects or contact the main account for authorization.   </div>
   


&nbsp;
