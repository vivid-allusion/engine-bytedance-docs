---
title: "IAM overview"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/IAM_overview01"
---

BytePlus Identity and Access Management (IAM) is a **free** permission management service that controls access to cloud resources for different identities. This service helps you improve permission management efficiency and minimize the risk of data leaks.

<span id="1Ef5F7sZ"></span>
## Why use IAM

To use cloud resources, you need to first [register an account](https://docs.byteplus.com/en/docs/6261/64925), which is known as a root user. **By default, the root user has full administrative permissions over all resources under it.** 

Using only the root user to manage resources may cause the following issues:


* Multiple users use the same root user, making it impossible to identify the actual user.

* The root user has extensive permissions, so any leak would lead to severe consequences.

* Using the root user directly for O&M tasks involves higher risks.


With the IAM feature, you can avoid the above issues by creating IAM users, user groups, and roles under the root user. The newly created IAM users, user groups, and roles have no permissions initially and can be granted appropriate permissions as needed for purposes such as multiple identity management and fine\-grained permission control. For more features, see [Product introduction](https://docs.byteplus.com/en/docs/6257/64959).

<span id="fOlQAofH"></span>
## IAM\-related information


|Topic |Detailed description |Related documents |
|---|---|---|
|IAM\-related concepts |Using IAM for permission management involves many technical terms, such as IAM identities (user, user group, and role), policies, and single sign\-on (SSO). |[Concepts](https://docs.byteplus.com/en/docs/6257/64963) |
|IAM limits |IAM resources are limited by resource quotas. If the quota limit is exceeded, new resources cannot be created. |[Limits](https://docs.byteplus.com/en/docs/6257/1285191) |
|IAM usage process |IAM user: You can authorize IAM users directly or authorize them by adding them to a user group. |[Authorizing IAM users to use ArkClaw Enterprise](https://docs.byteplus.com/en/docs/ArkClaw/Authorizing_an_IAM_user_to_use_ArkClaw_Enterprise) |
|IAM policy overview |A policy is a set of permissions described using a syntax structure.<br><br><br>* Policy types: IAM supports two types of policies: **system default policy ** and **custom policy**.<br><br>* Policy syntax structure: IAM policies follow a fixed syntax format, allowing you to create various and custom IAM policies as needed.<br><br>* Policy scope: IAM policies apply to two scopes: **global permissions** and **project\-level ** permissions. |[IAM policy syntax](https://docs.byteplus.com/en/docs/6257/65059) |
