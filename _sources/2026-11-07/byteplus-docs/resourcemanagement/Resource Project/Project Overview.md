---
title: "Project Overview"
product: "Byteplus Resource Management"
product_code: "resourcemanagement"
source: "https://docs.byteplus.com/en/docs/resourcemanagement/Project_Overview"
---

Project is a grouping mechanism provided by BytePlus to help achieve logical resource isolation. You can use resource projects for management operations such as project\-based authorization and bill management.

<span id="benefits"></span>
## Benefits

As a common cloud resource management tool, resource project offer the following benefits:


* **Improved management efficiency**: Once resources are grouped, you can manage them as projects for O&M, permission management, and bill management. This eliminates the need to handle individual resources separately.

* **Reduced O&M risks**: A project acts as a container for multiple resources, and a resource can belong to only one project. This ensures logical isolation and data security while preventing conflicts caused by duplicate management of the same resource.


<span id="project-resource-management"></span>
## Project resource management

For both newly created and existing resources, the following methods are recommended for project\-based resource management:


* **Newly created resources**: When you create resources by using cloud service consoles or calling APIs, specify the corresponding project to which the resources belong. If no project is selected, the resource is assigned to the system default project (default). Note that the default project is predefined by the system and cannot be deleted or renamed.

* **Existing resources**: You can use the project management feature of the [resource project console](https://console.byteplus.com/iam/resourcemanage/project) or call APIs to manage existing resources by moving them from one project to another.


<span id="project-permission-management"></span>
## Project permission management

Project permissions can be managed based on the identity, policy, and project dimensions:


* **Identity\-based authorization**: Grant permissions to users, roles, or user groups. If no project is specified, the authorization applies to all resources under the account. Otherwise, it applies only to the specified project.

* **Policy\-based authorization**: Assign specific policies to users, roles, or user groups. If no project is specified, the authorization applies to all resources under the account. Otherwise, it applies only to the specified project.

* **Project\-based authorization**: Assign users, roles, or user groups to a specific project, granting them permission to manage resources within that project.


<span id="submit-feedback"></span>
## Submit feedback

Only cloud services and resource types that support project management can be managed by using the project feature. If you find that a resource cannot be managed under a project, you can submit a work order in Work order center.

&nbsp;
