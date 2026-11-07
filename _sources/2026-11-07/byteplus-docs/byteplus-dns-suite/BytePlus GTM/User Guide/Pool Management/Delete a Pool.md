---
title: "Delete a Pool"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/AYaGwT"
---

This document describes how to delete a pool in BytePlus GTM.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If the GTM instance where the pool is included is running, you need to stop the GTM instance before deleting the pool.</div>


<span id="steps"></span>
## Steps

Follow the steps below to delete a pool.


1. On the [Instance management](https://console.byteplus.com/dns-suite/gtm/instances) page, find the GTM instance. Click the domain name of the GTM instance in the **Domain** column.

2. On the **Address management** page, find the pool you need to delete.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If a pool is still being used by any pool set or routing rule, BytePlus GTM cannot delete the pool.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If a pool is set as a traffic target, BytePlus GTM cannot delete the pool.   </div>
   

3. In the **Actions** column, click **Delete**. In the pop\-up window, confirm the pool you need to delete and click **Delete**.
