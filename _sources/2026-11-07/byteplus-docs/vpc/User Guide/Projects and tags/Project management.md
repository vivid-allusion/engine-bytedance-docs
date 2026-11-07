---
title: "Project management"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Managing-projects"
---

<span id=".566A5LuL"></span>
## **Introduction​** 

Project management is a resource management approach provided by the platform, allowing you to group and manage cloud resources used by different businesses or projects. IAM authorization based on projects (i.e., a group of resources) helps maintain resource independence and data security. It also enables viewing resource consumption bills from a project perspective, facilitating the calculation of cloud resource usage costs. 

The Virtual Private Cloud (VPC) supports the following project management features:


* Virtual Private Cloud instance

* Subnet

* Route Table

* Network interface

* Security group

* Network ACL

* HAVIP

* Prefix List

* Flow Log

* Traffic Mirror


<span id="bQpZIsWv"></span>
## **Precautions**


* Parent\-child resources:

   * When creating a subnet, it is not supported to specify a project for it. The project defaults to being the same as its associated VPC. However, when the parent VPC Modifies the project, its subnets' project affiliation does not automatically update. If synchronization updates are required, you must configure parent\-child resource grouping settings for both the VPC and its subnets.

   * When you create a High\-Availability Virtual IP Address (HAVIP), the project cannot be specified but is fixed to that of the subnet by default. When changing the project of a subnet, the project association of the High\-Availability Virtual IP Address (HAVIP) will synchronize automatically. It is not supported to change the project of an HAVIP separately.

   * When adding a route entry, the project cannot be specified but is fixed to that of the route table by default. When changing the project of a route table, the project association of route entries will synchronize automatically. It is not supported to change the project of route entries separately.

* A resource can only belong to one project, and the association relationship between resources does not change due to project assignment.

* If resources from different projects need to be associated, the IAM user must simultaneously have permissions for the relevant projects. For example, if an Elastic Compute Service (ECS) instance in project A is bound to an EIP from project B, the IAM user needs permissions for both projects A and B. For authorization, see Add project permission.
