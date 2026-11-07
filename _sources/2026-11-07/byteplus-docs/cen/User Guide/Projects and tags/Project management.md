---
title: "Project management"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Projects-and-tags-01"
---

<span id=".566A5LuL"></span>
## Introduction​

Project management is a resource management approach provided by the platform, allowing you to group and manage cloud resources used by different businesses or projects. IAM authorization based on projects (i.e., a group of resources) helps maintain resource independence and data security. It also enables viewing resource consumption bills from a project perspective, facilitating the calculation of cloud resource usage costs. 

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The resources supported by Cloud Enterprise Network (CEN) project management function include CEN instances and bandwidth packages.

* As a sub\-resource of a CEN instance, inter\-region bandwidth cannot be assigned to a specific project during creation. Its project affiliation defaults to the same project as the CEN instance. When a CEN instance is moved into or out of a project, the project affiliation of its inter\-region bandwidth changes accordingly. Moving inter\-region bandwidth into or out of a project independently is not supported.

* A resource can belong to only one project.

* Associations between resources do not change due to project assignments.

* To associate resources from multiple projects, you must have permissions for all projects involved. For example, to associate an elastic IP address (EIP) from Project B with an instance in Project A, you must have permissions for both Project A and Project B. 


<span id="LiQElv1X"></span>
## Usage process

The general workflow for project management is as follows:


|No. |Procedures |Explanation |
|---|---|---|
|1 |Create project |Create project: Create a project to manage Cloud Enterprise Network (CEN) resources. |
|2 |Add project permission for an IAM user |Authorize project permission for the IAM user. |
|3 |Create Cloud Enterprise Network (CEN) resources |Create Cloud Enterprise Network (CEN) resources using an IAM user. This example uses creating a CEN instance. |
|4 |(Optional) Cloud Enterprise Network (CEN) resource transfer in/out projects |You can transfer Cloud Enterprise Network (CEN) resources in or out when their project assignment changes. |
|5 |(Optional) View bills by project |You can filter bills by project. |


<span id="eKscNACC"></span>
## Search for resources by project


1. Log in to the CEN console.

2. In the top navigation bar, select Region, then select the project according to the instructions below.

   * Select All resources to view all resources under the current account.

   * Select a specific project to view all resources associated with that project.

   * Click Manage projects to redirect to the project list for project management.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When logging in with a root user or an IAM user, the system will display all resources under the account by default.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If your IAM user has not been granted global permissions, selecting All Resources will not display the complete resource list. Please switch projects or contact the root user for authorization.   </div>
