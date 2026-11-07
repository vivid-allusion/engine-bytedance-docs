---
title: "Instructions on expiration"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Expiration"
---

After a Subscription instance expires, the platform offers a retention period. During this period, you can [renew](https://docs.byteplus.com/en/docs/ecs/Renewal-and-unsubscription#.57ut6LS56K-05piO) or [unsubscribe](https://docs.byteplus.com/en/docs/ecs/Renewal-and-unsubscription#.6YCA6K6i6K-05piO) it based on your need for continuous use. If you do not perform any actions during the retention period, the resources associated with the instance will be forcibly released and are irrecoverable. This topic describes the impact to Subscription instances when they expire, as well as the procedures for handling resources after expiration.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you no longer require a Subscription instance after it expires, manually delete it during the retention period. For more information, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Deleting-ECS-instances">Deleting instance</a>.</div>


<span id=".5Yiw5pyf5b2x5ZON"></span>
## Impact of expiration

Once a Subscription instance expires, the status of the instances changes as shown in the following chart.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7c01dc3ff4f4ed3e52557f6fafa71ed0.png) </span>

<span id=".5Yiw5pyf6YeK5pS-6K-05piO"></span>
### Instructions on release after expiration


* Expiration time: 23:59:59 on the expiration date.

* Stopping time: 12 hours after expiration.

   > After the stop, the status of the Subscription instance changes to "Stopped". In the "Billing method" column, "Stopped" is displayed.   
   

* Release time: 15 days after expiration.


<span id=".5Yiw5pyf5ZCO6LWE5rqQ54q25oCB6K-05piO"></span>
### Instructions on resource status after expiration

The following table shows the resource status at different stages after expiration.


|Resource type |The expiration date ~ 12:00 noon of the next day |12 hours < Post\-expiration duration ≤ 15 days |Post\-expiration duration \> 15 days |
|---|---|---|---|
|Compute resources (vCPU and memory) |The compute resources are retained.<br><br>The following features are unavailable:<br><br><br>* Changing instance type<br><br>* Change the billing method from Subscription to Pay\-as\-you\-go<br><br>* Changing operating system |The compute resources are retained.<br><br>The following features are unavailable:<br><br><br>* Changing instance type<br><br>* Change the billing method from Subscription to Pay\-as\-you\-go<br><br>* Changing operating system<br><br>* Starting or restarting instance |The resources will be forcibly released, and all associated configurations and data will be permanently deleted and cannot be recovered. |
|Image |The image is retained, with limited use. |The image is retained, with limited use. |The image is retained, with limited use. |
|Local volume |The local volume and the data in it are retained. |The local volume and the data in it are retained. |The resources will be forcibly released, and all associated configurations and data will be permanently deleted and cannot be recovered. |
|Elastic Block Storage |The system volume, data volume, and the data in them are retained. |The system volume, data volume, and the data in them are retained. |Subscription volume is released, all associated configurations and data will be permanently deleted and cannot be recovered.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you have manually mounted a Pay\-as\-you\-go volume and set it to delete with the instance, this type of Pay\-as\-you\-go volume will also be released. If not set to delete with the instance, it will be automatically disassociated.</div><br> |
|EIP<br><br>(associated with the primary private IP address of the primary network interface of the instance) |The EIP applied is retained.<br><br><br>* You can dissociate an EIP.<br><br>* You can associate an active EIP. |The EIP applied is retained.<br><br>You can dissociate the EIP, but the bandwidth will be limited to 1 Kbps. |* Subscription EIP: Forcibly disassociated.<br><br>* Pay\-as\-you\-go EIP: Whether it is set to be released together with the ECS instance when you [buy the ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) or [associate the EIP with instance](https://docs.byteplus.com/en/docs/eip/Associating-Cloud-Resources-with-an-EIP):<br><br>   * If yes, it will be released together with the instance.<br><br>   * If no, it will be disassociated from the instance. You can still associate it with other instances. |
|EIP<br><br>(associated with the secondary private IP address of the primary network interface of the instance or associated with the secondary network interface of the instance) |The EIP applied is retained.<br><br><br>* You can dissociate an EIP.<br><br>* You can associate an active EIP. |The EIP applied is retained.<br><br>You can dissociate the EIP, but the bandwidth will be limited to 1 Kbps. |Forcibly disassociated. |


<span id=".5p-l55yL5Yiw5pyf5pe26Ze0"></span>
## View expiration time

You can view the expiration time of your Subscription instance by following these steps:


* On the Instances page, view the expiration time in the "Billing method" column.

* Click the instance name to enter the details page. In the ** Billing information** section, find the expiration time.


<span id=".57ut6LS5"></span>
## Renewal

If a subscription instance is not renewed after it expires, the resources will enter a retention period, and their usage will be restricted. Once the retention period expires, your resources will be forcibly reclaimed and cannot be recovered. To ensure uninterrupted usage of ECS resources, renew them within the specified period (before the resources are forcefully reclaimed). When renewing, you need to pay the fees that are due from the expiration time to the renewal time. For more information, refer to [Instructions on renewal](https://docs.byteplus.com/en/docs/ecs/Renewal-and-unsubscription#.57ut6LS56K-05piO).

After a renewal succeeds, the status of the Subscription instances is as shown in the table below.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Whether renewal is made before or after the expiration suspension (12 hours after expiration), the instance status after successful renewal is the same as that before the expiration.</div>


* <div data-tips="true" data-tips-type="tip">Upon service renewal and recovery, the new billing cycle starts from the expiration date of the previous cycle, rather than the recovery date. For example: If the instance expiration date is June 30, and you complete renewal and recovery for 1 month on July 5, the new cycle is June 30 to July 30, not July 5 to August 5.</div>




|Billing method |Before expiration |Upon expiration |Stopped upon expiration |After renewal |
|---|---|---|---|---|
|Subscription instances |In service |In service |Normal Mode |In service |
||Normal Mode |Normal Mode |Normal Mode |Normal Mode |


<span id=".5bi46KeB6Zeu6aKY"></span>
## FAQ

[For a Subscription instance I purchased at a discounted price, may I renew it at the same price when it expires?](https://docs.byteplus.com/en/docs/ecs/Billing-FAQs#.5rS75Yqo6LSt5Lmw55qE5YyF5bm05YyF5pyI5a6e5L6L77yM5Yiw5pyf5ZCO6L-Y5piv5Lul5ZCM5qC355qE5Lu35qC857ut6LS55ZCX77yf)

&nbsp;

&nbsp;

&nbsp;

&nbsp;
