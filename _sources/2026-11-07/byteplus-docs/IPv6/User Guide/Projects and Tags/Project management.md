---
title: "Project management"
product: "IPv6 Gateway"
product_code: "IPv6"
source: "https://docs.byteplus.com/en/docs/IPv6/Managing_projects"
---

<span id=".566A5LuL"></span>
## Instructions

Project management is a resource management approach provided by BytePlus, allowing you to group and manage cloud resources used by different businesses or projects. IAM authorization based on projects (i.e., a group of resources) helps maintain resource independence and data security. It also enables viewing resource consumption bills from a project perspective, facilitating the calculation of cloud resource usage costs. For more information, see [Project overview](https://docs.byteplus.com/en/docs/6649/189152).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* IPv6 Gateway instance resources created before January 8, 2025 default to the default project.

* Associations between resources do not change due to project assignments.

* Only the root account, IAM users with global permissions over the cloud resource, or IAM users authorized for the default project can manage resources in the default project.

* When logging in to the console as an IAM user for creating/viewing cloud resources, you cannot proceed any actions after switching to any unauthorized projects.

* When you create and manage cloud resources using an IAM user, the IAM user must have corresponding permissions granted by the root account. For related actions, see [IAM policy types for IPv6 Gateway](https://docs.byteplus.com/en/docs/6896/1222927).

* We do not recommend associating resources across projects. If you must associate resources from two projects, permissions for both projects of the to\-be\-associated resources are required.

* A resource can only exist in one project and cannot be shared across different projects. You can change the project to which a resource belongs. For details, see [Transfer resources in/out of a project](https://docs.byteplus.com/en/docs/6649/94337).


<span id=".6aG555uu566h55CG5L2_55So5rWB56iL"></span>
## Project management process

The general workflow for project management is as follows:


1. [Create a project](https://docs.byteplus.com/en/docs/6649/94336): Create a project for managing IPv6 Gateway resources.

2. [Permission policy](https://docs.byteplus.com/en/docs/6649/173422): Grant IAM users permissions to access the project.

3. [Create an IPv6 Gateway instance](https://docs.byteplus.com/en/docs/IPv6/Creating_an_IPv6_gateway_instance): Create an IPv6 Gateway instance using the IAM user.

4. [(Optional) Transfer IPv6 Gateway resources in/out of a project](https://docs.byteplus.com/en/docs/6649/94337): When the project of IPv6 Gateway resources changes, you can transfer resources in or out.

5. [(Optional) View bills by project](https://docs.byteplus.com/en/docs/byteplus-platform/docs-bill-details): Filter bills based on projects.


<span id=".6YCa6L-H6aG555uu5pCc57SiSVB2NuWunuS-i-i1hOa6kA=="></span>
## Search IPv6 instance resources by projects


1. Log in to [the IPv6 Gateway console](https://console.byteplus.com/eip/ipv6s).

2. In the top navigation bar, select Region, then select the project according to the instructions below.

   * Select All Resources to view them under your current account.

   * Select a specific project to view all resources associated with that project.

   * Click Manage projects to redirect to the project list for project management.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When logging in with a main account or an IAM user, the system will display all resources under the account by default.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the IAM user is not granted global permissions or the system fails to display all the resources under the account after All Resources is selected, switch to another project or contact the root account to obtain the required permissions.   </div>
