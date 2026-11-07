---
title: "Access control"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/identity_and_access_management"
---

RDS for PostgreSQL supports multi\-identity permission control through a multi\-user permission management system \- Identity and Access Management (IAM). IAM improves the security of operation and maintenance and the products integrated on the client side and the server side to guarantee the compliance and safety of coordinated service calls. This topic describes how to use IAM to manage RDS for PostgreSQL resources, permissions, and identities.

<span id=".5Z-65pys5qaC5b-1"></span>
## Basic concepts

Basic concepts in access control include the following:


* **User** A user is an identity in access control, created by an account (Account) or a user with permissions. After a user is granted permissions (Policy), they can log in to the console or use an Access Key to call an API to access cloud resources. An account (also known as the primary account) can be regarded as a special user (called the root user), owning cloud service resources and serving as the subject for resource metering and billing. The primary account has all permissions under the account by default.

* **User group** A user group is a collection of users. A user can belong to multiple user groups. After a user group is associated with a policy, users within the group will also have the corresponding permissions granted by the policy.

* **Role** a role is an identity within the IAM System whose permissions are defined by the associated policy or policies. Roles are typically used to grant trust for account permissions, allowing the trusted entities to access account resources.

* **Policy** a policy is a description of privileges. IAM provides **identity\-based policies and resource\-based policies**. Users, user groups, and roles must be granted permissions by associating policies. IAM supports two types of policies: system preset policies and custom policies.

* **Project** a project is a virtual concept that includes a set of resources, users, and roles. A project allows you to view and manage a group of resources in a unified manner and control the permissions of users and roles to these resources.


<span id=".6Lqr5Lu9566h55CG"></span>
### Identity management

Identity and Access Management provides three identity types: users, user groups, and roles, which can be managed based on different identity dimensions according to the actual business needs. For example, in scenarios with few and fixed users, management can be done by user or role dimension. In scenarios with many users and frequent changes, management can be done by user group dimension.


* [Creating a user](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user)

* [Creating a user group](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user-group)

* [Creating a role](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-role)


<span id=".6LWE5rqQ566h55CG"></span>
## Resource management

To facilitate permission and consumption management of resources, use the project management feature of resource management to add different resources to different projects.


* [Creating a project](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-project)

* [Add instance to project](https://docs.byteplus.com/en/docs/RDS_for_PG/adding_an_instance_to_a_project)


<span id=".5p2D6ZmQ566h55CG"></span>
## Permissions management

&nbsp;

After completing identity management and resource management deployment, authorize selected identities to resources (projects).

[Project permission management](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Permission_Management)

&nbsp;

&nbsp;
