---
title: "IAM overview"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/IAM_overview"
---

Identity and Access Management (IAM) is a ** free service ** provided by the platform for users. It is a permission management system used to control access to cloud resources for different identities. This service offers access management for resources and helps you improve management efficiency and reduce information leakage.

<span id=".5Li65LuA5LmI5L2_55SoSUFN"></span>
## Why use IAM

To use cloud resources, you need to first [register an account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account). After registration, you obtain an account that is referred to as "Root user". **By default, the root user has full administrative permissions over all resources under it**.

Using only the root user to manage resources may cause the following issues:


* Multiple users use the same root user, making it impossible to identify the actual user.

* The root user has extensive permissions, so any leak would lead to severe consequences.

* Using the root user directly for O&M tasks involves higher risks.


You can avoid the above issues by using IAM features. You can create IAM users, user groups, and roles under the root user. New IAM users, user groups, and roles have no permissions initially. You can grant them appropriate permissions based on actual needs to achieve multi\-identity management and granular permission control. For more features, refer to [IAM overview](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-3).

<span id=".SUFN55u45YWz5LuL57uN"></span>
## IAM\-related information


|Topic |Detailed description |Related documents |
|---|---|---|
|IAM usage process |IAM user: You can authorize IAM users directly or authorize them by adding them to a user group. |[Granting permissions to IAM users to use cloud resources required by ArkClaw](https://docs.byteplus.com/en/docs/ArkClaw/Granting_permissions_to_IAM_users_to_use_cloud_resources_required_by_ArkClaw) |
|IAM policy overview |A policy is a set of permissions described using a syntax structure.<br><br><br>* Policy types: IAM supports two types of policies: **system default policy ** and **custom policy**.<br><br>* Policy syntax structure: IAM policies follow a fixed syntax format, allowing you to create various and custom IAM policies as needed.<br><br>* Policy scope: IAM policies apply to two scopes: **global permissions** and **project\-level ** permissions. |[IAM policy syntax](https://docs.byteplus.com/en/docs/byteplus-platform/docs-what-is-the-policy-syntax) |
