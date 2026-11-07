---
title: "Announcement on overdue payment suspension and resource reclamation"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/announcement-on-overdue-payment-processing"
---

BytePlus VOD will introduce a standardized overdue payment suspension and resource reclamation policy to reduce billing risks and ensure consistent service management. This change may affect service availability, domain access, and the retention of your VOD resources.

For the complete policy, see [Processing of overdue payments](https://docs.byteplus.com/docs/byteplus-vod/docs-processing-of-overdue-payments).

## Effective dates

|Affected billing instance |Effective time |
|---|---|
|VOD billing instances created at or after 00:00 on November 9, 2026 (UTC+8) |Immediately after the instance is created |
|VOD billing instances created before 00:00 on November 9, 2026 (UTC+8) |00:00 on November 16, 2026 (UTC+8) |

## What will change

Within 72 hours after the account becomes overdue, the service remains available and you can continue to use BytePlus VOD normally.

If your BytePlus VOD account remains overdue for more than 72 hours and no more than 360 hours (15 days) after it becomes overdue:

* You can still sign in to the BytePlus VOD console and view existing resources, configurations, and statistics.

* You cannot create spaces, upload videos or materials, create media processing or workflow templates, start workflows, restart transcoding tasks, or create domain names.

* All BytePlus VOD CDN domain names will be disabled and client access through these domain names will be denied.

If you settle the overdue payment during suspension, the restricted operations become available again. Domain names disabled during suspension must be manually re\-enabled.

If your account remains overdue for more than 360 hours (15 days) after it becomes overdue, BytePlus VOD will start resource reclamation. All stored videos and materials will be deleted, related offline tasks will be stopped, and the VOD billing instance will be reclaimed. Data deleted during reclamation cannot be recovered.

## Recommended actions

* Review the [Processing of overdue payments](https://docs.byteplus.com/docs/byteplus-vod/docs-processing-of-overdue-payments) policy before the effective date that applies to your billing instance.

* Monitor [bills](https://docs.byteplus.com/docs/byteplus-vod/docs-viewing-bills) and keep a sufficient balance.

* Settle overdue payments in the [Billing center](https://console.byteplus.com/finance/overview) before resource reclamation begins.

* If you have questions, [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001112) before the effective date.

Thank you for your continued support.

BytePlus VOD

November 1, 2026
