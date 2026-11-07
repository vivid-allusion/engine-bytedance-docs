---
title: "Unified expiration day"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/docs-unified_expiration_day"
---

<span id="1e0bddd7"></span>
### Rules

Setting a unified expiration day allows all instances of **non\-calendar\-month subscriptions** within your account to expire on a fixed day of each month. Once configured, the setting applies to all instances of **non\-calendar\-month subscriptions**. You can choose whether to align with the set unified expiration day each time you perform a manual renewal.

**Notes**


* If you have never set a unified expiration day before, the default expiration time on the unified expiration day setup page will be 23:59:59 on the 1st of every month.

* The unified expiration day can be set to any day between the 1st to 28th or the last day of each month.

* The specified unified expiration day and the expiration date of the current billing period must be at least one month apart. For renewal to the unified expiration day, the subscriptions are billed based on a daily rate converted from the monthly price. The specific charge for renewal will be displayed on the order confirmation page.

* Currently, only instances of non\-calendar\-month subscriptions can have a unified expiration day during manual renewal; this feature is not supported for instances of annual/daily/calendar\-month subscriptions.

* Only manual renewal supports selecting a unified expiration day; auto\-renewal will continue to follow the preset renewal cycle.


**Example**

Instance A will expire on August 28, 2023, at 23:59:59. Absent any discount, the regular monthly price of Instance A is RMB 60, and you have set the unified expiration day to the 15th of every month:


* If you initiate a manual renewal for one month on August 27, 2023 without selecting renewing to the unified expiration day, then the expiration time after renewal will be September 28, 2023, 23:59:59, and the renewal fee is RMB 60 \* 1 month = RMB 60.

* If you initiate a manual renewal for one month on August 27, 2023 and select renewing to the unified expiration day (the 15th of each month), then the expiration time after renewal will be October 15, 2023, 23:59:59, the renewal duration will be 48 days, and the renewal fee is calculated as RMB 60/30 \* 48 days = RMB 96.


<span id="1f763bcd"></span>
### Steps


1. Go to the Renewal Management page and click Unify Expiration Day at the top right of the renewal list.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_70f85738b8710374120fd9c22e8bb6b4.png) </span>


2. Set a unified expiration day.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_44b9afdefb59c401b875745c1e9443e7.png) </span>


3. Click OK to complete the setup.

4. Select the instances to renew and click Renew or Batch Renew.

5. Select to renew based on the purchased duration and select Unify Expiration Day.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f8addd0b4e6be15166274b3887fe0acc.png) </span>


6. Click Pay and complete the renewal.
