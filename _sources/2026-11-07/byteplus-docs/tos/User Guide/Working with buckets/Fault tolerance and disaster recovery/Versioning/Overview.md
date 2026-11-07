---
title: "Overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-overview"
---

You can use the versioning feature to keep multiple versions of objects in your bucket so that you can restore objects that are accidentally deleted.

<span id=".5L2_55So5Zy65pmv"></span>
## Use cases

When versioning is enabled on your bucket, TOS automatically saves historical versions of your original data whenever you delete or overwrite it. If you perform an accidental operation, you can restore the data to a previous version to prevent data loss or unintended modifications. Versioning enhances fault tolerance and is therefore suitable for scenarios requiring high data reliability.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes

Enabling versioning does not incur additional fees. However, you will be charged for storing historical object versions. To avoid unnecessary charges, promptly delete historical versions that are no longer needed. Additionally, you will be charged for the request and data transfer when downloading or restoring historical versions. To learn more, see[ Billing overview](https://docs.byteplus.com/en/docs/tos/docs-billing-overview).

<span id=".54q25oCB6K-05piO"></span>
## Versioning state

Buckets can be in one of three states:


* **Unversioned**: Versioning is not enabled by default for a bucket. Each object in the bucket is unique and does not have a version ID. After enabling versioning, you can only suspend it. You cannot revert it to the "Disabled" state.

* **Versioning\-enabled**: When versioning is enabled, TOS assigns a unique version ID to every object within a bucket. For instructions, see [Enabling versioning](https://docs.byteplus.com/en/docs/tos/docs-enabling-and-suspending-versioning).

* **Versioning\-suspended**: If you do not need it, you can suspend versioning. After doing so, the version ID of objects uploaded to the bucket will become **null**. For instructions, see [Suspending versioning](https://docs.byteplus.com/en/docs/tos/docs-enabling-and-suspending-versioning).


Different versioning states result in different object behaviors. These behaviors are described below.


|**Versioning state** |**When you delete an object** |**When you overwrite an object** |
|---|---|---|
|Unversioned |The object is deleted immediately and cannot be retrieved later. |The object is overwritten immediately and is therefore unrecoverable. |
|Versioning\-enabled |Deleting an object without enabling **Show versions** does not permanently remove the object. Instead, a deletion mark is added, making TOS behave as if the object were deleted.<br><br>To permanently delete an object, enable **Show versions** on the Objects page and select the corresponding version to delete. |A new version of the object is generated with a globally unique version ID, while the historical version remains unaffected. |
|Versioning\-suspended |Deleting an object without enabling **Show versions** can result in one of two scenarios:<br><br><br>* If the object's version ID is `null`, the object will be deleted.<br><br>* If the version ID is not `null`, the object will not be deleted and a deletion mark will be added instead.<br><br><br>To permanently delete an object, enable **Show versions** on the Objects page and select the corresponding version to delete. |A new version of the object is generated with a null version ID. If a historical version with a null version ID has the same name as the new version, the historical version will be overwritten. Other historical versions with non\-null version IDs remain unaffected. |


&nbsp;
