---
title: "Processing of overdue payments"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-processing-of-overdue-payments"
---

This topic describes why a BytePlus VOD account can become overdue, how overdue payment affects service availability, how to resume service, how resources are reclaimed, and how to check your bill. For the customer notice about this policy change, see [Announcement on overdue payment suspension and resource reclamation](https://docs.byteplus.com/docs/byteplus-vod/announcement-on-overdue-payment-processing).

> **Warning**

> Resources deleted during reclamation cannot be restored. Settle overdue payments before reclamation begins to avoid data loss.

## Process overview

![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261102071952-1466741177110.png)

1. Your account enters an overdue state when the available balance is insufficient to settle BytePlus VOD charges.

2. BytePlus sends reminders during the overdue period.

3. Within 72 hours after the account becomes overdue, the service remains available and you can continue to use BytePlus VOD normally.

4. If the account remains overdue for more than 72 hours and no more than 360 hours (15 days), BytePlus VOD suspends new resource creation and disables VOD CDN domain names. Existing resources remain available for viewing.

5. If you settle the overdue payment during suspension, service restrictions are removed. Domain names disabled during suspension must be manually re\-enabled.

6. If the account remains overdue for more than 360 hours (15 days) after it becomes overdue, BytePlus VOD starts resource reclamation and reclaims the VOD billing instance.

Both the 72\-hour suspension threshold and the 360\-hour reclamation threshold are measured from when the account becomes overdue, not from when service is suspended.

## Why an account can become overdue

An account can become overdue when BytePlus VOD charges are generated but the available balance is insufficient to pay the bill. Common scenarios include:

* Pay\-as\-you\-go usage exceeds your available balance. BytePlus VOD supports daily and monthly billing cycles, and charges are settled after use. For details, see [Pricing overview](https://docs.byteplus.com/docs/byteplus-vod/docs-pricing) and [Pay-as-you-go pricing](https://docs.byteplus.com/docs/byteplus-vod/docs-pay-as-you-go-pricing).

* Resource package quotas are exhausted, or a charge is not covered by a resource package. Usage outside the package scope is charged on a pay\-as\-you\-go basis. For details, see [Prepaid resource packages](https://docs.byteplus.com/docs/byteplus-vod/docs-resource-packs).

* Stored media continues to occupy storage space and incur [storage fees](https://docs.byteplus.com/docs/byteplus-vod/docs-pay-as-you-go-pricing#310bc067).

* Playback or download requests continue to generate traffic. Requests served through VOD CDN domain names incur distribution acceleration fees; direct access to VOD storage addresses incurs [storage outbound traffic fees](https://docs.byteplus.com/docs/byteplus-vod/docs-pay-as-you-go-pricing#b7992460).

* Bill settlement is delayed. Real\-time billing data does not include all unsettled pay\-as\-you\-go charges, and the final amount is subject to the settled bill. For details, see [Viewing bills](https://docs.byteplus.com/docs/byteplus-vod/docs-viewing-bills).

> **Note**

> If you want to prevent additional BytePlus VOD charges, confirm whether stored media, accessible domain names, running media processing tasks, or active playback, download, or processing requests still exist. Delete resources, disable domain names, or stop business requests only after confirming that production services will not be affected.

## Overdue notifications

During the overdue period, BytePlus sends reminders to prompt you to renew your account and avoid service suspension or resource reclamation.

## Overdue suspension

If your account remains overdue for more than 72 hours and no more than 360 hours (15 days) after it becomes overdue, BytePlus VOD suspends your VOD service.

During suspension:

* You can still sign in to the BytePlus VOD console and view existing resources, configurations, and statistics.

* You cannot create a VOD space.

* You cannot upload videos or materials.

* You cannot create a media processing template or workflow template.

* You cannot start a workflow or restart a transcoding task.

* You cannot create a domain name.

* All BytePlus VOD CDN domain names are disabled, and client access through these domain names is denied.

To resume service, settle the overdue payment in the [Billing center](https://console.byteplus.com/finance/overview). If you need assistance, [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001112).

## Service resumption

* **Before suspension:**  If you settle the overdue payment before it has been overdue for 72 hours, you can continue using BytePlus VOD.

* **During suspension, before reclamation begins:**  After you settle the overdue payment, the operations restricted during suspension become available again. Domain names disabled during suspension are not re\-enabled automatically; you must manually re\-enable each required domain name.

* **After reclamation:**  Activate BytePlus VOD again to resume using the service. Payment does not restore media deleted during reclamation.

For domain name operations, see [Domain name configuration](https://docs.byteplus.com/docs/byteplus-vod/docs-domain-name-configuring).

## Resource reclamation

If your account remains overdue for more than 360 hours (15 days) after it becomes overdue, BytePlus VOD starts resource reclamation.

During reclamation:

* All videos and materials stored in VOD are deleted.

* Workflow and transcoding tasks are stopped.

* Configuration data is retained, but related offline tasks are stopped. Affected configurations include workflow and transcoding templates, domain settings, upload and storage settings, classification settings, and callback settings.

* The VOD billing instance is reclaimed.

After reclamation is complete, VOD is no longer activated for the account. To use BytePlus VOD again, you must activate the service and create the required resources again. Data deleted during reclamation cannot be recovered.

## Check your bill

1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas).

2. In the top navigation bar, click your profile and choose **Billing**.

3. View bills by charging period or open bill details to inspect BytePlus VOD charges. For detailed steps, see [Viewing bills](https://docs.byteplus.com/docs/byteplus-vod/docs-viewing-bills).
