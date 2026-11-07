---
title: "Project management"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-Project-Management"
---

## Introduction​

Project management is a resource management approach provided by the platform, allowing you to group and manage cloud resources used by different businesses or projects. IAM authorization based on projects (i.e., a group of resources) helps maintain resource independence and data security. It also enables viewing resource consumption bills from a project perspective, facilitating the calculation of cloud resource usage costs.

## Precautions

* Resources supported by NLB for project management include: NLB instances and server groups.

   > **tip**

   > As a sub\-resource of NLB instances, listeners cannot be assigned to a specific project during creation. Their project defaults to the NLB instance. When NLB instances are moved into or out of projects, the listeners' projects change synchronously. Moving the listeners into or out of projects independently is not supported.

* When NLB instances are moved into or out of a project, the project of the Elastic IP (EIP) created synchronously with the NLB instance changes correspondingly. (After moving, you are advised to wait for a few seconds before checking whether the projects of the NLB instance and its associated EIP are consistent.).

* A resource can belong to only one project.

* Associations between resources do not change due to project assignments.

* To associate resources from multiple projects, you must have permissions for all projects involved. For example, to attach an NLB instance in Project A to the EIP of Project B, you must have permissions for both Projects A and B. For more information on authorization, refer to Adding project permissions.

## Search for instances by project

1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the top navigation bar, select Region, then select the project according to the instructions below.

   * Select All resources to view all resources under the current account.

   * Select a specific project to view all resources associated with that project.

   * Click Manage projects to redirect to the project list for project management.

   > **tip**

   * > When logging in with a main account or an IAM user, the system will display all resources under the account by default.

   * > If your IAM user has not been granted global permissions, selecting **All Resources** will not display the complete resource list. Please switch projects or contact the main account for authorization.
