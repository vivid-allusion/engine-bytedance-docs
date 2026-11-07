---
title: "Managing projects"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/Managing-projects"
---

<span id=".566A5LuL"></span>
## Overview

Project management is a resource management method provided by the BytePlus platform. This method allows you to group and manage cloud resources based on businesses or projects. IAM authorization by project (where a project is a collection of resources) helps ensure resource isolation and data security. It also allows you to view resource usage bills from a project perspective, making it easier to calculate cloud resource costs. For more information, refer to [About projects](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-projects).

<span id=".6aG555uu566h55CG5L2_55So5rWB56iL"></span>
## Project management process

If you need to use a project, follow these steps:


1. [Create a project](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-project): Create a project to manage instances by project.

2. [Manage project permissions](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Permission_Management): Grant project permissions to IAM users.

3. (Optional) [Manage project resources](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Resource_Management): When the project to which a migration source or migration task belongs changes, project transfer operations (inbound/outbound) for the source or task can be performed based on your needs.


<span id=".6YCa6L-H6aG555uu5p-l55yL6L-B56e76LWE5rqQ"></span>
## View migration resources by project


1. Log in to [the ECS console](https://console.byteplus.com/ecs/instance).

2. In the left directory tree under any region, select "Server Migration Center \> Migration Source".

3. In the top menu bar, select the target project based on your needs.

   * Select All Resources to view all resources under this account.

   * Select specific project to view all resources associated with the project.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When you log in with root user or an IAM user, the system defaults to displaying all resources under that account.</div>


* <div data-tips="true" data-tips-type="tip">If the IAM user is not granted global permissions or the system fails to display all the resources under the account after All Resources is selected, switch to another project or contact the owner of the BytePlus account to obtain the required permissions.</div>
