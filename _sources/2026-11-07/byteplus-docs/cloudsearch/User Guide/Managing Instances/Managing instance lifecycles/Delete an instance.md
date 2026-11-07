---
title: "Delete an instance"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/deleting-instance"
---

When you finish data search tasks and no longer need to use an instance, you can delete the instance to avoid ongoing charges from the service running. When deleting an instance, snapshots created by the instance will be saved in the Object Storage Bucket and will not be deleted. This topic describes how to delete an instance.

<span id="713e9cf4"></span>
## Prerequisites

If deletion protection is turned on for an instance, you cannot delete the instance through the console or API. To delete an instance, first turn off deletion protection. For detailed steps, see [Set instance deletion protection](https://docs.byteplus.com/docs/cloudsearch/deletion-protection).

<span id="4f599025"></span>
## Precautions


* After deleting the instance, all your data will be deleted and cannot be recovered. Handle with care.

* Deleting the instance will automatically disassociate its elastic public network EIP. The EIP will remain active and incur charges. Release the related resources if you no longer need it.

* Deleting the instance unsubscribes it. Deleting pay\-as\-you\-go instances does not involve refunds. Deleting subscription instances will trigger refunds according to the unsubscribe refund policy. For more information, see [Unsubscription](https://docs.byteplus.com/en/docs/6269/81013).


<span id="40f425a8"></span>
## Procedure


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. On the **Instances** page, click  **... \> Delete** in the **Actions** column of the target instance.

4. In the pop\-up confirmation dialog, click **Delete** to delete the instance.
