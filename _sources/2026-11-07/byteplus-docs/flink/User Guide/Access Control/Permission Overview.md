---
title: "Permission Overview"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Permission_Overview"
---

This article provides basic information on project resource permission management for BytePlus Flink to help you manage permissions with fine granularity in your projects more conveniently.

<span id="ed07cad1"></span>
## Background Information

BytePlus Flink incorporates project and resource\-level permission control strategies based on the IAM authentication system. Please review the following concepts in the table below, which can effectively help you understand the project permission control mechanism in Flink.


|**Noun** |**Description** |
|---|---|
|Main account (Account) |The main account is the owner of the resource, and the username is generally used as the account's login identifier.<br><br>Service resources can be freely operated and accessed by their main accounts. |
|Sub\-user (User) |Sub\-users, also known as IAM users, are authorized entities under the main account and are a type of resource belonging to the main account.<br><br>When IAM users are created by the main account, they are set with passwords and access keys, enabling them to log into the console. By default, IAM users have no permissions and do not own any service resources. |
|Project Manager |The project manager is the sole responsible person for the project and has all the permissions within the project.<br><br>The project manager is fundamentally also a member of the project and supports the transfer of managerial permissions to other members. |
|Member |After IAM users are imported into the BytePlus Flink console, they can be added as project members.<br><br>The project manager is responsible for adding project members and associating related roles. Once members are associated with a role, they possess the permissions of that role. |
|Role |A role is a set of permission policies, which can also be understood as a group of users with the same permissions.<br><br>The project has preset four roles: Project_Admin, Project_Dev, Project_OPS, and Project_Member, and also supports adding custom roles.<br><br><br>* Project_Admin: Project administrator. Mainly responsible for managing project members, roles and policies, as well as full permissions for resource pool management.<br><br>* Project_Dev: Task developer. Has the necessary permissions for developing tasks, such as creating, debugging, and deleting tasks.<br><br>* Project_OPS: Task operations personnel. Has permissions for starting, stopping, onlining, and offlining tasks.<br><br>* Project_Member: Ordinary project user. You only have the permission to view project resources such as tasks and resource pools. |
|Strategy |As objects like resources, metadata, and services are used in the project, the system automatically creates corresponding preset system policies. It also supports adding custom fine\-grained permission policies.<br><br>Policies need to be associated with roles, and then roles with members, thus implementing member access control. |


<span id="e76d59a2"></span>
## Project Isolation

Only the **main account** can create projects in the project console and import projects in the Flink console. Different projects are isolated and independent from each other.

The main account has permissions over all its projects and project resources; project leaders and members only have permissions related to their current project.

<span id="a1f011d2"></span>
## Project Permission Control

The permission model adopts the RBAC (Role Based Access Control) model, which introduces the concept of "role" between visitors and resources. Roles are associated with resource permissions, and visitors are then indirectly authorized through associated roles.

The main account can appoint a project leader when creating a project.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7d15034afe3dd7d7ed82cb2ef5cf47a9.png) </span>

The project leader is the sole responsible person for the current project and manages the project members, roles, and policies.

There are two methods for project permission management: one is to directly associate users with preset system roles; the other is to create custom roles, bind certain resources and service policies to these roles, and then associate them with target members.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8d7e99d1369666fa33695b98398bcab8.png) </span>
