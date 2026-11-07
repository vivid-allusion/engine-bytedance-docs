---
title: "Change from Subscription volumes to Pay-as-you-go volumes"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Converting-from-subscription-volumes-to-pay-as-you-go"
---

Volumes support two billing methods: Pay\-as\-you\-go and Subscription. You can change the billing method of your volume based on your business needs. This topic describes how to change a Subscription volume to Pay\-as\-you\-go.

&nbsp;

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This topic describes only the prerequisites and procedure for changing a Subscription volume to Pay\-as\-you\-go. A Subscription system volume cannot be changed separately; it must be changed together with its associated ECS instance. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Converting-from-subscription-to-pay-as-you-go">Changing billing method from Subscription to Pay\-as\-you\-go</a>.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Before proceeding, ensure that your Subscription volume meets the following requirements:


* The volume status is **Attached**, and its associated instance status is **Running**.

* Your Subscription instance has not expired.

* The sum of your BytePlus account cash balance and coupon values is at least USD 100. If your balance is too low, please top up your account first.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Considerations


* You can change the billing method for multiple volumes in batches, up to 320 volumes at a time.

* After you change the billing method of your volume from Subscription to Pay\-as\-you\-go, the platform will deduct the amount used and refund the remaining actual payment amount (the portion paid in cash, excluding the amount deducted with coupons) to your BytePlus account balance. Note that used coupons cannot be refunded.

   For the detailed rules for calculating the refund amount after a change from Subscription to Pay\-as\-you\-go, refer to Instructions on unsubscription.

* After the billing method of a Subscription volume is changed to Pay\-as\-you\-go, the volume attribute "Whether to be deleted when the instance is deleted" stays the same as before the change.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If your volume is a Subscription volume created with an ECS instance, after you change it to Pay\-as\-you\-go, it will not be deleted with the instance.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If your volume is a Subscription volume created separately and then associated with an ECS instance, after you change it to Pay\-as\-you\-go, it will be deleted with the instance by default.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To set the volume attribute "Whether to be deleted when the instance is deleted", refer to <a href="https://docs.byteplus.com/en/docs/ecs/Modify-volume-attribute">Modifying volume attributes</a> for details.   </div>
   


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the[ ECS console](https://console.byteplus.com/ecs/instance).

2. In the top menu bar, select the project and region of the target volume.

3. In the left\-side navigation pane, click "Storage \> Volumes".

4. On the Volumes page, change the billing method based on your needs.

   * Change for a single volume: Locate the Subscription volume whose billing method you want to change. In the Actions column, select "··· \> Switch to Pay\-as\-you\-go".

   * Change for multiple volumes: Select multiple Subscription volumes whose billing methods you want to change. In the lower\-left corner of the volume list page, click "··· \> Switch to Pay\-as\-you\-go".

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can change the billing methods for up to 320 volumes at a time.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Note that if you select volumes with different billing methods, you cannot change from Subscription to Pay\-as\-you\-go.      </div>
      

5. After you confirm the volume information, check "I have read and agree Elastic Compute Service Terms of Service.".

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Make sure the sum of your account cash balance and coupon values is at least USD 100. Otherwise, the billing method change fails.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you change the billing method for volumes in a batch, you can cancel the operation for a specific volume. To do so, on the instance confirmation page, click "Remove \> Confirm" to the right of the target volume to complete the cancellation.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You cannot remove all selected volumes on the instance information confirmation page.   </div>
   

6. Click "Confirm order" to complete the payment and change the billing method.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Use the following methods to confirm whether the volume billing method has changed:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Success: On the "Order management" page, an order with the Change config type is generated. The order will be in the "<strong>Refunding</strong>" state, and the remaining unconsumed subscription duration will be refunded based on the actual payment. Then, the refund process is completed.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Failure: On the "Order management" page, an order with the Change config type and a "<strong>Refund failed</strong>" status is generated.   </div>
