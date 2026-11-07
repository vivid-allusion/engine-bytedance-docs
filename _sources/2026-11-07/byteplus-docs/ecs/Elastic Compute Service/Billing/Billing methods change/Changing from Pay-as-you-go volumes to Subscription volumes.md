---
title: "Changing from Pay-as-you-go volumes to Subscription volumes"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Changing-pay-as-you-go-volumes-to-subscription-volumes"
---

Volumes support two billing methods: Pay\-as\-you\-go and Subscription. You can change the billing method of Pay\-as\-you\-go data volumes associated with Subscription instances to Subscription based on your business needs.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The Pay\-as\-you\-go data volume whose billing method you want to change must be associated with a Subscription\-based instance that is running and has not expired.

* Your BytePlus account must not have overdue payments.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Considerations

A Pay\-as\-you\-go system volume can only be converted to a Subscription volume together with its associated ECS instance. For detailed steps, refer to [Change Pay-as-you-go to Subscription](https://docs.byteplus.com/en/docs/ecs/Converting-from-pay-as-you-go-to-subscription).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1.   

2. In the left\-side navigation pane, click "Volumes".

3. In the top menu bar, select the project and region of the target volume.

4. On the Volumes page, change the billing method based on your needs.

   * Change for a single volume: Locate the Pay\-as\-you\-go volume whose billing method you want to change. In the Actions column, select "··· \> Switch to Subscription".

   * Change for multiple volumes: Select multiple Pay\-as\-you\-go volumes whose billing methods you want to change. At the bottom of the page, select "··· \> Switch to Subscription".

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Change for multiple volumes is supported only for Pay\-as\-you\-go volumes that are associated with the same Subscription instance.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If you select volumes with different billing methods or associated with different instances, you cannot change their billing methods.      </div>
      

5. After you confirm the volume information, read and select "Elastic Compute Service Terms of Service".

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you change the billing method for volumes in a batch, you can cancel the operation for a specific volume. To do so, on the confirmation page, click "remove" to the right of the target volume to complete the cancellation.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">On the information confirmation page, keep at least one volume for the billing method change. You cannot remove all selected volumes on this page.   </div>
   

6. Click "Confirm order".

7. On the "Confirm order information" page, confirm volume details and the amount, and click "Next step".

8. On the "Submit payment information" tab, select the payment method, and click the "Pay" button.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If your account has overdue payments, you cannot change the billing method to Subscription. Please settle your bills and try again.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After payment completes, click "Go to console" to verify the volume billing method change.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After the billing method of a volume is changed from Pay\-as\-you\-go to Subscription, the volume expires at the same time as its associated instance.   </div>
