---
title: "Subscription and billing overview"
product: "TRAE"
product_code: "trae"
source: "https://docs.byteplus.com/en/docs/trae/billing-overview"
---

This article explains the subscription system of TRAE Enterprise, including subscription requirements, billing model, renewal policies, expiration rules, and cancellation policies.

<span id="67d3cb0d"></span>
## Subscription information


* **Subscription method**: Visit BytePlus official website, then purchase a desired plan on the TRAE Enterprise plan purchase page.

* **Billing model**: TRAE Enterprise adopts a hybrid billing model that combines seat\-based annual/monthly subscription (prepaid) and pay\-as\-you\-go (postpaid). For more information, refer to [Billing items](https://docs.byteplus.com/docs/trae/billing-items).

* **Plan features**: After purchasing a paid plan, your enterprise receives the fixed quota and corresponding features included in the plan. For more information, refer to [TRAE Enterprise plan](https://docs.byteplus.com/docs/trae/trae-enterprise-plans).

* **Pay\-as\-you\-go billing**: When resource usage by enterprise members exceeds the quota included in the paid plan, pay\-as\-you\-go billing must be enabled to continue using the models provided by TRAE Enterprise. The related fees will be automatically deducted from the cash balance of the enterprise's BytePlus account; if the cash balance is insufficient to cover the fees incurred by pay\-as\-you\-go, the TRAE Enterprise account will enter an overdue status.

* **Billing delay**: Currently, which means billing records may be generated with an hourly delay. An account enters overdue status only after the billing and deduction process is completed. Before that, the enterprise can continue using TRAE Enterprise and may continue to incur additional charges. 

   For example, usage generated between 16:00 and 17:00 may be billed and deducted at 17:00:00. If the account's cash balance is insufficient at that time, it will immediately enter an overdue status.


<span id="c7171eac"></span>
## Subscription rules

The enterprise must subscribe to a seat\-based annual/monthly plan before using TRAE Enterprise. 

If additional seats are purchased during an active subscription period, the expiration date of the newly added seats will be aligned with the expiration date of the original subscription.

Pay\-as\-you\-go billing can only be enabled and used after purchasing a seat\-based annual/monthly plan.

<span id="ee55d824"></span>
## Renewal and expiration rules

After purchasing a TRAE Enterprise plan, if auto\-renewal is enabled, the system will automatically charge the account **7 days before the subscription expires**. A successful charge automatically completes the renewal. For more information, refer to "[Renewal Rules](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-of-renewal-rules)".

If auto\-renewal is not enabled, enterprises can renew their subscription manually at any time before or after the current subscription expires.

If renewal is not completed successfully, access to TRAE Enterprise will be suspended after the current subscription expires. However, member accounts and related data will be retained for 48 months. Enterprise administrators can sign in to the console to renew the subscription. For more information, refer to [Manage renewals](https://docs.byteplus.com/docs/trae/manage-subscription).

<span id="da38e880"></span>
## Impact of expiration and cancellation

When a subscription expires or is canceled, the following changes take effect:


* All members lose access to the features included in TRAE Enterprise plan. 

* Member accounts are retained. Administrators can still log in to the console to renew subscriptions and view data, but the entire enterprise cannot access AI features through the TRAE IDE or TRAE Plugin.

* Pay\-as\-you\-go billing is automatically suspended. 

* New members cannot be added. 

* Existing resources are retained and will not be deleted. Resources in TRAE Enterprise cannot be migrated to TRAE's personal edition.
