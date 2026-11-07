---
title: "Project management"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Project_management"
---

[Project management](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Management) is a resource management method provided by BytePlus, allowing you to group resources used in different businesses or projects. Based on projects (a group of resources), IAM authorization is beneficial for maintaining resource independence and data security; it also facilitates the viewing of resource consumption bills from a project perspective to calculate the cost of cloud resource usage. This article introduces how to use projects in FaaS services.

<span id="note"></span>
## Note


* The FaaS\-related resources that support project management include: function.

* A resource can only belong to one project.

* If you do not specify a specific project for a newly created resource, it is added by default to the default project.

* Once bound to a project, resources can only be used by users with permissions for that project.

* If you need to associate resources from multiple projects, you must have permissions for all projects of the associated resources; for example, to associate a function in project a with a TOS Bucket in project b, you must have permissions for both project a and b. For authorization operations, refer to [Project Permission Management](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Permission_Management).

* When using IAM users to create and manage resources, the IAM user must have been granted the necessary permissions by the BytePlus account (main account). For detailed operations on adding global permissions or project permissions to a user, refer to [Creating a user](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user).


<span id="usage-process"></span>
## Usage process

This article uses functions as an example to introduce how to manage cloud resources by project. The general usage process for project management features is as follows:


1. [Create Project](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Management#creating-project): Create a project to manage functions by project.

2. [Add Project Permissions to IAM User](https://docs.byteplus.com/en/docs/resourcemanagement/Use_of_Project_by_IAM_User): Grant project permissions to IAM users.

3. [Create Function](https://docs.byteplus.com/en/docs/faas/Function_Creation_Option_Selection): Have IAM users create functions and bind the projects.

4. (Optional) [Function moves in/out of project](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Resource_Management): When the function's project affiliation changes, you can perform move in/out operations.


<span id="view-project-resource-information"></span>
## View project resource information

<span id="view-the-project-where-the-resource-is-located"></span>
### View the project where the resource is located


1. Log in to the [Function Service console](https://console.byteplus.com/vefaas).

2. Select the region where your business is located in the top navigation bar.

3. On the **Function** page, find the target function and click the function name.

4. In the **Function Configuration** tab, view the project information associated with the function.


<span id="search-for-resources-by-project"></span>
### Search for resources by project


1. Log in to the [Function Service console](https://console.byteplus.com/vefaas).

2. On the top navigation bar, select the region and follow the instructions below to choose the project.

   1. Select **All resources under account** to view all resources under the current account.

   2. Select the specific project to view all resources bound to that project.

   3. Select **Manage Projects** to jump to the project list page to manage projects.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The system defaults to displaying all resources under the logged\-in account.</div>


* <div data-tips="true" data-tips-type="tip">If you log in to the console with an IAM user, but the IAM user has not been granted global permissions, selecting <strong>All Resources of the Account</strong> will not display the complete list of resources under the account. Please switch projects or contact the BytePlus account for authorization.</div>
