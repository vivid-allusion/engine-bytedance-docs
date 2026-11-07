---
title: "IAM overview"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Overview_of_IAM"
---

Identity and Access Management (IAM) is a permission management system and one of the **free services** provided by BytePlus. You can create IAM users for your BytePlus account (main account), and grant IAM users permissions based on specific purposes. This allows you to control access to cloud resources by users with different identities. This way, you can manage resources through access control, increase management efficiency, and reduce information leakage.

<span id=".5Li65LuA5LmI5L2_55SoSUFN"></span>
## Why use IAM

To use BytePlus resources, you need to first register an account on BytePlus. The registered account is your root user on the platform, **which has full administrative permissions for all resources under it by default**.

Using only the root user to manage resources may cause the following issues:


* Multiple users use the same root user, making it impossible to identify the actual user.

* The root user has extensive permissions, so any leak would lead to severe consequences.

* Using the root user directly for O&M tasks involves higher risks.


You can avoid the above issues by using IAM features. You can create IAM users, user groups, and roles under the root user. New IAM users, user groups, and roles have no permissions initially. You can grant them appropriate permissions based on actual needs to achieve multi\-identity management and granular permission control. .

<span id=".SUFN55u45YWz5LuL57uN"></span>
## IAM\-related information


|Introduction |Detailed description |
|---|---|
|IAM\-related concepts |Using IAM for permission management involves many technical terms, such as IAM identities (user, user group, and role), policies, and single sign\-on (SSO). |
|IAM limits |IAM resources are limited by resource quotas. If the quota limit is exceeded, new resources cannot be created. |
|IAM usage process |You can directly grant permissions to IAM users or grant permissions to them by adding them to an IAM user group. |
|IAM policy overview |A policy is a set of permissions described using a syntax structure.<br><br><br>* Policy type: IAM supports two types of policies: **System default policy** and **Custom policy**.<br><br>* Policy syntax structure: IAM policies follow a fixed syntax format, allowing you to create diversified and customized IAM policies as needed.<br><br>* Policy Scope: IAM policies have two scopes: **global permission** and **project permission**. |
