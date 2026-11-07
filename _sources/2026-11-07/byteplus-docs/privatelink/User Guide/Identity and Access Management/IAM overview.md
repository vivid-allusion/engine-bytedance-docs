---
title: "IAM overview"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Permission-management-01"
---

Identity and Access Management (IAM) is a permission management system and one of the free services provided by BytePlus to customers. You can create IAM users for your account (root user) and grant them corresponding permissions based on different purposes, controlling access to cloud resources for different identities, achieving decentralized resource management, enhancing management efficiency, and reducing the risk of information leakage.

<span id=".5Li65LuA5LmI5L2_55SoSUFN"></span>
## Why use IAM

To use BytePlus resources, you first need to register an account on BytePlus. After registration, you will obtain a BytePlus account, which is the root user. The **root user has full administrative permissions for all resources under this account by default**.

Using only the root user to manage resources may cause the following issues:


* Multiple people share the root user for actions, making it impossible to identify the actual user.

* The root user has extensive permissions, so any exposure would have severe consequences.

* Using the root user directly for operation and maintenance (O&M) tasks involves higher risks.


You can address these concerns by using the IAM feature. Under the Root User, you can create IAM users, user groups, and roles. Newly created IAM users, user groups, and roles initially have no permissions. You can grant appropriate permissions based on their intended use cases, enabling multi\-identity management, granular permission controls, and more. 

<span id=".SUFN55u45YWz5LuL57uN"></span>
## IAM topics


|Topic |Description |
|---|---|
|IAM terms |Using IAM for permission management involves many technical terms, such as IAM identities (user, user group, or role), policies, and single sign\-on (SSO). |
|IAM limits |IAM resources are limited by resource quotas. If exceeding the quota limit, new resources cannot be created. |
|IAM usage process |You can authorize IAM users directly or authorize them by adding them to a user group. |
|IAM policy overview |A policy is a set of permissions described using a syntax structure.<br><br><br>* Policy type: IAM supports two types of policies: **System default policy** and **Custom policy**.<br><br>* Policy syntax structure: IAM policies follow a fixed syntax format, allowing you to create diversified and customized IAM policies as needed.<br><br>* Policy scope: IAM policies apply two scopes: **Global** and **Designated projects**. |
