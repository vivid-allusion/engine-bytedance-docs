---
title: "[Billing] Notice of Changes to Expiration and Renewal Policies for Subscription-Based Elastic Block Storage Volumes"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Notice-of-Changes-to-Expiration-and-Renewal-Policies-for-Subscription-Based-Elastic-Block-Storage-Vo"
---

Dear valued customer, BytePlus will adjust the expiration and renewal policies for subscription\-based Elastic Block Storage (EBS) volumes starting at **2:00 p.m. on October 30, 2026**.

## What's Changing

* The service for a subscription\-based volume is suspended immediately after the subscription expires. The volume cannot be read, written to, or attached. The previous 0–12\-hour grace period no longer applies, and no fees will be charged during the suspension.

* After service is suspended, the volume enters a 15\-day data retention period. If the subscription is renewed during this period, the volume becomes available again and a new, valid subscription period begins. No fees will be collected between the suspension and renewal dates.

* If renewal is not completed within 15 days, the volume will be released and its data will become irretrievable.

> **tip**

> This change only applies to EBS volumes that are charged on a **subscription** basis. The billing rules and lifecycles of **pay\-as\-you\-go** EBS volumes are **not affected**.

### Before and After the Change

|**Item** |**Before the change** |**After the change** |
|---|---|---|
|Volume availability in the 0–12 hours after expiration |The volume remains available for 0–12 hours after expiration. |The volume becomes unavailable immediately upon expiration, with no grace period of 0–12 hours. |
|Billing during service suspension |Subscription fees accrue until renewal. |There are no subscription fees. |
|Charges for the suspension period |You are charged for the period between the suspension and renewal dates. |No fees are charged for the suspension period. |
|Start of the new validity period |The new validity period begins at the time of the previous expiration. |The new validity period begins at the time of renewal. |
|Data retention period |The existing retention policy applies. |Data is retained for 15 days after service suspension. If the volume is not renewed before the end of the retention period, the volume and its data will be released. |
|Associated resources (i.e., instances) |Volume expiration may result in read/write errors or the early release of associated data. |Associated resources follow the volume lifecycle. There are no duplicate charges, and the associated data is not released early. |

### Diagrams

**Before the change**

The lifecycle consists of four stages and includes a grace period of 0–12 hours.![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_78bec44ca623e3fce3c6bf10ae4422c4.png)

**After the change**

The 0–12\-hour grace period has been eliminated, reducing the lifecycle to three stages.![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_134dfc5421a6475e51b84da9ffe381d7.png)

### Example

**Scenario**: Suppose a volume expires at 8:00 a.m. on October 30. User A renews it for one month at 12:00 p.m. on November 5.

Before the change

* After the volume expires, it remains readable and writable for 0–12 hours before the service is suspended.

* Billing continues at the subscription rate while the service is suspended.

* When User A renews at 12:00 p.m. on November 5, User A must pay the fees incurred from October 30 through November 5.

* The new validity period runs from **October 30** through **November 30**.

After the change

* After the volume expires, its service is suspended immediately, without a 0–12\-hour grace period. The volume then enters a 15\-day data retention period from October 30 through November 14.

* No fees are charged during the suspension from October 30 through November 5.

* When User A renews at 12:00 p.m. on November 5, the volume will still be within the retention period and will become available again. User A will not be charged retroactively for the period during which the service was suspended.

* The new validity period runs from **November 5** through **December 5**.

* If the volume has not been renewed by 8:00 a.m. on November 14, it will be released, and its data will be irretrievable.

## Impact on You

* **Costs**: No fees will be charged while the service is suspended. When you renew, you will not be charged retroactively for the period between the suspension and renewal dates.

* **Validity period**: The new validity period begins on the renewal date. This makes the validity period more predictable because you no longer need to calculate the renewal date based on the previous subscription period's expiration date.

* **Data security**: After the service is suspended, the volume enters a 15\-day data retention period. During this period, the data remains intact, and you can continue using the volume by renewing it. However, if the volume is not renewed within the retention period, the data will be irretrievable. Be sure to renew the volume or migrate its data before the retention period ends.

* **Business continuity**: The previous 0–12\-hour grace period no longer applies. If your workloads cannot tolerate interruptions, renew your volume before it expires.

## Actions Required

* **Volumes that have expired but have not been released**: Renewals completed before **2:00 p.m. on October 30, 2026** will follow the current policy. Renewals completed after this time will follow the new policy. Volumes not renewed within the applicable retention period will be released, and their data will be irretrievable.

* **Volumes that are about to expire and support workloads that cannot tolerate interruptions**: Renew them in advance or enable auto\-renewal to prevent service suspension from affecting your workloads.

* **Scenarios that rely on the post\-expiration grace period for data backup or migration**: Adjust your operations process so that data backup or migration is completed before your volume expires.
