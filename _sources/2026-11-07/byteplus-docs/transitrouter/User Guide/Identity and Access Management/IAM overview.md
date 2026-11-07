---
title: "IAM overview"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Permission-management-01"
---

Identity and Access Management (IAM) is a free system for permission management. You can create IAM users under your root account and grant them appropriate permissions based on their specific purposes. This enables controlled access to cloud resources for different identities, facilitates delegated management of resources, improves administrative efficiency, and mitigates the risk of information exposure.

<span id=".5Li65LuA5LmI5L2_55SoSUFN"></span>
## Why use IAM

To use cloud resources, you must first register an account on the platform. After registration, you will obtain a cloud account, which is the root account. **The root account has full administrative permissions over all resources under it by default**.

Using only the root account to manage resources may cause the following issues:


* Multiple people share the root account for actions, making it impossible to identify the actual user.

* The root account has extensive permissions, so any exposure would have severe consequences.

* Using the root account directly for operation and roottenance (O&M) tasks involves higher risks.


You can avoid the above problems through the IAM function. You can create IAM users, user groups, and roles under the root account. Newly created IAM users, user groups, and roles do not have any permissions. You can grant the corresponding permissions to create IAM users, user groups, and roles according to the actual use. Realize multiple identity management, refined permission control, etc.

<span id=".SUFN55u45YWz5LuL57uN"></span>
## IAM topics


|Topic |Description |
|---|---|
|IAM terms |Using IAM for permission management involves many technical terms, such as IAM identities (user, user group, or role), policies, and single sign\-on (SSO). |
|IAM limits |IAM resources are limited by resource quotas. If exceeding the quota limit, you cannot create new resources. |
|IAM usage process |You can authorize IAM users directly or authorize them by adding them to a user group. |
|IAM policy overview |A policy is a set of permissions described using a syntax structure.<br><br><br>* Policy type: IAM supports two policy types: **System default policy** and **Custom policy**.<br><br>* Policy syntax structure: IAM policies follow a fixed syntax format, allowing you to create diversified and customized IAM policies as needed.<br><br>* Policy scope: IAM policies apply two scopes: **Global** and **Designated projects**. |
