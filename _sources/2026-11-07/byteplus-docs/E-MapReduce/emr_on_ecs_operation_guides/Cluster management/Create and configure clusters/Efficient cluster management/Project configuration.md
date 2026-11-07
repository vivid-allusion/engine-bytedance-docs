---
title: "Project configuration"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ecs-project_configuration"
---

Project management is a resource management method provided by Volcano Engine, which allows you to group and manage cloud resources used by different businesses or projects. Granting IAM permissions based on projects (that is, a group of resources) helps maintain resource independence and data security. You can also view resource consumption bills from the project perspective, making it easier to calculate the cost of cloud resource usage.

<span id="_1-使用场景"></span>
## **Use cases**

<span id="_1-1-资源分组"></span>
### **Resource grouping**

When creating an EMR cluster or other cloud product resources, you can choose to place the resources in a specified project. In addition, you can later query resources within a project and migrate resources in or out in the resource management console.

<span id="_1-2-按项目授权"></span>
### **Project\-based authorization**

You can grant IAM permissions based on projects. In this case, the project serves as the resource boundary for the IAM policy, and the scope of the policy is limited to the project you specify. Any requests for resources outside the project will be denied.

<span id="_2-为emr集群指定项目"></span>
## **Specify a project for an EMR cluster**


1. Log in to [E-MapReduce Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?).

2. Create a cluster. In Step 3Other settings\-Advanced settings, select the project to which the cluster belongs.

3. Click "Create project" to jump to Access controlproject page to create a new project or manage projects.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd85128fe94c494dbd83c0dc25e24665~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Project creation and management are performed in the access control console. For details, see <a href="https://docs.byteplus.com/en/docs/resourcemanagement/Product_Overview">Resource management (project)</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When creating, expanding, or scaling a cluster, each node in the cluster, including ECS instances, is automatically added to the project to which the cluster belongs.   </div>
   


<span id="_3-emr集群在项目间移入移出"></span>
## Move EMR clusters between projects

You can refer to this operation to move an EMR cluster from the current project to the target project, or move an EMR cluster that has not been added to any project into the target project.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To move resources between projects, log in with the primary account or as an IAM user with project management permissions.</div>


<span id="_3-1-资源移入"></span>
### Resource migration in


1. Log in to .

2. On the project list page, click the target project name to enter the project details page.

3. Select the Resources tab, click the "Migrate in" button, and the migrate\-in resource window will appear.

4. Select "Migrate in from another project", choose the current project of the target EMR cluster, and check the target EMR cluster.


<span id="_3-2-资源移出"></span>
### Resource migration out


1. Log in to .

2. On the project list page, click the target project name to enter the project details page.

3. On the Resources tab, check the target EMR cluster, click the "Migrate out" button, and the migrate\-out resource window will appear.

4. Select the project to which the public IP will be moved out, click the "Confirm" button, and complete the operation.


<span id="_4-管理项目权限"></span>
## Manage project permissions

<span id="_4-1-添加项目权限"></span>
### **Add project permissions**

You can grant project permissions to IAM identities (users, user groups, roles) using either of the following methods. The two methods differ only in management perspective and entry point, but the result is exactly the same.

**Method 1: Grant permissions in the project console**


1. Log in to .

2. On the project list page, click the target project name to enter the project details page.

3. On the Authorization tab, click the "Add authorization" button to open the add authorization window.

4. In the identity selection section, select one or more target identities under the User, User Group, or Role tabs as needed.

5. In the policy selection section, select the target policies as needed.

6. Click the "Confirm" button to complete the operation.


**Method 2: Grant permissions in the identity management console**


1. Go to . To grant project permissions to a specific IAM user, go to that user's details page.

2. On the "Permissions \> Project permissions" tab, click the "Add permission" button to open the add permission window.

3. Select the policies and the project to apply them to as needed, then click the "Confirm" button to complete the operation.


After submission, the IAM identity (user, user group, role) will have the permissions described in the policies for resources within the project.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Compared to ordinary policy authorization, project\-based authorization requires an additional specification of the "project" scope. If not specified, the scope is "global", which includes all resources in the account and any resources added in the future.</div>


<span id="_4-2-修改项目权限"></span>
### **Modify project permissions**

You can modify project permissions for IAM identities (users, user groups, roles) using either of the following methods. The two methods differ only in management perspective and entry point, but the result is exactly the same.

**Method 1: Modify permissions in the project console**


1. Log in to .

2. On the project list page, click the target project name to enter the project details page.

3. On the Authorization tab, click the "Modify permissions" button to the right of the target IAM identity to open the modify permissions window.

4. Select or deselect policies as needed, then click the "Confirm" button to complete the operation.


**Method 2: Modify permissions in the identity management console**


1. Enter the . To modify project permissions for an IAM user, enter that user's details page.

2. On the "Permissions \> Project permissions" tab, click the "Modify scope" button to the right of the target policy. The modify policy scope window will pop up.

3. Select either Global or a specified project as needed, then click the "Confirm" button to complete the operation.


<span id="_4-3-移除项目权限"></span>
### **Remove project permissions**

You need to remove project permissions from an IAM identity (user, user group, or role) by following these two steps.

**Step 1: Remove permissions in the project console**


1. Log in to the .

2. On the project list page, click the target project name to enter the project details page.

3. On the Authorization tab, click the "Remove" button to the right of the target identity. The confirm removal dialog box will pop up.

4. After confirming the information is correct, click the "Remove" button to complete the operation.


**Step 2: Remove permissions in the identity management console**


1. Enter the . Enter the details page.

2. On the "Permissions \> Project permissions" tab, click the "Detach" button to the right of the target policy. The detach permissions dialog box will pop up.

3. After confirming the information is correct, click the "Detach" button to complete the operation.
