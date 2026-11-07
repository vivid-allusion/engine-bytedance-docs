---
title: "Project management"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Project-management"
---

<span id=".566A5LuL"></span>
## Overview

Project management is a resource management approach provided by BytePlus, allowing you to group and manage cloud resources used by different businesses or projects. IAM authorization based on projects (i.e., a group of resources) helps maintain resource independence and data security. It also enables viewing resource consumption bills from a project perspective, facilitating the calculation of cloud resource usage costs.

For more information, see [Project overview](https://docs.byteplus.com/en/docs/6649/189152).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Associations between cloud resources do not change due to project assignments.

* Direct Connect Connection resources created before August 31, 2023, and Direct Connect Gateway resources created before August 31, 2024, that were not assigned to a specific project will default to belonging to the **default** project.

* Only the root account, IAM users with global permissions over the cloud resource, or IAM users authorized for the default project can manage resources in the default project.

   * When logging in to the console as an IAM user for creating/viewing cloud resources, you cannot perform any actions after switching to any unauthorized projects.

   * When using an IAM user to create and manage cloud resources, the IAM user must have been granted the corresponding permissions by the main account.

   * If an IAM user cannot view resources, it might be because the IAM user lacks permissions for the project where those resources reside. Please switch to a project for which you have permissions before viewing.

* It is not recommended to associate resources across different projects. If associating resources from two different projects is necessary, the IAM user must have operational permissions for both projects involved.

* A resource can only exist in one project and cannot be shared across different projects. You can change the project to which a resource belongs. For details, see [Move resources in/out of a project](https://docs.byteplus.com/en/docs/6649/94337#%E8%B5%84%E6%BA%90%E8%BD%AC%E5%85%A5%E9%A1%B9%E7%9B%AE).

* Currently, within the Direct Connect service, only DC Connection and Direct Connect Gateway support the project management capability. Virtual Interface does not support this yet. If an IAM identity is granted only **Project permissions** for the DirectConnectFullAccess or DirectConnectReadOnlyAccess policy, the IAM identity will not be able to view or use the full Direct Connect functionality. You need to configure custom policies. See [Instructions for IAM users on using Direct Connect policies and permissions configuration](https://docs.byteplus.com/en/docs/directconnect/Configuration-example-of-custom-policy#.5a2Q55So5oi35L2_55So5LiT57q_6L-e5o6l562W55Wl5Y-K5p2D6ZmQ6YWN572u6K-05piO).


<span id=".6aG555uu566h55CG5L2_55So5rWB56iL"></span>
## Project management process

The general workflow for project management is as follows:


1. [Create project](https://docs.byteplus.com/en/docs/6649/94336#%E6%96%B0%E5%BB%BA%E9%A1%B9%E7%9B%AE): Create a project to manage DC Connection resources.

2. [Permission policy](https://docs.byteplus.com/en/docs/6649/173422#%E6%B7%BB%E5%8A%A0%E9%A1%B9%E7%9B%AE%E6%9D%83%E9%99%90): Grant IAM users permissions to access the project.

3. [Create DC Connection](https://docs.byteplus.com/en/docs/directconnect/Accessing-a-Direct-Connect-connection-1): Use an IAM user to access DC Connection resources.

4. [(Optional) Move DC Connection into or out of a project](https://docs.byteplus.com/en/docs/6649/94337#%E8%B5%84%E6%BA%90%E8%BD%AC%E5%85%A5%E9%A1%B9%E7%9B%AE): Transfer DC Connection resources into or out of projects.

5. [(Optional) View bills by project](https://docs.byteplus.com/en/docs/byteplus-platform/docs-bill-details#.5LiA44CB6LSm5Y2V5piO57uG): Filter bills based on projects.


<span id=".6YCa6L-H6aG555uu5pCc57Si6LWE5rqQ"></span>
## Search resources by project


1. Log in to [the Direct Connect Connection console](https://console.byteplus.com/dc/PhysicalConnection).

2. In the top navigation bar, select target region, then select the project according to the instructions below.

   * Select All Resources: View all resources under the current account.

   * Select a specific project: View all resources associated with that project.

   * Select Manage Project: Redirect to the project list for project management.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When logging in with the main account or a global IAM user (an IAM user granted the DirectConnectFullAccess policy with Global permissions), the system displays all resources under that account by default.</div>


* <div data-tips="true" data-tips-type="tip">If your IAM user has not been granted the DirectConnectFullAccess policy with Global permissions, selecting "All Resources" will not display the full list of the account's resources. Please switch to an authorized project to view resources or contact the main account for authorization.</div>


* <div data-tips="true" data-tips-type="tip">You can only search for resource information that supports project management capabilities. Resources that do not support project management cannot be found via project search.</div>
