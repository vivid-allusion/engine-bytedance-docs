---
title: "IAM overview"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/IAM_Overview"
---

Identity and Access Management (IAM) is a permission management system and one of the **free services** provided by BytePlus. You can create IAM users for your BytePlus account (root account) and grant them appropriate permissions based on different purposes to control access to cloud resources by different identities. This achieves decentralized resource management, improves management efficiency, and reduces the risk of information leakage.

<span id=".5Li65LuA5LmI5L2_55SoSUFN"></span>
## Why use IAM

Before using BytePlus resources, you need to register an account. The registered account is the root user, which by default has full management permissions for all resources under the account.

Using only the main account to manage resources may cause the following issues:


* Multiple people share the main account for actions, making it impossible to identify the actual user.

* The main account has extensive permissions, so any exposure would have severe consequences.

* Using the main account directly for operation and maintenance (O&M) tasks involves higher risks.


You can avoid the above issues through the IAM feature. Under the root user, you can create IAM users, user groups, and roles. Newly created IAM users, user groups, and roles have no permissions. You can grant corresponding permissions to the created IAM users, user groups, and roles based on actual needs, achieving multi\-identity management and fine\-grained permission control. For more features, see [IAM Overview](https://docs.byteplus.com/en/docs/6257/64959).

<span id=".SUFN55u45YWz5LuL57uN"></span>
## IAM topics


|Topic |Description |Related documents |
|---|---|---|
|IAM terms |Using IAM for permission management involves many technical terms, such as IAM identities (user, user group, or role), policies, and single sign\-on (SSO). |[Terms](https://docs.byteplus.com/en/docs/6257/64963) |
|IAM limits |IAM resources are limited by resource quotas. If the quota limit is exceeded, new resources cannot be created. |[Limits](https://docs.byteplus.com/en/docs/6257/1285191) |
|IAM usage process |You can authorize IAM users directly or authorize them by adding them to a user group. |* [Create a user and authorize it](https://docs.byteplus.com/en/docs/6257/94013)<br><br>* [Grant user API key management permissions](https://docs.byteplus.com/en/docs/6257/1319865) |
|IAM policy overview |A policy is a set of permissions described using a syntax structure.<br><br><br>* Policy type: IAM supports two types of policies: **System default policy** and **Custom policy**.<br><br>* Policy syntax structure: IAM policies follow a fixed syntax format, allowing you to create diversified and customized IAM policies as needed.<br><br>* Policy scope: IAM policies apply two scopes: **Global** and **Designated projects**. |* [Basic structure](https://docs.byteplus.com/en/docs/6257/65059)<br><br>* [NAT Gateway IAM policy types](https://docs.byteplus.com/en/docs/natgateway/NAT_gateway_IAM_policy_type) |
