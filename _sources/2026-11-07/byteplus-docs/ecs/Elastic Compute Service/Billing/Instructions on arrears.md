---
title: "Instructions on arrears"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Arrears"
---

This topic describes the impact of arrears on instances and associated resources, as well as the procedures for handling arrears, to help you manage your resources.  [How to view available balance?](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-2)

<span id=".5qyg6LS55b2x5ZON"></span>
## Impact of arrears

<span id=".5oyJ6YeP6K6h6LS55a6e5L6L"></span>
### Pay\-as\-you\-go instance

When your account is in arrears, your resources will enter a retention period, with usage being limited. Once the retention period expires, your resources will be forcibly reclaimed and cannot be recovered. To ensure uninterrupted use of ECS resources, [settle overdue bills](https://docs.byteplus.com/en/docs/ecs/Arrears#.57uT5riF6LSm5Y2V) within the specified period (before the resources are forcibly reclaimed).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When your account is in arrears, you will not be able to create instances, change instance type, or change operating system.</div>


Once your account is in arrears, the running and billing status of the ECS instance changes as shown in the following chart.

**Instructions on resource release due to arrears**


* Stopping time: On the 15th day after your account is in arrears.

   > After the stop, the status of the Pay\-as\-you\-go instance changes to "Stopped". In the "Billing method" column, "Stopped" is displayed.   
   

* Release time: On the 30th day after your account is in arrears.

   Regardless of whether your instance resources are suspended or released, you are required to pay the generated outstanding bills.


**Instructions on resource status during arrears**


|Resource type |Post\-arrears duration ＜ 15 days |15 days ≤ Post\-arrears duration ＜ 30 days |Post\-arrears duration ≥ 30 days |
|---|---|---|---|
|Compute resources (vCPU and memory) |Compute resources are retained and billing continues.<br><br>The following features are unavailable:<br><br><br>* Create an instance<br><br>* Changing an instance type<br><br>* Changing billing method from Pay\-as\-you\-go to Subscription<br><br>* Change the operating system |For instance type families that support [Economical Mode](https://docs.byteplus.com/en/docs/ecs/Economical-mode-for-pay-as-you-go-instances), the resources will be released and billing stops, regardless of whether Economical Mode is enabled.<br><br>The following features are unavailable:<br><br><br>* Create an instance<br><br>* Changing an instance type<br><br>* Changing billing method from Pay\-as\-you\-go to Subscription<br><br>* Changing operating system<br><br>* Starting or restarting instance |The resources will be forcibly released, and all associated configurations and data will be permanently deleted and cannot be recovered. |
|Image |The image is retained, with limited use. |The image is retained, with limited use. |The image is retained, with limited use. |
|Local volume |The local volume and the data in it are retained. |Local volumes are retained, but the data in them may be released at any time. |The resources will be forcibly released, and all associated configurations and data will be permanently deleted and cannot be recovered. |
|Elastic Block Storage |The system volume, data volume, and the data in them are retained. |The system volume, data volume, and the data in them are retained. |The resources will be forcibly released, and all associated configurations and data will be permanently deleted and cannot be recovered. |
|Snapshot |The snapshot data is retained. |The snapshot data is retained. |The resources will be forcibly released, and all associated configurations and data will be permanently deleted and cannot be recovered. |
|EIP |The EIP applied is retained.<br><br>Disassociation is supported, and you can associate an active EIP. |The EIP applied is retained.<br><br>You can dissociate the EIP, but the bandwidth will be limited to 1 Kbps. |EIP is forcibly disassociated. |


<span id=".5YyF5bm05YyF5pyI5a6e5L6L"></span>
### Subscription instances

If your account is in arrears, you can still use the Subscription ECS resources and volumes you have purchased. However, you cannot perform cost\-related operations, such as purchasing new instances, upgrading instance configuration, or renewal. Before you perform these operations, you need to settle all arrears under your account.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">After a Subscription instance is stopped due to arrears, if the overdue bill is settled and the instance is renewed and recovered, the new billing cycle starts from the expiration date of the previous cycle, rather than the recovery date. For example: If the instance expiration date is June 30, and you complete renewal and recovery for 1 month on July 5, the new cycle is June 30 to July 30, not July 5 to August 5.</div>


<span id=".5p-l55yL5qyg6LS56YeR6aKd"></span>
## Viewing outstanding amount


1.   Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the top menu bar, click "Billing \> Overview" to go to the billing center. On the page that appears, you can view the outstanding amount. On this page, you can also enable the "Available balance alert". After you do this, the system will send a notification when the available balance is less than the alert threshold.  For more information, refer to [Billing overview](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-2).


<span id=".57uT5riF6LSm5Y2V"></span>
## Bill settlement

If your account is in arrears, your instance may be stopped. To avoid interruption to your services, please recharge and settle overdue bills in a timely manner. 

After you settle overdue bills, the running status of instances will be as follows:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Regardless of whether you make a renewal before or after the suspension caused by arrears (2 hours after your account is in arrears), the instance status after settlement will be the same as that before the arrears.</div>


* <div data-tips="true" data-tips-type="tip">Instance type families that support <a href="https://docs.byteplus.com/en/docs/ecs/Economical-mode-for-pay-as-you-go-instances">Economical Mode</a> may fail to start due to insufficient stock when restarted. For details, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Economical-mode-for-pay-as-you-go-instances#.6IqC55yB5YGc5py65ZCO6LWE5rqQ5oOF5Ya1">Instructions on resource status after Economical Mode is enabled</a>.</div>




|Billing method |No arrears |Upon arrears |Stopped due to arrears |After recharge |
|---|---|---|---|---|
|Pay\-as\-you\-go instance |In service |In service |Stopped |In service |
||Normal Mode |Normal Mode |Stopped |Normal Mode |
||Economical Mode |Economical Mode |Stopped |Economical Mode |
|Subscription instances |In service |In service |Normal Mode |In service |
||Normal Mode |Normal Mode |Normal Mode |Normal Mode |
