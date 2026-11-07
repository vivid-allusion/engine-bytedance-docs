---
title: "IAM Overview"
product: "Vortex IP"
product_code: "gavi-sept-test1"
source: "https://docs.byteplus.com/en/docs/gavi-sept-test1/IAM_Overview"
---

Identity and Access Management (IAM) is a system for permission management and is one of the **free services** provided to customers. You can create IAM users for your Account (root user) and grant them corresponding permissions based on different purposes, controlling access to cloud resources for different identities, achieving decentralized resource management, enhancing management efficiency, and reducing the risk of information leakage.

<span id=".5Li65LuA5LmI5L2_55SoSUFN"></span>
## Why use IAM?

To use BytePlus resources, you need to [Create Account](https://docs.byteplus.com/en/docs/6261/64925) first. After the registration is completed, you will get an account, which is the "main account". The **main account has full management rights for all resources under the account by default**.

Using only the root user to manage resources may lead to the following issues:


* Multiple users perform actions using the root user, making it impossible to distinguish the specific user.

* The main account authority is very large, and once leaked, it will have a great impact.

*  Operation and maintenance directly performed using the root user carry high risks.


With the IAM feature, you can avoid the above issues by creating IAM users, user groups, and roles under the root user. The newly created IAM users, user groups, and roles have no permissions initially, and you can grant the newly created IAM users, user groups, and roles appropriate permissions based on actual purposes, thus achieving multiple identity management, fine\-grained permission control, etc. For more features, please refer to [Product Introduction](https://docs.byteplus.com/en/docs/6257/64959).

<span id=".SUFN55u45YWz5LuL57uN"></span>
## Introduction to IAM


|Introduction |Description |Related documents |
|---|---|---|
|IAM Concepts |Using IAM for permission management involves many professional terms, such as: IAM Identity (user, user group, role), policy, Single Sign\-On (SSO). |[Concepts](https://docs.byteplus.com/en/docs/6257/64963) |
|Limits |IAM resources are limited by quota. If the resources exceed the quota limit, new resources cannot be created. |[ Limits](https://docs.byteplus.com/en/docs/6257/1285191) |
|IAM Usage Process |You can directly authorize IAM users or authorize them by adding them to a user group. |* [Create a user and authorize](https://docs.byteplus.com/en/docs/6257/94013)<br><br>* [Grant users management permissions for API access keys](https://docs.byteplus.com/en/docs/6257/1319865) |
|IAM Policy Overview |A policy is a set of permissions described by a syntax structure.<br><br><br>* Policy types: IAM supports two types of policies, **system default policy** and **custom policy**.<br><br>* Policy Syntax: IAM policies have fixed syntactic patterns, and you can create more diverse and comprehensive IAM policies as needed.<br><br>* Policy Scope: IAM policies have two scopes: **global permissions** and **project permissions**. |* [IAM Policy Syntax](https://docs.byteplus.com/en/docs/6257/65059)<br><br>* [Vortex IP's IAM policy Type](https://docs.byteplus.com/en/docs/gavi-sept-test1/Types_of_IAM_policies_for_Vortex_IP) |
