---
title: "Overview"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Projects-Overview"
---

Project management is a resource management approach provided by BytePlus, allowing you to group and manage cloud resources used by different businesses or projects. IAM authorization based on projects (i.e., a group of resources) helps maintain resource independence and data security. It also enables viewing resource consumption bills from a project perspective, facilitating the calculation of cloud resource usage costs.

<span id="cc6ddcd4"></span>
## Application scenarios

<span id="5f0924a6"></span>
### Categorized by business

For instance, if a company has multiple product lines, it can create a separate project for the development, testing, and production environments of each product line. Adding cloud resources to these corresponding projects facilitates resource isolation and calculating cloud resource usage costs.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_71589983e200a4d3a2cd12ce832d49f7.png) </span>

<span id="5589929b"></span>
### Categorized by actual projects

For example, if a company runs different projects across the country, it can create distinct projects on BytePlus for the cloud resources used by each project. This simplifies IAM user permission management and calculating cloud resource usage costs.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_076722e9ffc8d8c2980a4b304c7d63d5.png) </span>

<span id="6e286715"></span>
### Categorized by company hierarchy

For instance, if a company has multiple organizational levels, it can leverage projects for permission control by setting up multi\-level projects. This allows for better management of permissions regarding which personnel from different departments can use specific cloud resources.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fbfb4197323dbdf23a3f8c716cdd9dd3.png) </span>

<span id="07090db9"></span>
## Precautions


* It is not recommended for cloud resources in the current project to be associated with resources from other projects. If such association is necessary, the IAM user must have the relevant permissions for the other project(s) to perform the association operation.

* Associations between cloud resources do not change due to project assignments.

* When an IAM user logs into the console to create or view cloud resources, if they switch to a project for which they have no permissions, they cannot proceed with operations.

* If an IAM user cannot view resources, it might be because the IAM user lacks permissions for the project where those resources reside. Please switch to a project for which you have permissions before viewing.
