---
title: "IAM overview"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-IAM-overview"
---

Identity and Access Management (IAM) is a **free service**. It is a permission management system designed to control access permissions to cloud resources for different identities. This allows decentralized resource management, improves management efficiency, and reduces the risk of information leakage.

<span id="为什么使用IAM"></span>
## Why use IAM?

To use BytePlus resources, you need to [Create Account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user) first. Once registered, you will get a BytePlus account. The registered account is the "root user", and **the root user by default has complete management permissions for all resources under the account**.

Using only the root user to manage resources may lead to the following issues:


* Multiple users perform actions using the root user, making it impossible to distinguish the specific user.

* The main account authority is very large, and once leaked, it will have a great impact.

* Operation and maintenance directly performed using the root user carry high risks.


With the IAM feature, you can avoid the above issues by creating IAM users, user groups, and roles under the root user. The newly created IAM users, user groups, and roles have no permissions initially, and you can grant the newly created IAM users, user groups, and roles appropriate permissions based on actual purposes, thus achieving multiple identity management, fine\-grained permission control, etc. For more features, please refer to [Product Introduction](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-3).

<span id="IAM相关介绍"></span>
##
