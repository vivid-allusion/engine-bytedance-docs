---
title: "Storage of temporary copies"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-temporary-storage-fee"
---

After you restore an object from Archive, Cold Archive, or Deep Cold Archive, TOS creates a temporary copy of the object in Standard Storage, so you can access it. This copy will be deleted automatically at the end of its specified validity period. You will be charged for the temporary storage of this copy during this period.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This topic only provides a description of billable items. For specific prices, see <a href="https://www.volcengine.com/pricing?product=TOS&tab=1">TOS pricing</a>.</div>


<span id="4e64a969"></span>
## Notes

When you restore an object from Archive, Cold Archive, or Deep Cold Archive, you pay for both the archived object and the copy that you restored temporarily. For example, if you restore a 10 GiB object from Cold Archive and the copy is valid for three days, you must pay for 10 GiB of archived objects and 10 GiB of temporary copies over the course of those three days.

<span id="59b39dd1"></span>
## Billable item


|**Billable item** |**Description** |**Formula** |
|---|---|---|
|Storage of temporary copies |After you restore an object from Archive, Cold Archive, or Deep Cold Archive, TOS creates a temporary copy of the object in Standard Storage, so you can access it. This copy will be deleted automatically at the end of its specified validity period. You will be charged for the temporary storage of this copy during this period. |**Pay\-as\-you\-go**: Hourly temporary storage cost = Copy size (GiB) × Monthly rate ÷ 30 (days) ÷ 24 (hours) |
