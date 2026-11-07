---
title: "IAM overview"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Identity-and-access-management"
---

Identity and Access Management (IAM) is a permission management system and one of the **free services** provided by BytePlus. You can create IAM users for your BytePlus account (root account) and grant them appropriate permissions based on different purposes to control access to cloud resources by different identities. This achieves decentralized resource management, improves management efficiency, and reduces the risk of information leakage.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, only Direct Connect Connection and Direct Connect Gateway support project management capability. Virtual Interface does not support this capability yet.</div>


<span id=".5Li65LuA5LmI5L2_55SoSUFN"></span>
## Why use IAM

To use BytePlus resources, you need to first [register an account](https://docs.byteplus.com/en/docs/6261/64925). After registration, you obtain a BytePlus account that is referred as "Root User". **By default, the root user has full administrative permissions over all resources under it**.

Using only the main account to manage resources may cause the following issues:


* Multiple people share the main account for actions, making it impossible to identify the actual user.

* The main account has extensive permissions, so any exposure would have severe consequences.

* Using the main account directly for operation and maintenance (O&M) tasks involves higher risks.


You can avoid the above issues by using IAM features. You can create IAM users, user groups, and roles under the root account. New IAM users, user groups, and roles have no permissions initially. You can grant them appropriate permissions based on actual needs to achieve multi\-identity management and granular permission control. For more features, see [Overview](https://docs.byteplus.com/en/docs/6257/64959).

<span id=".SUFN55u45YWz5LuL57uN"></span>
## IAM topics


|Topic |Description |Related documentation |
|---|---|---|
|IAM terms |Using IAM for permission management involves many technical terms, such as IAM identities (user, user group, or role), policies, and single sign\-on (SSO). |[Terms](https://docs.byteplus.com/en/docs/6257/64963) |
|IAM limits |IAM resources are limited by resource quotas. If exceeding the quota limit, new resources cannot be created. |[Limits](https://docs.byteplus.com/en/docs/6257/1285191) |
|IAM usage process |You can authorize IAM users directly or authorize them by adding them to a user group. |* [Create a user and authorize it](https://docs.byteplus.com/en/docs/6257/94013)<br><br>* [Grant user API key management permissions](https://docs.byteplus.com/en/docs/6257/1319865) |
|IAM policy overview |A policy is a set of permissions described using a syntax structure.<br><br><br>* Policy type: IAM supports two types of policies: **System default policy** and **Custom policy**.<br><br>* Policy syntax structure: IAM policies follow a fixed syntax format, allowing you to create diversified and customized IAM policies as needed.<br><br>* Policy scope: IAM policies apply two scopes: **Global** and **Designated projects**. |* [Policy Grammar](https://docs.byteplus.com/en/docs/6257/65059)<br><br>* [DC IAM policy types](https://docs.byteplus.com/en/docs/directconnect/Configuration-example-of-custom-policy) |
