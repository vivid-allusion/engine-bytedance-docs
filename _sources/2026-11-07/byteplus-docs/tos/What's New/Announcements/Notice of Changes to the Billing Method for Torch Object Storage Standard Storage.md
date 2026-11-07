---
title: "Notice of Changes to the Billing Method for Torch Object Storage Standard Storage"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Notice-of-changes-to-the-billing-method-for-torch-object-storage-standard-storage"
---

To improve our services, BytePlus Torch Object Storage will optimize its billing logic for Standard Storage on January 15, 2026. Once the number of objects stored in Standard Storage that are smaller than 64 KiB reaches a certain threshold, a minimum charge based on object size will be introduced. Objects smaller than 64 KiB will be charged as if they were 64 KiB for storage costs.

<span id="1mMMiZoY"></span>
## Estimated Change Time

2026\-01\-15 (Beijing Time). Please refer to the console for the specific time.

<span id="7U3gsbuF"></span>
## Change Description

This change only applies to "small objects", which are defined as objects in Standard Storage that are smaller than 64 KiB. The details are as follows:


* Before the change: Storage costs were calculated based on the actual size of small objects with no additional restrictions.

* After the change: The billing logic for small objects is different. A tiered billing policy has been implemented, which is based on a threshold of one billion small objects per account per region.

   * If the number of small objects in a region is below one billion, storage costs will continue to be calculated based on their actual size.

   * If the number of small objects in a region reaches or exceeds one billion, however, each small object will be charged as 64 KiB for storage costs.


<span id="vwLWkf05"></span>
## Impacts

Starting January 15, 2026, if you store more than one billion small objects in Standard Storage in a single region, each object will be charged as 64 KiB, which will increase your overall storage costs. Specific charges will be based on your actual billing records. For instructions on viewing your bills, see [Billing management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-billing-management).

If the total number of small objects in a region remains below one billion, the billing method will remain unchanged (based on actual size), and this change will not affect your costs.

If you have any questions about this change, [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000245) or contact your account manager for assistance.
