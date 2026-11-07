---
title: "Managing projects"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Managing-projects"
---

<span id=".566A5LuL"></span>
## Overview

Project management is a resource management method that allows you to group and manage cloud resources based on business or project. IAM authorization by project (where a project is a collection of resources) helps ensure resource isolation and data security. It also allows you to view resource usage bills from a project perspective, making it easier to calculate cloud resource costs.

For more information on projects, refer to [Managing projects](https://docs.byteplus.com/en/docs/resourcemanagement/Product_Overview).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* Currently, only scaling groups support the project feature.

* A resource (scaling group) can only belong to one project. After you associate it with a project, only users with permissions on the project can use the resource.

* Projects associated with resources such as ECS instances in a scaling group will not be affected by associating or disassociating the scaling group with/from a project.

* When you create and manage resources using an IAM user, the IAM user must have corresponding permissions granted by the root user. For detailed operations to grant global permission or project\-level permission for an IAM user, refer to .


<span id=".6aG555uu566h55CG5L2_55So5rWB56iL"></span>
## Project management process

The general process for project management is as follows:


1. [Create a project](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Management#creating-project): Create a project to manage scaling group resources.

2. [Grant project permissions to IAM user](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Permission_Management): Grant project permissions to an IAM user.

3. [Create a scaling group](https://docs.byteplus.com/en/docs/as/Creating-a-scaling-group): Create a scaling group with the IAM user.

4. [(Optional) Associate or disassociate target scaling group with/from the project](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Resource_Management): When the project associated with the scaling group changes, you can perform associating/disassociating operations.

6. [(Optional) View bill details by project](https://docs.byteplus.com/en/docs/byteplus-platform/docs-bill-details): You can filter bills by projects.


<span id=".6YCa6L-H6aG555uu5pCc57Si5Ly457yp57uE"></span>
## Search scaling groups by project


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the region and choose the project based on the description below.

   * Select All Resources to view all resources under this account.

   * Select a specific project to view all resources associated with the project.

   * Select Manage projects to go to the project list and manage the projects.

* When you log in with the root account or an IAM user, the system defaults to displaying all resources under that account.

* If the IAM user is not granted global permissions or the system fails to display all the resources under the account after All Resources is selected, switch to another project or contact the owner of the BytePlus account to obtain the required permissions.
