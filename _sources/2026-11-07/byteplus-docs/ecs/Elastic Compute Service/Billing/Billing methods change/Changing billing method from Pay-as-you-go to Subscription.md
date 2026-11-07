---
title: "Changing billing method from Pay-as-you-go to Subscription"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Converting-from-pay-as-you-go-to-subscription"
---

Elastic Compute Service (ECS) allows you to change the billing method from pay\-as\-you\-go to subscription. This way, you can change pay\-as\-you\-go instances to long\-term stable subscription instances. By doing this, you can reserve resources in advance and reduce cost. This topic describes how to change pay\-as\-you\-go instances to subscription instances in the ECS console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The instance type is not discontinued from sale. For discontinued types, see the [instance type list](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types#.5a6e5L6L6KeE5qC85peP5YiX6KGo).

* The instance status is **Running** or **Stopped**.

* The billing method of the target instance is **Pay\-as\-you\-go** (except for spot instances and Elastic Scheduled Instances).

* The account has no outstanding fees. [How to view the arrears amount?](https://docs.byteplus.com/en/docs/ecs/Arrears#.5p-l55yL5qyg6LS56YeR6aKd)


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* When you change the billing method from pay\-as\-you\-go to subscription, the billing method for the system volume and images is automatically synchronized and changed.

* By default, data volumes are not changed to subscription. You must manually select the option during the billing change process to cover them.

* You can select up to 20 instances for batch changing at a time.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The cost displayed on the billing change page represents the payable amount for changing to subscription. Data volumes that are not changed to subscription will continue to be billed on a pay\-as\-you\-go basis.

* If the account has outstanding fees, you can not change the billing method to subscription. Click the "Go to top up" button and settle the bill. Then, try it again.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1.  Log on to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the region and project where the target instance resides.

4. On the Instances page, change the billing method based on your needs.

   * Single instance changing: Find the pay\-as\-you\-go instance for which you want to change the billing method. Click the ellipsis (···) icon in the Actions column, and select "Resource allocation \> Switch to subscription".

      You can also click the target instance name to enter the instance overview page. Then, in the billing information section, click the "Change billing method" button.

   * Batch changing: Select one or more target instances, click the ellipsis icon, and select "Switch to subscription" at the top.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can select up to 20 instances for batch changing at a time.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Note that if you select instances with different billing methods, you can not change from pay\-as\-you\-go to subscription.   </div>
   

5. Review the instance information and complete setting based on the prompts on the page.

   
   |Parameter |Description |
   |---|---|
   |Subscription duration |Set a subscription duration. If you want to make a batch change, you can set only one subscription duration for multiple instances. |
   |Auto renewal |Specify whether to enable auto renewal. This feature is disabled by default. |
   |Data volume |Specify whether to change pay\-as\-you\-go data volumes to subscription simultaneously. |
   

6. follow the console instructions to review and confirm the legal agreements.

7. Click "Confirm order". Complete the payment, the billing method is changed.


<span id=".5pON5L2c57uT5p6c"></span>
## Result


* Success: On the "Order management" page, an order with the **Change config** type is generated.

* Failure: On the "Order management" page, an order with the **Change config** type and a "Refunded" status is generated. The amount of unsubscribed services is automatically refunded.


<span id=".55u45YWz5paH5qGj"></span>
## Related document

[ModifyInstanceChargeType - Change instance billing method](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceChargeType)
