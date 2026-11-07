---
title: "[Product update] Change of the overdue payment duration"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Change_of_the_Overdue_Payment_Duration"
---

The Container Registry will extend the usable duration when there is an overdue payment and the retention duration after an instance is in arrears. Please pay attention to the difference before and after this change and manage your account balance reasonably.

The rules for overdue payment duration changed on **October 24, 2024**.


|**Overdue Payment Duration** ||**Description** |
|---|---|---|
|**Before the Change** |**After the Change** ||
|＜ 2h |＜ 360h |**Product features are fully functional**, with charges incurred during usage **billed as usual**. For more information on billing, refer to [Billing overview](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-2). |
|≥ 2h |≥ 360h |BytePlus sends notifications through SMS and email to remind you of the overdue payment and **freezes** your resources (which means you can no longer operate the Enterprise Standard Edition instances). Resources are not charged when they are frozen. |
|2h ＜ duration ≤ 30d + 2h |360h ＜ duration ≤ 1080h |If you have paid the overdue payment under your account, BytePlus automatically unfreezes your resources to enable you to continue to use the product. |
|＞ 30d + 2h |＞ 1080h |BytePlus sends notifications through SMS and email and **releases your resources by deleting the instances**. **Resources cannot be recovered after they are released**. |
