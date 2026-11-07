---
title: "Access and Resource Management"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/Access_Control_and_Resource_Management"
---

This document describes how to implement access control and resource management in the TrafficRoute DNS Suite.

<span id="access-management"></span>
## Access management

Identity and Access Management (IAM) is a permission management system provided by BytePlus to control access to cloud resources for different identities. For example, an enterprise can use the admin account to purchase cloud resources and allocate access permissions to different IAM users as needed. The enterprise can allow employees to log in to the console and access cloud resources through IAM users.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following services in the TrafficRoute DNS Suite support access management functionality:</div>



* <div data-tips="true" data-tips-type="tip">BytePlus DNS</div>


* <div data-tips="true" data-tips-type="tip">BytePlus Global Traffic Management (GTM)</div>


* <div data-tips="true" data-tips-type="tip">BytePlus PrivateZone</div>



<span id="admin-account-and-iam-users"></span>
### Admin account and IAM users

When you register with BytePlus, the system creates a admin account for you. The admin account has all permissions to manage BytePlus cloud resources. If you have users who need to perform specific operations on designated cloud resources, you can create IAM user accounts and grant corresponding permissions. When IAM users access BytePlus using their own accounts, they can operate on the cloud resources they have permission to access. In BytePlus, IAM users are also referred to as IAM users. See [BytePlus Console Documentation](https://docs.byteplus.com/en/docs/byteplus-platform/docs-getting-started) to learn how to create IAM users.

<span id="policies"></span>
### Policies

You grant permissions to IAM users through policies. At the same time, you specify the cloud resources that IAM users can operate on by defining the scope of the policy. Policies contain permissions for cloud products. A policy can contain permissions for one cloud product or multiple cloud products. Permissions can be partial or all permissions for a cloud product.

Policies have the following types:


* System default policies: Each BytePlus cloud product has one or more system default policies. These system default policies have predefined permissions for common operation scenarios, making it convenient to authorize IAM users. For example, DNSReadOnlyAccess is a system default policy that includes permissions to read BytePlus DNS resources.

* User custom policies: If system default policies do not meet your needs, you can create custom combinations of permissions.


The TrafficRoute DNS Suite has the following system default policies:


|System default Policy |Description |
|---|---|
|DNSReadOnlyAccess |Read\-only access to BytePlus DNS |
|DNSFullAccess |Full management permissions for BytePlus DNS |
|PrivateZoneReadOnlyAccess |Read\-only access to BytePlus PrivateZone |
|PrivateZoneFullAccess |Full management permissions for BytePlus PrivateZone |
|GTMReadOnlyAccess |Read\-only access to BytePlus Global Traffic Management (GTM) |
|GTMFullAccess |Full management permissions for BytePlus Global Traffic Management (GTM) |


<span id="resource-management"></span>
## Resource management

Resource management is a cloud resource management system provided by BytePlus, commonly used for financial accounting and group operations management scenarios.

The following services in the TrafficRoute DNS Suite support resource management using projects and tags:


* BytePlus PrivateZone: Domains, forwarding rules, outbound endpoints, and inbound endpoints are defined as resources. You can manage resources through projects and tags.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When using projects in BytePlus PrivateZone, note the following:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Because a resource can only belong to one project, if you need to associate multiple types of resources with a project, you need to ensure that all interrelated resources belong to the same project. Otherwise, IAM users without global permissions will not be able to select associated resources or will receive error messages when creating resources. For example:   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When associating a VPC with a domain in Project A, you need to ensure that the VPC is also in Project A.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When changing the project for an endpoint, you need to ensure that the associated forwarding rules are also changed to the same project.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">IAM users without global permissions cannot use cross\-account VPC association and log operation features.   </div>
   


<span id="projects"></span>
### Projects

Projects are a resource grouping management mechanism provided by BytePlus to help users achieve logical resource isolation. You can use projects for project\-based authorization and accounting operations.

For specific usage methods of projects, see [BytePlus Console Documentation](https://docs.byteplus.com/en/docs/byteplus-platform/docs-getting-started).

<span id="tags"></span>
### Tags

Tags consist of a set of key\-value pairs. You can use tags to categorize and aggregate cloud resources from different dimensions.

For specific usage methods of tags, see [BytePlus Console Documentation](https://docs.byteplus.com/en/docs/byteplus-platform/docs-getting-started).
