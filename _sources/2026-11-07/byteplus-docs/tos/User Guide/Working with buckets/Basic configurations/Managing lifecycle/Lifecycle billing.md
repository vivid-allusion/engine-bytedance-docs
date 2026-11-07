---
title: "Lifecycle billing"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Lifecycle-rules-cost-description"
---

Using the lifecycle feature to transition or delete objects incurs costs for requests and storage if objects are deleted or transitioned before the minimum storage duration expires. This topic explains such costs in detail.

<span id=".6K-35rGC5qyh5pWw6LS555So"></span>
## Requests

The following describes the cost of requests to transition or delete objects through lifecycle rules:


* Transitioning objects

   The cost of requests is determined by the storage type of the source object. For example, if an object transitions from Standard Storage to Infrequent Access Storage, the Standard Storage rate applies.

* Deleting objects

   When you use lifecycle rules to delete objects, TOS will either permanently delete them or add a deletion mark. For permanent deletion, the applicable rate is based on the storage type of the object at the time of deletion. For adding deletion marks, the applicable rate is based on the default storage type of the bucket where the object resides.


For more information on request pricing, see [Requests](https://docs.byteplus.com/docs/tos/docs-request-fee).

<span id=".5a2Y5YKo5a656YeP6LS555So"></span>
## Storage

TOS calculates storage costs according to an object's storage type, size, and length of time stored. Additionally, the following storage types have minimum storage duration requirements:


* Infrequent Access Storage: 30 days

* Flashback Archive: 90 days

* Archive: 90 days

* Cold Archive: 180 days

* Deep Cold Archive: 180 days


Applying lifecycle rules to delete or transition objects in these storage types before the minimum storage duration has expired will result in early deletion charges.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When you use lifecycle rules to delete objects, TOS will either permanently delete them or add a deletion mark. If objects are permanently deleted before reaching the minimum storage duration, early deletion charges will apply. However, simply adding deletion marks will not incur these charges.</div>



|**How storage duration is calculated** |Lifecycle operations |**Storage** |**Early deletion or change in storage type** |
|---|---|---|---|
|The minimum storage duration for each storage type begins when the object is transitioned to that type.<br><br>&nbsp;<br><br> |Uploaded to Standard Storage (stored for 3 days) \-\-\> Transitioned to Infrequent Access Storage (stored for 10 days) \-\-\> Deleted |* Standard Storage daily cost \* 3 days<br><br>* Infrequent Access Storage daily cost \* 10 days |Early deletion daily charge for Infrequent Access Storage \* 20 days |
||Uploaded to Infrequent Access Storage (stored for 3 days) \-\-\> Transitioned to Flashback Archive (stored for 10 days) \-\-\> Transitioned to Archive |* Infrequent Access Storage daily cost \* 3 days<br><br>* Flashback Archive daily cost \* 10 days |* Early deletion daily charge for Infrequent Access Storage \* 27 days<br><br>* Early deletion daily charge for Flashback Archive \* 80 days |


For more information on storage pricing, see [Storage](https://docs.byteplus.com/docs/tos/docs-storage-fee).

<span id="47a9479e"></span>
## Access monitor

Although enabling the access monitor feature incurs a monitoring\-related fee, this fee is currently waived.
