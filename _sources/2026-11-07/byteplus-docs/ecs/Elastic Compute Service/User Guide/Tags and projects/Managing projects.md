---
title: "Managing projects"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Managing-projects"
---

<span id=".566A5LuL"></span>
## Overview

When you use ECS instances, each time you perform a creation operation, a corresponding resource may be created, such as instances, images, key pairs, volumes, snapshots, elastic network interfaces, and security groups. Project management is a resource management method provided by the platform. This method allows you to group and manage resources based on businesses or projects. With Identity and Access Management (IAM), you can grant permissions to users by project (i.e., a group of resources) to ensure resource isolation and data security. You can also view resource bills by project to facilitate the calculation of cloud resource costs.

 For more information about projects, see [Managing projects](https://docs.byteplus.com/en/docs/byteplus-platform/docs-project-management).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Considerations


* ECS\-related resources that can be managed by projects include: instances, volumes, custom images, key pairs, RIs, ESIs, launch templates, orchestration, and cloud assistant.

* A resource can belong to only one project.

* For a newly created resource, if you have not associated it with a project, it will be associated with the "default" project.

* After you associate the resource with a project, only users with permissions on the project can use the resource.

* Associations between resources do not change due to project assignments.

* If you need to associate resources from multiple projects, you need to have permissions for all projects that contain resources to be associated. For example, if you want to associate an EIP from Project B to an instance in Project A, you are required to have permissions for both Project A and Project B .

* When you create and manage resources using an IAM user, the IAM user must have corresponding permissions granted by the root account. 


<span id=".6aG555uu566h55CG5L2_55So5rWB56iL"></span>
## Project management process

The general process for project management is as follows (instances are used as an example here). If you need to associate projects with other newly created resources (such as images, key pairs, volumes, and RIs), select the target resource in the left\-side navigation pane.


1. [Create a project](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-project): Create a project to manage instances.

2. [Add the project permission for an IAM user](https://docs.byteplus.com/en/docs/byteplus-platform/docs-editing-a-project): Grant project permission for the IAM user.

3. [Create an instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances): Use the IAM user to create an instance and associate the instance with the project.

4. (Optional) [Move the instance into/out of a project](https://docs.byteplus.com/en/docs/byteplus-platform/docs-editing-a-project): When the project associated with the instance changes, you can move the instance into or out of the project.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you change the project an instance belongs to, resources associated with the instance are moved to the specified project along with the instance. Such resources include system and data volumes, primary network interfaces, and EIPs associated with the primary network interface.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">We recommend that you avoid changing the project for an instance right after you associate sub\-resources with the instance (such as data volumes or EIPs). Otherwise, the instance and its sub\-resources may belong to different projects. You can wait a few seconds after the association is complete before changing the project.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">We recommend that you avoid changing the project for an instance right after you disassociate sub\-resources from the instance (such as data volumes or EIPs). Otherwise, the instance and its disassociated sub\-resources may belong to the same project. You can wait a few seconds after the disassociation is complete before changing the project.   </div>
   


<span id=".5p-l55yL6aG555uu6LWE5rqQ5L-h5oGv"></span>
## View resource details of projects

<span id=".5p-l55yL6LWE5rqQ5omA5Zyo6aG555uu"></span>
### View projects that resources belong to

On the Instances page, click the target instance to enter the instance Overview page. In the  **"Basic information"**  section, you can view associated project of the instance.

<span id=".6YCa6L-H6aG555uu5pCc57Si6LWE5rqQ"></span>
### Search for resources by projects


1. Log in to the [ECS console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/instance).

2. In the top menu bar, select the region and choose the project based on the description below.

   * Select All Resources to view all resources under this account.

   * Select a specific project to view all resources associated with the project.

   * Select Manage projects to go to the project list and manage the projects.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you log in with the root account or an IAM user, the system defaults to displaying all resources under that account.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the IAM user is not granted permissions, after you select "All Resources", the system does not display all resources under the account. Follow the interface instructions to switch to another project or contact the root account to obtain the required permissions.   </div>
   


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

You can also use [tags](https://docs.byteplus.com/en/docs/ecs/Tag-overview) to categorize ECS resources for fine\-grained resource management.
