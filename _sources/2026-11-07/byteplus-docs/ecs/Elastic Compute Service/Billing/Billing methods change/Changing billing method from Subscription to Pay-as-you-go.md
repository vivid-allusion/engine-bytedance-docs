---
title: "Changing billing method from Subscription to Pay-as-you-go"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Converting-from-subscription-to-pay-as-you-go"
---

This topic describes how to change your subscription instances to pay\-as\-you\-go instances. This way, you can flexibly manage your cloud resources.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Before proceeding, ensure that your subscription instance meets the following requirements:


* The instance is in the **Running** or **Stopped** status.

* Your subscription\-based instance has not expired. [How do I view expiration time?](https://docs.byteplus.com/en/docs/ecs/Expiration#.5p-l55yL5Yiw5pyf5pe26Ze0)


<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* You cannot change the billing method of an instance from Subscription to Pay\-as\-you\-go if the instance uses a Red Hat or SUSE public image provided by , or a marketplace image.

* After you change the subscription instance to a pay\-as\-you\-go instance, charges will be deducted based on pay\-as\-you\-go rules. Please ensure sufficient account balance to avoid service interruption due to arrears. If you no longer need the instance, [back up](https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration) your data and then release the instance on the console.

* If you have any orders that have not taken effect for the instance, a full refund will be made. However, for orders that have taken effect, only a partial refund will be provided.

* When you change the billing method of an instance, the billing method for its associated resources is also changed. Note that the billing method for mounted resources needs to be changed separately. For example, for the associated subscription\-based EBS volume and the image used by the instance, their billing method will be changed accordingly. For subscription\-based Elastic IP (EIP) attached to the instance, the billing method remains unchanged.

* You can select up to 20 instances for batch changing at a time.


<span id=".6YCA5qy-6K-05piO"></span>
## Refund instructions

After you change the billing method from Subscription to Pay\-as\-you\-go, the platform will deduct the amount used and refund the remaining actual payment amount (the portion paid by the user in cash, excluding the amount deducted with coupons) to your account balance. Note that used coupons can not be refunded.  

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure 


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the region and project where the target instance resides.

4. On the Instances page, change the billing method based on your needs.

   * Change for a single instance: Find the subscription instance for which you want to change the billing method. Click the ellipsis (···) icon in the Actions column, and select "Resource allocation \> Switch to pay\-as\-you\-go".

   * Change for multiple instances: Select one or more target instances, click the ellipsis icon, and select "Switch to pay\-as\-you\-go" at the top.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can select up to 20 instances for batch changing at a time.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Note that if you select instances with different billing methods, you can not change from subscription to pay\-as\-you\-go.   </div>
   

5. On the billing method change page, review the instance information. Follow the console instructions to review and confirm the legal agreements.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">During batch changing, if you want to cancel the change action for an instance, click "Remove" next to the target instance on the page.   </div>
   

6. Click "Confirm order" to complete the payment and change the billing method.


<span id=".5pON5L2c57uT5p6c"></span>
## Operation results


* Success: On the "Order management" page, an order with the **Change config** type is generated. The order will be in the "Refunding" state, and the remaining unconsumed subscription duration will be refunded based on the actual payment. Then, the refund process is completed.

* Failure: On the "Order management" page, an order with the **Change config** type and a "Refund failed" status is generated.


<span id=".55u45YWz5paH5qGj"></span>
## Related document

[ModifyInstanceChargeType - Change instance billing method](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceChargeType)
