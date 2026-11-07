---
title: "Instructions on renewal and unsubscription"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Renewal-and-unsubscription"
---

This topic describes how to renew and unsubscribe Elastic Compute Service (ECS) instances.

<span id=".57ut6LS56K-05piO"></span>
## Instructions on renewal

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When you renew a subscription\-based instance, the associated image and mounted subscription\-based volumes are renewed accordingly. You can select whether to renew the associated subscription\-based Elastic IP (EIP).</div>


* <div data-tips="true" data-tips-type="tip">On the Instances page of the ECS console, you can view the renewal method (manual renewal or auto renewal) in the "Renewal method" column.</div>



<span id=".5omL5Yqo57ut6LS5"></span>
### Manual renewal


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the top menu bar, select the region and project of the target instance.

3. In the left\-side navigation pane, select "Instances & Images \> Instances".

4. On the Instances page, complete renewal by referring to the following methods.

   * Single renewal: Click "··· \> Cost \> Renew" on the right side of the target instance.

   * Batch renewal: On the Instances page, select one or more subscription\-based instances to be renewed and click the "Renew" button at the bottom.

      > You can select up to 100 subscription\-based instances at a time.      
      

5. You will be redirected to the renewal management page. Review and confirm the instance information. When you renew an ECS instance, specify whether to renew the associated subscription\-based EIP.

6. Select a renewal cycle, and check the "I have read the renewal instructions and agree to do the above", and click "Pay".

7. Click "Next step" to submit the payment information. Then, click "Pay" to complete the payment.

   > If you have available coupons, ​select them for payment deduction.   
   

<span id=".6Ieq5Yqo57ut6LS5"></span>
### Automatic renewal

You can select the "Enable automatic renewal" option when subscribing to a subscription\-based instance or enable automatic renewal before the instance expires. For detailed steps, refer to [Automatic renewal](https://docs.byteplus.com/en/docs/byteplus-platform/docs-auto-renewal-rules).

Once automatic renewal is enabled, the system automatically deducts the renewal fee from your account balance before the instance expires. If you have coupons in your account, they will be prioritized for the renewal.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For any instance with automatic renewal enabled, you can also manually renew it at any time. Manual renewal does not affect automatic renewal. The system will deduct fees 7 days before the updated expiration date.</div>


* <div data-tips="true" data-tips-type="tip">For expired instances, you can not enable or modify automatic renewal.</div>



<span id=".6YCA6K6i6K-05piO"></span>
## Instructions on unsubscription

If you no longer require a subscription\-based instance, you can unsubscribe it to reduce costs.

<span id=".5YeG5aSH5bel5L2c"></span>
### Preparations

Before unsubscription, make sure that the data you need is not stored in the subscription\-based instance you are about to unsubscribe, or that the data you need has been [backed up](https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration) or [migrated](https://docs.byteplus.com/en/docs/smc/Same-Account-or-Cross-Account-migration-of-ECS).

<span id=".5rOo5oSP5LqL6aG5"></span>
### Usage notes


* After you unsubscribe a subscription\-based instance, you can manually delete the instance during the retention period. For more information, refer to [Deleting instance](https://docs.byteplus.com/en/docs/ecs/Deleting-ECS-instances).

* To avoid data loss due to accidental unsubscription, the related resources will be retained for a certain period. During the retention period, the resources awaiting release will not incur charges. See the following detailed rules:

   
   |**Resources** |**After instance unsubscription** |
   |---|---|
   |vCPU, memory, and local volume |Released after 24\-hour retention. |
   |Image |* Custom images will be retained.<br><br>* Public images and marketplace images are unsubscribed together with the instances. |
   |Subscription\-based volume (including system volume) |Released after 15 days of retention. |
   |Pay\-as\-you\-go volume |Whether the volume is set to be deleted together with the instance:<br><br><br>* If yes, it will be released together with the instance after 24 hours of retention.<br><br>* If no, it will be automatically unmounted after 24 hours of retention. |
   |Subscription\-based EIP: |* The EIP associated with the primary private IP address of the primary network interface of the instance. Whether it is set to be unsubscribed when the ECS instance is unsubscribed:<br><br>   * If yes, it will be released immediately.<br><br>   * If no, it will be automatically disassociated after 24 hours of retention.<br><br>* The EIP associated with the secondary private IP address of the primary network interface of the instance or the EIP associated with the secondary network interface, they will be automatically disassociated after 24 hours of retention. |
   |Pay\-as\-you\-go EIP |* The EIP associated with the primary private IP address of the primary network interface of the instance: Whether it is set to be released together with the ECS instance when you [buy the ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) or [associate the EIP with instance](https://docs.byteplus.com/en/docs/eip/Associating-Cloud-Resources-with-an-EIP):<br><br>   * If yes, it will be released together with the instance after 24 hours of retention.<br><br>   * If no, it will be automatically disassociated after 24 hours of retention. You can still associate it with other instances.<br><br>* The EIP associated with the secondary private IP address of the primary network interface of the instance or the EIP associated with the secondary network interface, they will be automatically disassociated after 24 hours of retention. |
   |Secondary network interface |Whether the network interface is set to be deleted when the ECS instance is unsubscribed:<br><br><br>* If yes, it will be released together with the instance after 24 hours of retention.<br><br>* If no, it will be automatically unmounted after 24 hours of retention. You can still mount the secondary network interface to other instances. |
   

* Unsubscribed subscription\-based instances can not be restored directly. Once the retention period expires, for example, if you unsubscribe a Subscription\-based instance and do not renew it within 15 days after the unsubscription, the Subscription\-based volume will be released. After that, the data is irrecoverable and you cannot restore the instance through renewal. If you want to continue using ECS, we recommend you take the following measures:

   * Create a new instance: Purchase a new ECS instance and select appropriate configuration based on your business requirements. For more information, refer to [how to purchase instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

   * Restore data:

      * Before your volume is released, we recommend that you create a snapshot of the volume and then use the snapshot to restore data to the volume of your new instance. For more information, refer to 

      * If the data volumes of the original instance are set as not being deleted with the instance and being retained after unsubscription, you can mount the data volumes on the new instance for use.


<span id=".6YCA6K6i57G75Z6L"></span>
### Unsubscription type

For subscription\-based instances, **non\-7\-day refund** is supported. For more information, refer to [instructions on non-7-day refund policy](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management#ii-non-seven-day-refund-policy).

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">The platform reserves the right to reject unsubscription requests that appear to be suspicious or malicious.</div>


&nbsp;

<span id="M3mvArFC"></span>
### Procedure 


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the top menu bar, select the region and project of the target instance.

3. In the left\-side navigation pane, select "Instances & Images \> Instances".

4. On the Instances page, complete unsubscription by referring to the following methods.

   * Single unsubscription: On the right side of the target instance, hover on the ellipsis icon (···) and select "Cost \> Unsubscribe".

   * Batch unsubscription: Select one or more subscription\-based instances, select "··· \> Unsubscribe" at the bottom of the page.

      >  Up to 100 Subscription instances can be selected at a time.      
      

5. You are redirected to the unsubscription management page. Confirm the information of the instances, volumes, images, and other relevant resources. When you unsubscribe an ECS instance, specify whether to unsubscribe the subscription\-based EIP associated with it.

6. Select "I have read the unsubscription notice and agreed on the operations above", and click the "Confirm unsubscription" button. Then, check the unsubscription details (unsubscribed resources and amount).

7. Click "Confirm" to complete the procedure.


<span id=".5bi46KeB6Zeu6aKY"></span>
## FAQ


* [Is renewal required for pay-as-you-go instances?](https://docs.byteplus.com/en/docs/ecs/Billing-FAQs#.5oyJ6YeP6K6h6LS55a6e5L6L6ZyA6KaB57ut6LS55ZCX77yf)

* [How is the refund for subscription instances settled?](https://docs.byteplus.com/en/docs/ecs/Billing-FAQs#.5YyF5bm05YyF5pyI5a6e5L6L6YCA6K6i6YeR6aKd5aaC5L2V57uT566X77yf)

* [After a subscription-based instance is unsubscribed, where will the refund be returned?](https://docs.byteplus.com/en/docs/ecs/Billing-FAQs#.5YyF5bm05YyF5pyI5a6e5L6L6YCA6K6i5ZCO77yM6YCA5qy-6L-U5Zue5ZOq6YeM77yf)

* [How do I renew a subscription-based instance that has been unsubscribed?](https://docs.byteplus.com/en/docs/ecs/Billing-FAQs#.5bey6L-b6KGM6YCA6K6i5pON5L2c55qE5YyF5bm05YyF5pyI5a6e5L6L5aaC5L2V6L-b6KGM57ut6LS577yf)
