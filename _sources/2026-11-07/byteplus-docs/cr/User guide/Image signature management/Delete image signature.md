---
title: "Delete image signature"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Delete_image_signature"
---

When you no longer need to sign images under a namespace, you can delete the signature rule. You can also delete the signature of a single image tag.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default"> Part of the product features are provided in beta. To use beta features, please contact <strong>your account manager or after\-sales engineer</strong>.</div>


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After deleting the signature rule or signature information, it cannot be restored. This will cause image signature verification to fail, but will not impact image pulling and usage. Proceed with caution.</div>


<span id="P3ueouxa"></span>
## Comparison of deletion methods


|**Item** |**Delete signature rule** |**Delete image signature (image level)**  |
|---|---|---|
|Application scenario |No longer need to sign images in the entire namespace, and want to completely remove the signing policy. |To revoke the signature of a specific image tag while retaining the namespace\-level signature rules in effect. |
|Scope of impact |Newly pushed images in this namespace will no longer be signed automatically. |Only affects the operated image tag; signatures and automatic signing of other images are not affected. |


<span id="EjWvcmnx"></span>
## Delete signature rule

After deleting the signature rule, new images pushed under the namespace will no longer be automatically signed, and existing signature information will be deleted.


1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **List of instances**, find the target instance, and click **Enter instance**.

2. In the left navigation, click **Image signature**.

3. In the signature rule list, click **Actions** in the target rule's column, then click **Delete**.

4. In the confirmation dialog, click **Delete** to finish the operation.


<span id="onO24wsW"></span>
## Delete a single image signature

You can also delete only the signature of a specific image tag without deleting the entire signature rule.


1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **List of instances**, find the target instance, and click **Enter instance**.

2. In the namespace list, click the target namespace to enter the OCI artifact repository list, then click the target CR to enter the image tag list page.

3. In the **Actions** column of the target image tag, click **Delete signature**.

4. In the secondary confirmation dialog box, click **Delete** to finish the operation.
