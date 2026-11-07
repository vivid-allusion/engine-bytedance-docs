---
title: "IAM overview"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/IAM_overview"
---

Identity and Access Management (IAM) is a **free service** provided by the platform for users. It is a permission management system used to control access to cloud resources for different identities. This service offers access management for resources and helps you improve management efficiency and reduce information leakage.

<span id="5r5PYSXx"></span>
## Why use IAM

To use cloud resources, you need to first [register an account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account). After registration, you obtain an account that is referred to as "Root Account". **By default, the root account has full administrative permissions over all resources under it.** 

Using only the root account to manage resources may cause the following issues:


* Multiple users use the same root user, making it impossible to identify the actual user.

* The root user has extensive permissions, so any leak would lead to severe consequences.

* Using the root account directly for O&M tasks involves higher risks.


You can avoid the above issues by using IAM features. You can create IAM users, user groups, and roles under the root account. New IAM users, user groups, and roles have no permissions initially. You can grant them appropriate permissions based on actual needs to achieve multi\-identity management and granular permission control. For more features, refer to [IAM overview](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-3).

<span id="OBbkuldc"></span>
## IAM\-related information


|Topic |Detailed description |Related documents |
|---|---|---|
|IAM usage process |IAM user: You can authorize IAM users directly or authorize them by adding them to a user group. |[Creating users and authorizing them](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user) |
|IAM policy overview |A policy is a set of permissions described using a syntax structure.<br><br><br>* Policy type: IAM supports two types of policies: **System default policy** and **Custom policy**.<br><br>* Policy syntax structure: IAM policies follow a fixed syntax format, allowing you to create diversified and customized IAM policies as needed.<br><br>* Policy scope: IAM policies apply two scopes: **Global permissions** and **Project\-level permissions**. |* [IAM policy syntax](https://docs.byteplus.com/en/docs/byteplus-platform/docs-what-is-the-policy-syntax)<br><br>* [AgentKit IAM policy types](https://docs.byteplus.com/en/docs/agentkit/AgentKit_IAM_policy_types) |
