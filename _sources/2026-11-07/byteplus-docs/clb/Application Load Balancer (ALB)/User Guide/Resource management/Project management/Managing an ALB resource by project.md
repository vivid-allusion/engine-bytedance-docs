---
title: "Managing an ALB resource by project"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Using-projects-to-manage-ALB-resources"
---

Project management is a resource management approach provided by BytePlus, allowing you to group and manage cloud resources used by different projects. Project advantages:


* Projects provide combined and hierarchical management manners for cloud resources.​ Based on your business needs, you can deploy cloud resources into the specified project when creating them. After authorizing IAM users based on projects, you can manage cloud resources by group.

* Resources and permissions are isolated across projects. This provides flexible resource management and access control while maintains resource independence and data security.

* You can view resource bills at the project level to facilitate calculating cloud resource costs.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Application Load Balancer (ALB) resources that support project management include ALB instances, listeners, server groups, health check templates, Identity and Access Management (IAM) policy groups, customization templates, and certificates.

* A resource can belong to only one project.

* Associations between resources do not change due to project assignments.

* To associate resources from multiple projects, you must have permissions for all projects involved. For example, to associate an elastic IP address (EIP) from Project B with an instance in Project A, you must have permissions for both Project A and Project B. 


<span id=".YWxiLeeahOmhueebrueuoeeQhg=="></span>
## ALB project management

Common actions in ALB project management:


|SN |Feature |Description |
|---|---|---|
|1 |Create project |Create a project to manage ALB resources. |
|2 |Add project permission for an IAM user |Authorize project permission for IAM users belonging to the root account. |
|3 |Create ALB resource |You can use an IAM account to create ALB resources. This example demonstrates creating an ALB instance. |
|4 |Move ALB resources into or out of a project |You can move ALB resources into or out of a project when the resources' project changes. |


<span id=".6YCa6L-H6aG555uu5pCc57SiLWFsYi3otYTmupA="></span>
## Search for ALB resources by project


1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the region and choose the project based on the description below.

   * Select All resources to view all resources under the current account.

   * Select a specific project to view all resources associated with that project.

   * Click Manage projects to redirect to the project list for project management.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When you log in with a root account or an IAM user, the system defaults to display resources under the <strong>default</strong> project of that account.</div>


* <div data-tips="true" data-tips-type="tip">If an IAM user is not granted <strong>Global</strong> permissions or the system fails to display all resources under the account after <strong>All Resources</strong> is selected, switch to another project or contact the root account to obtain the required permissions.</div>
