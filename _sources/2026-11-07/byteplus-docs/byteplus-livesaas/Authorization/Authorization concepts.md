---
title: "Authorization concepts"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/Authorization_concepts"
---

BytePlus Live provides a comprehensive permission management system that enables you to grant users specific permissions, making it easier for multiple individuals to collaboratively manage your live streaming platform. This feature is particularly useful when you need to flexibly allocate and manage access to resources across different departments or employees within your enterprise.

Specifically, BytePlus Live allows you to manage IAM users, organizations, and roles, including assigning users to organizations and roles. This enables more granular and flexible management of IAM user permissions, ensuring that users have appropriate access to the resources they need. This document explains the key concepts of authorization.

<span id="6d6910f8"></span>
## Admin account

In BytePlus, the admin account is identified as the root user. The admin account is the owner of purchased BytePlus cloud resources, and is responsible for resource measurement and resource billing. By default, the admin account is granted all permissions.

<span id="31a80d12"></span>
## Subaccount (IAM User)

A subaccount, also known as an IAM user, is created by the admin account or permission\-granted users. If a user is assigned multiple roles, they have the permissions defined in these roles. Specifically,


* If no overlapping permissions exist between roles, the user has all the permissions defined in these roles. For example, User A is assigned Role A with "Live control \> Edit" permission and Role B with "Producer \> View only" permission. Then, User A has both "Live control \> Edit" and "Producer \> View only" permissions.

* If overlapping permissions exist between roles, the user has the most permissive one among these roles. For example, User A is assigned Role A with "Live control \> Edit" permission and Role B with "Live control \> View only" permission. Then, User A has the Live control \> Edit permission.


Each user can belong to only one organization but can be assigned multiple roles, as shown below.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8a0d9680033041fa8769bcd179f3f07e~tplv-goo7wpa0wc-image.image) </span>

<span id="dd9ec1c5"></span>
## Organization

A collection of users. Departments or subsidiaries of an enterprise can be divided into different organizations, which isolate resources between organizations and allow for the independent management of resources created by users within each organization.

All live rooms created by users within an organization belong to that organization. For example, if User A has "Live control \> Edit" permission and Organization 1 is set as the visible scope, then User A will have edit permission for the Live control page of all live rooms created by users in Organization 1.

<span id="680af609"></span>
## Role

A collection of permissions. You can define different permissions in a role and each role can be assigned to multiple users.
