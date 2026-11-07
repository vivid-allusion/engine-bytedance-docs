---
title: "Elastic Scheduled Instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Elastic_Scheduled_Instances"
---

Elastic Scheduled Instances (ESI) are pay\-as\-you\-go instances that support advance reservation and automatic delivery at the scheduled time. They are applicable for scenarios that require flexibility and ensure stable supply of resources. This topic describes the resource delivery methods and fee settlement rules for ESI.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For information on the operation process, applicable scenarios, limits, and user guide for ESI, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Elastic_Scheduled_Instances_Overview">Elastic Scheduled Instances (ESI) overview</a>.</div>


* <div data-tips="true" data-tips-type="tip">For ESI, a <a href="https://docs.byteplus.com/en/docs/ecs/Elastic_Scheduled_Instances#.6K6h6LS5">minimum 1\-hour consumption policy</a> is implemented. Regardless of whether the instance is released within the first hour after creation, a one\-hour bill will be issued and the fee will be charged. If the ESI is used for more than 1 hour, billing is based on your actual usage.</div>



<span id=".6aKE57qm5ZKM5Lqk5LuY"></span>
## Reservation and delivery

You can reserve an ESI **1–8 hours in advance (China (Beijing) region only)**  or **3–8 hours in advance (China (Shanghai) and China (Guangzhou) regions)** . When reserving, you are required to specify a delivery time period (10 minutes as a time period). For example, the current time is 17:42, the earliest delivery time period in the China (Beijing) region is 18:50\-19:00, which is 1 hour later. The latest delivery time period is 01:40\-01:50 (+1 day), which is 8 hours later.

After you have reserved an ESI, the system will generate an order for this purchase within the resource delivery time period and automatically creates an ESI. Once the instance is created, billing based on the ESI price starts.

<span id=".5Lu35qC85ZKM6K6h6LS56KeE5YiZ"></span>
## Prices and billing rules

<span id=".5Lu35qC8"></span>
### Prices


* Compared with Pay\-as\-you\-go, ESI allows you to save approximately 27% of the costs of compute resources (vCPU and memory). The fees for storage and network are the same as Pay\-as\-you\-go prices. The billing rules are as follows:

   * For billing rules for system volume and data volume, refer to [Pay-as-you-go](https://docs.byteplus.com/en/docs/ecs/Pay-as-you-go).

   * Network: For billing rules of EIP, refer to [EIP pay-as-you-go](https://docs.byteplus.com/en/docs/eip/Pay-as-you-go).

* The prices of ESIs vary based on specification. Please refer to the prices displayed on the ESI purchase page in the [ECS console](https://console.byteplus.com/ecs/buy?).

* Reserved Instances (RI) can not be used to deduct the costs of compute resources (vCPU and memory) for ESI.


<span id=".6K6h6LS5"></span>
### Billing rules

During the use of ESI, you need to pay the following fees:


* **Actual usage duration < 1 hour**: The 1\-hour minimum consumption policy is implemented. If the instance is released within 1 hour after creation, a bill will be issued and fee will be charged based on 1 hour of usage. For details, please refer to [Fee settlement example](https://docs.byteplus.com/en/docs/ecs/Elastic_Scheduled_Instances#.6LS555So57uT566X56S65L6L).

* **Actual usage duration ≥ 1 hour**: The 1\-hour minimum consumption policy is not applicable. Billing is done per second based on actual usage time, and a bill is issued hourly.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Actual usage duration: The duration from when the ESI is successfully created to when it is released. Billing ends after the instance is released.</div>


* <div data-tips="true" data-tips-type="tip">Instance release: ESI is not released automatically (except for resources release due to arrears). You can manually <a href="https://docs.byteplus.com/en/docs/ecs/Delete_Elastic_Scheduled_Instances">delete the instance</a> after business ends.</div>


* <div data-tips="true" data-tips-type="tip">Bill issued hourly: Billing for ESI is settled every hour (UTC+8). After this, the next settlement cycle starts. If the available amount in your account (including account balance and vouchers) is less than the outstanding bill, you will receive a notification via SMS or email regarding insufficient balance.</div>



<span id=".6LS555So57uT566X56S65L6L"></span>
## Fee settlement example

Assuming the price of an ESI is 1.2 USD/hour, the corresponding consumption in different scenarios is shown in the figures below.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Since a 1\-hour minimum consumption policy is implemented for ESI, two bills based on actual usage and minimum consumption are issued:</div>



* <div data-tips="true" data-tips-type="tip">[Consumption\-Minimum] bill: Records the cost for minimum consumption due to the usage duration not reaching 1 hour limit for Elastic Scheduled Instances. Minimum consumption = 60 minutes \- actual usage.</div>


* <div data-tips="true" data-tips-type="tip">[Consumption\-Usage] bill: Records the actual usage of the instance and the corresponding cost.</div>



<div data-tips="true" data-tips-type="tip">For details on bills, please refer to <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-bill-details">Bill management</a>.</div>


**Scenario 1: Actual usage duration is less than 1 hour and does not go beyond 1 settlement cycle, involving minimum consumption.** 

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ec41a7dda6c1b30673a43fcfecc2ec53.png) </span>

**Scenario 2: Actual usage usage duration is less than 1 hour but spans 2 settlement cycles, involving minimum consumption.** 

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_81db2c1f13cb00d79c7f44251d16faec.png) </span>

**Scenario 3: Actual usage duration exceeds 1 hour, not involving minimum consumption.** 

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_243f3325011b7745540b6b1373ae6cce.png) </span>
