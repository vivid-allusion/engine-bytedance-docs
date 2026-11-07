---
title: "Project management"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Project-management"
---

<span id=".566A5LuL"></span>
## Introduction​

Project management is a resource management approach provided by the platform, allowing you to group and manage cloud resources used by different businesses or projects. IAM authorization based on projects (i.e., a group of resources) helps maintain resource independence and data security. It also enables viewing resource consumption bills from a project perspective, facilitating the calculation of cloud resource usage costs.

For more information, see [Project overview](https://docs.byteplus.com/en/docs/6649/189152).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Associations between cloud resources do not change due to project assignments.

* Only the root account, IAM users with global permissions over the cloud resource, or IAM users authorized for the default project can manage resources in the default project.

   * When logging in to the console as an IAM user for creating/viewing cloud resources, you cannot perform any actions after switching to any unauthorized projects.

   * When you create and manage cloud resources using an IAM user, the IAM user must have corresponding permissions granted by the root account. For related actions, see Control resource access by IAM.

   * If an IAM user cannot view resources, it might be because the IAM user lacks permissions for the project where those resources reside. Please switch to a project for which you have permissions before viewing.

* We do not recommend associating resources across projects. If you must associate resources from two projects, permissions for both projects of the to\-be\-associated resources are required.

* A resource can only exist within one project and cannot be shared across different projects.

* Sub\-resources cannot be migrated independently between projects.

   * VPN gateway routes are sub\-resources of the VPN gateway and can only be migrated together with their parent VPN gateway. Independent migration of VPN gateway routes is not supported.

   * SSL client certificates are sub\-resources of the SSL server and can only be migrated together with their parent SSL server. Independent migration of SSL client certificates is not supported.


<span id=".6aG555uu566h55CG5L2_55So5rWB56iL"></span>
## Project management process

The general workflow for project management is as follows:


1. [Create project](https://docs.byteplus.com/en/docs/6649/94336): Create a project to manage resources in the scaling group.

2. [Permission policy](https://docs.byteplus.com/en/docs/6649/173422): Grant IAM users permissions to access the project.

3. [Create VPN Connect resources](https://docs.byteplus.com/en/docs/vpn/Creating-a-VPN-gateway-2): Use an IAM user to create VPN Connect resources.

4. [(Optional) Transfer VPN Connect resources into/out of projects](https://docs.byteplus.com/en/docs/6649/94337): Perform transfer operations for VPN Connect resources.

5. [(Optional) View bills by project](https://docs.byteplus.com/en/docs/byteplus-platform/docs-bill-details#.5LiA44CB6LSm5Y2V5piO57uG): Filter bills based on projects.


<span id=".6YCa6L-H6aG555uu5pCc57SiVlBO6L-e5o6l6LWE5rqQ"></span>
## Search VPN Connect resources by projects


1. Log in to the [VPN Connect console](https://console.byteplus.com/vpn/region:vpn+cn-beijing/vpnGateway).

2. In the top navigation bar, select target Region, then select the project according to the instructions below.

   * Select All Resources: View all resources under the current account.

   * Select a specific project: View all resources associated with that project.

   * Select Manage Project: Redirect to the project list for project management.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When logging in with the main account or a global IAM user, the system displays all resources under that account by default.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If your IAM user has not been granted global permissions, selecting <strong>All Resources</strong> will not display the full list of resources under the account. Switch to a project where your current account has read\-write permissions or contact the main account for authorization.   </div>
