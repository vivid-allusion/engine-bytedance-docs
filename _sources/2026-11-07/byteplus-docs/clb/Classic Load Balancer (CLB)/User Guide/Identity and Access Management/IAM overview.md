---
title: "IAM overview"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/IAM-Overview"
---

Identity and Access Management (IAM) is a permission management system and is one of the **free services** provided by the platform. You can create an IAM user for the BytePlus Account (main account), and grant IAM users corresponding permissions according to different purposes, control the access rights of different identities to cloud resources, realize decentralized management of resources, improve management efficiency, and reduce the risk of information leakage.

<span id=".5Li65LuA5LmI5L2_55SoSUFN"></span>
## Why use IAM?

Before using resources, you need to perform account registration on the platform. Once registered, you'll obtain a BytePlus Account, which is the **root user**. **The root user has full management permissions** for all resources within the account.

Using only the root user to manage resources may lead to the following issues:


* Multiple users perform actions using the root user, making it impossible to distinguish the specific user.

* The main account authority is very large, and once leaked, it will have a great impact.

* Using the root account to directly carry out operations and maintenance operations is risky.


You can avoid the above problems through the IAM function. You can create IAM users, user groups, and roles under the main account. Newly created IAM users, user groups, and roles do not have any permissions. You can grant the corresponding permissions to create IAM users, user groups, and roles according to the actual use. Realize multiple identity management, refined permission control, etc. For more features, refer to .

<span id=".SUFN55u45YWz5LuL57uN"></span>
## IAM Identity Introduction


|Introduction |Description |
|---|---|
|IAM Concepts |Using IAM for permission management involves many professional terms, such as: IAM Identity (user, user group, role), policy, Single Sign\-On (SSO). |
|Limits |IAM resources are limited by quota. If the resources exceed the quota limit, new resources cannot be created. |
|IAM Usage Process |You can directly authorize IAM users or authorize them by adding them to a user group. |
|IAM Policy Overview |A policy is a set of permissions described by a syntax structure.<br><br><br>* Policy types: IAM supports two types of policies, **system default policy** and **custom policy**.<br><br>* Policy Syntax: IAM policies have fixed syntactic patterns, and you can create more diverse and comprehensive IAM policies as needed.<br><br>* Policy Scope: IAM policies have two scopes: **global permission** and **project permission**. |


&nbsp;

&nbsp;
