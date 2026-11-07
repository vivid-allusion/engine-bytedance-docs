---
title: "Set Traffic Targets for Intelligent Policy"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/c7KpPz"
---

If your GTM instance's active policy type is intelligent policy, you need to set traffic targets for your policy. Once set, the GTM instance automatically creates rules according to the traffic targets after you start the GTM instance. One or multiple pools can be set as traffic targets.

If you do not set traffic targets, the GTM instance cannot start.

<span id="prerequisites"></span>
## Prerequisites


* You have created and configured a GTM instance. See [Configure a GTM Instance](https://docs.byteplus.com/docs/byteplus-dns-suite/0_OA55).

* You have added at least one pool to the GTM instance. See [Create a Pool](https://docs.byteplus.com/docs/byteplus-dns-suite/RmUweJ).


<span id="steps"></span>
## Steps

Follow the steps below to set traffic targets for the intelligent policy.


1. On the [Instance management page](https://console.byteplus.com/dns-suite/gtm/instances), find your GTM instance. Click the domain name in the **Domain** column.

2. On the **Policy management** tab, click the **Configure** button for **Intelligent routing**.

3. On the **Common configuration** tab, click **Edit** next to **Traffic targets**.

4. On the **Edit traffic targets** page, check the pools you need to set as traffic targets. After completion, click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the page is empty, it means you have not added any pool to the GTM instance. See <a href="https://docs.byteplus.com/docs/byteplus-dns-suite/RmUweJ">Create a Pool</a>.   </div>
