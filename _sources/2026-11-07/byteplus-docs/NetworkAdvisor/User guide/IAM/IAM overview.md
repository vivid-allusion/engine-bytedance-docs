---
title: "IAM overview"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/IAM-overview"
---

Identity and Access Management (IAM) is a system for permission management and is one of the **Free services** provided by the platform. You can create IAM users for your BytePlus account (root account) and grant them appropriate permissions based on different purposes to control access to cloud resources by different identities. This achieves decentralized resource management, improves management efficiency, and reduces the risk of information leakage.

<span id="Omdvs7by"></span>
## Why use IAM

Before using any resources, you must first  Register an account on the platform. After completing registration, you will obtain a BytePlus account, which is referred to as the **Root Account**. **The Root Account is automatically granted full administrative privileges over all resources under it by default**.

Using only the root account to manage resources may cause the following issues:


* Multiple people share the root account for actions, making it impossible to identify the actual user.

* The root account has extensive permissions, so any leak would have severe consequences.

* Using the root account directly for operation and maintenance (O&M) tasks involves higher risks.


You can avoid the above problems through the IAM function. You can create IAM users, user groups, and roles under the main account. Newly created IAM users, user groups, and roles do not have any permissions. You can grant the corresponding permissions to create IAM users, user groups, and roles according to the actual use. Realize multiple identity management, refined permission control, etc. .

<span id="OrfAi8hq"></span>
## IAM topics


|Topic |Description |
|---|---|
|IAM terms |Using IAM for permission management involves many technical terms, such as IAM identities (user, user group, and role), policies, and single sign\-on (SSO). |
|IAM limits |IAM resources are limited by resource quotas. If exceeding the quota limit, new resources cannot be created. |
|IAM usage process |You can authorize IAM users directly or authorize them by adding them to a user group. |
|IAM policy overview |A policy is a set of permissions described using a syntax structure.<br><br><br>* Policy type: IAM supports two types of policies: **System default policy** and **Custom policy**.<br><br>* Policy syntax structure: IAM policies follow a fixed syntax format, allowing you to create diversified and customized IAM policies as needed.<br><br>* Policy scope: IAM policies apply two scopes: **Global permissions** and **Project\-level permissions**. |


&nbsp;

&nbsp;
