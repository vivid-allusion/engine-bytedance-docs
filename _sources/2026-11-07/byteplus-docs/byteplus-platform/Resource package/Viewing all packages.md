---
title: "Viewing all packages"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/Viewing_all_packages"
---

In the Billing Center, you can view all packages and their detailed information, including package name, package type, quota, and so on.

<span id="98590a10"></span>
## View all packages

Use the following steps to view all packages:


1. Sign in to the [BytePlus Console](https://console.byteplus.com/auth/login/).

2. On the top navigation bar, click **Billing** \> **Resource management**.

   The overview tab appears.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_1bbaff7ba67ce18e9983e48e6f3f017a.png) </span>

3. (Optional) Perform the following operations as needed:

   1. Click **Remaining quota alert** to set quota notifications.

   2. Click **Details** to view the deduction details of a resource pack.

   3. Click **Export** to download resource pack information.


<span id="04df65a7"></span>
## About remaining quota alert

The platform triggers alerts to notify users when the remaining quota of their packages is below the threshold, which is 20% by default. Below are the alert rules for two types of packages:

**Periodic packages:** 

For periodic packages that are reset monthly, the platform sends a notification when the monthly remaining quota is below the threshold. For those reset weekly/hourly, remaining quota alert is not supported.

**Diminishing packages:** 

For dimishing packages, the platform sends a notification when the remaining quota is below the threshold.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If a new purchase, modification, renewal, or unsubscription changes the total quota of a package, the system will reset the remaining quota alert（the threshold ratio remains the same）. For example, if the total quota of a package is 100G, the current remaining quote is 20G, the threshold for triggering the remaining quota alert is 20%, and you make a new purchase of the same package, the total quota goes up to 200G based on which the system will reset the remaining quota alert.</div>


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/a6722a3-Remaining_Quota_Alert.PNG) </span>

You can perform the following operations in the Set balance alert window:


|**No.**  |**Description** |
|---|---|
|1 |Toggle the switch to enable remaining quota alert for all packages. |
|2 |Set a threshold below which an alert will be triggered. |
|3 |Enable/disable remaining quota alert for a single package. |
