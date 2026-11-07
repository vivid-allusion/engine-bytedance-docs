---
title: "IAM overview"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Overview-2"
---

Identity and Access Management (IAM) is a **free service** provided by the platform for customers. It is a permission management system that controls different identities' access rights to cloud resources. It enables decentralized resource management, improves management efficiency, and reduces the risk of information leakage.

<span id=".5Li65LuA5LmI5L2_55SoSUFN"></span>
## Why use IAM

To use cloud resources, you first need to register an account. This is the main account, which **by default has full management permissions over all resources under it**.

Using only the main account to manage resources may cause the following issues:


* Multiple people share the main account for actions, making it impossible to identify the actual user.

* The main account has extensive permissions, so any exposure would have severe consequences.

* Using the main account directly for operation and maintenance (O&M) tasks involves higher risks.


You can address these concerns by using the IAM feature. Under the Root Account, you can create IAM users, user groups, and roles. Newly created IAM users, user groups, and roles initially have no permissions. You can grant appropriate permissions based on their intended use cases, enabling multi\-identity management, granular permission controls, and more.

<span id=".SUFN55u45YWz5LuL57uN"></span>
## IAM topics


|Topic |Description |Related documentation |
|---|---|---|
|IAM terms |Using IAM for permission management involves many technical terms, such as IAM identities (user, user group, or role), policies, and single sign\-on (SSO). |[Terms](https://docs.byteplus.com/en/docs/6257/64963) |
|IAM limits |IAM resources are limited by resource quotas. If exceeding the quota limit, you cannot create new resources. |[Limits](https://docs.byteplus.com/en/docs/6257/1285191) |
|IAM usage process |You can authorize IAM users directly or authorize them by adding them to a user group. |* [Create a user and authorize it](https://docs.byteplus.com/en/docs/6257/94013)<br><br>* [Grant user API key management permissions](https://docs.byteplus.com/en/docs/6257/1319865) |
|IAM policy overview |A policy is a set of permissions described using a syntax structure.<br><br><br>* Policy type: IAM supports two types of policies: **System default policy** and **Custom policy**.<br><br>* Policy syntax structure: IAM policies follow a fixed syntax format, allowing you to create diversified and customized IAM policies as needed.<br><br>* Policy scope: IAM policies have two scopes: **Global** and **Designated projects**. |* [Policy Grammar > Basic structure](https://docs.byteplus.com/en/docs/6257/65059)<br><br>* [VPN Connect IAM policy types](https://docs.byteplus.com/en/docs/vpn/VPN-IAM-policy-type) |
