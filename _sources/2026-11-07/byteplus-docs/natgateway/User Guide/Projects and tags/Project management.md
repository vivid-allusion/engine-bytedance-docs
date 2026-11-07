---
title: "Project management"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Managing-projects"
---

<span id=".566A5LuL"></span>
## Instructions

Project management is a resource management approach provided by BytePlus, allowing you to group and manage cloud resources used by different businesses or projects. IAM authorization based on projects (i.e., a group of resources) helps maintain resource independence and data security. It also enables viewing resource consumption bills from a project perspective, facilitating the calculation of cloud resource usage costs. For more information, see [Project overview](https://docs.byteplus.com/en/docs/6649/189152).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* When a NAT Gateway is moved into or out of a project, its sub\-resources (SNAT entry, DNAT entry, secondary network interfaces created with the NAT Gateway, and NAT Gateway security groups) will also be moved accordingly.

* NAT Gateway resources created before September 5, 2023, and not assigned to any project, will default to the default project.


<span id=".6aG555uu566h55CG5L2_55So5rWB56iL"></span>
## Project management process

If you need to use a project, follow these steps:


1. [Create a project](https://docs.byteplus.com/en/docs/6649/94336).

2. [Add project permission](https://docs.byteplus.com/en/docs/6649/173422).

3. [Move resources into the project](https://docs.byteplus.com/en/docs/6649/94337).

4. [View project accounting](https://docs.byteplus.com/en/docs/6649/174601).


<span id=".6YCa6L-H6aG555uu5pCc57SiTkFU572R5YWz"></span>
## Search NAT Gateway by projects


1. Log in to [NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top navigation bar, select Region, then select the project according to the instructions below.

   * Select All resources to view all resources under the current account.

   * Select a specific project to view all resources associated with that project.

   * Click Manage projects to redirect to the project list for project management.

* When logging in with a main account or an IAM user, the system will display all resources under the account by default.

* If the IAM user is not granted global permissions or the system fails to display all the resources under the account after All Resources is selected, switch to another project or contact the root account to obtain the required permissions.
