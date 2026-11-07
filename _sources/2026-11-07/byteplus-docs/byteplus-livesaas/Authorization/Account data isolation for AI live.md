---
title: "Account data isolation for AI live"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/account-data-isolation-for-ai-live"
---

AI Live isolates data by account level to prevent unauthorized access to or modification of other users' data.

The access control model is as follows:


* **Subaccounts** can access only data created or owned by themselves.

* **The admin account** can access all data associated with the account, including data belonging to subaccounts.

* **For AI figures' quota**, each account has an independent quota and consumes only its own quota. The quotas of different accounts do not affect one another. For example, if the total quota is 13 and 5 quotas are allocated to each of two subaccounts, the admin account retains 3 quotas for its own use. Each subaccount can train up to its allocated quota of 5, independently of the other accounts. Currently, you can contact BytePlus Support for quota allocation by providing the sub\-account email address and the requested quota amount.


For non\-AI Live rooms, you can assign roles to users to allocate and manage access to resources. For details, see [Adding a role](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles#08751041).

<span id="433a996b"></span>
### Account visibility by feature

The following table describes the data visibility of subaccounts and the admin account for each feature.


|**Feature** |**Resource** |**Subaccount visibility** |**Admin account visibility** |
|---|---|---|---|
|AI Live |AI figures, voices, knowledge base, products, and integrated shops from TikTok Shop, Shopify, and In\-house system |Own data only. For example, a subaccount can view only the AI figures, voices, knowledge bases, products, and integrated shops that it created; it cannot view those created by other subaccounts or by the admin account. |All resources under the account. |
|AI Analysis |Host scoring and live\-stream review tasks |Own data only. For example, a subaccount can view only the host\-scoring and live\-stream review tasks that it created, not those created by other subaccounts. |All resources under the account. |


<span id="2851f01d"></span>
## Service center

The **Service center** page for AI Live and AI Analysis is available only to the admin account. Subaccounts do not have access to the **Service center** page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2fb09b6b3d6a4e888569431499623528~tplv-goo7wpa0wc-image.image) </span>
