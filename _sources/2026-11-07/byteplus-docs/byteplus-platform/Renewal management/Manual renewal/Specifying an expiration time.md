---
title: "Specifying an expiration time"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/docs-specifying-an-expiration-time"
---

<span id="c141da73"></span>
### Rules

Specifying an expiration time renews instances of **non\-calendar\-month subscriptions** to the same expiration time, ensuring that the expiration year, month, and day are consistent.

**Notes**


* The earliest expiration time that can be specified is one month beyond 23:59:59 on the latest expiration date among the renewed instances.

* For renewal to a specified expiration time, the subscriptions are billed based on a daily rate converted from the monthly price. The specific charge for renewal will be displayed on the order confirmation page.

* Currently, only instances of non\-calendar\-month subscriptions can have a specified expiration time during manual renewal; this feature is not supported for instances of annual/daily/calendar\-month subscriptions.

* Only manual renewal supports specifying an expiration time; auto\-renewal will continue to follow the preset renewal cycle.


**Example**

Instance A will expire on August 28, 2023, at 23:59:59. Absent any discount, the regular monthly price of Instance A is RMB 60/month. Instance B will expire on September 12, 2023, at 23:59:59. Absent any discount, the regular monthly price of Instance B is RMB 30/month. If you initiate a manual renewal on August 27, 2023, the earliest specifiable expiration time will be October 12, 2023, 23:59:59. If you specify the expiration time as October 30, 2023, 23:59:59, the renewal duration of Instance A will be 63 days, with a renewal fee of RMB 60/30 \* 63 days = RMB 126; the renewal duration of Instance B will be 48 days, with a renewal fee of RMB 30/30 \* 48 days = RMB 48.

<span id="809d0e07"></span>
### Steps


1. Select the instances to renew and click Renew or Batch Renew.

2. Click Specify Expiration Time and choose a specific date for renewal.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_894ffadf2682a451fb4d28a23f941659.png) </span>


3. Click Pay and complete the renewal.
