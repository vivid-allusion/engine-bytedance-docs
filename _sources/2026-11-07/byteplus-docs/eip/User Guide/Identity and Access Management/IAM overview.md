---
title: "IAM overview"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Identity-and-access-management"
---

Identity and Access Management (IAM) is a permission management system provided by BytePlus to customers **as a free service**. You can create IAM users under your BytePlus account (root account) and grant each user appropriate permissions based on their roles to control access to cloud resources. enabling decentralized resource management, improving efficiency, and reducing information leakage risks.

<span id="Ti62zg8E"></span>
## Application scenarios

To use BytePlus resources, you need to first register an account on BytePlus. After registration, you will obtain a BytePlus account, which is the "root account," and this root account initially has full administrative permissions over all resources under it. Using only the root account to manage resources may cause the following issues:


* Multiple people share the root account for actions, making it impossible to identify the actual user.

* The root account has extensive permissions, so any exposure would have severe consequences.

* Using the root account directly for operation and maintenance tasks involves higher risks.


You can avoid these issues by using the IAM feature. You can create IAM users, user groups, and roles under the root account. Newly created IAM users, user groups, and roles have no permissions initially. You can grant appropriate permissions based on actual needs to achieve multi\-identity management and fine\-grained permission control. For more features, see [Product introduction](https://docs.byteplus.com/en/docs/IAM/iam-overview).


* Set the same permissions over multiple cloud resources.


<span id=".SUFN55u45YWz5LuL57uN"></span>
## IAM topics


|Topic |Description |Related documentation |
|---|---|---|
|IAM terms |Using IAM for permission management involves many technical terms, such as IAM identities (user, user group, role), policies, and single sign\-on (SSO). |\-\- |
|IAM limits |IAM resources are limited by resource quotas. If the quota limit is exceeded, new resources cannot be created. |\-\- |
|IAM usage process |You can authorize IAM users directly or authorize them by adding them to a user group. |* [Create a user and authorize it](https://docs.byteplus.com/en/docs/IAM/creating-a-user)<br><br>* [Grant user API key management permissions](https://docs.byteplus.com/en/docs/IAM/managing-an-access-key) |
|IAM policy overview |A policy is a set of permissions described using a syntax structure.<br><br><br>* Policy types: IAM supports **system default policies** and **custom policies**.<br><br>* Policy syntax structure: IAM policies follow a fixed syntax format, allowing you to create diversified and customized IAM policies as needed.<br><br>* Policy scope: IAM policies apply to **global permissions** and **project permissions**. |* [Basic structure](https://docs.byteplus.com/en/docs/IAM/what-is-the-policy-syntax)<br><br>* [IAM policy types for Elastic IP Address](https://docs.byteplus.com/en/docs/eip/IAM_policy_types_for_Elastic_IP_Address)<br><br>* [IAM policy types for IP Address Pool](https://docs.byteplus.com/en/docs/eip/IAM_policy_types_for_IP_Address_Pool) |
