---
title: "Project management"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Managing-projects"
---

<span id=".566A5LuL"></span>
## Introduction​

Project management is a resource management approach provided by BytePlus, allowing you to group and manage cloud resources used by different businesses or projects. IAM authorization based on projects (i.e., a group of resources) helps maintain resource independence and data security. It also enables viewing resource consumption bills from a project perspective, facilitating the calculation of cloud resource usage costs.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* PrivateLink supports the project management feature for the following resources: Endpoint Services and Endpoints.

* The network interface associated with an endpoint belongs to the same project as the endpoint by default. When an endpoint is moved into or out of a project, the project affiliation of its network interface is updated accordingly.

* A resource can belong to only one project.

* Associations between resources do not change due to project assignments.

* To associate resources from multiple projects, you must have permissions for all projects involved. To associate a service resource from Project B with an endpoint service in Project A, you need permissions for both Project A and Project B. 


<span id=".5L2_55So5rWB56iL"></span>
## Usage process

The general workflow for project management is as follows:

&nbsp;


|No. |Procedures |Explanation |
|---|---|---|
|1 |Create a project |Create a project to manage PrivateLink connection resources by project. |
|2 |Add project permissions for IAM users |Authorize project permissions for sub\-users. |
|3 |Create Endpoint Service |Create private network connection resources using a subuser, taking the creation of an endpoint service as an example. |
|4 |(Optional) Move PrivateLink resources into/out of a project |If the project assignment of a PrivateLink resource changes, you can move it in or out of the project. |
|5 |(optional) View bill by project |You can filter bills by project. |


<span id=".6YCa6L-H6aG555uu5pCc57Si56eB572R6L-e5o6l6LWE5rqQ"></span>
## Search PrivateLink resources by project

The following steps use endpoint service as an example. The steps for managing endpoints are similar.


1. Use the service provider's account to log in to the Endpoint service console.

2. In the top navigation bar, select Region, then select the project according to the instructions below.

   * Select All Resources to view all resources under the current account's endpoint service.

   * Select a specific project to view all endpoint service resources that are bound to that project.

   * Select Manage Project to create, modify, or delete projects as needed.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When logging in with a root user or an IAM user, the system will display all resources under the account by default.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If your IAM user has not been granted global permissions, selecting <strong>All Resources</strong> will not display the complete resource list. Please switch projects or contact the root user for authorization.   </div>
