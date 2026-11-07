---
title: "Project management"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Projects"
---

<span id=".566A5LuL"></span>
## Introduction​

Project management is a resource management method that allows you to group and manage cloud resources used by different businesses or projects. IAM authorization based on projects (i.e., a group of resources) helps maintain resource independence and data security. It also enables viewing resource consumption bills from a project perspective, facilitating the calculation of cloud resource usage costs.

For more information, see [Project management](https://docs.byteplus.com/en/docs/6649/94333#%E9%A1%B9%E7%9B%AE%E7%AE%A1%E7%90%86)[Project management](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Management).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Transit Router (TR) supports project management for resources including TR instances and bandwidth packages.

   Network instance attachments, TR route tables, TR route entries, inter\-region peerings, and multicast domains are sub\-resources of TR instances. They do not support specifying projects during creation and inherit the project of their TR instance by default. When a TR instance moves into or out of a project, the projects of its related sub\-resources change in synchronization. Moving sub\-resources individually into or out of projects is not supported.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In cross\-account scenarios, after the recipient accepts instance sharing, the shared TR instance belongs to the default project by default. You can move this shared TR instance into or out of projects as needed. Changes to the shared TR instance project between the shared user account and the resource owner account do not affect each other.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In cross\-region scenarios, the projects to which the same inter\-region peering attachment belongs in different regions are the same as the project of the TR instance in the local region.   </div>
   

* Associations between resources do not change due to project assignments.

* If you operate resources across multiple projects, you must have permissions for all the projects to which the operated resources belong. For example, to create an attachment connecting a transit router instance in project A to a VPC in project B, you must have permissions for both projects A and B. For authorization actions, see[ Add project permissions](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Permission_Management).


<span id=".6YCa6L-H6aG555uu5pCc57Si5a6e5L6L"></span>
## Search instances by project


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. In the top navigation bar, select Region, then select the project according to the instructions below.

   * Select All resources to view all resources under the current account.

   * Select a specific project to view all resources associated with that project.

   * Select Manage Project to create, modify, or delete projects as needed.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When logging in with a main account or an IAM user, the system will display all resources under the account by default.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If your IAM user has not been granted global permissions, selecting <strong>All Resources</strong> will not display the complete resource list. Please switch projects or contact the main account for authorization.   </div>
