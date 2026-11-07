---
title: "Project management"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Managing-projects"
---

<span id=".566A5LuL"></span>
## Overview

Project management is a resource management approach provided by BytePlus, allowing you to group and manage cloud resources used by different businesses or projects. IAM authorization based on projects (i.e., a group of resources) helps maintain resource independence and data security. It also enables you view resource consumption bills from a project perspective, facilitating the calculation of cloud resource usage costs. For more information, see [Project overview](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Overview).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* After associating an EIP with an Elastic Compute Service instance (i.e., associating the EIP with the instance's primary network interface), the EIP becomes a sub\-resource of the ECS instance, just like the system disk, data disk, and primary network interface. If the ECS instance's project changes, the EIP's project changes accordingly.

* EIP resources applied before September 5, 2023, but not assigned to any project, default to the default project.


<span id=".6aG555uu566h55CG5L2_55So5rWB56iL"></span>
## Project management process

If you need to use a project, follow these steps:


1. [Create a new project](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Management#creating-project).

2. [Add project permissions](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Permission_Management).

3. [Transfer resources to the project](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Resource_Management#transferring-resource-into-project).


<span id=".6YCa6L-H6aG555uu5pCc57Si5YWs572RSVA="></span>
## Search for EIP by project


1. Log in to the [EIP console](https://console.byteplus.com/eip/eips).

2. In the top navigation bar, select region, then select the project according to the instructions below.

   * Select All Resources to view all resources under the current account.

   * Select a specific project to view all resources attached to the project.

   * Select Manage Project to go to the project list for project management.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">When logging in with the main account or an IAM user, the system defaults to display all resources under the account.</div>


* <div data-tips="true" data-tips-type="default">If your IAM user is not granted global permissions, selecting "All Resources" will fail to display the full list of resources under the account. Switch projects or contact the main account for authorization.</div>
