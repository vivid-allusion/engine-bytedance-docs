---
title: "Destroy an instance"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Destroy_mixed_billing_instances_pending_payment"
---

After successfully creating an instance, you can view instance details and instance status. If you no longer need to use the instance, you can also destroy it.

<span id="hEIwEZfs"></span>
## Background

CR provides the following methods for destroying instances, suitable for different scenarios. Please select the appropriate destruction method according to your requirements.


|**Destruction method** |**Description** |**Data retention** |**Application scenario** |
|---|---|---|---|
|**Temporary reclaim** |The instance enters the recycle bin, and data will not be deleted during the retention period (7 days). The instance can be restored during the retention period by renewing or recharging. After the retention period ends, the instance will automatically be completely destroyed. |Retained during the retention period, deleted after expiration |The instance is automatically reclaimed by the system due to overdue payment, or when a buffer period is desired to confirm whether restoration is needed. |
|**Completely destroy** |The instance and all its data are immediately and permanently deleted. Cannot be recovered. Instance billing stops. |Immediately permanently delete and cannot be recovered |Ensure that the instance is no longer in use, and that resources are released and billing is stopped immediately. |


<span id=".5p-l55yL5qCH5YeG54mI5a6e5L6L6K-m5oOF"></span>
## Temporary reclaim

<div data-tips="true" data-tips-type="default">Description</div>


<div data-tips="true" data-tips-type="default">This operation applies only to standard instances and does not apply to proxy repositories.</div>



1. Log in to the [CR console](https://console.byteplus.com/cr).

2. Select the target region in the top navigation bar.

3. In the left navigation bar, click **Instances**. Then, in the **Instances** area, find the instance that needs to be destroyed.

4. On the right side of the target instance, under the **Actions** column, click `···` \> **Temporary reclaim**.

5. In the pop\-up prompt box of the system, confirm the instance information and then click **Confirm**.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After you click <strong>Confirm</strong>, the instance enters the pending reclaim status. Instances in the pending reclaim state are retained for 7 days by default. During these 7 days, the instance continues to incur charges, and the images and other data stored within it are preserved. You can restore the instance quickly within this period. After 7 days, the instance is permanently deleted and cannot be recovered.   </div>
   

   Instances in the 'to be recycled' state can perform the following actions:

   * Restore the instance: Within 7 days after you destroy the instance, you can restore it at any time.

      In the **Instance list** region, on the right side of the instance in the 'to be recycled' state, under the **Actions** column, click `···` \> **Restore**. After confirming the instance information, you can restore the instance and the images, Helm Charts, and other information stored in the instance.

   * Completely destroy instance: If you are sure the instance does not need to be restored, you can immediately completely destroy the instance, and billing will stop.

      In the **Instance list** region, on the right side of the instance in the 'to be recycled' state, under the **Actions** column, click `···` \> **Completely destroy**. After confirming the instance information, you can immediately completely destroy the instance.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">After the instance is completely deleted, all data stored within it is completely destroyed and cannot be recovered. Ensure this does not impact your business.      </div>
      

<span id="of82v9IT"></span>
## Completely destroy

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">After the instance is completely deleted, all data stored within it is completely destroyed and cannot be recovered. Ensure this does not impact your business.</div>


* <div data-tips="true" data-tips-type="warning">If you have enabled the log audit feature, the associated TLS <code>project</code> and <code>topic </code>are also deleted when you permanently delete the instance.</div>


1. Log in to the [CR console](https://console.byteplus.com/cr).

2. Select the target region in the top navigation bar.

3. In the left navigation bar, click **Instance list \> Standard instance**.

4. In the **Actions** column on the right side of the target instance, click `···` \> **Completely destroy**.

5. On the secondary confirmation page, enter the verification information as prompted, and click **Completely destroy** to immediately destroy the instance.
